<script>
import {page} from "$app/stores";
</script>

<ul>
    <li aria-current={$page.url.pathname === '/' ? 'page' : undefined}>
        <a href="/">Home</a>
    </li>
    <li aria-current={$page.url.pathname === '/Tetris' ? 'page' : undefined}>
        <a href="/Tetris">Tetris</a>
    </li>
    <li aria-current={$page.url.pathname ==='/Calc' ? 'page' : undefined}>
        <a href="/Calc">Calc</a>
    </li>
</ul>

