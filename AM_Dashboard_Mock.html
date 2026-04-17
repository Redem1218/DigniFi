import { useState, useMemo } from "react";
import {
  LineChart, Line, BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip,
  ResponsiveContainer, Cell, PieChart, Pie, Legend, ReferenceLine
} from "recharts";

// ─── Salesforce Lightning tokens ────────────────────────────────────────
const SF = {
  blue:   "#0176d3",
  navy:   "#032d60",
  teal:   "#06a59a",
  green:  "#2e844a",
  greenBg:"#cdefc4",
  red:    "#ba0517",
  redBg:  "#ffdde1",
  orange: "#fe9339",
  orangeBg:"#fff3e0",
  gray:   "#f3f3f3",
  border: "#dddbda",
  text:   "#181818",
  muted:  "#3e3e3c",
  light:  "#706e6b",
};

// ─── KPI Thresholds (from AM Playbook) ──────────────────────────────────
const THRESHOLDS = {
  touchCoverage:  { green: 100, yellow: 80 },      // % contacted
  dormancy:       { green: 20,  yellow: 35, inverse: true }, // % at $0 (lower is better)
  highlyEngaged:  { green: 40,  yellow: 20 },      // % at $10K+
  captureRate:    { green: 60,  yellow: 40 },      // actual/max GMV
  gmvAtRisk:      { green: 25000, yellow: 75000, inverse: true },
  gmvGrowth:      { green: 10,  yellow: 0 },       // MoM %
  neverActive60:  { green: 0,   yellow: 2,  inverse: true },
  crmLogging:     { green: 100, yellow: 80 },
  daysToTraining: { green: 7,   yellow: 10, inverse: true },
  retraining:     { green: 14,  yellow: 21, inverse: true },
  cadenceComp:    { green: 95,  yellow: 80 },
};

const statusOf = (val, t) => {
  if (t.inverse) {
    if (val <= t.green) return "green";
    if (val <= t.yellow) return "yellow";
    return "red";
  }
  if (val >= t.green) return "green";
  if (val >= t.yellow) return "yellow";
  return "red";
};

const statusColor = (s) =>
  s === "green" ? SF.green : s === "yellow" ? SF.orange : SF.red;
const statusBg = (s) =>
  s === "green" ? SF.greenBg : s === "yellow" ? SF.orangeBg : SF.redBg;
const statusLabel = (s) =>
  s === "green" ? "On Track" : s === "yellow" ? "Watch" : "At Risk";

// ─── Account Manager Data ───────────────────────────────────────────────
const AMs = [
  {
    id: "jerome",
    name: "Jerome Carthen",
    initials: "JC",
    title: "AM Team Lead",
    role: "Lead",
    accounts: 48,
    tierHE: 20, tierME: 18, tierLE: 7, tierD: 3,
    touchCoverage: 97,
    dormancy: 6,
    captureRate: 64,
    gmvAtRisk: 18000,
    gmvGrowth: 14,
    neverActive60: 0,
    crmLogging: 100,
    daysToTraining: 5,
    retraining: 9,
    cadenceComp: 98,
    gmvMTD: 322500,
    ytdGrowth: 42,
  },
  {
    id: "megan",
    name: "Megan Buell",
    initials: "MB",
    title: "Account Manager",
    role: "AM",
    accounts: 52,
    tierHE: 24, tierME: 16, tierLE: 7, tierD: 5,
    touchCoverage: 92,
    dormancy: 10,
    captureRate: 58,
    gmvAtRisk: 34000,
    gmvGrowth: 9,
    neverActive60: 1,
    crmLogging: 96,
    daysToTraining: 6,
    retraining: 12,
    cadenceComp: 94,
    gmvMTD: 287000,
    ytdGrowth: 31,
  },
  {
    id: "kelsey",
    name: "Kelsey Rookard",
    initials: "KR",
    title: "Account Manager",
    role: "AM",
    accounts: 45,
    tierHE: 14, tierME: 17, tierLE: 9, tierD: 5,
    touchCoverage: 84,
    dormancy: 19,
    captureRate: 47,
    gmvAtRisk: 58000,
    gmvGrowth: 6,
    neverActive60: 2,
    crmLogging: 89,
    daysToTraining: 8,
    retraining: 17,
    cadenceComp: 86,
    gmvMTD: 182500,
    ytdGrowth: 18,
  },
  {
    id: "roman",
    name: "Roman Mitchell",
    initials: "RM",
    title: "Account Manager",
    role: "AM",
    accounts: 42,
    tierHE: 9, tierME: 15, tierLE: 11, tierD: 7,
    touchCoverage: 76,
    dormancy: 21,
    captureRate: 38,
    gmvAtRisk: 82000,
    gmvGrowth: 2,
    neverActive60: 3,
    crmLogging: 78,
    daysToTraining: 9,
    retraining: 22,
    cadenceComp: 74,
    gmvMTD: 127500,
    ytdGrowth: 8,
  },
  {
    id: "carlos",
    name: "Carlos Miller",
    initials: "CM",
    title: "Account Manager",
    role: "AM",
    accounts: 38,
    tierHE: 6, tierME: 12, tierLE: 10, tierD: 10,
    touchCoverage: 68,
    dormancy: 28,
    captureRate: 31,
    gmvAtRisk: 104000,
    gmvGrowth: -3,
    neverActive60: 4,
    crmLogging: 71,
    daysToTraining: 11,
    retraining: 26,
    cadenceComp: 68,
    gmvMTD: 89500,
    ytdGrowth: -4,
  },
];

// Performance score composite (percent of KPIs in green zone)
const scoreAM = (am) => {
  const keys = ["touchCoverage","dormancy","captureRate","gmvAtRisk",
                "gmvGrowth","neverActive60","crmLogging","daysToTraining",
                "retraining","cadenceComp"];
  const kpiMap = {
    touchCoverage: THRESHOLDS.touchCoverage,
    dormancy: THRESHOLDS.dormancy,
    captureRate: THRESHOLDS.captureRate,
    gmvAtRisk: THRESHOLDS.gmvAtRisk,
    gmvGrowth: THRESHOLDS.gmvGrowth,
    neverActive60: THRESHOLDS.neverActive60,
    crmLogging: THRESHOLDS.crmLogging,
    daysToTraining: THRESHOLDS.daysToTraining,
    retraining: THRESHOLDS.retraining,
    cadenceComp: THRESHOLDS.cadenceComp,
  };
  let g=0, y=0, r=0;
  keys.forEach(k => {
    const s = statusOf(am[k], kpiMap[k]);
    if (s==="green") g++; else if (s==="yellow") y++; else r++;
  });
  const score = Math.round(((g*1 + y*0.5) / keys.length) * 100);
  const status = r >= 2 ? "red" : y >= 3 ? "yellow" : g >= 7 ? "green" : "yellow";
  return { score, status, g, y, r };
};

