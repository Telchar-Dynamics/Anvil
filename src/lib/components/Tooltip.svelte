<script lang="ts">
	export let text: string;
	export let position: 'top' | 'bottom' | 'left' | 'right' = 'top';
	export let delay: number = 200;

	let visible = false;
	let timeout: ReturnType<typeof setTimeout>;

	function show() {
		timeout = setTimeout(() => {
			visible = true;
		}, delay);
	}

	function hide() {
		clearTimeout(timeout);
		visible = false;
	}
</script>

<div class="anvil-tooltip-wrapper" on:mouseenter={show} on:mouseleave={hide} on:focus={show} on:blur={hide}>
	<slot />
	{#if visible}
		<div class="anvil-tooltip {position}" role="tooltip">
			<span class="tooltip-text">{text}</span>
			<span class="tooltip-arrow"></span>
		</div>
	{/if}
</div>

<style>
	.anvil-tooltip-wrapper {
		position: relative;
		display: inline-block;
	}

	.anvil-tooltip {
		position: absolute;
		z-index: var(--anvil-z-tooltip, 1000);
		padding: var(--anvil-space-1, 0.25rem) var(--anvil-space-2, 0.5rem);
		background: var(--anvil-bg-2, #0e1319);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
		white-space: nowrap;
		pointer-events: none;
		animation: tooltip-fade-in 0.15s ease;
	}

	@keyframes tooltip-fade-in {
		from {
			opacity: 0;
			transform: scale(0.95);
		}
		to {
			opacity: 1;
			transform: scale(1);
		}
	}

	.tooltip-text {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 11px;
		color: var(--anvil-fg-1, #a8b5c4);
	}

	.tooltip-arrow {
		position: absolute;
		width: 6px;
		height: 6px;
		background: var(--anvil-bg-2, #0e1319);
		border: 1px solid var(--anvil-border, #1a242e);
		transform: rotate(45deg);
	}

	/* Positions */
	.anvil-tooltip.top {
		bottom: 100%;
		left: 50%;
		transform: translateX(-50%);
		margin-bottom: 8px;
	}

	.anvil-tooltip.top .tooltip-arrow {
		bottom: -4px;
		left: 50%;
		margin-left: -3px;
		border-top: none;
		border-left: none;
	}

	.anvil-tooltip.bottom {
		top: 100%;
		left: 50%;
		transform: translateX(-50%);
		margin-top: 8px;
	}

	.anvil-tooltip.bottom .tooltip-arrow {
		top: -4px;
		left: 50%;
		margin-left: -3px;
		border-bottom: none;
		border-right: none;
	}

	.anvil-tooltip.left {
		right: 100%;
		top: 50%;
		transform: translateY(-50%);
		margin-right: 8px;
	}

	.anvil-tooltip.left .tooltip-arrow {
		right: -4px;
		top: 50%;
		margin-top: -3px;
		border-left: none;
		border-bottom: none;
	}

	.anvil-tooltip.right {
		left: 100%;
		top: 50%;
		transform: translateY(-50%);
		margin-left: 8px;
	}

	.anvil-tooltip.right .tooltip-arrow {
		left: -4px;
		top: 50%;
		margin-top: -3px;
		border-right: none;
		border-top: none;
	}
</style>
