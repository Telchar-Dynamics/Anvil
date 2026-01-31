<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let value: number = 0;
	export let min: number = 0;
	export let max: number = 100;
	export let step: number = 1;
	export let disabled: boolean = false;
	export let showValue: boolean = false;
	export let label: string | undefined = undefined;

	const dispatch = createEventDispatcher<{ change: number }>();

	$: percentage = ((value - min) / (max - min)) * 100;

	function handleInput(e: Event) {
		const target = e.target as HTMLInputElement;
		value = parseFloat(target.value);
		dispatch('change', value);
	}
</script>

<div class="anvil-slider" class:disabled>
	{#if label}
		<div class="slider-header">
			<span class="slider-label">{label}</span>
			{#if showValue}
				<span class="slider-value">{value}</span>
			{/if}
		</div>
	{/if}
	<div class="slider-track-wrapper">
		<input
			type="range"
			class="slider-input"
			{min}
			{max}
			{step}
			{disabled}
			{value}
			on:input={handleInput}
			style:--slider-percentage="{percentage}%"
		/>
		<div class="slider-track">
			<div class="slider-fill" style:width="{percentage}%"></div>
		</div>
	</div>
	{#if !label && showValue}
		<span class="slider-value standalone">{value}</span>
	{/if}
</div>

<style>
	.anvil-slider {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-2, 0.5rem);
		width: 100%;
	}

	.anvil-slider.disabled {
		opacity: 0.5;
	}

	.slider-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.slider-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.slider-value {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		font-weight: 600;
		color: var(--anvil-accent, #00f0ff);
	}

	.slider-value.standalone {
		align-self: flex-end;
		margin-top: calc(-1 * var(--anvil-space-1, 0.25rem));
	}

	.slider-track-wrapper {
		position: relative;
		height: 20px;
		display: flex;
		align-items: center;
	}

	.slider-input {
		position: absolute;
		width: 100%;
		height: 100%;
		margin: 0;
		opacity: 0;
		cursor: pointer;
		z-index: 2;
	}

	.slider-input:disabled {
		cursor: not-allowed;
	}

	.slider-track {
		width: 100%;
		height: 4px;
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: 2px;
		overflow: hidden;
	}

	.slider-fill {
		height: 100%;
		background: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px var(--anvil-accent, #00f0ff);
		transition: width 0.1s ease;
	}

	/* Thumb styling via pseudo track */
	.slider-track-wrapper::after {
		content: '';
		position: absolute;
		left: calc(var(--slider-percentage, 0%) - 6px);
		width: 12px;
		height: 12px;
		background: var(--anvil-accent, #00f0ff);
		border-radius: 50%;
		box-shadow: 0 0 10px var(--anvil-accent, #00f0ff);
		pointer-events: none;
		transition: transform 0.1s ease;
		z-index: 1;
	}

	.slider-input:focus + .slider-track {
		border-color: var(--anvil-accent, #00f0ff);
	}

	.slider-input:hover ~ .slider-track-wrapper::after,
	.slider-input:focus ~ .slider-track-wrapper::after {
		transform: scale(1.2);
	}
</style>
