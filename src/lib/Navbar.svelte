<script>
	import CsIdea from '$lib/CsIdea.svelte';

	import { discordUrl } from '../data';
</script>

<nav>
	<CsIdea />
	<div class="nav-links">
		<!-- <a href="/">Home</a> -->
		<!-- <a href="#projects">Projects</a> -->
		<!-- <a href="/members">Members</a> -->
		<!-- <a href="/outreach">Outreach</a> -->
		<a class="nav-highlight" href={discordUrl}>Join</a>
	</div>
</nav>

<style lang="scss">
	nav {
		position: sticky;
		top: 0;
		display: flex;
		justify-content: space-between;
		align-items: center;

		padding: 0.75rem;

		background-color: var(--color-background--nav);
		backdrop-filter: blur(4px);

		font-size: var(--font-sm);

		z-index: 5;

		.nav-links {
			display: flex;
			align-items: center;
			gap: var(--spacing-sm);
		}

		.nav-highlight {
			color: var(--color-background) !important;
			background-color: var(--color-text);
			padding: 0.25rem 1rem;
			border-radius: 999px;

			transition: opacity 0.15s;

			&:hover {
				opacity: 0.8;
			}
		}
	}

	@media (width < 400px) {
		nav {
			flex-direction: column;
		}
	}
</style>
