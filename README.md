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

There is no build step and no package installation. Open [`index.html`](./index.html) directly in a browser:

```bash
open index.html
```

For an HTTP origin:

```bash
uv run python -m http.server 8000
open http://localhost:8000
```

The only runtime network dependency is Google Fonts. The page remains functional with its local fallback fonts if that request is unavailable.

## Repository structure

```text
.
├── index.html      # Complete application, styles, content model, and interactions
├── README.md       # Project overview and local workflow
├── AGENTS.md       # Instructions and invariants for coding agents
└── CHANGELOG.md    # Revision history
```

`index.html` is intentionally self-contained. The element definitions, references, functional groups, compounds, and complexes live in JavaScript data structures near the bottom of the file.

## Editing and validation

When changing the ontology, keep every dependent representation synchronized:

1. Element and family counts in the metadata, hero, filters, and section labels
2. The `atoms`, `references`, and orthogonality-question maps
3. Functional-group, molecule, and complex formulas
4. Appendix explanations and the visible revision number

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

## License

Licensed under the [Apache License 2.0](./LICENSE).
