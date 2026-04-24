<!DOCTYPE html>  
<html lang="es">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>Buzón del Equipo ✨</title>  
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">  
<style>  
  :root {  
    --cream: #FAF7F2;  
    --warm: #F0E8DA;  
    --blush: #E8C4B8;  
    --rose: #C97B6B;  
    --deep: #3D2B2B;  
    --ink: #5C3D3D;  
    --gold: #C4935A;  
    --green: #7A9E87;  
  }  
  
  * { margin: 0; padding: 0; box-sizing: border-box; }  
  
  body {  
    font-family: 'DM Sans', sans-serif;  
    background: var(--cream);  
    color: var(--deep);  
    min-height: 100vh;  
  }  
  
  /* --- NOISE TEXTURE OVERLAY --- */  
  body::before {  
    content: '';  
    position: fixed; inset: 0;  
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='[http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)](http://www.w3.org/2000/svg'%253E%253Cfilter%20id='n'%253E%253CfeTurbulence%20type='fractalNoise'%20baseFrequency='0.75'%20numOctaves='4'%20stitchTiles='stitch'/%253E%253C/filter%253E%253Crect%20width='100%2525'%20height='100%2525'%20filter='url(%2523n))' opacity='0.03'/%3E%3C/svg%3E");  
    pointer-events: none;  
    z-index: 0;  
  }  
  
  .app { position: relative; z-index: 1; max-width: 480px; margin: 0 auto; padding: 0 20px 60px; }  
  
  /* --- HEADER --- */  
  header {  
    padding: 40px 0 32px;  
    text-align: center;  
    border-bottom: 1px solid var(--blush);  
    margin-bottom: 32px;  
  }  
  
  .tag {  
    display: inline-block;  
    font-size: 10px;  
    letter-spacing: 0.2em;  
    text-transform: uppercase;  
    color: var(--rose);  
    background: rgba(232,196,184,0.3);  
    padding: 4px 12px;  
    border-radius: 20px;  
    margin-bottom: 12px;  
  }  
  
  h1 {  
    font-family: 'Playfair Display', serif;  
    font-size: 2rem;  
    line-height: 1.15;  
    color: var(--deep);  
    margin-bottom: 8px;  
  }  
  
  h1 em { font-style: italic; color: var(--rose); }  
  
  header p {  
    font-size: 0.85rem;  
    color: var(--ink);  
    opacity: 0.7;  
    line-height: 1.5;  
  }  
  
  /* --- ANON BADGE --- */  
  .anon-badge {  
    display: flex;  
    align-items: center;  
    gap: 10px;  
    background: rgba(122,158,135,0.12);  
    border: 1px solid rgba(122,158,135,0.3);  
    border-radius: 12px;  
    padding: 12px 16px;  
    margin-bottom: 28px;  
    font-size: 0.8rem;  
    color: var(--green);  
  }  
  .anon-badge svg { flex-shrink: 0; }  
  
  /* --- TYPE SELECTOR --- */  
  .type-selector {  
    display: grid;  
    grid-template-columns: 1fr 1fr;  
    gap: 10px;  
    margin-bottom: 24px;  
  }  
  
  .type-btn {  
    border: 1.5px solid var(--warm);  
    background: var(--warm);  
    border-radius: 14px;  
    padding: 16px 12px;  
    cursor: pointer;  
    text-align: center;  
    transition: all 0.2s ease;  
  }  
  
  .type-btn:hover { border-color: var(--blush); }  
  
  .type-btn.active.halago {  
    background: rgba(232,196,184,0.4);  
    border-color: var(--rose);  
  }  
  
  .type-btn.active.feedback {  
    background: rgba(196,147,90,0.12);  
    border-color: var(--gold);  
  }  
  
  .type-btn .icon { font-size: 1.6rem; margin-bottom: 4px; }  
  .type-btn .label { font-size: 0.78rem; font-weight: 500; color: var(--ink); }  
  .type-btn .sublabel { font-size: 0.7rem; color: var(--ink); opacity: 0.5; margin-top: 2px; }  
  
  /* --- FOR WHOM --- */  
  .section-label {  
    font-size: 0.75rem;  
    text-transform: uppercase;  
    letter-spacing: 0.1em;  
    color: var(--rose);  
    margin-bottom: 10px;  
    font-weight: 500;  
  }  
  
  .recipient-grid {  
    display: flex;  
    flex-wrap: wrap;  
    gap: 8px;  
    margin-bottom: 24px;  
  }  
  
  .chip {  
    border: 1.5px solid var(--warm);  
    background: var(--warm);  
    border-radius: 20px;  
    padding: 7px 14px;  
    font-size: 0.8rem;  
    cursor: pointer;  
    transition: all 0.15s;  
    color: var(--ink);  
  }  
  
  .chip:hover { border-color: var(--blush); }  
  .chip.selected { background: var(--blush); border-color: var(--rose); color: var(--deep); font-weight: 500; }  
  .chip.team { background: rgba(122,158,135,0.15); border-color: rgba(122,158,135,0.4); color: var(--green); }  
  .chip.team.selected { background: rgba(122,158,135,0.35); border-color: var(--green); }  
  
  /* --- MESSAGE BOX --- */  
  .message-wrap {  
    margin-bottom: 24px;  
    position: relative;  
  }  
  
  textarea {  
    width: 100%;  
    min-height: 130px;  
    background: var(--warm);  
    border: 1.5px solid var(--warm);  
    border-radius: 16px;  
    padding: 16px;  
    font-family: 'DM Sans', sans-serif;  
    font-size: 0.9rem;  
    color: var(--deep);  
    resize: none;  
    outline: none;  
    transition: border-color 0.2s;  
    line-height: 1.5;  
  }  
  
  textarea::placeholder { color: var(--ink); opacity: 0.35; }  
  textarea:focus { border-color: var(--rose); }  
  
  .char-count {  
    position: absolute;  
    bottom: 10px;  
    right: 14px;  
    font-size: 0.7rem;  
    opacity: 0.35;  
  }  
  
  /* --- SEND BUTTON --- */  
  .send-btn {  
    width: 100%;  
    background: var(--deep);  
    color: var(--cream);  
    border: none;  
    border-radius: 16px;  
    padding: 16px;  
    font-family: 'DM Sans', sans-serif;  
    font-size: 0.9rem;  
    font-weight: 500;  
    cursor: pointer;  
    transition: all 0.2s;  
    letter-spacing: 0.02em;  
  }  
  
  .send-btn:hover { background: var(--rose); }  
  .send-btn:active { transform: scale(0.98); }  
  .send-btn:disabled { opacity: 0.4; cursor: not-allowed; }  
  
  /* --- SUCCESS STATE --- */  
  .success {  
    display: none;  
    text-align: center;  
    padding: 40px 20px;  
    animation: fadeIn 0.4s ease;  
  }  
  
  .success.show { display: block; }  
  
  .success-icon { font-size: 3rem; margin-bottom: 16px; }  
  
  .success h2 {  
    font-family: 'Playfair Display', serif;  
    font-size: 1.5rem;  
    margin-bottom: 8px;  
    color: var(--deep);  
  }  
  
  .success p { font-size: 0.85rem; color: var(--ink); opacity: 0.7; margin-bottom: 24px; }  
  
  .reset-btn {  
    background: var(--warm);  
    border: 1.5px solid var(--blush);  
    border-radius: 12px;  
    padding: 10px 24px;  
    font-family: 'DM Sans', sans-serif;  
    font-size: 0.85rem;  
    cursor: pointer;  
    color: var(--ink);  
    transition: all 0.2s;  
  }  
  .reset-btn:hover { background: var(--blush); }  
  
  /* --- MESSAGES PANEL (moderator view) --- */  
  .mod-toggle {  
    text-align: center;  
    margin-top: 40px;  
    padding-top: 24px;  
    border-top: 1px dashed var(--blush);  
  }  
  
  .mod-btn {  
    font-size: 0.72rem;  
    color: var(--ink);  
    opacity: 0.3;  
    cursor: pointer;  
    background: none;  
    border: none;  
    font-family: 'DM Sans', sans-serif;  
    text-decoration: underline dotted;  
  }  
  
  .mod-panel { display: none; margin-top: 20px; }  
  .mod-panel.open { display: block; }  
  
  .mod-header {  
    display: flex;  
    align-items: center;  
    justify-content: space-between;  
    margin-bottom: 16px;  
  }  
  
  .mod-title {  
    font-family: 'Playfair Display', serif;  
    font-size: 1.1rem;  
    font-style: italic;  
  }  
  
  .clear-btn {  
    font-size: 0.72rem;  
    color: var(--rose);  
    background: none;  
    border: none;  
    cursor: pointer;  
    font-family: 'DM Sans', sans-serif;  
  }  
  
  .messages-list { display: flex; flex-direction: column; gap: 12px; }  
  
  .msg-card {  
    background: var(--warm);  
    border-radius: 14px;  
    padding: 14px 16px;  
    border-left: 3px solid var(--blush);  
    animation: slideUp 0.3s ease;  
  }  
  
  .msg-card.feedback { border-left-color: var(--gold); }  
  
  .msg-meta {  
    display: flex;  
    align-items: center;  
    justify-content: space-between;  
    margin-bottom: 8px;  
  }  
  
  .msg-type { font-size: 0.7rem; font-weight: 500; }  
  .msg-type.halago { color: var(--rose); }  
  .msg-type.feedback { color: var(--gold); }  
  
  .msg-to { font-size: 0.7rem; color: var(--ink); opacity: 0.5; }  
  .msg-text { font-size: 0.85rem; line-height: 1.5; color: var(--deep); }  
  .msg-time { font-size: 0.65rem; color: var(--ink); opacity: 0.35; margin-top: 6px; }  
  
  .empty-state {  
    text-align: center;  
    padding: 30px;  
    font-size: 0.82rem;  
    color: var(--ink);  
    opacity: 0.4;  
  }  
  
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }  
  @keyframes slideUp { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }  
