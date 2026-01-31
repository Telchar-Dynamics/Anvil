<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let variant: 'info' | 'success' | 'warning' | 'error' = 'info';
	export let title: string | undefined = undefined;
	export let dismissible: boolean = false;

	const dispatch = createEventDispatcher<{ dismiss: void }>();

	let visible = true;

	function dismiss() {
		visible = false;
		dispatch('dismiss');
	}

	const icons: Record<string, string> = {
		info: 'ℹ',
		success: '✓',
		warning: '⚠',
		error: '✕'
	};
</script>

{#if visible}
	<div class="anvil-alert {variant}" role="alert">
		<span class="alert-icon">{icons[variant]}</span>
		<div class="alert-content">
			{#if title}
				<strong class="alert-title">{title}</strong>
			{/if}
			<div class="alert-message"><slot /></div>
		</div>
		{#if dismissible}
			<button class="alert-dismiss" on:click={dismiss} aria-label="Dismiss">×</button>
		{/if}
	</div>
{/if}

<style>
	.anvil-alert {
		display: flex;
		align-items: flex-start;
		gap: var(--anvil-space-3, 0.75rem);
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		border-left-width: 3px;
	}

	.anvil-alert.info { border-left-color: var(--anvil-accent, #00f0ff); }
	.anvil-alert.success { border-left-color: var(--anvil-success, #00ff88); }
	.anvil-alert.warning { border-left-color: var(--anvil-warning, #ffaa00); }
	.anvil-alert.error { border-left-color: var(--anvil-error, #ff3366); }

	.alert-icon {
		flex-shrink: 0;
		width: 20px;
		height: 20px;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 12px;
		border-radius: 50%;
	}

	.info .alert-icon { background: rgba(0, 240, 255, 0.2); color: var(--anvil-accent, #00f0ff); }
	.success .alert-icon { background: rgba(0, 255, 136, 0.2); color: var(--anvil-success, #00ff88); }
	.warning .alert-icon { background: rgba(255, 170, 0, 0.2); color: var(--anvil-warning, #ffaa00); }
	.error .alert-icon { background: rgba(255, 51, 102, 0.2); color: var(--anvil-error, #ff3366); }

	.alert-content {
		flex: 1;
		min-width: 0;
	}

	.alert-title {
		display: block;
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		font-weight: 600;
		color: var(--anvil-fg-0, #e8eef5);
		margin-bottom: var(--anvil-space-1, 0.25rem);
	}

	.alert-message {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-1, #a8b5c4);
		line-height: 1.5;
	}

	.alert-dismiss {
		flex-shrink: 0;
		width: 24px;
		height: 24px;
		display: flex;
		align-items: center;
		justify-content: center;
		background: transparent;
		border: none;
		color: var(--anvil-fg-muted, #5a6a7a);
		font-size: 18px;
		cursor: pointer;
		transition: color var(--anvil-transition-fast, 100ms ease);
	}

	.alert-dismiss:hover {
		color: var(--anvil-fg-0, #e8eef5);
	}
</style>
