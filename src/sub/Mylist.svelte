<script>

    export let mylist = [
        {"name": "Uno", "preis": 1},
        {"name": "Due", "preis": 2},
        {"name": "Tre", "preis": 3},
    ]

</script>

{#each mylist as item}
     <p>Name: {item.name} Preis: {item.preis}</p>
{/each}




