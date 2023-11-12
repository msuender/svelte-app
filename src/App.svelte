<script>
	import Counter from './Counter.svelte';
	import Hiddenline from './Hiddenline.svelte';
	import Staticlist from './Staticlist.svelte';
	import Mytable from './Mytable.svelte';
	import Entertext from './Entertext.svelte';
	import Pressenter from './Pressenter.svelte';
	import Language from './Language.svelte';
	import Mainmodule from './Mainmodule.svelte';
	import Download from './Download.svelte';

	import Jsoninput from './Jsoninput.svelte';

	export let name;

</script>

<main>
	<h1>Hello {name}!</h1>
	<p>A litte app to practice on the new framework.</p>
</main>

<Jsoninput/>

<hr>

<Counter/>

<Hiddenline/>

<Staticlist/>

<Mytable/>

<Entertext myTitle="My nice title" steil="color:blue"/>

<Pressenter/>

<Language/>

<Mainmodule/>

<hr>

<div>
<p>Just plain HTML :-)</p>
</div>

<hr>

<Download />



<svelte:head>
	<link rel="stylesheet" href="https://unpkg.com/primitive-ui/dist/css/main.css" />
</svelte:head>
