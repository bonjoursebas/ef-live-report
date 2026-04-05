[ef_live_report (1).html](https://github.com/user-attachments/files/26487620/ef_live_report.1.html)# ef-live-report[Uploading<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EF — Générateur live report</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/docx/8.5.0/docx.umd.min.js"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Lato:wght@300;400;700&display=swap');
*{box-sizing:border-box;margin:0;padding:0}
:root{--bg:#0e0e0e;--surface:#161616;--border:#2a2a2a;--border-light:#333;--text:#e8e6df;--text-muted:#777;--text-dim:#444;--accent:#c8a96e;--accent-dim:#7a6340;--radius:6px}
body{background:var(--bg);color:var(--text);font-family:'Lato',sans-serif;font-weight:300;padding:2rem 1rem 4rem;min-height:100vh}
.wrap{max-width:740px;margin:0 auto}
header{margin-bottom:2.5rem;padding-bottom:1.5rem;border-bottom:1px solid var(--border)}
.ef-label{font-size:10px;font-weight:700;letter-spacing:.25em;text-transform:uppercase;color:var(--accent);margin-bottom:.5rem}
header h1{font-family:'Playfair Display',serif;font-size:clamp(1.6rem,4vw,2.2rem);font-weight:400;line-height:1.2}
header p{margin-top:.5rem;font-size:13px;color:var(--text-muted);line-height:1.6}
.section{margin-bottom:1.75rem}
.section-title{font-size:10px;font-weight:700;letter-spacing:.2em;text-transform:uppercase;color:var(--accent-dim);margin-bottom:1rem;display:flex;align-items:center;gap:.75rem}
.section-title::after{content:'';flex:1;height:1px;background:var(--border)}
.row{display:flex;gap:1rem;flex-wrap:wrap}
.row .field{flex:1;min-width:200px}
.field{margin-bottom:1rem}
label{display:block;font-size:11px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--text-muted);margin-bottom:.4rem}
label .opt{font-weight:300;letter-spacing:0;text-transform:none;color:var(--text-dim);font-size:11px}
.hint{display:block;font-size:11px;font-weight:300;letter-spacing:0;text-transform:none;color:var(--text-dim);margin-top:2px}
input[type=text],input[type=date],textarea{width:100%;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:10px 12px;font-size:14px;font-family:'Lato',sans-serif;font-weight:300;color:var(--text);outline:none;transition:border-color .15s;-webkit-appearance:none}
input[type=text]:focus,input[type=date]:focus,textarea:focus{border-color:var(--accent-dim)}
input[type=date]::-webkit-calendar-picker-indicator{filter:invert(.4);cursor:pointer}
textarea{resize:vertical;line-height:1.65;min-height:90px}
.url-row{display:flex;gap:.5rem}
.url-row input{flex:1}
.btn-clear{padding:10px 12px;background:none;border:1px solid var(--border);border-radius:var(--radius);color:var(--text-muted);cursor:pointer;font-size:12px;white-space:nowrap;transition:all .15s;font-family:'Lato',sans-serif}
.btn-clear:hover{border-color:var(--border-light);color:var(--text)}
.btn-generate{width:100%;padding:14px;background:var(--accent);color:#0e0e0e;border:none;border-radius:var(--radius);font-family:'Lato',sans-serif;font-size:14px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;cursor:pointer;transition:opacity .15s,transform .1s;margin-top:.5rem}
.btn-generate:hover{opacity:.88}
.btn-generate:active{transform:scale(.99)}
.btn-generate:disabled{opacity:.35;cursor:default}
.loading{display:none;align-items:center;gap:.75rem;margin-top:1.5rem;font-size:13px;color:var(--text-muted)}
.loading.active{display:flex}
.spinner{width:16px;height:16px;border:2px solid var(--border);border-top-color:var(--accent);border-radius:50%;animation:spin .7s linear infinite;flex-shrink:0}
@keyframes spin{to{transform:rotate(360deg)}}
.error{margin-top:1rem;padding:10px 14px;background:rgba(192,57,43,.1);border:1px solid rgba(192,57,43,.3);border-radius:var(--radius);font-size:13px;color:#e74c3c;display:none}
.output-wrap{margin-top:2rem;display:none}
.output-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:1rem;flex-wrap:wrap;gap:.5rem}
.output-header h2{font-family:'Playfair Display',serif;font-size:1.1rem;font-weight:400}
.output-actions{display:flex;gap:.5rem}
.btn-sec{padding:7px 14px;background:none;border:1px solid var(--border-light);border-radius:var(--radius);color:var(--text-muted);font-family:'Lato',sans-serif;font-size:12px;cursor:pointer;transition:all .15s}
.btn-sec:hover{border-color:var(--accent-dim);color:var(--accent)}
.btn-sec.primary{background:var(--accent);color:#0e0e0e;border-color:var(--accent);font-weight:700}
.btn-sec.primary:hover{opacity:.85}
.output-box{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:1.5rem;font-size:14px;line-height:1.85;color:var(--text);white-space:pre-wrap;font-family:'Lato',sans-serif;font-weight:300}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}
.cursor{display:inline-block;width:2px;height:14px;background:var(--accent);vertical-align:middle;margin-left:2px;animation:blink .8s infinite}
.toast{position:fixed;bottom:1.5rem;right:1.5rem;background:var(--surface);border:1px solid var(--border-light);border-radius:var(--radius);padding:10px 16px;font-size:13px;color:var(--text);display:none;z-index:100;box-shadow:0 4px 20px rgba(0,0,0,.5)}
</style>
</head>
<body>
<div class="wrap">

<header>
  <div class="ef-label">Esprit Festivalier</div>
  <h1>Générateur de live report</h1>
  <p>Remplis les champs ci-dessous. Claude lira la page auteur pour adapter son style, puis générera un brouillon téléchargeable en .docx.</p>
</header>

<div class="section">
  <div class="section-title">Rédacteur</div>
  <div class="row">
    <div class="field">
      <label>Nom du rédacteur</label>
      <input type="text" id="auteur" value="Sébastien Martinez-Cerisier">
    </div>
  </div>
  <div class="field">
    <label>
      Page auteur Esprit Festivalier <span class="opt">optionnel</span>
      <span class="hint">Claude lira cette page pour s'adapter au style d'écriture — efface le champ si non pertinent</span>
    </label>
    <div class="url-row">
      <input type="text" id="urlAuteur" value="https://esprit-festivalier.fr/author/sebastien-martinez/">
      <button class="btn-clear" onclick="document.getElementById('urlAuteur').value=''">Effacer</button>
    </div>
  </div>
</div>

<div class="section">
  <div class="section-title">Infos concert</div>
  <div class="row">
    <div class="field" style="flex:2">
      <label>Artiste / Groupe</label>
      <input type="text" id="artiste" placeholder="ex. Renée Rapp">
    </div>
    <div class="field">
      <label>Date du concert</label>
      <input type="date" id="date">
    </div>
  </div>
  <div class="row">
    <div class="field" style="flex:2">
      <label>Salle</label>
      <input type="text" id="salle" placeholder="ex. Le Zénith de Paris">
    </div>
    <div class="field">
      <label>Ville</label>
      <input type="text" id="ville" placeholder="ex. Paris">
    </div>
  </div>
  <div class="field">
    <label>Nom de la tournée <span class="opt">optionnel</span></label>
    <input type="text" id="tournee" placeholder="ex. Bite Me Tour">
  </div>
</div>

<div class="section">
  <div class="section-title">Chansons jouées</div>
  <div class="field">
    <label>
      Chansons jouées <span class="opt">optionnel</span>
      <span class="hint">Celle du concert ou d'une date similaire (setlist.fm, etc.)</span>
    </label>
    <textarea id="setlist" style="min-height:140px" placeholder="1. Pretty Girls&#10;2. Tattoo&#10;3. Poison&#10;..."></textarea>
  </div>
</div>

<div class="section">
  <div class="section-title">Notes pour la rédaction</div>
  <div class="field">
    <label>
      Notes du concert
      <span class="hint">Moments forts, ambiance, scénographie, rapport au public, ressenti, ce qui t'a moins convaincu, angle d'article souhaité...</span>
    </label>
    <textarea id="notes" style="min-height:200px" placeholder="ex. Ouverture tendue sur Pretty Girls, lumières très contrastées, Renée Rapp très à l'aise à parler entre les morceaux, rappel a cappella dévastateur, voix encore plus impressionnante live que sur disque, salle sold out très chaleureuse, fin du set un peu essoufflée..."></textarea>
  </div>
</div>

<button class="btn-generate" id="btnGenerate">✦ Générer le brouillon</button>
<div class="loading" id="loading"><div class="spinner"></div><span id="loadingMsg">En cours...</span></div>
<div class="error" id="errorBox"></div>

<div class="output-wrap" id="outputWrap">
  <div class="output-header">
    <h2>Brouillon généré</h2>
    <div class="output-actions">
      <button class="btn-sec" id="btnCopy">Copier</button>
      <button class="btn-sec primary" id="btnDocx">⬇ Télécharger .docx</button>
    </div>
  </div>
  <div class="output-box" id="outputBox"></div>
</div>

</div>
<div class="toast" id="toast"></div>

<script>
let generatedText = '';

function val(id){ return (document.getElementById(id)||{}).value?.trim()||'' }

function showToast(msg, dur=2800){
  const t = document.getElementById('toast');
  t.textContent = msg; t.style.display = 'block';
  setTimeout(()=>t.style.display='none', dur);
}

function fmtDate(s){
  if(!s) return '';
  const [y,m,d] = s.split('-');
  return new Date(y,m-1,d).toLocaleDateString('fr-FR',{day:'numeric',month:'long',year:'numeric'});
}

async function generate(){
  const artiste = val('artiste');
  if(!artiste){ showToast('Renseigne au moins le nom de l\'artiste.'); return; }

  const auteur    = val('auteur');
  const urlAuteur = val('urlAuteur');
  const date      = val('date');
  const salle     = val('salle');
  const ville     = val('ville');
  const tournee   = val('tournee');
  const setlist   = val('setlist');
  const notes     = val('notes');

  const btn = document.getElementById('btnGenerate');
  const loading = document.getElementById('loading');
  const loadingMsg = document.getElementById('loadingMsg');
  const errorBox = document.getElementById('errorBox');
  const outputWrap = document.getElementById('outputWrap');
  const outputBox = document.getElementById('outputBox');

  btn.disabled = true;
  errorBox.style.display = 'none';
  outputWrap.style.display = 'none';
  outputBox.textContent = '';
  loading.classList.add('active');
  generatedText = '';
  loadingMsg.textContent = urlAuteur ? 'Lecture de la page auteur...' : 'Rédaction en cours...';

  const systemPrompt = `Tu es rédacteur pour Esprit Festivalier, média français dédié aux festivals et à la musique live.

Ton rôle : rédiger un live report complet et publiable à partir des notes fournies.

Style attendu (impératif) :
- Prose fluide et journalistique, subjectivité assumée, point de vue personnel tranché
- PAS de tirets cadratins (—), PAS de langage promotionnel, PAS d'hyperboles marketing
- PAS de structure annoncée, pas de plan apparent dans le texte
- Une intro qui pose l'atmosphère sans annoncer le plan
- Une conclusion opinionnée, pas de morale générale
- Longueur cible : 400 à 550 mots
- Ne pas mentionner le nom de l'auteur dans le texte
- Rédige directement l'article, sans préambule ni commentaire`;

  let userMsg = '';

  if(urlAuteur){
    userMsg += `Commence par lire cette page pour analyser le style d'écriture du rédacteur et t'y adapter au maximum dans l'article : ${urlAuteur}\n\n`;
  }

  userMsg += `Rédige un live report pour Esprit Festivalier à partir de ces informations :\n\n`;
  userMsg += `Artiste : ${artiste}\n`;
  if(date) userMsg += `Date : ${fmtDate(date)}\n`;
  if(salle||ville) userMsg += `Lieu : ${[salle,ville].filter(Boolean).join(', ')}\n`;
  if(tournee) userMsg += `Tournée : ${tournee}\n`;
  if(auteur) userMsg += `Rédacteur (ne pas citer dans le texte) : ${auteur}\n`;
  if(setlist) userMsg += `\nChansons jouées :\n${setlist}\n`;
  if(notes) userMsg += `\nNotes et observations :\n${notes}\n`;
  userMsg += `\nRédige l'article directement.`;

  const body = {
    model: "claude-sonnet-4-20250514",
    max_tokens: 1500,
    system: systemPrompt,
    messages: [{ role: "user", content: userMsg }],
    stream: true
  };

  if(urlAuteur){
    body.tools = [{ type: "web_search_20250305", name: "web_search" }];
  }

  try {
    const resp = await fetch("https://api.anthropic.com/v1/messages", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(body)
    });

    if(!resp.ok){
      const err = await resp.json().catch(()=>({}));
      throw new Error(err.error?.message || `Erreur API (${resp.status})`);
    }

    loading.classList.remove('active');
    outputWrap.style.display = 'block';
    outputBox.innerHTML = '<span class="cursor"></span>';

    const reader = resp.body.getReader();
    const decoder = new TextDecoder();
    let buffer = '';
    let inToolUse = false;

    while(true){
      const {done, value} = await reader.read();
      if(done) break;
      buffer += decoder.decode(value, {stream:true});
      const lines = buffer.split('\n');
      buffer = lines.pop();

      for(const line of lines){
        if(!line.startsWith('data: ')) continue;
        const data = line.slice(6);
        if(data==='[DONE]') continue;
        try{
          const evt = JSON.parse(data);
          if(evt.type==='content_block_start'){
            inToolUse = evt.content_block?.type==='tool_use';
            if(inToolUse){ loadingMsg.textContent='Lecture de la page auteur...'; loading.classList.add('active'); outputWrap.style.display='none'; }
          }
          if(evt.type==='content_block_stop' && inToolUse){
            inToolUse=false;
            loadingMsg.textContent='Rédaction en cours...';
            loading.classList.remove('active');
            outputWrap.style.display='block';
            outputBox.innerHTML='<span class="cursor"></span>';
          }
          if(!inToolUse && evt.type==='content_block_delta' && evt.delta?.type==='text_delta'){
            generatedText += evt.delta.text;
            outputBox.textContent = generatedText;
            outputBox.insertAdjacentHTML('beforeend','<span class="cursor"></span>');
          }
        }catch(e){}
      }
    }

    outputBox.textContent = generatedText.trim();
    generatedText = generatedText.trim();

  } catch(err){
    loading.classList.remove('active');
    errorBox.textContent = 'Erreur : ' + err.message;
    errorBox.style.display = 'block';
  }

  btn.disabled = false;
}

async function downloadDocx(){
  if(!generatedText){ showToast('Génère d\'abord un brouillon.'); return; }

  const { Document, Packer, Paragraph, TextRun, AlignmentType } = docx;

  const auteur  = val('auteur');
  const artiste = val('artiste');
  const date    = val('date');
  const salle   = val('salle');
  const ville   = val('ville');
  const tournee = val('tournee');

  const metaParts = [artiste,[salle,ville].filter(Boolean).join(', '),date?fmtDate(date):'',tournee].filter(Boolean);
  const title = `Live report — ${artiste}${salle?' @ '+salle:''}${date?' ('+fmtDate(date)+')':''}`;
  const paras = generatedText.split(/\n+/).filter(l=>l.trim());

  const children = [];

  // Titre
  children.push(new Paragraph({
    children:[new TextRun({text:title,bold:true,size:30,font:"Georgia"})],
    spacing:{after:120}
  }));

  // Méta
  if(metaParts.length){
    children.push(new Paragraph({
      children:[new TextRun({text:metaParts.join(' · '),size:20,color:"888888",font:"Arial"})],
      spacing:{after:80}
    }));
  }

  // Auteur
  if(auteur){
    children.push(new Paragraph({
      children:[new TextRun({text:`Par ${auteur}`,size:20,italics:true,color:"666666",font:"Arial"})],
      spacing:{after:360}
    }));
  }

  // Corps
  paras.forEach((p,i)=>{
    children.push(new Paragraph({
      children:[new TextRun({text:p,size:24,font:"Georgia"})],
      spacing:{after:i===paras.length-1?0:180},
      alignment:AlignmentType.JUSTIFIED
    }));
  });

  const doc = new Document({
    sections:[{
      properties:{page:{size:{width:11906,height:16838},margin:{top:1440,right:1440,bottom:1440,left:1440}}},
      children
    }]
  });

  const blob = await Packer.toBlob(doc);
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `live-report_${(artiste||'article').toLowerCase().replace(/[^a-z0-9]+/g,'-')}.docx`;
  a.click();
  URL.revokeObjectURL(url);
  showToast('Fichier .docx téléchargé ✓');
}

document.getElementById('btnGenerate').addEventListener('click', generate);
document.getElementById('btnDocx').addEventListener('click', downloadDocx);
document.getElementById('btnCopy').addEventListener('click',()=>{
  if(!generatedText){showToast('Rien à copier.');return;}
  navigator.clipboard.writeText(generatedText).then(()=>showToast('Texte copié ✓')).catch(()=>showToast('Copie manuelle depuis le cadre.'));
});
</script>
</body>
</html>
 ef_live_report (1).html…]()
