<script lang="ts">
	export let label: string | undefined = undefined;
	export let variant: 'default' | 'accent' = 'default';
</script>

{#if label}
	<div class="anvil-divider labeled {variant}">
		<span class="divider-line"></span>
		<span class="divider-label">{label}</span>
		<span class="divider-line"></span>
	</div>
{:else}
	<div class="anvil-divider {variant}"></div>
{/if}

<style>
	.anvil-divider {
		height: 1px;
		background: var(--anvil-border, #1a242e);
		margin: var(--anvil-space-2, 0.5rem) 0;
	}

	.anvil-divider.accent {
		background: linear-gradient(
			90deg,
			transparent,
			var(--anvil-accent, #00f0ff) 20%,
			var(--anvil-accent, #00f0ff) 80%,
			transparent
		);
		opacity: 0.3;
	}

	.anvil-divider.labeled {
		display: flex;
		align-items: center;
		gap: var(--anvil-space-2, 0.5rem);
		height: auto;
		background: transparent;
	}

	.divider-line {
		flex: 1;
		height: 1px;
		background: var(--anvil-border, #1a242e);
	}

	.anvil-divider.labeled.accent .divider-line {
		background: var(--anvil-accent, #00f0ff);
		opacity: 0.3;
	}

	.divider-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 9px;
		font-weight: 600;
		letter-spacing: 0.12em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.anvil-divider.labeled.accent .divider-label {
		color: var(--anvil-accent, #00f0ff);
	}
</style>
