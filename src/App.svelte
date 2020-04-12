<script>
	import Counter from './Counter.svelte';
	export let name;

</script>

<main>
	<h1>Hello {name}!</h1>
	<p>A litte app to practice on the new framework.</p>
</main>

<Counter/>


<svelte:head>
	<link rel="stylesheet" href="https://unpkg.com/primitive-ui/dist/css/main.css" />
</svelte:head>