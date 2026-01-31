<script lang="ts">
	export let inline: boolean = false;
	export let language: string | undefined = undefined;
</script>

{#if inline}
	<code class="anvil-code inline"><slot /></code>
{:else}
	<div class="anvil-code-block">
		{#if language}
			<span class="code-language">{language}</span>
		{/if}
		<pre class="anvil-code"><code><slot /></code></pre>
	</div>
{/if}

<style>
	.anvil-code {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-0, #e8eef5);
		background: var(--anvil-bg-1, #0a0d12);
		tab-size: 2;
	}

	.anvil-code.inline {
		padding: 2px var(--anvil-space-1, 0.25rem);
		border-radius: var(--anvil-radius-sm, 2px);
		border: 1px solid var(--anvil-border, #1a242e);
	}

	.anvil-code-block {
		position: relative;
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		overflow: hidden;
	}

	.anvil-code-block pre {
		margin: 0;
		padding: var(--anvil-space-4, 1rem);
		overflow-x: auto;
	}

	.anvil-code-block code {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		line-height: 1.6;
		color: var(--anvil-fg-0, #e8eef5);
	}

	.code-language {
		position: absolute;
		top: var(--anvil-space-2, 0.5rem);
		right: var(--anvil-space-2, 0.5rem);
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.05em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted, #5a6a7a);
	}
</style>
