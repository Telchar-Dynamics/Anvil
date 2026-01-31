<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let variant: 'primary' | 'secondary' | 'danger' | 'ghost' | 'success' = 'secondary';
	export let size: 'sm' | 'md' | 'lg' = 'md';
	export let disabled: boolean = false;
	export let type: 'button' | 'submit' | 'reset' = 'button';

	const dispatch = createEventDispatcher();
</script>

<button
	class="anvil-btn {variant} {size}"
	{disabled}
	{type}
	on:click
	on:click={() => dispatch('click')}
>
	<slot />
</button>

<style>
	.anvil-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: var(--anvil-space-2, 0.5rem);
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		font-weight: 600;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		border: 1px solid transparent;
		border-radius: var(--anvil-radius-sm, 2px);
		cursor: pointer;
		transition: all var(--anvil-transition-fast, 100ms ease);
	}

	.anvil-btn:disabled {
		opacity: 0.4;
		cursor: not-allowed;
	}

	/* Sizes */
	.sm {
		height: 26px;
		padding: 0 var(--anvil-space-2, 0.5rem);
		font-size: 10px;
	}

	.md {
		height: 32px;
		padding: 0 var(--anvil-space-3, 0.75rem);
	}

	.lg {
		height: 40px;
		padding: 0 var(--anvil-space-4, 1rem);
		font-size: 12px;
	}

	/* Variants */
	.primary {
		background: var(--anvil-accent, #00f0ff);
		color: var(--anvil-bg-0, #050608);
		box-shadow: 0 0 12px rgba(0, 240, 255, 0.3);
	}

	.primary:hover:not(:disabled) {
		background: #33f5ff;
		box-shadow: 0 0 20px rgba(0, 240, 255, 0.5);
	}

	.secondary {
		background: var(--anvil-bg-2, #0e1319);
		border-color: var(--anvil-border, #1a242e);
		color: var(--anvil-fg-1, #a8b5c4);
	}

	.secondary:hover:not(:disabled) {
		border-color: var(--anvil-accent, #00f0ff);
		color: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px rgba(0, 240, 255, 0.2);
	}

	.danger {
		background: rgba(255, 51, 102, 0.2);
		border-color: var(--anvil-error, #ff3366);
		color: var(--anvil-error, #ff3366);
	}

	.danger:hover:not(:disabled) {
		background: var(--anvil-error, #ff3366);
		color: white;
		box-shadow: 0 0 12px rgba(255, 51, 102, 0.4);
	}

	.success {
		background: rgba(0, 255, 136, 0.2);
		border-color: var(--anvil-success, #00ff88);
		color: var(--anvil-success, #00ff88);
	}

	.success:hover:not(:disabled) {
		background: var(--anvil-success, #00ff88);
		color: var(--anvil-bg-0, #050608);
		box-shadow: 0 0 12px rgba(0, 255, 136, 0.4);
	}

	.ghost {
		background: transparent;
		color: var(--anvil-fg-1, #a8b5c4);
		border-color: transparent;
	}

	.ghost:hover:not(:disabled) {
		background: var(--anvil-bg-2, #0e1319);
		border-color: var(--anvil-border, #1a242e);
		color: var(--anvil-accent, #00f0ff);
	}
</style>
