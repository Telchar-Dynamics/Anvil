# ⚒️ ANVIL

**Tactical HUD Component Library for Svelte**

*Forged at Telchar Dynamics*

---

## Overview

Anvil is a sleek, tactical-themed component library built for Svelte applications. Inspired by military HUD interfaces and C2 systems, it features:

- 🎯 **Tactical Aesthetic** - Dark theme with electric cyan accents and subtle glows
- 📐 **HUD Elements** - Corner brackets, scanlines, and status indicators
- ⚡ **Svelte-Native** - Built specifically for Svelte 4/5
- 🎨 **CSS Variables** - Fully customizable design tokens
- 📦 **Zero Dependencies** - Lightweight and standalone

## Installation

```bash
npm install @telchar/anvil
```

## Usage

```svelte
<script>
  import { Button, Card, Badge, Indicator } from '@telchar/anvil';
  import '@telchar/anvil/styles';
</script>

<div class="anvil">
  <Card title="System Status">
    <Indicator status="success" label="Online" pulse />
    <Badge variant="accent">ACTIVE</Badge>
    <Button variant="primary">Engage</Button>
  </Card>
</div>
```

## Components

| Component | Description |
|-----------|-------------|
| `Button` | Tactical buttons with glow effects |
| `Card` | Panels with HUD corner brackets |
| `Badge` | Status badges with dot indicators |
| `Panel` | Collapsible overlay panels |
| `Input` | Text inputs with tactical styling |
| `Toggle` | Checkbox toggles |
| `Divider` | Section dividers with optional labels |
| `DataValue` | Labeled data display |
| `Indicator` | Status dot indicators |

## Design Tokens

Anvil uses CSS custom properties for theming:

```css
:root {
  --anvil-accent: #00f0ff;      /* Primary accent */
  --anvil-bg-0: #050608;        /* Background */
  --anvil-success: #00ff88;     /* Success state */
  --anvil-warning: #ffaa00;     /* Warning state */
  --anvil-error: #ff3366;       /* Error state */
}
```

## Development

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build library
npm run package

# Type check
npm run check
```

## License

MIT © Telchar Dynamics
