<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>UF Art Museum LCA Manager — EN 15804 Module Game</title>
  <style>
    :root{
      --bg:#0b1220; --card:#0f1930; --card2:#0b142a;
      --border:#223055; --text:#e8eefc; --muted:#b6c3e6;
      --btn:#14224a; --btnh:#1a2a5b;
    }
    body { margin:0; font-family:system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif; background:var(--bg); color:var(--text); }
    header { padding:14px 18px; background:#101a33; border-bottom:1px solid var(--border); }
    header .title { font-size:16px; font-weight:700; }
    header .sub { color:var(--muted); font-size:12px; margin-top:4px; line-height:1.35; }
    main { max-width:1320px; margin:0 auto; padding:18px; }
    .grid { display:grid; grid-template-columns: 1.05fr 0.95fr; gap:14px; align-items:start; }
    .card { background:var(--card); border:1px solid var(--border); border-radius:12px; padding:14px; }
    .row { display:flex; gap:10px; align-items:center; justify-content:space-between; flex-wrap:wrap; }
    h2 { margin:0 0 8px; font-size:15px; }
    h3 { margin:0 0 8px; font-size:13px; color:#dbe7ff; }
    .muted { color:var(--muted); font-size:12px; line-height:1.4; }
    .pill { display:inline-block; padding:2px 8px; border-radius:999px; background:#1a2a5b; border:1px solid #2a3c6c; font-size:12px; color:#cfe0ff; }
    .kpis { display:grid; grid-template-columns: repeat(2, 1fr); gap:10px; margin-top:10px; }
    .kpi { background:var(--card2); border:1px solid var(--border); border-radius:10px; padding:10px; }
    .kpi b { display:block; font-size:12px; color:var(--muted); }
    .kpi span { font-size:18px; }
    .choices { display:grid; gap:10px; margin-top:10px; }
    button {
      width:100%;
      text-align:left;
      padding:12px;
      border-radius:12px;
      border:1px solid #2a3c6c;
      background:var(--btn);
      color:var(--text);
      cursor:pointer;
    }
    button:hover { background:var(--btnh); }
    button:disabled { opacity:.6; cursor:not-allowed; }
    .btnrow { display:flex; gap:10px; margin-top:10px; flex-wrap:wrap; }
    .btnrow button { width:auto; flex:1; min-width:190px; text-align:center; }
    .table { width:100%; border-collapse:collapse; margin-top:10px; font-size:12px; }
    .table th, .table td { border-bottom:1px solid #1e2a4a; padding:6px 6px; vertical-align:top; }
    .barwrap { display:flex; align-items:center; gap:8px; }
    .bar { height:10px; background:#1a2a5b; border:1px solid #2a3c6c; border-radius:999px; flex:1; overflow:hidden; }
    .bar > div { height:100%; background:linear-gradient(90deg, #5aa7ff, #9bd0ff); width:0%; }
    .mono { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; }
    .log { height:170px; overflow:auto; background:#071027; border:1px solid var(--border); border-radius:10px; padding:10px; font-size:12px; white-space:pre-wrap; }
    .small { font-size:11px; }
    .good { color:#a6ffcf; }
    .bad { color:#ffb3b3; }
    .sectionTitle { margin-top:12px; margin-bottom:6px; font-weight:700; font-size:12px; color:#dbe7ff; }
    .split { display:grid; grid-template-columns: 1fr 1fr; gap:10px; }
    .panel { background:#0b142a; border:1px solid var(--border); border-radius:10px; padding:10px; }
    .tabs { display:flex; gap:8px; flex-wrap:wrap; margin-top:10px; }
    .tab {
      padding:8px 10px; border-radius:10px; border:1px solid #2a3c6c;
      background:#0b142a; cursor:pointer; font-size:12px; color:var(--text); user-select:none;
    }
    .tab.active { background:#1a2a5b; }
    .hidden { display:none; }
    @media (max-width: 980px){ .grid{ grid-template-columns: 1fr; } .split{ grid-template-columns: 1fr; } }

    /* === Clearer choice cards === */
    .choice-card {
      width:100%; text-align:left; padding:14px; border-radius:12px;
      border:2px solid #2a3c6c; background:var(--btn); color:var(--text);
      cursor:pointer; transition: border-color 0.15s, background 0.15s;
    }
    .choice-card:hover { background:var(--btnh); }
    .choice-card:disabled { opacity:.5; cursor:not-allowed; }
    .choice-card.green  { border-color:#1e5c30; background:#0d2a18; }
    .choice-card.green:hover  { background:#0f3620; }
    .choice-card.yellow { border-color:#5c4a10; background:#2a2210; }
    .choice-card.yellow:hover { background:#332a12; }
    .choice-card.red    { border-color:#5c1a1a; background:#2a0f0f; }
    .choice-card.red:hover    { background:#3a1212; }
    .choice-title { font-size:14px; font-weight:700; margin-bottom:4px; }
    .choice-desc  { font-size:12px; color:var(--muted); margin-bottom:10px; }
    .impact-chips { display:flex; flex-wrap:wrap; gap:6px; margin-bottom:10px; }
    .chip {
      display:inline-flex; align-items:center; gap:4px;
      padding:3px 9px; border-radius:999px; font-size:12px; font-weight:600;
      border:1px solid;
    }
    .chip-carbon-good { background:#0d2a18; border-color:#1e5c30; color:#a6ffcf; }
    .chip-carbon-bad  { background:#2a0f0f; border-color:#5c1a1a; color:#ffb3b3; }
    .chip-carbon-neu  { background:#0b142a; border-color:#2a3c6c; color:#b6c3e6; }
    .chip-cost-bad    { background:#2a1e0a; border-color:#6b4a10; color:#ffd6a0; }
    .chip-cost-good   { background:#0a2018; border-color:#1a5c30; color:#a6ffcf; }
    .chip-cost-neu    { background:#0b142a; border-color:#2a3c6c; color:#b6c3e6; }
    .chip-sched-bad   { background:#2a1a0a; border-color:#6b3a10; color:#ffd6a0; }
    .chip-sched-good  { background:#0a1a2a; border-color:#1a3c5c; color:#a0d4ff; }
    .chip-sched-neu   { background:#0b142a; border-color:#2a3c6c; color:#b6c3e6; }
    .chip-cred-good   { background:#0d1f2a; border-color:#1a4a6b; color:#a0d4ff; }
    .chip-cred-bad    { background:#2a0f1a; border-color:#5c1a30; color:#ffb3b3; }
    .chip-cred-neu    { background:#0b142a; border-color:#2a3c6c; color:#b6c3e6; }
    .consequence-box {
      font-size:12px; padding:7px 10px; border-radius:8px;
      border-left:3px solid #5aa7ff; background:#071830; color:#cfe0ff;
      margin-bottom:8px;
    }
    .insight-box {
      font-size:12px; padding:7px 10px; border-radius:8px;
      border-left:3px solid #a0d4ff; background:#040e1f; color:#b6c3e6;
    }
    .insight-label { font-weight:700; color:#dbe7ff; }
    /* Progress bar */
    .progress-wrap { margin:10px 0 14px; }
    .progress-label { font-size:12px; color:var(--muted); margin-bottom:4px; }
    .progress-track { height:8px; background:#1a2a5b; border-radius:999px; overflow:hidden; }
    .progress-fill  { height:100%; background:linear-gradient(90deg,#5aa7ff,#9bd0ff); border-radius:999px; transition:width 0.3s; }
  </style>
</head>
<body>
<header>
  <div class="title">UF Art Museum — LCA Manager (EN 15804 Modules)</div>
  <div class="sub">
    Play in your browser: make one decision per module (A1–A5, B1–B7, C1–C4, D). Export CSV + a printable submission report.
  </div>
</header>

<main>
  <div class="grid">
    <section class="card">
      <div class="row">
        <div>
          <h2 id="levelTitle">Level</h2>
          <div class="muted" id="levelBrief"></div>
          <div class="muted small" id="levelScopeNote"></div>
        </div>
        <div class="pill" id="levelPill">—</div>
      </div>

      <div class="progress-wrap">
        <div class="progress-label" id="progressLabel">Module 1 of 17</div>
        <div class="progress-track"><div class="progress-fill" id="progressFill" style="width:0%"></div></div>
      </div>

      <div class="panel" style="margin-top:0;">
        <div class="row">
          <h3 style="margin:0;">What is this module?</h3>
          <span class="pill mono" id="moduleExplainerCode">—</span>
        </div>
        <div class="muted" id="moduleExplainerText"></div>
        <div class="muted small" id="moduleExplainerTip" style="margin-top:6px;"></div>
      </div>

      <div class="choices" id="choices"></div>

      <div class="btnrow">
        <button id="restartBtn">Restart</button>
        <button id="trialBtn">Auto Trial Run</button>
        <button id="nextBtn">Next Module</button>
      </div>

      <div class="tabs">
        <div class="tab active" id="tabLogBtn">Decision log</div>
        <div class="tab" id="tabReportBtn">Submission report</div>
      </div>

      <div id="tabLog" class="panel">
        <div class="log mono" id="log"></div>
      </div>

      <div id="tabReport" class="panel hidden">
        <div class="row">
          <h3 style="margin:0;">Printable submission report</h3>
          <button id="downloadReportBtn" style="width:auto; min-width:240px; text-align:center;">Download report (HTML)</button>
        </div>
        <div class="muted" id="reportSummary"></div>
        <div class="muted small" style="margin-top:8px;">
          After downloading, open the report in your browser and use "Print → Save as PDF" if needed.
        </div>
      </div>
    </section>

    <aside class="card">
      <h2>Dashboard</h2>
      <div class="muted">
        "Gross" = A+B+C. Module D is reported separately; "Net" = Gross + D.
      </div>

      <div class="kpis">
        <div class="kpi"><b>Gross total (A+B+C)</b><span id="kpiGross">—</span><div class="muted">tCO₂e</div></div>
        <div class="kpi"><b>Module D total</b><span id="kpiD">—</span><div class="muted">tCO₂e</div></div>
        <div class="kpi"><b>Net (A+B+C + D)</b><span id="kpiNet">—</span><div class="muted">tCO₂e</div></div>
        <div class="kpi"><b>Target (≤, gross)</b><span id="kpiTarget">—</span><div class="muted">tCO₂e</div></div>
      </div>

      <div class="kpis" style="margin-top:10px;">
        <div class="kpi"><b>Additional cost</b><span id="kpiCost">—</span><div class="muted">M USD (cap)</div></div>
        <div class="kpi"><b>Schedule impact</b><span id="kpiSched">—</span><div class="muted">weeks (cap)</div></div>
      </div>

      <div class="kpis" style="margin-top:10px;">
        <div class="kpi"><b>Credibility</b><span id="kpiCred">—</span><div class="muted">/100</div></div>
        <div class="kpi"><b>Status</b><span id="kpiStatus">—</span><div class="muted">constraints</div></div>
      </div>

      <div class="split">
        <div>
          <div class="sectionTitle">Hotspots by Module</div>
          <table class="table" id="stageTable"></table>
        </div>
        <div>
          <div class="sectionTitle">Hotspots by System (gross only)</div>
          <table class="table" id="systemTable"></table>
        </div>
      </div>

      <div class="sectionTitle">A3 Fabrication Sub-process Breakdown</div>
      <table class="table" id="a3Table"></table>

      <div class="sectionTitle">Module D Breakdown (beyond system boundary)</div>
      <table class="table" id="dTable"></table>

      <div class="sectionTitle">Export</div>
      <div class="btnrow">
        <button id="exportRunBtn">Download CSV (this run)</button>
        <button id="exportSnapshotBtn">Download CSV (full snapshot)</button>
      </div>
      <div class="muted small">
        "This run" exports module-by-module KPI history. "Full snapshot" exports every Module×Process×System bucket including D.
      </div>
    </aside>
  </div>
</main>

<script>
/* =========================
   EN 15804 modules as stages
========================= */
const STAGES_ABC = ["A1","A2","A3","A4","A5","B1","B2","B3","B4","B5","B6","B7","C1","C2","C3","C4"];
const STAGE_D = ["D"];
const STAGES_ALL = [...STAGES_ABC, ...STAGE_D];

const SYSTEMS = ["Structure","Envelope","Interiors","MEP","Site/Other","Construction"];

const PROCESSES_BY_STAGE = {
  "A1": ["Raw material supply"],
  "A2": ["Transport to manufacturer"],
  "A3": [
    "Primary production (cement/steel/glass)",
    "Fabrication shop (cut/weld/form)",
    "Coatings/finishes (paint/anodize)",
    "Assembly/packaging (components)",
    "Factory energy (electricity/heat)",
    "Scrap & yield loss (manufacturing waste)"
  ],
  "A4": ["Transport to site"],
  "A5": ["Onsite equipment & fuel","Waste & rework","Temporary works","Crew travel (commute/vehicles)"],

  "B1": ["Use (direct impacts)"],
  "B2": ["Maintenance (materials & travel)"],
  "B3": ["Repair (materials & travel)"],
  "B4": ["Replacement (materials & install)"],
  "B5": ["Refurbishment (materials & install)"],
  "B6": ["Operational energy use"],
  "B7": ["Operational water use"],

  "C1": ["Deconstruction/demolition"],
  "C2": ["Transport to waste processing"],
  "C3": ["Waste processing (sorting/recycling)"],
  "C4": ["Disposal (landfill/incineration)"],

  "D": ["Beyond system boundary benefits/loads"]
};

const STAGE_LABEL = {
  "A1":"Raw material supply","A2":"Transport to manufacturer","A3":"Manufacturing / fabrication",
  "A4":"Transport to site","A5":"Construction / installation",
  "B1":"Use","B2":"Maintenance","B3":"Repair","B4":"Replacement","B5":"Refurbishment","B6":"Operational energy","B7":"Operational water",
  "C1":"Deconstruction","C2":"Transport (waste)","C3":"Waste processing","C4":"Disposal",
  "D":"Beyond system boundary (Module D)"
};

const MODULE_EXPLAINERS = {
  "A1": { text: "Raw material supply for product/material production (upstream extraction and processing).", tip: "Most embodied-carbon hotspots in buildings live here (cement, steel, glass, aluminum)." },
  "A2": { text: "Transport of raw materials to the manufacturer.", tip: "Usually smaller than A1/A3, but can matter for heavy/bulky materials and long distances." },
  "A3": { text: "Manufacturing/fabrication of products (including factory energy and yield losses).", tip: "Use the A3 process breakdown to see whether scrap, shop work, coatings, or energy dominate." },
  "A4": { text: "Transport of products/materials to the construction site.", tip: "Logistics decisions (consolidation, distance, mode) show up here." },
  "A5": { text: "Construction/installation processes (site energy, waste, rework, temporary works).", tip: "Waste prevention and coordination can cut A5 without changing design intent." },
  "B1": { text: "Use stage direct impacts during use (often minimal for many materials).", tip: "For museums, many practical interventions show up more in B2–B5." },
  "B2": { text: "Maintenance during use (materials, consumables, travel, minor works).", tip: "Good maintenance planning can reduce whole-life impacts and improve performance." },
  "B3": { text: "Repair impacts during use (materials and activities needed to restore performance).", tip: "Durability and protection strategies can reduce repairs." },
  "B4": { text: "Replacement of components over service life.", tip: "Often a big driver for interiors/finishes and some MEP components—document service lives." },
  "B5": { text: "Refurbishment/renovation impacts (major refreshes/changes).", tip: "Museums renovate galleries; flexibility/modularity can reduce refurbishment burden." },
  "B6": { text: "Operational energy use (not embodied). Included for completeness in EN 15804.", tip: "If included, keep it clearly separated from embodied-carbon claims." },
  "B7": { text: "Operational water use (not embodied). Included for completeness in EN 15804.", tip: "Separate it and document assumptions." },
  "C1": { text: "Deconstruction/demolition at end-of-life.", tip: "Design for disassembly can reduce burdens and improve recovery." },
  "C2": { text: "Transport of waste to processing/disposal facilities.", tip: "Depends on realistic routing and facility distances." },
  "C3": { text: "Waste processing (sorting, recycling processes, recovery operations).", tip: "Recycling claims require evidence; conservative documented assumptions are safer." },
  "C4": { text: "Final disposal (landfill/incineration).", tip: "Diversion strategies affect C4; local reality matters." },
  "D":  { text: "Benefits/loads beyond the system boundary (e.g., credits from reuse/recycling in future systems). Report separately.", tip: "Overstated D credits can undermine credibility." },
};

/* =========================
   3D matrix utilities
========================= */
function empty3D() {
  const m = {};
  for (const s of STAGES_ALL) {
    m[s] = {};
    for (const p of PROCESSES_BY_STAGE[s]) {
      m[s][p] = {};
      for (const sys of SYSTEMS) m[s][p][sys] = 0;
    }
  }
  return m;
}
function deepCopy3D(m){
  const out = {};
  for (const s of STAGES_ALL){
    out[s] = {};
    for (const p of PROCESSES_BY_STAGE[s]){
      out[s][p] = {};
      for (const sys of SYSTEMS){
        out[s][p][sys] = m[s][p][sys];
      }
    }
  }
  return out;
}
function total3D(m, stages){
  let t = 0;
  for (const s of stages) for (const p of PROCESSES_BY_STAGE[s]) for (const sys of SYSTEMS) t += m[s][p][sys];
  return t;
}
function totalsByStage(m, stages){
  const out = {};
  for (const s of stages){
    let v = 0;
    for (const p of PROCESSES_BY_STAGE[s]) for (const sys of SYSTEMS) v += m[s][p][sys];
    out[s] = v;
  }
  return out;
}
function totalsBySystem(m, stages){
  const out = {};
  for (const sys of SYSTEMS) out[sys] = 0;
  for (const s of stages){
    for (const p of PROCESSES_BY_STAGE[s]){
      for (const sys of SYSTEMS) out[sys] += m[s][p][sys];
    }
  }
  return out;
}
function totalsByProcessWithinStage(m, stage){
  const out = {};
  for (const p of PROCESSES_BY_STAGE[stage]){
    let v = 0;
    for (const sys of SYSTEMS) v += m[stage][p][sys];
    out[p] = v;
  }
  return out;
}
function multStageSystem(m, stage, system, mult){
  for (const p of PROCESSES_BY_STAGE[stage]) m[stage][p][system] *= mult;
}
function multBucket(m, stage, process, system, mult){
  m[stage][process][system] *= mult;
}
function multStageAll(m, stage, mult){
  for (const p of PROCESSES_BY_STAGE[stage]) for (const sys of SYSTEMS) m[stage][p][sys] *= mult;
}

/* =========================
   Game state + baseline
========================= */
const initialState = () => ({
  lca: empty3D(),
  costM: 0,
  schedW: 0,
  cred: 78,

  reductionTargetPct: 30,
  maxCostM: 8.0,
  maxSchedW: 14,
  minCred: 70,

  baselineGross: 0,
  levelIndex: 0,
  chosenThisLevel: false,
  runHistory: [],
});

let state = initialState();

function seedBaseline(){
  const stageTotals = {
    "A1": 3200, "A2": 220, "A3": 2350, "A4": 300, "A5": 650,
    "B1": 0, "B2": 80, "B3": 60, "B4": 700, "B5": 120, "B6": 0, "B7": 0,
    "C1": 90, "C2": 70, "C3": 120, "C4": 300,
    "D": 0
  };

  const sysShare = {
    "A1": {"Structure":0.52,"Envelope":0.22,"Interiors":0.08,"MEP":0.12,"Site/Other":0.04,"Construction":0.02},
    "A2": {"Structure":0.45,"Envelope":0.25,"Interiors":0.10,"MEP":0.15,"Site/Other":0.05,"Construction":0.00},
    "A3": {"Structure":0.45,"Envelope":0.25,"Interiors":0.10,"MEP":0.15,"Site/Other":0.03,"Construction":0.02},
    "A4": {"Structure":0.40,"Envelope":0.30,"Interiors":0.10,"MEP":0.15,"Site/Other":0.05,"Construction":0.00},
    "A5": {"Structure":0.35,"Envelope":0.15,"Interiors":0.15,"MEP":0.10,"Site/Other":0.05,"Construction":0.20},

    "B1": {"Structure":0.0,"Envelope":0.0,"Interiors":0.0,"MEP":0.0,"Site/Other":0.0,"Construction":0.0},
    "B2": {"Structure":0.02,"Envelope":0.10,"Interiors":0.45,"MEP":0.38,"Site/Other":0.05,"Construction":0.00},
    "B3": {"Structure":0.02,"Envelope":0.10,"Interiors":0.40,"MEP":0.43,"Site/Other":0.05,"Construction":0.00},
    "B4": {"Structure":0.02,"Envelope":0.10,"Interiors":0.55,"MEP":0.28,"Site/Other":0.03,"Construction":0.02},
    "B5": {"Structure":0.01,"Envelope":0.08,"Interiors":0.58,"MEP":0.28,"Site/Other":0.05,"Construction":0.00},
    "B6": {"Structure":0.0,"Envelope":0.0,"Interiors":0.0,"MEP":1.0,"Site/Other":0.0,"Construction":0.0},
    "B7": {"Structure":0.0,"Envelope":0.0,"Interiors":0.0,"MEP":1.0,"Site/Other":0.0,"Construction":0.0},

    "C1": {"Structure":0.45,"Envelope":0.20,"Interiors":0.20,"MEP":0.10,"Site/Other":0.05,"Construction":0.00},
    "C2": {"Structure":0.45,"Envelope":0.20,"Interiors":0.20,"MEP":0.10,"Site/Other":0.05,"Construction":0.00},
    "C3": {"Structure":0.42,"Envelope":0.20,"Interiors":0.20,"MEP":0.10,"Site/Other":0.08,"Construction":0.00},
    "C4": {"Structure":0.40,"Envelope":0.18,"Interiors":0.20,"MEP":0.10,"Site/Other":0.12,"Construction":0.00},

    "D":  {"Structure":0.55,"Envelope":0.15,"Interiors":0.15,"MEP":0.10,"Site/Other":0.05,"Construction":0.00},
  };

  const a3ProcShare = {
    "Primary production (cement/steel/glass)":0.38,
    "Fabrication shop (cut/weld/form)":0.18,
    "Coatings/finishes (paint/anodize)":0.07,
    "Assembly/packaging (components)":0.08,
    "Factory energy (electricity/heat)":0.17,
    "Scrap & yield loss (manufacturing waste)":0.12
  };
  const a5ProcShare = {"Onsite equipment & fuel":0.33,"Waste & rework":0.30,"Temporary works":0.22,"Crew travel (commute/vehicles)":0.15};

  for (const s of STAGES_ALL){
    const total = stageTotals[s];
    if (s === "A3"){
      for (const [p,ps] of Object.entries(a3ProcShare)){
        for (const sys of SYSTEMS) state.lca[s][p][sys] = total * ps * sysShare[s][sys];
      }
    } else if (s === "A5"){
      for (const [p,ps] of Object.entries(a5ProcShare)){
        for (const sys of SYSTEMS) state.lca[s][p][sys] = total * ps * sysShare[s][sys];
      }
    } else {
      const p = PROCESSES_BY_STAGE[s][0];
      for (const sys of SYSTEMS) state.lca[s][p][sys] = total * sysShare[s][sys];
    }
  }

  state.baselineGross = total3D(state.lca, STAGES_ABC);
}

function clampCred(){ state.cred = Math.max(0, Math.min(100, state.cred)); }
function targetGross(){ return state.baselineGross * (1 - state.reductionTargetPct/100); }

/* =========================
   Levels (modules) + choices
========================= */
function moduleLevels(){
  return [
    { id:"A1", title:"A1 — Raw material supply", scope:"Product stage (A1–A3).", brief:"Choose material sourcing strategies (recycled content, lower-carbon cement/steel, EPD selection).", choices:[
      { title:"Low-carbon concrete SCM targets", desc:"Reduce clinker intensity for structure & foundations.", learning:"A1 is often dominated by cement/steel primary burdens.", act:()=>{ multStageSystem(state.lca,"A1","Structure",0.78); state.costM += 0.90; state.schedW += 1; state.cred += 2; }},
      { title:"High-recycled EAF steel for structural steel", desc:"Shift to EAF and verified recycled content for applicable packages.", learning:"Steel routes vary; EPD-backed procurement improves credibility.", act:()=>{ multStageSystem(state.lca,"A1","Structure",0.86); state.costM += 0.70; state.cred += 2; }},
      { title:"Baseline procurement (supplier averages)", desc:"No special sourcing requirements.", learning:"Leaving A1 untouched usually preserves the biggest hotspot.", act:()=>{ state.cred -= 1; }},
    ]},
    { id:"A2", title:"A2 — Transport to manufacturer", scope:"Product stage (A1–A3).", brief:"Reduce upstream transport impacts (supplier distance, mode, consolidation).", choices:[
      { title:"Supplier consolidation + shorter upstream routes", desc:"Reduce A2 transport distances for major materials.", learning:"A2 is usually smaller than A1/A3 but can matter in aggregate.", act:()=>{ multStageAll(state.lca,"A2",0.85); state.costM += 0.15; state.cred += 1; }},
      { title:"Shift upstream freight to rail/ship where possible", desc:"Mode shift for bulk materials.", learning:"Mode choice can reduce transport emissions, but needs logistics feasibility.", act:()=>{ multStageAll(state.lca,"A2",0.80); state.costM += 0.10; state.schedW += 1; }},
      { title:"No upstream logistics intervention", desc:"Keep baseline logistics.", learning:"A2 remains unchanged.", act:()=>{}},
    ]},
    { id:"A3", title:"A3 — Manufacturing / fabrication", scope:"Product stage (A1–A3).", brief:"Reduce fabrication emissions via yield, shop efficiency, coatings choices, and factory energy.", choices:[
      { title:"Reduce fabrication scrap via standardization + QA", desc:"Targets A3 scrap/yield and shop work.", learning:"A3 can be driven by yield losses and fabrication energy.", act:()=>{ multBucket(state.lca,"A3","Scrap & yield loss (manufacturing waste)","Structure",0.78); multBucket(state.lca,"A3","Fabrication shop (cut/weld/form)","Structure",0.92); state.costM += 0.35; state.schedW += 1; state.cred += 2; }},
      { title:"Lower-impact coatings/finishes where feasible", desc:"Reduce coatings intensity for envelope/interiors packages.", learning:"Coatings can be material/energy intensive; details matter.", act:()=>{ multBucket(state.lca,"A3","Coatings/finishes (paint/anodize)","Envelope",0.88); multBucket(state.lca,"A3","Coatings/finishes (paint/anodize)","Interiors",0.85); state.costM += 0.20; state.cred += 1; }},
      { title:"Supplier renewable electricity requirement", desc:"Reduce 'factory energy' in key supplier packages.", learning:"Supplier energy affects A3 'factory energy' directly.", act:()=>{ multBucket(state.lca,"A3","Factory energy (electricity/heat)","Structure",0.85); multBucket(state.lca,"A3","Factory energy (electricity/heat)","Envelope",0.88); multBucket(state.lca,"A3","Factory energy (electricity/heat)","MEP",0.88); state.costM += 0.55; state.cred += 2; }},
    ]},
    { id:"A4", title:"A4 — Transport to site", scope:"Construction stage (A4–A5).", brief:"Cut A4 by reducing distance, consolidating deliveries, and shifting modes.", choices:[
      { title:"Consolidate deliveries + optimize routes", desc:"Fewer trips and better load factors.", learning:"A4 is logistics-driven; consolidation reduces emissions per delivered unit.", act:()=>{ multStageAll(state.lca,"A4",0.88); state.costM += 0.10; state.cred += 1; }},
      { title:"Regional sourcing for heavy materials", desc:"Shorter distances for bulk deliveries.", learning:"Distance matters most for heavy, bulky materials.", act:()=>{ multStageAll(state.lca,"A4",0.85); state.costM += 0.20; state.schedW += 1; }},
      { title:"Baseline A4 logistics", desc:"No intervention.", learning:"A4 remains unchanged.", act:()=>{}},
    ]},
    { id:"A5", title:"A5 — Installation / construction", scope:"Construction stage (A4–A5).", brief:"Reduce waste & rework; manage temporary works; electrify site equipment where possible.", choices:[
      { title:"Waste prevention + prefab + tracking", desc:"Reduce rework and capture better data.", learning:"A5 reductions often come from waste prevention and fewer mistakes.", act:()=>{ multBucket(state.lca,"A5","Waste & rework","Construction",0.80); multBucket(state.lca,"A5","Temporary works","Construction",0.88); multBucket(state.lca,"A5","Onsite equipment & fuel","Construction",0.92); state.costM += 0.30; state.cred += 3; }},
      { title:"Crash schedule (more overtime/rework)", desc:"Schedule improves but A5 usually rises.", learning:"Schedule acceleration can increase rework and fuel use.", act:()=>{ multBucket(state.lca,"A5","Waste & rework","Construction",1.10); multBucket(state.lca,"A5","Onsite equipment & fuel","Construction",1.08); state.costM += 0.65; state.schedW -= 2; state.cred -= 1; }},
      { title:"Baseline construction approach", desc:"Minimal tracking.", learning:"Less proof reduces credibility.", act:()=>{ state.cred -= 2; }},
    ]},
    { id:"B1", title:"B1 — Use", scope:"Use stage (B1–B7).", brief:"Direct impacts from use/application of installed product (often minimal for many materials).", choices:[
      { title:"No change (B1 negligible here)", desc:"Keep baseline.", learning:"B1 is often small for many building-material LCAs.", act:()=>{}},
      { title:"Protective measures to reduce damage to finishes", desc:"May reduce downstream repairs/replacements.", learning:"Some B1 actions show up later in B3/B4.", act:()=>{ state.costM += 0.10; state.cred += 1; }},
      { title:"Unverified assumption: B1 = 0 always", desc:"You claim zero without justification.", learning:"Unjustified assumptions reduce credibility.", act:()=>{ state.cred -= 6; }},
    ]},
    { id:"B2", title:"B2 — Maintenance", scope:"Use stage (B1–B7).", brief:"Maintenance materials + travel can add up (cleaning, filters, minor works).", choices:[
      { title:"Maintenance optimization plan (reduce consumables)", desc:"Lower maintenance material usage.", learning:"Maintenance reductions are incremental but credible when documented.", act:()=>{ multStageAll(state.lca,"B2",0.85); state.costM += 0.15; state.cred += 2; }},
      { title:"Baseline maintenance plan", desc:"No changes.", learning:"B2 remains unchanged.", act:()=>{}},
      { title:"Assume unrealistically low maintenance", desc:"Looks good but risky.", learning:"Unrealistic assumptions hurt credibility.", act:()=>{ multStageAll(state.lca,"B2",0.70); state.cred -= 12; }},
    ]},
    { id:"B3", title:"B3 — Repair", scope:"Use stage (B1–B7).", brief:"Repair impacts depend on durability and protection strategies.", choices:[
      { title:"Durability detailing + protection (reduce repairs)", desc:"Reduce repair frequency.", learning:"Plausible if tied to detailing/specs.", act:()=>{ multStageAll(state.lca,"B3",0.85); state.costM += 0.20; state.cred += 1; }},
      { title:"Baseline repair assumptions", desc:"No changes.", learning:"B3 remains unchanged.", act:()=>{}},
      { title:"Optimistic repair assumptions without evidence", desc:"Model says great; reviewers disagree.", learning:"Unsupported optimism hurts credibility.", act:()=>{ multStageAll(state.lca,"B3",0.70); state.cred -= 10; }},
    ]},
    { id:"B4", title:"B4 — Replacement", scope:"Use stage (B1–B7).", brief:"Replacement is often a major whole-life hotspot (especially interiors).", choices:[
      { title:"EPD-based finishes + longer service life", desc:"Reduce replacement frequency for interiors.", learning:"Service life assumptions must be documented.", act:()=>{ multStageSystem(state.lca,"B4","Interiors",0.75); state.costM += 0.55; state.cred += 5; }},
      { title:"Value engineer finishes (more frequent replacement)", desc:"Lower cost now, more replacement later.", learning:"Short-term savings can increase whole-life carbon.", act:()=>{ multStageSystem(state.lca,"B4","Interiors",1.12); state.costM -= 0.60; state.schedW -= 1; state.cred -= 8; }},
      { title:"Baseline replacement assumptions", desc:"No change.", learning:"B4 remains unchanged.", act:()=>{}},
    ]},
    { id:"B5", title:"B5 — Refurbishment", scope:"Use stage (B1–B7).", brief:"Museums reconfigure galleries; flexibility can reduce refurbishment impacts.", choices:[
      { title:"Design for flexibility (modular partitions, reusable systems)", desc:"Reduce refurbishment material intensity.", learning:"Flexibility can cut B5 if tied to realistic cycles.", act:()=>{ multStageAll(state.lca,"B5",0.82); state.costM += 0.35; state.cred += 2; }},
      { title:"Baseline refurbishment assumptions", desc:"No changes.", learning:"B5 remains unchanged.", act:()=>{}},
      { title:"Assume no refurbishments ever", desc:"Unrealistic for museums.", learning:"Unrealistic B5 assumptions hurt credibility.", act:()=>{ multStageAll(state.lca,"B5",0.0); state.cred -= 14; }},
    ]},
    { id:"B6", title:"B6 — Operational energy", scope:"Use stage (B1–B7).", brief:"Operational energy is not embodied, but EN15804 includes it for completeness.", choices:[
      { title:"Track B6 separately (do not mix with embodied target)", desc:"You keep B6 in the table but don't use it for the embodied target.", learning:"Clear scoping avoids mixing metrics.", act:()=>{ state.cred += 1; }},
      { title:"Include placeholder B6 estimate (transparent)", desc:"Adds an operational placeholder to show completeness.", learning:"If you include B6, label it clearly and document assumptions.", act:()=>{ const p=PROCESSES_BY_STAGE["B6"][0]; state.lca["B6"][p]["MEP"] += 250; state.cred += 1; state.costM += 0.10; }},
      { title:"Ignore B6 without disclosure", desc:"Omit it quietly.", learning:"Omissions without disclosure reduce credibility.", act:()=>{ state.cred -= 6; }},
    ]},
    { id:"B7", title:"B7 — Operational water", scope:"Use stage (B1–B7).", brief:"Operational water is not embodied; included for completeness.", choices:[
      { title:"Track B7 separately (do not mix with embodied target)", desc:"You keep B7 visible but separated.", learning:"Transparency helps credibility.", act:()=>{ state.cred += 1; }},
      { title:"Include placeholder B7 estimate (transparent)", desc:"Adds an operational placeholder to show completeness.", learning:"Document assumptions.", act:()=>{ const p=PROCESSES_BY_STAGE["B7"][0]; state.lca["B7"][p]["MEP"] += 40; state.cred += 1; state.costM += 0.05; }},
      { title:"Omit B7 without disclosure", desc:"Not recommended.", learning:"Disclosure matters.", act:()=>{ state.cred -= 5; }},
    ]},
    { id:"C1", title:"C1 — Deconstruction/demolition", scope:"End-of-life stage (C1–C4).", brief:"Design for disassembly can reduce C1 burdens and support circularity.", choices:[
      { title:"Design for disassembly detailing", desc:"Reduce deconstruction intensity.", learning:"Feasibility depends on design and documentation.", act:()=>{ multStageAll(state.lca,"C1",0.90); state.costM += 0.30; state.schedW += 1; state.cred += 2; }},
      { title:"Baseline demolition assumptions", desc:"No changes.", learning:"C1 remains unchanged.", act:()=>{}},
      { title:"Assume effortless deconstruction (unjustified)", desc:"Looks good but fragile.", learning:"Over-optimism hurts credibility.", act:()=>{ multStageAll(state.lca,"C1",0.75); state.cred -= 10; }},
    ]},
    { id:"C2", title:"C2 — Transport to waste processing", scope:"End-of-life stage (C1–C4).", brief:"Depends on waste routing and local facilities.", choices:[
      { title:"Local waste routing + consolidation", desc:"Reduce transport burdens.", learning:"Depends on realistic routing and distances.", act:()=>{ multStageAll(state.lca,"C2",0.85); state.costM += 0.10; state.cred += 1; }},
      { title:"Baseline C2 routing", desc:"No change.", learning:"C2 remains unchanged.", act:()=>{}},
      { title:"Assume zero C2 transport", desc:"Not credible.", learning:"Zero-transport assumptions are indefensible.", act:()=>{ multStageAll(state.lca,"C2",0.0); state.cred -= 14; }},
    ]},
    { id:"C3", title:"C3 — Waste processing", scope:"End-of-life stage (C1–C4).", brief:"Processing burdens and recovery rates need evidence.", choices:[
      { title:"Documented recycling pathways (conservative)", desc:"Small improvement but defensible.", learning:"Conservative documented assumptions are safer.", act:()=>{ multStageAll(state.lca,"C3",0.90); state.costM += 0.10; state.cred += 2; }},
      { title:"Optimistic recycling without evidence", desc:"Big modeled reduction, credibility hit.", learning:"Unsupported assumptions can get your LCA rejected.", act:()=>{ multStageAll(state.lca,"C3",0.70); state.cred -= 18; }},
      { title:"Baseline C3", desc:"No changes.", learning:"C3 remains unchanged.", act:()=>{}},
    ]},
    { id:"C4", title:"C4 — Disposal", scope:"End-of-life stage (C1–C4).", brief:"Landfill/incineration burdens; affected by diversion strategies.", choices:[
      { title:"Diversion plan + documented disposal assumptions", desc:"Reduce disposal burdens modestly.", learning:"Diversion must match local capability.", act:()=>{ multStageAll(state.lca,"C4",0.90); state.costM += 0.10; state.cred += 1; }},
      { title:"Assume minimal disposal without evidence", desc:"Not credible.", learning:"Disposal assumptions are scrutinized.", act:()=>{ multStageAll(state.lca,"C4",0.75); state.cred -= 14; }},
      { title:"Baseline disposal", desc:"No changes.", learning:"C4 remains unchanged.", act:()=>{}},
    ]},
    { id:"D", title:"Module D — Beyond system boundary", scope:"Beyond system boundary (report separately).", brief:"Potential credits/loads from reuse, recycling, or recovery beyond the building life cycle.", choices:[
      { title:"Conservative Module D credits (documented)", desc:"Small credits with strong evidence.", learning:"Module D should be reported separately; conservative is safest.", act:()=>{ const p=PROCESSES_BY_STAGE["D"][0]; state.lca["D"][p]["Structure"] -= 260; state.lca["D"][p]["Envelope"] -= 80; state.cred += 2; state.costM += 0.10; }},
      { title:"Optimistic high Module D credits (weak evidence)", desc:"Large credits but credibility hit.", learning:"Overstated D credits can undermine the entire study.", act:()=>{ const p=PROCESSES_BY_STAGE["D"][0]; state.lca["D"][p]["Structure"] -= 650; state.lca["D"][p]["Envelope"] -= 180; state.cred -= 12; }},
      { title:"No Module D reported", desc:"Omit Module D entirely.", learning:"Omission reduces completeness.", act:()=>{ state.cred -= 6; }},
    ]},
  ];
}

/* =========================
   Rendering + gameplay
========================= */
function fmt0(n){ return Math.round(n).toString(); }
function fmt2(n){ return (Math.round(n*100)/100).toFixed(2); }

function snapshotKPIs(){
  const gross = total3D(state.lca, STAGES_ABC);
  const dTotal = total3D(state.lca, STAGE_D);
  const net = gross + dTotal;
  return {
    levelIndex: state.levelIndex,
    gross_tco2e:gross,
    d_tco2e:dTotal,
    net_tco2e:net,
    target_gross_tco2e: targetGross(),
    cost_musd: state.costM,
    schedule_weeks: state.schedW,
    credibility: state.cred
  };
}
function statusText(){
  const s = snapshotKPIs();
  const passCarbon = s.gross_tco2e <= s.target_gross_tco2e;
  const passCost = state.costM <= state.maxCostM;
  const passSched = state.schedW <= state.maxSchedW;
  const passCred = state.cred >= state.minCred;
  const ok = passCarbon && passCost && passSched && passCred;
  return { ok, passCarbon, passCost, passSched, passCred, ...s };
}
function logLine(msg){
  const el = document.getElementById("log");
  el.textContent += msg + "\n";
  el.scrollTop = el.scrollHeight;
}
function renderBarRow(label, value, maxValue, rightText){
  const w = maxValue ? (Math.abs(value)/maxValue*100) : 0;
  return `
    <tr>
      <td class="mono">${label}</td>
      <td class="mono" style="text-align:right;">${fmt0(value)}</td>
      <td>
        <div class="barwrap">
          <div class="bar"><div style="width:${Math.max(0,Math.min(100,w))}%"></div></div>
          <span class="mono">${rightText}</span>
        </div>
      </td>
    </tr>`;
}
function renderTables(){
  const gross = total3D(state.lca, STAGES_ABC);
  const dTotal = total3D(state.lca, STAGE_D);

  // module table
  const byStage = totalsByStage(state.lca, STAGES_ALL);
  const stageMax = Math.max(...Object.values(byStage).map(v=>Math.abs(v))) || 1;
  let stageHtml = `<tr><th>Module</th><th>tCO2e</th><th style="width:60%;">Magnitude / share</th></tr>`;
  for (const s of STAGES_ALL){
    const v = byStage[s];
    const denom = (s==="D") ? (Math.abs(dTotal)||1) : (gross||1);
    const share = denom ? (v/denom*100) : 0;
    stageHtml += renderBarRow(s, v, stageMax, (s==="D") ? `${share.toFixed(1)}% of D` : `${share.toFixed(1)}% of gross`);
  }
  document.getElementById("stageTable").innerHTML = stageHtml;

  // system (gross only)
  const bySys = totalsBySystem(state.lca, STAGES_ABC);
  const sysMax = Math.max(...Object.values(bySys)) || 1;
  let sysHtml = `<tr><th>System</th><th>tCO2e</th><th style="width:60%;">Share of gross</th></tr>`;
  for (const sys of SYSTEMS){
    const v = bySys[sys];
    const share = gross ? (v/gross*100) : 0;
    sysHtml += renderBarRow(sys, v, sysMax, `${share.toFixed(1)}%`);
  }
  document.getElementById("systemTable").innerHTML = sysHtml;

  // A3 breakdown
  const a3 = totalsByProcessWithinStage(state.lca, "A3");
  const a3Total = Object.values(a3).reduce((a,b)=>a+b,0) || 1;
  const a3Max = Math.max(...Object.values(a3)) || 1;
  let a3Html = `<tr><th>A3 process</th><th>tCO2e</th><th style="width:60%;">Share of A3</th></tr>`;
  for (const p of PROCESSES_BY_STAGE["A3"]){
    const v = a3[p] || 0;
    const share = (v/a3Total*100);
    a3Html += `
      <tr>
        <td>${p}</td>
        <td class="mono" style="text-align:right;">${fmt0(v)}</td>
        <td>
          <div class="barwrap">
            <div class="bar"><div style="width:${Math.max(0,Math.min(100,(v/a3Max*100)))}%"></div></div>
            <span class="mono">${share.toFixed(1)}%</span>
          </div>
        </td>
      </tr>`;
  }
  document.getElementById("a3Table").innerHTML = a3Html;

  // D breakdown by system
  const dProc = PROCESSES_BY_STAGE["D"][0];
  const dBySys = {};
  for (const sys of SYSTEMS) dBySys[sys] = state.lca["D"][dProc][sys];
  const dMax = Math.max(...Object.values(dBySys).map(v=>Math.abs(v))) || 1;
  let dHtml = `<tr><th>System</th><th>tCO2e</th><th style="width:60%;">Magnitude</th></tr>`;
  for (const sys of SYSTEMS){
    dHtml += renderBarRow(sys, dBySys[sys], dMax, "");
  }
  document.getElementById("dTable").innerHTML = dHtml;
}

function renderExplainer(){
  const lvl = moduleLevels()[state.levelIndex];
  if (!lvl){
    document.getElementById("moduleExplainerCode").textContent = "—";
    document.getElementById("moduleExplainerText").textContent = "Run complete. Export your results or restart.";
    document.getElementById("moduleExplainerTip").textContent = "";
    return;
  }
  const ex = MODULE_EXPLAINERS[lvl.id] || {text:"", tip:""};
  document.getElementById("moduleExplainerCode").textContent = lvl.id;
  document.getElementById("moduleExplainerText").textContent = ex.text;
  document.getElementById("moduleExplainerTip").textContent = ex.tip ? ("Tip: " + ex.tip) : "";
}

function renderReportSummary(){
  const st = statusText();
  const topModules = (() => {
    const byStage = totalsByStage(state.lca, STAGES_ALL);
    const entries = Object.entries(byStage).sort((a,b)=>Math.abs(b[1]) - Math.abs(a[1]));
    return entries.slice(0,5).map(([k,v]) => `${k}: ${Math.round(v)} tCO2e`).join(", ");
  })();

  document.getElementById("reportSummary").innerHTML = `
    <div><b>Project:</b> New UF Art Museum (educational prototype)</div>
    <div><b>Date:</b> ${new Date().toISOString().slice(0,10)}</div>
    <div style="margin-top:8px;"><b>Results:</b></div>
    <div class="mono">Gross (A+B+C): ${Math.round(st.gross_tco2e)} tCO2e</div>
    <div class="mono">Module D:        ${Math.round(st.d_tco2e)} tCO2e</div>
    <div class="mono">Net:             ${Math.round(st.net_tco2e)} tCO2e</div>
    <div class="mono">Target (gross):  ≤ ${Math.round(st.target_gross_tco2e)} tCO2e</div>
    <div class="${st.ok ? "good" : "bad"}" style="margin-top:8px;"><b>Status:</b> ${st.ok ? "APPROVED" : "REVISE"}</div>
    <div style="margin-top:8px;"><b>Hot modules (by magnitude):</b> ${topModules}</div>
    <div style="margin-top:8px;"><b>Decisions made:</b></div>
    <div class="mono small">${state.runHistory.slice(1).map(r => `[${r.module}] ${r.decision}`).join("<br/>") || "(none yet)"}</div>
  `;
}

function render(){
  const lvls = moduleLevels();
  const lvl = lvls[state.levelIndex];

  document.getElementById("levelTitle").textContent = lvl ? lvl.title : "Finished (EN 15804 modules)";
  document.getElementById("levelBrief").textContent = lvl ? lvl.brief : "Run complete. Export your results or restart.";
  document.getElementById("levelScopeNote").textContent = lvl ? ("Scope note: " + lvl.scope) : "";
  const pillIdx = Math.min(state.levelIndex+1, lvls.length);
  document.getElementById("levelPill").textContent = `${pillIdx} / ${lvls.length}`;
  document.getElementById("progressLabel").textContent = `Module ${pillIdx} of ${lvls.length}`;
  document.getElementById("progressFill").style.width = `${Math.round((pillIdx / lvls.length) * 100)}%`;

  renderExplainer();

  const st = statusText();
  document.getElementById("kpiGross").textContent = fmt0(st.gross_tco2e);
  document.getElementById("kpiD").textContent = fmt0(st.d_tco2e);
  document.getElementById("kpiNet").textContent = fmt0(st.net_tco2e);
  document.getElementById("kpiTarget").textContent = fmt0(st.target_gross_tco2e);

  document.getElementById("kpiCost").textContent = `${fmt2(state.costM)} / ${state.maxCostM.toFixed(2)}`;
  document.getElementById("kpiSched").textContent = `${state.schedW} / ${state.maxSchedW}`;
  document.getElementById("kpiCred").textContent = `${state.cred} / 100`;

  document.getElementById("kpiStatus").innerHTML = st.ok ? `<span class="good">On track</span>` : `<span class="bad">Constraints failing</span>`;

  renderTables();
  renderReportSummary();

  const choicesEl = document.getElementById("choices");
  choicesEl.innerHTML = "";

  if (!lvl){
    choicesEl.innerHTML = `<div class="muted">Game complete. Export your results (right panel) or restart.</div>`;
    document.getElementById("nextBtn").disabled = true;
    return;
  }
  document.getElementById("nextBtn").disabled = !state.chosenThisLevel;

  lvl.choices.forEach((c) => {
    const before = snapshotKPIs();

    const saved = { lca: state.lca, costM: state.costM, schedW: state.schedW, cred: state.cred };
    const tmpLca = deepCopy3D(state.lca);
    state.lca = tmpLca; state.costM = saved.costM; state.schedW = saved.schedW; state.cred = saved.cred;
    c.act(); clampCred();
    const after = snapshotKPIs();
    state.lca = saved.lca; state.costM = saved.costM; state.schedW = saved.schedW; state.cred = saved.cred;

    const dGross = after.gross_tco2e - before.gross_tco2e;
    const dD    = after.d_tco2e - before.d_tco2e;
    const dCost = after.cost_musd - before.cost_musd;
    const dSched = after.schedule_weeks - before.schedule_weeks;
    const dCred = after.credibility - before.credibility;

    // Card color: green = saves carbon & no cred hit, red = hurts cred or adds carbon, yellow = trade-off
    let cardClass = "choice-card";
    if (dCred < -4 || dGross > 30) cardClass += " red";
    else if (dGross < -30 && dCred >= 0) cardClass += " green";
    else if (dGross < 0 || dCred > 0) cardClass += " yellow";

    // Carbon chip
    const absCO2 = Math.abs(Math.round(dGross));
    let carbonChip, carbonClass;
    if (dGross < -5)      { carbonChip = `🌍 Saves ~${absCO2} tCO₂e on gross`; carbonClass = "chip chip-carbon-good"; }
    else if (dGross > 5)  { carbonChip = `🌍 Adds ~${absCO2} tCO₂e to gross`; carbonClass = "chip chip-carbon-bad"; }
    else if (dD < -5)     { carbonChip = `🌍 Saves ~${Math.abs(Math.round(dD))} tCO₂e (Module D)`; carbonClass = "chip chip-carbon-good"; }
    else                  { carbonChip = `🌍 No carbon change`; carbonClass = "chip chip-carbon-neu"; }

    // Cost chip
    let costChip, costClass;
    if (dCost > 0.009)        { costChip = `💰 +$${dCost.toFixed(2)}M cost`; costClass = "chip chip-cost-bad"; }
    else if (dCost < -0.009)  { costChip = `💰 Saves $${Math.abs(dCost).toFixed(2)}M`; costClass = "chip chip-cost-good"; }
    else                      { costChip = `💰 No cost impact`; costClass = "chip chip-cost-neu"; }

    // Schedule chip
    let schedChip, schedClass;
    if (dSched > 0)       { schedChip = `⏱ +${dSched} week${dSched>1?"s":""} longer`; schedClass = "chip chip-sched-bad"; }
    else if (dSched < 0)  { schedChip = `⏱ ${Math.abs(dSched)} week${Math.abs(dSched)>1?"s":""} faster`; schedClass = "chip chip-sched-good"; }
    else                  { schedChip = `⏱ No schedule change`; schedClass = "chip chip-sched-neu"; }

    // Credibility chip
    let credChip, credClass;
    if (dCred > 0)       { credChip = `📋 Credibility +${dCred}`; credClass = "chip chip-cred-good"; }
    else if (dCred < 0)  { credChip = `📋 Credibility ${dCred} ⚠️`; credClass = "chip chip-cred-bad"; }
    else                 { credChip = `📋 Credibility unchanged`; credClass = "chip chip-cred-neu"; }

    // One-sentence consequence
    const consequence = c.consequence || (() => {
      const parts = [];
      if (dGross < -5) parts.push(`cuts gross carbon by ~${absCO2} tCO₂e`);
      if (dD < -5) parts.push(`reduces Module D by ~${Math.abs(Math.round(dD))} tCO₂e`);
      if (dGross > 5) parts.push(`raises gross carbon by ~${absCO2} tCO₂e`);
      if (dCost > 0.01) parts.push(`costs an extra $${dCost.toFixed(2)}M`);
      if (dCost < -0.01) parts.push(`saves $${Math.abs(dCost).toFixed(2)}M`);
      if (dSched > 0) parts.push(`adds ${dSched} week${dSched>1?"s":""} to schedule`);
      if (dSched < 0) parts.push(`saves ${Math.abs(dSched)} week${Math.abs(dSched)>1?"s":""} on schedule`);
      if (dCred < -4) parts.push(`hurts credibility (reviewers will question this)`);
      if (dCred > 1) parts.push(`strengthens credibility`);
      return parts.length ? parts.join(", ") + "." : "No measurable impact on KPIs.";
    })();

    const btn = document.createElement("button");
    btn.className = cardClass;
    btn.disabled = state.chosenThisLevel;
    btn.innerHTML = `
      <div class="choice-title">${c.title}</div>
      <div class="choice-desc">${c.desc}</div>
      <div class="impact-chips">
        <span class="${carbonClass}">${carbonChip}</span>
        <span class="${costClass}">${costChip}</span>
        <span class="${schedClass}">${schedChip}</span>
        <span class="${credClass}">${credChip}</span>
      </div>
      <div class="consequence-box">↳ ${consequence}</div>
      <div class="insight-box"><span class="insight-label">💡 Why it matters: </span>${c.learning}</div>
    `;
    btn.onclick = () => applyChoice(c);
    choicesEl.appendChild(btn);
  });
}

function applyChoice(choice){
  const before = snapshotKPIs();
  choice.act();
  clampCred();
  const after = snapshotKPIs();

  state.chosenThisLevel = true;
  state.runHistory.push({ ...after, decision: choice.title, module: moduleLevels()[state.levelIndex].id });

  logLine(`[${moduleLevels()[state.levelIndex].id}] ${choice.title} | ΔGross ${(after.gross_tco2e-before.gross_tco2e>=0?"+":"")}${Math.round(after.gross_tco2e-before.gross_tco2e)} | ` +
          `ΔD ${(after.d_tco2e-before.d_tco2e>=0?"+":"")}${Math.round(after.d_tco2e-before.d_tco2e)} | Net ${Math.round(after.net_tco2e)} | ` +
          `Cost ${after.cost_musd.toFixed(2)}M | Sched ${after.schedule_weeks}w | Cred ${after.credibility}`);

  render();
}

function nextLevel(){
  if (!state.chosenThisLevel) return;
  state.levelIndex += 1;
  state.chosenThisLevel = false;

  if (state.levelIndex >= moduleLevels().length){
    state.levelIndex = moduleLevels().length;
    const st = statusText();
    logLine("---- FINAL REVIEW ----");
    logLine(`Gross target: ${st.passCarbon ? "PASS" : "FAIL"} | Cost: ${st.passCost ? "PASS" : "FAIL"} | Schedule: ${st.passSched ? "PASS" : "FAIL"} | Credibility: ${st.passCred ? "PASS" : "FAIL"}`);
    logLine(st.ok ? "APPROVED: Gross (A+B+C) meets target and constraints; Module D reported separately." :
                    "REVISE: Missed constraints. Attack A1/A3 first; avoid unjustified B/C/D assumptions.");
    render();
    return;
  }
  render();
}

function restart(){
  state = initialState();
  seedBaseline();
  document.getElementById("log").textContent = "";
  state.runHistory = [{...snapshotKPIs(), decision:"(start)", module:"(start)"}];
  logLine("New run started.");
  render();
}
function autoTrialRun(){
  restart();
  const picks = moduleLevels().map(_ => 1);
  for (let i=0;i<picks.length;i++){
    const lvl = moduleLevels()[state.levelIndex];
    const choice = lvl.choices[picks[i]-1];
    applyChoice(choice);
    nextLevel();
  }
}

/* =========================
   Export CSV + Report
========================= */
function toCSV(rows){
  const cols = Object.keys(rows[0] || {});
  const esc = (v) => {
    const s = String(v ?? "");
    if (s.includes('"') || s.includes(",") || s.includes("\n")) return `"${s.replaceAll('"','""')}"`;
    return s;
  };
  const head = cols.map(esc).join(",");
  const body = rows.map(r => cols.map(c => esc(r[c])).join(",")).join("\n");
  return head + "\n" + body + "\n";
}
function download(name, text, mime="text/csv"){
  const blob = new Blob([text], {type:mime});
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url; a.download = name; a.click();
  URL.revokeObjectURL(url);
}
function exportRunCSV(){
  const rows = (state.runHistory || []).map((r, idx) => ({
    step: idx,
    module: r.module,
    decision: r.decision,
    gross_tco2e: Math.round(r.gross_tco2e ?? 0),
    d_tco2e: Math.round(r.d_tco2e ?? 0),
    net_tco2e: Math.round(r.net_tco2e ?? 0),
    target_gross_tco2e: Math.round(r.target_gross_tco2e ?? 0),
    cost_musd: Number(r.cost_musd ?? 0).toFixed(2),
    schedule_weeks: r.schedule_weeks ?? 0,
    credibility: r.credibility ?? 0
  }));
  download("uf_art_museum_en15804_run.csv", toCSV(rows));
}
function exportSnapshotCSV(){
  const rows = [];
  for (const s of STAGES_ALL){
    for (const p of PROCESSES_BY_STAGE[s]){
      for (const sys of SYSTEMS){
        rows.push({
          module: s,
          module_label: STAGE_LABEL[s],
          process: p,
          system: sys,
          tco2e: state.lca[s][p][sys].toFixed(2)
        });
      }
    }
  }
  download("uf_art_museum_en15804_snapshot_3d.csv", toCSV(rows));
}

function buildReportHTML(){
  const st = statusText();
  const byStage = totalsByStage(state.lca, STAGES_ALL);
  const stageEntries = Object.entries(byStage).sort((a,b)=>Math.abs(b[1])-Math.abs(a[1]));
  const bySys = totalsBySystem(state.lca, STAGES_ABC);
  const sysEntries = Object.entries(bySys).sort((a,b)=>b[1]-a[1]);
  const a3 = totalsByProcessWithinStage(state.lca, "A3");
  const a3Entries = Object.entries(a3).sort((a,b)=>b[1]-a[1]);

  const decisions = state.runHistory.slice(1).map(r => `<li><b>[${r.module}]</b> ${r.decision}</li>`).join("") || "<li>(none)</li>";

  const stageRows = stageEntries.map(([k,v]) => `<tr><td>${k}</td><td style="text-align:right">${Math.round(v)}</td></tr>`).join("");
  const sysRows = sysEntries.map(([k,v]) => `<tr><td>${k}</td><td style="text-align:right">${Math.round(v)}</td></tr>`).join("");
  const a3Rows = a3Entries.map(([k,v]) => `<tr><td>${k}</td><td style="text-align:right">${Math.round(v)}</td></tr>`).join("");

  return `<!doctype html>
<html><head><meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>UF Art Museum LCA Manager — Submission Report</title>
<style>
  body{font-family:system-ui, Arial, sans-serif; margin:24px; color:#111;}
  h1{margin:0 0 6px;}
  .muted{color:#444;}
  .box{border:1px solid #ccc; border-radius:10px; padding:12px; margin-top:12px;}
  table{border-collapse:collapse; width:100%; margin-top:8px;}
  th,td{border-bottom:1px solid #eee; padding:6px;}
  .ok{color:#0a7a3c; font-weight:700;}
  .bad{color:#b00020; font-weight:700;}
  code{font-family:ui-monospace, Menlo, Consolas, monospace;}
</style>
</head>
<body>
  <h1>UF Art Museum — EN 15804 LCA Manager (Submission Report)</h1>
  <div class="muted">Generated: ${new Date().toISOString().slice(0,19).replace("T"," ")} (local prototype)</div>

  <div class="box">
    <h2>Results</h2>
    <div><b>Status:</b> <span class="${st.ok ? "ok" : "bad"}">${st.ok ? "APPROVED" : "REVISE"}</span></div>
    <ul>
      <li><b>Gross (A+B+C):</b> ${Math.round(st.gross_tco2e)} tCO2e (target ≤ ${Math.round(st.target_gross_tco2e)})</li>
      <li><b>Module D:</b> ${Math.round(st.d_tco2e)} tCO2e (reported separately)</li>
      <li><b>Net (Gross + D):</b> ${Math.round(st.net_tco2e)} tCO2e</li>
      <li><b>Additional cost:</b> $${st.cost_musd.toFixed(2)}M (cap $${state.maxCostM.toFixed(2)}M)</li>
      <li><b>Schedule impact:</b> ${st.schedule_weeks} weeks (cap ${state.maxSchedW})</li>
      <li><b>Credibility:</b> ${st.credibility}/100 (min ${state.minCred})</li>
    </ul>
  </div>

  <div class="box">
    <h2>Decisions</h2>
    <ol>${decisions}</ol>
  </div>

  <div class="box">
    <h2>Hotspots</h2>
    <h3>By module</h3>
    <table><thead><tr><th>Module</th><th style="text-align:right">tCO2e</th></tr></thead><tbody>${stageRows}</tbody></table>
    <h3 style="margin-top:14px;">By system (gross only)</h3>
    <table><thead><tr><th>System</th><th style="text-align:right">tCO2e</th></tr></thead><tbody>${sysRows}</tbody></table>
    <h3 style="margin-top:14px;">A3 fabrication sub-processes</h3>
    <table><thead><tr><th>Process</th><th style="text-align:right">tCO2e</th></tr></thead><tbody>${a3Rows}</tbody></table>
  </div>

  <div class="box">
    <h2>Notes</h2>
    <p class="muted">
      This is an educational prototype. Numbers are illustrative and meant to show how decisions map to EN 15804 modules
      and how hotspots can be targeted (A1 raw material supply, A3 fabrication, B4 replacement, etc.).
    </p>
  </div>
</body></html>`;
}

function downloadReport(){
  const html = buildReportHTML();
  download("uf_art_museum_submission_report.html", html, "text/html");
}

/* =========================
   Tabs
========================= */
function setTab(which){
  const logBtn = document.getElementById("tabLogBtn");
  const repBtn = document.getElementById("tabReportBtn");
  const log = document.getElementById("tabLog");
  const rep = document.getElementById("tabReport");
  if (which === "log"){
    logBtn.classList.add("active"); repBtn.classList.remove("active");
    log.classList.remove("hidden"); rep.classList.add("hidden");
  } else {
    repBtn.classList.add("active"); logBtn.classList.remove("active");
    rep.classList.remove("hidden"); log.classList.add("hidden");
  }
}

/* =========================
   Wire up
========================= */
document.getElementById("restartBtn").onclick = restart;
document.getElementById("trialBtn").onclick = autoTrialRun;
document.getElementById("nextBtn").onclick = nextLevel;
document.getElementById("exportRunBtn").onclick = exportRunCSV;
document.getElementById("exportSnapshotBtn").onclick = exportSnapshotCSV;
document.getElementById("downloadReportBtn").onclick = downloadReport;

document.getElementById("tabLogBtn").onclick = () => setTab("log");
document.getElementById("tabReportBtn").onclick = () => setTab("report");

/* Start */
restart();
</script>
</body>
</html>
