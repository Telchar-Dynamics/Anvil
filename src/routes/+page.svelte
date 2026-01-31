<script lang="ts">
	import '$lib/styles/anvil.css';
	import {
		Button,
		Card,
		Badge,
		Panel,
		Input,
		Toggle,
		Divider,
		DataValue,
		Indicator
	} from '$lib';

	let inputValue = '';
	let toggleChecked = true;
</script>

<div class="demo-page">
	<header class="demo-header">
		<h1>ANVIL</h1>
		<p class="subtitle">Tactical HUD Component Library</p>
		<p class="tagline">Forged at Telchar Dynamics</p>
	</header>

	<main class="demo-content">
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

		<!-- Badges Section -->
		<Card title="Badges">
			<div class="component-grid">
				<Badge>Default</Badge>
				<Badge variant="success">Success</Badge>
				<Badge variant="warning">Warning</Badge>
				<Badge variant="error">Error</Badge>
				<Badge variant="accent">Accent</Badge>
			</div>
			<Divider label="With Pulse" />
			<div class="component-grid">
				<Badge variant="success" pulse>Online</Badge>
				<Badge variant="warning" pulse>Standby</Badge>
				<Badge variant="error" pulse>Alert</Badge>
			</div>
		</Card>

		<!-- Indicators Section -->
		<Card title="Indicators">
			<div class="component-grid">
				<Indicator status="success" label="Connected" />
				<Indicator status="warning" label="Standby" />
				<Indicator status="error" label="Offline" />
				<Indicator status="accent" label="Active" />
				<Indicator status="muted" label="Inactive" />
			</div>
			<Divider label="Pulsing" />
			<div class="component-grid">
				<Indicator status="success" pulse label="Live" />
				<Indicator status="error" pulse label="Critical" />
			</div>
		</Card>

		<!-- Data Values Section -->
		<Card title="Data Values">
			<div class="component-grid">
				<DataValue label="Altitude" value="1,250" unit="m" variant="accent" />
				<DataValue label="Speed" value="45.2" unit="m/s" />
				<DataValue label="Fuel" value="78" unit="%" variant="success" />
				<DataValue label="Temp" value="92" unit="°C" variant="warning" />
				<DataValue label="Error Rate" value="12.5" unit="%" variant="error" />
			</div>
		</Card>

		<!-- Inputs Section -->
		<Card title="Form Controls">
			<div class="form-grid">
				<Input label="Callsign" placeholder="Enter callsign..." bind:value={inputValue} />
				<Input label="Frequency" type="number" placeholder="121.5" />
				<Input label="With Error" error="Invalid input" value="bad data" />
			</div>
			<Divider label="Toggles" />
			<div class="toggle-list">
				<Toggle label="Enable Tracking" bind:checked={toggleChecked} />
				<Toggle label="Night Mode" />
				<Toggle label="Disabled Option" disabled />
			</div>
		</Card>

		<!-- Panel Section -->
		<Card title="Panels" padding={false}>
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

		<!-- Card Variants -->
		<Card title="Card With Glow" glow>
			<p>This card has the glow effect enabled, creating a subtle cyan ambient light.</p>
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
	</main>

	<footer class="demo-footer">
		<Divider variant="accent" />
		<p>ANVIL v0.1.0 • MIT License • Telchar Dynamics</p>
	</footer>
</div>

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

	.form-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: var(--anvil-space-4);
	}

	.toggle-list {
		display: flex;
		flex-direction: column;
		gap: var(--anvil-space-2);
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
	}

	.card-footer-actions {
		display: flex;
		justify-content: flex-end;
		gap: var(--anvil-space-2);
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
