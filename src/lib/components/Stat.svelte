<script lang="ts">
	export let label: string;
	export let value: string | number;
	export let change: number | undefined = undefined;
	export let unit: string | undefined = undefined;
	export let size: 'sm' | 'md' | 'lg' = 'md';
</script>

<div class="anvil-stat {size}">
	<span class="stat-label">{label}</span>
	<div class="stat-value-row">
		<span class="stat-value">{value}</span>
		{#if unit}
			<span class="stat-unit">{unit}</span>
		{/if}
	</div>
	{#if change !== undefined}
		<span class="stat-change" class:positive={change > 0} class:negative={change < 0}>
			{change > 0 ? '↑' : change < 0 ? '↓' : '→'} {Math.abs(change)}%
		</span>
	{/if}
</div>

<style>
	.anvil-stat {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-1, 0.25rem);
	}

	.stat-label {
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 600;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.sm .stat-label { font-size: 9px; }
	.md .stat-label { font-size: 10px; }
	.lg .stat-label { font-size: 11px; }

	.stat-value-row {
		display: flex;
		align-items: baseline;
		gap: var(--anvil-space-1, 0.25rem);
	}

	.stat-value {
		font-family: var(--anvil-font-display, sans-serif);
		font-weight: 700;
		color: var(--anvil-fg-0, #e8eef5);
	}

	.sm .stat-value { font-size: 20px; }
	.md .stat-value { font-size: 28px; }
	.lg .stat-value { font-size: 36px; }

	.stat-unit {
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 500;
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.sm .stat-unit { font-size: 11px; }
	.md .stat-unit { font-size: 12px; }
	.lg .stat-unit { font-size: 14px; }

	.stat-change {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		font-weight: 600;
	}

	.stat-change.positive { color: var(--anvil-success, #00ff88); }
	.stat-change.negative { color: var(--anvil-error, #ff3366); }
	.stat-change:not(.positive):not(.negative) { color: var(--anvil-fg-muted, #5a6a7a); }
</style>
