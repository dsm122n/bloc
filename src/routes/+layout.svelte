<script>
	import Header from './Header.svelte';
	import './styles.css';
</script>

<div class="app">
<!-- 	<Header /> -->
	<h1>Editor de texto rapidito de dan :) </h1>
	<main>
		<slot />
	</main>

<!-- 	<footer>
		<p>visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn SvelteKit</p>
	</footer> -->
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}

	footer a {
		font-weight: bold;
	}
	.tiptap{
      border: 1px solid black;
      background-color: lightgreen;
      padding: 1rem;
      min-width: 100px;
      max-width: 800px;
      min-height: 100px;
      max-height: 600px;

    }
	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
