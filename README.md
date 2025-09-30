[quiz_sholat_gerhana.html](https://github.com/user-attachments/files/22616240/quiz_sholat_gerhana.html)
<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>CBT - Sholat Gerhana</title>
  <style>
    :root{
      --accent:#0ea5a4;
      --bg:#0f172a;
      --card:#0b1220;
      --muted:#94a3b8;
      --success:#16a34a;
      --danger:#ef4444;
      --glass: rgba(255,255,255,0.03);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:linear-gradient(180deg,#071025 0%, #0b1220 100%);color:#e6eef8}
    .app{max-width:1100px;margin:28px auto;padding:20px;display:grid;grid-template-columns:320px 1fr;gap:20px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;padding:18px;box-shadow:0 6px 20px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}
    .sidebar{position:sticky;top:24px;height:calc(100vh - 48px);overflow:auto}
    h1{font-size:20px;margin:0 0 8px 0}
    .meta{color:var(--muted);font-size:13px;margin-bottom:12px}
    .timer{font-weight:700;color:var(--accent);font-size:18px}
    .qnav{display:grid;grid-template-columns:repeat(5,1fr);gap:8px;margin-top:12px}
    .qnav button{padding:8px;border-radius:8px;border:0;background:var(--glass);color:var(--muted);cursor:pointer}
    .qnav button.current{outline:2px solid rgba(14,165,164,0.18);background:rgba(14,165,164,0.06);color:#fff}
    .qnav button.answered{background:linear-gradient(90deg,#06303a,#08323a);color:#b8fff0}
    .start-area{text-align:center;padding-top:10px}
    .start-area button{background:var(--accent);border:0;padding:10px 14px;border-radius:10px;color:#05201f;font-weight:700;cursor:pointer}
    .content{min-height:520px;display:flex;flex-direction:column}
    .topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
    .question-area{flex:1;padding:12px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.005));border:1px solid rgba(255,255,255,0.02)}
    .qtext{font-size:18px;margin-bottom:8px}
    .opts{display:flex;flex-direction:column;gap:8px}
    .opt{padding:12px;border-radius:8px;border:1px solid rgba(255,255,255,0.03);background:transparent;cursor:pointer;text-align:left}
    .opt input{margin-right:10px}
    .controls{display:flex;justify-content:space-between;margin-top:12px;gap:10px}
    .controls button{padding:10px 12px;border-radius:8px;border:0;background:#0ea5a4;color:#022;cursor:pointer;font-weight:700}
    .controls .secondary{background:transparent;color:var(--muted);border:1px solid rgba(255,255,255,0.03)}
    footer{margin-top:14px;color:var(--muted);font-size:13px;text-align:center}
    .result{padding:14px;border-radius:10px;background:linear-gradient(90deg,#062017,#07323a);color:#dffbf6}
    .hidden{display:none}
    .download-btn{background:linear-gradient(90deg,#06b6d4,#06b6b4);border:0;color:#012;padding:10px 12px;border-radius:8px;cursor:pointer;font-weight:700}
    .top-progress{height:8px;background:rgba(255,255,255,0.03);border-radius:8px;overflow:hidden}
    .top-progress > i{display:block;height:100%;background:linear-gradient(90deg,#06b6d4,#0ea5a4);width:0%}
    @media(max-width:880px){.app{grid-template-columns:1fr; padding:12px}.sidebar{position:relative;height:auto}}
  </style>
</head>
<body>
  <div class="app">
    <aside class="card sidebar">
      <h1>CBT: Sholat Gerhana</h1>
      <div class="meta">Guru: <strong>—</strong> • Kelas: <strong>SMP</strong></div>
      <div>Durasi: <strong id="durationText">25</strong> menit</div>
      <div style="margin-top:8px">Timer: <div class="timer" id="timer">00:00</div></div>
      <div style="margin-top:12px">Navigasi Soal</div>
      <div class="qnav" id="qnav"></div>
      <div class="start-area" style="margin-top:14px">
        <button id="btnStart">Mulai Ujian</button>
      </div>
      <div style="margin-top:18px">
        <div style="font-size:13px;color:var(--muted)">Keterangan</div>
        <div style="margin-top:8px;color:var(--muted);font-size:13px">
          • Pilihan ganda & benar/salah bernilai 1 poin.<br/>
          • Isian singkat dinilai otomatis jika cocok jawaban. <br/>
          • Hasil dapat diunduh dalam format CSV (Excel).
        </div>
      </div>
    </aside>

    <main class="card content">
      <div class="topbar">
        <div class="top-progress" style="width:50%">
          <i id="progressBar"></i>
        </div>
        <div>
          <button class="secondary download-btn" id="btnExport" style="display:none">Download Hasil (CSV)</button>
          <button class="secondary" id="btnReview" style="display:none">Tampilkan Jawaban</button>
        </div>
      </div>

      <div class="question-area" id="questionArea">
        <div style="text-align:center;color:var(--muted);padding-top:40px">
          <p style="font-size:18px">Selamat datang di CBT Sholat Gerhana</p>
          <p style="max-width:680px;margin:8px auto;color:var(--muted)">Tekan <strong>Mulai Ujian</strong> untuk memulai. Aplikasi ini offline, bisa diunggah ke hosting (GitHub Pages / Netlify) lalu dibagikan melalui link.</p>
        </div>
      </div>

      <div class="controls" style="display:none" id="controls">
        <button class="secondary" id="prevBtn">Sebelumnya</button>
        <div style="display:flex;gap:8px">
          <button class="secondary" id="saveBtn">Simpan Jawaban</button>
          <button id="nextBtn">Selanjutnya</button>
          <button class="secondary" id="submitBtn" title="Akhiri dan submit ujian">Kumpulkan</button>
        </div>
      </div>

      <footer>Versi CBT sederhana • Simpan file -> upload ke hosting untuk membagikan link</footer>
    </main>
  </div>

<script>
const durationMinutes = 25; // default duration
document.getElementById('durationText').innerText = durationMinutes;

const questions = [
  // 1-10 multiple choice
  {type:'mcq', q:"Apa yang dimaksud dengan sholat gerhana?", choices:["Sholat sunnah karena hujan","Sholat sunnah ketika terjadi gerhana matahari atau bulan","Sholat sunnah karena bencana alam","Sholat sunnah ketika mendapat rezeki"], a:1},
  {type:'mcq', q:"Sholat gerhana disebut juga dengan istilah…", choices:["Istisqa dan Khusuf","Kusuf dan Khusuf","Tahajjud dan Dhuha","Qiyamul Lail"], a:1},
  {type:'mcq', q:"Gerhana matahari dalam istilah Arab disebut…", choices:["Khusuf","Kusuf","Istisqa","Tarawih"], a:1},
  {type:'mcq', q:"Gerhana bulan dalam istilah Arab disebut…", choices:["Khusuf","Kusuf","Istisqa","Witir"], a:1},
  {type:'mcq', q:"Hukum sholat gerhana adalah…", choices:["Fardhu ‘ain","Sunnah muakkadah","Wajib","Fardhu kifayah"], a:1},
  {type:'mcq', q:"Jumlah rakaat sholat gerhana adalah…", choices:["2 rakaat","4 rakaat","3 rakaat","5 rakaat"], a:1},
  {type:'mcq', q:"Dalam satu rakaat sholat gerhana terdapat…", choices:["1 ruku’","2 ruku’","3 ruku’","4 ruku’"], a:2},
  {type:'mcq', q:"Sholat gerhana sebaiknya dilaksanakan di…", choices:["Rumah","Masjid secara berjamaah","Sekolah","Pasar"], a:1},
  {type:'mcq', q:"Bacaan surat dalam sholat gerhana sebaiknya…", choices:["Surat-surat pendek","Surat panjang dengan suara keras","Surat pendek dengan suara pelan","Surat bebas"], a:1},
  {type:'mcq', q:"Hikmah dari sholat gerhana adalah…", choices:["Menunjukkan kehebatan manusia","Mengingatkan bahwa semua fenomena adalah tanda kebesaran Allah","Menghindari bencana","Menambah rezeki"], a:1},

  // 11-15 true/false
  {type:'tf', q:"Gerhana matahari terjadi karena bumi berada di antara bulan dan matahari.", a:false},
  {type:'tf', q:"Sholat gerhana boleh dikerjakan sendiri atau berjamaah.", a:true},
  {type:'tf', q:"Sholat gerhana dilakukan 4 rakaat dengan 4 kali salam.", a:false},
  {type:'tf', q:"Pada setiap rakaat sholat gerhana terdapat 2 kali ruku’.", a:true},
  {type:'tf', q:"Imam membaca surat dengan suara keras pada sholat gerhana bulan.", a:false},

  // 16-20 short answer
  {type:'short', q:"Sholat gerhana bulan disebut sholat ______.", a:"kusuf"},
  {type:'short', q:"Sholat gerhana matahari disebut sholat ______.", a:"khusuf"},
  {type:'short', q:"Rasulullah SAW melaksanakan sholat gerhana sebanyak ____ rakaat.", a:"2"},
  {type:'short', q:"Hikmah sholat gerhana adalah agar manusia selalu mengingat ______.", a:"kebesaran Allah"},
  {type:'short', q:"Dalam sholat gerhana, khutbah dilakukan setelah ______.", a:"shalat"}
];

let state = {
  current:0,
  answers: Array(questions.length).fill(null),
  started:false,
  timeLeft: durationMinutes * 60,
  intervalId: null,
  submitted:false
};

function buildNav(){
  const nav = document.getElementById('qnav');
  nav.innerHTML='';
  questions.forEach((_,i)=>{
    const btn=document.createElement('button');
    btn.innerText = (i+1);
    btn.id='nav-'+i;
    btn.addEventListener('click',()=>goTo(i));
    nav.appendChild(btn);
  });
}
function goTo(i){
  state.current = i;
  renderQuestion();
  updateNav();
}
function updateNav(){
  questions.forEach((_,i)=>{
    const btn = document.getElementById('nav-'+i);
    btn.classList.toggle('current', i===state.current);
    btn.classList.toggle('answered', state.answers[i] !== null);
  });
  const pct = Math.round((state.answers.filter(x=>x!==null).length / questions.length)*100);
  document.getElementById('progressBar').style.width = pct + '%';
}

function renderQuestion(){
  const qa = questions[state.current];
  const area = document.getElementById('questionArea');
  area.innerHTML = '';
  const top = document.createElement('div');
  top.className='qheader';
  top.innerHTML = '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px"><div style="font-size:13px;color:var(--muted)">Soal '+(state.current+1)+' dari '+questions.length+'</div><div style="font-size:13px;color:var(--muted)">Tipe: '+qa.type.toUpperCase()+'</div></div>';
  area.appendChild(top);

  const qbox = document.createElement('div');
  qbox.innerHTML = '<div class="qtext">'+escapeHtml(qa.q)+'</div>';
  const body = document.createElement('div');
  body.className='opts';
  if(qa.type==='mcq'){
    qa.choices.forEach((c,idx)=>{
      const div = document.createElement('label');
      div.className='opt';
      div.innerHTML = '<input type="radio" name="opt" value="'+idx+'"> <span>'+escapeHtml(c)+'</span>';
      div.addEventListener('click', (e)=>{
        const val = idx;
        state.answers[state.current] = {type:'mcq', value:val};
        updateNav();
      });
      body.appendChild(div);
    });
    // restore previous
    const prev = state.answers[state.current];
    if(prev && prev.type==='mcq'){
      setTimeout(()=>{ const radios = body.querySelectorAll('input'); if(radios[prev.value]) radios[prev.value].checked=true },10);
    }
  } else if(qa.type==='tf'){
    ['Benar','Salah'].forEach((t,idx)=>{
      const div = document.createElement('label');
      div.className='opt';
      div.innerHTML = '<input type="radio" name="opt" value="'+(idx===0)+'"> <span>'+t+'</span>';
      div.addEventListener('click', ()=>{
        state.answers[state.current] = {type:'tf', value: idx===0};
        updateNav();
      });
      body.appendChild(div);
    });
    const prev = state.answers[state.current];
    if(prev && prev.type==='tf'){
      setTimeout(()=>{ const radios = body.querySelectorAll('input'); radios[prev.value?0:1].checked=true },10);
    }
  } else if(qa.type==='short'){
    const inp = document.createElement('input');
    inp.type='text';
    inp.placeholder='Tulis jawaban singkat...';
    inp.style.width='100%';
    inp.style.padding='10px';
    inp.style.borderRadius='8px';
    inp.style.border='1px solid rgba(255,255,255,0.03)';
    inp.value = (state.answers[state.current] && state.answers[state.current].value) || '';
    inp.addEventListener('input', ()=> {
      state.answers[state.current] = {type:'short', value: inp.value};
      updateNav();
    });
    body.appendChild(inp);
  }

  qbox.appendChild(body);
  area.appendChild(qbox);
}

function escapeHtml(s){
  return String(s).replace(/[&<>"']/g,function(m){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]});
}

document.getElementById('btnStart').addEventListener('click', startExam);
document.getElementById('nextBtn').addEventListener('click', ()=>{ if(state.current < questions.length-1) goTo(state.current+1); });
document.getElementById('prevBtn').addEventListener('click', ()=>{ if(state.current > 0) goTo(state.current-1); });
document.getElementById('saveBtn').addEventListener('click', ()=>{ alert('Jawaban sementara disimpan pada sesi ini.') });
document.getElementById('submitBtn').addEventListener('click', ()=>{ if(confirm('Yakin ingin mengumpulkan?')) submitExam(); });
document.getElementById('btnExport').addEventListener('click', exportCSV);
document.getElementById('btnReview').addEventListener('click', showReview);

function startExam(){
  if(state.started) return;
  state.started = true;
  document.getElementById('btnStart').style.display='none';
  document.getElementById('controls').style.display='flex';
  document.getElementById('btnExport').style.display='none';
  buildNav();
  goTo(0);
  state.timeLeft = durationMinutes * 60;
  updateTimerDisplay();
  state.intervalId = setInterval(()=>{
    state.timeLeft--;
    updateTimerDisplay();
    if(state.timeLeft <= 0){ clearInterval(state.intervalId); submitExam(); }
  },1000);
}

function updateTimerDisplay(){
  const m = Math.floor(state.timeLeft/60).toString().padStart(2,'0');
  const s = (state.timeLeft%60).toString().padStart(2,'0');
  document.getElementById('timer').innerText = m+':'+s;
}

function grade(){
  let score = 0;
  const details = [];
  questions.forEach((q,i)=>{
    const ans = state.answers[i];
    let correct=false;
    if(!ans){ correct=false; }
    else if(q.type==='mcq'){
      correct = ans.value === q.a;
      if(correct) score+=1;
    } else if(q.type==='tf'){
      correct = (ans.value === q.a);
      if(correct) score+=1;
    } else if(q.type==='short'){
      const got = (ans.value || '').trim().toLowerCase();
      const want = (q.a || '').toString().trim().toLowerCase();
      // simple matching, allow answer variations for certain items
      let ok = false;
      if(got === want) ok = true;
      else {
        // some simple synonyms
        const synonyms = {
          "kebesaran allah":["kebesaran allah","kebesaran tuhan","kebesaran Allah"],
          "kusuf":["kusuf"],
          "khusuf":["khusuf"],
          "2":["2","dua"]
        };
        for(const k in synonyms){
          if(synonyms[k].includes(got)) { if(want.includes(k) || synonyms[k].includes(want)) ok=true; }
        }
      }
      correct = ok;
      if(correct) score+=1;
    }
    details.push({no:i+1, type:q.type, correct:correct, given: ans?ans.value:null});
  });
  return {score, total: questions.length, details};
}

function submitExam(){
  if(state.submitted) return;
  state.submitted = true;
  clearInterval(state.intervalId);
  const res = grade();
  const area = document.getElementById('questionArea');
  area.innerHTML = '';
  const out = document.createElement('div');
  out.className='result';
  out.innerHTML = '<h2>Hasil Ujian</h2><p>Skor: <strong>'+res.score+'</strong> dari '+res.total+'</p><p style="color:var(--muted)">Persentase: <strong>'+Math.round((res.score/res.total)*100)+'%</strong></p>';
  const tableWrap = document.createElement('div');
  tableWrap.style.marginTop='12px';
  const tbl = document.createElement('table');
  tbl.style.width='100%';
  tbl.style.borderCollapse='collapse';
  tbl.innerHTML = '<thead><tr style="text-align:left"><th>No</th><th>Soal</th><th>Jenis</th><th>Dijawab</th><th>Benar?</th></tr></thead>';
  const tb = document.createElement('tbody');
  res.details.forEach(d=>{
    const tr = document.createElement('tr');
    tr.innerHTML = '<td style="padding:6px 8px;border-top:1px solid rgba(255,255,255,0.03)">'+d.no+'</td><td style="padding:6px 8px;border-top:1px solid rgba(255,255,255,0.03)">'+escapeHtml(questions[d.no-1].q)+'</td><td style="padding:6px 8px;border-top:1px solid rgba(255,255,255,0.03)">'+d.type+'</td><td style="padding:6px 8px;border-top:1px solid rgba(255,255,255,0.03)">'+escapeHtml(String(d.given))+'</td><td style="padding:6px 8px;border-top:1px solid rgba(255,255,255,0.03)">'+(d.correct?'<span style="color:var(--success)">Benar</span>':'<span style="color:var(--danger)">Salah</span>')+'</td>';
    tb.appendChild(tr);
  });
  tbl.appendChild(tb);
  tableWrap.appendChild(tbl);
  out.appendChild(tableWrap);

  const btnArea = document.createElement('div');
  btnArea.style.marginTop='12px';
  const btnExport = document.getElementById('btnExport');
  btnExport.style.display='inline-block';
  document.getElementById('btnReview').style.display='inline-block';
  out.appendChild(btnArea);
  area.appendChild(out);

  // prepare result data for export
  state.latestResult = res;
  // auto-scroll to top
  window.scrollTo({top:0,behavior:'smooth'});
}

function exportCSV(){
  if(!state.submitted){
    alert('Silakan kumpulkan ujian terlebih dahulu.');
    return;
  }
  const res = state.latestResult;
  const rows = [];
  rows.push(['No','Soal','Jenis','Jawaban','Benar']);
  res.details.forEach(d=>{
    rows.push([d.no, questions[d.no-1].q, d.type, String(d.given), d.correct ? 'Benar' : 'Salah']);
  });
  rows.push([]);
  rows.push(['Skor', res.score+'/'+res.total]);
  const csv = rows.map(r=>r.map(cell=>'"'+String(cell).replace(/"/g,'""')+'"').join(',')).join('\\n');
  const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  const now = new Date();
  const fname = 'hasil_cbt_sholat_gerhana_'+now.getFullYear()+(now.getMonth()+1).toString().padStart(2,'0')+now.getDate().toString().padStart(2,'0')+'.csv';
  a.download = fname;
  document.body.appendChild(a);
  a.click();
  a.remove();
}

function showReview(){
  if(!state.submitted) return;
  const area = document.getElementById('questionArea');
  area.innerHTML = '';
  const wrap = document.createElement('div');
  wrap.innerHTML = '<h2>Review Jawaban</h2>';
  const ul = document.createElement('div');
  ul.style.marginTop='12px';
  state.latestResult.details.forEach(d=>{
    const card = document.createElement('div');
    card.style.padding='10px';
    card.style.borderRadius='8px';
    card.style.marginBottom='8px';
    card.style.background='rgba(255,255,255,0.02)';
    card.innerHTML = '<div style="font-weight:700">Soal '+d.no+'</div><div style="margin-top:6px">'+escapeHtml(questions[d.no-1].q)+'</div><div style="margin-top:6px;color:var(--muted)">Jawaban Anda: <strong>'+escapeHtml(String(d.given))+'</strong></div><div style="color:'+(d.correct? '#78f6be':'#ff9e9e')+'">Status: '+(d.correct? 'Benar':'Salah')+'</div><div style="margin-top:6px;color:var(--muted)">Kunci: <strong>'+(questions[d.no-1].a !== undefined ? String(questions[d.no-1].a) : '')+'</strong></div>';
    ul.appendChild(card);
  });
  wrap.appendChild(ul);
  area.appendChild(wrap);
}

// initial
buildNav();
updateNav();
</script>
</body>
</html>
