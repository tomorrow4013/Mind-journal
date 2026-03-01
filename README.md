<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>こころの日記 — 振り返り</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@300;400;500&family=Zen+Kaku+Gothic+New:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0c0b14;
    --surface: #161424;
    --surface2: #1e1b2e;
    --surface3: #252238;
    --border: rgba(255,255,255,0.06);
    --border2: rgba(255,255,255,0.1);
    --accent: #c9a96e;
    --accent2: #8b7fc7;
    --accent3: #7eb8a4;
    --text: #e8e6f0;
    --muted: #6a6880;
    --muted2: #9896a8;
    --danger: #e07070;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Zen Kaku Gothic New', sans-serif;
    font-weight: 300;
    min-height: 100vh;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse at 10% 10%, rgba(139,127,199,0.06) 0%, transparent 45%),
      radial-gradient(ellipse at 90% 90%, rgba(201,169,110,0.04) 0%, transparent 45%);
    pointer-events: none;
    z-index: 0;
  }

  .app {
    display: grid;
    grid-template-columns: 220px 1fr;
    min-height: 100vh;
    position: relative;
    z-index: 1;
  }

  /* Sidebar */
  .sidebar {
    background: var(--surface);
    border-right: 1px solid var(--border);
    padding: 32px 0;
    display: flex;
    flex-direction: column;
    position: sticky;
    top: 0;
    height: 100vh;
    overflow-y: auto;
  }

  .logo {
    padding: 0 24px 24px;
    border-bottom: 1px solid var(--border);
    margin-bottom: 24px;
  }

  .logo-text {
    font-family: 'Noto Serif JP', serif;
    font-size: 18px;
    font-weight: 300;
    letter-spacing: 0.12em;
  }
  .logo-text span { color: var(--accent); }
  .logo-sub { font-size: 10px; color: var(--muted); letter-spacing: 0.15em; text-transform: uppercase; margin-top: 4px; }

  .nav-section { padding: 0 16px; margin-bottom: 24px; }
  .nav-label { font-size: 10px; color: var(--muted); letter-spacing: 0.15em; text-transform: uppercase; padding: 0 8px; margin-bottom: 8px; }

  .nav-item {
    display: flex; align-items: center; gap: 10px;
    padding: 9px 12px; border-radius: 10px; cursor: pointer;
    transition: all 0.2s; font-size: 13px; color: var(--muted2); margin-bottom: 2px;
  }
  .nav-item:hover { background: var(--surface2); color: var(--text); }
  .nav-item.active { background: var(--surface3); color: var(--text); }
  .nav-item .icon { font-size: 14px; width: 18px; text-align: center; }

  .tag-filters { padding: 0 16px; }
  .tag-filter {
    display: flex; align-items: center; gap: 8px;
    padding: 7px 12px; border-radius: 8px; cursor: pointer;
    transition: all 0.2s; font-size: 12px; color: var(--muted2); margin-bottom: 2px;
  }
  .tag-filter:hover { background: var(--surface2); color: var(--text); }
  .tag-filter.active { background: var(--surface2); color: var(--text); }
  .tag-dot { width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0; }

  /* Main */
  .main { padding: 40px; overflow-y: auto; }

  .page-header {
    display: flex; align-items: flex-end; justify-content: space-between; margin-bottom: 32px;
  }
  .page-title { font-family: 'Noto Serif JP', serif; font-size: 22px; font-weight: 300; letter-spacing: 0.08em; }
  .page-subtitle { font-size: 12px; color: var(--muted); margin-top: 4px; }

  .reload-btn {
    background: none;
    border: 1px solid var(--border2);
    color: var(--muted2);
    font-size: 12px;
    font-family: inherit;
    padding: 7px 14px;
    border-radius: 20px;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.05em;
  }
  .reload-btn:hover { color: var(--text); border-color: var(--border2); }

  /* Stats */
  .stats-row { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-bottom: 32px; }

  .stat-card {
    background: var(--surface); border: 1px solid var(--border); border-radius: 16px;
    padding: 20px 22px; animation: fadeUp 0.4s ease both;
  }
  .stat-card:nth-child(1) { animation-delay: 0.05s; }
  .stat-card:nth-child(2) { animation-delay: 0.1s; }
  .stat-card:nth-child(3) { animation-delay: 0.15s; }

  .stat-label { font-size: 11px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 8px; }
  .stat-value { font-family: 'Noto Serif JP', serif; font-size: 28px; font-weight: 300; line-height: 1; }
  .stat-unit { font-size: 12px; color: var(--muted2); margin-left: 4px; }
  .stat-sub { font-size: 11px; color: var(--muted); margin-top: 6px; }

  /* Chart */
  .chart-card {
    background: var(--surface); border: 1px solid var(--border); border-radius: 16px;
    padding: 24px; margin-bottom: 32px; animation: fadeUp 0.4s ease 0.2s both;
  }
  .chart-title { font-size: 13px; color: var(--muted2); letter-spacing: 0.05em; margin-bottom: 20px; }
  .chart-area {
    height: 120px; position: relative; display: flex;
    align-items: flex-end; gap: 6px;
  }
  .chart-baseline { position: absolute; bottom: 26px; left: 0; right: 0; height: 1px; background: var(--border2); }
  .chart-bar-wrap { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 6px; height: 100%; justify-content: flex-end; }
  .chart-bar { width: 100%; border-radius: 4px 4px 0 0; transition: height 0.6s cubic-bezier(0.34,1.56,0.64,1); cursor: pointer; }
  .chart-bar:hover { opacity: 0.75; }
  .chart-bar-label { font-size: 10px; color: var(--muted); text-align: center; }

  .mood-legend { display: flex; gap: 16px; margin-top: 12px; }
  .mood-legend-item { display: flex; align-items: center; gap: 6px; font-size: 11px; color: var(--muted); }
  .mood-legend-dot { width: 8px; height: 8px; border-radius: 50%; }

  /* Entry list */
  .section-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 16px; }
  .section-title { font-size: 12px; color: var(--muted); letter-spacing: 0.12em; text-transform: uppercase; }
  .entry-count { font-size: 12px; color: var(--muted); }

  .entry-list { display: flex; flex-direction: column; gap: 12px; }

  .entry-card {
    background: var(--surface); border: 1px solid var(--border); border-radius: 16px;
    padding: 20px 22px; cursor: pointer; transition: all 0.25s; animation: fadeUp 0.4s ease both;
  }
  .entry-card:hover { border-color: var(--border2); background: var(--surface2); transform: translateY(-1px); }

  .entry-top { display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; margin-bottom: 10px; }
  .entry-title { font-family: 'Noto Serif JP', serif; font-size: 15px; font-weight: 400; letter-spacing: 0.04em; line-height: 1.5; }
  .entry-meta { display: flex; align-items: center; gap: 10px; flex-shrink: 0; }
  .entry-date { font-size: 11px; color: var(--muted); }
  .mood-emoji { font-size: 16px; }

  .entry-worry {
    font-size: 13px; color: var(--muted2); line-height: 1.7; margin-bottom: 12px;
    display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden;
  }

  .entry-bottom { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }

  .tag { padding: 3px 10px; border-radius: 20px; font-size: 11px; border: 1px solid; }
  .tag-work { color: #c9a96e; border-color: rgba(201,169,110,0.3); background: rgba(201,169,110,0.08); }
  .tag-relation { color: #8b7fc7; border-color: rgba(139,127,199,0.3); background: rgba(139,127,199,0.08); }
  .tag-health { color: #7eb8a4; border-color: rgba(126,184,164,0.3); background: rgba(126,184,164,0.08); }
  .tag-money { color: #d4877a; border-color: rgba(212,135,122,0.3); background: rgba(212,135,122,0.08); }
  .tag-other { color: var(--muted2); border-color: rgba(152,150,168,0.3); background: rgba(152,150,168,0.08); }

  .entry-advice-preview { font-size: 12px; color: var(--muted); margin-left: auto; white-space: nowrap; }

  .entry-advice { display: none; margin-top: 14px; padding-top: 14px; border-top: 1px solid var(--border); }
  .entry-card.expanded .entry-advice { display: block; }
  .advice-label { font-size: 10px; color: var(--accent2); letter-spacing: 0.12em; text-transform: uppercase; margin-bottom: 8px; }
  .advice-text { font-size: 13px; color: var(--muted2); line-height: 1.8; white-space: pre-wrap; }

  /* Loading / empty */
  .loading-state { text-align: center; padding: 60px 20px; color: var(--muted); font-size: 14px; }
  .loading-spinner {
    width: 32px; height: 32px; border: 2px solid var(--border2);
    border-top-color: var(--accent2); border-radius: 50%;
    animation: spin 0.8s linear infinite; margin: 0 auto 16px;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  .empty-state { text-align: center; padding: 60px 20px; color: var(--muted); font-size: 14px; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @media (max-width: 700px) {
    .app { grid-template-columns: 1fr; }
    .sidebar { display: none; }
    .main { padding: 24px 16px; }
    .stats-row { grid-template-columns: 1fr 1fr; }
  }
</style>
</head>
<body>
<div class="app">

  <aside class="sidebar">
    <div class="logo">
      <div class="logo-text">こころの<span>日記</span></div>
      <div class="logo-sub">振り返りダッシュボード</div>
    </div>
    <div class="nav-section">
      <div class="nav-label">表示</div>
      <div class="nav-item active" onclick="filterTag('all', this)"><span class="icon">📋</span> すべての記録</div>
    </div>
    <div class="tag-filters">
      <div class="nav-label">タグ</div>
      <div class="tag-filter active" onclick="filterTag('all', this)">
        <span class="tag-dot" style="background:#6a6880"></span> すべて
      </div>
      <div class="tag-filter" onclick="filterTag('仕事・キャリア', this)">
        <span class="tag-dot" style="background:#c9a96e"></span> 仕事・キャリア
      </div>
      <div class="tag-filter" onclick="filterTag('人間関係', this)">
        <span class="tag-dot" style="background:#8b7fc7"></span> 人間関係
      </div>
      <div class="tag-filter" onclick="filterTag('健康・メンタル', this)">
        <span class="tag-dot" style="background:#7eb8a4"></span> 健康・メンタル
      </div>
      <div class="tag-filter" onclick="filterTag('お金・生活', this)">
        <span class="tag-dot" style="background:#d4877a"></span> お金・生活
      </div>
      <div class="tag-filter" onclick="filterTag('その他', this)">
        <span class="tag-dot" style="background:#9896a8"></span> その他
      </div>
    </div>
  </aside>

  <main class="main">
    <div class="page-header">
      <div>
        <div class="page-title">振り返りダッシュボード</div>
        <div class="page-subtitle" id="lastUpdated">読み込み中…</div>
      </div>
      <button class="reload-btn" onclick="loadData()">↻ 更新</button>
    </div>

    <div class="stats-row">
      <div class="stat-card">
        <div class="stat-label">総記録数</div>
        <div class="stat-value" id="statTotal">—<span class="stat-unit">件</span></div>
        <div class="stat-sub" id="statMonth"></div>
      </div>
      <div class="stat-card">
        <div class="stat-label">平均気分スコア</div>
        <div class="stat-value" id="statMood">—<span class="stat-unit">/ 5</span></div>
        <div class="stat-sub" id="statMoodSub"></div>
      </div>
      <div class="stat-card">
        <div class="stat-label">最多タグ</div>
        <div class="stat-value" id="statTopTag" style="font-size:16px; padding-top:6px;">—</div>
        <div class="stat-sub" id="statTopTagSub"></div>
      </div>
    </div>

    <div class="chart-card">
      <div class="chart-title">気分スコアの推移</div>
      <div class="chart-area" id="chart">
        <div class="chart-baseline"></div>
      </div>
      <div class="mood-legend">
        <div class="mood-legend-item"><div class="mood-legend-dot" style="background:#e07070"></div> つらい (1-2)</div>
        <div class="mood-legend-item"><div class="mood-legend-dot" style="background:#c9a96e"></div> ふつう (3)</div>
        <div class="mood-legend-item"><div class="mood-legend-dot" style="background:#7eb8a4"></div> 良い (4-5)</div>
      </div>
    </div>

    <div class="section-header">
      <div class="section-title">記録一覧</div>
      <div class="entry-count" id="entryCount"></div>
    </div>
    <div class="entry-list" id="entryList">
      <div class="loading-state">
        <div class="loading-spinner"></div>
        Notionから読み込んでいます…
      </div>
    </div>
  </main>
</div>

<script>
  const NOTION_KEY = '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';
  const NOTION_DB  = '31526ba2e5b68006a052e47535b0fbff';

  const colorMap = { 1: '#e07070', 2: '#e07070', 3: '#c9a96e', 4: '#7eb8a4', 5: '#7eb8a4' };
  const moodEmoji = { 1: '😞', 2: '😔', 3: '😐', 4: '🙂', 5: '😊' };
  const tagClass  = {
    '仕事・キャリア': 'tag-work',
    '人間関係': 'tag-relation',
    '健康・メンタル': 'tag-health',
    'お金・生活': 'tag-money',
    'その他': 'tag-other'
  };

  let allEntries = [];
  let currentFilter = 'all';

  async function loadData() {
    document.getElementById('entryList').innerHTML = `
      <div class="loading-state">
        <div class="loading-spinner"></div>
        Notionから読み込んでいます…
      </div>`;

    try {
      const res = await fetch(`https://api.notion.com/v1/databases/${NOTION_DB}/query`, {
        method: 'POST',
        headers: {
          'Authorization': 'Bearer ' + NOTION_KEY,
          'Content-Type': 'application/json',
          'Notion-Version': '2022-06-28'
        },
        body: JSON.stringify({
          sorts: [{ property: '日付', direction: 'descending' }],
          page_size: 100
        })
      });

      const data = await res.json();
      if (!res.ok) throw new Error(data.message);

      allEntries = data.results.map(page => {
        const p = page.properties;
        return {
          id: page.id,
          title: p['タイトル']?.title?.[0]?.plain_text || '無題',
          date: p['日付']?.date?.start || '',
          worry: p['悩み']?.rich_text?.[0]?.plain_text || '',
          advice: p['アドバイス']?.rich_text?.[0]?.plain_text || '',
          tags: p['タグ']?.multi_select?.map(t => t.name) || [],
          mood: p['気分スコア']?.number || 0,
        };
      });

      updateStats();
      buildChart();
      renderEntries();

      const now = new Date();
      document.getElementById('lastUpdated').textContent =
        `最終更新：${now.getHours()}:${String(now.getMinutes()).padStart(2,'0')}`;

    } catch(e) {
      document.getElementById('entryList').innerHTML =
        `<div class="empty-state">読み込みに失敗しました。<br><small style="color:var(--danger)">${e.message}</small></div>`;
    }
  }

  function updateStats() {
    const total = allEntries.length;
    document.getElementById('statTotal').innerHTML = `${total}<span class="stat-unit">件</span>`;

    const thisMonth = new Date().getMonth();
    const monthCount = allEntries.filter(e => e.date && new Date(e.date).getMonth() === thisMonth).length;
    document.getElementById('statMonth').textContent = `今月 ${monthCount} 件`;

    const withMood = allEntries.filter(e => e.mood > 0);
    if (withMood.length > 0) {
      const avg = (withMood.reduce((s, e) => s + e.mood, 0) / withMood.length).toFixed(1);
      document.getElementById('statMood').innerHTML = `${avg}<span class="stat-unit">/ 5</span>`;
      document.getElementById('statMoodSub').textContent = `${withMood.length} 件の記録から`;
    }

    const tagCount = {};
    allEntries.forEach(e => e.tags.forEach(t => { tagCount[t] = (tagCount[t] || 0) + 1; }));
    const topTag = Object.entries(tagCount).sort((a,b) => b[1]-a[1])[0];
    if (topTag) {
      document.getElementById('statTopTag').textContent = topTag[0];
      const pct = Math.round(topTag[1] / total * 100);
      document.getElementById('statTopTagSub').textContent = `全体の ${pct}%`;
    }
  }

  function buildChart() {
    const chart = document.getElementById('chart');
    // Keep baseline
    chart.innerHTML = '<div class="chart-baseline"></div>';

    const withMood = allEntries.filter(e => e.mood > 0 && e.date).slice(0, 12).reverse();
    if (withMood.length === 0) return;

    const chartH = 94;
    withMood.forEach(e => {
      const wrap = document.createElement('div');
      wrap.className = 'chart-bar-wrap';

      const bar = document.createElement('div');
      bar.className = 'chart-bar';
      bar.style.height = '0px';
      bar.style.background = colorMap[e.mood] || '#6a6880';
      bar.title = `${e.date}：${e.mood}`;

      const label = document.createElement('div');
      label.className = 'chart-bar-label';
      label.textContent = e.date.slice(5); // MM-DD

      wrap.appendChild(bar);
      wrap.appendChild(label);
      chart.appendChild(wrap);

      setTimeout(() => {
        bar.style.height = ((e.mood / 5) * chartH) + 'px';
      }, 100);
    });
  }

  function renderEntries() {
    const filtered = currentFilter === 'all'
      ? allEntries
      : allEntries.filter(e => e.tags.includes(currentFilter));

    document.getElementById('entryCount').textContent = `${filtered.length} 件`;

    if (filtered.length === 0) {
      document.getElementById('entryList').innerHTML =
        '<div class="empty-state">記録がありません</div>';
      return;
    }

    document.getElementById('entryList').innerHTML = filtered.map((e, i) => {
      const tagsHtml = e.tags.map(t =>
        `<span class="tag ${tagClass[t] || 'tag-other'}">${t}</span>`
      ).join('');
      const emoji = e.mood ? moodEmoji[e.mood] || '' : '';
      const dateStr = e.date ? e.date.replace(/-/g, '/') : '';

      return `
        <div class="entry-card" onclick="toggleEntry(this)" style="animation-delay:${i * 0.05}s">
          <div class="entry-top">
            <div class="entry-title">${escHtml(e.title)}</div>
            <div class="entry-meta">
              <span class="entry-date">${dateStr}</span>
              <span class="mood-emoji">${emoji}</span>
            </div>
          </div>
          ${e.worry ? `<div class="entry-worry">${escHtml(e.worry)}</div>` : ''}
          <div class="entry-bottom">
            ${tagsHtml}
            ${e.advice ? '<span class="entry-advice-preview">アドバイスを見る ›</span>' : ''}
          </div>
          ${e.advice ? `
          <div class="entry-advice">
            <div class="advice-label">Claude のアドバイス</div>
            <div class="advice-text">${escHtml(e.advice)}</div>
          </div>` : ''}
        </div>`;
    }).join('');
  }

  function filterTag(tag, el) {
    currentFilter = tag;
    document.querySelectorAll('.tag-filter, .nav-item').forEach(el => el.classList.remove('active'));
    el.classList.add('active');
    renderEntries();
  }

  function toggleEntry(el) {
    el.classList.toggle('expanded');
    const preview = el.querySelector('.entry-advice-preview');
    if (preview) preview.textContent = el.classList.contains('expanded') ? '閉じる ›' : 'アドバイスを見る ›';
  }

  function escHtml(str) {
    return str.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
  }

  loadData();
</script>
</body>
</html>
