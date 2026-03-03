import { useState, useCallback, useEffect } from "react";

const STYLES = `
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&family=DM+Mono:wght@400;500&display=swap');
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'Noto Sans KR', sans-serif; background: #0f0f11; color: #e8e8f0; min-height: 100vh; }
  .bg-grid {
    position: fixed; inset: 0; pointer-events: none; z-index: 0;
    background-image: linear-gradient(rgba(108,99,255,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(108,99,255,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
  }
  .wrapper { position: relative; z-index: 1; max-width: 860px; margin: 0 auto; padding: 40px 24px 80px; }
  header { display: flex; align-items: center; gap: 16px; margin-bottom: 48px; }
  .logo-mark {
    width: 44px; height: 44px; background: #6c63ff; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-family: 'DM Mono', monospace; font-weight: 500; font-size: 14px; color: white; flex-shrink: 0;
  }
  .header-text h1 { font-size: 18px; font-weight: 700; letter-spacing: -0.3px; }
  .header-text p  { font-size: 12px; color: #7a7a8c; margin-top: 2px; }
  .header-badge {
    margin-left: auto; background: rgba(108,99,255,0.12); border: 1px solid rgba(108,99,255,0.25);
    color: #a89fff; font-size: 11px; font-family: 'DM Mono', monospace; padding: 4px 10px; border-radius: 20px;
  }
  .upload-zone {
    border: 1.5px dashed #2e2e38; border-radius: 20px; padding: 52px 32px; text-align: center;
    cursor: pointer; transition: all 0.25s; background: #18181c; position: relative; overflow: hidden;
  }
  .upload-zone::before {
    content: ''; position: absolute; inset: 0; pointer-events: none;
    background: radial-gradient(ellipse at 50% 0%, rgba(108,99,255,0.06) 0%, transparent 70%);
  }
  .upload-zone.drag-over { border-color: #6c63ff; background: rgba(108,99,255,0.05); }
  .upload-icon { width: 52px; height: 52px; margin: 0 auto 20px; background: #222228; border-radius: 14px; display: flex; align-items: center; justify-content: center; font-size: 24px; }
  .upload-zone h2 { font-size: 16px; font-weight: 600; margin-bottom: 8px; }
  .upload-zone p  { font-size: 13px; color: #7a7a8c; line-height: 1.6; }
  .processing { margin-top: 32px; padding: 28px; background: #18181c; border: 1px solid #2e2e38; border-radius: 16px; display: flex; align-items: center; gap: 20px; }
  .spinner { width: 36px; height: 36px; border: 2.5px solid #2e2e38; border-top-color: #6c63ff; border-radius: 50%; animation: spin 0.8s linear infinite; flex-shrink: 0; }
  @keyframes spin { to { transform: rotate(360deg); } }
  .processing-text h3 { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
  .processing-text p  { font-size: 12px; color: #7a7a8c; }
  .result-card { margin-top: 32px; background: #1c1c22; border: 1px solid #2e2e38; border-radius: 20px; overflow: hidden; animation: fadeUp 0.4s ease; }
  @keyframes fadeUp { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }
  .card-header { padding: 24px 28px 20px; border-bottom: 1px solid #2e2e38; display: flex; align-items: flex-start; justify-content: space-between; gap: 16px; }
  .card-company { font-size: 11px; font-family: 'DM Mono', monospace; color: #6c63ff; letter-spacing: 0.5px; text-transform: uppercase; margin-bottom: 6px; }
  .card-title { font-size: 20px; font-weight: 700; letter-spacing: -0.4px; line-height: 1.3; }
  .card-meta { display: flex; gap: 8px; margin-top: 10px; flex-wrap: wrap; }
  .chip { display: inline-flex; align-items: center; gap: 4px; font-size: 11px; padding: 3px 10px; border-radius: 20px; font-weight: 500; }
  .chip-purple { background: rgba(108,99,255,0.15); color: #a89fff; }
  .chip-green  { background: rgba(6,214,160,0.12);  color: #06d6a0; }
  .chip-yellow { background: rgba(255,209,102,0.12); color: #ffd166; }
  .chip-red    { background: rgba(255,107,107,0.12); color: #ff6b6b; }
  .copy-btn {
    flex-shrink: 0; background: #222228; border: 1px solid #2e2e38; color: #7a7a8c;
    font-family: 'Noto Sans KR', sans-serif; font-size: 12px; padding: 8px 16px; border-radius: 10px;
    cursor: pointer; transition: all 0.2s; display: flex; align-items: center; gap: 6px; white-space: nowrap;
  }
  .copy-btn:hover { background: #6c63ff; border-color: #6c63ff; color: white; }
  .copy-btn.copied { background: #06d6a0; border-color: #06d6a0; color: white; }
  .section { padding: 22px 28px; border-bottom: 1px solid #2e2e38; display: grid; grid-template-columns: 140px 1fr; gap: 16px; align-items: start; }
  .section:last-child { border-bottom: none; }
  .section-label { display: flex; align-items: center; gap: 8px; font-size: 12px; font-weight: 600; color: #7a7a8c; letter-spacing: 0.2px; padding-top: 2px; }
  .section-icon { width: 26px; height: 26px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 13px; flex-shrink: 0; }
  .icon-blue   { background: rgba(108,99,255,0.15); }
  .icon-green  { background: rgba(6,214,160,0.12); }
  .icon-yellow { background: rgba(255,209,102,0.12); }
  .icon-red    { background: rgba(255,107,107,0.12); }
  .icon-orange { background: rgba(255,157,60,0.12); }
  .section-content { font-size: 14px; line-height: 1.75; color: #e8e8f0; }
  .schedule-table { width: 100%; border-collapse: collapse; font-size: 13px; }
  .schedule-table th { text-align: left; padding: 8px 12px; background: #222228; color: #7a7a8c; font-weight: 500; font-size: 11px; letter-spacing: 0.3px; }
  .schedule-table th:first-child { border-radius: 8px 0 0 8px; }
  .schedule-table th:last-child  { border-radius: 0 8px 8px 0; }
  .schedule-table td { padding: 10px 12px; border-bottom: 1px solid rgba(255,255,255,0.04); vertical-align: middle; }
  .schedule-table tr:last-child td { border-bottom: none; }
  .time-badge { font-family: 'DM Mono', monospace; font-size: 11px; background: #222228; padding: 2px 8px; border-radius: 6px; white-space: nowrap; }
  .instructor-tag { display: inline-block; background: rgba(108,99,255,0.15); color: #a89fff; font-size: 11px; padding: 2px 8px; border-radius: 6px; }
  .highlight-box { background: rgba(255,107,107,0.06); border: 1px solid rgba(255,107,107,0.2); border-radius: 10px; padding: 12px 16px; font-size: 13px; line-height: 1.7; white-space: pre-wrap; }
  .deadline-box  { background: rgba(255,157,60,0.06); border: 1px solid rgba(255,157,60,0.25); border-radius: 10px; padding: 12px 16px; font-size: 13px; line-height: 1.7; white-space: pre-wrap; }
  .error-box { margin-top: 24px; padding: 20px 24px; background: rgba(255,107,107,0.07); border: 1px solid rgba(255,107,107,0.2); border-radius: 14px; color: #ff9090; font-size: 13px; line-height: 1.6; }
  footer { text-align: center; margin-top: 60px; font-size: 11px; color: #7a7a8c; font-family: 'DM Mono', monospace; opacity: 0.5; }
  @media (max-width: 600px) {
    .section { grid-template-columns: 1fr; gap: 8px; }
    .card-header { flex-direction: column; }
    .copy-btn { width: 100%; justify-content: center; }
  }
`;