</style>  
</head>  
<body>  
<div class="app">  
  
  <!-- HEADER -->  
  <header>  
    <div class="tag">💌 100% anónimo</div>  
    <h1>Buzón del<br><em>Equipo</em></h1>  
    <p>Comparte un halago o feedback con alguna compañera.<br>Tu identidad nunca se guarda.</p>  
  </header>  
  
  <!-- FORM -->  
  <div id="form-section">  
  
    <div class="anon-badge">  
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">  
        <rect x="3" y="11" width="18" height="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/>  
      </svg>  
      <span>No se guarda ningún dato tuyo. Nadie sabe quién escribe.</span>  
    </div>  
  
    <!-- TYPE -->  
    <div class="section-label">¿Qué quieres enviar?</div>  
    <div class="type-selector">  
      <div class="type-btn halago active" onclick="selectType('halago', this)">  
        <div class="icon">✨</div>  
        <div class="label">Halago</div>  
        <div class="sublabel">Reconocer algo bonito</div>  
      </div>  
      <div class="type-btn feedback" onclick="selectType('feedback', this)">  
        <div class="icon">💬</div>  
        <div class="label">Feedback</div>  
        <div class="sublabel">Algo que mejorar</div>  
      </div>  
    </div>  
  
    <!-- PARA QUIÉN -->  
    <div class="section-label">¿Para quién es?</div>  
    <div class="recipient-grid" id="recipients">  
      <div class="chip team selected" onclick="toggleChip(this)" data-name="Todo el equipo">Todo el equipo 🌿</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Alexia">Alexia</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Gilda">Gilda</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Baby">Baby</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Pris Tyler">Pris Tyler</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Pris Heimpel">Pris Heimpel</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Angie">Angie</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Reyna">Reyna</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Nalleli">Nalleli</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Claudia">Claudia</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Rubí">Rubí</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Brenda">Brenda</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Ale">Ale</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Camila">Camila</div>  
      <div class="chip" onclick="toggleChip(this)" data-name="Mafer">Mafer</div>  
    </div>  
  
    <!-- MENSAJE -->  
    <div class="section-label">Tu mensaje</div>  
    <div class="message-wrap">  
      <textarea id="msg-input" maxlength="400" placeholder="Escribe aquí... puede ser algo tan simple como 'gracias por tu energía hoy' 💛" oninput="updateCount()"></textarea>  
      <span class="char-count" id="char-count">0/400</span>  
    </div>  
  
    <button class="send-btn" id="send-btn" onclick="sendMessage()">Enviar anónimamente →</button>  
  
  </div>  
  
  <!-- SUCCESS -->  
  <div class="success" id="success-section">  
    <div class="success-icon">🌸</div>  
    <h2>¡Enviado!</h2>  
    <p>Tu mensaje llegó de forma anónima.<br>Gracias por construir el equipo.</p>  
    <button class="reset-btn" onclick="resetForm()">Enviar otro mensaje</button>  
  </div>  
  
  <!-- MOD VIEW -->  
  <div class="mod-toggle">  
    <button class="mod-btn" onclick="toggleMod()">ver mensajes (moderadora)</button>  
  </div>  
  
  <div class="mod-panel" id="mod-panel">  
    <div class="mod-header">  
      <span class="mod-title">Mensajes recibidos</span>  
      <button class="clear-btn" onclick="clearMessages()">Limpiar todo</button>  
    </div>  
    <div class="messages-list" id="messages-list">  
      <div class="empty-state">Aún no hay mensajes 🌱</div>  
    </div>  
  </div>  
  
