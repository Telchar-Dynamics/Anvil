<script lang="ts">
	export let size: 'sm' | 'md' | 'lg' | 'xl' = 'md';
	export let variant: 'default' | 'accent' | 'light' = 'accent';
	export let label: string | undefined = undefined;
</script>

<div class="anvil-spinner {size} {variant}">
	<svg class="spinner-svg" viewBox="0 0 50 50">
		<circle
			class="spinner-track"
			cx="25"
			cy="25"
			r="20"
			fill="none"
			stroke-width="4"
		/>
		<circle
			class="spinner-circle"
			cx="25"
			cy="25"
			r="20"
			fill="none"
			stroke-width="4"
			stroke-linecap="round"
		/>
	</svg>
	{#if label}
		<span class="spinner-label">{label}</span>
	{/if}
</div>

<style>
	.anvil-spinner {
		display: inline-flex;
		flex-direction: column;
		align-items: center;
		gap: var(--anvil-space-2, 0.5rem);
	}

	.spinner-svg {
		animation: spinner-rotate 1s linear infinite;
	}

	/* Sizes */
	.sm .spinner-svg { width: 16px; height: 16px; }
	.md .spinner-svg { width: 24px; height: 24px; }
	.lg .spinner-svg { width: 36px; height: 36px; }
	.xl .spinner-svg { width: 48px; height: 48px; }

	.spinner-track {
		stroke: var(--anvil-border, #1a242e);
	}

	.spinner-circle {
		stroke-dasharray: 90, 150;
		stroke-dashoffset: 0;
		animation: spinner-dash 1.5s ease-in-out infinite;
	}

	/* Variants */
	.default .spinner-circle {
		stroke: var(--anvil-fg-muted, #5a6a7a);
	}

	.accent .spinner-circle {
		stroke: var(--anvil-accent, #00f0ff);
		filter: drop-shadow(0 0 4px var(--anvil-accent, #00f0ff));
	}

	.light .spinner-circle {
		stroke: var(--anvil-fg-0, #e8eef5);
	}

	@keyframes spinner-rotate {
		100% { transform: rotate(360deg); }
	}

	@keyframes spinner-dash {
		0% {
			stroke-dasharray: 1, 150;
			stroke-dashoffset: 0;
		}
		50% {
			stroke-dasharray: 90, 150;
			stroke-dashoffset: -35;
		}
		100% {
			stroke-dasharray: 90, 150;
			stroke-dashoffset: -124;
		}
	}

	.spinner-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
	}
</style>
