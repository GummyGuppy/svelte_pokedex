<script>
    export let name, img
</script>

<div class="w-1/2 h-3/4 bg-red-200 rounded-xl">
    <h1>{name}</h1>
    {img}
</div>





<style>

    h1::first-letter {
        text-transform:capitalize;
    }

</style>