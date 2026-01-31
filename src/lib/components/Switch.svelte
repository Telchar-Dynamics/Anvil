<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let checked: boolean = false;
	export let disabled: boolean = false;
	export let size: 'sm' | 'md' | 'lg' = 'md';
	export let label: string | undefined = undefined;
	export let labelPosition: 'left' | 'right' = 'right';

	const dispatch = createEventDispatcher<{ change: boolean }>();

	function toggle() {
		if (!disabled) {
			checked = !checked;
			dispatch('change', checked);
		}
	}
</script>

<label class="anvil-switch {size}" class:disabled class:label-left={labelPosition === 'left'}>
	{#if label && labelPosition === 'left'}
		<span class="switch-label">{label}</span>
	{/if}
	<button
		type="button"
		class="switch-track"
		class:checked
		{disabled}
		role="switch"
		aria-checked={checked}
		on:click={toggle}
	>
		<span class="switch-thumb"></span>
	</button>
	{#if label && labelPosition === 'right'}
		<span class="switch-label">{label}</span>
	{/if}
</label>

<style>
	.anvil-switch {
		display: inline-flex;
		align-items: center;
		gap: var(--anvil-space-2, 0.5rem);
		cursor: pointer;
	}

	.anvil-switch.disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	.anvil-switch.label-left {
		flex-direction: row;
	}

	.switch-track {
		position: relative;
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: 999px;
		cursor: inherit;
		transition: all var(--anvil-transition-fast, 100ms ease);
	}

	.switch-track:focus {
		outline: none;
		border-color: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px rgba(0, 240, 255, 0.2);
	}

	.switch-track.checked {
		background: var(--anvil-accent-dim, #00f0ff40);
		border-color: var(--anvil-accent, #00f0ff);
	}

	.switch-thumb {
		position: absolute;
		top: 2px;
		left: 2px;
		background: var(--anvil-fg-muted, #5a6a7a);
		border-radius: 50%;
		transition: all var(--anvil-transition-fast, 100ms ease);
	}

	.switch-track.checked .switch-thumb {
		background: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px var(--anvil-accent, #00f0ff);
	}

	/* Sizes */
	.sm .switch-track { width: 28px; height: 16px; }
	.sm .switch-thumb { width: 10px; height: 10px; }
	.sm .switch-track.checked .switch-thumb { transform: translateX(12px); }

	.md .switch-track { width: 36px; height: 20px; }
	.md .switch-thumb { width: 14px; height: 14px; }
	.md .switch-track.checked .switch-thumb { transform: translateX(16px); }

	.lg .switch-track { width: 44px; height: 24px; }
	.lg .switch-thumb { width: 18px; height: 18px; }
	.lg .switch-track.checked .switch-thumb { transform: translateX(20px); }

	.switch-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		color: var(--anvil-fg-1, #a8b5c4);
	}
</style>
