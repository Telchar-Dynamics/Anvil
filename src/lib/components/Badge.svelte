<script lang="ts">
	export let variant: 'default' | 'success' | 'warning' | 'error' | 'accent' = 'default';
	export let size: 'sm' | 'md' = 'md';
	export let pulse: boolean = false;
	export let dot: boolean = true;
</script>

<span class="anvil-badge {variant} {size}" class:pulse>
	{#if dot}
		<span class="badge-dot"></span>
	{/if}
	<slot />
</span>

<style>
	.anvil-badge {
		display: inline-flex;
		align-items: center;
		gap: 6px;
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 600;
		border-radius: var(--anvil-radius-sm, 2px);
		text-transform: uppercase;
		letter-spacing: 0.1em;
		border: 1px solid transparent;
	}

	/* Sizes */
	.sm {
		padding: 2px 8px;
		font-size: 9px;
	}

	.md {
		padding: 4px 10px;
		font-size: 10px;
	}

	.badge-dot {
		width: 6px;
		height: 6px;
		border-radius: 50%;
		background: currentColor;
	}

	.pulse .badge-dot {
		animation: badge-pulse 1.5s ease-in-out infinite;
	}

	@keyframes badge-pulse {
		0%, 100% {
			opacity: 1;
			box-shadow: 0 0 4px currentColor;
		}
		50% {
			opacity: 0.5;
			box-shadow: 0 0 8px currentColor;
		}
	}

	/* Variants */
	.default {
		background: var(--anvil-bg-1, #0a0d12);
		border-color: var(--anvil-border, #1a242e);
		color: var(--anvil-fg-1, #a8b5c4);
	}

	.success {
		background: rgba(0, 255, 136, 0.1);
		border-color: rgba(0, 255, 136, 0.4);
		color: var(--anvil-success, #00ff88);
		text-shadow: 0 0 6px var(--anvil-success, #00ff88);
	}

	.warning {
		background: rgba(255, 170, 0, 0.1);
		border-color: rgba(255, 170, 0, 0.4);
		color: var(--anvil-warning, #ffaa00);
		text-shadow: 0 0 6px var(--anvil-warning, #ffaa00);
	}

	.error {
		background: rgba(255, 51, 102, 0.1);
		border-color: rgba(255, 51, 102, 0.4);
		color: var(--anvil-error, #ff3366);
		text-shadow: 0 0 6px var(--anvil-error, #ff3366);
	}

	.accent {
		background: rgba(0, 240, 255, 0.1);
		border-color: rgba(0, 240, 255, 0.4);
		color: var(--anvil-accent, #00f0ff);
		text-shadow: 0 0 6px var(--anvil-accent, #00f0ff);
	}
</style>
