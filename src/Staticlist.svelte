<script>
    let list = [
        {"name": "Ans", "preis": 1},
        {"name": "Zwa", "preis": 2},
        {"name": "Drei", "preis": 2},
    ]
    

</script>

<h2>Static List</h2>

{#each list as item}
     <p>Name: {item.name} Preis: {item.preis}</p>
{/each}