// ─── Partner Data ───────────────────────────────────────────────────────
const PARTNERS = [
  { name: "Mazda",              stores: 32, dormRate: 7,  gmv: 64300,  trend: "down" },
  { name: "CDK Global",         stores: 61, dormRate: 14, gmv: 148900, trend: "flat" },
  { name: "MyKaarma",           stores: 28, dormRate: 11, gmv: 71200,  trend: "down" },
  { name: "Xtime",              stores: 44, dormRate: 23, gmv: 102400, trend: "up"   },
  { name: "EVE",                stores: 19, dormRate: 26, gmv: 41800,  trend: "up"   },
  { name: "Endurance Warranty", stores: 41, dormRate: 22, gmv: 89700,  trend: "up"   },
];

// ─── Team GMV Trend ─────────────────────────────────────────────────────
const TREND = [
  { month: "Sep", gmv: 742, dormancy: 24 },
  { month: "Oct", gmv: 821, dormancy: 22 },
  { month: "Nov", gmv: 887, dormancy: 20 },
  { month: "Dec", gmv: 934, dormancy: 19 },
  { month: "Jan", gmv: 981, dormancy: 18 },
  { month: "Feb", gmv: 1008, dormancy: 17 },
];

// ─── Sample merchant data (per AM) ──────────────────────────────────────
const MERCHANTS_BY_AM = {
  jerome: [
    { name: "Lindsay Mazda Alexandria",   partner: "Mazda",    tier: "HE", gmv: 14200, lastTouch: 2, status: "green"  },
    { name: "Koons CDK Sterling",          partner: "CDK",      tier: "HE", gmv: 22800, lastTouch: 4, status: "green"  },
    { name: "Priority MyKaarma Chesapeake",partner: "MyKaarma",tier: "HE", gmv: 11600, lastTouch: 1, status: "green"  },
    { name: "Rosenthal Xtime Tysons",      partner: "Xtime",    tier: "ME", gmv: 4800,  lastTouch: 6, status: "green"  },
    { name: "Passport EVE Alexandria",     partner: "EVE",      tier: "LE", gmv: 1800,  lastTouch: 14,status: "yellow" },
    { name: "Lindsay Endurance Manassas",  partner: "Endurance",tier: "D",  gmv: 0,     lastTouch: 9, status: "red"    },
    { name: "Fitzgerald Mazda Frederick",  partner: "Mazda",    tier: "D",  gmv: 0,     lastTouch: 7, status: "red"    },
  ],
  megan: [
    { name: "Ourisman CDK Bethesda",       partner: "CDK",      tier: "HE", gmv: 31400, lastTouch: 3, status: "green"  },
    { name: "Sheehy MyKaarma Springfield", partner: "MyKaarma",tier: "HE", gmv: 18200, lastTouch: 5, status: "green"  },
    { name: "Browns Mazda Fairfax",        partner: "Mazda",    tier: "HE", gmv: 12700, lastTouch: 8, status: "yellow" },
    { name: "Easterns Xtime Laurel",       partner: "Xtime",    tier: "ME", gmv: 6200,  lastTouch: 11,status: "yellow" },
    { name: "Darcars EVE Silver Spring",   partner: "EVE",      tier: "LE", gmv: 920,   lastTouch: 16,status: "red"    },
    { name: "Jim Coleman Endurance",       partner: "Endurance",tier: "D",  gmv: 0,     lastTouch: 12,status: "red"    },
  ],
  kelsey: [
    { name: "Thompson CDK Richmond",       partner: "CDK",      tier: "HE", gmv: 19800, lastTouch: 4, status: "green"  },
    { name: "Haley Mazda Midlothian",      partner: "Mazda",    tier: "ME", gmv: 7400,  lastTouch: 9, status: "yellow" },
    { name: "Pohanka MyKaarma Chantilly",  partner: "MyKaarma",tier: "ME", gmv: 5100,  lastTouch: 13,status: "yellow" },
    { name: "Brown Xtime Glen Allen",      partner: "Xtime",    tier: "LE", gmv: 1400,  lastTouch: 18,status: "red"    },
    { name: "Hall EVE Chesterfield",       partner: "EVE",      tier: "D",  gmv: 0,     lastTouch: 21,status: "red"    },
    { name: "West Broad Endurance",        partner: "Endurance",tier: "D",  gmv: 0,     lastTouch: 15,status: "red"    },
  ],
  roman: [
    { name: "Criswell CDK Germantown",     partner: "CDK",      tier: "HE", gmv: 16200, lastTouch: 7, status: "yellow" },
    { name: "Lustine Xtime Woodbridge",    partner: "Xtime",    tier: "ME", gmv: 4900,  lastTouch: 14,status: "yellow" },
    { name: "Stafford Mazda Fredericksburg",partner:"Mazda",    tier: "ME", gmv: 3800,  lastTouch: 16,status: "red"    },
    { name: "Battlefield MyKaarma",        partner: "MyKaarma",tier: "LE", gmv: 1200,  lastTouch: 22,status: "red"    },
    { name: "Safford EVE Dulles",          partner: "EVE",      tier: "D",  gmv: 0,     lastTouch: 19,status: "red"    },
    { name: "Ted Britt Endurance Fairfax", partner: "Endurance",tier: "D",  gmv: 0,     lastTouch: 24,status: "red"    },
    { name: "Jack Taylor Xtime Leesburg",  partner: "Xtime",    tier: "D",  gmv: 0,     lastTouch: 28,status: "red"    },
  ],
  carlos: [
    { name: "Sheehy CDK Marlow Heights",   partner: "CDK",      tier: "ME", gmv: 6800,  lastTouch: 11,status: "yellow" },
    { name: "Heritage Xtime Owings Mills", partner: "Xtime",    tier: "ME", gmv: 3100,  lastTouch: 18,status: "red"    },
    { name: "Ourisman Mazda Laurel",       partner: "Mazda",    tier: "LE", gmv: 1600,  lastTouch: 23,status: "red"    },
    { name: "Antwerpen MyKaarma",          partner: "MyKaarma",tier: "LE", gmv: 900,   lastTouch: 26,status: "red"    },
    { name: "Tate EVE Glen Burnie",        partner: "EVE",      tier: "D",  gmv: 0,     lastTouch: 31,status: "red"    },
    { name: "Len Stoler Endurance",        partner: "Endurance",tier: "D",  gmv: 0,     lastTouch: 34,status: "red"    },
    { name: "Koons Xtime Annapolis",       partner: "Xtime",    tier: "D",  gmv: 0,     lastTouch: 29,status: "red"    },
    { name: "Brown Mazda Amityville",      partner: "Mazda",    tier: "D",  gmv: 0,     lastTouch: 38,status: "red"    },
  ],
};

