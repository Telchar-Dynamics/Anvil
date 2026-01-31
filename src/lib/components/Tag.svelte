<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let variant: 'default' | 'accent' | 'success' | 'warning' | 'error' = 'default';
	export let size: 'sm' | 'md' = 'md';
	export let removable: boolean = false;

	const dispatch = createEventDispatcher<{ remove: void }>();
</script>

<span class="anvil-tag {variant} {size}">
	<slot />
	{#if removable}
		<button class="tag-remove" on:click={() => dispatch('remove')} aria-label="Remove">×</button>
	{/if}
</span>

<style>
	.anvil-tag {
		display: inline-flex;
		align-items: center;
		gap: var(--anvil-space-1, 0.25rem);
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 500;
		background: var(--anvil-bg-2, #0e1319);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
	}

	.sm {
		padding: 2px var(--anvil-space-2, 0.5rem);
		font-size: 10px;
	}

	.md {
		padding: var(--anvil-space-1, 0.25rem) var(--anvil-space-2, 0.5rem);
		font-size: 11px;
	}

	.default { color: var(--anvil-fg-1, #a8b5c4); }
	.accent { color: var(--anvil-accent, #00f0ff); border-color: var(--anvil-accent, #00f0ff); }
	.success { color: var(--anvil-success, #00ff88); border-color: var(--anvil-success, #00ff88); }
	.warning { color: var(--anvil-warning, #ffaa00); border-color: var(--anvil-warning, #ffaa00); }
	.error { color: var(--anvil-error, #ff3366); border-color: var(--anvil-error, #ff3366); }

	.tag-remove {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 14px;
		height: 14px;
		padding: 0;
		background: transparent;
		border: none;
		color: inherit;
		opacity: 0.6;
		cursor: pointer;
		font-size: 14px;
		line-height: 1;
		transition: opacity var(--anvil-transition-fast, 100ms ease);
	}

	.tag-remove:hover {
		opacity: 1;
	}
</style>
