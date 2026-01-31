<script lang="ts" context="module">
	export type ToastType = 'info' | 'success' | 'warning' | 'error';
	export type ToastPosition = 'top-right' | 'top-left' | 'bottom-right' | 'bottom-left' | 'top-center' | 'bottom-center';

	export interface ToastItem {
		id: string;
		message: string;
		type: ToastType;
		duration?: number;
	}
</script>

<script lang="ts">
	import { fly, fade } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	export let toasts: ToastItem[] = [];
	export let position: ToastPosition = 'top-right';

	function dismiss(id: string) {
		toasts = toasts.filter(t => t.id !== id);
	}

	function getIcon(type: ToastType): string {
		switch (type) {
			case 'success': return '✓';
			case 'warning': return '⚠';
			case 'error': return '✕';
			default: return 'ℹ';
		}
	}
</script>

<div class="anvil-toast-container {position}">
	{#each toasts as toast (toast.id)}
		<div
			class="anvil-toast {toast.type}"
			animate:flip={{ duration: 200 }}
			in:fly={{ y: position.startsWith('top') ? -20 : 20, duration: 200 }}
			out:fade={{ duration: 150 }}
		>
			<span class="toast-icon">{getIcon(toast.type)}</span>
			<span class="toast-message">{toast.message}</span>
			<button class="toast-close" on:click={() => dismiss(toast.id)}>×</button>
		</div>
	{/each}
</div>

<style>
	.anvil-toast-container {
		position: fixed;
		z-index: var(--anvil-z-toast, 2000);
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-2, 0.5rem);
		padding: var(--anvil-space-4, 1rem);
		pointer-events: none;
	}

	/* Positions */
	.top-right { top: 0; right: 0; align-items: flex-end; }
	.top-left { top: 0; left: 0; align-items: flex-start; }
	.bottom-right { bottom: 0; right: 0; align-items: flex-end; }
	.bottom-left { bottom: 0; left: 0; align-items: flex-start; }
	.top-center { top: 0; left: 50%; transform: translateX(-50%); align-items: center; }
	.bottom-center { bottom: 0; left: 50%; transform: translateX(-50%); align-items: center; }

	.anvil-toast {
		display: flex;
		align-items: center;
		gap: var(--anvil-space-2, 0.5rem);
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		background: var(--anvil-bg-2, #0e1319);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		box-shadow: 0 4px 16px rgba(0, 0, 0, 0.4);
		pointer-events: all;
		max-width: 360px;
	}

	.toast-icon {
		flex-shrink: 0;
		width: 18px;
		height: 18px;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 12px;
		border-radius: 50%;
	}

	.toast-message {
		flex: 1;
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-1, #a8b5c4);
	}

	.toast-close {
		flex-shrink: 0;
		width: 20px;
		height: 20px;
		display: flex;
		align-items: center;
		justify-content: center;
		background: transparent;
		border: none;
		color: var(--anvil-fg-muted, #5a6a7a);
		cursor: pointer;
		font-size: 16px;
		padding: 0;
		transition: color var(--anvil-transition-fast, 100ms ease);
	}

	.toast-close:hover {
		color: var(--anvil-fg-0, #e8eef5);
	}

	/* Types */
	.anvil-toast.info {
		border-left: 3px solid var(--anvil-accent, #00f0ff);
	}
	.anvil-toast.info .toast-icon {
		background: var(--anvil-accent-dim, #00f0ff40);
		color: var(--anvil-accent, #00f0ff);
	}

	.anvil-toast.success {
		border-left: 3px solid var(--anvil-success, #00ff88);
	}
	.anvil-toast.success .toast-icon {
		background: rgba(0, 255, 136, 0.2);
		color: var(--anvil-success, #00ff88);
	}

	.anvil-toast.warning {
		border-left: 3px solid var(--anvil-warning, #ffaa00);
	}
	.anvil-toast.warning .toast-icon {
		background: rgba(255, 170, 0, 0.2);
		color: var(--anvil-warning, #ffaa00);
	}

	.anvil-toast.error {
		border-left: 3px solid var(--anvil-error, #ff3366);
	}
	.anvil-toast.error .toast-icon {
		background: rgba(255, 51, 102, 0.2);
		color: var(--anvil-error, #ff3366);
	}
</style>
