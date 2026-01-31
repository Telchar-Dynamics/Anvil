<script lang="ts">
	export let size: 'sm' | 'md' = 'md';
</script>

<kbd class="anvil-kbd {size}"><slot /></kbd>

<style>
	.anvil-kbd {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 500;
		color: var(--anvil-fg-1, #a8b5c4);
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-bottom-width: 2px;
		border-radius: var(--anvil-radius-sm, 2px);
		white-space: nowrap;
	}

	.sm {
		min-width: 18px;
		height: 18px;
		padding: 0 var(--anvil-space-1, 0.25rem);
		font-size: 10px;
	}

	.md {
		min-width: 24px;
		height: 24px;
		padding: 0 var(--anvil-space-2, 0.5rem);
		font-size: 11px;
	}
</style>
