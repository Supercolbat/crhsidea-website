<script>
	import { page } from '$app/stores';
</script>

<main>
	<div>
		<h1>{$page.status}</h1>
		<p>{$page.error ? $page.error.message : 'Unknown error'}</p>
	</div>
</main>

<style>
	main {
		display: flex;
		justify-content: center;

		height: 100vh;
		height: 100dvh;

		font-family: Outfit, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
			Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
	}

	h1 {
		display: inline-block;

		font-size: 10rem;

		opacity: 0.5;
	}

	p {
		position: relative;
		right: 10rem;
		display: inline-block;

		font-size: 3rem;
	}
</style>
