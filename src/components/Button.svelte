<script>
    export let fn, title
</script>

<button class="bg-gradient-to-r active:bg-gradient-to-l from-slate-200 to-blue-300 
    py-2 px-6 rounded-lg border-blue-300 border-2 active:outline active:outline-2 shadow-lg
    active:outline-blue-400 active:outline-spacing-2"
    on:click={fn}>{title}</button>

