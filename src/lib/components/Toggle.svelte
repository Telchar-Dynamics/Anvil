<script lang="ts">
	export let checked: boolean = false;
	export let label: string | undefined = undefined;
	export let disabled: boolean = false;
</script>

<label class="anvil-toggle" class:disabled>
	<input type="checkbox" bind:checked {disabled} on:change />
	<span class="toggle-indicator"></span>
	{#if label}
		<span class="toggle-label">{label}</span>
	{/if}
	<slot />
</label>

<style>
	.anvil-toggle {
		display: flex;
		align-items: center;
		gap: 8px;
		cursor: pointer;
		padding: 4px;
		border-radius: var(--anvil-radius-sm, 2px);
		transition: background var(--anvil-transition-fast, 100ms ease);
	}

	.anvil-toggle:hover {
		background: var(--anvil-bg-1, #0a0d12);
	}

	.anvil-toggle.disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	.anvil-toggle.disabled:hover {
		background: transparent;
	}

	.anvil-toggle input {
		display: none;
	}

	.toggle-indicator {
		width: 14px;
		height: 14px;
		border: 2px solid var(--anvil-fg-muted, #5a6a7a);
		border-radius: 2px;
		transition: all var(--anvil-transition-fast, 100ms ease);
		position: relative;
		flex-shrink: 0;
	}

	.anvil-toggle input:checked + .toggle-indicator {
		border-color: var(--anvil-accent, #00f0ff);
		background: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px var(--anvil-accent, #00f0ff);
	}

	.anvil-toggle input:checked + .toggle-indicator::after {
		content: '';
		position: absolute;
		left: 3px;
		top: 0px;
		width: 4px;
		height: 8px;
		border: solid var(--anvil-bg-0, #050608);
		border-width: 0 2px 2px 0;
		transform: rotate(45deg);
	}

	.toggle-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		color: var(--anvil-fg-1, #a8b5c4);
	}
</style>
