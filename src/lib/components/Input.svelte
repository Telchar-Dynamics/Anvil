<script lang="ts">
	export let value: string = '';
	export let type: 'text' | 'number' | 'password' | 'email' | 'search' = 'text';
	export let placeholder: string = '';
	export let label: string | undefined = undefined;
	export let disabled: boolean = false;
	export let error: string | undefined = undefined;
	export let size: 'sm' | 'md' | 'lg' = 'md';
	export let id: string = `input-${Math.random().toString(36).slice(2, 9)}`;

	function handleInput(e: Event) {
		value = (e.target as HTMLInputElement).value;
	}
</script>

<div class="anvil-input-wrapper" class:has-error={!!error}>
	{#if label}
		<label class="input-label" for={id}>{label}</label>
	{/if}
	{#if type === 'number'}
		<input
			{id}
			class="anvil-input {size}"
			type="number"
			{placeholder}
			{disabled}
			{value}
			on:input={handleInput}
			on:input
			on:focus
			on:blur
			on:keydown
		/>
	{:else if type === 'password'}
		<input
			{id}
			class="anvil-input {size}"
			type="password"
			{placeholder}
			{disabled}
			{value}
			on:input={handleInput}
			on:input
			on:focus
			on:blur
			on:keydown
		/>
	{:else if type === 'email'}
		<input
			{id}
			class="anvil-input {size}"
			type="email"
			{placeholder}
			{disabled}
			{value}
			on:input={handleInput}
			on:input
			on:focus
			on:blur
			on:keydown
		/>
	{:else if type === 'search'}
		<input
			{id}
			class="anvil-input {size}"
			type="search"
			{placeholder}
			{disabled}
			{value}
			on:input={handleInput}
			on:input
			on:focus
			on:blur
			on:keydown
		/>
	{:else}
		<input
			{id}
			class="anvil-input {size}"
			type="text"
			{placeholder}
			{disabled}
			{value}
			on:input={handleInput}
			on:input
			on:focus
			on:blur
			on:keydown
		/>
	{/if}
	{#if error}
		<span class="input-error">{error}</span>
	{/if}
</div>

<style>
	.anvil-input-wrapper {
		display: flex;
		flex-direction: column;
		gap: 4px;
	}

	.input-label {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.08em;
		color: var(--anvil-fg-muted, #5a6a7a);
		text-transform: uppercase;
	}

	.anvil-input {
		width: 100%;
		padding: 0 var(--anvil-space-3, 0.75rem);
		background: var(--anvil-bg-1, #0a0d12);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: var(--anvil-radius-sm, 2px);
		font-family: var(--anvil-font-mono, monospace);
		font-size: 12px;
		color: var(--anvil-fg-0, #e8eef5);
		transition: border-color var(--anvil-transition-fast, 100ms ease),
		            box-shadow var(--anvil-transition-fast, 100ms ease);
	}

	.anvil-input::placeholder {
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.anvil-input:focus {
		outline: none;
		border-color: var(--anvil-accent, #00f0ff);
		box-shadow: 0 0 8px rgba(0, 240, 255, 0.2);
	}

	.anvil-input:disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	.has-error .anvil-input {
		border-color: var(--anvil-error, #ff3366);
	}

	.has-error .anvil-input:focus {
		box-shadow: 0 0 8px rgba(255, 51, 102, 0.2);
	}

	/* Sizes */
	.sm {
		height: 28px;
		font-size: 11px;
	}

	.md {
		height: 32px;
	}

	.lg {
		height: 40px;
		font-size: 14px;
	}

	.input-error {
		font-family: var(--anvil-font-mono, monospace);
		font-size: 10px;
		color: var(--anvil-error, #ff3366);
	}
</style>
