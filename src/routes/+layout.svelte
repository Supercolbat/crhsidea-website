<script>
	import '../app.scss';
	import '../css/outfit.css';
	import '../css/reset.css';

	import Footer from '$lib/Footer.svelte';
	import Navbar from '$lib/Navbar.svelte';
</script>

<svelte:head>
	<title>CS/IDEA — Go beyond CompSci</title>
	<meta
		name="description"
		content="CS/IDEA helps students go beyond school curriculum and step into the world of software development."
	/>
</svelte:head>

<!-- <Navbar /> -->

<slot />

<!-- <Footer /> -->
