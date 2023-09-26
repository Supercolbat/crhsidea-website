<script>
	import CsIdea from './CsIdea.svelte';

	import { discordUrl } from '../data';
</script>

<footer>
	<img src="/assets/wave.svg" alt="Wave page transition" aria-hidden="true" />

	<div class="footer-container">
		<div>
			<div>
				<span style="font-size: var(--font-lg);"><CsIdea /></span>
				<p>Going beyond CS</p>
			</div>

			<div class="footer-nav">
				<div>
					<b>Explore</b>
					<div class="footer-links">
						<a href="/">Home</a>
						<!-- <a href="/join">Join</a> -->
						<!-- <a href="/projects">Projects</a> -->
						<!-- <a href="/members">Members</a> -->
					</div>
				</div>
				<div>
					<b>Socials</b>
					<div class="footer-links">
						<a href={discordUrl}>Discord</a>
						<!-- <a href="#">Instagram</a> -->
					</div>
				</div>
			</div>
		</div>
	</div>
</footer>

<style lang="scss">
	p,
	a {
		color: var(--color-text--footer);
	}

	footer {
		margin-top: var(--spacing-xl);

		font-size: var(--font-sm);
		color: #fff;

		overflow-x: hidden;

		img {
			width: 100%;
			min-width: 500px;

			transform: translateY(1px);
		}
	}

	.footer-container {
		display: flex;
		justify-content: center;
		padding: 2rem var(--spacing--page-x);
		padding-top: 2rem;

		background-color: #004cbb;

		& > div {
			display: flex;
			justify-content: space-between;
			width: var(--size--max-width);
		}
	}

	.footer-nav {
		display: flex;
		gap: var(--spacing-lg);

		b {
			font-size: var(--font-md);
		}
	}

	.footer-links {
		display: flex;
		flex-direction: column;
	}
</style>
