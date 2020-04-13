<script>
    let hideLine = true;
    
    const showLine = () => {
        if (hideLine) {
            hideLine = false;
        } else {
            hideLine = true;
        }
    }

</script>

<h2>Hidden Line</h2>

<p hidden={hideLine}>Tataaah!</p>

<button on:click={showLine}>{hideLine ? 'Show the line' : 'Hide the line'}</button>