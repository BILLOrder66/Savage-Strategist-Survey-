[diagnostic.html](https://github.com/user-attachments/files/29069800/diagnostic.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Savage Strategist Diagnostic</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600&family=IBM+Plex+Serif:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #FAFAF7;
    --surface: #FFFFFF;
    --border: #E5E2DA;
    --border-strong: #C8C5BC;
    --text: #1A1A1A;
    --text-muted: #5A5A55;
    --algo: #B8741C;
    --bric: #1E7F5C;
    --prin: #5D55B8;
    --vel: #C44A2C;
    --info: #2A4D8F;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'IBM Plex Sans', system-ui, sans-serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.55;
    padding: 40px 24px;
    min-height: 100vh;
  }

  .container {
    max-width: 720px;
    margin: 0 auto;
  }

  header {
    margin-bottom: 32px;
    padding-bottom: 20px;
    border-bottom: 1px solid var(--border);
  }

  .eyebrow {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 8px;
  }

  h1 {
    font-family: 'IBM Plex Serif', serif;
    font-size: 28px;
    font-weight: 500;
    line-height: 1.2;
    margin-bottom: 8px;
  }

  .lede {
    font-size: 15px;
    color: var(--text-muted);
    max-width: 580px;
  }

  .stage {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px;
    margin-bottom: 16px;
  }

  .meta {
    display: flex;
    gap: 8px;
    margin-bottom: 16px;
  }

  .meta span {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.05em;
    padding: 3px 9px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 3px;
    color: var(--text-muted);
  }

  .trace {
    display: flex;
    gap: 8px;
    margin-bottom: 20px;
  }

  .dot {
    width: 26px;
    height: 26px;
    border-radius: 50%;
    border: 1px solid var(--border-strong);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    color: var(--text-muted);
  }

  .dot.done {
    background: var(--info);
    color: white;
    border-color: var(--info);
  }

  .dot.current {
    border: 2px solid var(--info);
    color: var(--info);
    font-weight: 500;
  }

  .prompt {
    font-size: 16px;
    line-height: 1.6;
    margin-bottom: 20px;
    color: var(--text);
  }

  .choices {
    display: grid;
    gap: 10px;
  }

  .choice {
    text-align: left;
    padding: 14px 16px;
    font-family: inherit;
    font-size: 14px;
    line-height: 1.55;
    color: var(--text);
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 3px;
    cursor: pointer;
    transition: border-color 0.15s, background 0.15s;
  }

  .choice:hover {
    border-color: var(--border-strong);
    background: var(--surface);
  }

  .choice.picked {
    border: 2px solid var(--info);
    background: #F0F4FB;
    padding: 13px 15px;
  }

  .choice:disabled { cursor: default; }

  .result { display: none; }
  .result.shown { display: block; }

  .signature-grid {
    display: grid;
    gap: 14px;
    margin: 20px 0 24px;
  }

  .bar-row { font-size: 13px; }

  .bar-label {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 5px;
  }

  .bar-label .name { font-weight: 500; }
  .bar-label .pct {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--text-muted);
  }

  .bar-track {
    height: 8px;
    background: var(--bg);
    border-radius: 4px;
    overflow: hidden;
    border: 1px solid var(--border);
  }

  .bar-fill {
    height: 100%;
    transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .verdict {
    padding: 18px 20px;
    background: var(--bg);
    border-left: 3px solid var(--info);
    font-size: 14px;
    line-height: 1.6;
    margin-bottom: 16px;
  }

  .verdict strong {
    font-family: 'IBM Plex Serif', serif;
    font-weight: 500;
    font-size: 15px;
  }

  .actions {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin-top: 16px;
  }

  .btn {
    font-family: inherit;
    font-size: 13px;
    padding: 8px 14px;
    background: var(--surface);
    color: var(--text);
    border: 1px solid var(--border-strong);
    border-radius: 3px;
    cursor: pointer;
    transition: background 0.15s;
  }

  .btn:hover { background: var(--bg); }

  .btn-primary {
    background: var(--text);
    color: var(--surface);
    border-color: var(--text);
  }
  .btn-primary:hover { background: #000; }

  footer {
    margin-top: 32px;
    padding-top: 16px;
    border-top: 1px solid var(--border);
    font-size: 12px;
    color: var(--text-muted);
    line-height: 1.6;
  }

  @media print {
    body { background: white; padding: 20px; }
    .actions, .stage:not(.result .stage) { display: none; }
    .result .stage { border: 1px solid #000; }
  }

  @media (max-width: 600px) {
    body { padding: 24px 16px; }
    h1 { font-size: 22px; }
    .stage { padding: 20px; }
  }
</style>
</head>
<body>
<div class="container">

<header>
  <div class="eyebrow">Alpha Blue · Cognitive Diagnostic</div>
  <h1>The Savage Strategist Diagnostic</h1>
  <p class="lede">A scenario walkthrough that surfaces your cognitive signature across algorithmic, bricoleur, and principled-action modes — with velocity as a separate axis. Four decisions, no doctrinally correct answers. The instrument is a teaching mirror, not a measurement.</p>
</header>

<div class="stage" id="stage">
  <div class="meta">
    <span id="stage-label">Decision 1 of 4</span>
    <span id="phase-label">Phase II — Shaping</span>
  </div>
  <div class="trace" id="trace"></div>
  <div class="prompt" id="prompt"></div>
  <div class="choices" id="choices"></div>
</div>

<div class="result" id="result">
  <div class="stage">
    <div class="eyebrow" style="margin-bottom: 6px;">Result</div>
    <h2 style="font-family: 'IBM Plex Serif', serif; font-size: 22px; font-weight: 500; margin-bottom: 4px;">Your cognitive signature</h2>
    <p style="font-size: 13px; color: var(--text-muted); margin-bottom: 8px;">Pattern across four decisions</p>

    <div class="signature-grid">
      <div class="bar-row">
        <div class="bar-label"><span class="name">Algorithmic</span><span class="pct" id="algo-pct">0%</span></div>
        <div class="bar-track"><div class="bar-fill" id="algo-bar" style="width: 0%; background: var(--algo);"></div></div>
      </div>
      <div class="bar-row">
        <div class="bar-label"><span class="name">Bricoleur</span><span class="pct" id="bric-pct">0%</span></div>
        <div class="bar-track"><div class="bar-fill" id="bric-bar" style="width: 0%; background: var(--bric);"></div></div>
      </div>
      <div class="bar-row">
        <div class="bar-label"><span class="name">Principled action</span><span class="pct" id="prin-pct">0%</span></div>
        <div class="bar-track"><div class="bar-fill" id="prin-bar" style="width: 0%; background: var(--prin);"></div></div>
      </div>
      <div class="bar-row">
        <div class="bar-label"><span class="name">Velocity bias</span><span class="pct" id="vel-pct">0%</span></div>
        <div class="bar-track"><div class="bar-fill" id="vel-bar" style="width: 0%; background: var(--vel);"></div></div>
      </div>
    </div>

    <div class="verdict" id="verdict"></div>

    <div class="actions">
      <button class="btn btn-primary" onclick="reset()">Run again</button>
      <button class="btn" onclick="window.print()">Print result</button>
      <button class="btn" onclick="copyResult()" id="copy-btn">Copy result text</button>
    </div>
  </div>
</div>

<footer>
  This diagnostic is a teaching provocation, not an assessment instrument. It surfaces a cognitive disposition under low-stakes conditions and cannot predict performance under sustained pressure. The instrument's purpose is to generate a seminar conversation in which you defend or revise the pattern it identifies.
</footer>

</div>

<script>
// =============================================================
// SCENARIOS — edit these to refit for different phases or cases.
// Each scoring object weights the four dimensions:
//   algo = algorithmic / doctrinal pattern-matching
//   bric = bricoleur / improvise from tools at hand
//   prin = principled action / hold the durability line
//   vel  = velocity bias (positive = pro-tempo, negative = anti-tempo)
// =============================================================
const decisions = [
  {
    phase: "Phase II — Shaping",
    prompt: "Your intelligence brief reports an adversary force concentration that closely matches a doctrinal template from a previous campaign. Your J2 is confident in the read. Time to commitment of shaping fires: 90 minutes. You:",
    choices: [
      { text: "Execute the doctrinal counter-template. The match is high-confidence and time is short.", scores: { algo: 3, bric: 0, prin: 0, vel: 2 } },
      { text: "Run a quick red-team challenge on the template match before committing fires.", scores: { algo: 0, bric: 2, prin: 2, vel: -1 } },
      { text: "Hold fires, request additional collection, accept the timeline slip.", scores: { algo: 0, bric: 1, prin: 3, vel: -2 } },
      { text: "Commit partial fires against the highest-confidence nodes, hold the rest pending confirmation.", scores: { algo: 1, bric: 3, prin: 1, vel: 1 } }
    ]
  },
  {
    phase: "Phase II — Shaping",
    prompt: "A subordinate commander proposes an unconventional sequencing that violates a standard phasing assumption but exploits an adversary cognitive vulnerability your staff identified yesterday. Doctrine doesn't address it. You:",
    choices: [
      { text: "Approve and resource it. The vulnerability window is real and doctrine is a guide, not a constraint.", scores: { algo: 0, bric: 2, prin: 2, vel: 1 } },
      { text: "Decline. Untested sequencing introduces risk you can't bound under current ROE.", scores: { algo: 3, bric: 0, prin: 1, vel: 0 } },
      { text: "Approve a scaled-down version that tests the concept without betting the campaign on it.", scores: { algo: 1, bric: 3, prin: 2, vel: 0 } },
      { text: "Send it back for a written branch plan with explicit risk-to-force and risk-to-mission framing.", scores: { algo: 1, bric: 1, prin: 3, vel: -1 } }
    ]
  },
  {
    phase: "Phase III — Decisive ops",
    prompt: "Mid-campaign, a strike opportunity opens against a high-value target. The legal review is incomplete but the window closes in 40 minutes. Collateral estimate is at the upper edge of policy. Your political advisor flags potential strategic blowback. You:",
    choices: [
      { text: "Strike. The target is doctrinally decisive and the window is the constraint.", scores: { algo: 2, bric: 0, prin: 0, vel: 3 } },
      { text: "Pass. No strike without completed legal review, regardless of window.", scores: { algo: 1, bric: 0, prin: 3, vel: -2 } },
      { text: "Push for an expedited legal review by phone with the COL JAG; accept the window may close.", scores: { algo: 0, bric: 2, prin: 3, vel: 0 } },
      { text: "Strike with reduced munitions to drop collateral inside policy, accepting lower target effects.", scores: { algo: 0, bric: 3, prin: 1, vel: 2 } }
    ]
  },
  {
    phase: "Phase IV — Stabilization",
    prompt: "The campaign has succeeded militarily but the cognitive web shows the adversary regime narrative consolidating rather than collapsing. Your staff offers three reads: doctrine says press the advantage, history suggests the regime is brittle and one push will break it, your own gut says something has shifted that nobody's frameworks are catching. You:",
    choices: [
      { text: "Press. Doctrine and historical analogy converge.", scores: { algo: 3, bric: 0, prin: 0, vel: 2 } },
      { text: "Pause operations and commission a fresh assessment that takes the gut signal seriously.", scores: { algo: 0, bric: 2, prin: 3, vel: -2 } },
      { text: "Shift effort toward cognitive web operations while maintaining current military tempo.", scores: { algo: 0, bric: 3, prin: 2, vel: 1 } },
      { text: "Request strategic guidance from above before adjusting; this is above your level.", scores: { algo: 2, bric: 0, prin: 2, vel: -1 } }
    ]
  }
];

let idx = 0;
let totals = { algo: 0, bric: 0, prin: 0, vel: 0 };

function renderTrace() {
  const el = document.getElementById('trace');
  el.innerHTML = '';
  for (let i = 0; i < decisions.length; i++) {
    const dot = document.createElement('div');
    dot.className = 'dot' + (i < idx ? ' done' : i === idx ? ' current' : '');
    dot.textContent = i + 1;
    el.appendChild(dot);
  }
}

function renderDecision() {
  if (idx >= decisions.length) { showResult(); return; }
  const d = decisions[idx];
  document.getElementById('stage-label').textContent = 'Decision ' + (idx + 1) + ' of ' + decisions.length;
  document.getElementById('phase-label').textContent = d.phase;
  document.getElementById('prompt').textContent = d.prompt;
  const cEl = document.getElementById('choices');
  cEl.innerHTML = '';
  d.choices.forEach((c, i) => {
    const btn = document.createElement('button');
    btn.className = 'choice';
    btn.textContent = c.text;
    btn.onclick = () => pick(i, btn);
    cEl.appendChild(btn);
  });
  renderTrace();
}

function pick(i, btn) {
  document.querySelectorAll('.choice').forEach(b => b.disabled = true);
  btn.classList.add('picked');
  const s = decisions[idx].choices[i].scores;
  totals.algo += s.algo;
  totals.bric += s.bric;
  totals.prin += s.prin;
  totals.vel += s.vel;
  setTimeout(() => { idx++; renderDecision(); }, 500);
}

function getVerdict(totals, pcts) {
  const dominant = ['algo', 'bric', 'prin'].reduce((a, b) => totals[a] > totals[b] ? a : b);
  if (dominant === 'algo' && pcts.vel > 60) {
    return '<strong>Pattern: doctrinal speed.</strong> You commit fast to the template that fits. This wins battles when the template is right and loses campaigns when the adversary has read your doctrine. Action velocity is being mistaken for strategic durability.';
  }
  if (dominant === 'algo') {
    return '<strong>Pattern: cautious doctrinaire.</strong> You reach for the framework and accept its tempo costs. Reliable inside the framework, brittle outside it. Watch for the moment the framework stops describing the problem.';
  }
  if (dominant === 'bric') {
    return '<strong>Pattern: adaptive improviser.</strong> You assemble responses from available tools rather than reaching for templates. Strong in novel terrain. Risk: improvisation without principled grounding drifts into expediency. Bricoleur is a filter, not a destination.';
  }
  if (dominant === 'prin' && pcts.vel < 40) {
    return '<strong>Pattern: principled deliberator.</strong> You hold the line on durability, legality, and second-order consequences. The hardest mode to maintain under tempo pressure and the one PME claims to teach but rarely tests. Watch for paralysis dressed as principle.';
  }
  if (dominant === 'prin') {
    return '<strong>Pattern: principled operator.</strong> You hold the durability line without surrendering tempo. The closest signature to the target pattern. Not stable under sustained crisis without institutional support.';
  }
  return '<strong>Pattern: mixed signal.</strong> No dominant mode emerged across four decisions. This is either genuine flexibility or unsettled doctrine — the difference shows up under sustained pressure, which this instrument does not simulate.';
}

function showResult() {
  document.getElementById('stage').style.display = 'none';
  document.getElementById('result').classList.add('shown');
  const max = 12;
  const pcts = {
    algo: Math.round(Math.max(0, totals.algo) / max * 100),
    bric: Math.round(Math.max(0, totals.bric) / max * 100),
    prin: Math.round(Math.max(0, totals.prin) / max * 100),
    vel: Math.round(Math.max(0, Math.min(100, (totals.vel + 4) / 12 * 100)))
  };
  document.getElementById('algo-pct').textContent = pcts.algo + '%';
  document.getElementById('bric-pct').textContent = pcts.bric + '%';
  document.getElementById('prin-pct').textContent = pcts.prin + '%';
  document.getElementById('vel-pct').textContent = pcts.vel + '%';
  setTimeout(() => {
    document.getElementById('algo-bar').style.width = pcts.algo + '%';
    document.getElementById('bric-bar').style.width = pcts.bric + '%';
    document.getElementById('prin-bar').style.width = pcts.prin + '%';
    document.getElementById('vel-bar').style.width = pcts.vel + '%';
  }, 80);
  document.getElementById('verdict').innerHTML = getVerdict(totals, pcts);
  window.lastResult = pcts;
}

function reset() {
  idx = 0;
  totals = { algo: 0, bric: 0, prin: 0, vel: 0 };
  document.getElementById('stage').style.display = '';
  document.getElementById('result').classList.remove('shown');
  renderDecision();
}

function copyResult() {
  const p = window.lastResult;
  if (!p) return;
  const txt = `Savage Strategist Diagnostic — result
Algorithmic: ${p.algo}%
Bricoleur: ${p.bric}%
Principled action: ${p.prin}%
Velocity bias: ${p.vel}%`;
  navigator.clipboard.writeText(txt).then(() => {
    const btn = document.getElementById('copy-btn');
    const orig = btn.textContent;
    btn.textContent = 'Copied';
    setTimeout(() => { btn.textContent = orig; }, 1500);
  });
}

renderDecision();
</script>
</body>
</html>
