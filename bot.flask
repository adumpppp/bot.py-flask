<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Gatcha Bandar</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
* { margin:0; padding:0; box-sizing:border-box; }
body {
  background:#0f0f1a; color:white;
  font-family:Arial,sans-serif; min-height:100vh;
  padding:16px; padding-bottom:32px;
}
.header { display:flex; align-items:center; gap:12px; margin-bottom:20px; }
.avatar {
  width:48px; height:48px; border-radius:50%;
  background:linear-gradient(135deg,#f0c040,#e07020);
  display:flex; align-items:center; justify-content:center;
  font-size:22px; font-weight:bold; flex-shrink:0;
}
.user-info { flex:1; }
.user-name { font-size:16px; font-weight:bold; }
.user-id { font-size:11px; color:#888; }
.saldo-card {
  background:linear-gradient(135deg,#1a1a3e,#0f3460);
  border-radius:16px; padding:20px; margin-bottom:16px;
  text-align:center; border:1px solid #1e4080;
}
.saldo-label { font-size:12px; color:#aaa; margin-bottom:4px; }
.saldo-amount { font-size:32px; font-weight:bold; color:#f0c040; }
.saldo-sub { font-size:12px; color:#888; margin-top:4px; }
.dw-row { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:20px; }
.btn-dw {
  border:none; border-radius:12px; padding:14px;
  font-size:14px; font-weight:bold; cursor:pointer;
  display:flex; align-items:center; justify-content:center; gap:8px;
}
.btn-deposit { background:linear-gradient(135deg,#1a7a4a,#0f5a30); color:white; }
.btn-withdraw { background:linear-gradient(135deg,#7a1a1a,#5a0f0f); color:white; }
.section-title { font-size:12px; color:#888; margin-bottom:10px; text-transform:uppercase; letter-spacing:1px; }
.btn-primary {
  width:100%; border:none; border-radius:12px; padding:15px;
  font-size:15px; font-weight:bold; cursor:pointer; margin-bottom:10px;
  background:linear-gradient(135deg,#f0c040,#e07020); color:#1a1a2e;
}
.btn-secondary {
  width:100%; border:1px solid #1e3060; border-radius:12px; padding:15px;
  font-size:15px; font-weight:bold; cursor:pointer; margin-bottom:10px;
  background:#16213e; color:white;
}
.room-list { display:flex; flex-direction:column; gap:10px; margin-bottom:20px; }
.room-card {
  background:#16213e; border-radius:14px; padding:16px;
  border:1px solid #1e3060; cursor:pointer; transition:all 0.15s;
}
.room-card:active { border-color:#f0c040; transform:scale(0.98); }
.room-card-header { display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; }
.room-card-name { font-size:15px; font-weight:bold; }
.badge {
  font-size:10px; padding:3px 8px; border-radius:20px; font-weight:bold;
}
.badge-waiting { background:#1a4a1a; color:#4afa4a; }
.badge-playing { background:#4a1a1a; color:#fa4a4a; }
.room-card-info { font-size:12px; color:#888; }
.empty-state { text-align:center; padding:40px 0; color:#666; }
.modal-overlay {
  display:none; position:fixed; top:0; left:0; width:100%; height:100%;
  background:rgba(0,0,0,0.75); z-index:100; align-items:center; justify-content:center;
}
.modal-overlay.aktif { display:flex; }
.modal-box {
  background:#16213e; border-radius:16px; padding:24px;
  width:90%; max-width:360px; border:1px solid #1e3060;
}
.modal-title { font-size:17px; font-weight:bold; margin-bottom:12px; }
.input-field {
  width:100%; background:#0f0f1a; border:1px solid #1e3060;
  border-radius:10px; padding:12px; color:white; font-size:14px;
  margin-bottom:10px; outline:none;
}
.input-field:focus { border-color:#f0c040; }
.input-row { display:grid; grid-template-columns:1fr 1fr; gap:8px; }
.input-label { font-size:11px; color:#888; margin-bottom:4px; }
.modal-actions { display:grid; grid-template-columns:1fr 1fr; gap:8px; margin-top:12px; }
.btn-confirm {
  border:none; border-radius:10px; padding:12px;
  font-size:14px; font-weight:bold; cursor:pointer;
  background:linear-gradient(135deg,#f0c040,#e07020); color:#1a1a2e;
}
.btn-cancel {
  border:1px solid #333; border-radius:10px; padding:12px;
  font-size:14px; font-weight:bold; cursor:pointer;
  background:transparent; color:#aaa;
}
.error-text { color:#fa4a4a; font-size:12px; margin-bottom:8px; text-align:center; }
.toast {
  position:fixed; bottom:24px; left:50%; transform:translateX(-50%);
  background:#333; color:white; padding:10px 20px; border-radius:20px;
  font-size:13px; z-index:200; opacity:0; transition:opacity 0.3s;
  pointer-events:none;
}
.toast.show { opacity:1; }
.loading { text-align:center; padding:40px 0; color:#888; }
.select-field {
  width:100%; background:#0f0f1a; border:1px solid #1e3060;
  border-radius:10px; padding:12px; color:white; font-size:14px;
  margin-bottom:10px; outline:none;
}
</style>
</head>
<body>

<div class="header">
  <div class="avatar" id="avatar">?</div>
  <div class="user-info">
    <div class="user-name" id="user-name">Memuat...</div>
    <div class="user-id" id="user-id">ID: -</div>
  </div>
</div>

<div class="saldo-card">
  <div class="saldo-label">💰 Saldo Kamu</div>
  <div class="saldo-amount" id="saldo-amount">-</div>
  <div class="saldo-sub">koin virtual</div>
</div>

<div class="dw-row">
  <button class="btn-dw btn-deposit" onclick="showDeposit()">⬇️ Deposit</button>
  <button class="btn-dw btn-withdraw" onclick="showWithdraw()">⬆️ Withdraw</button>
</div>

<div class="section-title">🎮 Permainan</div>
<button class="btn-primary" onclick="showBuatRoom()">🏠 Buat Room (Jadi Bandar)</button>
<button class="btn-secondary" onclick="muatDaftarRoom()">🔍 Lihat & Join Room</button>

<div class="section-title" id="label-rooms" style="margin-top:16px; display:none;">📋 Room Tersedia</div>
<div class="room-list" id="room-list"></div>

<!-- MODAL BUAT ROOM -->
<div class="modal-overlay" id="modal-buat">
  <div class="modal-box">
    <div class="modal-title">🏠 Buat Room Baru</div>
    <div class="input-label">Nama Room</div>
    <input class="input-field" id="br-nama" placeholder="Nama room..." maxlength="30">
    <div class="input-row">
      <div>
        <div class="input-label">Min Taruhan</div>
        <input class="input-field" id="br-min" type="number" placeholder="1000">
      </div>
      <div>
        <div class="input-label">Max Taruhan</div>
        <input class="input-field" id="br-max" type="number" placeholder="10000">
      </div>
    </div>
    <div class="input-row">
      <div>
        <div class="input-label">Max Pemain (4-8)</div>
        <input class="input-field" id="br-maxp" type="number" placeholder="6" min="4" max="8">
      </div>
      <div>
        <div class="input-label">Mode Ganda</div>
        <select class="select-field" id="br-ganda">
          <option value="off">OFF (×2.5)</option>
          <option value="on">ON (×4)</option>
        </select>
      </div>
    </div>
    <div class="input-label">Deskripsi (5-48 karakter)</div>
    <input class="input-field" id="br-desk" placeholder="Deskripsi room..." maxlength="48">
    <div class="error-text" id="br-error"></div>
    <div class="modal-actions">
      <button class="btn-cancel" onclick="tutupModal('modal-buat')">Batal</button>
      <button class="btn-confirm" id="br-submit" onclick="submitBuatRoom()">Buat Room</button>
    </div>
  </div>
</div>

<!-- MODAL JOIN ROOM -->
<div class="modal-overlay" id="modal-join">
  <div class="modal-box">
    <div class="modal-title">🎮 Join Room</div>
    <div id="join-room-info" style="font-size:13px; color:#aaa; margin-bottom:12px;"></div>
    <div class="input-label">Nama Panggilan (maks 20 karakter)</div>
    <input class="input-field" id="join-nama" placeholder="Nama kamu..." maxlength="20">
    <div class="error-text" id="join-error"></div>
    <div class="modal-actions">
      <button class="btn-cancel" onclick="tutupModal('modal-join')">Batal</button>
      <button class="btn-confirm" id="join-submit" onclick="submitJoin()">Bergabung</button>
    </div>
  </div>
</div>

<!-- MODAL INFO -->
<div class="modal-overlay" id="modal-info">
  <div class="modal-box" style="text-align:center;">
    <div class="modal-title" id="info-title">-</div>
    <div style="font-size:13px; color:#aaa; margin-bottom:16px;" id="info-desc">-</div>
    <button class="btn-confirm" style="width:100%;" onclick="tutupModal('modal-info')">OK</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
const tg    = window.Telegram.WebApp;
const API   = 'http://localhost:8081';  // Ganti dengan URL ngrok API saat deploy
tg.expand();

let userData  = null;
let joinRoomId = null;

// ==================== AUTH HEADER ====================
function getHeaders() {
  return {
    'Content-Type': 'application/json',
    'X-Init-Data' : tg.initData || '',
    // Mode dev: pakai X-Dev-UID kalau initData kosong
    'X-Dev-UID'   : (!tg.initData && tg.initDataUnsafe?.user?.id)
                    ? String(tg.initDataUnsafe.user.id) : ''
  };
}

// ==================== INIT ====================
async function init() {
  const user = tg.initDataUnsafe?.user;
  if (user) {
    const nama = user.first_name + (user.last_name ? ' ' + user.last_name : '');
    document.getElementById('user-name').textContent = nama;
    document.getElementById('user-id').textContent   = 'ID: ' + user.id;
    document.getElementById('avatar').textContent    = nama.charAt(0).toUpperCase();
  }

  try {
    const res  = await fetch(`${API}/api/user`, { headers: getHeaders() });
    const data = await res.json();
    if (data.error) { showToast('⚠️ ' + data.error); return; }
    userData = data;
    document.getElementById('saldo-amount').textContent =
      data.saldo.toLocaleString('id-ID');

    // Kalau user masih di room, langsung redirect ke game
    if (data.active_room) {
      window.location.href = 'game.html';
    }
  } catch(e) {
    document.getElementById('saldo-amount').textContent = '?';
    showToast('⚠️ Gagal konek ke server');
  }
}

// ==================== DAFTAR ROOM ====================
async function muatDaftarRoom() {
  const list  = document.getElementById('room-list');
  const label = document.getElementById('label-rooms');
  list.innerHTML  = '<div class="loading">Memuat...</div>';
  label.style.display = 'block';

  try {
    const res   = await fetch(`${API}/api/rooms`, { headers: getHeaders() });
    const data  = await res.json();
    const rooms = data.rooms || [];

    if (rooms.length === 0) {
      list.innerHTML = '<div class="empty-state">😔 Belum ada room tersedia</div>';
      return;
    }

    list.innerHTML = '';
    rooms.forEach(r => {
      const badge  = r.status === 'waiting'
        ? '<span class="badge badge-waiting">⏳ Waiting</span>'
        : '<span class="badge badge-playing">🎲 Playing</span>';
      const div    = document.createElement('div');
      div.className = 'room-card';
      div.innerHTML = `
        <div class="room-card-header">
          <div class="room-card-name">${esc(r.nama_room)}</div>
          ${badge}
        </div>
        <div class="room-card-info">
          💰 ${r.min_taruhan.toLocaleString()} – ${r.max_taruhan.toLocaleString()} &nbsp;|&nbsp;
          👥 ${r.jumlah_pemain}/${r.max_pemain} &nbsp;|&nbsp;
          🎯 Ganda: ${r.ganda.toUpperCase()}
        </div>
        <div class="room-card-info" style="margin-top:4px; color:#666;">${esc(r.deskripsi)}</div>
      `;
      div.onclick = () => showJoin(r);
      list.appendChild(div);
    });
  } catch(e) {
    list.innerHTML = '<div class="empty-state">⚠️ Gagal memuat room</div>';
  }
}

// ==================== BUAT ROOM ====================
function showBuatRoom() {
  document.getElementById('br-error').textContent = '';
  document.getElementById('modal-buat').classList.add('aktif');
}

async function submitBuatRoom() {
  const btn = document.getElementById('br-submit');
  if (btn.disabled) return;

  const nama  = document.getElementById('br-nama').value.trim();
  const min   = parseInt(document.getElementById('br-min').value) || 0;
  const max   = parseInt(document.getElementById('br-max').value) || 0;
  const maxp  = parseInt(document.getElementById('br-maxp').value) || 0;
  const ganda = document.getElementById('br-ganda').value;
  const desk  = document.getElementById('br-desk').value.trim();

  document.getElementById('br-error').textContent = '';
  btn.disabled    = true;
  btn.textContent = 'Memproses...';

  try {
    const res  = await fetch(`${API}/api/room/buat`, {
      method : 'POST',
      headers: getHeaders(),
      body   : JSON.stringify({ nama_room: nama, min_taruhan: min, max_taruhan: max,
                                 max_pemain: maxp, ganda, deskripsi: desk })
    });
    const data = await res.json();
    if (data.error) {
      document.getElementById('br-error').textContent = data.error;
      return;
    }
    tutupModal('modal-buat');
    window.location.href = 'game.html';
  } catch(e) {
    document.getElementById('br-error').textContent = 'Gagal konek ke server';
  } finally {
    btn.disabled    = false;
    btn.textContent = 'Buat Room';
  }
}

// ==================== JOIN ROOM ====================
function showJoin(room) {
  joinRoomId = room.room_id;
  document.getElementById('join-room-info').innerHTML =
    `<b>${esc(room.nama_room)}</b><br>` +
    `Min taruhan: ${room.min_taruhan.toLocaleString()}<br>` +
    `Pemain: ${room.jumlah_pemain}/${room.max_pemain}`;
  document.getElementById('join-error').textContent = '';
  document.getElementById('join-nama').value = '';
  document.getElementById('modal-join').classList.add('aktif');
}

async function submitJoin() {
  const btn  = document.getElementById('join-submit');
  if (btn.disabled) return;

  const nama = document.getElementById('join-nama').value.trim();
  if (!nama) {
    document.getElementById('join-error').textContent = 'Masukkan nama dulu';
    return;
  }

  document.getElementById('join-error').textContent = '';
  btn.disabled    = true;
  btn.textContent = 'Bergabung...';

  try {
    const res  = await fetch(`${API}/api/room/join`, {
      method : 'POST',
      headers: getHeaders(),
      body   : JSON.stringify({ room_id: joinRoomId, nama })
    });
    const data = await res.json();
    if (data.error) {
      document.getElementById('join-error').textContent = data.error;
      return;
    }
    tutupModal('modal-join');
    window.location.href = 'game.html';
  } catch(e) {
    document.getElementById('join-error').textContent = 'Gagal konek ke server';
  } finally {
    btn.disabled    = false;
    btn.textContent = 'Bergabung';
  }
}

// ==================== DEPOSIT / WITHDRAW ====================
function showDeposit() {
  document.getElementById('info-title').textContent = '⬇️ Deposit';
  document.getElementById('info-desc').textContent  =
    'Fitur deposit dalam pengembangan.\nHubungi admin untuk tambah saldo.';
  document.getElementById('modal-info').classList.add('aktif');
}

function showWithdraw() {
  document.getElementById('info-title').textContent = '⬆️ Withdraw';
  document.getElementById('info-desc').textContent  =
    'Fitur withdraw dalam pengembangan.';
  document.getElementById('modal-info').classList.add('aktif');
}

// ==================== UTILS ====================
function tutupModal(id) {
  document.getElementById(id).classList.remove('aktif');
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}

function esc(str) {
  return String(str || '').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

init();
</script>
</body>
</html>
