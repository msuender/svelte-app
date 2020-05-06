<script>
  
  import Uuidfinder, {findUuids} from './sub/Uuidfinder.svelte';
  import Uuidcreator, {createUuid} from './sub/Uuidcreator.svelte';
  import Samplejson, {sampleJSON1, sampleJSON2, sampleJSON3} from './sub/Samplejson.svelte';
  
  
  let textInput1 = "";
  let textInput2 = "";
  let textInput3 = "";
  let inputJson = {"input1": {}, "input2": {}, "input3": {}};
  let uuidsFound = {};
  let uuidsToReplace = [];
  let outputJson = {"input1": {}, "input2": {}, "input3": {}};
  let outputObj1;
  let outputObj2;
  let outputObj3;

  const clearAll = () => {
    textInput1 = "";
    textInput2 = "";
    textInput3 = "";
    uuidsFound = {};
    uuidsToReplace = [];
  }


  $: input1IsJson = isJSON(textInput1, "input1");
  $: input2IsJson = isJSON(textInput2, "input2");
  $: input3IsJson = isJSON(textInput3, "input3");

  const isJSON = (textToCheck, field) => {

       try { JSON.parse(textToCheck); 
            inputJson[field] = JSON.parse(textToCheck);
            return true; } 
       catch (e) { return false; } 
  };

  const setSampleInput = () => {
      textInput1 = JSON.stringify(sampleJSON1, null, 2);
      textInput2 = JSON.stringify(sampleJSON2, null, 2);
      textInput3 = JSON.stringify(sampleJSON3, null, 2);
  }

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

      //deep cloning absolutely needed
      const workJSON = JSON.parse(JSON.stringify(inputJson));

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
      }
    outputJson = {...workJSON};
  }

$: outputObj1 = JSON.stringify(outputJson.input1, null, 2);
$: outputObj2 = JSON.stringify(outputJson.input2, null, 2);
$: outputObj3 = JSON.stringify(outputJson.input3, null, 2);

</script>

<style>

textarea {
    font-family: monospace;
}
    .flex-container {
    display: flex;
}

.flex-child {
    flex: 1;
    /* border: 2px solid; */
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

<button on:click={setSampleInput}>Sample JSON</button>

    <div class="flex-container">

        <div class="flex-child">

        <h2>Input 1</h2>

        <textarea bind:value={textInput1} cols="1" rows="20" placeholder="Paste your JSON here!"/>

        Is it a JSON? {input1IsJson}

        </div>

        <div class ="flex-child">

        <h2>Output 1</h2>
        
        <textarea bind:value={outputObj1} cols="1" rows="20"/>
        
        </div>

    </div>

<hr>

    <div class="flex-container">

        <div class="flex-child">

        <h2>Input 2</h2>

        <textarea bind:value={textInput2} cols="1" rows="20" placeholder="Paste your JSON here!"/>

        Is it a JSON? {input2IsJson}

        </div>

        <div class ="flex-child">

        <h2>Output 2</h2>
        
        <textarea bind:value={outputObj2} cols="1" rows="20"/>
        
        </div>

    </div>

<hr>

    <div class="flex-container">

        <div class="flex-child">

        <h2>Input 3</h2>

        <textarea bind:value={textInput3} cols="1" rows="20" placeholder="Paste your JSON here!"/>

        Is it a JSON? {input3IsJson}

        </div>

        <div class ="flex-child">

        <h2>Output 3</h2>
        
        <textarea bind:value={outputObj3} cols="1" rows="20"/>
        
        </div>

    </div>

<div>

<hr>

<button disabled={!input1IsJson && !input2IsJson} on:click={findUuidsInInput}>Finde UUIDs</button>

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