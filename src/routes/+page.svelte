<script lang="ts">
	import '$lib/styles/anvil.css';
	import '$lib/styles/fonts.css';
	import { onMount } from 'svelte';
	import {
		Button,
		Card,
		Badge,
		Panel,
		Input,
		Select,
		Toggle,
		Switch,
		Slider,
		Divider,
		DataValue,
		Indicator,
		Progress,
		Spinner,
		Tabs,
		Table,
		Modal,
		Tooltip,
		Toast
	} from '$lib';
	import type { ToastItem } from '$lib';

	// Form state
	let inputValue = '';
	let toggleChecked = true;
	let switchChecked = false;
	let sliderValue = 50;
	let selectValue = 'option1';

	// Font loading - only load what's needed
	const fontUrls: Record<string, string> = {
		default: 'https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;500;600;700&family=Share+Tech+Mono&display=swap',
		orbitron: 'https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;600;700;800;900&family=Space+Mono:wght@400;700&display=swap',
		military: 'https://fonts.googleapis.com/css2?family=Black+Ops+One&family=VT323&family=Rajdhani:wght@400;500;600;700&display=swap',
		modern: 'https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap',
		tech: 'https://fonts.googleapis.com/css2?family=Oxanium:wght@400;500;600;700&family=Fira+Code:wght@400;500;600&display=swap',
		geist: 'https://fonts.googleapis.com/css2?family=Geist:wght@400;500;600;700&family=Geist+Mono:wght@400;500;600&display=swap'
	};
	const loadedFonts = new Set<string>();
	let mounted = false;

	function loadFont(theme: string) {
		if (!mounted || theme === 'system' || loadedFonts.has(theme)) return;
		const url = fontUrls[theme];
		if (!url) return;

		const link = document.createElement('link');
		link.rel = 'stylesheet';
		link.href = url;
		document.head.appendChild(link);
		loadedFonts.add(theme);
	}

	// Font theme state
	let fontTheme = 'default';
	let disableMono = false;
	$: if (mounted) loadFont(fontTheme);

	const fontThemes = [
		{ value: 'default', label: 'Default (Rajdhani)' },
		{ value: 'orbitron', label: 'Orbitron' },
		{ value: 'military', label: 'Military (Black Ops)' },
		{ value: 'modern', label: 'Modern (Inter)' },
		{ value: 'tech', label: 'Tech (Oxanium)' },
		{ value: 'geist', label: 'Geist' },
		{ value: 'system', label: 'System' }
	];

	// Modal state
	let showModal = false;

	// Tab state
	let activeTab = 'overview';
	const tabs = [
		{ id: 'overview', label: 'Overview' },
		{ id: 'controls', label: 'Controls' },
		{ id: 'feedback', label: 'Feedback' }
	];

	// Progress animation
	let progressValue = 0;

	onMount(() => {
		mounted = true;
		loadFont(fontTheme);
		const interval = setInterval(() => {
			progressValue = (progressValue + 1) % 101;
		}, 50);
		return () => clearInterval(interval);
	});

	// Toast state
	let toasts: ToastItem[] = [];
	let toastId = 0;

	function addToast(type: 'info' | 'success' | 'warning' | 'error') {
		const messages = {
			info: 'Information received',
			success: 'Operation completed successfully',
			warning: 'Warning: Resource threshold exceeded',
			error: 'Connection lost to remote system'
		};
		toasts = [...toasts, { id: String(++toastId), message: messages[type], type }];
		setTimeout(() => {
			toasts = toasts.filter(t => t.id !== String(toastId));
		}, 3000);
	}

	// Table data
	const tableColumns = [
		{ key: 'callsign', label: 'Callsign' },
		{ key: 'type', label: 'Type' },
		{ key: 'status', label: 'Status', align: 'center' as const },
		{ key: 'fuel', label: 'Fuel %', align: 'right' as const }
	];
	const tableData = [
		{ callsign: 'VIPER-01', type: 'UAV', status: 'ACTIVE', fuel: 78 },
		{ callsign: 'HAWK-03', type: 'UGV', status: 'STANDBY', fuel: 92 },
		{ callsign: 'GHOST-12', type: 'UAV', status: 'RTB', fuel: 23 },
		{ callsign: 'WOLF-07', type: 'UGV', status: 'ACTIVE', fuel: 65 }
	];
