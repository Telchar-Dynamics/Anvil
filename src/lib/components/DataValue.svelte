<script lang="ts">
	export let label: string;
	export let value: string | number;
	export let unit: string | undefined = undefined;
	export let variant: 'default' | 'accent' | 'success' | 'warning' | 'error' = 'default';
	export let size: 'sm' | 'md' | 'lg' = 'md';
	export let inline: boolean = false;
</script>

<div class="anvil-data-value {size}" class:inline>
	<span class="data-label">{label}</span>
	<span class="data-value {variant}">
		{value}{#if unit}<span class="data-unit">{unit}</span>{/if}
	</span>
</div>

<style>
	.anvil-data-value {
		display: flex;
		flex-direction: column;
		gap: 2px;
	}

	.anvil-data-value.inline {
		flex-direction: row;
		align-items: baseline;
		gap: var(--anvil-space-2, 0.5rem);
	}

	.data-label {
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 500;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.data-value {
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 600;
	}

	.data-unit {
		font-size: 0.8em;
		opacity: 0.7;
		margin-left: 2px;
	}

	/* Sizes */
	.sm .data-label { font-size: 8px; }
	.sm .data-value { font-size: 12px; }

	.md .data-label { font-size: 9px; }
	.md .data-value { font-size: 14px; }

	.lg .data-label { font-size: 10px; }
	.lg .data-value { font-size: 18px; }

	/* Variants */
	.data-value.default {
		color: var(--anvil-fg-0, #e8eef5);
	}

	.data-value.accent {
		color: var(--anvil-accent, #00f0ff);
		text-shadow: 0 0 8px var(--anvil-accent, #00f0ff);
	}

	.data-value.success {
		color: var(--anvil-success, #00ff88);
		text-shadow: 0 0 8px var(--anvil-success, #00ff88);
	}

	.data-value.warning {
		color: var(--anvil-warning, #ffaa00);
		text-shadow: 0 0 8px var(--anvil-warning, #ffaa00);
	}

	.data-value.error {
		color: var(--anvil-error, #ff3366);
		text-shadow: 0 0 8px var(--anvil-error, #ff3366);
	}
</style>
