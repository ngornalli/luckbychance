<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Luck By Chance — 50 Categories</title>
  <style>
    :root{
      --bg:#0f172a; --bg-accent:#111827; --card:#111827; --text:#e5e7eb; --muted:#9ca3af;
      --accent:#22c55e; --accent-2:#60a5fa; --danger:#ef4444; --shadow:0 20px 40px rgba(0,0,0,.35); --radius:16px;
    }
    @media (prefers-color-scheme: light){
      :root{
        --bg:#f3f4f6; --bg-accent:#e5e7eb; --card:#fff; --text:#0f172a; --muted:#475569;
        --accent:#16a34a; --accent-2:#2563eb; --danger:#dc2626; --shadow:0 10px 30px rgba(0,0,0,.08);
      }
    }
    *{box-sizing:border-box}
    body{
      margin:0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial;
      background:
        radial-gradient(1200px 600px at 20% -10%, rgba(96,165,250,0.15), transparent 60%),
        radial-gradient(1200px 600px at 120% 10%, rgba(34,197,94,0.15), transparent 60%),
        var(--bg);
      color:var(--text); min-height:100vh; display:flex; align-items:center; justify-content:center; padding:24px;
    }
    .wrap{ width:min(900px,100%); }
    header{ display:flex; align-items:center; justify-content:space-between; gap:16px; margin-bottom:16px; }
    .title{ font-size:clamp(20px,3vw,28px); font-weight:700; }
    .round{ font-size:14px; color:var(--muted); }
    .card{
      background:linear-gradient(180deg,var(--card),var(--bg-accent));
      border-radius:var(--radius); box-shadow:var(--shadow); padding:clamp(18px,3.5vw,28px);
      border:1px solid rgba(255,255,255,0.06);
    }
    .badge{
      display:inline-flex; align-items:center; gap:8px; padding:6px 12px; border-radius:999px;
      background:linear-gradient(180deg, rgba(96,165,250,0.18), rgba(96,165,250,0.08));
      color:var(--accent-2); font-weight:600; font-size:12px; letter-spacing:.3px; text-transform:uppercase;
      border:1px solid rgba(96,165,250,0.35);
    }
    .content{ margin-top:16px; }
    .prompt{ font-size:clamp(20px,3vw,26px); font-weight:700; margin:10px 0 6px; }
    .reveal{ display:grid; gap:10px; margin-top:12px; }
    .hint,.answer{
      border:1px dashed rgba(255,255,255,0.18); background:rgba(255,255,255,0.04);
      padding:14px 16px; border-radius:12px;
    }
    .hint h3,.answer h3{ margin:0 0 6px 0; font-size:14px; color:var(--muted); font-weight:700; letter-spacing:.3px; text-transform:uppercase; }
    .hint p,.answer p{ margin:0; font-size:clamp(16px,2.4vw,20px); }
    .hint.hidden,.answer.hidden{ display:none; }
    .controls{ display:flex; flex-wrap:wrap; gap:10px; margin-top:18px; }
    button{
      appearance:none; border:none; cursor:pointer; padding:12px 16px; border-radius:12px; font-weight:700;
      color:white; background:#374151; transition:transform .04s ease, filter .2s ease, background .2s ease;
      border:1px solid rgba(255,255,255,0.08);
    }
    button.primary{ background:linear-gradient(180deg,var(--accent),#15803d); }
    button.alt{ background:linear-gradient(180deg,var(--accent-2),#1d4ed8); }
    button.ghost{ background:transparent; color:var(--muted); border:1px dashed rgba(255,255,255,0.25); }
    button:disabled{ opacity:.6; cursor:not-allowed; filter:grayscale(.2); }
    button:active{ transform:translateY(1px); }
    .footer{ display:flex; align-items:center; justify-content:space-between; gap:10px; margin-top:14px; color:var(--muted); font-size:12px; }
    .steps{ display:flex; align-items:center; gap:6px; }
    .dot{ width:10px; height:10px; border-radius:999px; background:#374151; border:1px solid rgba(255,255,255,0.12); box-shadow: inset 0 0 0 2px rgba(0,0,0,0.15); }
    .dot.on{ background:var(--accent); border-color:rgba(34,197,94,0.8); }
    .dot.ans{ background:#f59e0b; border-color:rgba(245,158,11,0.8); }
    .grid{ display:grid; grid-template-columns:1fr auto; gap:14px; align-items:center; }
    select{ padding:10px 12px; border-radius:10px; background:rgba(255,255,255,0.05); color:var(--text); border:1px solid rgba(255,255,255,0.12); font-weight:600; }
    .sr{ position:absolute; left:-10000px; top:auto; width:1px; height:1px; overflow:hidden; }
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div>
        <div class="title">Luck By Chance — 50 Categories</div>
        <div class="round" id="roundInfo">Round 1 of 50</div>
      </div>
      <div class="grid">
        <label for="jump" class="sr">Jump to question</label>
        <select id="jump"></select>
        <button id="randomBtn" class="alt" title="Pick a random question">Random</button>
      </div>
    </header>

    <div class="card">
      <span class="badge" id="categoryBadge">Category</span>

      <div class="content">
        <div class="prompt" id="promptText"></div>

        <div class="reveal">
          <div class="hint hidden" id="hint1">
            <h3>Hint 1</h3>
            <p id="hint1Text"></p>
          </div>
          <div class="hint hidden" id="hint2">
            <h3>Hint 2</h3>
            <p id="hint2Text"></p>
          </div>
          <div class="answer hidden" id="answer">
            <h3>Answer</h3>
            <p id="answerText"></p>
          </div>
        </div>

        <div class="controls">
          <button id="revealBtn" class="primary">Reveal next (Space)</button>
          <button id="resetBtn" class="ghost">Reset reveals</button>
          <button id="prevBtn">Previous (←)</button>
          <button id="nextBtn">Next (→)</button>
          <button id="shuffleBtn" class="ghost" title="Shuffle all questions">Shuffle order</button>
        </div>

        <div class="footer">
          <div class="steps" aria-label="Reveal progress">
            <div class="dot" id="dotPrompt" title="Prompt"></div>
            <div class="dot" id="dotHint1" title="Hint 1"></div>
            <div class="dot" id="dotHint2" title="Hint 2"></div>
            <div class="dot" id="dotAnswer" title="Answer"></div>
          </div>
          <div>Tip: Space to reveal, ←/→ to navigate</div>
        </div>
      </div>
    </div>
  </div>

  <!-- Embedded questions JSON -->
  <script type="application/json" id="questions-data">
  [
    {"id":1,"category":"Bollywood Song","prompt":"Guess the Bollywood song title.","hints":["Romantic ballad from 2013.","Sung by Arijit Singh; featured in Aashiqui 2."],"answer":"Tum Hi Ho"},
    {"id":2,"category":"Bollywood Character","prompt":"Guess the iconic Bollywood character.","hints":["Lovable Mumbai goon known for 'jaadu ki jhappi'.","Played by Sanjay Dutt in an MBBS-themed comedy."],"answer":"Munna Bhai"},
    {"id":3,"category":"Anil Kapoor Film","prompt":"Guess the Anil Kapoor movie.","hints":["Invisibility device plays a key role.","Features the line 'Mogambo khush hua!'"],"answer":"Mr. India"},
    {"id":4,"category":"Madhuri Dixit Film","prompt":"Guess the Madhuri Dixit movie.","hints":["Family musical by Sooraj Barjatya.","Co-stars Salman Khan; released in 1994."],"answer":"Hum Aapke Hain Koun..!"},
    {"id":5,"category":"Brand","prompt":"Guess the Indian brand.","hints":["Dairy cooperative from Gujarat.","Tagline: 'Utterly Butterly'."],"answer":"Amul"},
    {"id":6,"category":"Freedom Fighter","prompt":"Guess the Indian freedom fighter.","hints":["Associated with HSRA.","Executed in 1931 along with Rajguru and Sukhdev."],"answer":"Bhagat Singh"},
    {"id":7,"category":"Sport","prompt":"Guess the sport.","hints":["Players raid while chanting without a breath.","Popularized by a Pro league in India."],"answer":"Kabaddi"},
    {"id":8,"category":"Indian Festival","prompt":"Guess the Indian festival.","hints":["Known as the Festival of Lights.","Lakshmi Puja is performed."],"answer":"Diwali"},
    {"id":9,"category":"Salesforce Feature","prompt":"Guess the Salesforce feature.","hints":["Declarative automation builder.","Successor to many Workflow Rules/Process Builder use-cases."],"answer":"Flow"},
    {"id":10,"category":"IT Company","prompt":"Guess the Indian IT company.","hints":["Founded by N. R. Narayana Murthy.","Headquartered in Bengaluru."],"answer":"Infosys"},
    {"id":11,"category":"Bike Model","prompt":"Guess the bike model.","hints":["Iconic Indian single-cylinder thump.","A timeless Royal Enfield cruiser."],"answer":"Royal Enfield Classic 350"},
    {"id":12,"category":"Car Model","prompt":"Guess the car model.","hints":["Compact SUV from an Indian automaker.","Also sold as an EV variant."],"answer":"Tata Nexon"},
    {"id":13,"category":"Cricketer","prompt":"Guess the Indian cricketer.","hints":["Nicknamed 'King' for batting prowess.","Former India captain with many ODI and T20 records."],"answer":"Virat Kohli"},
    {"id":14,"category":"Indian Monument","prompt":"Guess the Indian monument.","hints":["Tallest brick minaret.","Located in Delhi."],"answer":"Qutub Minar"},
    {"id":15,"category":"Indian State Capital","prompt":"Guess the Indian state capital city.","hints":["Known as the City of Nawabs.","Capital of Uttar Pradesh."],"answer":"Lucknow"},
    {"id":16,"category":"Indian River","prompt":"Guess the Indian river.","hints":["Considered holy by millions.","Empties into the Bay of Bengal via a vast delta."],"answer":"Ganga"},
    {"id":17,"category":"Yoga Pose","prompt":"Guess the yoga pose (asana).","hints":["One-legged balance posture.","Named after a tree."],"answer":"Vrikshasana (Tree Pose)"},
    {"id":18,"category":"Programming Language","prompt":"Guess the programming language.","hints":["Runs in all modern browsers.","Created by Brendan Eich in 1995."],"answer":"JavaScript"},
    {"id":19,"category":"Cloud Service (AWS)","prompt":"Guess the AWS service.","hints":["Object storage at scale.","You store data in 'buckets'."],"answer":"Amazon S3"},
    {"id":20,"category":"Cloud Service (Azure)","prompt":"Guess the Azure service.","hints":["Object storage on Microsoft cloud.","Organized into containers of blobs."],"answer":"Azure Blob Storage"},
    {"id":21,"category":"Social Media Platform","prompt":"Guess the social media platform.","hints":["Photo and video sharing app.","Owned by Meta."],"answer":"Instagram"},
    {"id":22,"category":"Board Game","prompt":"Guess the board game.","hints":["Four colored homes on the board.","You roll a die to move tokens to the finish."],"answer":"Ludo"},
    {"id":23,"category":"Indian Dessert","prompt":"Guess the Indian dessert.","hints":["Soft paneer patties in thickened milk.","Flavored with cardamom and saffron."],"answer":"Rasmalai"},
    {"id":24,"category":"Indian Street Food","prompt":"Guess the Indian street food.","hints":["Called Mumbai's burger.","Spicy potato fritter in a bun with chutneys."],"answer":"Vada Pav"},
    {"id":25,"category":"Punjabi Dish","prompt":"Guess the Punjabi dish.","hints":["Mustard greens curry.","Traditionally eaten with makki di roti."],"answer":"Sarson ka Saag"},
    {"id":26,"category":"Gujarati Snack","prompt":"Guess the Gujarati snack.","hints":["Steamed, fluffy and savory.","Made from fermented batter; often yellow."],"answer":"Dhokla"},
    {"id":27,"category":"Musical Instrument","prompt":"Guess the musical instrument.","hints":["Plucked Indian classical string instrument.","Popularized globally by Ravi Shankar."],"answer":"Sitar"},
    {"id":28,"category":"Classical Dance Form","prompt":"Guess the Indian classical dance form.","hints":["Originated in Tamil Nadu.","Emphasizes mudras and expressive abhinaya."],"answer":"Bharatanatyam"},
    {"id":29,"category":"Mythological Character","prompt":"Guess the character from Indian epics.","hints":["Master archer from Mahabharata.","Receives guidance from Krishna in the Gita."],"answer":"Arjuna"},
    {"id":30,"category":"Indian Animal","prompt":"Guess the Indian wild animal.","hints":["Only wild population in Gir Forest.","Distinct belly fold along the abdomen."],"answer":"Asiatic Lion"},
    {"id":31,"category":"Indian Bird","prompt":"Guess the Indian bird.","hints":["Striking blue-winged rollers.","Often called 'neelkanth' in parts of India."],"answer":"Indian Roller"},
    {"id":32,"category":"National Park (India)","prompt":"Guess the Indian national park.","hints":["Located in Uttarakhand.","India's oldest national park; famous for tigers."],"answer":"Jim Corbett National Park"},
    {"id":33,"category":"Mountain Range","prompt":"Guess the mountain range.","hints":["Runs parallel to India's west coast.","UNESCO biodiversity hotspot."],"answer":"Western Ghats"},
    {"id":34,"category":"Planet","prompt":"Guess the planet.","hints":["Prominent ring system.","Sixth from the Sun."],"answer":"Saturn"},
    {"id":35,"category":"Web Browser","prompt":"Guess the web browser.","hints":["Developed by Google.","Uses the Blink rendering engine."],"answer":"Google Chrome"},
    {"id":36,"category":"Database","prompt":"Guess the database system.","hints":["Popular open-source RDBMS.","Owned by Oracle Corporation."],"answer":"MySQL"},
    {"id":37,"category":"Version Control System","prompt":"Guess the version control system.","hints":["Created by Linus Torvalds.","Distributed source control."],"answer":"Git"},
    {"id":38,"category":"IDE/Code Editor","prompt":"Guess the code editor.","hints":["Made by Microsoft.","Has a vast Extensions Marketplace."],"answer":"Visual Studio Code"},
    {"id":39,"category":"Operating System","prompt":"Guess the operating system.","hints":["Linux-based mobile OS.","Developed by Google."],"answer":"Android"},
    {"id":40,"category":"HTTP Status Code","prompt":"Guess the HTTP status code.","hints":["Client error category.","Means the requested resource could not be located."],"answer":"404 Not Found"},
    {"id":41,"category":"Currency","prompt":"Guess the currency.","hints":["Symbol is ₹.","Issued and managed by the RBI."],"answer":"Indian Rupee"},
    {"id":42,"category":"Stock Exchange","prompt":"Guess the stock exchange.","hints":["Based in Mumbai, India.","Flagship index: NIFTY 50."],"answer":"National Stock Exchange (NSE)"},
    {"id":43,"category":"Indian Bank","prompt":"Guess the Indian bank.","hints":["Largest public sector bank in India.","Commonly abbreviated to SBI."],"answer":"State Bank of India"},
    {"id":44,"category":"ISRO Mission","prompt":"Guess the ISRO mission.","hints":["Lunar exploration mission.","Achieved soft landing near the south pole in 2023."],"answer":"Chandrayaan-3"},
    {"id":45,"category":"Indian Train","prompt":"Guess the Indian train service.","hints":["Semi-high-speed indigenous trainset.","Also known as Train 18."],"answer":"Vande Bharat Express"},
    {"id":46,"category":"Indian Airport","prompt":"Guess the Indian airport.","hints":["IATA code DEL.","Located in New Delhi."],"answer":"Indira Gandhi International Airport"},
    {"id":47,"category":"Indian Stadium","prompt":"Guess the stadium.","hints":["Located in Mumbai.","Hosted the ICC Cricket World Cup 2011 final."],"answer":"Wankhede Stadium"},
    {"id":48,"category":"Indian Startup","prompt":"Guess the Indian startup.","hints":["Food delivery and dining platform.","Acquired Uber Eats India in 2020."],"answer":"Zomato"},
    {"id":49,"category":"Payment App (India)","prompt":"Guess the Indian payment app.","hints":["UPI-based digital payments.","Purple logo featuring the Devanagari 'फ'."],"answer":"PhonePe"},
    {"id":50,"category":"E-commerce Platform (India)","prompt":"Guess the Indian e-commerce platform.","hints":["Founded by Sachin and Binny Bansal.","Known for the Big Billion Days sale."],"answer":"Flipkart"}
  ]
  </script>

  <script>
    const raw = document.getElementById('questions-data').textContent.trim();
    const QUESTIONS = JSON.parse(raw);

    const els = {
      roundInfo: document.getElementById('roundInfo'),
      category: document.getElementById('categoryBadge'),
      prompt: document.getElementById('promptText'),
      hint1Wrap: document.getElementById('hint1'),
      hint2Wrap: document.getElementById('hint2'),
      answerWrap: document.getElementById('answer'),
      hint1: document.getElementById('hint1Text'),
      hint2: document.getElementById('hint2Text'),
      answer: document.getElementById('answerText'),
      revealBtn: document.getElementById('revealBtn'),
      resetBtn: document.getElementById('resetBtn'),
      prevBtn: document.getElementById('prevBtn'),
      nextBtn: document.getElementById('nextBtn'),
      shuffleBtn: document.getElementById('shuffleBtn'),
      randomBtn: document.getElementById('randomBtn'),
      jump: document.getElementById('jump'),
      dotPrompt: document.getElementById('dotPrompt'),
      dotHint1: document.getElementById('dotHint1'),
      dotHint2: document.getElementById('dotHint2'),
      dotAnswer: document.getElementById('dotAnswer')
    };

    const state = {
      order: [...QUESTIONS.keys()],
      index: 0,
      revealStep: 0
    };

    function shuffle(array){
      for(let i=array.length-1;i>0;i--){
        const j=Math.floor(Math.random()*(i+1));
        [array[i],array[j]]=[array[j],array[i]];
      }
      return array;
    }

    function setIndex(i){
      if(i<0) i=0;
      if(i>state.order.length-1) i=state.order.length-1;
      state.index=i; state.revealStep=0; render();
    }

    function revealNext(){
      if(state.revealStep<3){ state.revealStep++; renderReveal(); }
    }
    function resetReveals(){ state.revealStep=0; renderReveal(); }

    function render(){
      const q = QUESTIONS[state.order[state.index]];
      els.category.textContent = q.category;
      els.prompt.textContent = q.prompt;
      els.hint1.textContent = q.hints[0] || "";
      els.hint2.textContent = q.hints[1] || "";
      els.answer.textContent = q.answer;

      els.roundInfo.textContent = `Round ${state.index+1} of ${state.order.length}`;

      els.jump.innerHTML = "";
      state.order.forEach((qi,pos)=>{
        const opt=document.createElement('option');
        const item=QUESTIONS[qi];
        opt.value=String(pos);
        opt.textContent = `${pos+1}. ${item.category} — ${item.prompt}`.slice(0,120);
        if(pos===state.index) opt.selected=true;
        els.jump.appendChild(opt);
      });

      renderReveal();
    }

    function renderReveal(){
      const step = state.revealStep;
      els.hint1Wrap.classList.toggle('hidden', !(step>=1));
      els.hint2Wrap.classList.toggle('hidden', !(step>=2));
      els.answerWrap.classList.toggle('hidden', !(step>=3));

      els.dotPrompt.classList.toggle('on', true);
      els.dotHint1.classList.toggle('on', step>=1);
      els.dotHint2.classList.toggle('on', step>=2);
      els.dotAnswer.classList.toggle('on', step>=3);
      els.dotAnswer.classList.toggle('ans', step>=3);

      els.revealBtn.disabled = step>=3;
      els.revealBtn.textContent = step>=3 ? 'Answer shown' : 'Reveal next (Space)';
      els.prevBtn.disabled = state.index===0;
      els.nextBtn.disabled = state.index===state.order.length-1;
    }

    els.revealBtn.addEventListener('click', revealNext);
    els.resetBtn.addEventListener('click', resetReveals);
    els.prevBtn.addEventListener('click', ()=>setIndex(state.index-1));
    els.nextBtn.addEventListener('click', ()=>setIndex(state.index+1));
    els.shuffleBtn.addEventListener('click', ()=>{ shuffle(state.order); setIndex(0); });
    els.randomBtn.addEventListener('click', ()=>{ const r=Math.floor(Math.random()*state.order.length); setIndex(r); });
    els.jump.addEventListener('change', (e)=> setIndex(parseInt(e.target.value,10)));

    window.addEventListener('keydown', (e)=>{
      if(e.key===' '){ e.preventDefault(); revealNext(); }
      else if(e.key==='ArrowRight'){ setIndex(state.index+1); }
      else if(e.key==='ArrowLeft'){ setIndex(state.index-1); }
      else if(e.key.toLowerCase()==='r'){ resetReveals(); }
    });

    render();
  </script>
</body>
</html>
