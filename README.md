<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#10131d">
  <title>TrustAI — Kiểm chứng thông tin</title>
  <style>
    :root {
      color-scheme: dark;
      --bg: #0c0f17;
      --panel: #141925;
      --panel-2: #191f2d;
      --line: #2a3244;
      --text: #f3f5fb;
      --muted: #9da8bd;
      --accent: #a7f3d0;
      --accent-2: #5eead4;
      --warn: #fbbf24;
      --bad: #fb7185;
      --radius: 18px;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0; min-height: 100vh; color: var(--text);
      background: radial-gradient(ellipse at top left, #17283a 0, transparent 42%), var(--bg);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      line-height: 1.55;
    }
    button, textarea { font: inherit; }
    button { cursor: pointer; }
    a { color: inherit; }
    .shell { width: min(1120px, calc(100% - 32px)); margin: 0 auto; }
    .topbar { display:flex; align-items:center; justify-content:space-between; padding: 24px 0; gap: 16px; }
    .brand { display:flex; align-items:center; gap: 11px; font-weight: 800; letter-spacing: -.04em; font-size: 1.25rem; }
    .brand-mark { display:grid; place-items:center; width:40px; height:40px; border-radius:13px; color:#0b1720; background:linear-gradient(135deg,#a7f3d0,#67e8f9); font-weight:900; }
    .top-note { color:var(--muted); font-size:.85rem; }
    .hero { padding: 44px 0 30px; max-width: 800px; }
    .eyebrow { display:inline-flex; align-items:center; gap:8px; color:var(--accent); border:1px solid #28594f; background:#112b2b88; padding:7px 11px; border-radius:999px; font-size:.78rem; font-weight:750; letter-spacing:.08em; text-transform:uppercase; }
    h1 { margin:20px 0 14px; font-size:clamp(2.25rem, 6vw, 4.5rem); line-height:1.03; letter-spacing:-.065em; }
    h1 span { color:var(--accent); }
    .lead { max-width:660px; color:var(--muted); font-size:1.08rem; }
    .panel { border:1px solid var(--line); background:linear-gradient(145deg,#171d2aee,#111621f2); border-radius:var(--radius); padding:clamp(18px, 3vw, 28px); box-shadow:0 22px 65px #0002; }
    .panel-heading { display:flex; justify-content:space-between; align-items:center; gap:12px; margin-bottom:15px; }
    .panel-heading h2 { font-size:1rem; margin:0; }
    .subtle { color:var(--muted); font-size:.85rem; }
    textarea { width:100%; min-height:150px; resize:vertical; border:1px solid #354057; border-radius:13px; background:#0d121d; color:var(--text); padding:16px; outline:none; transition:border .2s, box-shadow .2s; }
    textarea:focus { border-color:var(--accent-2); box-shadow:0 0 0 3px #5eead422; }
    .form-foot { display:flex; justify-content:space-between; align-items:center; gap:14px; flex-wrap:wrap; margin-top:13px; }
    .char-count { color:var(--muted); font-size:.82rem; }
    .primary { border:0; border-radius:12px; padding:12px 18px; font-weight:800; color:#071a18; background:linear-gradient(135deg,var(--accent),#67e8f9); box-shadow:0 7px 24px #5eead422; }
    .primary:hover { filter:brightness(1.06); transform:translateY(-1px); }
    .samples { display:flex; gap:8px; flex-wrap:wrap; margin-top:18px; align-items:center; }
    .sample-chip { color:#dce5f4; border:1px solid var(--line); border-radius:999px; background:#1b2231; padding:7px 11px; font-size:.8rem; }
    .sample-chip:hover { border-color:#668c92; }
    .notice { display:flex; gap:10px; color:var(--muted); font-size:.84rem; margin:16px 2px 0; }
    .notice strong { color:#d8e2ef; }
    .section-title { display:flex; align-items:center; justify-content:space-between; gap:12px; margin:38px 0 14px; }
    .section-title h2 { font-size:1.15rem; margin:0; letter-spacing:-.025em; }
    .count-pill { border:1px solid var(--line); color:var(--muted); border-radius:999px; padding:4px 9px; font-size:.78rem; }
    .history-list { display:grid; gap:8px; }
    .empty-state { display:flex; gap:14px; align-items:center; border:1px dashed #30394b; border-radius:14px; padding:20px; color:var(--muted); }
    .empty-state strong { color:var(--text); }
    .empty-state p { margin:4px 0 0; font-size:.88rem; }
    .empty-icon { font-size:1.4rem; }
    .history-item { display:flex; justify-content:space-between; align-items:center; gap:12px; padding:14px 16px; border:1px solid var(--line); background:#121824; border-radius:13px; }
    .history-item-content { min-width:0; cursor:pointer; flex:1; }
    .history-item-content strong { display:block; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; font-size:.92rem; }
    .history-item-content span { color:var(--muted); font-size:.78rem; }
    .history-status { white-space:nowrap; color:#fcd34d; background:#3c2d12; border-radius:999px; padding:5px 9px; font-size:.73rem; font-weight:750; }
    .history-status.good { color:#a7f3d0; background:#12362f; }
    .history-status.caution { color:#fda4af; background:#411d2b; }
    .text-button { color:var(--muted); background:transparent; border:1px solid var(--line); border-radius:9px; padding:6px 10px; font-size:.8rem; }
    .text-button:hover { color:var(--text); border-color:#5a657a; }
    footer { padding:40px 0 28px; color:var(--muted); font-size:.8rem; display:flex; justify-content:space-between; gap:12px; flex-wrap:wrap; }
    dialog { width:min(900px, calc(100% - 24px)); max-height:88vh; overflow:auto; border:1px solid #384258; border-radius:22px; padding:0; background:#111722; color:var(--text); box-shadow:0 30px 100px #000a; }
    dialog::backdrop { background:#03060bc9; backdrop-filter:blur(7px); }
    .dialog-head { display:flex; justify-content:space-between; align-items:center; gap:12px; padding:18px 22px; border-bottom:1px solid var(--line); position:sticky; top:0; background:#111722ee; backdrop-filter:blur(10px); z-index:2; }
    .dialog-head h2 { font-size:1rem; margin:0; }
    .close-button { border:1px solid var(--line); background:#1b2230; color:var(--text); border-radius:10px; padding:7px 11px; }
    .dialog-body { padding:clamp(16px, 3vw, 26px); }
    .verdict { display:flex; align-items:center; gap:14px; padding:18px; border:1px solid #38534f; background:#122b2a; border-radius:15px; }
    .verdict.caution { border-color:#684e24; background:#302516; }
    .verdict:not(.good):not(.caution) { border-color:#594b29; background:#272418; }
    .verdict-icon { display:grid; place-items:center; flex:0 0 46px; width:46px; height:46px; border-radius:14px; background:#204b43; color:#a7f3d0; font-size:1.5rem; }
    .verdict.caution .verdict-icon { background:#593d1a; color:#fcd34d; }
    .verdict-kicker { color:var(--accent); font-size:.7rem; font-weight:800; letter-spacing:.1em; }
    .verdict.caution .verdict-kicker { color:#fcd34d; }
    .verdict h3 { margin:2px 0 3px; font-size:1.15rem; }
    .verdict p { margin:0; color:#b9c4d5; font-size:.85rem; }
    .result-grid { display:grid; grid-template-columns:minmax(0,1.15fr) minmax(0,.85fr); gap:14px; margin-top:14px; }
    .result-box { min-width:0; border:1px solid var(--line); background:#151c29; border-radius:14px; padding:17px; }
    .result-box h4 { margin:0 0 12px; font-size:.9rem; }
    .result-box p { color:#c0cada; font-size:.9rem; margin:0; }
    .score-line { display:flex; align-items:center; gap:12px; margin-bottom:12px; }
    .score-number { font-size:2rem; font-weight:850; letter-spacing:-.06em; }
    .score-caption { color:var(--muted); font-size:.78rem; }
    .score-track { height:6px; background:#2a3446; border-radius:99px; overflow:hidden; margin-top:7px; }
    .score-track span { display:block; height:100%; background:linear-gradient(90deg,#fbbf24,#5eead4); border-radius:99px; }
    .claim-quote { border-left:3px solid var(--accent-2); padding:3px 0 3px 12px; color:#e4eaf4; }
    mark { color:#ffe7a0; background:#5a431f; border-radius:3px; padding:0 2px; }
    .signals { display:flex; gap:7px; flex-wrap:wrap; margin-top:13px; }
    .signal { border:1px solid #4a4050; color:#e8c9e9; background:#282031; padding:5px 8px; border-radius:999px; font-size:.75rem; }
    .recommendations { margin:0; padding-left:19px; color:#c8d1df; font-size:.86rem; }
    .recommendations li + li { margin-top:8px; }
    .source-list { display:grid; gap:8px; }
    .source-link { display:flex; justify-content:space-between; gap:12px; text-decoration:none; border:1px solid #30394b; border-radius:11px; padding:11px 12px; background:#101622; }
    .source-link:hover { border-color:#5c8d89; background:#152329; }
    .source-link strong { display:block; font-size:.84rem; }
    .source-link small { display:block; color:var(--muted); margin-top:2px; font-size:.76rem; }
    .source-arrow { color:var(--accent); align-self:center; }
    .source-disclaimer { color:var(--muted); font-size:.76rem; margin-top:10px; }
    .result-time { color:var(--muted); font-size:.78rem; }
    @media (max-width:680px) {
      .topbar { align-items:flex-start; flex-direction:column; }
      .hero { padding-top:24px; }
      .result-grid { grid-template-columns:1fr; }
      .history-item { align-items:flex-start; flex-direction:column; }
      .history-status { align-self:flex-start; }
      .form-foot { align-items:stretch; }
      .primary { width:100%; }
      .dialog-head { padding:14px 16px; }
    }
  </style>
</head>
<body>
  <div class="shell">
    <header class="topbar">
      <div class="brand"><span class="brand-mark">T</span><span>TrustAI</span></div>
      <div class="top-note">Công cụ hỗ trợ tư duy phản biện</div>
    </header>

    <main>
      <section class="hero">
        <span class="eyebrow">✦ Kiểm chứng thông tin</span>
        <h1>Đừng chỉ tin.<br><span>Hãy kiểm chứng.</span></h1>
        <p class="lead">Phân tích dấu hiệu đáng chú ý trong một nhận định, tìm các nguồn tham khảo và gợi ý bước tiếp theo trước khi bạn tin hoặc chia sẻ thông tin.</p>
      </section>

      <section class="panel" aria-labelledby="inputTitle">
        <div class="panel-heading">
          <h2 id="inputTitle">Bạn muốn kiểm tra thông tin nào?</h2>
          <span class="subtle">Tối đa 2.000 ký tự</span>
        </div>
        <form id="verifyForm">
          <textarea id="claimInput" maxlength="2000" placeholder="Dán một câu nói, bài đăng hoặc nhận định bạn muốn kiểm chứng..." aria-label="Nội dung cần kiểm chứng" required></textarea>
          <div class="form-foot">
            <span class="char-count" id="charCount">0 / 2000</span>
            <button class="primary" type="submit">Phân tích thông tin <span aria-hidden="true">→</span></button>
          </div>
        </form>
        <div class="samples">
          <span class="subtle">Thử một ví dụ:</span>
          <button class="sample-chip" type="button" data-sample="Theo nghiên cứu mới, uống nước chanh có thể chữa khỏi mọi bệnh.">Thông tin sức khỏe</button>
          <button class="sample-chip" type="button" data-sample="Các nhà khoa học xác nhận rằng con người chỉ sử dụng 10% bộ não.">Trích dẫn nghiên cứu</button>
          <button class="sample-chip" type="button" data-sample="Một quy định mới có hiệu lực từ năm 2026 áp dụng cho tất cả mọi người.">Thông tin thời sự</button>
        </div>
        <p class="notice"><span aria-hidden="true">ⓘ</span><span><strong>Lưu ý:</strong> Bản HTML này dùng các quy tắc minh họa để nhận diện từ ngữ cần chú ý; chưa tự động xác minh sự thật bằng AI hoặc xác nhận nội dung từ các nguồn.</span></p>
      </section>

      <section aria-labelledby="historyTitle">
        <div class="section-title">
          <h2 id="historyTitle">Lịch sử trong phiên này</h2>
          <div style="display:flex;align-items:center;gap:9px"><span class="count-pill"><span id="historyCount">0</span> mục</span><span class="count-pill" id="historyBadge">0</span><button id="clearHistory" class="text-button" type="button" hidden>Xóa lịch sử</button></div>
        </div>
        <div class="history-list" id="historyList"></div>
      </section>
    </main>

    <footer><span>© TrustAI · Hỗ trợ kiểm chứng thông tin</span><span>Hãy đối chiếu nguồn gốc trước khi chia sẻ.</span></footer>
  </div>

  <dialog id="resultDialog" aria-labelledby="dialogTitle">
    <div class="dialog-head">
      <div><h2 id="dialogTitle">Kết quả phân tích</h2><span class="result-time">Thời gian: <span id="resultTime">--:--</span></span></div>
      <button id="closeResult" class="close-button" type="button" aria-label="Đóng kết quả">Đóng ✕</button>
    </div>
    <div class="dialog-body" id="resultCard" hidden>
      <div class="verdict" id="verdictBox">
        <div class="verdict-icon" id="verdictIcon">⌕</div>
        <div><div class="verdict-kicker" id="verdictKicker">CẦN ĐỐI CHIẾU</div><h3 id="verdictTitle">Cần kiểm chứng thêm</h3><p id="verdictDescription"></p></div>
      </div>
      <div class="result-grid">
        <section class="result-box">
          <h4>Nhận định được kiểm tra</h4>
          <div class="claim-quote" id="highlightedClaim"></div>
          <div class="signals" id="signalRow"></div>
        </section>
        <section class="result-box">
          <h4>Điểm cảnh báo demo</h4>
          <div class="score-line"><span class="score-number" id="scoreValue">0</span><div style="flex:1"><div class="score-caption">Điểm quy tắc minh họa: <strong id="summaryScore">0</strong>/100</div><div class="score-track"><span id="scoreTrack" style="width:0%"></span></div></div></div>
          <p id="explanationText"></p>
        </section>
        <section class="result-box">
          <h4>Nguồn tham khảo để tra cứu</h4>
          <div class="source-list" id="sourceList"></div>
          <p class="source-disclaimer">Các liên kết bên dưới mở trang tìm kiếm, không phải bằng chứng đã được xác nhận cho nhận định này.</p>
        </section>
        <section class="result-box">
          <h4>Đề xuất bước tiếp theo</h4>
          <ol class="recommendations" id="recommendationList"></ol>
        </section>
      </div>
      <p class="source-disclaimer" style="margin-top:15px">Nội dung đang hiển thị là đánh giá sơ bộ theo từ khóa, không phải kết luận đúng/sai và không thay thế tư vấn chuyên môn.</p>
    </div>
  </dialog>

  <script>
    const form = document.getElementById('verifyForm');
    const input = document.getElementById('claimInput');
    const charCount = document.getElementById('charCount');
    const resultCard = document.getElementById('resultCard');
    const resultDialog = document.getElementById('resultDialog');
    const closeResultButton = document.getElementById('closeResult');
    const historyList = document.getElementById('historyList');
    const historyCount = document.getElementById('historyCount');
    const historyBadge = document.getElementById('historyBadge');
    const clearHistoryButton = document.getElementById('clearHistory');

    let history = [];

    const cautionTerms = [
      { pattern: /chữa khỏi|chữa bệnh|điều trị khỏi|phòng ngừa tuyệt đối|100%/i, label: 'Khẳng định y tế tuyệt đối' },
      { pattern: /chắc chắn|luôn luôn|tất cả mọi người|không bao giờ|duy nhất/i, label: 'Từ ngữ khẳng định mạnh' },
      { pattern: /bí mật|bị che giấu|không ai muốn bạn biết|sự thật gây sốc/i, label: 'Ngôn ngữ giật gân' },
      { pattern: /theo nghiên cứu|nghiên cứu mới|chuyên gia nói|các nhà khoa học/i, label: 'Cần kiểm tra nguồn trích dẫn' },
      { pattern: /năm 20\d\d|hôm nay|vừa qua|mới nhất/i, label: 'Thông tin phụ thuộc thời điểm' },
      { pattern: /tất cả|mọi người|mọi quốc gia|100%/i, label: 'Phạm vi khẳng định rộng' }
    ];

    function escapeHTML(value) {
      return String(value).replace(/[&<>"']/g, char => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' })[char]);
    }

    function analyzeClaim(text) {
      const matched = cautionTerms.filter(item => item.pattern.test(text));
      const terms = matched.map(item => item.label);
      const cautious = matched.some(item => /y tế|giật gân|khẳng định mạnh|phạm vi/i.test(item.label));
      const status = cautious ? 'caution' : matched.length ? 'review' : 'support';
      const score = Math.min(94, Math.max(24, 36 + matched.length * 13 + (cautious ? 14 : 0)));
      const explanations = {
        caution: 'Nội dung có dấu hiệu khẳng định mạnh hoặc tuyệt đối. Đây là lý do nên kiểm tra kỹ nguồn và bằng chứng gốc; dấu hiệu này không tự chứng minh nhận định là sai.',
        review: 'Nội dung có chi tiết cần đặt trong ngữ cảnh hoặc kiểm tra nguồn trích dẫn. Hãy đối chiếu tài liệu gốc và thời điểm công bố trước khi kết luận.',
        support: 'Chưa phát hiện từ khóa cảnh báo rõ ràng theo các quy tắc minh họa. Điều này không đồng nghĩa nhận định đã được xác minh; vẫn cần đối chiếu nguồn độc lập.'
      };
      if (!terms.length) terms.push('Chưa có dấu hiệu rõ theo quy tắc demo');
      return { status, score, terms, explanation: explanations[status] };
    }

    function getClaimSentence(text) {
      const sentences = text.match(/[^.!?]+[.!?]?/g) || [text];
      return sentences.map(sentence => sentence.trim()).find(Boolean) || text;
    }

    function createSourceLinks(text) {
      const query = encodeURIComponent(text.slice(0, 180));
      const sources = [
        { title: 'Tra cứu Thư viện Pháp luật', detail: 'Tìm văn bản pháp luật và bài viết liên quan trên thuvienphapluat.vn', url: `https://www.google.com/search?q=${encodeURIComponent(`site:thuvienphapluat.vn ${text.slice(0, 140)}`)}` },
        { title: 'Tìm trên Google Scholar', detail: 'Bài báo khoa học và tài liệu học thuật', url: `https://scholar.google.com/scholar?q=${query}` },
        { title: 'Tìm nguồn từ cơ quan nhà nước', detail: 'Ưu tiên trang có tên miền .gov.vn', url: `https://www.google.com/search?q=${encodeURIComponent(`site:gov.vn ${text.slice(0, 140)}`)}` },
        { title: 'Tìm trên WHO', detail: 'Thông tin y tế từ Tổ chức Y tế Thế giới', url: `https://www.google.com/search?q=${encodeURIComponent(`site:who.int ${text.slice(0, 140)}`)}` }
      ];
      document.getElementById('sourceList').innerHTML = sources.map(source => `
        <a class="source-link" href="${source.url}" target="_blank" rel="noopener noreferrer">
          <span><strong>${source.title}</strong><small>${source.detail}</small></span><span class="source-arrow" aria-hidden="true">↗</span>
        </a>`).join('');
    }

    function renderResult(text, result, timestamp = new Date()) {
      const verdict = document.getElementById('verdictBox');
      const labels = {
        caution: ['CẦN THẬN TRỌNG', 'Có dấu hiệu cần kiểm chứng', '⚠'],
        review: ['CẦN ĐỐI CHIẾU', 'Cần kiểm chứng thêm', '⌕'],
        support: ['CHƯA THẤY CẢNH BÁO', 'Chưa có dấu hiệu rõ ràng', '✓']
      };
      const [kicker, title, icon] = labels[result.status];
      verdict.className = `verdict ${result.status === 'support' ? 'good' : result.status === 'caution' ? 'caution' : ''}`;
      document.getElementById('verdictKicker').textContent = kicker;
      document.getElementById('verdictTitle').textContent = title;
      document.getElementById('verdictIcon').textContent = icon;
      document.getElementById('verdictDescription').textContent = 'Đánh giá sơ bộ theo quy tắc minh họa — không phải kết luận xác thực.';
      document.getElementById('scoreValue').textContent = result.score;
      document.getElementById('summaryScore').textContent = result.score;
      document.getElementById('scoreTrack').style.width = `${result.score}%`;
      document.getElementById('resultTime').textContent = new Intl.DateTimeFormat('vi-VN', { hour: '2-digit', minute: '2-digit' }).format(timestamp);
      const claim = getClaimSentence(text);
      const safeClaim = escapeHTML(claim);
      const matchedTerms = cautionTerms.filter(item => item.pattern.test(claim));
      let highlighted = safeClaim;
      matchedTerms.forEach(item => {
        highlighted = highlighted.replace(new RegExp(`(${item.pattern.source})`, 'gi'), '<mark>$1</mark>');
      });
      document.getElementById('highlightedClaim').innerHTML = highlighted;
      document.getElementById('explanationText').textContent = result.explanation;
      document.getElementById('signalRow').innerHTML = result.terms.map(term => `<span class="signal">${escapeHTML(term)}</span>`).join('');
      const recommendations = {
        caution: ['Tìm tài liệu gốc hoặc hướng dẫn từ cơ quan chuyên môn trước khi chia sẻ.', 'Đối chiếu nhận định với ít nhất hai nguồn độc lập, đáng tin cậy.', 'Nếu liên quan sức khỏe, hãy hỏi nhân viên y tế thay vì tự điều trị.'],
        review: ['Kiểm tra tác giả, ngày đăng và ngữ cảnh đầy đủ của thông tin.', 'Mở các liên kết tìm kiếm bên dưới để tìm tài liệu gốc và nguồn chính thức.', 'So sánh nội dung từ nhiều nguồn độc lập trước khi kết luận.'],
        support: ['Không xem việc thiếu từ khóa cảnh báo là bằng chứng xác nhận thông tin.', 'Tìm nguồn gốc ban đầu và kiểm tra ngày cập nhật.', 'Đối chiếu thêm với nguồn độc lập trước khi chia sẻ.']
      };
      document.getElementById('recommendationList').innerHTML = recommendations[result.status].map(item => `<li>${escapeHTML(item)}</li>`).join('');
      createSourceLinks(text);
      resultCard.hidden = false;
    }

    function renderHistory() {
      const count = history.length;
      historyCount.textContent = count;
      historyBadge.textContent = count;
      clearHistoryButton.hidden = count === 0;
      if (!count) {
        historyList.innerHTML = '<div class="empty-state"><span class="empty-icon">◷</span><div><strong>Chưa có nội dung nào</strong><p>Kết quả bạn kiểm chứng sẽ xuất hiện ở đây trong phiên này.</p></div></div>';
        return;
      }
      historyList.innerHTML = history.map((entry, index) => {
        const status = entry.result.status;
        const label = status === 'caution' ? 'Cần thận trọng' : status === 'review' ? 'Cần đối chiếu' : 'Chưa thấy cảnh báo';
        const statusClass = status === 'caution' ? 'caution' : status === 'support' ? 'good' : '';
        const time = new Intl.DateTimeFormat('vi-VN', { hour: '2-digit', minute: '2-digit' }).format(entry.timestamp);
        return `<div class="history-item"><div class="history-item-content" data-history="${index}" role="button" tabindex="0" aria-label="Xem lại nội dung đã kiểm chứng"><strong>${escapeHTML(entry.text)}</strong><span>${time}</span></div><span class="history-status ${statusClass}">${label}</span></div>`;
      }).join('');
    }

    input.addEventListener('input', () => { charCount.textContent = `${input.value.length} / 2000`; });

    document.querySelectorAll('.sample-chip').forEach(button => {
      button.addEventListener('click', () => {
        input.value = button.dataset.sample;
        charCount.textContent = `${input.value.length} / 2000`;
        input.focus();
      });
    });

    form.addEventListener('submit', event => {
      event.preventDefault();
      const text = input.value.trim();
      if (!text) return;
      const result = analyzeClaim(text);
      const entry = { text, result, timestamp: new Date() };
      history.unshift(entry);
      history = history.slice(0, 10);
      renderResult(text, result, entry.timestamp);
      renderHistory();
      if (!resultDialog.open) resultDialog.showModal();
    });

    historyList.addEventListener('click', event => {
      const item = event.target.closest('[data-history]');
      if (!item) return;
      const entry = history[Number(item.dataset.history)];
      if (!entry) return;
      renderResult(entry.text, entry.result, entry.timestamp);
      if (!resultDialog.open) resultDialog.showModal();
    });
    historyList.addEventListener('keydown', event => {
      if (event.key === 'Enter' || event.key === ' ') {
        const item = event.target.closest('[data-history]');
        if (item) { event.preventDefault(); item.click(); }
      }
    });
    closeResultButton.addEventListener('click', () => resultDialog.close());
    resultDialog.addEventListener('click', event => {
      if (event.target === resultDialog) resultDialog.close();
    });
    clearHistoryButton.addEventListener('click', () => { history = []; renderHistory(); });

    renderHistory();
  </script>
</body>
</html>
