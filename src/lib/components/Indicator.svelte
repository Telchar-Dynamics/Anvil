<script lang="ts">
	export let status: 'success' | 'warning' | 'error' | 'accent' | 'muted' = 'muted';
	export let size: 'sm' | 'md' | 'lg' = 'md';
	export let pulse: boolean = false;
	export let label: string | undefined = undefined;
</script>

<span class="anvil-indicator {status} {size}" class:pulse>
	<span class="indicator-dot"></span>
	{#if label}
		<span class="indicator-label">{label}</span>
	{/if}
</span>

<style>
	.anvil-indicator {
		display: inline-flex;
		align-items: center;
		gap: 6px;
	}

	.indicator-dot {
		border-radius: 50%;
		transition: box-shadow var(--anvil-transition-fast, 100ms ease);
	}

	/* Sizes */
	.sm .indicator-dot {
		width: 6px;
		height: 6px;
	}

	.md .indicator-dot {
		width: 8px;
		height: 8px;
	}

	.lg .indicator-dot {
		width: 10px;
		height: 10px;
	}

	/* Status colors */
	.success .indicator-dot {
		background: var(--anvil-success, #00ff88);
		box-shadow: 0 0 6px var(--anvil-success, #00ff88);
	}

	.warning .indicator-dot {
		background: var(--anvil-warning, #ffaa00);
		box-shadow: 0 0 6px var(--anvil-warning, #ffaa00);
	}

	.error .indicator-dot {
		background: var(--anvil-error, #ff3366);
		box-shadow: 0 0 6px var(--anvil-error, #ff3366);
	}

	.accent .indicator-dot {
		background: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 6px var(--anvil-accent, #00f0ff);
	}

	.muted .indicator-dot {
		background: var(--anvil-fg-muted, #5a6a7a);
		box-shadow: none;
	}

	/* Pulse animation */
	.pulse .indicator-dot {
		animation: indicator-pulse 1.5s ease-in-out infinite;
	}

	@keyframes indicator-pulse {
		0%, 100% {
			opacity: 1;
			transform: scale(1);
		}
		50% {
			opacity: 0.6;
			transform: scale(1.1);
		}
	}

	.indicator-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		color: var(--anvil-fg-1, #a8b5c4);
		text-transform: uppercase;
		letter-spacing: 0.08em;
	}
</style>
