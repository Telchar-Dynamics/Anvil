# ANVIL

**Tactical HUD Component Library for Svelte**

*Forged at Telchar Dynamics*

---

## Overview

Anvil is a sleek, tactical-themed component library built for Svelte applications. Inspired by military HUD interfaces and C2 systems, it features:

- **Tactical Aesthetic** - Dark theme with electric cyan accents and subtle glows
- **HUD Elements** - Corner brackets, scanlines, and status indicators
- **Svelte-Native** - Built specifically for Svelte 4/5
- **CSS Variables** - Fully customizable design tokens
- **Font Themes** - Multiple font presets including Geist, JetBrains Mono, and more
- **Zero Dependencies** - Lightweight and standalone

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

<div class="anvil font-geist">
  <Card title="System Status">
    <Indicator status="success" label="Online" pulse />
    <Badge variant="accent">ACTIVE</Badge>
    <Button variant="primary">Engage</Button>
  </Card>
</div>
```

## Components

### Form Controls
| Component | Description |
|-----------|-------------|
| `Button` | Tactical buttons with glow effects |
| `Input` | Text inputs with tactical styling |
| `Select` | Dropdown select menus |
| `Toggle` | Checkbox toggles |
| `Switch` | On/off toggle switches |
| `Slider` | Range slider inputs |

### Layout
| Component | Description |
|-----------|-------------|
| `Card` | Panels with HUD corner brackets |
| `Panel` | Collapsible overlay panels |
| `Divider` | Section dividers with optional labels |
| `Modal` | Dialog modals with backdrop |
| `Tabs` | Tabbed content panels |
| `Table` | Data tables with tactical styling |
| `Accordion` | Collapsible content sections |

### Feedback
| Component | Description |
|-----------|-------------|
| `Badge` | Status badges with dot indicators |
| `Indicator` | Status dot indicators with pulse |
| `Progress` | Progress bars |
| `Spinner` | Loading spinners |
| `Toast` | Toast notifications |
| `Tooltip` | Hover tooltips |
| `Alert` | Alert banners with dismiss |
| `Skeleton` | Loading placeholder with shimmer |
| `Empty` | Empty state placeholders |

### Data Display
| Component | Description |
|-----------|-------------|
| `DataValue` | Labeled data display |
| `Stat` | Statistics with change indicators |
| `Code` | Inline and block code display |
| `Kbd` | Keyboard key display |
| `Tag` | Removable label tags |

### Navigation
| Component | Description |
|-----------|-------------|
| `Breadcrumb` | Navigation breadcrumbs |

### Media
| Component | Description |
|-----------|-------------|
| `Avatar` | User avatars with status indicators |

## Font Themes

Anvil includes several font theme presets. Apply them by adding a class to your container:

```html
<div class="anvil font-geist">...</div>
```

| Class | Fonts |
|-------|-------|
| `font-geist` | Geist / Geist Mono (default) |
| `font-jetbrains` | JetBrains Mono |
| `font-fira` | Fira Code |
| `font-ibm` | IBM Plex Mono |
| `font-source` | Source Code Pro |
| `font-inter` | Inter / JetBrains Mono |
| `font-space` | Space Grotesk / Space Mono |

### Disable Monospace

To use the body font instead of monospace for component text:

```html
<div class="anvil font-geist no-mono">...</div>
```

## Design Tokens

Anvil uses CSS custom properties for theming:

```css
:root {
  /* Colors */
  --anvil-accent: #00f0ff;
  --anvil-bg-0: #050608;
  --anvil-bg-1: #0a0d12;
  --anvil-bg-2: #0e1319;
  --anvil-fg-0: #e8eef5;
  --anvil-fg-1: #a8b5c4;
  --anvil-fg-muted: #5a6a7a;
  --anvil-border: #1a242e;
  --anvil-success: #00ff88;
  --anvil-warning: #ffaa00;
  --anvil-error: #ff3366;

  /* Typography */
  --anvil-font-display: 'Geist', system-ui, sans-serif;
  --anvil-font-body: 'Geist', system-ui, sans-serif;
  --anvil-font-mono: 'Geist Mono', monospace;

  /* Spacing */
  --anvil-space-1: 0.25rem;
  --anvil-space-2: 0.5rem;
  --anvil-space-4: 1rem;
  --anvil-space-8: 2rem;

  /* Radii */
  --anvil-radius-sm: 2px;
  --anvil-radius-md: 4px;
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

MIT
