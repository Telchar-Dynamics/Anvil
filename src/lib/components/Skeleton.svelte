<script lang="ts">
	export let variant: 'text' | 'circular' | 'rectangular' = 'text';
	export let width: string | undefined = undefined;
	export let height: string | undefined = undefined;
	export let lines: number = 1;
</script>

{#if variant === 'text' && lines > 1}
	<div class="anvil-skeleton-lines">
		{#each Array(lines) as _, i}
			<div
				class="anvil-skeleton text"
				style:width={i === lines - 1 ? '75%' : width ?? '100%'}
				style:height={height}
			></div>
		{/each}
	</div>
{:else}
	<div
		class="anvil-skeleton {variant}"
		style:width={width}
		style:height={height}
	></div>
{/if}

<style>
	.anvil-skeleton {
		background: linear-gradient(
			90deg,
			var(--anvil-bg-1, #0a0d12) 25%,
			var(--anvil-bg-2, #0e1319) 50%,
			var(--anvil-bg-1, #0a0d12) 75%
		);
		background-size: 200% 100%;
		animation: skeleton-shimmer 1.5s ease-in-out infinite;
	}

	@keyframes skeleton-shimmer {
		0% { background-position: 200% 0; }
		100% { background-position: -200% 0; }
	}

	.anvil-skeleton.text {
		height: 1em;
		border-radius: var(--anvil-radius-sm, 2px);
	}

	.anvil-skeleton.circular {
		width: 40px;
		height: 40px;
		border-radius: 50%;
	}

	.anvil-skeleton.rectangular {
		width: 100%;
		height: 100px;
		border-radius: var(--anvil-radius-sm, 2px);
	}

	.anvil-skeleton-lines {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-2, 0.5rem);
	}
</style>
