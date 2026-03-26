import { useState, useEffect, useMemo, useCallback } from "react";
import { LineChart, Line, XAxis, YAxis, Tooltip, ResponsiveContainer, Area, ComposedChart, ReferenceLine } from "recharts";

const PERIODS = [
  { key: "1mo", label: "1개월" },
  { key: "3mo", label: "3개월" },
  { key: "6mo", label: "6개월" },
  { key: "1y", label: "1년" },
];

const fetchData = async (symbol, range) => {
  const yahooUrl = `https://query1.finance.yahoo.com/v8/finance/chart/${symbol}?range=${range}&interval=1d&includePrePost=false`;
  const proxies = [
    yahooUrl,
    `https://api.allorigins.win/raw?url=${encodeURIComponent(yahooUrl)}`,
    `https://corsproxy.io/?url=${encodeURIComponent(yahooUrl)}`,
  ];
  for (const url of proxies) {
    try {
      const r = await fetch(url, { signal: AbortSignal.timeout(8000) });
      if (!r.ok) continue;
      const d = await r.json();
      const res = d.chart?.result?.[0];
      if (!res) continue;
      const ts = res.timestamp || [];
      const closes = res.indicators?.quote?.[0]?.close || [];
      const current = res.meta?.regularMarketPrice;
      const points = ts.map((t, i) => ({ ts: t * 1000, close: closes[i] })).filter(p => p.close != null);
      return { current, points };
    } catch { continue; }
  }
  return null;
};

/* ── Gauge Bar ─────────────────────────────────────────── */
function GaugeBar({ label, current, min, max, midpoint, midLabel, isGood, unit, decimals = 2 }) {
  const range = max - min || 1;
  const pct = Math.max(0, Math.min(100, ((current - min) / range) * 100));
  const midPct = midpoint != null ? Math.max(0, Math.min(100, ((midpoint - min) / range) * 100)) : null;
  const diffFromMin = ((current - min) / min * 100);
  const diffFromMax = ((current - max) / max * 100);
  const diffFromMid = midpoint != null ? ((current - midpoint) / midpoint * 100) : null;

  const fmt = (v) => {
    if (unit === "%") return v.toFixed(decimals) + "%";
    return v.toFixed(decimals);
  };

  return (
    <div style={{ marginBottom: 28 }}>
      <div style={{ display: "flex", alignItems: "center", gap: 16, marginBottom: 8 }}>
        <div style={{
          width: 52, height: 52, borderRadius: "50%", display: "flex", alignItems: "center", justifyContent: "center",
          background: isGood ? "rgba(74,222,128,0.12)" : "rgba(248,113,113,0.12)",
          border: `2.5px solid ${isGood ? "#4ade80" : "#f87171"}`,
          fontSize: 26, fontWeight: 700, color: isGood ? "#4ade80" : "#f87171",
          flexShrink: 0, transition: "all 0.4s ease",
        }}>
          {isGood ? "O" : "✕"}
        </div>
        <div style={{ flex: 1 }}>
          <div style={{ fontSize: 15, fontWeight: 600, color: "#cbd5e1", marginBottom: 2, letterSpacing: "0.02em" }}>{label}</div>
          <div style={{
            fontSize: 24, fontWeight: 700, letterSpacing: "-0.02em",
            color: isGood ? "#4ade80" : "#f87171",
            fontFamily: "'JetBrains Mono', 'SF Mono', monospace",
          }}>{fmt(current)}</div>
        </div>
      </div>
      {/* Track */}
      <div style={{ position: "relative", height: 10, borderRadius: 5, background: "#1e293b", margin: "8px 0 6px", overflow: "visible" }}>
        {/* Filled portion */}
        <div style={{
          position: "absolute", left: 0, top: 0, bottom: 0, borderRadius: 5,
          width: `${pct}%`, background: isGood
            ? "linear-gradient(90deg, #065f46, #4ade80)"
            : "linear-gradient(90deg, #991b1b, #f87171)",
          transition: "width 0.6s cubic-bezier(0.4,0,0.2,1)",
        }} />
        {/* Midpoint marker */}
        {midPct != null && (
          <div style={{
            position: "absolute", left: `${midPct}%`, top: -3, width: 16, height: 16,
            borderRadius: "50%", background: "#475569", border: "2px solid #64748b",
            transform: "translateX(-50%)", zIndex: 2,
          }} />
        )}
        {/* Current marker */}
        <div style={{
          position: "absolute", left: `${pct}%`, top: -4, width: 18, height: 18,
          borderRadius: "50%", border: "2.5px solid #fff",
          background: isGood ? "#4ade80" : "#f87171",
          transform: "translateX(-50%)", zIndex: 3,
          boxShadow: `0 0 12px ${isGood ? "rgba(74,222,128,0.5)" : "rgba(248,113,113,0.5)"}`,
          transition: "left 0.6s cubic-bezier(0.4,0,0.2,1)",
        }} />
      </div>
      {/* Labels */}
      <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12, fontFamily: "'JetBrains Mono', monospace" }}>
        <div style={{ color: "#64748b" }}>
          {fmt(min)}<br />
          <span style={{ color: "#94a3b8", fontSize: 11 }}>({diffFromMin >= 0 ? "+" : ""}{diffFromMin.toFixed(2)}%)</span>
        </div>
        {midpoint != null && (
          <div style={{ color: "#94a3b8", textAlign: "center" }}>
            {midLabel || fmt(midpoint)}<br />
            <span style={{ fontSize: 11 }}>({diffFromMid >= 0 ? "+" : ""}{diffFromMid.toFixed(2)}%)</span>
          </div>
        )}
        <div style={{ color: "#64748b", textAlign: "right" }}>
          {fmt(max)}<br />
          <span style={{ color: "#94a3b8", fontSize: 11 }}>({diffFromMax >= 0 ? "+" : ""}{diffFromMax.toFixed(2)}%)</span>
        </div>
      </div>
    </div>
  );
}

