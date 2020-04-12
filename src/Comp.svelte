<script>
    let count = 0;

    const handleClick = () => {
        count++;
    }
</script>

<style>

</style>

<p>Mein erster Text</p>

<button on:click={handleClick}>Clicked {count} times </button>

