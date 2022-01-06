<script>
	
	export let selected = false;

	export let type = "";
	export let valk;
	export let battlesuit;
	export let abbreviation = "";
	export let role;
	export let utilisation;
	export let farm;

	export let image_url = "img/card/" + abbreviation + ".png";
	
</script>


<div class:checked={selected===true} class="waifu-card card {type} valk-{abbreviation}" on:click> <!-- on:click(doSelect(abbreviation)) -->
    <span class="card-img-type">
        <i class="waifu-image-card" style="background-image: url({image_url});" alt="{battlesuit}"></i>
        <span class="tag-search">{abbreviation}</span>
        <span class="tag-search">{valk}</span>
        <span class="rank rank-0"></span>
   </span>

    <div class="card-body row">
        <span class="col waifu-name">{battlesuit} ({abbreviation})</span>
    </div>

</div>

<style>
    .selected {
        font-weight: bolder;
    }

    .card-body {
        line-height: 12px;
        min-height: 40px;
        text-align: center;
        align-content: center;
    }

    .waifu-name {
        padding-right: 0;
        padding-left: 0;
        overflow: visible;
    }
</style>