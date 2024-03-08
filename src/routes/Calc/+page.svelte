<script>
    import { count } from './stores.js';
    import {answer} from './Answer.js';
    import NumPad from "./NumPad.svelte";
    import Symbols from "./Symbols.svelte";
    import Equal from "./Equal.svelte";
    import Reset from "./Reset.svelte"

    let count_value;
    let answer_value;
    count.subscribe((value => {
        count_value  = value;
    }));

    answer.subscribe((value => {
        answer_value = value;
    }))


</script>

<div class="calculator">
    <input class="inputText" type="text" readonly value="{count_value}"/>
    <input class="inputText" type="text" readonly value="{answer_value}"/>
    <NumPad/>
    <Symbols />
    <Equal/>
    <Reset />
</div>

<style>
    .calculator {
        display: compact;
        width: 300px;
        background: #E5E3E4;
        box-shadow: #E5E3E4 2px 2px 0 0;
        justify-content: center;
        align-items: center;
        border-radius: 8px;
    }

    .inputText {

        width: 90%;
        height: 50px;
        margin: 10px 10px 10px 10px;
        border: 1px #5BA199 solid;
        border-radius: 8px;
        text-align: center;
    }
</style>