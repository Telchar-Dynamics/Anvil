<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	type Option = { value: string; label: string; disabled?: boolean };

	export let options: Option[] = [];
	export let value: string = '';
	export let placeholder: string = 'Select...';
	export let label: string | undefined = undefined;
	export let disabled: boolean = false;
	export let size: 'sm' | 'md' | 'lg' = 'md';

	const dispatch = createEventDispatcher<{ change: string }>();

	function handleChange(e: Event) {
		const target = e.target as HTMLSelectElement;
		value = target.value;
		dispatch('change', value);
	}
</script>

<div class="anvil-select-wrapper">
	{#if label}
		<label class="select-label">{label}</label>
	{/if}
	<div class="select-container {size}">
		<select
			class="anvil-select"
			{disabled}
			{value}
			on:change={handleChange}
		>
			{#if placeholder}
				<option value="" disabled selected={!value}>{placeholder}</option>
			{/if}
			{#each options as option}
				<option value={option.value} disabled={option.disabled}>
					{option.label}
				</option>
			{/each}
		</select>
		<span class="select-arrow">
			<svg width="10" height="6" viewBox="0 0 10 6" fill="currentColor">
				<path d="M0 0L5 6L10 0H0Z"/>
			</svg>
		</span>
	</div>
</div>

<style>
	.anvil-select-wrapper {
		display: flex;
		flex-direction: column;
		gap: 4px;
	}

	.select-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.08em;
		color: var(--anvil-fg-muted, #5a6a7a);
		text-transform: uppercase;
	}

	.select-container {
		position: relative;
		display: flex;
		align-items: center;
	}

	.anvil-select {
		width: 100%;
		padding: 0 var(--anvil-space-8, 2rem) 0 var(--anvil-space-3, 0.75rem);
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-0, #e8eef5);
		cursor: pointer;
		appearance: none;
		transition: border-color var(--anvil-transition-fast, 100ms ease),
		            box-shadow var(--anvil-transition-fast, 100ms ease);
	}

	.anvil-select:focus {
		outline: none;
		border-color: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px rgba(0, 240, 255, 0.2);
	}

	.anvil-select:disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	.select-arrow {
		position: absolute;
		right: var(--anvil-space-3, 0.75rem);
		pointer-events: none;
		color: var(--anvil-fg-muted, #5a6a7a);
		transition: color var(--anvil-transition-fast, 100ms ease);
	}

	.select-container:hover .select-arrow {
		color: var(--anvil-accent, #00f0ff);
	}

	/* Sizes */
	.sm .anvil-select { height: 28px; font-size: 11px; }
	.md .anvil-select { height: 32px; }
	.lg .anvil-select { height: 40px; font-size: 14px; }
</style>
