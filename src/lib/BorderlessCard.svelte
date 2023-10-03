<script lang="ts">
	export let title: string;
</script>

<div class="noborder-card">
	<h2>{title}</h2>
	<p><slot /></p>
</div>

<style lang="scss">
	.noborder-card {
		width: min-content;

		padding: 0;

		text-align: left;

		div {
			margin-bottom: var(--spacing-md);
			height: 2.5rem;
			width: 2.5rem;

			background-color: var(--color-icon);
		}

		h2 {
			color: var(--color-text--accent);
		}

		p {
			min-width: 12rem;
			color: var(--color-text);
		}
	}

	@media (width < 448px) {
		.noborder-card {
			width: 100%;
		}
	}
</style>
