<script lang="ts">
	export let title: string | undefined = undefined;
	export let collapsible: boolean = false;
	export let collapsed: boolean = false;
	export let width: string = '240px';

	function toggleCollapse() {
		if (collapsible) {
			collapsed = !collapsed;
		}
	}
</script>

<div class="anvil-panel" style:width={width}>
	{#if title}
		<button
			class="panel-header"
			class:collapsible
			on:click={toggleCollapse}
			disabled={!collapsible}
		>
			<h3 class="panel-title">{title}</h3>
			{#if collapsible}
				<span class="collapse-toggle">{collapsed ? '+' : '−'}</span>
			{/if}
		</button>
	{/if}

	{#if !collapsed}
		<div class="panel-content">
			<slot />
		</div>
	{/if}
</div>

<style>
	.anvil-panel {
		position: relative;
		background: rgba(10, 13, 18, 0.98);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		display: flex;
		flex-direction: column;
		backdrop-filter: blur(12px);
		overflow: hidden;
	}

	/* Corner brackets */
	.anvil-panel::before,
	.anvil-panel::after {
		content: '';
		position: absolute;
		width: 12px;
		height: 12px;
		border-color: var(--anvil-accent, #00f0ff);
		border-style: solid;
		opacity: 0.5;
		pointer-events: none;
	}

	.anvil-panel::before {
		top: -1px;
		left: -1px;
		border-width: 2px 0 0 2px;
	}

	.anvil-panel::after {
		bottom: -1px;
		right: -1px;
		border-width: 0 2px 2px 0;
	}

	.panel-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		width: 100%;
		padding: var(--anvil-space-3, 0.75rem);
		background: var(--anvil-bg-1, #0a0d12);
		border: none;
		border-bottom: 1px solid var(--anvil-border, #1a242e);
		cursor: default;
		text-align: left;
	}

	.panel-header.collapsible {
		cursor: pointer;
		transition: background var(--anvil-transition-fast, 100ms ease);
	}

	.panel-header.collapsible:hover {
		background: var(--anvil-bg-2, #0e1319);
	}

	.panel-title {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.15em;
		color: var(--anvil-accent, #00f0ff);
		margin: 0;
		text-transform: uppercase;
	}

	.collapse-toggle {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 14px;
		font-weight: 600;
		color: var(--anvil-fg-muted, #5a6a7a);
		line-height: 1;
	}

	.panel-content {
		flex: 1;
		overflow-y: auto;
		padding: var(--anvil-space-2, 0.5rem);
	}

	/* Scrollbar */
	.panel-content::-webkit-scrollbar {
		width: 4px;
	}

	.panel-content::-webkit-scrollbar-track {
		background: var(--anvil-bg-1, #0a0d12);
	}

	.panel-content::-webkit-scrollbar-thumb {
		background: var(--anvil-border, #1a242e);
		border-radius: 2px;
	}
</style>
