<script lang="ts">
	export let iconUrl: string;
	export let title: string;
</script>

<div class="noborder-card">
	<!-- TODO: improve alt -->
	<div style="mask-image: url({iconUrl}); -webkit-mask-image: url({iconUrl})" />
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
</style>
