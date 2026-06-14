# case-feedback
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Case Interview Feedback</title>
<style>
  * { box-sizing: border-box; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    background: #f5f5f7;
    color: #222;
    margin: 0;
    padding: 24px;
    line-height: 1.4;
  }
  .container { max-width: 900px; margin: 0 auto; background: #fff; border-radius: 8px; padding: 32px; box-shadow: 0 1px 3px rgba(0,0,0,.08); }
  h1 { color: #4b2e83; margin: 0 0 4px; font-size: 28px; border-bottom: 2px solid #4b2e83; padding-bottom: 12px; }
  .subtitle { color: #666; font-size: 14px; margin-bottom: 24px; }
  .meta { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; margin-bottom: 28px; }
  .meta label { display: flex; flex-direction: column; font-size: 13px; color: #555; font-weight: 600; }
  .meta input, .meta select { margin-top: 4px; padding: 8px 10px; border: 1px solid #ccc; border-radius: 4px; font-size: 14px; }
  .section { margin-bottom: 24px; border: 1px solid #e0d9ec; border-radius: 6px; overflow: hidden; }
  .section-header { background: #4b2e83; color: #fff; padding: 10px 14px; font-weight: 600; display: flex; justify-content: space-between; font-size: 15px; }
  .section-header .rating-label { font-weight: 400; font-size: 13px; }
  .criterion { display: grid; grid-template-columns: 1fr auto; gap: 16px; align-items: center; padding: 10px 14px; border-bottom: 1px solid #ede8f5; background: #f9f7fc; font-size: 14px; }
  .criterion:nth-child(even) { background: #f3eff8; }
  .rating-group { display: flex; gap: 6px; }
  .rating-group label { cursor: pointer; padding: 4px 10px; border: 1px solid #c4b6dc; border-radius: 4px; background: #fff; font-size: 13px; font-weight: 600; color: #4b2e83; transition: all .15s; }
  .rating-group input { display: none; }
  .rating-group input:checked + span { background: #4b2e83; color: #fff; }
  .rating-group label:hover { background: #ede8f5; }
  .rating-group input:checked + span { display: inline-block; padding: 4px 10px; margin: -4px -10px; border-radius: 3px; }
  textarea { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 4px; font-family: inherit; font-size: 14px; resize: vertical; min-height: 60px; margin-top: 4px; }
  .feedback-row { padding: 12px 14px; background: #fff; }
  .feedback-row label { font-size: 13px; color: #555; font-weight: 600; }
  .overall { background: #ede8f5; padding: 16px; border-radius: 6px; margin-bottom: 20px; }
  .overall-rating { display: flex; gap: 10px; margin-top: 8px; }
  .overall-rating label { flex: 1; text-align: center; padding: 10px; border: 1px solid #c4b6dc; border-radius: 4px; background: #fff; cursor: pointer; font-weight: 600; color: #4b2e83; }
  .overall-rating input { display: none; }
  .overall-rating input:checked + span { display: block; }
  .overall-rating label:has(input:checked) { background: #4b2e83; color: #fff; }
  .sw-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px; }
  .sw-box { border: 1px solid #c4b6dc; border-radius: 6px; padding: 14px; }
  .sw-box h3 { margin: 0 0 10px; color: #4b2e83; font-size: 15px; }
  .sw-options { display: flex; flex-direction: column; gap: 6px; }
  .sw-options label { font-size: 14px; cursor: pointer; padding: 4px 6px; border-radius: 3px; }
  .sw-options label:hover { background: #f3eff8; }
  .sw-hint { font-size: 12px; color: #888; font-weight: 400; }
  .scale-note { font-size: 12px; color: #666; font-style: italic; text-align: center; margin: 16px 0; padding: 8px; background: #f3eff8; border-radius: 4px; }
  .actions { display: flex; gap: 10px; margin-top: 24px; flex-wrap: wrap; }
  button { padding: 12px 20px; border: none; border-radius: 6px; font-size: 14px; font-weight: 600; cursor: pointer; transition: opacity .15s; }
  .btn-primary { background: #4b2e83; color: #fff; }
  .btn-secondary { background: #fff; color: #4b2e83; border: 1px solid #4b2e83; }
  button:hover { opacity: .85; }
  .toast { position: fixed; bottom: 20px; right: 20px; background: #2d7a3f; color: #fff; padding: 12px 20px; border-radius: 6px; opacity: 0; transition: opacity .3s; pointer-events: none; }
  .toast.show { opacity: 1; }
  @media (max-width: 600px) {
    .meta, .sw-grid { grid-template-columns: 1fr; }
    .criterion { grid-template-columns: 1fr; }
    .overall-rating { flex-direction: column; }
  }
</style>
</head>
<body>
<div class="container">
  <h1>Case Interview Feedback</h1>
  <div class="subtitle">Structured feedback form for MBB-style case practice partners</div>

  <div class="meta">
    <label>Candidate name<input type="text" id="m_candidate" value="Annick"></label>
    <label>Case partner name<input type="text" id="m_partner"></label>
    <label>Date<input type="date" id="m_date"></label>
    <label>Case type
      <select id="m_type">
        <option>Market sizing</option>
        <option>Profitability</option>
        <option>Market entry</option>
        <option>M&A / investment</option>
        <option>Growth strategy</option>
        <option>Operations / cost reduction</option>
        <option>Pricing</option>
        <option>Other</option>
      </select>
    </label>
    <label>Case name / source<input type="text" id="m_casename" placeholder="e.g. Hugo Boss India market entry"></label>
    <label>Difficulty
      <select id="m_difficulty">
        <option>Easy</option>
        <option selected>Medium</option>
        <option>Hard</option>
        <option>MBB final round</option>
      </select>
    </label>
  </div>

  <div class="scale-note">Rating scale: <strong>1 = Needs improvement / coaching</strong> &nbsp;|&nbsp; <strong>2 = Good; needs some coaching</strong> &nbsp;|&nbsp; <strong>3 = Excellent</strong></div>

  <!-- Section 1 -->
  <div class="section" data-section="Case setup and structure">
    <div class="section-header"><span>Case setup and structure</span><span class="rating-label">Rating (1–3)</span></div>
    <div class="criterion"><span>Listens to the case prompt carefully; asks appropriate clarifying questions</span><div class="rating-group" data-name="s1_q1"></div></div>
    <div class="criterion"><span>Clearly understands and defines the problem/question; breaks problems into components</span><div class="rating-group" data-name="s1_q2"></div></div>
    <div class="criterion"><span>Takes a well-structured, MECE approach to solving the client's problem</span><div class="rating-group" data-name="s1_q3"></div></div>
    <div class="criterion"><span>Shows a deep/case-specific understanding of the client's problem and industry</span><div class="rating-group" data-name="s1_q4"></div></div>
    <div class="feedback-row"><label>Specific feedback<textarea data-name="s1_fb"></textarea></label></div>
  </div>

  <!-- Section 2 -->
  <div class="section" data-section="Quantitative abilities">
    <div class="section-header"><span>Quantitative abilities</span><span class="rating-label">Rating (1–3)</span></div>
    <div class="criterion"><span>Structures quantitative analyses in a clear and logical manner</span><div class="rating-group" data-name="s2_q1"></div></div>
    <div class="criterion"><span>Simplifies complex math to minimize time and possible errors in calculation</span><div class="rating-group" data-name="s2_q2"></div></div>
    <div class="criterion"><span>Performs math calculations with minimal errors</span><div class="rating-group" data-name="s2_q3"></div></div>
    <div class="criterion"><span>Sanity-checks numbers and interprets results in business terms (the "so what")</span><div class="rating-group" data-name="s2_q4"></div></div>
    <div class="feedback-row"><label>Specific feedback<textarea data-name="s2_fb"></textarea></label></div>
  </div>

  <!-- Section 3 -->
  <div class="section" data-section="Communication and team skills">
    <div class="section-header"><span>Communication and team skills</span><span class="rating-label">Rating (1–3)</span></div>
    <div class="criterion"><span>Clearly communicates ideas in a structured, top-down (Pyramid Principle) manner</span><div class="rating-group" data-name="s3_q1"></div></div>
    <div class="criterion"><span>Good listener; receives coaching and pushback in an open and thoughtful manner</span><div class="rating-group" data-name="s3_q2"></div></div>
    <div class="criterion"><span>Projects confidence when providing recommendations and solutions</span><div class="rating-group" data-name="s3_q3"></div></div>
    <div class="criterion"><span>Friendly and personable in case discussions; appears relaxed and confident</span><div class="rating-group" data-name="s3_q4"></div></div>
    <div class="feedback-row"><label>Specific feedback<textarea data-name="s3_fb"></textarea></label></div>
  </div>

  <!-- Section 4 -->
  <div class="section" data-section="Business acumen and creativity">
    <div class="section-header"><span>Business acumen and creativity</span><span class="rating-label">Rating (1–3)</span></div>
    <div class="criterion"><span>Demonstrates strong business acumen in structuring client analyses</span><div class="rating-group" data-name="s4_q1"></div></div>
    <div class="criterion"><span>Drives the discussion in a hypothesis-driven and logical manner</span><div class="rating-group" data-name="s4_q2"></div></div>
    <div class="criterion"><span>Provides numerous creative solutions to client problems; structures brainstorms</span><div class="rating-group" data-name="s4_q3"></div></div>
    <div class="criterion"><span>Shows strong business judgment and pragmatism when making recommendations</span><div class="rating-group" data-name="s4_q4"></div></div>
    <div class="feedback-row"><label>Specific feedback<textarea data-name="s4_fb"></textarea></label></div>
  </div>

  <!-- Overall -->
  <div class="overall">
    <strong>Overall rating of the candidate based on the case</strong>
    <div class="overall-rating" id="overall">
      <label><input type="radio" name="overall" value="Needs improvement"><span>Needs improvement</span></label>
      <label><input type="radio" name="overall" value="Good"><span>Good</span></label>
      <label><input type="radio" name="overall" value="Excellent"><span>Excellent</span></label>
    </div>
  </div>

  <div class="sw-grid">
    <div class="sw-box">
      <h3>Top strengths <span class="sw-hint">(select 2)</span></h3>
      <div class="sw-options" id="strengths">
        <label><input type="checkbox" value="Framework / structure"> Framework / structure</label>
        <label><input type="checkbox" value="Analytics / data interpretation"> Analytics / data interpretation</label>
        <label><input type="checkbox" value="Qualitative analysis"> Qualitative analysis</label>
        <label><input type="checkbox" value="Synthesizing"> Synthesizing</label>
        <label><input type="checkbox" value="Creativity / insights"> Creativity / insights</label>
        <label><input type="checkbox" value="Driving the case"> Driving the case</label>
        <label><input type="checkbox" value="Conclusion / recommendation"> Conclusion / recommendation</label>
        <label><input type="checkbox" value="Communication / executive presence"> Communication / executive presence</label>
      </div>
    </div>
    <div class="sw-box">
      <h3>Top areas to improve <span class="sw-hint">(select 2)</span></h3>
      <div class="sw-options" id="weaknesses">
        <label><input type="checkbox" value="Framework / structure"> Framework / structure</label>
        <label><input type="checkbox" value="Analytics / data interpretation"> Analytics / data interpretation</label>
        <label><input type="checkbox" value="Qualitative analysis"> Qualitative analysis</label>
        <label><input type="checkbox" value="Synthesizing"> Synthesizing</label>
        <label><input type="checkbox" value="Creativity / insights"> Creativity / insights</label>
        <label><input type="checkbox" value="Driving the case"> Driving the case</label>
        <label><input type="checkbox" value="Conclusion / recommendation"> Conclusion / recommendation</label>
        <label><input type="checkbox" value="Communication / executive presence"> Communication / executive presence</label>
      </div>
    </div>
  </div>

  <div class="feedback-row" style="background:#f9f7fc;border:1px solid #e0d9ec;border-radius:6px;">
    <label>One specific thing to practice before the next case
      <textarea id="practice"></textarea>
    </label>
  </div>

  <div class="feedback-row" style="background:#f9f7fc;border:1px solid #e0d9ec;border-radius:6px;margin-top:10px;">
    <label>Any other specific feedback
      <textarea id="other_fb" style="min-height:90px;"></textarea>
    </label>
  </div>

  <div class="actions">
    <button class="btn-primary" onclick="copyResults()">Copy feedback to clipboard</button>
    <button class="btn-secondary" onclick="downloadResults()">Download as .txt</button>
    <button class="btn-secondary" onclick="if(confirm('Clear all fields?')) location.reload()">Reset form</button>
  </div>
</div>

<div class="toast" id="toast">Copied!</div>

<script>
  // Build rating buttons
  document.querySelectorAll('.rating-group').forEach(group => {
    const name = group.dataset.name;
    [1,2,3].forEach(n => {
      const lbl = document.createElement('label');
      lbl.innerHTML = `<input type="radio" name="${name}" value="${n}"><span>${n}</span>`;
      group.appendChild(lbl);
    });
  });

  // Set today's date
  document.getElementById('m_date').valueAsDate = new Date();

  // Limit strengths/weaknesses to 2
  function limitTwo(containerId) {
    const boxes = document.querySelectorAll(`#${containerId} input[type=checkbox]`);
    boxes.forEach(cb => cb.addEventListener('change', () => {
      const checked = [...boxes].filter(b => b.checked);
      if (checked.length > 2) cb.checked = false;
    }));
  }
  limitTwo('strengths');
  limitTwo('weaknesses');

  function getRating(name) {
    const sel = document.querySelector(`input[name="${name}"]:checked`);
    return sel ? sel.value : '—';
  }
  function getText(name) {
    const el = document.querySelector(`textarea[data-name="${name}"]`);
    return el ? (el.value.trim() || '—') : '—';
  }
  function getChecked(id) {
    return [...document.querySelectorAll(`#${id} input:checked`)].map(c => c.value).join(', ') || '—';
  }

  function buildReport() {
    const sections = [
      { name: 'Case setup and structure', prefix: 's1', qs: [
        'Listens to prompt; asks clarifying questions',
        'Defines the problem; breaks into components',
        'Well-structured, MECE approach',
        'Case-specific understanding of client/industry'
      ]},
      { name: 'Quantitative abilities', prefix: 's2', qs: [
        'Structures quant analyses clearly',
        'Simplifies complex math',
        'Math accuracy',
        'Sanity-checks and interprets results'
      ]},
      { name: 'Communication and team skills', prefix: 's3', qs: [
        'Top-down, structured communication',
        'Listens; receives coaching openly',
        'Confident recommendations',
        'Personable and relaxed'
      ]},
      { name: 'Business acumen and creativity', prefix: 's4', qs: [
        'Business acumen in analyses',
        'Hypothesis-driven discussion',
        'Creative, structured brainstorms',
        'Business judgment and pragmatism'
      ]}
    ];

    let out = '';
    out += 'CASE INTERVIEW FEEDBACK\n';
    out += '========================\n\n';
    out += `Candidate:   ${document.getElementById('m_candidate').value || '—'}\n`;
    out += `Partner:     ${document.getElementById('m_partner').value || '—'}\n`;
    out += `Date:        ${document.getElementById('m_date').value || '—'}\n`;
    out += `Case type:   ${document.getElementById('m_type').value}\n`;
    out += `Case name:   ${document.getElementById('m_casename').value || '—'}\n`;
    out += `Difficulty:  ${document.getElementById('m_difficulty').value}\n\n`;
    out += 'Scale: 1 = Needs improvement, 2 = Good, 3 = Excellent\n\n';

    sections.forEach(s => {
      out += `--- ${s.name.toUpperCase()} ---\n`;
      s.qs.forEach((q, i) => {
        out += `  [${getRating(s.prefix + '_q' + (i+1))}]  ${q}\n`;
      });
      out += `  Feedback: ${getText(s.prefix + '_fb')}\n\n`;
    });

    const overall = document.querySelector('input[name=overall]:checked');
    out += `OVERALL RATING:  ${overall ? overall.value : '—'}\n\n`;
    out += `Top strengths:        ${getChecked('strengths')}\n`;
    out += `Areas to improve:     ${getChecked('weaknesses')}\n\n`;
    out += `One thing to practice next: ${document.getElementById('practice').value.trim() || '—'}\n\n`;
    out += `Other feedback:\n${document.getElementById('other_fb').value.trim() || '—'}\n`;

    return out;
  }

  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(() => t.classList.remove('show'), 1800);
  }

  function copyResults() {
    const text = buildReport();
    navigator.clipboard.writeText(text).then(
      () => showToast('Copied to clipboard!'),
      () => {
        // fallback
        const ta = document.createElement('textarea');
        ta.value = text;
        document.body.appendChild(ta);
        ta.select();
        document.execCommand('copy');
        document.body.removeChild(ta);
        showToast('Copied!');
      }
    );
  }

  function downloadResults() {
    const text = buildReport();
    const candidate = (document.getElementById('m_candidate').value || 'candidate').replace(/\s+/g,'_');
    const date = document.getElementById('m_date').value || 'undated';
    const blob = new Blob([text], {type: 'text/plain'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `case_feedback_${candidate}_${date}.txt`;
    a.click();
    URL.revokeObjectURL(url);
  }
</script>
</body>
</html>