// PDF.js 동적 로드
function loadPDFJS() {
  return new Promise((resolve, reject) => {
    if (window.pdfjsLib) { resolve(window.pdfjsLib); return; }
    const script = document.createElement("script");
    script.src = "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js";
    script.onload = () => {
      const lib = window.pdfjsLib;
      if (lib) {
        lib.GlobalWorkerOptions.workerSrc =
          "https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js";
        resolve(lib);
      } else {
        reject(new Error("pdfjsLib not found after load"));
      }
    };
    script.onerror = () => reject(new Error("PDF.js 스크립트 로드 실패"));
    document.head.appendChild(script);
  });
}

async function extractTextFromPDF(file) {
  const pdfjsLib = await loadPDFJS();
  const arrayBuffer = await file.arrayBuffer();
  const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
  let fullText = "";
  for (let i = 1; i <= pdf.numPages; i++) {
    const page = await pdf.getPage(i);
    const tc = await page.getTextContent();
    fullText += tc.items.map(item => item.str).join(" ") + "\n";
  }
  return fullText;
}

async function analyzeWithClaude(pdfText) {
  const prompt = `당신은 PSI컨설팅의 강의정보카드를 분석하는 전문 어시스턴트입니다.

아래 텍스트는 PSI컨설팅 강의정보카드에서 추출한 내용입니다.
강사 관점에서 가장 중요한 정보를 추출하여 JSON으로 정리해주세요.

중요 규칙:
1. 여러 필드에 분산된 정보를 의미 기반으로 통합 (교육목표/교육개요/기타정보 등)
2. 없는 정보는 "미기재"
3. schedule은 날짜별 배열
4. 교재 제작 기한: 교재요청 내용, 교재/배송 정보에서 교재 제출 마감일을 찾아서 정리. 여러 건이면 모두 포함. 없으면 "미기재"
5. notes에는 학습자 성향, 교육 운영 방식, 담당자 요청사항 중 강사가 꼭 알아야 할 것만

반드시 JSON만 응답 (마크다운 코드블록 없이 순수 JSON):

{
  "company": "고객사명",
  "title": "교육명",
  "instructor": "강사명(쉼표 구분)",
  "total_hours": "총 강의시간 숫자만",
  "headcount": "교육인원 숫자만",
  "location_short": "장소 짧게",
  "location_full": "장소 전체 주소",
  "schedule": [
    {"date": "날짜", "time": "시작~종료", "hours": "시간 숫자", "instructor": "강사"}
  ],
  "purpose": "교육 목적과 배경 통합 (2~4문장. 왜 이 교육을 하는지, 어떤 맥락인지)",
  "audience": "대상자 특성 (직급, 특징, 강사가 알아야 할 정보)",
  "notes": "특이사항 (학습자 성향, 담당자 요청, 운영 관련 주의사항. 없으면 '특별한 사항 없음')",
  "material_deadline": "교재 제출 기한 (예: '9월 1일까지 / 교재 도착 희망: 2025.09.05'. 없으면 '미기재')"
}

강의정보카드 텍스트:
${pdfText}`;

  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      model: "claude-sonnet-4-20250514",
      max_tokens: 1000,
      messages: [{ role: "user", content: prompt }],
    }),
  });

  if (!response.ok) {
    const err = await response.json().catch(() => ({}));
    throw new Error(err?.error?.message || `API 오류 (${response.status})`);
  }

  const data = await response.json();
  const raw = data.content.map(i => i.text || "").join("");
  const clean = raw.replace(/```json|```/g, "").trim();
  return JSON.parse(clean);
}

