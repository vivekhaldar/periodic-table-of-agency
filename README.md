# The Periodic Table of Agency

An interactive field guide to the atomic operators behind agentic systems—and the bonds, functional groups, compounds, and complexes they form.

Live site: [agentatoms.dev](https://agentatoms.dev)

The project uses the periodic table as a compositional metaphor. It is not claiming a physical periodic law for agent engineering.

## Current field chart

Revision 0.6 contains:

- 29 atomic operators in seven behavioral families
- eight bond types and three bond strengths
- 11 reusable functional groups
- 10 agent molecules and compounds
- four multi-agent complexes and assemblies
- direct links from each element to the relevant [Harness Course](https://harnesscourse.com/) section and a canonical reading

The ontology deliberately distinguishes:

- **Atoms** — irreducible engineering operators such as Retrieve, Loop, Verify, Ask, Merge, and Wait
- **Modalities** — specializations written in brackets, such as `Tl[browse]`, `Vf[test]`, and `Wt[schedule]`
- **Bonds** — sequence `→`, feedback `↺`, gate `⊣`, evidence `⊨`, state `—`, parallel `⇉`, together `+`, and containment `[ ]`
- **Strengths** — advisory `~`, coded (unmarked), and enforced `!`
- **Functional groups** — recurring subassemblies such as durable memory, an evaluation rig, or an input quarantine
- **Molecules and complexes** — complete agent patterns and coordinated multi-agent systems

## Run locally

The authored field chart has no build step or package installation. The playground uses JavaScript modules, so serve the repository over HTTP to exercise both pages:

```bash
uv run python -m http.server 8000
open http://localhost:8000
open http://localhost:8000/play/
```

Both pages request Google Fonts and remain usable with their local fallback stacks when the font request is unavailable. The field chart otherwise runs locally. Playground analysis is also local and offline; choosing **Run** makes direct requests from the browser to either Anthropic or the OpenAI-compatible base URL the user supplied.

The public site is deployed from `main` through GitHub Pages at [agentatoms.dev](https://agentatoms.dev). The repository is public and licensed under Apache-2.0.

## Repository structure

```text
.
├── index.html                         # Canonical authored field chart and ontology
├── play/
│   ├── index.html                    # Authored playground UI and preset gallery
│   └── agent-algebra-playground.js   # Generated browser runtime; do not edit
├── README.md                          # Project overview and local workflow
├── AGENTS.md                          # Instructions and ontology invariants
└── CHANGELOG.md                       # Field-chart revision history
```

`index.html` remains the canonical ontology and the self-contained field-chart artifact. The element definitions, references, functional groups, compounds, and complexes live in JavaScript data structures near the bottom of that file. `play/index.html` owns the playground presentation and presets. `play/agent-algebra-playground.js` is generated from the separate [agent-algebra](https://github.com/vivekhaldar/agent-algebra) repository; changes to parser, compiler, analyzer, or runtime behavior belong there.

## Refresh the generated playground runtime

The checked-in bundle was generated from agent-algebra commit [`f3f646bf82634c2bdfe1f7f978d4a277755150da`](https://github.com/vivekhaldar/agent-algebra/commit/f3f646bf82634c2bdfe1f7f978d4a277755150da) (`agent-algebra` package version `0.2.0`) and has SHA-256 `abc8cb33a7888c690a749ddd27fd788fc1d594e64a2a159980b26f46af2c28e4`. To rebuild it from an agent-algebra checkout, first use that repository's supported Node version and dependencies, then run:

```bash
cd ../agent-algebra
npm ci
npm run build
node playground/build.mjs \
  --out ../periodic-table-of-agency/play/agent-algebra-playground.js
```

Do not edit the generated bundle directly. Review its diff together with the source commit, run the agent-algebra checks, and then validate both pages here before releasing it. Cross-repository version automation is intentionally not defined in this repository yet; [issue #4](https://github.com/vivekhaldar/periodic-table-of-agency/issues/4) tracks that larger contract.

## Editing and validation

When changing the ontology, keep every dependent representation synchronized:

1. Element and family counts in the metadata, hero, filters, and section labels
2. The `atoms`, `references`, and orthogonality-question maps
3. Functional-group, molecule, and complex formulas
4. Appendix explanations and the visible revision number
5. Positional copy: placements are editorial and may suggest approximate reach or horizon, but must not be described as an enforced semantic axis without an explicit scoring rule

Minimum validation:

```bash
node - <<'NODE'
const fs = require('fs');
const html = fs.readFileSync('index.html', 'utf8');
const scripts = [...html.matchAll(/<script>([\s\S]*?)<\/script>/g)];
if (scripts.length !== 1) throw new Error(`Expected one inline script, found ${scripts.length}`);
new Function(scripts[0][1]);
console.log('Inline JavaScript parses');
NODE
```

Then verify the page at mobile and desktop widths, exercise every family filter, open several element details, and check the browser console for errors.

For playground changes, also verify:

1. Every preset displays its execution level before Analyze or Run.
2. Analysis-only presets explain why Run is unavailable.
3. Analyze works without a key or network access.
4. Provider configuration names the exact destination: Anthropic's API origin or the entered OpenAI-compatible base URL.
5. A scoped test key can run one conventional preset and can be cleared from the tab afterward.
6. No authored change was made directly inside `play/agent-algebra-playground.js`.

## License

Licensed under the [Apache License 2.0](./LICENSE).
