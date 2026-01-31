<script lang="ts">
	type Column = {
		key: string;
		label: string;
		width?: string;
		align?: 'left' | 'center' | 'right';
	};

	export let columns: Column[] = [];
	export let data: Record<string, unknown>[] = [];
	export let striped: boolean = true;
	export let hoverable: boolean = true;
	export let compact: boolean = false;
</script>

<div class="anvil-table-wrapper">
	<table class="anvil-table" class:striped class:hoverable class:compact>
		<thead>
			<tr>
				{#each columns as col}
					<th style:width={col.width} style:text-align={col.align ?? 'left'}>
						{col.label}
					</th>
				{/each}
			</tr>
		</thead>
		<tbody>
			{#each data as row, i}
				<tr>
					{#each columns as col}
						<td style:text-align={col.align ?? 'left'}>
							{row[col.key] ?? '—'}
						</td>
					{/each}
				</tr>
			{/each}
			{#if data.length === 0}
				<tr class="empty-row">
					<td colspan={columns.length}>
						<span class="empty-message">No data available</span>
					</td>
				</tr>
			{/if}
		</tbody>
	</table>
</div>

<style>
	.anvil-table-wrapper {
		width: 100%;
		overflow-x: auto;
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		background: var(--anvil-bg-1, #0a0d12);
	}

	.anvil-table {
		width: 100%;
		border-collapse: collapse;
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
	}

	thead {
		background: var(--anvil-bg-2, #0e1319);
		border-bottom: 1px solid var(--anvil-border, #1a242e);
	}

	th {
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
		text-align: left;
	}

	td {
		padding: var(--anvil-space-3, 0.75rem) var(--anvil-space-4, 1rem);
		color: var(--anvil-fg-1, #a8b5c4);
		border-bottom: 1px solid var(--anvil-border, #1a242e);
	}

	tbody tr:last-child td {
		border-bottom: none;
	}

	/* Compact */
	.compact th,
	.compact td {
		padding: var(--anvil-space-2, 0.5rem) var(--anvil-space-3, 0.75rem);
	}

	/* Striped */
	.striped tbody tr:nth-child(even) {
		background: rgba(0, 0, 0, 0.2);
	}

	/* Hoverable */
	.hoverable tbody tr:hover {
		background: rgba(0, 240, 255, 0.05);
	}

	/* Empty state */
	.empty-row td {
		text-align: center;
		padding: var(--anvil-space-6, 1.5rem);
	}

	.empty-message {
		color: var(--anvil-fg-muted, #5a6a7a);
		font-style: italic;
	}
</style>
