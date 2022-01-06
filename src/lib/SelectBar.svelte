<script>

	export let available = false;

</script>

<div class="bottom-section"></div>

<nav class="navbar navbar-expand-md navbar-dark fixed-bottom bg-dark">

    <ul class="navbar-nav ml-auto mr-auto">
        <li class="nav-item">
            <button class:disabled={available!==true} class="btn-sauce btn btn-outline-primary my-2 my-sm-0" type="submit" onclick="sauce()">Match !</button>
        </li>
    </ul>
    <ul class="navbar-nav">
        <li class="nav-item">
            <button  class:disabled={available!==true} class="btn-reset btn btn-outline-secondary my-2 my-sm-0" onclick="reset()">Reset</button>
        </li>
    </ul>
</nav>