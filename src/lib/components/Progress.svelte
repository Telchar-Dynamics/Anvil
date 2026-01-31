<script lang="ts">
	export let value: number = 0;
	export let max: number = 100;
	export let variant: 'default' | 'accent' | 'success' | 'warning' | 'error' = 'accent';
	export let size: 'sm' | 'md' | 'lg' = 'md';
	export let showValue: boolean = false;
	export let animated: boolean = false;
	export let striped: boolean = false;

	$: percentage = Math.min(100, Math.max(0, (value / max) * 100));
</script>

<div class="anvil-progress {size}">
	<div class="progress-track">
		<div
			class="progress-fill {variant}"
			class:animated
			class:striped
			style:width="{percentage}%"
		></div>
	</div>
	{#if showValue}
		<span class="progress-value">{Math.round(percentage)}%</span>
	{/if}
</div>

<style>
	.anvil-progress {
		display: flex;
		align-items: center;
		gap: var(--anvil-space-2, 0.5rem);
		width: 100%;
	}

	.progress-track {
		flex: 1;
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		overflow: hidden;
	}

	.progress-fill {
		height: 100%;
		transition: width 0.3s ease;
		position: relative;
	}

	/* Sizes */
	.sm .progress-track { height: 4px; }
	.md .progress-track { height: 8px; }
	.lg .progress-track { height: 12px; }

	/* Variants */
	.progress-fill.default {
		background: var(--anvil-fg-muted, #5a6a7a);
	}

	.progress-fill.accent {
		background: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 10px var(--anvil-accent, #00f0ff);
	}

	.progress-fill.success {
		background: var(--anvil-success, #00ff88);
		box-shadow: 0 0 10px var(--anvil-success, #00ff88);
	}

	.progress-fill.warning {
		background: var(--anvil-warning, #ffaa00);
		box-shadow: 0 0 10px var(--anvil-warning, #ffaa00);
	}

	.progress-fill.error {
		background: var(--anvil-error, #ff3366);
		box-shadow: 0 0 10px var(--anvil-error, #ff3366);
	}

	/* Striped */
	.progress-fill.striped {
		background-image: linear-gradient(
			45deg,
			rgba(255, 255, 255, 0.1) 25%,
			transparent 25%,
			transparent 50%,
			rgba(255, 255, 255, 0.1) 50%,
			rgba(255, 255, 255, 0.1) 75%,
			transparent 75%,
			transparent
		);
		background-size: 20px 20px;
	}

	/* Animated */
	.progress-fill.animated.striped {
		animation: progress-stripes 1s linear infinite;
	}

	@keyframes progress-stripes {
		from { background-position: 20px 0; }
		to { background-position: 0 0; }
	}

	.progress-value {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		font-weight: 600;
		color: var(--anvil-fg-muted, #5a6a7a);
		min-width: 36px;
		text-align: right;
	}
</style>