// ─── Formatters ─────────────────────────────────────────────────────────
const fmt$ = (n) =>
  n >= 1000000 ? `$${(n/1000000).toFixed(2)}M`
  : n >= 1000 ? `$${(n/1000).toFixed(1)}K`
  : `$${n.toLocaleString()}`;
const fmt$full = (n) => `$${n.toLocaleString()}`;
const pct = (n) => `${n}%`;

// ─── Reusable UI primitives ─────────────────────────────────────────────
const Card = ({ title, action, children, style, padded = true }) => (
  <div style={{
    background: "white",
    border: `1px solid ${SF.border}`,
    borderRadius: 6,
    boxShadow: "0 1px 2px rgba(0,0,0,0.04)",
    ...style
  }}>
    {title && (
      <div style={{
        padding: "12px 16px",
        borderBottom: `1px solid ${SF.border}`,
        display: "flex",
        justifyContent: "space-between",
        alignItems: "center",
        background: "#fafaf9",
        borderRadius: "6px 6px 0 0",
      }}>
        <div style={{ fontSize: 13, fontWeight: 700, color: SF.navy, letterSpacing: 0.2, textTransform: "uppercase" }}>
          {title}
        </div>
        {action}
      </div>
    )}
    <div style={{ padding: padded ? 16 : 0 }}>{children}</div>
  </div>
);

const StatusDot = ({ status, size = 8 }) => (
  <span style={{
    display: "inline-block",
    width: size, height: size,
    borderRadius: "50%",
    background: statusColor(status),
    marginRight: 6,
    boxShadow: `0 0 0 2px ${statusBg(status)}`,
  }} />
);

const Pill = ({ status, children }) => (
  <span style={{
    display: "inline-flex",
    alignItems: "center",
    fontSize: 11,
    fontWeight: 600,
    padding: "3px 10px",
    borderRadius: 12,
    background: statusBg(status),
    color: statusColor(status),
    border: `1px solid ${statusColor(status)}40`,
  }}>
    <StatusDot status={status} size={6} />
    {children}
  </span>
);

const Avatar = ({ initials, status, size = 36 }) => (
  <div style={{
    width: size, height: size,
    borderRadius: "50%",
    background: `linear-gradient(135deg, ${SF.blue} 0%, ${SF.navy} 100%)`,
    color: "white",
    fontWeight: 700,
    fontSize: size * 0.38,
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    position: "relative",
    flexShrink: 0,
  }}>
    {initials}
    {status && (
      <div style={{
        position: "absolute",
        bottom: -1, right: -1,
        width: size * 0.32, height: size * 0.32,
        borderRadius: "50%",
        background: statusColor(status),
        border: "2px solid white",
      }} />
    )}
  </div>
);

const ProgressBar = ({ value, max = 100, status, target, showLabel = true, height = 8 }) => {
  const pctFilled = Math.min(100, (value / max) * 100);
  const targetPct = target ? (target / max) * 100 : null;
  return (
    <div style={{ position: "relative" }}>
      <div style={{
        width: "100%", height, background: "#ececec",
        borderRadius: height / 2, overflow: "hidden", position: "relative",
      }}>
        <div style={{
          width: `${pctFilled}%`, height: "100%",
          background: statusColor(status),
          transition: "width 0.4s",
        }} />
        {targetPct !== null && (
          <div style={{
            position: "absolute",
            left: `${targetPct}%`,
            top: -2, bottom: -2,
            width: 2, background: SF.navy,
          }} />
        )}
      </div>
      {showLabel && (
        <div style={{
          fontSize: 11, marginTop: 3, color: SF.muted,
          display: "flex", justifyContent: "space-between",
        }}>
          <span>{value}{max === 100 ? "%" : ""}</span>
          {target && <span style={{ fontWeight: 600 }}>Target: {target}{max === 100 ? "%" : ""}</span>}
        </div>
      )}
    </div>
  );
};

const Trend = ({ dir }) => {
  const isUp = dir === "up", isDown = dir === "down";
  const arrow = isUp ? "▲" : isDown ? "▼" : "—";
  const color = isUp ? SF.red : isDown ? SF.green : SF.light; // up = worse dormancy
  return <span style={{ color, fontSize: 11, fontWeight: 700 }}>{arrow}</span>;
};

// ─── KPI Card (scorecard tile) ──────────────────────────────────────────
const KpiTile = ({ label, value, subtitle, status, target, format }) => (
  <div style={{
    background: "white",
    border: `1px solid ${SF.border}`,
    borderLeft: `3px solid ${statusColor(status)}`,
    borderRadius: 4,
    padding: "12px 14px",
  }}>
    <div style={{ fontSize: 10, fontWeight: 700, color: SF.muted, textTransform: "uppercase", letterSpacing: 0.4, marginBottom: 6 }}>
      {label}
    </div>
    <div style={{ fontSize: 24, fontWeight: 700, color: SF.navy, lineHeight: 1 }}>
      {value}
    </div>
    {subtitle && (
      <div style={{ fontSize: 11, color: SF.muted, marginTop: 4 }}>{subtitle}</div>
    )}
    {target && (
      <div style={{ fontSize: 10, color: SF.light, marginTop: 4 }}>
        Target: {target}
      </div>
    )}
  </div>
);

// ─── Tier distribution bar ──────────────────────────────────────────────
const TierBar = ({ he, me, le, d }) => {
  const total = he + me + le + d;
  const seg = (count, color, label) => (
    count > 0 ? (
      <div style={{
        width: `${(count/total)*100}%`,
        background: color,
        color: "white",
        fontSize: 10, fontWeight: 700,
        textAlign: "center",
        padding: "4px 0",
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
      }} title={`${label}: ${count}`}>
        {(count/total)*100 >= 8 ? count : ""}
      </div>
    ) : null
  );
  return (
    <div style={{
      display: "flex", width: "100%",
      height: 22, borderRadius: 4, overflow: "hidden",
      border: `1px solid ${SF.border}`,
    }}>
      {seg(he, SF.green,  "Highly Engaged")}
      {seg(me, SF.teal,   "Mid Engaged")}
      {seg(le, SF.orange, "Low Engaged")}
      {seg(d,  SF.red,    "Dormant")}
    </div>
  );
};