export default function App() {
  const [state, setState] = useState("idle");
  const [result, setResult] = useState(null);
  const [error, setError] = useState("");
  const [dragging, setDragging] = useState(false);
  const [copied, setCopied] = useState(false);
  const [step, setStep] = useState("");

  const processFile = useCallback(async (file) => {
    if (!file || file.type !== "application/pdf") {
      setError("PDF 파일만 업로드할 수 있습니다.");
      setState("error");
      return;
    }
    setState("processing");
    setError("");
    setResult(null);
    try {
      setStep("PDF 텍스트 추출 중...");
      const text = await extractTextFromPDF(file);
      setStep("AI가 핵심 정보를 분석 중...");
      const parsed = await analyzeWithClaude(text);
      setResult(parsed);
      setState("done");
    } catch (e) {
      setError(e.message);
      setState("error");
    }
  }, []);

  const handleDrop = useCallback((e) => {
    e.preventDefault();
    setDragging(false);
    const file = e.dataTransfer.files[0];
    if (file) processFile(file);
  }, [processFile]);

  const copyText = () => {
    if (!result) return;
    const sched = (result.schedule || [])
      .map(s => `  ${s.date} | ${s.time} | ${s.hours}H | ${s.instructor}`)
      .join("\n");
    const text = `[${result.company}] ${result.title}
${"=".repeat(44)}
📅 강사 스케줄
${sched}
장소: ${result.location_full || result.location_short || "—"}

🎯 교육 목적·배경
${result.purpose}

👥 대상자 특성
${result.audience}

⚠️ 특이사항
${result.notes}

📦 교재 제출 기한
${result.material_deadline}`;
    navigator.clipboard.writeText(text).then(() => {
      setCopied(true);
      setTimeout(() => setCopied(false), 2000);
    });
  };

  const muted = { color: "#7a7a8c" };

  return (
    <>
      <style>{STYLES}</style>
      <div className="bg-grid" />
      <div className="wrapper">

        <header>
          <div className="logo-mark">PSI</div>
          <div className="header-text">
            <h1>강의정보 요약 시스템</h1>
            <p>강의정보카드 PDF → 핵심 요약 카드</p>
          </div>
          <div className="header-badge">AI Powered</div>
        </header>

        {/* Upload */}
        <div
          className={`upload-zone${dragging ? " drag-over" : ""}`}
          onDragOver={e => { e.preventDefault(); setDragging(true); }}
          onDragLeave={() => setDragging(false)}
          onDrop={handleDrop}
        >
          <input
            type="file" accept=".pdf"
            onChange={e => { if (e.target.files[0]) processFile(e.target.files[0]); e.target.value = ""; }}
            style={{ position: "absolute", inset: 0, opacity: 0, cursor: "pointer", width: "100%", height: "100%" }}
          />
          <div className="upload-icon">📄</div>
          <h2>강의정보카드 PDF를 업로드하세요</h2>
          <p>파일을 여기에 드래그하거나 클릭하여 선택<br />PSI 강의정보카드 형식을 자동으로 분석합니다</p>
        </div>

        {state === "processing" && (
          <div className="processing">
            <div className="spinner" />
            <div className="processing-text">
              <h3>AI가 강의정보를 분석 중입니다...</h3>
              <p>{step}</p>
            </div>
          </div>
        )}

        {state === "error" && (
          <div className="error-box">⚠️ {error}</div>
        )}

        {state === "done" && result && (
          <div className="result-card">
            <div className="card-header">
              <div>
                <div className="card-company">{result.company}</div>
                <div className="card-title">{result.title}</div>
                <div className="card-meta">
                  {result.headcount && <span className="chip chip-green">👥 {result.headcount}명</span>}
                  {result.total_hours && <span className="chip chip-purple">⏱ {result.total_hours}H</span>}
                  {result.instructor && <span className="chip chip-yellow">🎤 {result.instructor}</span>}
                  {result.location_short && <span className="chip chip-red">📍 {result.location_short}</span>}
                </div>
              </div>
              <button className={`copy-btn${copied ? " copied" : ""}`} onClick={copyText}>
                {copied ? "✅ 복사 완료!" : "📋 텍스트 복사"}
              </button>
            </div>

            {/* 일시·장소 */}
            <div className="section">
              <div className="section-label">
                <div className="section-icon icon-blue">📅</div>일시 · 장소
              </div>
              <div className="section-content">
                <table className="schedule-table">
                  <thead><tr><th>날짜</th><th>시간</th><th>강의시간</th><th>강사</th></tr></thead>
                  <tbody>
                    {(result.schedule || []).map((s, i) => (
                      <tr key={i}>
                        <td>{s.date}</td>
                        <td><span className="time-badge">{s.time}</span></td>
                        <td>{s.hours}H</td>
                        <td><span className="instructor-tag">{s.instructor}</span></td>
                      </tr>
                    ))}
                  </tbody>
                </table>
                {result.location_full && (
                  <div style={{ marginTop: 10, fontSize: 12, ...muted }}>📍 {result.location_full}</div>
                )}
              </div>
            </div>

            {/* 목적·배경 */}
            <div className="section">
              <div className="section-label">
                <div className="section-icon icon-yellow">🎯</div>교육 목적·배경
              </div>
              <div className="section-content">{result.purpose || "미기재"}</div>
            </div>

            {/* 대상자 */}
            <div className="section">
              <div className="section-label">
                <div className="section-icon icon-green">👥</div>대상자 특성
              </div>
              <div className="section-content">{result.audience || "미기재"}</div>
            </div>

            {/* 특이사항 */}
            <div className="section">
              <div className="section-label">
                <div className="section-icon icon-red">⚠️</div>특이사항
              </div>
              <div className="section-content">
                {result.notes && result.notes !== "특별한 사항 없음" && result.notes !== "미기재"
                  ? <div className="highlight-box">{result.notes}</div>
                  : <span style={muted}>{result.notes || "특별한 사항 없음"}</span>
                }
              </div>
            </div>

            {/* 교재 기한 */}
            <div className="section">
              <div className="section-label">
                <div className="section-icon icon-orange">📦</div>교재 제출 기한
              </div>
              <div className="section-content">
                {result.material_deadline && result.material_deadline !== "미기재"
                  ? <div className="deadline-box">{result.material_deadline}</div>
                  : <span style={muted}>미기재</span>
                }
              </div>
            </div>

          </div>
        )}

        <footer>PSI 강의정보 요약 시스템 · Powered by Claude AI</footer>
      </div>
    </>
  );
}
