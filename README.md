# ReadTime
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>ReadTime — Smart Text Analyzer for Writers</title>
  <meta name="description" content="Advanced reading time, readability, tone, and passive voice detection. Free & private.">

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

  <!-- Styles -->
  <style>
    :root {
      --primary: #4361ee;
      --success: #4CAF50;
      --warning: #FFC107;
      --danger: #F44336;
      --text: #1a1a1a;
      --text-muted: #5a5a5a;
      --bg: #ffffff;
      --bg-alt: #f8fafd;
      --border: #e0e6f0;
      --card-shadow: 0 6px 20px rgba(67, 97, 238, 0.1);
      --transition: all 0.3s ease;
    }

    @media (prefers-color-scheme: dark) {
      :root {
        --text: #e0e0e0;
        --text-muted: #aaaaaa;
        --bg: #121212;
        --bg-alt: #1e1e1e;
        --border: #333333;
      }
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Inter', sans-serif;
      background: var(--bg-alt);
      color: var(--text);
      line-height: 1.65;
      min-height: 100vh;
    }

    .container {
      max-width: 900px;
      margin: 40px auto;
      padding: 20px;
    }

    header {
      text-align: center;
      margin-bottom: 32px;
    }

    .logo {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
      margin-bottom: 12px;
    }

    .logo h1 {
      font-size: 2.6rem;
      background: linear-gradient(to right, #4361ee, #3a0ca3);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin: 0;
    }

    .subtitle {
      font-size: 1.1rem;
      color: var(--text-muted);
    }

    .tool-box {
      background: var(--bg);
      border-radius: 16px;
      box-shadow: var(--card-shadow);
      padding: 32px;
      border: 1px solid var(--border);
    }

    textarea {
      width: 100%;
      min-height: 160px;
      padding: 18px;
      border: 1px solid var(--border);
      border-radius: 12px;
      font-size: 1.05rem;
      resize: vertical;
      font-family: inherit;
    }

    textarea:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
    }

    .controls {
      display: flex;
      justify-content: space-between;
      margin: 20px 0;
      flex-wrap: wrap;
      gap: 12px;
    }

    .wpm-selector {
      font-size: 0.95rem;
      color: var(--text-muted);
      display: flex;
      align-items: center;
    }

    .wpm-selector input {
      width: 55px;
      margin: 0 6px;
      padding: 6px;
      border: 1px solid var(--border);
      border-radius: 6px;
    }

    .btn-copy, .btn-export {
      padding: 8px 14px;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: var(--transition);
    }

    .btn-export {
      background: #2a9d8f;
    }

    .btn-copy:hover, .btn-export:hover {
      transform: translateY(-2px);
    }

    .results {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
      gap: 14px;
      margin: 20px 0;
    }

    .result-card {
      padding: 16px;
      background: #f6f9ff;
      border-radius: 10px;
      text-align: center;
      border: 1px solid var(--border);
    }

    .result-card h3 {
      font-size: 0.9rem;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .result-card .value {
      font-size: 1.4rem;
      font-weight: 700;
      color: var(--primary);
    }

    .audience { background: #e3f2fd; }
    .tone { background: #f3e5f5; }
    .passive { background: #ffebee; }

    .details {
      margin-top: 20px;
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
    }

    .section {
      padding: 18px;
      background: #f8fdff;
      border-radius: 12px;
      border-left: 4px solid var(--primary);
    }

    .section h3 {
      color: var(--primary);
      margin-bottom: 10px;
    }

    .tags {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-top: 10px;
    }

    .tag {
      padding: 4px 10px;
      background: #e0f2f1;
      color: #00695c;
      border-radius: 20px;
      font-size: 0.85rem;
    }

    footer {
      text-align: center;
      margin-top: 60px;
      padding: 20px;
      color: var(--text-muted);
      font-size: 0.9rem;
      border-top: 1px solid var(--border);
    }

    .footer-links a {
      color: var(--primary);
      text-decoration: none;
      margin: 0 15px;
    }

    .footer-links a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <div class="logo">
        <span style="font-size: 2rem;">⏱️</span>
        <h1>ReadTime</h1>
      </div>
      <p class="subtitle">Smart text analysis: reading time, tone, passive voice, and audience match.</p>
    </header>

    <div class="tool-box">
      <textarea id="textInput" placeholder="Paste your blog post, article, or story here..."></textarea>

      <div class="controls">
        <div class="wpm-selector">
          Speed: <input type="number" id="wpmInput" value="230" min="100" max="500"> WPM
        </div>
        <div>
          <button class="btn-copy" id="copyBtn">📋 Copy Results</button>
          <button class="btn-export" id="exportBtn">🖼️ Share Card</button>
        </div>
      </div>

      <div class="results">
        <div class="result-card">
          <h3>Words</h3>
          <div class="value" id="wordCount">0</div>
        </div>
        <div class="result-card">
          <h3>Time</h3>
          <div class="value" id="readingTime">1 min</div>
        </div>
        <div class="result-card audience">
          <h3>Audience</h3>
          <div class="value" id="audience">—</div>
        </div>
        <div class="result-card tone">
          <h3>Tone</h3>
          <div class="value" id="tone">—</div>
        </div>
        <div class="result-card passive">
          <h3>Passive</h3>
          <div class="value" id="passive">0%</div>
        </div>
      </div>

      <div class="details">
        <!-- Age-Based Reading Time -->
        <div class="section">
          <h3>👶⏱️ Reading Time by Age</h3>
          <div id="ageTime">Enter text to see</div>
        </div>

        <!-- Passive Voice -->
        <div class="section">
          <h3>🚫 Passive Voice Detected</h3>
          <div id="passiveList">None found</div>
        </div>

        <!-- Tone Tags -->
        <div class="section">
          <h3>🎭 Tone & Style</h3>
          <div class="tags" id="toneTags">Analyzing...</div>
        </div>
      </div>
    </div>

    <footer>
      <p>&copy; 2025 by Sudip Sharma — All rights reserved</p>
      <div class="footer-links">
        <a href="privacy.html">📄 Privacy Policy</a>
        <a href="mailto:sudipsharma2061@gmail.com">✉️ Contact Us</a>
      </div>
    </footer>
  </div>

  <!-- Canvas for Export -->
  <canvas id="exportCanvas" style="display:none;"></canvas>

  <script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
  <script>
    const textInput = document.getElementById("textInput");
    const wordCountEl = document.getElementById("wordCount");
    const readingTimeEl = document.getElementById("readingTime");
    const audienceEl = document.getElementById("audience");
    const toneEl = document.getElementById("tone");
    const passiveEl = document.getElementById("passive");
    const ageTimeEl = document.getElementById("ageTime");
    const passiveListEl = document.getElementById("passiveList");
    const toneTagsEl = document.getElementById("toneTags");
    const wpmInput = document.getElementById("wpmInput");
    const copyBtn = document.getElementById("copyBtn");
    const exportBtn = document.getElementById("exportBtn");

    const PASSIVE_VERBS = ['is', 'are', 'was', 'were', 'been', 'being', 'be', 'am'];
    const FORM_WORDS = ['utilize', 'facilitate', 'demonstrate', 'indicate'];
    const EMOTIVE_WORDS = ['love', 'hate', 'amazing', 'terrible', 'excited', 'sad'];

    function updateStats() {
      const text = textInput.value.trim();
      const wpm = parseInt(wpmInput.value) || 230;
      if (!text) {
        resetAll();
        return;
      }

      const words = text.split(/\s+/).filter(Boolean).length;
      const sentences = text.split(/[.!?]+/).filter(s => s.trim().length > 0);
      const minutes = Math.max(1, Math.ceil(words / wpm));

      wordCountEl.textContent = words;
      readingTimeEl.textContent = `${minutes} min`;

      // Flesch Score
      const flesch = calculateFlesch(text);
      audienceEl.textContent = getAudience(flesch);

      // Tone
      const { tone, tags } = getTone(text, flesch);
      toneEl.textContent = tone;
      toneTagsEl.innerHTML = tags.map(t => `<span class="tag">${t}</span>`).join('');

      // Passive Voice
      const { percent, examples } = detectPassiveVoice(text);
      passiveEl.textContent = `${percent}%`;
      passiveListEl.innerHTML = examples.length ? examples.map(ex => `<em>${ex}</em>`).join('<br>') : 'None found';

      // Age-Based Reading Time
      ageTimeEl.innerHTML = `
        <strong>8–12 yrs:</strong> ${Math.ceil(words / 150)} min |
        <strong>Adult:</strong> ${minutes} min |
        <strong>Senior:</strong> ${Math.ceil(words / 180)} min
      `;
    }

    function resetAll() {
      wordCountEl.textContent = "0";
      readingTimeEl.textContent = "1 min";
      audienceEl.textContent = "—";
      toneEl.textContent = "—";
      passiveEl.textContent = "0%";
      ageTimeEl.textContent = "Enter text to see";
      passiveListEl.innerHTML = "None found";
      toneTagsEl.innerHTML = "Analyzing...";
    }

    function calculateFlesch(text) {
      const sentences = Math.max(1, text.split(/[.!?]+/).filter(s => s.trim().length > 0).length);
      const words = text.split(/\s+/).filter(w => w.length > 0);
      const wordCount = words.length;
      if (wordCount === 0) return 0;

      let syllables = 0;
      words.forEach(w => {
        const clean = w.toLowerCase().replace(/[^a-z]/g, '');
        if (clean.length <= 3) return syllables++;
        for (let i = 0; i < clean.length; i++) {
          if ('aeiouy'.includes(clean[i]) && (i === 0 || !'aeiouy'.includes(clean[i-1]))) syllables++;
        }
        if (clean.endsWith('e')) syllables--;
        syllables = Math.max(syllables, 1);
      });

      const ASL = wordCount / sentences;
      const ASW = syllables / wordCount;
      return 206.835 - (1.015 * ASL) - (84.6 * ASW);
    }

    function getAudience(score) {
      if (score >= 70) return "General";
      if (score >= 50) return "Advanced";
      return "Expert";
    }

    function getTone(text, flesch) {
      const lower = text.toLowerCase();
      const tags = [];
      let tone = "Neutral";

      if (flesch > 70) tags.push("Simple");
      if (flesch < 50) tags.push("Complex");

      if (FORM_WORDS.some(w => lower.includes(w))) tags.push("Formal");
      if (EMOTIVE_WORDS.some(w => lower.includes(w))) {
        tags.push("Emotional");
        tone = "Emotional";
      }
      if (!tags.includes("Formal") && !tags.includes("Emotional")) {
        tags.push("Casual");
        tone = "Casual";
      }

      return { tone, tags };
    }

    function detectPassiveVoice(text) {
      const sentences = text.split(/[.!?]+/).filter(s => s.trim().length > 0);
      const passive = [];
      let count = 0;

      sentences.forEach(sent => {
        const words = sent.toLowerCase().trim().split(/\s+/);
        PASSIVE_VERBS.forEach(verb => {
          const idx = words.indexOf(verb);
          if (idx > -1 && idx < words.length - 1) {
            const next = words[idx + 1];
            if (next.endsWith('ed') || ['broken', 'written', 'done'].includes(next)) {
              passive.push(sent.trim());
              count++;
              return;
            }
          }
        });
      });

      const percent = Math.round((count / sentences.length) * 100);
      return { percent, examples: passive.slice(0, 3) };
    }

    // Copy Results
    copyBtn.addEventListener("click", () => {
      const results = `
📄 ReadTime Analysis
----------------------------
Words: ${wordCountEl.textContent}
Reading Time: ${readingTimeEl.textContent}
Audience: ${audienceEl.textContent}
Tone: ${toneEl.textContent}
Passive Voice: ${passiveEl.textContent}
      `.trim();

      navigator.clipboard.writeText(results).then(() => {
        copyBtn.textContent = "✅ Copied!";
        setTimeout(() => copyBtn.textContent = "📋 Copy Results", 2000);
      });
    });

    // Export as PNG (Share Card)
    exportBtn.addEventListener("click", () => {
      alert("Generating shareable card...");
      html2canvas(document.querySelector(".tool-box"), {
        backgroundColor: '#f8fafd',
        scale: 2
      }).then(canvas => {
        const link = document.createElement('a');
        link.download = 'readtime-analysis.png';
        link.href = canvas.toDataURL();
        link.click();
      });
    });

    // Auto-update
    textInput.addEventListener("input", () => setTimeout(updateStats, 100));
    updateStats();
  </script>
</body>
</html>