</div>  
  
<script>  
  let selectedType = 'halago';  
  let selectedRecipient = 'Todo el equipo';  
  let messages = JSON.parse(localStorage.getItem('buzon_msgs') || '[]');  
  
  function selectType(type, el) {  
    selectedType = type;  
    document.querySelectorAll('.type-btn').forEach(b => b.classList.remove('active'));  
    el.classList.add('active');  
    updatePlaceholder();  
  }  
  
  function updatePlaceholder() {  
    const ta = document.getElementById('msg-input');  
    if (selectedType === 'halago') {  
      ta.placeholder = 'Escribe aquí... puede ser algo tan simple como "gracias por tu energía hoy" 💛';  
    } else {  
      ta.placeholder = 'Escribe tu feedback con respeto y buena intención 🌿';  
    }  
  }  
  
  function toggleChip(el) {  
    document.querySelectorAll('.chip').forEach(c => c.classList.remove('selected'));  
    el.classList.add('selected');  
    selectedRecipient = el.dataset.name;  
  }  
  
  function updateCount() {  
    const val = document.getElementById('msg-input').value.length;  
    document.getElementById('char-count').textContent = val + '/400';  
  }  
  
  const SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbxjpWMuzxlOSsLroEMy5ApMWhj6zG48BbhXd-qLebZwOteQ1jKgEm70qSr4yGG0SxOtAQ/exec';  
  
  async function sendMessage() {  
    const text = document.getElementById('msg-input').value.trim();  
    if (!text) return;  
  
    const btn = document.getElementById('send-btn');  
    btn.disabled = true;  
    btn.textContent = 'Enviando...';  
  
    const payload = {  
      tipo: selectedType === 'halago' ? '✨ Halago' : '💬 Feedback',  
      para: selectedRecipient,  
      admiro: selectedType === 'halago' ? text : '',  
      bienHace: '',  
      sugerencia: selectedType === 'feedback' ? text : ''  
    };  
  
    try {  
      await fetch(SCRIPT_URL, {  
        method: 'POST',  
        mode: 'no-cors',  
        headers: { 'Content-Type': 'application/json' },  
        body: JSON.stringify(payload)  
      });  
  
      // Also save locally as backup  
      const msg = {  
        type: selectedType,  
        to: selectedRecipient,  
        text,  
        time: new Date().toLocaleTimeString('es-MX', { hour: '2-digit', minute: '2-digit' }) + ' · ' +  
              new Date().toLocaleDateString('es-MX', { day: 'numeric', month: 'short' })  
      };  
      messages.unshift(msg);  
      localStorage.setItem('buzon_msgs', JSON.stringify(messages));  
  
    } catch (e) {  
      console.log('Error al enviar, guardado solo local');  
    }  
  
    btn.disabled = false;  
    btn.textContent = 'Enviar anónimamente →';  
    document.getElementById('form-section').style.display = 'none';  
    document.getElementById('success-section').classList.add('show');  
  }  
  
  function resetForm() {  
    document.getElementById('msg-input').value = '';  
    document.getElementById('char-count').textContent = '0/400';  
    selectedType = 'halago';  
    selectedRecipient = 'Todo el equipo';  
    document.querySelectorAll('.type-btn').forEach(b => b.classList.remove('active'));  
    document.querySelector('.type-btn.halago').classList.add('active');  
    document.querySelectorAll('.chip').forEach(c => c.classList.remove('selected'));  
    document.querySelector('.chip.team').classList.add('selected');  
    document.getElementById('form-section').style.display = 'block';  
    document.getElementById('success-section').classList.remove('show');  
  }  
  
  function toggleMod() {  
    const panel = document.getElementById('mod-panel');  
    panel.classList.toggle('open');  
    renderMessages();  
  }  
  
  function renderMessages() {  
    const list = document.getElementById('messages-list');  
    if (messages.length === 0) {  
      list.innerHTML = '<div class="empty-state">Aún no hay mensajes 🌱</div>';  
      return;  
    }  
    list.innerHTML = messages.map(m => `  
      <div class="msg-card ${m.type}">  
        <div class="msg-meta">  
          <span class="msg-type ${m.type}">${m.type === 'halago' ? '✨ Halago' : '💬 Feedback'}</span>  
          <span class="msg-to">Para: ${m.to}</span>  
        </div>  
        <div class="msg-text">${m.text}</div>  
        <div class="msg-time">${m.time}</div>  
      </div>  
    `).join('');  
  }  
  
  function clearMessages() {  
    if (confirm('¿Segura que quieres borrar todos los mensajes?')) {  
      messages = [];  
      localStorage.removeItem('buzon_msgs');  
      renderMessages();  
    }  
  }  
</script>  
</body>  
</html>  
