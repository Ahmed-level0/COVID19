<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>COVID-19 Data Cleaning & Exploratory Analysis – README</title>
  <style>
    :root {
      --bg: #0b0f14;
      --card: #121821;
      --text: #e8eef7;
      --muted: #9fb3c8;
      --accent: #5aa9ff;
      --accent-2: #7ee787;
      --border: #1f2a37;
      --code-bg: #0d1117;
    }
    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji";
      color: var(--text);
      background: radial-gradient(1200px 800px at 80% -10%, #123, transparent 50%),
                  radial-gradient(800px 600px at -10% 20%, #112233, transparent 40%),
                  var(--bg);
      line-height: 1.6;
    }
    .container { max-width: 980px; margin: 48px auto; padding: 0 20px; }
    header {
      background: linear-gradient(180deg, rgba(90,169,255,0.12), transparent 60%);
      padding: 24px 20px; border: 1px solid var(--border); border-radius: 16px;
    }
    h1 { font-size: 2rem; margin: 0 0 12px; letter-spacing: 0.4px; }
    .subtitle { color: var(--muted); margin-top: 0; }
    .badges { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 10px; }
    .badge { border: 1px solid var(--border); background: #0f1520; color: var(--muted); padding: 6px 10px; border-radius: 999px; font-size: 12px; }
    nav.toc { margin: 28px 0 12px; }
    nav.toc a { display: inline-block; margin: 4px 10px 4px 0; color: var(--accent); text-decoration: none; }
    section { background: var(--card); padding: 22px; border: 1px solid var(--border); border-radius: 16px; margin: 18px 0; }
    h2 { margin-top: 0; font-size: 1.3rem; }
    h3 { margin-bottom: 8px; font-size: 1.05rem; color: var(--accent-2); }
    p { margin: 8px 0 12px; color: var(--text); }
    ul { margin: 0 0 6px 18px; }
    li { margin: 6px 0; }
    code, pre { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace; }
    pre { background: var(--code-bg); color: #eef; padding: 14px; border-radius: 12px; overflow: auto; border: 1px solid #222a36; }
    .grid { display: grid; gap: 14px; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); }
    .hint { font-size: 0.95rem; color: var(--muted); }
    .footer { text-align: center; color: var(--muted); margin-top: 28px; font-size: 0.9rem; }
    .pill { display: inline-block; padding: 2px 8px; border-radius: 999px; border: 1px solid var(--border); color: var(--muted); font-size: 12px; }
    .arabic { direction: rtl; text-align: right; }
    a.button {
      display: inline-block; padding: 10px 14px; border-radius: 10px; border: 1px solid var(--border);
      color: var(--text); text-decoration: none; background: #0e1525; transition: transform .05s ease;
    }
    a.button:hover { transform: translateY(-1px); }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>COVID-19 Data Cleaning & Exploratory Analysis</h1>
      <p class="subtitle">A concise, production-quality README for the project notebook <code>analysis.ipynb</code>.</p>
      <div class="badges">
        <span class="badge">Python</span>
        <span class="badge">Pandas</span>
        <span class="badge">NumPy</span>
        <span class="badge">Matplotlib</span>
        <span class="badge">Seaborn</span>
      </div>
      <nav class="toc">
        <a href="#overview">Overview</a>
        <a href="#tools">Tools</a>
        <a href="#data-cleaning">Data&nbsp;Cleaning</a>
        <a href="#eda">EDA</a>
        <a href="#insights">Insights</a>
        <a href="#future-work">Future Work</a>
        <a href="#structure">Project Structure</a>
        <a href="#author">Author</a>
        <a href="#ar">ملخص بالعربية</a>
      </nav>
    </header>

    <section id="overview">
      <h2>Overview</h2>
      <p>
        This repository contains a complete workflow for <strong>cleaning</strong> and <strong>exploring</strong> COVID‑19 case and death data sourced from the WHO.
        The primary objectives are to resolve missing values, reconstruct daily metrics from cumulative counts, and generate visual analyses across years and WHO regions.
      </p>
      <div class="grid">
        <div>
          <h3>Goals</h3>
          <ul>
            <li>Handle and impute <em>missing values</em>.</li>
            <li>Recalculate <code>New_cases</code> and <code>New_deaths</code> from cumulative columns.</li>
            <li>Perform <strong>EDA</strong> with clear, readable plots.</li>
            <li>Document decisions and assumptions along the way.</li>
          </ul>
        </div>
        <div>
          <h3>Key Plots</h3>
          <ul>
            <li>Line plots: yearly trends for <strong>cases</strong> and <strong>deaths</strong>.</li>
            <li>Count plot: distribution of cases per WHO region.</li>
          </ul>
        </div>
      </div>
    </section>

    <section id="tools">
      <h2>Tools & Libraries</h2>
      <ul>
        <li><strong>Python</strong> – analysis, transformation, and visualization.</li>
        <li><strong>Pandas</strong> – data manipulation and grouping.</li>
        <li><strong>NumPy</strong> – numerical helpers.</li>
        <li><strong>Matplotlib / Seaborn</strong> – visualizations.</li>
      </ul>
      <p class="hint">Dataset filename: <code>Covid19.csv</code> (ensure it’s placed in the project root or update paths accordingly).</p>
    </section>

    <section id="data-cleaning">
      <h2>Data Cleaning Steps</h2>
      <ol>
        <li>Load and inspect the dataset: <code>head()</code>, <code>info()</code>, <code>isna().sum()</code>.</li>
        <li>Sort by <code>Country</code>, <code>WHO_region</code>, and <code>Date_reported</code>.</li>
        <li>Create previous-day cumulative columns using <code>groupby</code> + <code>shift()</code>.</li>
        <li>Impute <code>New_cases</code> and <code>New_deaths</code> by subtracting previous cumulative values.</li>
        <li>Drop minor or irrelevant missing fields (e.g., sparse country codes).</li>
        <li>Validate: ensure no remaining <code>NaN</code> values post-cleaning.</li>
      </ol>
      <p class="hint">Rationale: Using cumulative-to-daily differences preserves the time series and minimizes information loss.</p>
    </section>

    <section id="eda">
      <h2>Exploratory Data Analysis (EDA)</h2>
      <ul>
        <li><strong>Line Plots</strong> – cases and deaths across years, highlighting wave peaks and declines.</li>
        <li><strong>Count Plot</strong> – per WHO region, enabling quick regional comparisons.</li>
      </ul>
      <p class="hint">Extend with 7‑day rolling averages and seasonal breakdowns for smoother patterns and deeper insight.</p>
    </section>

    <section id="insights">
      <h2>Insights (Examples)</h2>
      <ul>
        <li>Sharp growth throughout 2020–2021 for both cases and deaths, consistent with initial waves.</li>
        <li>European and American regions typically show the highest cumulative counts in the dataset.</li>
        <li>Death trends generally lag behind case spikes, indicating reporting and disease progression delays.</li>
      </ul>
    </section>

    <section id="future-work">
      <h2>Future Work</h2>
      <ul>
        <li>Add <strong>rolling averages</strong> (e.g., 7‑day) for trend smoothing.</li>
        <li>Run a <strong>correlation analysis</strong> between daily cases and deaths.</li>
        <li>Experiment with <strong>time‑series models</strong> (ARIMA / Prophet) for forecasting.</li>
        <li>Package an interactive dashboard (Streamlit or Plotly Dash).</li>
      </ul>
    </section>

    <section id="structure">
      <h2>Project Structure</h2>
      <pre>
📦 covid19-analysis
 ┣ 📜 analysis.ipynb      # Main notebook (cleaning + EDA)
 ┣ 📜 Covid19.csv         # Dataset (excluded if large)
 ┗ 📜 README.html         # This file (rendered on GitHub Pages or locally)
      </pre>
    </section>

    <section id="author">
      <h2>Author</h2>
      <p><strong>Ahmed Hambuta</strong> – Data Analyst & ML Enthusiast</p>
      <ul>
        <li>Focus: Data Cleaning · EDA · Visualization · ML</li>
        <li>GitHub: <a class="button" href="#" target="_blank" rel="noopener">Add your profile link</a></li>
      </ul>
    </section>

    <section id="ar" class="arabic">
      <h2>ملخص بالعربية</h2>
      <p>
        المشروع بيقدّم خطوات كاملة لتنظيف بيانات كوفيد‑19 وتحليلها بصريًا. 
        تم معالجة القيم المفقودة وإعادة بناء القيم اليومية من الأعمدة التراكمية، 
        مع رسم مخططات خطية لعدد الحالات والوفيات عبر السنين، و<em>count plot</em> حسب أقاليم منظمة الصحة العالمية.
      </p>
      <ul>
        <li>تنظيف البيانات: ترتيب + <code>groupby</code> + <code>shift()</code> + تعويض المفقود.</li>
        <li>تحليل بصري: خطوط زمنية وتوزيع حسب الأقاليم.</li>
        <li>تطوير مستقبلي: متوسطات متحركة، ترابط، ونماذج تنبؤية.</li>
      </ul>
    </section>

    <p class="footer">© <span id="year"></span> Ahmed Hambuta — Released under MIT (optional)</p>
  </div>
  <script>
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>
