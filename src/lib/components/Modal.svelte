<script lang="ts">
	import { createEventDispatcher, onMount, onDestroy } from 'svelte';
	import { fade, scale } from 'svelte/transition';
	import { browser } from '$app/environment';

	export let open: boolean = false;
	export let title: string | undefined = undefined;
	export let size: 'sm' | 'md' | 'lg' | 'full' = 'md';
	export let closable: boolean = true;

	const dispatch = createEventDispatcher<{ close: void }>();

	function handleClose() {
		if (closable) {
			dispatch('close');
		}
	}

	function handleKeydown(e: KeyboardEvent) {
		if (e.key === 'Escape' && open && closable) {
			handleClose();
		}
	}

	function handleBackdropClick(e: MouseEvent) {
		if (e.target === e.currentTarget) {
			handleClose();
		}
	}

	onMount(() => {
		if (browser) {
			document.addEventListener('keydown', handleKeydown);
		}
	});

	onDestroy(() => {
		if (browser) {
			document.removeEventListener('keydown', handleKeydown);
		}
	});
</script>

{#if open}
	<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
	<div
		class="anvil-modal-backdrop"
		on:click={handleBackdropClick}
		on:keydown
		role="dialog"
		aria-modal="true"
		transition:fade={{ duration: 150 }}
	>
		<div
			class="anvil-modal {size}"
			transition:scale={{ duration: 150, start: 0.95 }}
		>
			<div class="modal-corner tl"></div>
			<div class="modal-corner tr"></div>
			<div class="modal-corner bl"></div>
			<div class="modal-corner br"></div>

			{#if title || closable}
				<div class="modal-header">
					{#if title}
						<h2 class="modal-title">{title}</h2>
					{:else}
						<div></div>
					{/if}
					{#if closable}
						<button class="modal-close" on:click={handleClose} aria-label="Close">
							<svg width="14" height="14" viewBox="0 0 14 14" fill="none" stroke="currentColor" stroke-width="2">
								<path d="M1 1L13 13M13 1L1 13"/>
							</svg>
						</button>
					{/if}
				</div>
			{/if}

			<div class="modal-content">
				<slot />
			</div>

			{#if $$slots.footer}
				<div class="modal-footer">
					<slot name="footer" />
				</div>
			{/if}
		</div>
	</div>
{/if}

<style>
	.anvil-modal-backdrop {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: rgba(0, 0, 0, 0.8);
		backdrop-filter: blur(4px);
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: var(--anvil-z-modal, 300);
		padding: var(--anvil-space-4, 1rem);
	}

	.anvil-modal {
		position: relative;
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-md, 4px);
		max-height: 90vh;
		display: flex;
		flex-direction: column;
		box-shadow: var(--anvil-shadow-lg, 0 4px 16px rgba(0, 0, 0, 0.7)),
		            0 0 40px rgba(0, 240, 255, 0.1);
	}

	/* Sizes */
	.sm { width: 320px; }
	.md { width: 480px; }
	.lg { width: 640px; }
	.full { width: calc(100vw - 2rem); height: calc(100vh - 2rem); }

	/* Corner brackets */
	.modal-corner {
		position: absolute;
		width: 12px;
		height: 12px;
		border-color: var(--anvil-accent, #00f0ff);
		border-style: solid;
		opacity: 0.6;
		pointer-events: none;
	}

	.modal-corner.tl { top: -1px; left: -1px; border-width: 2px 0 0 2px; }
	.modal-corner.tr { top: -1px; right: -1px; border-width: 2px 2px 0 0; }
	.modal-corner.bl { bottom: -1px; left: -1px; border-width: 0 0 2px 2px; }
	.modal-corner.br { bottom: -1px; right: -1px; border-width: 0 2px 2px 0; }

	.modal-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		border-bottom: 1px solid var(--anvil-border, #1a242e);
		background: var(--anvil-bg-2, #0e1319);
	}

	.modal-title {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		font-weight: 600;
		letter-spacing: 0.1em;
		text-transform: uppercase;
		color: var(--anvil-fg-0, #e8eef5);
		margin: 0;
	}

	.modal-close {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 28px;
		height: 28px;
		background: transparent;
		border: 1px solid transparent;
		border-radius: var(--anvil-radius-sm, 2px);
		color: var(--anvil-fg-muted, #5a6a7a);
		cursor: pointer;
		transition: all var(--anvil-transition-fast, 100ms ease);
	}

	.modal-close:hover {
		background: var(--anvil-bg-3, #141a22);
		border-color: var(--anvil-border, #1a242e);
		color: var(--anvil-fg-0, #e8eef5);
	}

	.modal-content {
		flex: 1;
		overflow-y: auto;
		padding: var(--anvil-space-4, 1rem);
	}

	.modal-footer {
		display: flex;
		justify-content: flex-end;
		gap: var(--anvil-space-2, 0.5rem);
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		border-top: 1px solid var(--anvil-border, #1a242e);
		background: var(--anvil-bg-2, #0e1319);
	}
</style>
