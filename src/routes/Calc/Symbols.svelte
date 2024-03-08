<script>
    import {count} from './stores.js';
    import {onDestroy, onMount} from "svelte";

    function addArithmetic(value) {
        count.update(n => n + ' ' + value + ' ');
    }

    const symbols = ['+', '-', '*', '/']

    function handleKeydown(event) {
        const key = event.key;
        if (symbols.includes(key)) {
            addArithmetic(key);
        }
    }

    onMount(() => {
        window.addEventListener('keydown', handleKeydown);
    });

    onDestroy(() => {
        window.removeEventListener('keydown', handleKeydown);
    });
</script>


<div class="arithmeticSymbols">
    {#each symbols as symbol}
        <div class="arithmeticSymbolsDivision">
            <button on:click={() => addArithmetic(symbol)}>{symbol}</button>
        </div>
    {/each}
</div>
<style>
    .arithmeticSymbols {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
        padding: 10px;
    }

    .arithmeticSymbols button {
        width: 45px;
        height: 45px;
        background-color: #5BA199;
        color: white;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        cursor: pointer;
        border: none;
        border-radius: 4px;
    }

    .arithmeticSymbolsDivision {
        border-right: 8px;
        padding: 10px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>
