<script>
    import Navbar from "../lib/Navbar.svelte";
    import Waifu from "../lib/Waifu.svelte";
    import SelectBar from "../lib/SelectBar.svelte";
    import Composition from "../lib/Composition.svelte";

    let french = false;
    let url = '/data/db.json';

    let allValks = [];
    let types = [];

    const fetchData = (async () => {
        const response = await fetch(url);
        let database = await response.json();
        allValks = database.valks;

        allValks.forEach(v => v.selected = false);

        types = database.types;
        return database;
    })()

    function getType(index) {
        if (index >= types.length || index <= 0) {
            return "";
        } else {
            return types[index];
        }
    }

    let selectedValk = [];
    let matchAvail = false;

    let compos = [];

    function switchValk(index) {
        // Look for valk in our selection
        let valkIndex = selectedValk.indexOf(index);

        // If already selected, deselect it !
        if (valkIndex > -1) {
            selectedValk.splice(valkIndex, 1);
            selectedValk = selectedValk;

            allValks[index].selected = false;
            return false;
        }

        // remove if too much items

        while (selectedValk.length >= 3) {
            let oldValkIndex = selectedValk.pop();
            allValks[oldValkIndex].selected = false;
        }

        // append to array
        selectedValk = [index, ...selectedValk];

        allValks[index].selected = true;

        return true;
    }

    function resetValks() {
        selectedValk.map(s => switchValk(s));
        allValks.map(e => e.selected = false);
        selectedValk = [];
        matchAvail = false;
    }


    function doSelect(index) {
        if (switchValk(index)) {
            let valk = allValks[index];

            console.log(valk.abbreviation);
        } else {
            allValks[index].selected = false;
        }

        matchAvail = selectedValk.length === 3;

        console.log("Selected : " + selectedValk.map(e => {
            return allValks[e].abbreviation
        }).join(" "));
    }

    function sauce() {
        console.log("Selected : " + selectedValk.map(e => {
            return allValks[e].abbreviation
        }).join(" "));

        compos = [{
            'type': 'Abyss'
        }, {
            'type': 'Abyss'
        }, {
            'type': 'MA'
        }]
    }

</script>


<Navbar />

{#await fetchData}
    <p>... Loading</p>
{:then data}
    <div class="container-fluid-lim">
        <div class="row waifus-list">
        {#each allValks as valk, index}
            <div class="col col-waifu-card" data-waifu="{JSON.stringify(valk)}">
                <Waifu
                        bind:selected="{valk.selected}"
                        type="{getType(valk.type)}"
                        valk="{valk.valk}"
                        role="{valk.role}"
                        utilisation="{valk.utilisation}"
                        farm="{valk.farm}"
                        battlesuit="{french ? valk.battlesuitFR : valk.battlesuit}"
                        abbreviation="{valk.abbreviation}"
                        on:click={() => doSelect(index)} />
            </div>
        {/each}
        </div>

    </div>

    <SelectBar />

    <div class="bottom-section"></div>

    <nav class="navbar navbar-expand-md navbar-dark fixed-bottom bg-dark">

        <ul class="navbar-nav ml-auto mr-auto">
            <li class="nav-item">
                <button class:disabled={matchAvail!==true} class="btn-sauce btn btn-primary my-2 my-sm-0" type="submit" on:click={sauce}>Match !</button>
            </li>
        </ul>
        <ul class="navbar-nav">
            <li class="nav-item">
                <button  class:disabled={matchAvail!==true} class="btn-reset btn btn-outline-secondary my-2 my-sm-0" on:click={resetValks}>Reset</button>
            </li>
        </ul>
    </nav>

    {#if compos.length > 0}
        <div id="compo" class="container-fluid">
            <h2>Compositions</h2>
            <h3>Abyss</h3>
            <ul class="list-unstyled compos-list">
            {#each compos as compo, index}
                {#if compo.type === 'Abyss'}
                    <li class="compo-item" data-compo="{JSON.stringify(compo)}">
                        <Composition compo={compo}/>
                    </li>
                {/if}
            {/each}
            </ul>

            <h3>MA</h3>
            <ul class="list-unstyled compos-list">
            {#each compos as compo, index}
                {#if compo.type === 'MA'}
                    <li class="compo-item" data-compo="{JSON.stringify(compo)}">
                        <Composition compo={compo}/>
                    </li>
                {/if}
            {/each}
            </ul>
        </div>
    {:else}
        <p>Please select 3 valks to start matchmaking !</p>
    {/if}

{:catch error}
<p>An error occurred!</p>
{/await}

<style>
    .compos-list {
        display: flex;
        /*justify-content: space-around;*/
        flex-wrap: wrap;
        overflow: scroll;
    }

    .compo-item {
        min-width: 700px;
        flex-shrink: 0;
        flex-grow: 1;
        margin: 0 16px;
    }

    .waifus-list {
        place-content: center;
    }

    .col-waifu-card {
        flex-grow: 0;
    }
</style>
