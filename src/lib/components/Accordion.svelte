<script lang="ts">
	import { slide } from 'svelte/transition';

	export let title: string;
	export let open: boolean = false;
	export let disabled: boolean = false;

	function toggle() {
		if (!disabled) {
			open = !open;
		}
	}
</script>

<div class="anvil-accordion" class:open class:disabled>
	<button class="accordion-header" on:click={toggle} {disabled}>
		<span class="accordion-title">{title}</span>
		<span class="accordion-icon">
			<svg width="10" height="6" viewBox="0 0 10 6" fill="currentColor">
				<path d="M0 0L5 6L10 0H0Z"/>
			</svg>
		</span>
	</button>
	{#if open}
		<div class="accordion-content" transition:slide={{ duration: 150 }}>
			<slot />
		</div>
	{/if}
</div>

<style>
	.anvil-accordion {
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		overflow: hidden;
	}

	.anvil-accordion.disabled {
		opacity: 0.5;
	}

	.accordion-header {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		background: transparent;
		border: none;
		cursor: pointer;
		transition: background var(--anvil-transition-fast, 100ms ease);
	}

	.accordion-header:hover:not(:disabled) {
		background: var(--anvil-bg-2, #0e1319);
	}

	.accordion-header:disabled {
		cursor: not-allowed;
	}

	.accordion-title {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		font-weight: 600;
		color: var(--anvil-fg-0, #e8eef5);
		text-align: left;
	}

	.accordion-icon {
		color: var(--anvil-fg-muted, #5a6a7a);
		transition: transform var(--anvil-transition-fast, 100ms ease);
	}

	.open .accordion-icon {
		transform: rotate(180deg);
	}

	.accordion-content {
		padding: var(--anvil-space-4, 1rem);
		border-top: 1px solid var(--anvil-border, #1a242e);
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-1, #a8b5c4);
	}
</style>
