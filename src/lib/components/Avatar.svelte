<script lang="ts">
	export let src: string | undefined = undefined;
	export let alt: string = '';
	export let initials: string | undefined = undefined;
	export let size: 'xs' | 'sm' | 'md' | 'lg' | 'xl' = 'md';
	export let status: 'online' | 'offline' | 'busy' | 'away' | undefined = undefined;
</script>

<div class="anvil-avatar {size}">
	{#if src}
		<img {src} {alt} class="avatar-image" />
	{:else if initials}
		<span class="avatar-initials">{initials.slice(0, 2).toUpperCase()}</span>
	{:else}
		<span class="avatar-placeholder">
			<svg viewBox="0 0 24 24" fill="currentColor">
				<path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
			</svg>
		</span>
	{/if}
	{#if status}
		<span class="avatar-status {status}"></span>
	{/if}
</div>

<style>
	.anvil-avatar {
		position: relative;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		background: var(--anvil-bg-2, #0e1319);
		border: 1px solid var(--anvil-border, #1a242e);
		border-radius: 50%;
		overflow: hidden;
	}

	.xs { width: 24px; height: 24px; }
	.sm { width: 32px; height: 32px; }
	.md { width: 40px; height: 40px; }
	.lg { width: 56px; height: 56px; }
	.xl { width: 72px; height: 72px; }

	.avatar-image {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.avatar-initials {
		font-family: var(--anvil-font-mono, monospace);
		font-weight: 600;
		color: var(--anvil-accent, #00f0ff);
	}

	.xs .avatar-initials { font-size: 10px; }
	.sm .avatar-initials { font-size: 12px; }
	.md .avatar-initials { font-size: 14px; }
	.lg .avatar-initials { font-size: 18px; }
	.xl .avatar-initials { font-size: 24px; }

	.avatar-placeholder {
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--anvil-fg-muted, #5a6a7a);
	}

	.avatar-placeholder svg {
		width: 60%;
		height: 60%;
	}

	.avatar-status {
		position: absolute;
		bottom: 0;
		right: 0;
		border-radius: 50%;
		border: 2px solid var(--anvil-bg-0, #060809);
	}

	.xs .avatar-status { width: 8px; height: 8px; }
	.sm .avatar-status { width: 10px; height: 10px; }
	.md .avatar-status { width: 12px; height: 12px; }
	.lg .avatar-status { width: 14px; height: 14px; }
	.xl .avatar-status { width: 16px; height: 16px; }

	.avatar-status.online { background: var(--anvil-success, #00ff88); box-shadow: 0 0 6px var(--anvil-success, #00ff88); }
	.avatar-status.offline { background: var(--anvil-fg-muted, #5a6a7a); }
	.avatar-status.busy { background: var(--anvil-error, #ff3366); box-shadow: 0 0 6px var(--anvil-error, #ff3366); }
	.avatar-status.away { background: var(--anvil-warning, #ffaa00); box-shadow: 0 0 6px var(--anvil-warning, #ffaa00); }
</style>