// ═══════════════════════════════════════════════════════════════════════
// EXECUTIVE VIEW
// ═══════════════════════════════════════════════════════════════════════
function ExecutiveView({ onDrill }) {
  const totals = useMemo(() => {
    const accounts = AMs.reduce((s, a) => s + a.accounts, 0);
    const gmv = AMs.reduce((s, a) => s + a.gmvMTD, 0);
    const dormant = AMs.reduce((s, a) => s + a.tierD, 0);
    const he = AMs.reduce((s, a) => s + a.tierHE, 0);
    const avgTouch = Math.round(
      AMs.reduce((s, a) => s + a.touchCoverage * a.accounts, 0) / accounts
    );
    const dormancy = Math.round((dormant / accounts) * 100);
    const heRate = Math.round((he / accounts) * 100);
    const atRisk = AMs.reduce((s, a) => s + a.gmvAtRisk, 0);
    return { accounts, gmv, dormant, dormancy, he, heRate, avgTouch, atRisk };
  }, []);

  const ranked = [...AMs].map(am => ({ ...am, ...scoreAM(am) }))
    .sort((a, b) => b.score - a.score);

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>

      {/* ── Top KPI Summary ── */}
      <div style={{ display: "grid", gridTemplateColumns: "repeat(6, 1fr)", gap: 12 }}>
        <KpiTile
          label="Team GMV · MTD"
          value={fmt$(totals.gmv)}
          subtitle="5 AMs · Feb run-rate"
          status="green"
        />
        <KpiTile
          label="Active Dealer Book"
          value={totals.accounts}
          subtitle={`${totals.he} Highly Engaged ($10K+)`}
          status="green"
        />
        <KpiTile
          label="Team Dormancy Rate"
          value={pct(totals.dormancy)}
          subtitle={`${totals.dormant} stores at $0`}
          status={statusOf(totals.dormancy, THRESHOLDS.dormancy)}
          target="< 20%"
        />
        <KpiTile
          label="Touch Coverage (avg)"
          value={pct(totals.avgTouch)}
          subtitle="Accounts contacted MTD"
          status={statusOf(totals.avgTouch, THRESHOLDS.touchCoverage)}
          target="100%"
        />
        <KpiTile
          label="Highly Engaged Rate"
          value={pct(totals.heRate)}
          subtitle="% of book at $10K+"
          status={statusOf(totals.heRate, THRESHOLDS.highlyEngaged)}
          target="≥ 40%"
        />
        <KpiTile
          label="Team GMV at Risk"
          value={fmt$(totals.atRisk)}
          subtitle="Dormant + never-active"
          status="red"
          target="< $25K/AM"
        />
      </div>

      {/* ── AM Leaderboard ── */}
      <Card
        title="Account Manager Performance Leaderboard"
        action={
          <div style={{ display: "flex", gap: 8, fontSize: 11, color: SF.muted }}>
            <span><StatusDot status="green" /> On Track</span>
            <span><StatusDot status="yellow" /> Watch</span>
            <span><StatusDot status="red" /> At Risk</span>
          </div>
        }
        padded={false}
      >
        <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 13 }}>
          <thead>
            <tr style={{ background: "#fafaf9", borderBottom: `2px solid ${SF.border}` }}>
              <th style={th}>Rank</th>
              <th style={thL}>Account Manager</th>
              <th style={th}>Score</th>
              <th style={thL}>Portfolio Composition</th>
              <th style={th}>Touch</th>
              <th style={th}>Dormancy</th>
              <th style={th}>Capture</th>
              <th style={th}>GMV MTD</th>
              <th style={th}>At Risk</th>
              <th style={th}>Status</th>
              <th style={th}></th>
            </tr>
          </thead>
          <tbody>
            {ranked.map((am, i) => {
              const touchS   = statusOf(am.touchCoverage, THRESHOLDS.touchCoverage);
              const dormS    = statusOf(am.dormancy, THRESHOLDS.dormancy);
              const captureS = statusOf(am.captureRate, THRESHOLDS.captureRate);
              const riskS    = statusOf(am.gmvAtRisk, THRESHOLDS.gmvAtRisk);
              return (
                <tr key={am.id}
                    style={{ borderBottom: `1px solid ${SF.border}`, cursor: "pointer" }}
                    onClick={() => onDrill(am.id)}
                    onMouseEnter={(e) => e.currentTarget.style.background = "#f7fafd"}
                    onMouseLeave={(e) => e.currentTarget.style.background = "white"}
                >
                  <td style={td}>
                    <div style={{
                      width: 24, height: 24, borderRadius: "50%",
                      background: i === 0 ? "#ffd700" : i === ranked.length - 1 ? SF.redBg : SF.gray,
                      color: i === ranked.length - 1 ? SF.red : SF.navy,
                      display: "flex", alignItems: "center", justifyContent: "center",
                      fontSize: 11, fontWeight: 700, margin: "0 auto",
                    }}>
                      {i + 1}
                    </div>
                  </td>
                  <td style={tdL}>
                    <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                      <Avatar initials={am.initials} status={am.status} size={34} />
                      <div>
                        <div style={{ fontWeight: 600, color: SF.navy }}>{am.name}</div>
                        <div style={{ fontSize: 11, color: SF.muted }}>{am.title} · {am.accounts} accts</div>
                      </div>
                    </div>
                  </td>
                  <td style={td}>
                    <div style={{
                      fontSize: 20, fontWeight: 700,
                      color: statusColor(am.status),
                    }}>
                      {am.score}
                    </div>
                    <div style={{ fontSize: 10, color: SF.muted }}>
                      {am.g}G · {am.y}Y · {am.r}R
                    </div>
                  </td>
                  <td style={{ ...tdL, minWidth: 160 }}>
                    <TierBar he={am.tierHE} me={am.tierME} le={am.tierLE} d={am.tierD} />
                    <div style={{ fontSize: 10, color: SF.muted, marginTop: 3 }}>
                      HE {am.tierHE} · ME {am.tierME} · LE {am.tierLE} · D {am.tierD}
                    </div>
                  </td>
                  <td style={td}>
                    <div style={{ fontWeight: 700, color: statusColor(touchS) }}>{am.touchCoverage}%</div>
                  </td>
                  <td style={td}>
                    <div style={{ fontWeight: 700, color: statusColor(dormS) }}>{am.dormancy}%</div>
                  </td>
                  <td style={td}>
                    <div style={{ fontWeight: 700, color: statusColor(captureS) }}>{am.captureRate}%</div>
                  </td>
                  <td style={td}>
                    <div style={{ fontWeight: 700, color: SF.navy }}>{fmt$(am.gmvMTD)}</div>
                    <div style={{ fontSize: 10, color: am.gmvGrowth >= 0 ? SF.green : SF.red }}>
                      {am.gmvGrowth >= 0 ? "▲" : "▼"} {Math.abs(am.gmvGrowth)}% MoM
                    </div>
                  </td>
                  <td style={td}>
                    <div style={{ fontWeight: 700, color: statusColor(riskS) }}>
                      {fmt$(am.gmvAtRisk)}
                    </div>
                  </td>
                  <td style={td}><Pill status={am.status}>{statusLabel(am.status)}</Pill></td>
                  <td style={td}>
                    <button style={btnLink} onClick={(e) => { e.stopPropagation(); onDrill(am.id); }}>
                      Drill →
                    </button>
                  </td>
                </tr>
              );
            })}
          </tbody>
        </table>
      </Card>

      {/* ── Row: Trend + Partner Rollup ── */}
      <div style={{ display: "grid", gridTemplateColumns: "1.6fr 1fr", gap: 16 }}>
        <Card title="Team GMV & Dormancy · 6-Month Trend">
          <ResponsiveContainer width="100%" height={240}>
            <LineChart data={TREND} margin={{ top: 8, right: 20, left: 0, bottom: 0 }}>
              <CartesianGrid strokeDasharray="3 3" stroke="#ececec" />
              <XAxis dataKey="month" stroke={SF.muted} style={{ fontSize: 11 }} />
              <YAxis yAxisId="left"  stroke={SF.blue}  style={{ fontSize: 11 }}
                     label={{ value: "GMV ($K)", angle: -90, position: "insideLeft", fill: SF.blue, fontSize: 11 }} />
              <YAxis yAxisId="right" orientation="right" stroke={SF.red} style={{ fontSize: 11 }}
                     label={{ value: "Dormancy %", angle: 90, position: "insideRight", fill: SF.red, fontSize: 11 }} />
              <Tooltip />
              <Line yAxisId="left"  dataKey="gmv"      stroke={SF.blue} strokeWidth={3} dot={{ r: 4 }} name="GMV ($K)" />
              <Line yAxisId="right" dataKey="dormancy" stroke={SF.red}  strokeWidth={2}
                    strokeDasharray="5 5" dot={{ r: 3 }} name="Dormancy %" />
            </LineChart>
          </ResponsiveContainer>
          <div style={{ fontSize: 11, color: SF.muted, borderTop: `1px solid ${SF.border}`, paddingTop: 10, marginTop: 8 }}>
            <strong style={{ color: SF.green }}>↑ $266K GMV (+36%)</strong> and <strong style={{ color: SF.green }}>↓ 7pts dormancy</strong> since Sep. Trajectory is healthy at the team level — but distribution is the story (see leaderboard).
          </div>
        </Card>

        <Card title="Partner Rollup · Dormancy vs 20% Target">
          <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
            {PARTNERS.sort((a,b) => b.dormRate - a.dormRate).map(p => {
              const s = p.dormRate < 20 ? "green" : p.dormRate < 35 ? "yellow" : "red";
              return (
                <div key={p.name}>
                  <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12, marginBottom: 3 }}>
                    <span style={{ fontWeight: 600, color: SF.navy }}>
                      {p.name} <span style={{ fontWeight: 400, color: SF.muted }}>· {p.stores} stores</span>
                    </span>
                    <span style={{ fontWeight: 700, color: statusColor(s) }}>
                      {p.dormRate}% <Trend dir={p.trend} />
                    </span>
                  </div>
                  <div style={{ position: "relative", height: 8, background: "#ececec", borderRadius: 4, overflow: "hidden" }}>
                    <div style={{
                      width: `${Math.min(100, (p.dormRate / 40) * 100)}%`,
                      height: "100%", background: statusColor(s),
                    }} />
                    <div style={{
                      position: "absolute", left: "50%", top: -2, bottom: -2,
                      width: 2, background: SF.navy,
                    }} title="20% Target" />
                  </div>
                  <div style={{ fontSize: 10, color: SF.muted, marginTop: 2 }}>
                    {fmt$(p.gmv)} GMV MTD
                  </div>
                </div>
              );
            })}
          </div>
        </Card>
      </div>

      {/* ── Executive Insights ── */}
      <Card title="Executive Coaching Signals">
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr", gap: 12 }}>
          <InsightBox color={SF.green} title="Proof Point" copy="Jerome (97% touch → 6% dormancy) and Megan (92% → 10%) demonstrate the cadence model works. Promote their playbook across the team." />
          <InsightBox color={SF.orange} title="Watch" copy="Kelsey is borderline across 4 KPIs. A 14-day retraining sprint + AM Playbook cadence reset should pull her to green by EOM." />
          <InsightBox color={SF.red} title="At Risk" copy="Carlos is red on 4 KPIs. $104K GMV at risk. Trigger an immediate PIP + portfolio reallocation of the 8 dormant stores to Jerome/Megan." />
        </div>
      </Card>
    </div>
  );
}

