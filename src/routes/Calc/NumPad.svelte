<script>
    import {onDestroy, onMount} from 'svelte';
    import {count} from './stores.js';
    import {answer} from './Answer.js'
    import {get} from "svelte/store";

    function addNum(value) {
        count.update(n => n + value);
    }

    function backSpace() {
        const line = get(count);

        if (line.charAt(line.length - 1) === " ") {
            count.set(line.toString().slice(0, -2));
        } else {
            count.set(line.toString().slice(0, -1));
        }

        if (line.length <= 1) {
            answer.set('0');
        }
    }

    const numbers = Array.from({length: 9}, (_, i) => i + 1);

    function handleKeydown(event) {
        const key = event.key;
        const num = parseInt(key, 10);

        console.log(key);
        if (!isNaN(num) && num >= 0 && num <= 9) {
            addNum(num);
        } else if (key === ".") {
            addNum(".");
        } else if (key === "Backspace") {
            backSpace();
        }
    }

    onMount(() => {
        window.addEventListener('keydown', handleKeydown);
    });

    onDestroy(() => {
        window.removeEventListener('keydown', handleKeydown);
    });
</script>

<div class="numPad">
    {#each numbers as number}
        <div class="grid-item">
            <button on:click={() => addNum(number)}>{number}</button>
        </div>
    {/each}
    <div class="grid-item second">
        <button on:click={() => addNum(0)}>.</button>
    </div>
    <div class="grid-item second">
        <button on:click={() => addNum(0)}>0</button>
    </div>
    <div class="grid-item second">
        <button on:click={backSpace}>C</button>
    </div>
</div>


<style>
    .numPad {
        display: grid;
        grid-gap: 1px;
        grid-template-columns: 1fr 1fr 1fr;
    }

    .numPad .grid-item {
        border: white;
        font-size: 20px;
        color: white;
        border-right: 8px;
        padding: 10px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .numPad .grid-item button {
        width: 50px;
        height: 50px;
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
</style>