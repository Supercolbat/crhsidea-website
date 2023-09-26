<script lang="ts">
	export let title: string;
</script>

<div class="card">
	<h2>{title}</h2>
	<p><slot /></p>
</div>

<style lang="scss">
	.card {
		flex: 1;

		padding: var(--spacing-md);
		border-radius: 1rem;

		background-color: var(--color-background--card);

		h2 {
			color: var(--color-text--accent);
		}

		p {
			color: var(--color-text);
		}
	}
</style>
