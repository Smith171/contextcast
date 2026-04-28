[contextcast_app.html](https://github.com/user-attachments/files/27181784/contextcast_app.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>ContextCast</title>
<style>
  :root {
    --primary: #1D9E75;
    --primary-dark: #0F6E56;
    --primary-light: #E1F5EE;
    --accent: #D85A30;
    --accent-light: #FAECE7;
    --surface: #ffffff;
    --surface2: #f7f9f8;
    --border: rgba(0,0,0,0.10);
    --text: #1a1a1a;
    --text2: #5F5E5A;
    --text3: #888780;
    --radius: 16px;
    --radius-sm: 10px;
    --shadow: 0 2px 16px rgba(0,0,0,0.08);
    --font: 'Segoe UI', system-ui, sans-serif;
  }
  @media(prefers-color-scheme: dark){
    :root{
      --surface:#1a1f1e;--surface2:#232927;--border:rgba(255,255,255,0.10);
      --text:#f0f0f0;--text2:#B4B2A9;--text3:#888780;--primary-light:#085041;
      --accent-light:#4A1B0C;--shadow:0 2px 16px rgba(0,0,0,0.4);
    }
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  body{font-family:var(--font);background:var(--surface2);color:var(--text);min-height:100vh;font-size:16px;line-height:1.5;}
  .sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0;}
  
  /* HEADER */
  .app-header{background:var(--primary);color:#fff;padding:1rem 1.25rem;display:flex;align-items:center;gap:12px;position:sticky;top:0;z-index:100;}
  .logo-icon{width:36px;height:36px;background:rgba(255,255,255,0.2);border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0;}
  .app-title{font-size:20px;font-weight:600;letter-spacing:-0.3px;}
  .app-tagline{font-size:12px;opacity:0.85;margin-top:1px;}
  .nav-tabs{display:flex;gap:4px;margin-left:auto;}
  .nav-btn{background:rgba(255,255,255,0.15);border:none;color:#fff;padding:6px 12px;border-radius:8px;font-size:13px;cursor:pointer;transition:background 0.2s;font-family:var(--font);}
  .nav-btn:hover,.nav-btn[aria-selected="true"]{background:rgba(255,255,255,0.3);}
  .nav-btn:focus-visible{outline:3px solid #fff;outline-offset:2px;}

  /* MAIN */
  .main{padding:1.25rem;max-width:700px;margin:0 auto;}
  
  /* CAPTURE CARD */
  .capture-card{background:var(--surface);border-radius:var(--radius);padding:1.25rem;border:0.5px solid var(--border);box-shadow:var(--shadow);margin-bottom:1.25rem;}
  .capture-label{font-size:13px;font-weight:500;color:var(--text2);margin-bottom:10px;display:flex;align-items:center;gap:6px;}
  .capture-textarea{width:100%;border:1.5px solid var(--border);border-radius:var(--radius-sm);padding:12px;font-size:15px;font-family:var(--font);color:var(--text);background:var(--surface2);resize:none;min-height:90px;transition:border 0.2s;}
  .capture-textarea:focus{outline:none;border-color:var(--primary);}
  .capture-textarea::placeholder{color:var(--text3);}
  .capture-row{display:flex;gap:10px;margin-top:10px;flex-wrap:wrap;}
  .context-btn{background:var(--surface2);border:0.5px solid var(--border);border-radius:8px;padding:7px 13px;font-size:13px;cursor:pointer;color:var(--text2);transition:all 0.2s;display:flex;align-items:center;gap:5px;font-family:var(--font);}
  .context-btn:hover{border-color:var(--primary);color:var(--primary);}
  .context-btn:focus-visible{outline:3px solid var(--primary);outline-offset:2px;}
  .context-btn.active{background:var(--primary-light);border-color:var(--primary);color:var(--primary-dark);}
  .save-btn{margin-left:auto;background:var(--primary);color:#fff;border:none;border-radius:10px;padding:9px 22px;font-size:14px;font-weight:500;cursor:pointer;transition:background 0.2s;font-family:var(--font);}
  .save-btn:hover{background:var(--primary-dark);}
  .save-btn:focus-visible{outline:3px solid var(--primary);outline-offset:2px;}
  .save-btn:disabled{opacity:0.5;cursor:not-allowed;}

  /* TAGS */
  .tags-row{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px;}
  .tag{background:var(--primary-light);color:var(--primary-dark);border-radius:20px;padding:3px 11px;font-size:12px;font-weight:500;}

  /* INTENTIONS LIST */
  .section-title{font-size:15px;font-weight:600;color:var(--text);margin-bottom:12px;display:flex;align-items:center;gap:8px;}
  .badge{background:var(--primary);color:#fff;border-radius:20px;padding:1px 8px;font-size:12px;font-weight:500;}
  .intention-card{background:var(--surface);border-radius:var(--radius-sm);padding:1rem 1.1rem;border:0.5px solid var(--border);margin-bottom:10px;display:flex;gap:12px;cursor:pointer;transition:box-shadow 0.2s;position:relative;}
  .intention-card:hover{box-shadow:var(--shadow);}
  .intention-card:focus-visible{outline:3px solid var(--primary);outline-offset:2px;border-radius:var(--radius-sm);}
  .intention-icon{width:40px;height:40px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0;}
  .intention-icon.casa{background:var(--primary-light);}
  .intention-icon.trabalho{background:#E6F1FB;}
  .intention-icon.ideia{background:#FAEEDA;}
  .intention-icon.social{background:#FBEAF0;}
  .intention-title{font-size:14px;font-weight:500;color:var(--text);margin-bottom:3px;}
  .intention-meta{font-size:12px;color:var(--text3);display:flex;gap:8px;flex-wrap:wrap;}
  .intention-time{font-size:11px;color:var(--text3);position:absolute;top:12px;right:12px;}
  .status-dot{width:8px;height:8px;border-radius:50%;display:inline-block;margin-right:4px;}
  .status-dot.pending{background:#EF9F27;}
  .status-dot.done{background:var(--primary);}
  .empty-state{text-align:center;padding:3rem 1rem;color:var(--text3);}
  .empty-icon{font-size:48px;margin-bottom:12px;}
  .empty-text{font-size:14px;line-height:1.6;}

  /* AI CHAT PANEL */
  .ai-panel{background:var(--surface);border-radius:var(--radius);border:0.5px solid var(--border);box-shadow:var(--shadow);overflow:hidden;}
  .ai-header{background:var(--primary-light);padding:1rem 1.25rem;border-bottom:0.5px solid var(--border);display:flex;align-items:center;gap:10px;}
  .ai-avatar{width:36px;height:36px;background:var(--primary);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:18px;}
  .ai-name{font-size:14px;font-weight:600;color:var(--primary-dark);}
  .ai-sub{font-size:12px;color:var(--primary-dark);opacity:0.7;}
  .chat-body{padding:1rem;display:flex;flex-direction:column;gap:10px;min-height:200px;max-height:320px;overflow-y:auto;}
  .msg{max-width:85%;padding:10px 14px;border-radius:14px;font-size:14px;line-height:1.5;}
  .msg.ai{background:var(--surface2);border:0.5px solid var(--border);align-self:flex-start;border-bottom-left-radius:4px;}
  .msg.user{background:var(--primary);color:#fff;align-self:flex-end;border-bottom-right-radius:4px;}
  .msg.loading{display:flex;gap:4px;align-items:center;padding:14px;}
  .dot{width:7px;height:7px;background:var(--text3);border-radius:50%;animation:bounce 1.2s infinite;}
  .dot:nth-child(2){animation-delay:0.2s;}
  .dot:nth-child(3){animation-delay:0.4s;}
  @keyframes bounce{0%,80%,100%{transform:translateY(0);}40%{transform:translateY(-6px);}}
  .chat-input-row{display:flex;gap:8px;padding:0.75rem 1rem;border-top:0.5px solid var(--border);}
  .chat-input{flex:1;border:1.5px solid var(--border);border-radius:10px;padding:9px 13px;font-size:14px;font-family:var(--font);color:var(--text);background:var(--surface2);}
  .chat-input:focus{outline:none;border-color:var(--primary);}
  .send-btn{background:var(--primary);color:#fff;border:none;border-radius:10px;padding:9px 16px;font-size:14px;cursor:pointer;font-family:var(--font);transition:background 0.2s;}
  .send-btn:hover{background:var(--primary-dark);}
  .send-btn:focus-visible{outline:3px solid var(--primary);outline-offset:2px;}
  .send-btn:disabled{opacity:0.5;cursor:not-allowed;}

  /* MODAL */
  .modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:200;display:flex;align-items:flex-end;justify-content:center;padding:0;}
  .modal-overlay[hidden]{display:none;}
  .modal{background:var(--surface);border-radius:var(--radius) var(--radius) 0 0;padding:1.5rem;width:100%;max-width:700px;max-height:90vh;overflow-y:auto;}
  .modal-handle{width:40px;height:4px;background:var(--border);border-radius:2px;margin:0 auto 1.25rem;}
  .modal-close{background:none;border:none;color:var(--text2);font-size:20px;cursor:pointer;float:right;padding:4px;}
  .modal-close:focus-visible{outline:3px solid var(--primary);outline-offset:2px;border-radius:4px;}
  .modal-title{font-size:18px;font-weight:600;margin-bottom:1rem;}
  .modal-section{margin-bottom:1rem;}
  .modal-label{font-size:12px;font-weight:500;color:var(--text2);margin-bottom:4px;}
  .modal-value{font-size:15px;color:var(--text);}
  .modal-actions{display:flex;gap:10px;margin-top:1.25rem;flex-wrap:wrap;}
  .btn-outline{background:none;border:1.5px solid var(--border);color:var(--text2);border-radius:10px;padding:9px 18px;font-size:14px;cursor:pointer;font-family:var(--font);transition:all 0.2s;}
  .btn-outline:hover{border-color:var(--primary);color:var(--primary);}
  .btn-outline:focus-visible{outline:3px solid var(--primary);outline-offset:2px;}
  .btn-danger{background:none;border:1.5px solid #F09595;color:#A32D2D;border-radius:10px;padding:9px 18px;font-size:14px;cursor:pointer;font-family:var(--font);transition:all 0.2s;}
  .btn-danger:hover{background:#FCEBEB;}
  .btn-danger:focus-visible{outline:3px solid #E24B4A;outline-offset:2px;}

  /* SKIP LINK */
  .skip-link{position:absolute;top:-40px;left:0;background:var(--primary);color:#fff;padding:8px 16px;z-index:999;border-radius:0 0 8px 0;transition:top 0.2s;font-size:14px;}
  .skip-link:focus{top:0;}

  /* API KEY NOTICE */
  .api-notice{background:var(--accent-light);border:0.5px solid #F0997B;border-radius:var(--radius-sm);padding:10px 14px;font-size:13px;color:var(--accent);margin-bottom:1rem;display:flex;gap:8px;align-items:flex-start;}
  .api-notice input{flex:1;border:1px solid #F0997B;border-radius:7px;padding:5px 9px;font-size:13px;font-family:var(--font);background:var(--surface);color:var(--text);}
  .api-notice input:focus{outline:2px solid var(--accent);}
  .api-notice button{background:var(--accent);color:#fff;border:none;border-radius:7px;padding:5px 12px;font-size:13px;cursor:pointer;font-family:var(--font);white-space:nowrap;}

  @media(min-width:640px){
    .capture-row{flex-wrap:nowrap;}
    .modal{border-radius:var(--radius);}
    .modal-overlay{align-items:center;}
  }
</style>
</head>
<body>
<h2 class="sr-only">ContextCast — App de intenções contextuais com IA</h2>
<a class="skip-link" href="#main-content">Ir para conteúdo principal</a>

<header class="app-header" role="banner">
  <div class="logo-icon" aria-hidden="true">📍</div>
  <div>
    <div class="app-title">ContextCast</div>
    <div class="app-tagline">Lembra o que você queria fazer</div>
  </div>
  <nav class="nav-tabs" aria-label="Navegação principal">
    <button class="nav-btn" id="tab-capture" role="tab" aria-selected="true" onclick="switchTab('capture')">Capturar</button>
    <button class="nav-btn" id="tab-list" role="tab" aria-selected="false" onclick="switchTab('list')">Intenções</button>
    <button class="nav-btn" id="tab-ai" role="tab" aria-selected="false" onclick="switchTab('ai')">IA</button>
  </nav>
</header>

<main class="main" id="main-content" role="main">

  <!-- API KEY NOTICE -->
  <div class="api-notice" id="api-notice" role="alert" aria-live="polite">
    <span aria-hidden="true">🔑</span>
    <div style="flex:1;">
      <strong>Chave da API Anthropic</strong><br>
      <span>Para o assistente IA funcionar, insira sua chave:</span>
      <div style="display:flex;gap:6px;margin-top:6px;">
        <input type="password" id="api-key-input" placeholder="sk-ant-..." aria-label="Chave da API Anthropic"/>
        <button onclick="saveApiKey()" aria-label="Salvar chave da API">Salvar</button>
      </div>
    </div>
  </div>

  <!-- TAB: CAPTURE -->
  <section id="panel-capture" role="tabpanel" aria-label="Capturar intenção">
    <div class="capture-card">
      <div class="capture-label" id="capture-label">
        <span aria-hidden="true">✏️</span> O que você quer lembrar?
      </div>
      <textarea
        class="capture-textarea"
        id="intention-text"
        aria-labelledby="capture-label"
        aria-required="true"
        placeholder="Ex: quando eu chegar em casa, quero meditar por 10 minutos..."
        rows="3"
        maxlength="300"
      ></textarea>
      <div class="tags-row" id="selected-tags" aria-live="polite" aria-label="Contexto selecionado"></div>
      <div class="capture-row" role="group" aria-label="Contexto da intenção">
        <button class="context-btn" id="ctx-casa" onclick="toggleCtx(this,'🏠','casa')" aria-pressed="false">🏠 Casa</button>
        <button class="context-btn" id="ctx-trabalho" onclick="toggleCtx(this,'💼','trabalho')" aria-pressed="false">💼 Trabalho</button>
        <button class="context-btn" id="ctx-ideia" onclick="toggleCtx(this,'💡','ideia')" aria-pressed="false">💡 Ideia</button>
        <button class="context-btn" id="ctx-social" onclick="toggleCtx(this,'👥','social')" aria-pressed="false">👥 Social</button>
        <button class="save-btn" onclick="saveIntention()" aria-label="Salvar esta intenção" id="save-btn">Salvar</button>
      </div>
    </div>

    <div id="quick-suggestions">
      <div class="section-title">Sugestões rápidas</div>
      <div style="display:flex;flex-direction:column;gap:8px;" role="list">
        <button class="intention-card" role="listitem" style="border:0.5px dashed var(--border);background:transparent;width:100%;text-align:left;font-family:var(--font);" onclick="fillSuggestion('Quando eu chegar em casa, quero ligar para minha família','casa')">
          <div class="intention-icon casa" aria-hidden="true">🏠</div>
          <div><div class="intention-title">Ligar para a família</div><div class="intention-meta"><span>Ao chegar em casa</span></div></div>
        </button>
        <button class="intention-card" role="listitem" style="border:0.5px dashed var(--border);background:transparent;width:100%;text-align:left;font-family:var(--font);" onclick="fillSuggestion('Preciso registrar a ideia que tive sobre o projeto de IA','ideia')">
          <div class="intention-icon ideia" aria-hidden="true">💡</div>
          <div><div class="intention-title">Registrar ideia de IA</div><div class="intention-meta"><span>Agora</span></div></div>
        </button>
        <button class="intention-card" role="listitem" style="border:0.5px dashed var(--border);background:transparent;width:100%;text-align:left;font-family:var(--font);" onclick="fillSuggestion('No próximo encontro com amigos, quero propor um jogo novo','social')">
          <div class="intention-icon social" aria-hidden="true">👥</div>
          <div><div class="intention-title">Propor jogo aos amigos</div><div class="intention-meta"><span>Próximo encontro</span></div></div>
        </button>
      </div>
    </div>
  </section>

  <!-- TAB: LIST -->
  <section id="panel-list" role="tabpanel" aria-label="Lista de intenções" hidden>
    <div class="section-title">
      Suas intenções <span class="badge" id="count-badge" aria-label="total de intenções">0</span>
    </div>
    <div id="intentions-list" aria-live="polite" aria-relevant="additions removals">
      <div class="empty-state" id="empty-state">
        <div class="empty-icon" aria-hidden="true">📭</div>
        <div class="empty-text">Nenhuma intenção ainda.<br>Vá à aba <strong>Capturar</strong> e registre a primeira!</div>
      </div>
    </div>
  </section>

  <!-- TAB: AI -->
  <section id="panel-ai" role="tabpanel" aria-label="Assistente IA" hidden>
    <div class="ai-panel" role="region" aria-label="Chat com assistente">
      <div class="ai-header">
        <div class="ai-avatar" aria-hidden="true">🤖</div>
        <div>
          <div class="ai-name">Assistente ContextCast</div>
          <div class="ai-sub">Powered by Claude</div>
        </div>
      </div>
      <div class="chat-body" id="chat-body" role="log" aria-live="polite" aria-label="Conversa com IA">
        <div class="msg ai" role="article">Olá! Sou seu assistente de intenções. Posso te ajudar a refletir sobre suas intenções, identificar padrões e desenvolver seus pensamentos. O que você gostaria de explorar?</div>
      </div>
      <div class="chat-input-row">
        <input
          class="chat-input"
          id="chat-input"
          type="text"
          placeholder="Digite uma mensagem..."
          aria-label="Mensagem para o assistente"
          onkeydown="if(event.key==='Enter')sendMsg()"
        />
        <button class="send-btn" onclick="sendMsg()" id="send-btn" aria-label="Enviar mensagem">Enviar</button>
      </div>
    </div>
  </section>

</main>

<!-- DETAIL MODAL -->
<div class="modal-overlay" id="modal" hidden role="dialog" aria-modal="true" aria-labelledby="modal-title-el" onclick="closeModal(event)">
  <div class="modal" id="modal-content">
    <div class="modal-handle" aria-hidden="true"></div>
    <button class="modal-close" onclick="closeModal()" aria-label="Fechar">✕</button>
    <h2 class="modal-title" id="modal-title-el"></h2>
    <div class="modal-section"><div class="modal-label">Contexto</div><div class="modal-value" id="modal-ctx"></div></div>
    <div class="modal-section"><div class="modal-label">Criada em</div><div class="modal-value" id="modal-date"></div></div>
    <div class="modal-section"><div class="modal-label">Status</div><div class="modal-value" id="modal-status"></div></div>
    <div class="modal-section" id="modal-reflection-section" hidden>
      <div class="modal-label">Reflexão da IA</div>
      <div class="modal-value" id="modal-reflection" style="font-size:14px;color:var(--text2);line-height:1.6;"></div>
    </div>
    <div class="modal-actions">
      <button class="save-btn" onclick="markDone()" id="modal-done-btn" aria-label="Marcar como concluída">✓ Concluída</button>
      <button class="btn-outline" onclick="getAIReflection()" id="modal-ai-btn" aria-label="Pedir reflexão da IA">🤖 Reflexão da IA</button>
      <button class="btn-danger" onclick="deleteIntention()" aria-label="Excluir intenção">Excluir</button>
    </div>
  </div>
</div>

<script>
let intentions = JSON.parse(localStorage.getItem('cc_intentions') || '[]');
let apiKey = localStorage.getItem('cc_apikey') || '';
let selectedCtx = [];
let currentModal = null;
let chatHistory = [];

if(apiKey) document.getElementById('api-notice').style.display='none';

function saveApiKey(){
  const k = document.getElementById('api-key-input').value.trim();
  if(!k){alert('Por favor insira uma chave válida.');return;}
  apiKey = k;
  localStorage.setItem('cc_apikey', k);
  document.getElementById('api-notice').style.display='none';
  announce('Chave salva com sucesso!');
}

function announce(msg){
  let el = document.getElementById('live-announce');
  if(!el){el=document.createElement('div');el.id='live-announce';el.setAttribute('aria-live','assertive');el.className='sr-only';document.body.appendChild(el);}
  el.textContent='';
  setTimeout(()=>{el.textContent=msg;},50);
}

function switchTab(tab){
  ['capture','list','ai'].forEach(t=>{
    document.getElementById('panel-'+t).hidden = (t!==tab);
    document.getElementById('tab-'+t).setAttribute('aria-selected', t===tab ? 'true':'false');
  });
  if(tab==='list') renderList();
  document.getElementById('panel-'+tab).focus?.();
}

function toggleCtx(btn, emoji, ctx){
  const pressed = btn.getAttribute('aria-pressed')==='true';
  btn.setAttribute('aria-pressed', !pressed);
  btn.classList.toggle('active', !pressed);
  if(!pressed){ selectedCtx.push({emoji,ctx}); }
  else { selectedCtx = selectedCtx.filter(c=>c.ctx!==ctx); }
  renderSelectedTags();
}

function renderSelectedTags(){
  const el = document.getElementById('selected-tags');
  el.innerHTML = selectedCtx.map(c=>`<span class="tag">${c.emoji} ${c.ctx}</span>`).join('');
}

function saveIntention(){
  const text = document.getElementById('intention-text').value.trim();
  if(!text){
    announce('Por favor escreva uma intenção antes de salvar.');
    document.getElementById('intention-text').focus();
    return;
  }
  const intention = {
    id: Date.now(),
    text,
    ctx: [...selectedCtx],
    date: new Date().toISOString(),
    status: 'pending',
    reflection: null
  };
  intentions.unshift(intention);
  localStorage.setItem('cc_intentions', JSON.stringify(intentions));
  document.getElementById('intention-text').value='';
  selectedCtx=[];
  document.querySelectorAll('.context-btn').forEach(b=>{b.classList.remove('active');b.setAttribute('aria-pressed','false');});
  renderSelectedTags();
  announce('Intenção salva com sucesso!');
  switchTab('list');
}

function fillSuggestion(text, ctx){
  document.getElementById('intention-text').value = text;
  const btn = document.getElementById('ctx-'+ctx);
  if(btn && btn.getAttribute('aria-pressed')==='false'){
    const emojiMap = {casa:'🏠',trabalho:'💼',ideia:'💡',social:'👥'};
    toggleCtx(btn, emojiMap[ctx], ctx);
  }
  document.getElementById('intention-text').focus();
}

function renderList(){
  const el = document.getElementById('intentions-list');
  const emptyState = document.getElementById('empty-state');
  document.getElementById('count-badge').textContent = intentions.length;
  document.getElementById('count-badge').setAttribute('aria-label', intentions.length + ' intenções');

  if(intentions.length===0){
    emptyState.hidden=false;
    return;
  }
  emptyState.hidden=true;

  const iconMap={casa:'🏠 casa',trabalho:'💼 trabalho',ideia:'💡 ideia',social:'👥 social'};
  const classMap={casa:'casa',trabalho:'trabalho',ideia:'ideia',social:'social'};

  el.innerHTML = '';
  intentions.forEach(i=>{
    const ctxClass = i.ctx.length ? classMap[i.ctx[0].ctx]||'ideia' : 'ideia';
    const ctxEmoji = i.ctx.length ? i.ctx[0].emoji : '📌';
    const date = new Date(i.date).toLocaleDateString('pt-BR',{day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'});
    const div = document.createElement('button');
    div.className='intention-card';
    div.setAttribute('tabindex','0');
    div.setAttribute('aria-label', `Intenção: ${i.text}. Status: ${i.status==='done'?'concluída':'pendente'}. Clique para ver detalhes.`);
    div.style.cssText='width:100%;text-align:left;background:var(--surface);border:0.5px solid var(--border);cursor:pointer;font-family:var(--font);';
    div.innerHTML=`
      <div class="intention-icon ${ctxClass}" aria-hidden="true">${ctxEmoji}</div>
      <div style="flex:1;min-width:0;">
        <div class="intention-title" style="${i.status==='done'?'text-decoration:line-through;opacity:0.6;':''}">${escapeHtml(i.text)}</div>
        <div class="intention-meta">
          <span><span class="status-dot ${i.status}" aria-hidden="true"></span>${i.status==='done'?'Concluída':'Pendente'}</span>
          ${i.ctx.map(c=>`<span>${c.emoji} ${c.ctx}</span>`).join('')}
        </div>
      </div>
      <div class="intention-time" aria-hidden="true">${date}</div>
    `;
    div.onclick=()=>openModal(i.id);
    el.appendChild(div);
  });
}

function escapeHtml(t){return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}

function openModal(id){
  const i = intentions.find(x=>x.id===id);
  if(!i) return;
  currentModal = id;
  document.getElementById('modal-title-el').textContent = i.text;
  document.getElementById('modal-ctx').textContent = i.ctx.length ? i.ctx.map(c=>c.emoji+' '+c.ctx).join(', ') : 'Geral';
  document.getElementById('modal-date').textContent = new Date(i.date).toLocaleString('pt-BR');
  document.getElementById('modal-status').textContent = i.status==='done' ? '✓ Concluída' : '⏳ Pendente';
  const refSec = document.getElementById('modal-reflection-section');
  if(i.reflection){
    refSec.hidden=false;
    document.getElementById('modal-reflection').textContent = i.reflection;
  } else { refSec.hidden=true; }
  document.getElementById('modal-done-btn').disabled = i.status==='done';
  document.getElementById('modal').hidden=false;
  document.getElementById('modal-content').focus?.();
  document.body.style.overflow='hidden';
}

function closeModal(e){
  if(e && e.target!==document.getElementById('modal') && e.type==='click') return;
  document.getElementById('modal').hidden=true;
  document.body.style.overflow='';
  currentModal=null;
}

document.addEventListener('keydown',e=>{
  if(e.key==='Escape' && !document.getElementById('modal').hidden) closeModal();
});

function markDone(){
  if(!currentModal) return;
  const i = intentions.find(x=>x.id===currentModal);
  if(i){ i.status='done'; localStorage.setItem('cc_intentions',JSON.stringify(intentions)); announce('Intenção marcada como concluída!'); closeModal(); renderList(); }
}

function deleteIntention(){
  if(!currentModal) return;
  if(!confirm('Excluir esta intenção?')) return;
  intentions = intentions.filter(x=>x.id!==currentModal);
  localStorage.setItem('cc_intentions',JSON.stringify(intentions));
  announce('Intenção excluída.');
  closeModal();
  renderList();
}

async function getAIReflection(){
  if(!currentModal) return;
  if(!apiKey){ announce('Configure sua chave da API primeiro.'); return; }
  const i = intentions.find(x=>x.id===currentModal);
  if(!i) return;
  const btn = document.getElementById('modal-ai-btn');
  btn.disabled=true;
  btn.textContent='Gerando...';
  try{
    const resp = await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':apiKey,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({
        model:'claude-sonnet-4-20250514',
        max_tokens:300,
        messages:[{role:'user',content:`Sou usuário do app ContextCast. Registrei esta intenção: "${i.text}". Contexto: ${i.ctx.map(c=>c.ctx).join(', ')||'geral'}. Faça uma reflexão curta e útil (3-4 frases) que me ajude a desenvolver ou executar melhor essa intenção. Seja empático e prático.`}]
      })
    });
    const data = await resp.json();
    const reflection = data.content?.[0]?.text || 'Não foi possível gerar reflexão.';
    i.reflection = reflection;
    localStorage.setItem('cc_intentions',JSON.stringify(intentions));
    document.getElementById('modal-reflection').textContent = reflection;
    document.getElementById('modal-reflection-section').hidden=false;
    announce('Reflexão da IA gerada com sucesso!');
  } catch(e){
    announce('Erro ao contatar a IA. Verifique sua chave.');
  }
  btn.disabled=false;
  btn.textContent='🤖 Reflexão da IA';
}

async function sendMsg(){
  if(!apiKey){ announce('Configure sua chave da API primeiro.'); return; }
  const input = document.getElementById('chat-input');
  const text = input.value.trim();
  if(!text) return;
  input.value='';
  const body = document.getElementById('chat-body');
  const userMsg = document.createElement('div');
  userMsg.className='msg user';
  userMsg.setAttribute('role','article');
  userMsg.setAttribute('aria-label','Você disse: '+text);
  userMsg.textContent=text;
  body.appendChild(userMsg);
  const loading = document.createElement('div');
  loading.className='msg loading';
  loading.setAttribute('aria-label','Assistente digitando...');
  loading.innerHTML='<div class="dot"></div><div class="dot"></div><div class="dot"></div>';
  body.appendChild(loading);
  body.scrollTop=body.scrollHeight;
  document.getElementById('send-btn').disabled=true;
  chatHistory.push({role:'user',content:text});
  const ctx = intentions.slice(0,5).map(i=>`- "${i.text}" [${i.status}]`).join('\n');
  const systemPrompt = `Você é o assistente ContextCast, um diário inteligente de intenções. Ajude o usuário a refletir, desenvolver e executar suas intenções de forma empática e prática. Suas últimas intenções registradas:\n${ctx||'Nenhuma ainda.'}\nResponda sempre em português, de forma concisa e útil.`;
  try{
    const resp = await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':apiKey,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:400,system:systemPrompt,messages:chatHistory})
    });
    const data = await resp.json();
    const reply = data.content?.[0]?.text || 'Não consegui responder. Tente novamente.';
    chatHistory.push({role:'assistant',content:reply});
    loading.remove();
    const aiMsg = document.createElement('div');
    aiMsg.className='msg ai';
    aiMsg.setAttribute('role','article');
    aiMsg.setAttribute('aria-label','Assistente disse: '+reply);
    aiMsg.textContent=reply;
    body.appendChild(aiMsg);
    body.scrollTop=body.scrollHeight;
  } catch(e){
    loading.remove();
    const errMsg = document.createElement('div');
    errMsg.className='msg ai';
    errMsg.textContent='Erro ao contatar a IA. Verifique sua chave da API.';
    body.appendChild(errMsg);
  }
  document.getElementById('send-btn').disabled=false;
  input.focus();
}

renderList();
</script>
</body>
</html>
