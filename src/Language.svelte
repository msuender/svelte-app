<script>

let selectedLang = "de";

const langData = {
    "de": { "language": "German", "greet": "Hallo!"},
    "mx": { "language": "Mexican", "greet": "Hola!"},
    "en": { "language": "English", "greet": "Hello!"},
}

$: actualData = langData[selectedLang];
$: avialableLangs = Object.keys(langData);

const setLang = (language) => {
    selectedLang = language;
    }

</script>

<h2>Language Selection</h2>

<p>
{actualData.greet} ({actualData.language})

{#each avialableLangs as lang}
     <button 
        on:click={() => setLang(lang)} 
        disabled={lang === selectedLang ? true : false}>
        {langData[lang].language}
    </button>
{/each}
</p>
