<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	type Tab = { id: string; label: string; disabled?: boolean };

	export let tabs: Tab[] = [];
	export let activeTab: string = tabs[0]?.id ?? '';
	export let variant: 'default' | 'pills' | 'underline' = 'default';

	const dispatch = createEventDispatcher<{ change: string }>();

	function selectTab(tabId: string) {
		const tab = tabs.find(t => t.id === tabId);
		if (tab && !tab.disabled) {
			activeTab = tabId;
			dispatch('change', tabId);
		}
	}
</script>

<div class="anvil-tabs {variant}">
	<div class="tabs-list" role="tablist">
		{#each tabs as tab}
			<button
				class="tab-item"
				class:active={activeTab === tab.id}
				class:disabled={tab.disabled}
				role="tab"
				aria-selected={activeTab === tab.id}
				disabled={tab.disabled}
				on:click={() => selectTab(tab.id)}
			>
				{tab.label}
			</button>
		{/each}
		{#if variant === 'default'}
			<div class="tab-indicator" style:--tab-count={tabs.length}></div>
		{/if}
	</div>
</div>

<div class="anvil-tab-content">
	<slot />
</div>

<style>
	.anvil-tabs {
		width: 100%;
	}

	.tabs-list {
		display: flex;
		position: relative;
		gap: 2px;
	}

	.tab-item {
		flex: 1;
		padding: var(--anvil-space-2, 0.5rem) var(--anvil-space-4, 1rem);
		background: transparent;
		border: none;
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		font-weight: 600;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
		cursor: pointer;
		transition: all var(--anvil-transition-fast, 100ms ease);
		position: relative;
		z-index: 1;
	}

	.tab-item:hover:not(.disabled) {
		color: var(--anvil-fg-1, #a8b5c4);
	}

	.tab-item.active {
		color: var(--anvil-accent, #00f0ff);
	}

	.tab-item.disabled {
		opacity: 0.4;
		cursor: not-allowed;
	}

	/* Default variant */
	.default .tabs-list {
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		padding: 2px;
	}

	.default .tab-item.active {
		background: var(--anvil-bg-2, #0e1319);
		border-radius: var(--anvil-radius-sm, 2px);
		box-shadow: 0 0 8px rgba(0, 240, 255, 0.2);
	}

	/* Pills variant */
	.pills .tabs-list {
		gap: var(--anvil-space-2, 0.5rem);
	}

	.pills .tab-item {
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
	}

	.pills .tab-item:hover:not(.disabled) {
		border-color: var(--anvil-accent, #00f0ff);
	}

	.pills .tab-item.active {
		background: var(--anvil-accent-dim, #00f0ff40);
		border-color: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 10px rgba(0, 240, 255, 0.2);
	}

	/* Underline variant */
	.underline .tabs-list {
		border-bottom: 1px solid var(--anvil-border, #1a242e);
	}

	.underline .tab-item {
		padding-bottom: var(--anvil-space-3, 0.75rem);
		margin-bottom: -1px;
	}

	.underline .tab-item.active::after {
		content: '';
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		height: 2px;
		background: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px var(--anvil-accent, #00f0ff);
	}

	.anvil-tab-content {
		padding: var(--anvil-space-4, 1rem) 0;
	}
</style>
