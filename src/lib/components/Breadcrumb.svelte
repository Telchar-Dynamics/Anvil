<script lang="ts">
	type BreadcrumbItem = {
		label: string;
		href?: string;
	};

	export let items: BreadcrumbItem[] = [];
	export let separator: string = '/';
</script>

<nav class="anvil-breadcrumb" aria-label="Breadcrumb">
	<ol class="breadcrumb-list">
		{#each items as item, i}
			<li class="breadcrumb-item">
				{#if item.href && i < items.length - 1}
					<a href={item.href} class="breadcrumb-link">{item.label}</a>
				{:else}
					<span class="breadcrumb-current" aria-current={i === items.length - 1 ? 'page' : undefined}>
						{item.label}
					</span>
				{/if}
			</li>
			{#if i < items.length - 1}
				<li class="breadcrumb-separator" aria-hidden="true">{separator}</li>
			{/if}
		{/each}
	</ol>
</nav>

<style>
	.anvil-breadcrumb {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
	}

	.breadcrumb-list {
		display: flex;
		align-items: center;
		gap: var(--anvil-space-2, 0.5rem);
		list-style: none;
		margin: 0;
		padding: 0;
	}

	.breadcrumb-link {
		color: var(--anvil-fg-muted, #5a6a7a);
		text-decoration: none;
		transition: color var(--anvil-transition-fast, 100ms ease);
	}

	.breadcrumb-link:hover {
		color: var(--anvil-accent, #00f0ff);
	}

	.breadcrumb-current {
		color: var(--anvil-fg-0, #e8eef5);
		font-weight: 600;
	}

	.breadcrumb-separator {
		color: var(--anvil-fg-muted, #5a6a7a);
	}
</style>
