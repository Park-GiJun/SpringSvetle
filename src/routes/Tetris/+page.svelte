<script>
    function draw(){
        const canvas = document.getElementById('canvas');
        if(canvas.getContext){
            const ctx = canvas.getContext('2d');

            const x = canvas.width/2;
            const y = 10;

            ctx.fillStyle = 'black';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = 'orange';
            ctx.fillRect(-10, -10, 20, 20);
        }
    }

</script>

<button on:click={draw}>클릭</button>

<canvas id="canvas" width="100%" height="100%">

</canvas>