const InsightBox = ({ color, title, copy }) => (
  <div style={{
    padding: 14, borderRadius: 6,
    background: `${color}0D`,
    borderLeft: `4px solid ${color}`,
  }}>
    <div style={{ fontSize: 11, fontWeight: 700, color, textTransform: "uppercase", letterSpacing: 0.4, marginBottom: 6 }}>
      {title}
    </div>
    <div style={{ fontSize: 13, color: SF.text, lineHeight: 1.45 }}>{copy}</div>
  </div>
);

// ═══════════════════════════════════════════════════════════════════════
// INDIVIDUAL AM VIEW
// ═══════════════════════════════════════════════════════════════════════
function AMDetailView({ amId, onBack, isExec }) {
  const am = AMs.find(a => a.id === amId);
  if (!am) return null;
  const merchants = MERCHANTS_BY_AM[am.id] || [];
  const score = scoreAM(am);

  // All KPIs with their status
  const kpis = [
    { label: "Touch Coverage", value: `${am.touchCoverage}%`, status: statusOf(am.touchCoverage, THRESHOLDS.touchCoverage), target: "100%", raw: am.touchCoverage, max: 100 },
    { label: "Dormancy Rate",  value: `${am.dormancy}%`,      status: statusOf(am.dormancy, THRESHOLDS.dormancy),           target: "< 20%", raw: am.dormancy, max: 40 },
    { label: "Highly Engaged %",value: `${Math.round(am.tierHE/am.accounts*100)}%`, status: statusOf(Math.round(am.tierHE/am.accounts*100), THRESHOLDS.highlyEngaged), target: "≥ 40%", raw: Math.round(am.tierHE/am.accounts*100), max: 100 },
    { label: "Capture Rate",   value: `${am.captureRate}%`,   status: statusOf(am.captureRate, THRESHOLDS.captureRate),     target: "≥ 60%", raw: am.captureRate, max: 100 },
    { label: "GMV at Risk",    value: fmt$(am.gmvAtRisk),     status: statusOf(am.gmvAtRisk, THRESHOLDS.gmvAtRisk),         target: "< $25K", raw: am.gmvAtRisk, max: 120000 },
    { label: "GMV Growth MoM", value: `${am.gmvGrowth >= 0 ? "+" : ""}${am.gmvGrowth}%`, status: statusOf(am.gmvGrowth, THRESHOLDS.gmvGrowth), target: "≥ 10%", raw: Math.max(0, am.gmvGrowth), max: 20 },
    { label: "Never-Active > 60d",value: am.neverActive60,    status: statusOf(am.neverActive60, THRESHOLDS.neverActive60), target: "0", raw: am.neverActive60, max: 5 },
    { label: "CRM Logging (24h)", value: `${am.crmLogging}%`, status: statusOf(am.crmLogging, THRESHOLDS.crmLogging),       target: "100%", raw: am.crmLogging, max: 100 },
    { label: "Days to Training", value: `${am.daysToTraining}d`, status: statusOf(am.daysToTraining, THRESHOLDS.daysToTraining), target: "< 7d", raw: am.daysToTraining, max: 15 },
    { label: "Retraining SLA",  value: `${am.retraining}d`,   status: statusOf(am.retraining, THRESHOLDS.retraining),       target: "< 14d", raw: am.retraining, max: 30 },
    { label: "Cadence Completion",value: `${am.cadenceComp}%`,status: statusOf(am.cadenceComp, THRESHOLDS.cadenceComp),     target: "≥ 95%", raw: am.cadenceComp, max: 100 },
  ];

  const untouched = merchants.filter(m => m.lastTouch > 7).sort((a,b) => b.lastTouch - a.lastTouch);
  const dormant   = merchants.filter(m => m.tier === "D");

  // Partner breakdown for this AM
  const partnerCounts = merchants.reduce((acc, m) => {
    acc[m.partner] = acc[m.partner] || { gmv: 0, stores: 0, dormant: 0 };
    acc[m.partner].gmv += m.gmv;
    acc[m.partner].stores++;
    if (m.tier === "D") acc[m.partner].dormant++;
    return acc;
  }, {});
  const partnerData = Object.entries(partnerCounts).map(([name, v]) => ({ name, ...v }));

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>

      {/* ── Header ── */}
      <Card padded={false}>
        <div style={{ padding: 20, display: "flex", alignItems: "center", gap: 20, borderBottom: `1px solid ${SF.border}` }}>
          <Avatar initials={am.initials} status={score.status} size={64} />
          <div style={{ flex: 1 }}>
            <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
              <div style={{ fontSize: 22, fontWeight: 700, color: SF.navy }}>{am.name}</div>
              <Pill status={score.status}>{statusLabel(score.status)}</Pill>
            </div>
            <div style={{ fontSize: 13, color: SF.muted, marginTop: 2 }}>
              {am.title} · {am.accounts} dealer accounts{am.id !== "jerome" ? " · Reporting to Jerome Carthen (AM Team Lead)" : ""}
            </div>
          </div>
          <div style={{ textAlign: "right" }}>
            <div style={{ fontSize: 11, color: SF.muted, textTransform: "uppercase", letterSpacing: 0.4, fontWeight: 700 }}>
              Performance Score
            </div>
            <div style={{ fontSize: 44, fontWeight: 700, color: statusColor(score.status), lineHeight: 1 }}>
              {score.score}
            </div>
            <div style={{ fontSize: 11, color: SF.muted }}>
              <span style={{ color: SF.green }}>{score.g} Green</span> ·{" "}
              <span style={{ color: SF.orange }}>{score.y} Yellow</span> ·{" "}
              <span style={{ color: SF.red }}>{score.r} Red</span>
            </div>
          </div>
        </div>
        <div style={{ padding: "14px 20px", display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 20, background: "#fafaf9" }}>
          <HeaderStat label="GMV · MTD"       value={fmt$full(am.gmvMTD)} sub={`${am.gmvGrowth >= 0 ? "▲" : "▼"} ${Math.abs(am.gmvGrowth)}% MoM`} subColor={am.gmvGrowth >= 0 ? SF.green : SF.red} />
          <HeaderStat label="Highly Engaged"  value={`${am.tierHE} / ${am.accounts}`}     sub={`${Math.round(am.tierHE/am.accounts*100)}% of book`} />
          <HeaderStat label="Dormant ($0)"    value={am.tierD}                            sub={`${am.dormancy}% dormancy rate`} subColor={statusColor(statusOf(am.dormancy, THRESHOLDS.dormancy))} />
          <HeaderStat label="GMV at Risk"     value={fmt$full(am.gmvAtRisk)}              sub="Opportunity to recover" subColor={SF.red} />
        </div>
      </Card>

      {/* ── KPI Scorecard (Playbook Alignment) ── */}
      <Card title="KPI Scorecard · AM Playbook Thresholds">
        <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 10 }}>
          {kpis.map(k => (
            <div key={k.label} style={{
              padding: 12,
              border: `1px solid ${SF.border}`,
              borderLeft: `4px solid ${statusColor(k.status)}`,
              borderRadius: 4,
              background: k.status === "red" ? SF.redBg + "40" : "white",
            }}>
              <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 6 }}>
                <div style={{ fontSize: 11, fontWeight: 700, color: SF.muted, textTransform: "uppercase", letterSpacing: 0.3 }}>
                  {k.label}
                </div>
                <StatusDot status={k.status} />
              </div>
              <div style={{ display: "flex", alignItems: "baseline", justifyContent: "space-between" }}>
                <div style={{ fontSize: 22, fontWeight: 700, color: statusColor(k.status) }}>{k.value}</div>
                <div style={{ fontSize: 10, color: SF.muted }}>Target: {k.target}</div>
              </div>
            </div>
          ))}
        </div>
      </Card>

      {/* ── Portfolio Composition ── */}
      <div style={{ display: "grid", gridTemplateColumns: "1.4fr 1fr", gap: 16 }}>
        <Card title="Portfolio Composition by Engagement Tier">
          <div style={{ marginBottom: 16 }}>
            <TierBar he={am.tierHE} me={am.tierME} le={am.tierLE} d={am.tierD} />
          </div>
          <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 10 }}>
            <TierTile label="Highly Engaged" count={am.tierHE} subtitle="$10K+ / mo" color={SF.green}  total={am.accounts} />
            <TierTile label="Mid Engaged"    count={am.tierME} subtitle="$2.5K–$10K" color={SF.teal}   total={am.accounts} />
            <TierTile label="Low Engaged"    count={am.tierLE} subtitle="< $2.5K"    color={SF.orange} total={am.accounts} />
            <TierTile label="Dormant"        count={am.tierD}  subtitle="$0"         color={SF.red}    total={am.accounts} />
          </div>
          <div style={{
            marginTop: 16, padding: 12,
            background: SF.gray, borderRadius: 4,
            fontSize: 12, color: SF.muted, lineHeight: 1.5,
          }}>
            <strong style={{ color: SF.navy }}>GMV Capture Model:</strong>{" "}
            Max potential = (book × $10K floor) = <strong>{fmt$(am.accounts * 10000)}/mo</strong>.
            Current capture at {am.captureRate}% implies <strong>{fmt$(am.accounts * 10000 * (1 - am.captureRate/100))}</strong> in recoverable upside.
          </div>
        </Card>

        <Card title="Partner Distribution">
          <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 12 }}>
            <thead>
              <tr style={{ borderBottom: `1px solid ${SF.border}` }}>
                <th style={thLSm}>Partner</th>
                <th style={thSm}>Stores</th>
                <th style={thSm}>GMV</th>
                <th style={thSm}>Dormant</th>
              </tr>
            </thead>
            <tbody>
              {partnerData.map(p => (
                <tr key={p.name} style={{ borderBottom: `1px solid ${SF.border}` }}>
                  <td style={tdLSm}>{p.name}</td>
                  <td style={tdSm}>{p.stores}</td>
                  <td style={tdSm}>{fmt$(p.gmv)}</td>
                  <td style={{ ...tdSm, color: p.dormant > 0 ? SF.red : SF.green, fontWeight: 700 }}>
                    {p.dormant}
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </Card>
      </div>

      {/* ── Action Queues ── */}
      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
        <Card title={`Untouched Accounts (${untouched.length})`}
              action={<span style={{ fontSize: 11, color: SF.red }}>Priority outreach required</span>}>
          {untouched.length === 0 ? (
            <div style={{ padding: 20, textAlign: "center", color: SF.green, fontWeight: 600 }}>
              All accounts touched this month ✓
            </div>
          ) : (
            <div style={{ display: "flex", flexDirection: "column", gap: 6 }}>
              {untouched.map(m => (
                <div key={m.name} style={{
                  display: "flex", alignItems: "center",
                  padding: "8px 10px", borderRadius: 4,
                  background: m.lastTouch > 20 ? SF.redBg + "60" : SF.orangeBg,
                  borderLeft: `3px solid ${m.lastTouch > 20 ? SF.red : SF.orange}`,
                }}>
                  <div style={{ flex: 1 }}>
                    <div style={{ fontSize: 12, fontWeight: 600, color: SF.navy }}>{m.name}</div>
                    <div style={{ fontSize: 11, color: SF.muted }}>{m.partner} · Tier {m.tier} · {m.gmv === 0 ? "Dormant" : fmt$(m.gmv)}</div>
                  </div>
                  <div style={{ fontSize: 11, fontWeight: 700, color: m.lastTouch > 20 ? SF.red : SF.orange, marginRight: 10 }}>
                    {m.lastTouch}d
                  </div>
                  <button style={btnPrimary}>Log Touch</button>
                </div>
              ))}
            </div>
          )}
        </Card>

        <Card title={`Dormant Accounts ($0 GMV) (${dormant.length})`}
              action={<span style={{ fontSize: 11, color: SF.red }}>14-day retraining trigger</span>}>
          {dormant.length === 0 ? (
            <div style={{ padding: 20, textAlign: "center", color: SF.green, fontWeight: 600 }}>
              No dormant accounts ✓
            </div>
          ) : (
            <div style={{ display: "flex", flexDirection: "column", gap: 6 }}>
              {dormant.map(m => (
                <div key={m.name} style={{
                  display: "flex", alignItems: "center",
                  padding: "8px 10px", borderRadius: 4,
                  background: SF.redBg + "60",
                  borderLeft: `3px solid ${SF.red}`,
                }}>
                  <div style={{ flex: 1 }}>
                    <div style={{ fontSize: 12, fontWeight: 600, color: SF.navy }}>{m.name}</div>
                    <div style={{ fontSize: 11, color: SF.muted }}>{m.partner} · GMV at Risk: <strong style={{ color: SF.red }}>$10K/mo</strong></div>
                  </div>
                  <button style={btnPrimary}>Schedule Retraining</button>
                </div>
              ))}
            </div>
          )}
        </Card>
      </div>

      {/* ── Coaching Note (visible to Exec only) ── */}
      {isExec && (
        <Card title="Manager Coaching Note · Exec Only">
          <CoachingNote am={am} score={score} />
        </Card>
      )}
    </div>
  );
}

const HeaderStat = ({ label, value, sub, subColor }) => (
  <div>
    <div style={{ fontSize: 10, fontWeight: 700, color: SF.muted, textTransform: "uppercase", letterSpacing: 0.4 }}>
      {label}
    </div>
    <div style={{ fontSize: 20, fontWeight: 700, color: SF.navy, marginTop: 2 }}>{value}</div>
    {sub && <div style={{ fontSize: 11, color: subColor || SF.muted, marginTop: 2 }}>{sub}</div>}
  </div>
);

const TierTile = ({ label, count, subtitle, color, total }) => (
  <div style={{ textAlign: "center", padding: 12, border: `1px solid ${SF.border}`, borderRadius: 4, borderTop: `3px solid ${color}` }}>
    <div style={{ fontSize: 28, fontWeight: 700, color }}>{count}</div>
    <div style={{ fontSize: 12, fontWeight: 600, color: SF.navy }}>{label}</div>
    <div style={{ fontSize: 10, color: SF.muted }}>{subtitle}</div>
    <div style={{ fontSize: 10, color: SF.muted, marginTop: 4 }}>
      {Math.round((count/total)*100)}% of book
    </div>
  </div>
);

const CoachingNote = ({ am, score }) => {
  let note;
  if (score.status === "green") {
    note = `${am.name.split(" ")[0]} is performing above target on ${score.g} of 10 KPIs. Recommendation: amplify their cadence as the team standard. Consider assigning 2-3 new Xtime merchants from Roman or Carlos's book to test scale capacity.`;
  } else if (score.status === "yellow") {
    note = `${am.name.split(" ")[0]} is mixed — ${score.g} green, ${score.y} yellow, ${score.r} red. Weakest areas: ${am.dormancy > 20 ? "dormancy" : ""} ${am.captureRate < 60 ? ", capture rate" : ""} ${am.retraining > 14 ? ", retraining SLA" : ""}. Recommendation: 30-day focus plan on untouched accounts + retraining backlog. Revisit in weekly 1:1.`;
  } else {
    note = `${am.name.split(" ")[0]} is red on ${score.r} KPIs with $${(am.gmvAtRisk/1000).toFixed(0)}K GMV at risk. Recommendation: formal PIP, reassignment of ${am.tierD} dormant stores to a top-performing AM, and a cadence audit this week. Escalate to VP if no green-zone KPI recovery within 30 days.`;
  }
  return (
    <div style={{
      padding: 14, borderRadius: 6,
      background: statusBg(score.status) + "60",
      borderLeft: `4px solid ${statusColor(score.status)}`,
      fontSize: 13, color: SF.text, lineHeight: 1.55,
    }}>
      {note}
    </div>
  );
};

// ═══════════════════════════════════════════════════════════════════════
// TABLE STYLES
// ═══════════════════════════════════════════════════════════════════════
const th    = { padding: "10px 12px", textAlign: "center", fontSize: 11, fontWeight: 700, color: SF.muted, textTransform: "uppercase", letterSpacing: 0.3 };
const thL   = { ...th, textAlign: "left" };
const thSm  = { padding: "8px 8px", textAlign: "center", fontSize: 10, fontWeight: 700, color: SF.muted, textTransform: "uppercase" };
const thLSm = { ...thSm, textAlign: "left" };
const td    = { padding: "12px 12px", textAlign: "center", fontSize: 13, color: SF.text };
const tdL   = { ...td, textAlign: "left" };
const tdSm  = { padding: "6px 8px", textAlign: "center", fontSize: 12, color: SF.text };
const tdLSm = { ...tdSm, textAlign: "left" };
const btnLink    = { fontSize: 11, background: "transparent", border: "none", color: SF.blue, cursor: "pointer", fontWeight: 600 };
const btnPrimary = { fontSize: 11, background: SF.blue, border: "none", color: "white", padding: "5px 12px", borderRadius: 4, cursor: "pointer", fontWeight: 600 };

// ═══════════════════════════════════════════════════════════════════════
// MAIN APP
// ═══════════════════════════════════════════════════════════════════════
export default function Dashboard() {
  // view = "exec" | "am-<id>"  (and isExecAsAM tracks whether we drilled from exec)
  const [view, setView] = useState("exec");
  const [drilledFromExec, setDrilledFromExec] = useState(false);

  // User identity — in real Salesforce this comes from session. Here, selector.
  const [identity, setIdentity] = useState("exec");
  const isExec = identity === "exec";

  const currentAM = view.startsWith("am-") ? view.slice(3) : null;
  const goExec = () => { setView("exec"); setDrilledFromExec(false); };
  const goAM = (id, fromExec = false) => { setView(`am-${id}`); setDrilledFromExec(fromExec); };

  // When user switches identity, reset to their default view
  const switchIdentity = (id) => {
    setIdentity(id);
    if (id === "exec") setView("exec");
    else setView(`am-${id}`);
    setDrilledFromExec(false);
  };

  return (
    <div style={{
      minHeight: "100vh",
      background: "#f3f3f3",
      fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif',
      color: SF.text,
    }}>
      {/* ── Salesforce-style top bar ── */}
      <div style={{
        background: SF.navy, color: "white",
        padding: "10px 24px",
        display: "flex", alignItems: "center", gap: 20,
        borderBottom: `3px solid ${SF.blue}`,
      }}>
        <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
          <div style={{
            width: 30, height: 30, borderRadius: 6,
            background: SF.blue, color: "white",
            display: "flex", alignItems: "center", justifyContent: "center",
            fontWeight: 700, fontSize: 14,
          }}>
            ☁
          </div>
          <div style={{ fontSize: 15, fontWeight: 600 }}>
            DigniFi · Sales <span style={{ opacity: 0.6 }}>/</span> AM Performance
          </div>
        </div>
        <div style={{ flex: 1 }} />
        <div style={{ display: "flex", alignItems: "center", gap: 10, fontSize: 12 }}>
          <span style={{ opacity: 0.7 }}>Viewing as:</span>
          <select
            value={identity}
            onChange={(e) => switchIdentity(e.target.value)}
            style={{
              background: "rgba(255,255,255,0.1)",
              color: "white", border: "1px solid rgba(255,255,255,0.2)",
              padding: "4px 10px", borderRadius: 4, fontSize: 12,
            }}
          >
            <option value="exec" style={{ color: "black" }}>👔 Executive (Full Access)</option>
            <optgroup label="Individual AM View" style={{ color: "black" }}>
              {AMs.map(am => (
                <option key={am.id} value={am.id} style={{ color: "black" }}>
                  {am.name} — {am.title}
                </option>
              ))}
            </optgroup>
          </select>
        </div>
      </div>

      {/* ── Page Header ── */}
      <div style={{
        background: "white",
        padding: "16px 24px",
        borderBottom: `1px solid ${SF.border}`,
        display: "flex", alignItems: "center", justifyContent: "space-between",
      }}>
        <div>
          <div style={{ fontSize: 11, color: SF.muted, textTransform: "uppercase", letterSpacing: 0.4, fontWeight: 600 }}>
            <span style={{ cursor: isExec && currentAM ? "pointer" : "default" }} onClick={() => isExec && goExec()}>
              Account Management
            </span>
            {currentAM && <> <span style={{ opacity: 0.5 }}>/</span> {AMs.find(a => a.id === currentAM)?.name}</>}
          </div>
          <div style={{ fontSize: 22, fontWeight: 700, color: SF.navy, marginTop: 2 }}>
            {currentAM
              ? `${AMs.find(a => a.id === currentAM)?.name} · Performance`
              : "AM Performance Dashboard"}
          </div>
          <div style={{ fontSize: 12, color: SF.muted, marginTop: 2 }}>
            {isExec
              ? "Executive rollup · Full access to all AMs and merchants"
              : `Account Manager view · ${AMs.find(a => a.id === identity)?.name}'s book only`}
            {" · "}Period: Feb 1 – Feb 28, 2026
          </div>
        </div>
        {isExec && currentAM && drilledFromExec && (
          <button
            onClick={goExec}
            style={{
              fontSize: 12, background: "white",
              border: `1px solid ${SF.blue}`, color: SF.blue,
              padding: "6px 14px", borderRadius: 4, cursor: "pointer", fontWeight: 600,
            }}
          >
            ← Back to Team Rollup
          </button>
        )}
      </div>

      {/* ── Main Content ── */}
      <div style={{ padding: 20, maxWidth: 1480, margin: "0 auto" }}>
        {view === "exec" && isExec ? (
          <ExecutiveView onDrill={(id) => goAM(id, true)} />
        ) : (
          <AMDetailView
            amId={currentAM || identity}
            onBack={goExec}
            isExec={isExec}
          />
        )}
      </div>

      {/* ── Footer ── */}
      <div style={{ textAlign: "center", padding: "16px 0 24px", fontSize: 11, color: SF.light }}>
        DigniFi · AM Performance Dashboard · Salesforce Lightning · Data refreshed daily at 6:00 AM CT
      </div>
    </div>
  );
}
