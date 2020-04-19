<script>
  
  import Uuidfinder, {findUuids} from './sub/Uuidfinder.svelte';
  
  
  let textInput = "";
  let inputJson;
  let uuidsFound = {};
  let uuidsToReplace = [];

  $: inputIsJson = isJSON(textInput);

  const isJSON = (textToCheck) => {

       try { JSON.parse(textToCheck); 
            inputJson = JSON.parse(textToCheck);
            return true; } 
       catch (e) { return false; }
        
  };

  const findUuidsInInput = () => {
      uuidsFound = findUuids(inputJson);
  }

  $: availableUuids = Object.keys(uuidsFound);

</script>

<style>
    .flex-container {
    display: flex;
}

.flex-child {
    flex: 1;
    border: 2px solid;
}  

.flex-child:first-child {
    margin-right: 20px;
} 
</style>

<h1>UUID Updater</h1>

<div class="flex-container">

    <div class="flex-child">

    <h2>Input</h2>

    <textarea bind:value={textInput} cols="1" rows="20" placeholder="Paste your JSON here!"/>

    Is it a JSON? {inputIsJson}

    </div>

    <div class ="flex-child">

    <h2>Output</h2>
    
    No text yet!
    
    </div>

</div>

<div>

<button disabled={!inputIsJson} on:click={findUuidsInInput}>{inputIsJson ? "Finde UUIDs" : "Kein JSON erkannt"}</button>

<p>{uuidsFound ? JSON.stringify(uuidsFound, undefined, 2) : "No nix da"}</p>

</div>

<div>

<select multiple bind:value={uuidsToReplace}>
	{#each availableUuids as uuid}
		<option value={uuid}>
			{uuid}
		</option>
	{/each}
</select>

</div>