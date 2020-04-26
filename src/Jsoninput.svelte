<script>
  
  import Uuidfinder, {findUuids} from './sub/Uuidfinder.svelte';
  import Uuidcreator, {createUuid} from './sub/Uuidcreator.svelte';
  
  
  let textInput = "";
  let inputJson;
  let uuidsFound = {};
  let uuidsToReplace = [];
  let outputJson = {};
  let outputObj;

  const clearAll = () => {
    textInput = "";
    uuidsFound = {};
    uuidsToReplace = [];
    outputJson = {};
  }


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

  $: uuidsFoundArray = uuidsFoundToArray(availableUuids);

  const uuidsFoundToArray = (availableUuidsInput) => {

      let workArray = [];

      for (var item in availableUuidsInput) {

          let workItem = {};

          workItem.uuid = availableUuidsInput[item];
          workItem.path = uuidsFound[availableUuidsInput[item]].paths;

          workArray.push(workItem);

      }

      return workArray;
  }

  $: selectedUuids = uuidsToReplace;

  const replaceUuids = () => {

      let workJSON = {...inputJson};

      for (var item in selectedUuids) {

          let allPaths = uuidsFound[selectedUuids[item]].paths;
          let newUuid = createUuid();
          
          for (var pathItem in allPaths) {

            let splitter = allPaths[pathItem].split('.');

                switch (splitter.length) {
                case 1: workJSON[splitter[0]] = newUuid; break;
                case 2: workJSON[splitter[0]][splitter[1]] = newUuid; break;
                case 3: workJSON[splitter[0]][splitter[1]][splitter[2]] = newUuid; break;
                case 4: workJSON[splitter[0]][splitter[1]][splitter[2]][splitter[3]] = newUuid; break;
                case 5: workJSON[splitter[0]][splitter[1]][splitter[2]][splitter[3]][splitter[4]] = newUuid; break;
                case 6: workJSON[splitter[0]][splitter[1]][splitter[2]][splitter[3]][splitter[4]][splitter[5]] = newUuid; break;
                case 7: workJSON[splitter[0]][splitter[1]][splitter[2]][splitter[3]][splitter[4]][splitter[5]][splitter[6]] = newUuid; break;
                case 8: workJSON[splitter[0]][splitter[1]][splitter[2]][splitter[3]][splitter[4]][splitter[5]][splitter[6]][splitter[7]] = newUuid; break;
                case 9: workJSON[splitter[0]][splitter[1]][splitter[2]][splitter[3]][splitter[4]][splitter[5]][splitter[6]][splitter[7]][splitter[8]] = newUuid; break;
            }
        }

        outputJson = {...workJSON};
      }
  }

$: outputObj = JSON.stringify(outputJson, null, '\t');

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

  button:disabled,button[disabled]{
    background-color: #cccccc;
    cursor:not-allowed !important;
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
    
    <textarea cols="1" rows="20" readonly>
        {outputObj}
    </textarea>
    
    </div>

</div>

<div>

<button disabled={!inputIsJson} on:click={findUuidsInInput}>{inputIsJson ? "Finde UUIDs" : "Kein JSON erkannt"}</button>

<button on:click={clearAll}>Reset</button>

<h5>Found UUIDs and their path:</h5>

<ul>
    {#each uuidsFoundArray as mainItem}
        <li>{mainItem.uuid}
            <ul>
                {#each mainItem.path as subItem}
                    <li>{subItem}</li>
                {/each}
            </ul>
        </li>  
    {/each}
</ul>

</div>

<div>

<h5>Select one or more UUIDs to be replace:</h5>

<select multiple bind:value={uuidsToReplace}>
	{#each availableUuids as uuid}
		<option value={uuid}>
			{uuid}
		</option>
	{/each}
</select>
<button disabled={uuidsToReplace.length === 0} on:click={replaceUuids}>Replace selected</button>

</div>
<div>


</div>