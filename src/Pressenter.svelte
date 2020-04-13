<script>
    let entered;
    let entered2;

    const sendAlert = (value) => {
        alert("You wrote " + value);
    }

</script>


<h2>Key events</h2>

<p>Type and press Enter: <input bind:value={entered} on:keydown={e => {if (e.keyCode === 13) {sendAlert(entered)}}}></p>

<p>Very nasty solution! <code>on:keydown={e => {if (e.keyCode === 13) {sendAlert()}}}</code>

<h3>Alternative way: Submit</h3>

<form on:submit|preventDefault={sendAlert(entered2)}>
    Type and submit: <input type="text" bind:value={entered2}>
     <input type="submit" value="Submit">
</form>