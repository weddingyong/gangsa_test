<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PSI 강의정보 요약 시스템</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&family=DM+Mono:wght@400;500&display=swap');

  :root {
    --bg: #0f0f11;
    --surface: #18181c;
    --surface2: #222228;
    --border: #2e2e38;
    --accent: #6c63ff;
    --accent2: #ff6b6b;
    --accent3: #ffd166;
    --text: #e8e8f0;
    --text-muted: #7a7a8c;
    --green: #06d6a0;
    --card-bg: #1c1c22;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Noto Sans KR', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Background grid */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: 
      linear-gradient(rgba(108,99,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(108,99,255,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 40px 24px 80px;
  }

  /* Header */
  header {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 48px;
  }

  .logo-mark {
    width: 44px;
    height: 44px;
    background: var(--accent);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'DM Mono', monospace;
    font-weight: 500;
    font-size: 14px;
    color: white;
    letter-spacing: -0.5px;
    flex-shrink: 0;
  }

  .header-text h1 {
    font-size: 18px;
    font-weight: 700;
    letter-spacing: -0.3px;
    color: var(--text);
  }

  .header-text p {
    font-size: 12px;
    color: var(--text-muted);
    margin-top: 2px;
  }

  .header-badge {
    margin-left: auto;
    background: rgba(108,99,255,0.12);
    border: 1px solid rgba(108,99,255,0.25);
    color: #a89fff;
    font-size: 11px;
    font-family: 'DM Mono', monospace;
    padding: 4px 10px;
    border-radius: 20px;
  }

  /* Upload Zone */
  .upload-zone {
    border: 1.5px dashed var(--border);
    border-radius: 20px;
    padding: 52px 32px;
    text-align: center;
    cursor: pointer;
    transition: all 0.25s;
    background: var(--surface);
    position: relative;
    overflow: hidden;
  }

  .upload-zone::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 50% 0%, rgba(108,99,255,0.06) 0%, transparent 70%);
    pointer-events: none;
  }

  .upload-zone:hover, .upload-zone.drag-over {
    border-color: var(--accent);
    background: rgba(108,99,255,0.05);
  }

  .upload-icon {
    width: 52px;
    height: 52px;
    margin: 0 auto 20px;
    background: var(--surface2);
    border-radius: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
  }

  .upload-zone h2 {
    font-size: 16px;
    font-weight: 600;
    margin-bottom: 8px;
  }

  .upload-zone p {
    font-size: 13px;
    color: var(--text-muted);
    line-height: 1.6;
  }

  .upload-zone input[type="file"] {
    position: absolute;
    inset: 0;
    opacity: 0;
    cursor: pointer;
    width: 100%;
    height: 100%;
  }

  /* Processing state */
  .processing {
    margin-top: 32px;
    padding: 28px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    display: none;
    align-items: center;
    gap: 20px;
  }

  .processing.show { display: flex; }

  .spinner {
    width: 36px;
    height: 36px;
    border: 2.5px solid var(--border);
    border-top-color: var(--accent);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
    flex-shrink: 0;
  }

  @keyframes spin { to { transform: rotate(360deg); } }

  .processing-text h3 { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
  .processing-text p { font-size: 12px; color: var(--text-muted); }

  /* Result Card */
  .result-card {
    margin-top: 32px;
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 20px;
    overflow: hidden;
    display: none;
    animation: fadeUp 0.4s ease;
  }

  .result-card.show { display: block; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* Card Header */
  .card-header {
    padding: 24px 28px 20px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    gap: 16px;
  }

  .card-title-area {}

  .card-company {
    font-size: 11px;
    font-family: 'DM Mono', monospace;
    color: var(--accent);
    letter-spacing: 0.5px;
    text-transform: uppercase;
    margin-bottom: 6px;
  }

  .card-title {
    font-size: 20px;
    font-weight: 700;
    letter-spacing: -0.4px;
    line-height: 1.3;
  }

  .card-meta {
    display: flex;
    gap: 8px;
    margin-top: 10px;
    flex-wrap: wrap;
  }

  .chip {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 20px;
    font-weight: 500;
  }

  .chip-purple { background: rgba(108,99,255,0.15); color: #a89fff; }
  .chip-green  { background: rgba(6,214,160,0.12);  color: var(--green); }
  .chip-yellow { background: rgba(255,209,102,0.12); color: var(--accent3); }
  .chip-red    { background: rgba(255,107,107,0.12); color: var(--accent2); }

  .copy-btn {
    flex-shrink: 0;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--text-muted);
    font-family: 'Noto Sans KR', sans-serif;
    font-size: 12px;
    padding: 8px 16px;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    gap: 6px;
    white-space: nowrap;
  }

  .copy-btn:hover {
    background: var(--accent);
    border-color: var(--accent);
    color: white;
  }

  /* Sections */
  .card-body {
    padding: 0;
  }

  .section {
    padding: 22px 28px;
    border-bottom: 1px solid var(--border);
    display: grid;
    grid-template-columns: 140px 1fr;
    gap: 16px;
    align-items: start;
  }

  .section:last-child {
    border-bottom: none;
  }

  .section-label {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    font-weight: 600;
    color: var(--text-muted);
    letter-spacing: 0.2px;
    padding-top: 2px;
  }

  .section-icon {
    width: 26px;
    height: 26px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 13px;
    flex-shrink: 0;
  }

  .icon-blue   { background: rgba(108,99,255,0.15); }
  .icon-green  { background: rgba(6,214,160,0.12); }
  .icon-yellow { background: rgba(255,209,102,0.12); }
  .icon-red    { background: rgba(255,107,107,0.12); }

  .section-content {
    font-size: 14px;
    line-height: 1.75;
    color: var(--text);
  }

  /* Schedule table */
  .schedule-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 13px;
  }

  .schedule-table th {
    text-align: left;
    padding: 8px 12px;
    background: var(--surface2);
    color: var(--text-muted);
    font-weight: 500;
    font-size: 11px;
    letter-spacing: 0.3px;
  }

  .schedule-table th:first-child { border-radius: 8px 0 0 8px; }
  .schedule-table th:last-child  { border-radius: 0 8px 8px 0; }

  .schedule-table td {
    padding: 10px 12px;
    border-bottom: 1px solid rgba(255,255,255,0.04);
    vertical-align: middle;
  }

  .schedule-table tr:last-child td { border-bottom: none; }

  .time-badge {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    background: var(--surface2);
    padding: 2px 8px;
    border-radius: 6px;
    white-space: nowrap;
  }

  .instructor-tag {
    display: inline-block;
    background: rgba(108,99,255,0.15);
    color: #a89fff;
    font-size: 11px;
    padding: 2px 8px;
    border-radius: 6px;
  }

  /* Highlight box */
  .highlight-box {
    background: rgba(255,107,107,0.06);
    border: 1px solid rgba(255,107,107,0.2);
    border-radius: 10px;
    padding: 12px 16px;
    font-size: 13px;
    line-height: 1.7;
  }

  /* Error state */
  .error-box {
    margin-top: 24px;
    padding: 20px 24px;
    background: rgba(255,107,107,0.07);
    border: 1px solid rgba(255,107,107,0.2);
    border-radius: 14px;
    display: none;
    color: #ff9090;
    font-size: 13px;
    line-height: 1.6;
  }

  .error-box.show { display: block; }

  /* Footer */
  footer {
    text-align: center;
    margin-top: 60px;
    font-size: 11px;
    color: var(--text-muted);
    font-family: 'DM Mono', monospace;
    opacity: 0.5;
  }

  /* Textbook deadline highlight */
  .deadline-box {
    background: rgba(255, 209, 102, 0.07);
    border: 1px solid rgba(255, 209, 102, 0.25);
    border-radius: 10px;
    padding: 14px 16px;
    font-size: 13px;
    line-height: 1.8;
  }

  .deadline-row {
    display: flex;
    align-items: baseline;
    gap: 10px;
    padding: 4px 0;
  }

  .deadline-date {
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    font-weight: 500;
    color: var(--accent3);
    white-space: nowrap;
  }

  .deadline-label {
    font-size: 12px;
    color: var(--text-muted);
  }

  #sectionTextbook .section-label {
    color: var(--accent3);
  }
  @media (max-width: 600px) {
    .section {
      grid-template-columns: 1fr;
      gap: 8px;
    }
    .card-header {
      flex-direction: column;
    }
    .copy-btn {
      width: 100%;
      justify-content: center;
    }
  }
</style>
</head>
<body>

<div class="wrapper">

  <header>
    <div class="logo-mark">PSI</div>
    <div class="header-text">
      <h1>강의정보 요약 시스템</h1>
      <p>강의정보카드 PDF → 핵심 요약 카드</p>
    </div>
    <div class="header-badge">AI Powered</div>
  </header>

  <div class="upload-zone" id="uploadZone">
    <input type="file" id="fileInput" accept=".pdf" />
    <div class="upload-icon">📄</div>
    <h2>강의정보카드 PDF를 업로드하세요</h2>
    <p>파일을 여기에 드래그하거나 클릭하여 선택<br>PSI 강의정보카드 형식을 자동으로 분석합니다</p>
  </div>

  <div class="processing" id="processing">
    <div class="spinner"></div>
    <div class="processing-text">
      <h3>AI가 강의정보를 분석 중입니다...</h3>
      <p>PDF 텍스트 추출 및 핵심 정보 정리 중</p>
    </div>
  </div>

  <div class="error-box" id="errorBox"></div>

  <div class="result-card" id="resultCard">
    <div class="card-header">
      <div class="card-title-area">
        <div class="card-company" id="resCompany">—</div>
        <div class="card-title" id="resTitle">—</div>
        <div class="card-meta" id="resMeta"></div>
      </div>
      <button class="copy-btn" onclick="copyResult()">
        <span>📋</span> 텍스트 복사
      </button>
    </div>

    <div class="card-body">

      <div class="section">
        <div class="section-label">
          <div class="section-icon icon-blue">📅</div>
          일시 · 장소
        </div>
        <div class="section-content" id="resSchedule">—</div>
      </div>

      <div class="section">
        <div class="section-label">
          <div class="section-icon icon-yellow">🎯</div>
          교육 목적 · 배경
        </div>
        <div class="section-content" id="resPurpose">—</div>
      </div>

      <div class="section">
        <div class="section-label">
          <div class="section-icon icon-green">👥</div>
          대상자 특성
        </div>
        <div class="section-content" id="resAudience">—</div>
      </div>

      <div class="section" id="sectionTextbook" style="display:none">
        <div class="section-label">
          <div class="section-icon icon-red">📚</div>
          교재 제작
        </div>
        <div class="section-content" id="resTextbook">—</div>
      </div>

      <div class="section" id="sectionTextbook">
        <div class="section-label">
          <div class="section-icon icon-orange">📚</div>
          교재 제작 마감
        </div>
        <div class="section-content" id="resTextbook">—</div>
      </div>

      <div class="section">
        <div class="section-label">
          <div class="section-icon icon-red">⚠️</div>
          특이사항
        </div>
        <div class="section-content" id="resNotes">—</div>
      </div>

    </div>
  </div>

  <footer>PSI 강의정보 요약 시스템 · Powered by Claude AI</footer>

</div>

<script>
pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

const fileInput = document.getElementById('fileInput');
const uploadZone = document.getElementById('uploadZone');
const processing = document.getElementById('processing');
const resultCard = document.getElementById('resultCard');
const errorBox = document.getElementById('errorBox');

// Drag & drop
uploadZone.addEventListener('dragover', e => { e.preventDefault(); uploadZone.classList.add('drag-over'); });
uploadZone.addEventListener('dragleave', () => uploadZone.classList.remove('drag-over'));
uploadZone.addEventListener('drop', e => {
  e.preventDefault();
  uploadZone.classList.remove('drag-over');
  const file = e.dataTransfer.files[0];
  if (file && file.type === 'application/pdf') processFile(file);
});

fileInput.addEventListener('change', e => {
  const file = e.target.files[0];
  if (file) processFile(file);
});

async function extractTextFromPDF(file) {
  const arrayBuffer = await file.arrayBuffer();
  const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
  let fullText = '';
  for (let i = 1; i <= pdf.numPages; i++) {
    const page = await pdf.getPage(i);
    const textContent = await page.getTextContent();
    const pageText = textContent.items.map(item => item.str).join(' ');
    fullText += pageText + '\n';
  }
  return fullText;
}

async function processFile(file) {
  // Reset
  resultCard.classList.remove('show');
  errorBox.classList.remove('show');
  processing.classList.add('show');

  try {
    const pdfText = await extractTextFromPDF(file);

    const prompt = `당신은 PSI컨설팅의 강의정보카드를 분석하는 전문 어시스턴트입니다.

아래는 PSI컨설팅의 강의정보카드에서 추출한 텍스트입니다. 이 정보를 분석하여 강사가 강의 준비 시 가장 중요한 정보를 JSON 형태로 정리해주세요.

중요한 규칙:
1. 여러 필드에 분산된 정보를 의미 기반으로 통합해주세요 (예: 교육목표/교육개요/기타정보에 분산된 목적/배경 정보를 하나로 통합)
2. 각 항목은 강사 관점에서 실용적으로 작성해주세요
3. 없는 정보는 "미기재"로 표시하세요
4. 특이사항에는 강의 운영 시 반드시 알아야 할 내용을 담아주세요 (학습자 성향, 주의사항, 담당자 요청사항 등)
5. schedule은 날짜별 배열로 구성하세요

반드시 아래 JSON 형식으로만 응답하세요. 다른 텍스트나 마크다운 없이 JSON만:

{
  "company": "고객사명",
  "title": "교육명",
  "instructor": "강사명 (여러 명이면 쉼표로)",
  "total_hours": "총 강의시간",
  "headcount": "교육인원 명",
  "location_short": "교육 장소 (짧게)",
  "schedule": [
    {"date": "날짜", "time": "시작~종료", "hours": "시간", "instructor": "강사"}
  ],
  "location_full": "교육 장소 전체 주소 포함",
  "purpose": "교육 목적과 배경을 통합 정리 (교육목표, 교육개요, 기타정보 등을 종합하여 왜 이 교육을 하는지, 어떤 배경인지 2~4문장으로)",
  "audience": "대상자 특성 (직급, 연차, 특징 등 강사가 알아야 할 정보)",
  "notes": "특이사항 (학습자 성향, 담당자 요청, 운영 관련 주의사항 등 강사가 꼭 알아야 할 내용. 없으면 '특별한 사항 없음')",
  "textbook": [
    {"deadline": "YYYY.MM.DD", "instructor": "강사명 또는 '전체'", "note": "교재 관련 안내사항 (제본방식, 수량, 특이사항 등)"}
  ]
}

textbook 배열: 교재요청 내용, 교재요청 기타, 교재/배송 정보에서 마감일과 강사별 안내를 추출하세요. 교재 관련 내용이 없으면 빈 배열 []로 두세요.

강의정보카드 텍스트:
${pdfText}`;

    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{ role: 'user', content: prompt }]
      })
    });

    const data = await response.json();
    const rawText = data.content.map(i => i.text || '').join('');
    const clean = rawText.replace(/```json|```/g, '').trim();
    const parsed = JSON.parse(clean);

    renderResult(parsed);

  } catch (err) {
    console.error(err);
    errorBox.textContent = '분석 중 오류가 발생했습니다. PDF 형식을 확인하거나 다시 시도해주세요. (' + err.message + ')';
    errorBox.classList.add('show');
  } finally {
    processing.classList.remove('show');
    fileInput.value = '';
  }
}

