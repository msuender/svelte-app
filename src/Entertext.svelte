<script>
    let wert = '';

    export let myTitle = "Placeholder";
    export let steil = "color: orange";
</script>


<h2>Text binding</h2>

<p>
Type something <input bind:value={wert}>
You typed: {wert}
</p>

<button on:click={() => {wert = 'Set with button'} }>Set some input</button>

<h1>{myTitle}</h1>
Titel set at usage of component.

<p style={steil}>This sentence got styled!</p>




