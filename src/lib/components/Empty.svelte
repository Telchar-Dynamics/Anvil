<script lang="ts">
	export let title: string = 'No data';
	export let description: string | undefined = undefined;
	export let icon: 'inbox' | 'search' | 'error' | 'none' = 'inbox';
</script>

<div class="anvil-empty">
	{#if icon !== 'none'}
		<div class="empty-icon">
			{#if icon === 'inbox'}
				<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
					<path d="M20 6L12 2L4 6v6c0 5.55 3.84 10.74 8 12 4.16-1.26 8-6.45 8-12V6z"/>
				</svg>
			{:else if icon === 'search'}
				<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
					<circle cx="11" cy="11" r="7"/>
					<path d="M21 21l-4.35-4.35"/>
				</svg>
			{:else if icon === 'error'}
				<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
					<circle cx="12" cy="12" r="10"/>
					<path d="M12 8v4M12 16h.01"/>
				</svg>
			{/if}
		</div>
	{/if}
	<p class="empty-title">{title}</p>
	{#if description}
		<p class="empty-description">{description}</p>
	{/if}
	{#if $$slots.default}
		<div class="empty-action">
			<slot />
		</div>
	{/if}
</div>

<style>
	.anvil-empty {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: var(--anvil-space-8, 2rem);
		text-align: center;
	}

	.empty-icon {
		width: 48px;
		height: 48px;
		margin-bottom: var(--anvil-space-4, 1rem);
		color: var(--anvil-fg-muted, #5a6a7a);
		opacity: 0.5;
	}

	.empty-icon svg {
		width: 100%;
		height: 100%;
	}

	.empty-title {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 14px;
		font-weight: 600;
		color: var(--anvil-fg-1, #a8b5c4);
		margin: 0 0 var(--anvil-space-2, 0.5rem);
	}

	.empty-description {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-muted, #5a6a7a);
		margin: 0;
		max-width: 280px;
	}

	.empty-action {
		margin-top: var(--anvil-space-4, 1rem);
	}
</style>
