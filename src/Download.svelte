<script>
	let textvalue = 'ssd';

	let downloadContent = new Blob(["abcsl lalsl"]);
	let blobURL = URL.createObjectURL(downloadContent);

    let dataURL = 'data:text/plain;charset=utf-8,Das ist ein Test';

    const createFile = (textinp, filename) => {
        let textBlob = new Blob([textinp]);
        let file = new File([textBlob], filename, {type: "text/plain"});
        let fileURL = URL.createObjectURL(file);

        var a = document.createElement('a');
        document.body.append(a);
        a.download = filename;
        a.href = fileURL;
        a.click();
        a.remove();
    }

</script>

<h2>Download Links</h2>

<div>
<h4>using blob</h4>
	blobURL: {blobURL}
    <a href={blobURL} download="blobURL.txt">Click to download</a>
</div>


<div>
<h4>using data url</h4>
    dataURL: {dataURL}
    <a href={dataURL} download="dataURL.txt">Click to download</a>
</div>

<div>
<h4>using textarea</h4>
<textarea name="textfield" id="textfield" cols="10" rows="3" bind:value={textvalue}></textarea>
<button on:click={createFile(textvalue,"textfield.txt")}>get file</button>
</div>
