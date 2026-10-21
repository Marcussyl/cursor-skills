# HTML shell template (extract for new guides)

Replace `{{TITLE}}`, `{{SUBTITLE}}`, section bodies, and TOC links. Keep class names so styling stays consistent.

## Minimal head + layout skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>{{TITLE}}</title>
  <style>
    :root {
      --bg: #0f1419;
      --panel: #1a2332;
      --border: #2d3a4f;
      --text: #e7ecf3;
      --muted: #9aa8bc;
      --accent: #5eb3ff;
      --warn: #f0b429;
      --danger: #f87171;
      --ok: #4ade80;
      --mono: ui-monospace, 'SF Mono', Menlo, Consolas, monospace;
      --sans: system-ui, -apple-system, 'Segoe UI', sans-serif;
    }
    * { box-sizing: border-box; }
    body { margin: 0; font-family: var(--sans); background: var(--bg); color: var(--text); line-height: 1.55; font-size: 15px; }
    header { padding: 2rem 1.5rem 1rem; border-bottom: 1px solid var(--border); background: linear-gradient(180deg, #152033 0%, var(--bg) 100%); }
    header h1 { margin: 0 0 0.35rem; font-size: 1.65rem; }
    header p { margin: 0; color: var(--muted); max-width: 72ch; }
    .meta { margin-top: 0.75rem; font-size: 0.85rem; color: var(--muted); }
    nav.toc { position: sticky; top: 0; z-index: 10; background: rgba(15, 20, 25, 0.92); backdrop-filter: blur(8px); border-bottom: 1px solid var(--border); padding: 0.6rem 1.5rem; display: flex; flex-wrap: wrap; gap: 0.5rem 1rem; font-size: 0.88rem; }
    nav.toc a { color: var(--accent); text-decoration: none; }
    main { max-width: 1100px; margin: 0 auto; padding: 1.5rem; }
    section { margin-bottom: 2.5rem; padding: 1.25rem 1.35rem; background: var(--panel); border: 1px solid var(--border); border-radius: 10px; }
    h2 { margin-top: 0; font-size: 1.25rem; color: var(--accent); }
    p.zh { color: #c5d0e0; font-size: 0.92rem; border-left: 3px solid var(--border); padding-left: 0.75rem; }
    code { font-family: var(--mono); font-size: 0.86em; background: #0d1117; padding: 0.12em 0.35em; border-radius: 4px; border: 1px solid #30363d; }
    pre { font-family: var(--mono); font-size: 0.8rem; background: #0d1117; border: 1px solid var(--border); border-radius: 8px; padding: 1rem; overflow-x: auto; }
    table { width: 100%; border-collapse: collapse; font-size: 0.88rem; margin: 1rem 0; }
    th, td { border: 1px solid var(--border); padding: 0.5rem 0.65rem; text-align: left; vertical-align: top; }
    th { background: #121a26; color: var(--accent); }
    .tag { display: inline-block; padding: 0.15em 0.5em; border-radius: 4px; font-size: 0.75rem; font-weight: 600; text-transform: uppercase; }
    .tag-critical { background: #7f1d1d; color: #fecaca; }
    .tag-high { background: #78350f; color: #fde68a; }
    .tag-medium { background: #1e3a5f; color: #bfdbfe; }
    ul.checklist { list-style: none; padding-left: 0; }
    ul.checklist li { position: relative; padding-left: 1.75rem; margin-bottom: 0.45rem; }
    ul.checklist li::before { content: '☐'; position: absolute; left: 0; color: var(--muted); }
    .finding { border-left: 4px solid var(--warn); padding: 0.75rem 1rem; margin: 0.75rem 0; background: #1c1917; border-radius: 0 8px 8px 0; }
    .finding.ok { border-left-color: var(--ok); }
    .finding.danger { border-left-color: var(--danger); }
    details.test-case { margin: 0.75rem 0; border: 1px solid var(--border); border-radius: 8px; background: #121a26; }
    details.test-case summary { cursor: pointer; padding: 0.65rem 1rem; font-weight: 600; }
    details.test-case .body { padding: 0 1rem 1rem; font-size: 0.9rem; }
    @media print {
      body { background: #fff; color: #111; }
      section { break-inside: avoid; border-color: #ccc; background: #f9fafb; }
      nav.toc { display: none; }
    }
  </style>
</head>
<body>
  <header>
    <h1>{{TITLE}}</h1>
    <p>{{SUBTITLE}}</p>
    <div class="meta">Scope: … · Repos: …</div>
  </header>
  <nav class="toc" aria-label="Table of contents">
    <a href="#architecture">Architecture</a>
    <a href="#critical-paths">Critical paths</a>
    <a href="#function-map">Function map</a>
    <a href="#review">Code review</a>
    <a href="#apis">APIs</a>
    <a href="#testing">Test guide</a>
    <a href="#matrix">Matrix</a>
  </nav>
  <main>
    <section id="architecture"><h2>1. Architecture</h2><!-- diagram + prose --></section>
    <section id="critical-paths"><h2>2. Critical paths</h2><!-- P1 tables --></section>
    <section id="function-map"><h2>3. Function map</h2></section>
    <section id="review"><h2>4. Code review</h2></section>
    <section id="apis"><h2>5. APIs</h2></section>
    <section id="testing"><h2>6. Test guide</h2></section>
    <section id="matrix"><h2>7. Matrix</h2></section>
  </main>
  <footer><!-- optional --></footer>
</body>
</html>
```

## Critical path table row pattern

```html
<h3><span class="tag tag-critical">P1</span> Short path title</h3>
<table>
  <thead><tr><th>Step</th><th>Repo</th><th>Critical function(s)</th><th>Notes</th></tr></thead>
  <tbody>
    <tr><td>…</td><td>…</td><td><code>exactSymbol</code></td><td>…</td></tr>
  </tbody>
</table>
```

## Test case pattern

```html
<details class="test-case">
  <summary>T1 — Scenario title</summary>
  <div class="body">
    <p><strong>Path:</strong> P1 · <code>fnA</code> → <code>fnB</code></p>
    <p><strong>Pre:</strong> …</p>
    <ul class="checklist">
      <li>Step one</li>
    </ul>
    <p><strong>Expected:</strong> …</p>
  </div>
</details>
```
