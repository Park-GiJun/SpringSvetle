<script>
    import {count} from './stores.js';
    import {answer} from "./Answer.js";
    import {onDestroy, onMount} from "svelte";

    function reset() {
        count.set('');
        answer.set(0);
    }

    function handleKeydown(event) {
        const key = event.key;
        if (key === "Delete") {
            reset();
        }
    }

    onMount(() => {
        window.addEventListener('keydown', handleKeydown);
    });

    onDestroy(() => {
        window.removeEventListener('keydown', handleKeydown);
    });
</script>

<div class="resetButton">
    <button on:click={reset}>
        Reset
    </button>
</div>


<style>
    .resetButton {
        display: grid;
        padding: 10px;
        justify-items: center;
        align-items: center;
    }

    .resetButton button {
        width: 260px;
        height: 60px;
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