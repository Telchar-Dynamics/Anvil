<script lang="ts">
	export let title: string | undefined = undefined;
	export let padding: boolean = true;
	export let glow: boolean = false;
	export let corners: boolean = true;
</script>

<div class="anvil-card" class:with-padding={padding} class:glow class:with-corners={corners}>
	{#if corners}
		<div class="card-corner tl"></div>
		<div class="card-corner tr"></div>
		<div class="card-corner bl"></div>
		<div class="card-corner br"></div>
	{/if}
	{#if title}
		<div class="card-header">
			<h3 class="card-title">{title}</h3>
			<slot name="actions" />
		</div>
	{/if}
	<div class="card-content">
		<slot />
	</div>
	{#if $$slots.footer}
		<div class="card-footer">
			<slot name="footer" />
		</div>
	{/if}
</div>

<style>
	.anvil-card {
		position: relative;
		background: var(--anvil-bg-2, #0e1319);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-md, 4px);
		transition: border-color var(--anvil-transition-fast, 100ms ease),
		            box-shadow var(--anvil-transition-fast, 100ms ease);
	}

	.anvil-card:hover {
		border-color: var(--anvil-border-accent, #2de2e640);
	}

	.anvil-card.glow {
		box-shadow: var(--anvil-shadow-glow, 0 0 30px rgba(0, 240, 255, 0.15));
	}

	/* HUD corner brackets */
	.card-corner {
		position: absolute;
		width: 10px;
		height: 10px;
		border-color: var(--anvil-accent, #00f0ff);
		border-style: solid;
		opacity: 0.5;
		transition: opacity var(--anvil-transition-fast, 100ms ease);
		pointer-events: none;
	}

	.anvil-card:hover .card-corner {
		opacity: 0.8;
	}

	.card-corner.tl {
		top: -1px;
		left: -1px;
		border-width: 2px 0 0 2px;
	}

	.card-corner.tr {
		top: -1px;
		right: -1px;
		border-width: 2px 2px 0 0;
	}

	.card-corner.bl {
		bottom: -1px;
		left: -1px;
		border-width: 0 0 2px 2px;
	}

	.card-corner.br {
		bottom: -1px;
		right: -1px;
		border-width: 0 2px 2px 0;
	}

	.anvil-card.with-padding .card-content {
		padding: var(--anvil-space-4, 1rem);
	}

	.card-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		border-bottom: 1px solid var(--anvil-border, #1a242e);
		background: var(--anvil-bg-1, #0a0d12);
	}

	.card-title {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		font-weight: 600;
		letter-spacing: 0.1em;
		text-transform: uppercase;
		color: var(--anvil-fg-1, #a8b5c4);
		margin: 0;
	}

	.card-footer {
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		border-top: 1px solid var(--anvil-border, #1a242e);
		background: var(--anvil-bg-1, #0a0d12);
	}
</style>
