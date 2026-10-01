# Anvil

Anvil is a tactical HUD component library for Svelte, published as `@telchar/anvil` under the MIT licence. Components live in `src/lib/components/`, themed through `--anvil-*` CSS custom properties and font-theme classes.

## Company standards (Norma)

This repo follows the Telchar Dynamics standards in **Telchar-Dynamics/Norma** (https://github.com/Telchar-Dynamics/Norma). Locally, Norma is cloned next to this repo at `../Norma`. If `../Norma` does not exist (for example in a cloud or CI session), clone it there first: `git clone https://github.com/Telchar-Dynamics/Norma ../Norma`. If you can't clone it, read the files from GitHub. Read before working:

- [`../Norma/AGENTS.md`](../Norma/AGENTS.md): company standards (always);
- [`../Norma/SOFTWARE.md`](../Norma/SOFTWARE.md): software standards;
- the `telchar-design` skill ([`../Norma/.agents/skills/telchar-design/SKILL.md`](../Norma/.agents/skills/telchar-design/SKILL.md)): for component and UI work. Anvil's own design tokens and tactical aesthetic take precedence inside this repo.

Where this file and Norma disagree, this file wins for this repo.

Norma is a private repository. Contributors without access can follow this file and `README.md` alone.

## Repo rules

- This repository is public. Keep internal standards, private repo content and internal links out of commits, issues and published package files.
- Keep the library free of runtime dependencies and Svelte-native (Svelte 4/5 peer).
- Before handing off, run `npm run check`, `npm run lint` and `npm run package` (`svelte-package` + `publint`).

## Where to find current state

- `README.md`: components, font themes, design tokens and development commands.
- `package.json`: the published version and exports.
