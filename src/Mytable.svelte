<script>

    let newName = '';
    let newPreis = 0;

    let list = [
    { name: "Ans", preis: 1 },
    { name: "Zwa", preis: 2 },
    { name: "Drei", preis: 3 }
    ];

    const addData = (name, preis) => {
        list = [...list, {name, preis}];
    }

    const removeData = () => {
        list.pop();
        list = list;
    }

</script>

<h2>Table with push and pop</h2>

<table>
  <tr>
    <th>Index</th>
    <th>Name</th>
    <th>Price</th>
  </tr>
  {#each list as item, index}
    <tr>
      <td>{index}</td>
      <td>{item.name}</td>
      <td>{item.preis}</td>
    </tr>
  {/each}
</table>

<p>
Name: <input bind:value={newName}>
Price: <input bind:value={newPreis}>

<button on:click={addData(newName,Number(newPreis))}>Add Data</button>
<button on:click={removeData} disabled={list.length > 1 ? false : true}>Remove Row</button>
</p>
