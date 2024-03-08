<script>
    import {count} from './stores.js';
    import {get} from 'svelte/store';
    import {answer} from './Answer.js';
    import {onDestroy, onMount} from "svelte";

    let display = answer;

    function calc() {
        const storeValue = get(count);

        let result = storeValue.split(' ');
        console.log(result);

        let answer = 0;
        for (let i = 0; i < result.length; i++) {
            if (result[i] === '*') {
                answer = parseInt(result[i - 1]) * parseInt(result[i + 1]);
                result.splice(i - 1, 3, answer.toString());
                i = 0;
            } else if (result[i] === '/') {
                answer = parseInt(result[i - 1]) / parseInt(result[i + 1]);
                result.splice(i - 1, 3, answer.toString());
                i = 0;
            }
        }
        while (result.length > 1) {
            for (let i = 0; i < result.length; i++) {
                if (result[i] === '+') {
                    answer = parseInt(result[i - 1]) + parseInt(result[i + 1]);
                    result.splice(i - 1, 3, answer.toString());
                    break;
                } else if (result[i] === '-') {
                    answer = parseInt(result[i - 1]) - parseInt(result[i + 1]);
                    result.splice(i - 1, 3, answer.toString());
                    break;
                }
            }
        }
        display.set(answer);
    }

    function handleKeydown(event) {
        const key = event.key;
        if (key === "Enter") {
            calc();
        }
    }

    onMount(() => {
        window.addEventListener('keydown', handleKeydown);
    });

    onDestroy(() => {
        window.removeEventListener('keydown', handleKeydown);
    });
</script>
<div class="equalButton">
    <button on:click={calc}>
        =
    </button>
</div>


<style>
    .equalButton {
        display: grid;
        padding: 10px;
        justify-items: center;
        align-items: center;
    }

    .equalButton button {
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
