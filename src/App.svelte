<script>
	import Translate from './components/Translate.svelte';
	import Advicer from './components/Advicer.svelte';
	import Header from './components/Header.svelte';
	import Welcome from './components/Welcome.svelte';
</script>

<main>
	<Header/>
	<div id="main-container">
		<Welcome />
		<Translate />
		<br />
		<Advicer />
	</div>
</main>

<style>
	main {
		width: 100vw;
		height: 100%;
		background-color: #E0E0E0;
		display: flex;
		flex-direction: column;
		overflow:auto;
	}

	#main-container {
		max-width: 1024px;
		margin: 0 auto;
	}
</style>