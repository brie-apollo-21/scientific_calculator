<script>
    export let text;
    export let func;
</script>

<style>
    button {
        border-bottom-width: 0;
        border-right-width: 0;
        border-left-width: 0;
    }
    @media (min-width: 640px) {
        button {
            border-bottom-width: 1.5px;
            border-right-width: 1.5px;
            border-left-width: 1.5px;
        }
    }
</style>

<button style="" class="aspect-square sm:aspect-auto from-slate-700 to-slate-800 bg-gradient-to-bl shadow-2xl lg:shadow-none lg:hover:shadow-xl sm:border-x-slate-500 sm:border-b-slate-500 border-x-transparent border-b-transparent border-opacity-75 lg:active:shadow-none active:opacity-90 duration-150 flex justify-center rounded-md h-min w-full sm:mx-2 m-1" on:click={func}>
    <p style="font-family: 'Inter Tight', sans-serif;" class="my-auto text-slate-100 text-xl sm:text-base md:text-sm p-3 w-full text-center align-middle">{@html text}</p>
</button>