</script>

<div class="demo-page font-{fontTheme}" class:no-mono={disableMono}>
	<header class="demo-header">
		<h1>ANVIL</h1>
		<p class="subtitle">Tactical HUD Component Library</p>
		<p class="tagline">Forged at Telchar Dynamics</p>

		<div class="theme-selector">
			<span class="theme-label">Font Theme:</span>
			<Select
				options={fontThemes}
				bind:value={fontTheme}
			/>
			<Toggle label="Disable Mono" bind:checked={disableMono} />
		</div>
	</header>

	<main class="demo-content">
		<!-- Tab Navigation -->
		<Tabs {tabs} bind:activeTab variant="pills" />

		{#if activeTab === 'overview'}
			<!-- Buttons Section -->
			<Card title="Buttons">
				<div class="component-grid">
					<Button variant="primary">Primary</Button>
					<Button variant="secondary">Secondary</Button>
					<Button variant="success">Success</Button>
					<Button variant="danger">Danger</Button>
					<Button variant="ghost">Ghost</Button>
					<Button variant="primary" disabled>Disabled</Button>
				</div>
				<Divider label="Sizes" />
				<div class="component-grid">
					<Button variant="primary" size="sm">Small</Button>
					<Button variant="primary" size="md">Medium</Button>
					<Button variant="primary" size="lg">Large</Button>
				</div>
			</Card>

			<!-- Badges & Indicators -->
			<Card title="Badges & Indicators">
				<div class="component-grid">
					<Badge>Default</Badge>
					<Badge variant="success">Success</Badge>
					<Badge variant="warning">Warning</Badge>
					<Badge variant="error">Error</Badge>
					<Badge variant="accent">Accent</Badge>
				</div>
				<Divider label="Pulsing Status" />
				<div class="component-grid">
					<Indicator status="success" pulse label="Connected" />
					<Indicator status="warning" pulse label="Standby" />
					<Indicator status="error" pulse label="Offline" />
					<Indicator status="accent" pulse label="Active" />
				</div>
			</Card>

			<!-- Data Display -->
			<Card title="Data Values">
				<div class="data-grid">
					<DataValue label="Altitude" value="1,250" unit="m" variant="accent" />
					<DataValue label="Speed" value="45.2" unit="m/s" />
					<DataValue label="Fuel" value="78" unit="%" variant="success" />
					<DataValue label="Temp" value="92" unit="°C" variant="warning" />
					<DataValue label="Error Rate" value="12.5" unit="%" variant="error" />
				</div>
			</Card>

			<!-- Table -->
			<Card title="Data Table">
				<Table columns={tableColumns} data={tableData} />
			</Card>

			<!-- Tooltips -->
			<Card title="Tooltips">
				<div class="component-grid">
					<Tooltip text="Tooltip on top" position="top">
						<Button variant="secondary">Top</Button>
					</Tooltip>
					<Tooltip text="Tooltip on right" position="right">
						<Button variant="secondary">Right</Button>
					</Tooltip>
					<Tooltip text="Tooltip on bottom" position="bottom">
						<Button variant="secondary">Bottom</Button>
					</Tooltip>
					<Tooltip text="Tooltip on left" position="left">
						<Button variant="secondary">Left</Button>
					</Tooltip>
				</div>
			</Card>
		{/if}

		{#if activeTab === 'controls'}
			<!-- Input Fields -->
			<Card title="Text Inputs">
				<div class="form-grid">
					<Input label="Callsign" placeholder="Enter callsign..." bind:value={inputValue} />
					<Input label="Frequency" type="number" placeholder="121.5" />
					<Input label="With Error" error="Invalid input" value="bad data" />
				</div>
			</Card>

			<!-- Select -->
			<Card title="Select Dropdown">
				<div class="form-grid">
					<Select
						label="Mission Type"
						options={[
							{ value: 'option1', label: 'Reconnaissance' },
							{ value: 'option2', label: 'Strike' },
							{ value: 'option3', label: 'Transport' }
						]}
						bind:value={selectValue}
					/>
					<Select
						label="Disabled Select"
						disabled
						options={[{ value: 'x', label: 'Locked' }]}
					/>
				</div>
			</Card>

			<!-- Toggles & Switches -->
			<Card title="Toggles & Switches">
				<div class="toggle-section">
					<h4 class="section-label">Toggles (Checkboxes)</h4>
					<div class="toggle-list">
						<Toggle label="Enable Tracking" bind:checked={toggleChecked} />
						<Toggle label="Night Mode" />
						<Toggle label="Disabled Option" disabled />
					</div>
				</div>
				<Divider />
				<div class="toggle-section">
					<h4 class="section-label">Switches</h4>
					<div class="switch-list">
						<Switch label="Auto-pilot" bind:checked={switchChecked} size="sm" />
						<Switch label="Weapons Safety" size="md" />
						<Switch label="Comms Relay" size="lg" checked />
					</div>
				</div>
			</Card>

			<!-- Slider -->
			<Card title="Sliders">
				<div class="slider-section">
					<Slider label="Throttle" bind:value={sliderValue} showValue />
					<Slider label="Heading" min={0} max={360} step={1} value={180} showValue />
					<Slider label="Disabled" disabled value={30} />
				</div>
			</Card>

			<!-- Modal -->
			<Card title="Modal Dialog">
				<Button variant="primary" on:click={() => showModal = true}>
					Open Modal
				</Button>
			</Card>
		{/if}

		{#if activeTab === 'feedback'}
			<!-- Progress Bars -->
			<Card title="Progress Bars">
				<div class="progress-section">
					<Progress value={progressValue} showValue variant="accent" />
					<Progress value={75} showValue variant="success" />
					<Progress value={45} showValue variant="warning" striped />
					<Progress value={90} showValue variant="error" striped animated />
				</div>
				<Divider label="Sizes" />
				<div class="progress-section">
					<Progress value={60} size="sm" />
					<Progress value={60} size="md" />
					<Progress value={60} size="lg" />
				</div>
			</Card>

			<!-- Spinners -->
			<Card title="Loading Spinners">
				<div class="component-grid">
					<Spinner size="sm" />
					<Spinner size="md" />
					<Spinner size="lg" />
					<Spinner size="xl" />
				</div>
				<Divider label="Variants" />
				<div class="component-grid">
					<Spinner variant="default" label="Loading" />
					<Spinner variant="accent" label="Processing" />
					<Spinner variant="light" label="Syncing" />
				</div>
			</Card>

			<!-- Toasts -->
			<Card title="Toast Notifications">
				<div class="component-grid">
					<Button variant="secondary" on:click={() => addToast('info')}>Info Toast</Button>
					<Button variant="success" on:click={() => addToast('success')}>Success Toast</Button>
					<Button variant="ghost" on:click={() => addToast('warning')}>Warning Toast</Button>
					<Button variant="danger" on:click={() => addToast('error')}>Error Toast</Button>
				</div>
			</Card>

			<!-- Panels -->
			<Card title="Overlay Panels" padding={false}>
				<div class="panel-demo">
					<Panel title="System Status" width="200px">
						<div class="panel-content-demo">
							<Indicator status="success" label="Comms" />
							<Indicator status="success" label="Nav" />
							<Indicator status="warning" label="Sensors" />
						</div>
					</Panel>
					<Panel title="Collapsible Panel" collapsible width="200px">
						<div class="panel-content-demo">
							<p>This panel can be collapsed by clicking the header.</p>
						</div>
					</Panel>
				</div>
			</Card>
		{/if}

		<!-- Card Variants (always visible) -->
		<Divider label="Card Variants" />

		<div class="card-grid">
			<Card title="Standard Card">
				<p>Default card styling with tactical HUD aesthetics.</p>
			</Card>

			<Card title="Card With Glow" glow>
				<p>Ambient glow effect for highlighted content.</p>
			</Card>

			<Card title="Card With Footer">
				<p>Cards can have footer sections for actions.</p>
				<svelte:fragment slot="footer">
					<div class="card-footer-actions">
						<Button variant="ghost" size="sm">Cancel</Button>
						<Button variant="primary" size="sm">Confirm</Button>
					</div>
				</svelte:fragment>
			</Card>
		</div>
	</main>

	<footer class="demo-footer">
		<Divider variant="accent" />
		<p>ANVIL v0.1.0 • MIT License • Telchar Dynamics</p>
	</footer>
</div>

<!-- Modal -->
<Modal title="System Configuration" open={showModal} on:close={() => showModal = false}>
	<div class="modal-content">
		<Input label="System Name" placeholder="Enter name..." />
		<Select
			label="Operating Mode"
			options={[
				{ value: 'auto', label: 'Autonomous' },
				{ value: 'manual', label: 'Manual Control' },
				{ value: 'hybrid', label: 'Hybrid' }
			]}
		/>
		<Switch label="Enable Logging" checked />
	</div>
	<svelte:fragment slot="footer">
		<Button variant="ghost" on:click={() => showModal = false}>Cancel</Button>
		<Button variant="primary" on:click={() => showModal = false}>Save Changes</Button>
	</svelte:fragment>
</Modal>

<!-- Toast Container -->
<Toast bind:toasts position="top-right" />

<style>
	.demo-page {
		min-height: 100vh;
		padding: var(--anvil-space-6);
		max-width: 1200px;
		margin: 0 auto;
	}

	.demo-header {
		text-align: center;
		margin-bottom: var(--anvil-space-8);
	}

	.demo-header h1 {
		font-family: var(--anvil-font-display);
		font-size: 3rem;
		font-weight: 700;
		letter-spacing: 0.3em;
		color: var(--anvil-accent);
		text-shadow: 0 0 30px var(--anvil-accent);
		margin-bottom: var(--anvil-space-2);
	}

	.subtitle {
		font-family: var(--anvil-font-mono);
		font-size: 14px;
		letter-spacing: 0.15em;
		text-transform: uppercase;
		color: var(--anvil-fg-1);
	}

	.tagline {
		font-family: var(--anvil-font-mono);
		font-size: 11px;
		letter-spacing: 0.1em;
		color: var(--anvil-fg-muted);
		margin-top: var(--anvil-space-1);
	}

	.theme-selector {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: var(--anvil-space-3);
		margin-top: var(--anvil-space-4);
	}

	.theme-label {
		font-family: var(--anvil-font-mono);
		font-size: 11px;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		color: var(--anvil-fg-muted);
	}

	.demo-content {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-4);
	}

	.component-grid {
		display: flex;
		flex-wrap: wrap;
		gap: var(--anvil-space-3);
		align-items: center;
	}

	.data-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
		gap: var(--anvil-space-4);
	}

	.form-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: var(--anvil-space-4);
	}

	.card-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: var(--anvil-space-4);
	}

	.toggle-section {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-3);
	}

	.section-label {
		font-family: var(--anvil-font-mono);
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		color: var(--anvil-fg-muted);
		margin: 0;
	}

	.toggle-list, .switch-list {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-2);
	}

	.slider-section {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-4);
		max-width: 400px;
	}

	.progress-section {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-3);
	}

	.panel-demo {
		display: flex;
		gap: var(--anvil-space-4);
		padding: var(--anvil-space-4);
		flex-wrap: wrap;
	}

	.panel-content-demo {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-2);
		padding: var(--anvil-space-2);
	}

	.panel-content-demo p {
		font-family: var(--anvil-font-mono);
		font-size: 11px;
		color: var(--anvil-fg-1);
		margin: 0;
	}

	.card-footer-actions {
		display: flex;
		justify-content: flex-end;
		gap: var(--anvil-space-2);
	}

	.modal-content {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-4);
	}

	.demo-footer {
		margin-top: var(--anvil-space-8);
		text-align: center;
	}

	.demo-footer p {
		font-family: var(--anvil-font-mono);
		font-size: 10px;
		letter-spacing: 0.1em;
		color: var(--anvil-fg-muted);
		margin-top: var(--anvil-space-3);
	}
</style>
