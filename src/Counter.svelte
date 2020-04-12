<script>
    let count = 0;
    let countText = 'Click me!';

    $: double = count * 2;
    
    $: if (count === 0) {
            countText = 'Never clicked'
        } else if (count === 1) {
            countText = 'Clicked ' + count + ' time'
        } else {
            countText = 'Clicked ' + count + ' times';
        }

    const handleClick = () => {
        count++;
    }

    const resetClick = () => {
        count = 0;
    }
</script>

<p>My counter</p>

<button on:click={handleClick}>{countText}</button>
<button on:click={resetClick}>Reset Counter</button>

<p>Double: {double}</p>