function renderResult(d) {
  // Header
  document.getElementById('resCompany').textContent = d.company || '—';
  document.getElementById('resTitle').textContent = d.title || '—';

  // Chips
  const meta = document.getElementById('resMeta');
  meta.innerHTML = '';
  if (d.headcount) meta.innerHTML += `<span class="chip chip-green">👥 ${d.headcount}</span>`;
  if (d.total_hours) meta.innerHTML += `<span class="chip chip-purple">⏱ ${d.total_hours}H</span>`;
  if (d.instructor) meta.innerHTML += `<span class="chip chip-yellow">🎤 ${d.instructor}</span>`;
  if (d.location_short) meta.innerHTML += `<span class="chip chip-red">📍 ${d.location_short}</span>`;

  // Schedule
  const schedEl = document.getElementById('resSchedule');
  if (d.schedule && d.schedule.length > 0) {
    let html = `<table class="schedule-table">
      <thead><tr>
        <th>날짜</th><th>시간</th><th>강의시간</th><th>강사</th>
      </tr></thead><tbody>`;
    d.schedule.forEach(s => {
      html += `<tr>
        <td>${s.date || '—'}</td>
        <td><span class="time-badge">${s.time || '—'}</span></td>
        <td>${s.hours ? s.hours + 'H' : '—'}</td>
        <td><span class="instructor-tag">${s.instructor || '—'}</span></td>
      </tr>`;
    });
    html += '</tbody></table>';
    if (d.location_full) html += `<div style="margin-top:10px;font-size:12px;color:var(--text-muted)">📍 ${d.location_full}</div>`;
    schedEl.innerHTML = html;
  } else {
    schedEl.textContent = d.location_full || '—';
  }

  // Purpose
  document.getElementById('resPurpose').textContent = d.purpose || '미기재';

  // Audience
  document.getElementById('resAudience').textContent = d.audience || '미기재';

  // Textbook
  const tbSection = document.getElementById('sectionTextbook');
  const tbEl = document.getElementById('resTextbook');
  if (d.textbook && d.textbook.length > 0) {
    let html = '<div class="deadline-box">';
    d.textbook.forEach(tb => {
      html += `<div class="deadline-row">
        <span class="deadline-date">📅 ${tb.deadline || '—'} 까지</span>
        <span style="font-size:13px;color:var(--text)">${tb.instructor ? `[${tb.instructor}]` : ''} ${tb.note || ''}</span>
      </div>`;
    });
    html += '</div>';
    tbEl.innerHTML = html;
    tbSection.style.display = 'grid';
  } else {
    tbSection.style.display = 'none';
  }

  // Notes
  const notesEl = document.getElementById('resNotes');
  const notesText = d.notes || '특별한 사항 없음';
  if (notesText !== '특별한 사항 없음' && notesText !== '미기재') {
    notesEl.innerHTML = `<div class="highlight-box">${notesText.replace(/\n/g, '<br>')}</div>`;
  } else {
    notesEl.textContent = notesText;
  }

  resultCard.classList.add('show');
}