/* ── Mini sparkline ─────────────────────────────────────── */
function Sparkline({ data, color, height = 60 }) {
  if (!data || data.length === 0) return null;
  return (
    <ResponsiveContainer width="100%" height={height}>
      <LineChart data={data} margin={{ top: 4, right: 4, bottom: 4, left: 4 }}>
        <Line type="monotone" dataKey="v" stroke={color} strokeWidth={1.5} dot={false} />
      </LineChart>
    </ResponsiveContainer>
  );
}

/* ── Custom Tooltip ─────────────────────────────────────── */
function ChartTooltip({ active, payload, label }) {
  if (!active || !payload?.length) return null;
  return (
    <div style={{
      background: "#1e293b", border: "1px solid #334155", borderRadius: 8, padding: "10px 14px",
      fontSize: 12, fontFamily: "'JetBrains Mono', monospace",
    }}>
      <div style={{ color: "#94a3b8", marginBottom: 6 }}>{label}</div>
      {payload.map((p, i) => (
        <div key={i} style={{ color: p.color, marginBottom: 2 }}>
          {p.name}: {p.value?.toFixed(2)}
        </div>
      ))}
    </div>
  );
}

/* ── Main App ──────────────────────────────────────────── */
export default function DollarDashboard() {
  const [period, setPeriod] = useState("1y");
  const [krwData, setKrwData] = useState(null);
  const [dxyData, setDxyData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [tab, setTab] = useState("suitability"); // suitability | fairrate

  const loadData = useCallback(async () => {
    setLoading(true);
    setError(null);
    try {
      const [krw, dxy] = await Promise.all([
        fetchData("KRW=X", period),
        fetchData("DX-Y.NYB", period),
      ]);
      if (!krw || !dxy) {
        setError("데이터를 가져올 수 없습니다. 잠시 후 다시 시도해주세요.");
      } else {
        setKrwData(krw);
        setDxyData(dxy);
      }
    } catch (e) {
      setError("네트워크 오류: " + e.message);
    }
    setLoading(false);
  }, [period]);

  useEffect(() => { loadData(); }, [loadData]);

  /* ── Derived stats ──────────────────────────────── */
  const stats = useMemo(() => {
    if (!krwData || !dxyData) return null;

    const krwPrices = krwData.points.map(p => p.close);
    const dxyPrices = dxyData.points.map(p => p.close);

    const krwCurrent = krwData.current;
    const dxyCurrent = dxyData.current;
    const krwMin = Math.min(...krwPrices);
    const krwMax = Math.max(...krwPrices);
    const dxyMin = Math.min(...dxyPrices);
    const dxyMax = Math.max(...dxyPrices);
    const krwAvg = krwPrices.reduce((a, b) => a + b, 0) / krwPrices.length;
    const dxyAvg = dxyPrices.reduce((a, b) => a + b, 0) / dxyPrices.length;

    // Fair rate: Use average ratio of KRW/DXY over the period, then multiply by current DXY
    const minLen = Math.min(krwData.points.length, dxyData.points.length);
    const ratios = [];
    for (let i = 0; i < minLen; i++) {
      const k = krwData.points[krwData.points.length - minLen + i]?.close;
      const d = dxyData.points[dxyData.points.length - minLen + i]?.close;
      if (k && d && d > 0) ratios.push(k / d);
    }
    const avgRatio = ratios.length > 0 ? ratios.reduce((a, b) => a + b, 0) / ratios.length : krwAvg / dxyAvg;
    const fairRate = dxyCurrent * avgRatio;

    // Gap ratio: how much current deviates from fair
    const gapRatio = ((krwCurrent - fairRate) / fairRate) * 100;

    // Historical gap ratios for min/max
    const gapHistory = ratios.map((r, i) => {
      const k = krwData.points[krwData.points.length - minLen + i]?.close;
      const d = dxyData.points[dxyData.points.length - minLen + i]?.close;
      const fair = d * avgRatio;
      return ((k - fair) / fair) * 100;
    }).filter(g => isFinite(g));
    const gapMin = gapHistory.length > 0 ? Math.min(...gapHistory) : gapRatio - 3;
    const gapMax = gapHistory.length > 0 ? Math.max(...gapHistory) : gapRatio + 3;
    const gapAvg = gapHistory.length > 0 ? gapHistory.reduce((a, b) => a + b, 0) / gapHistory.length : 0;

    // Chart data (merged by index)
    const chartData = [];
    for (let i = 0; i < minLen; i++) {
      const ki = krwData.points.length - minLen + i;
      const di = dxyData.points.length - minLen + i;
      const date = new Date(krwData.points[ki].ts);
      const k = krwData.points[ki].close;
      const d = dxyData.points[di].close;
      const fair = d * avgRatio;
      chartData.push({
        date: `${date.getMonth() + 1}/${date.getDate()}`,
        krw: Math.round(k * 100) / 100,
        dxy: Math.round(d * 100) / 100,
        fair: Math.round(fair * 100) / 100,
        gap: Math.round(((k - fair) / fair) * 10000) / 100,
      });
    }

    // Suitability logic
    const krwPosition = (krwCurrent - krwMin) / (krwMax - krwMin || 1); // 0=low(good), 1=high(bad)
    const dxyPosition = (dxyCurrent - dxyMin) / (dxyMax - dxyMin || 1);
    const isKrwGood = krwPosition < 0.4; // dollar is cheap
    const isDxyGood = dxyPosition < 0.4; // DXY is low
    const isGapGood = gapRatio < gapAvg; // gap is below average
    const isFairGood = krwCurrent < fairRate; // actual < fair = cheap

    const goodCount = [isKrwGood, isDxyGood, isGapGood, isFairGood].filter(Boolean).length;
    const overallGood = goodCount >= 3;

    return {
      krwCurrent, dxyCurrent, krwMin, krwMax, dxyMin, dxyMax, krwAvg, dxyAvg,
      fairRate, gapRatio, gapMin, gapMax, gapAvg,
      chartData,
      isKrwGood, isDxyGood, isGapGood, isFairGood, overallGood, goodCount,
      krwSparkline: krwData.points.slice(-30).map(p => ({ v: p.close })),
      dxySparkline: dxyData.points.slice(-30).map(p => ({ v: p.close })),
    };
  }, [krwData, dxyData]);

  /* ── Styles ──────────────────────────────────────── */
  const card = {
    background: "linear-gradient(135deg, #111827 0%, #0f172a 100%)",
    borderRadius: 16, padding: "20px 22px", marginBottom: 16,
    border: "1px solid rgba(71,85,105,0.3)",
    boxShadow: "0 4px 24px rgba(0,0,0,0.3)",
  };

  return (
    <div style={{
      minHeight: "100vh", background: "#030712",
      color: "#e2e8f0", fontFamily: "'Pretendard', 'Apple SD Gothic Neo', -apple-system, sans-serif",
      padding: "0 0 40px",
    }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&display=swap');
        * { box-sizing: border-box; margin: 0; padding: 0; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #334155; border-radius: 3px; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.4; } }
        @keyframes spin { to { transform: rotate(360deg); } }
        .fade-in { animation: fadeIn 0.5s ease forwards; }
        .stagger-1 { animation-delay: 0.05s; opacity: 0; }
        .stagger-2 { animation-delay: 0.15s; opacity: 0; }
        .stagger-3 { animation-delay: 0.25s; opacity: 0; }
        .stagger-4 { animation-delay: 0.35s; opacity: 0; }
        .tab-btn { cursor: pointer; border: none; padding: 10px 20px; border-radius: 10px; font-size: 14px; font-weight: 600; transition: all 0.25s; font-family: inherit; }
        .tab-btn.active { background: #1e40af; color: #fff; box-shadow: 0 0 20px rgba(59,130,246,0.3); }
        .tab-btn.inactive { background: transparent; color: #64748b; }
        .tab-btn.inactive:hover { color: #94a3b8; background: rgba(51,65,85,0.3); }
        .period-btn { cursor: pointer; border: 1px solid #334155; padding: 7px 16px; border-radius: 8px; font-size: 13px; font-weight: 600; transition: all 0.2s; font-family: inherit; background: transparent; color: #94a3b8; }
        .period-btn.active { background: #1e293b; color: #60a5fa; border-color: #3b82f6; box-shadow: 0 0 12px rgba(59,130,246,0.15); }
        .period-btn:hover { border-color: #475569; }
      `}</style>

      {/* Header */}
      <div style={{
        background: "linear-gradient(180deg, #0f172a 0%, #030712 100%)",
        padding: "28px 20px 20px", borderBottom: "1px solid rgba(51,65,85,0.3)",
        position: "sticky", top: 0, zIndex: 10, backdropFilter: "blur(12px)",
      }}>
        <div style={{ maxWidth: 600, margin: "0 auto" }}>
          <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", marginBottom: 16 }}>
            <div>
              <h1 style={{
                fontSize: 22, fontWeight: 800, letterSpacing: "-0.03em",
                background: "linear-gradient(135deg, #60a5fa, #a78bfa)",
                WebkitBackgroundClip: "text", WebkitTextFillColor: "transparent",
              }}>💵 달러 투자 대시보드</h1>
              <div style={{ fontSize: 11, color: "#475569", marginTop: 4, fontFamily: "'JetBrains Mono', monospace" }}>
                Yahoo Finance 실시간 데이터
              </div>
            </div>
            <button onClick={loadData} disabled={loading} style={{
              background: "rgba(51,65,85,0.4)", border: "1px solid #334155", borderRadius: 10,
              padding: "8px 14px", color: "#94a3b8", fontSize: 13, cursor: "pointer",
              display: "flex", alignItems: "center", gap: 6, fontFamily: "inherit",
            }}>
              <span style={{ display: "inline-block", animation: loading ? "spin 1s linear infinite" : "none" }}>↻</span>
              새로고침
            </button>
          </div>

          {/* Tabs */}
          <div style={{ display: "flex", gap: 8, marginBottom: 12 }}>
            <button className={`tab-btn ${tab === "suitability" ? "active" : "inactive"}`} onClick={() => setTab("suitability")}>
              투자 적합성
            </button>
            <button className={`tab-btn ${tab === "fairrate" ? "active" : "inactive"}`} onClick={() => setTab("fairrate")}>
              적정환율 분석
            </button>
          </div>

          {/* Period selector */}
          <div style={{ display: "flex", gap: 6 }}>
            {PERIODS.map(p => (
              <button key={p.key} className={`period-btn ${period === p.key ? "active" : ""}`} onClick={() => setPeriod(p.key)}>
                {p.label}
              </button>
            ))}
          </div>
        </div>
      </div>

      <div style={{ maxWidth: 600, margin: "0 auto", padding: "20px 16px 0" }}>
        {/* Loading state */}
        {loading && (
          <div style={{ textAlign: "center", padding: "60px 0" }}>
            <div style={{
              width: 48, height: 48, border: "3px solid #1e293b", borderTopColor: "#3b82f6",
              borderRadius: "50%", animation: "spin 0.8s linear infinite", margin: "0 auto 16px",
            }} />
            <div style={{ color: "#64748b", fontSize: 14 }}>데이터를 불러오는 중...</div>
          </div>
        )}

        {/* Error state */}
        {error && !loading && (
          <div style={{
            ...card, background: "rgba(127,29,29,0.15)", border: "1px solid rgba(248,113,113,0.3)",
            textAlign: "center", padding: 32,
          }}>
            <div style={{ fontSize: 36, marginBottom: 12 }}>⚠️</div>
            <div style={{ color: "#fca5a5", fontSize: 14, marginBottom: 8 }}>{error}</div>
            <div style={{ color: "#64748b", fontSize: 12 }}>
              Yahoo Finance API 접근이 차단된 환경일 수 있습니다.<br />
              로컬 환경에서 실행하면 정상 동작합니다.
            </div>
          </div>
        )}

        {/* ══════════════ TAB: 투자 적합성 ══════════════ */}
        {!loading && stats && tab === "suitability" && (
          <div>
            {/* Overall verdict */}
            <div className="fade-in" style={{
              ...card, textAlign: "center", position: "relative", overflow: "hidden",
              background: stats.overallGood
                ? "linear-gradient(135deg, rgba(6,95,70,0.25), rgba(4,47,46,0.15))"
                : "linear-gradient(135deg, rgba(127,29,29,0.25), rgba(69,10,10,0.15))",
              border: `1px solid ${stats.overallGood ? "rgba(74,222,128,0.2)" : "rgba(248,113,113,0.2)"}`,
            }}>
              <div style={{
                position: "absolute", inset: 0, opacity: 0.04,
                background: `radial-gradient(circle at 50% 50%, ${stats.overallGood ? "#4ade80" : "#f87171"}, transparent 70%)`,
              }} />
              <div style={{ position: "relative" }}>
                <div style={{ fontSize: 11, color: "#94a3b8", fontWeight: 600, letterSpacing: "0.15em", textTransform: "uppercase", marginBottom: 8 }}>
                  달러 투자 적합성 종합 판단
                </div>
                <div style={{
                  fontSize: 56, fontWeight: 800, lineHeight: 1,
                  color: stats.overallGood ? "#4ade80" : "#f87171",
                  textShadow: `0 0 40px ${stats.overallGood ? "rgba(74,222,128,0.4)" : "rgba(248,113,113,0.4)"}`,
                }}>
                  {stats.overallGood ? "매수 적합" : "매수 부적합"}
                </div>
                <div style={{
                  display: "inline-flex", gap: 6, marginTop: 12, padding: "6px 16px",
                  background: "rgba(15,23,42,0.6)", borderRadius: 20,
                }}>
                  {[stats.isKrwGood, stats.isDxyGood, stats.isGapGood, stats.isFairGood].map((g, i) => (
                    <span key={i} style={{
                      width: 10, height: 10, borderRadius: "50%",
                      background: g ? "#4ade80" : "#f87171",
                      boxShadow: `0 0 6px ${g ? "rgba(74,222,128,0.5)" : "rgba(248,113,113,0.5)"}`,
                    }} />
                  ))}
                  <span style={{ fontSize: 12, color: "#94a3b8", marginLeft: 4 }}>{stats.goodCount}/4</span>
                </div>
              </div>
            </div>

            {/* KRW Rate */}
            <div className="fade-in stagger-1" style={card}>
              <GaugeBar
                label="원달러 환율 (USD/KRW)"
                current={stats.krwCurrent} min={stats.krwMin} max={stats.krwMax}
                midpoint={stats.krwAvg} midLabel={`평균 ${stats.krwAvg.toFixed(2)}`}
                isGood={stats.isKrwGood}
              />
              <Sparkline data={stats.krwSparkline} color={stats.isKrwGood ? "#4ade80" : "#f87171"} />
              <div style={{ fontSize: 11, color: "#475569", marginTop: 4 }}>
                {stats.isKrwGood
                  ? "📉 기간 내 저점 부근 — 달러 매수 타이밍 양호"
                  : "📈 기간 내 고점 부근 — 달러가 비싼 구간"}
              </div>
            </div>

            {/* DXY */}
            <div className="fade-in stagger-2" style={card}>
              <GaugeBar
                label="달러 인덱스 (DXY)"
                current={stats.dxyCurrent} min={stats.dxyMin} max={stats.dxyMax}
                midpoint={stats.dxyAvg} midLabel={`평균 ${stats.dxyAvg.toFixed(2)}`}
                isGood={stats.isDxyGood}
              />
              <Sparkline data={stats.dxySparkline} color={stats.isDxyGood ? "#4ade80" : "#f87171"} />
              <div style={{ fontSize: 11, color: "#475569", marginTop: 4 }}>
                {stats.isDxyGood
                  ? "📉 달러지수 약세 구간 — 원화 대비 저평가 가능성"
                  : "📈 달러지수 강세 구간 — 추가 상승 여력 제한"}
              </div>
            </div>

            {/* Gap Ratio */}
            <div className="fade-in stagger-3" style={card}>
              <GaugeBar
                label="달러 갭 비율"
                current={stats.gapRatio} min={stats.gapMin} max={stats.gapMax}
                midpoint={stats.gapAvg} midLabel={`평균 ${stats.gapAvg.toFixed(2)}%`}
                isGood={stats.isGapGood} unit="%" decimals={2}
              />
              <div style={{ fontSize: 11, color: "#475569", marginTop: 4 }}>
                {stats.isGapGood
                  ? "✅ 갭이 평균 이하 — 적정가 대비 저평가"
                  : "⛔ 갭이 평균 이상 — 적정가 대비 고평가"}
              </div>
            </div>

            {/* Fair Rate */}
            <div className="fade-in stagger-4" style={card}>
              <GaugeBar
                label="적정 환율"
                current={stats.krwCurrent}
                min={Math.min(stats.fairRate, stats.krwMin)}
                max={Math.max(stats.fairRate * 1.05, stats.krwMax)}
                midpoint={stats.fairRate}
                midLabel={`적정 ${stats.fairRate.toFixed(2)}`}
                isGood={stats.isFairGood}
              />
              <div style={{
                display: "flex", justifyContent: "center", alignItems: "baseline", gap: 8,
                marginTop: 4, fontSize: 13, fontFamily: "'JetBrains Mono', monospace",
              }}>
                <span style={{ color: "#94a3b8" }}>현재</span>
                <span style={{ color: "#e2e8f0", fontWeight: 700, fontSize: 16 }}>{stats.krwCurrent.toFixed(2)}</span>
                <span style={{ color: "#475569" }}>vs</span>
                <span style={{ color: "#94a3b8" }}>적정</span>
                <span style={{ color: "#60a5fa", fontWeight: 700, fontSize: 16 }}>{stats.fairRate.toFixed(2)}</span>
                <span style={{
                  color: stats.isFairGood ? "#4ade80" : "#f87171", fontWeight: 600, fontSize: 12,
                  padding: "2px 8px", borderRadius: 6,
                  background: stats.isFairGood ? "rgba(74,222,128,0.1)" : "rgba(248,113,113,0.1)",
                }}>
                  {stats.gapRatio >= 0 ? "+" : ""}{stats.gapRatio.toFixed(2)}%
                </span>
              </div>
            </div>
          </div>
        )}

        {/* ══════════════ TAB: 적정환율 분석 ══════════════ */}
        {!loading && stats && tab === "fairrate" && (
          <div>
            {/* Summary cards */}
            <div className="fade-in" style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 12, marginBottom: 16 }}>
              {[
                { label: "현재 환율", value: stats.krwCurrent.toFixed(2), sub: "KRW/USD", color: "#f0abfc" },
                { label: "달러 인덱스", value: stats.dxyCurrent.toFixed(2), sub: "DXY", color: "#60a5fa" },
                { label: "적정 환율", value: stats.fairRate.toFixed(2), sub: "DXY 기반", color: "#4ade80" },
                {
                  label: "괴리율",
                  value: `${stats.gapRatio >= 0 ? "+" : ""}${stats.gapRatio.toFixed(2)}%`,
                  sub: stats.gapRatio > 0 ? "고평가" : "저평가",
                  color: stats.gapRatio > 0 ? "#f87171" : "#4ade80",
                },
              ].map((c, i) => (
                <div key={i} style={{
                  ...card, marginBottom: 0, padding: "16px 18px",
                  borderLeft: `3px solid ${c.color}`,
                }}>
                  <div style={{ fontSize: 11, color: "#64748b", fontWeight: 600, marginBottom: 4 }}>{c.label}</div>
                  <div style={{
                    fontSize: 22, fontWeight: 700, color: c.color,
                    fontFamily: "'JetBrains Mono', monospace", letterSpacing: "-0.02em",
                  }}>{c.value}</div>
                  <div style={{ fontSize: 10, color: "#475569", marginTop: 2 }}>{c.sub}</div>
                </div>
              ))}
            </div>

            {/* USD/KRW vs Fair Rate chart */}
            <div className="fade-in stagger-1" style={card}>
              <div style={{ fontSize: 14, fontWeight: 700, color: "#cbd5e1", marginBottom: 4 }}>원달러 환율 vs 적정환율</div>
              <div style={{ fontSize: 11, color: "#475569", marginBottom: 16 }}>
                적정환율 = 달러인덱스 × 기간 평균 환율/DXY 비율
              </div>
              <ResponsiveContainer width="100%" height={240}>
                <ComposedChart data={stats.chartData} margin={{ top: 8, right: 8, bottom: 4, left: -10 }}>
                  <XAxis dataKey="date" tick={{ fill: "#475569", fontSize: 10 }} interval="preserveStartEnd" tickLine={false} axisLine={{ stroke: "#1e293b" }} />
                  <YAxis tick={{ fill: "#475569", fontSize: 10 }} tickLine={false} axisLine={false} domain={["auto", "auto"]} />
                  <Tooltip content={<ChartTooltip />} />
                  <Area type="monotone" dataKey="fair" stroke="none" fill="rgba(96,165,250,0.08)" />
                  <Line type="monotone" dataKey="krw" stroke="#f0abfc" strokeWidth={2} dot={false} name="실제 환율" />
                  <Line type="monotone" dataKey="fair" stroke="#60a5fa" strokeWidth={1.5} strokeDasharray="6 3" dot={false} name="적정 환율" />
                </ComposedChart>
              </ResponsiveContainer>
              <div style={{ display: "flex", justifyContent: "center", gap: 20, marginTop: 8, fontSize: 11 }}>
                <span style={{ display: "flex", alignItems: "center", gap: 4 }}>
                  <span style={{ width: 16, height: 3, background: "#f0abfc", borderRadius: 2, display: "inline-block" }} />
                  <span style={{ color: "#94a3b8" }}>실제 환율</span>
                </span>
                <span style={{ display: "flex", alignItems: "center", gap: 4 }}>
                  <span style={{ width: 16, height: 3, background: "#60a5fa", borderRadius: 2, display: "inline-block", borderTop: "1px dashed #60a5fa" }} />
                  <span style={{ color: "#94a3b8" }}>적정 환율</span>
                </span>
              </div>
            </div>

            {/* Gap ratio chart */}
            <div className="fade-in stagger-2" style={card}>
              <div style={{ fontSize: 14, fontWeight: 700, color: "#cbd5e1", marginBottom: 4 }}>달러 갭 추이</div>
              <div style={{ fontSize: 11, color: "#475569", marginBottom: 16 }}>
                (실제환율 - 적정환율) / 적정환율 × 100
              </div>
              <ResponsiveContainer width="100%" height={180}>
                <ComposedChart data={stats.chartData} margin={{ top: 8, right: 8, bottom: 4, left: -10 }}>
                  <XAxis dataKey="date" tick={{ fill: "#475569", fontSize: 10 }} interval="preserveStartEnd" tickLine={false} axisLine={{ stroke: "#1e293b" }} />
                  <YAxis tick={{ fill: "#475569", fontSize: 10 }} tickLine={false} axisLine={false} />
                  <Tooltip content={<ChartTooltip />} />
                  <ReferenceLine y={0} stroke="#334155" strokeDasharray="3 3" />
                  <ReferenceLine y={stats.gapAvg} stroke="#fbbf24" strokeDasharray="4 4" label={{ value: "평균", fill: "#fbbf24", fontSize: 10, position: "right" }} />
                  <Area type="monotone" dataKey="gap" stroke="none" fill="rgba(248,113,113,0.1)" />
                  <Line type="monotone" dataKey="gap" stroke="#f87171" strokeWidth={1.5} dot={false} name="갭 비율 (%)" />
                </ComposedChart>
              </ResponsiveContainer>
            </div>

            {/* DXY chart */}
            <div className="fade-in stagger-3" style={card}>
              <div style={{ fontSize: 14, fontWeight: 700, color: "#cbd5e1", marginBottom: 4 }}>달러 인덱스 (DXY)</div>
              <div style={{ fontSize: 11, color: "#475569", marginBottom: 16 }}>
                {PERIODS.find(p => p.key === period)?.label} 추이
              </div>
              <ResponsiveContainer width="100%" height={160}>
                <ComposedChart data={stats.chartData} margin={{ top: 8, right: 8, bottom: 4, left: -10 }}>
                  <XAxis dataKey="date" tick={{ fill: "#475569", fontSize: 10 }} interval="preserveStartEnd" tickLine={false} axisLine={{ stroke: "#1e293b" }} />
                  <YAxis tick={{ fill: "#475569", fontSize: 10 }} tickLine={false} axisLine={false} domain={["auto", "auto"]} />
                  <Tooltip content={<ChartTooltip />} />
                  <Area type="monotone" dataKey="dxy" stroke="none" fill="rgba(96,165,250,0.08)" />
                  <Line type="monotone" dataKey="dxy" stroke="#60a5fa" strokeWidth={2} dot={false} name="DXY" />
                </ComposedChart>
              </ResponsiveContainer>
            </div>

            {/* Methodology */}
            <div className="fade-in stagger-4" style={{
              ...card, background: "rgba(15,23,42,0.6)", border: "1px solid rgba(51,65,85,0.2)",
            }}>
              <div style={{ fontSize: 13, fontWeight: 700, color: "#64748b", marginBottom: 8 }}>📊 산출 방법</div>
              <div style={{ fontSize: 12, color: "#475569", lineHeight: 1.8 }}>
                <b style={{ color: "#94a3b8" }}>적정환율</b> = 현재 DXY × (선택 기간 평균 USD-KRW ÷ 평균 DXY)<br />
                <b style={{ color: "#94a3b8" }}>갭 비율</b> = (실제환율 - 적정환율) ÷ 적정환율 × 100<br />
                <b style={{ color: "#94a3b8" }}>투자 적합성</b> = 환율·DXY 위치, 갭 비율, 적정환율 비교 4개 지표 중 3개 이상 충족 시 매수 적합
              </div>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