function copyResult() {
  const company = document.getElementById('resCompany').textContent;
  const title = document.getElementById('resTitle').textContent;
  const purpose = document.getElementById('resPurpose').textContent;
  const audience = document.getElementById('resAudience').textContent;
  const notes = document.getElementById('resNotes').textContent;

  // Schedule text
  const rows = document.querySelectorAll('.schedule-table tbody tr');
  let schedText = '';
  rows.forEach(row => {
    const cells = row.querySelectorAll('td');
    if (cells.length >= 4) {
      schedText += `  ${cells[0].textContent} | ${cells[1].textContent} | ${cells[2].textContent} | ${cells[3].textContent}\n`;
    }
  });

  // Textbook copy
  let tbText = '';
  document.querySelectorAll('.deadline-row').forEach(row => {
    tbText += '  ' + row.textContent.trim().replace(/\s+/g, ' ') + '\n';
  });

  const text = `[${company}] ${title}
${'='.repeat(40)}
📅 강사 스케줄
${schedText}${tbText ? `📚 교재 제작 마감\n${tbText}\n` : ''}
🎯 교육 목적·배경
${purpose}

👥 대상자 특성
${audience}

⚠️ 특이사항
${notes}`;

  navigator.clipboard.writeText(text).then(() => {
    const btn = document.querySelector('.copy-btn');
    btn.innerHTML = '<span>✅</span> 복사 완료!';
    setTimeout(() => { btn.innerHTML = '<span>📋</span> 텍스트 복사'; }, 2000);
  });
}
</script>
</body>
</html>
