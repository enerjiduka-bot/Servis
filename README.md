[servis-takip.html](https://github.com/user-attachments/files/25931455/servis-takip.html)
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Servis Takip</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=IBM+Plex+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<script type="module" id="firebase-init">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getFirestore, doc, setDoc, getDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "AIzaSyBstCDQjavpU1s-w7y_tQclir7elmIp_04",
  authDomain: "duka-finance.firebaseapp.com",
  projectId: "duka-finance",
  storageBucket: "duka-finance.firebasestorage.app",
  messagingSenderId: "1090361325722",
  appId: "1:1090361325722:web:867e7e820f9f465b578723"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
window._db = db;
window._firestoreFns = { doc, setDoc, getDoc, onSnapshot };
window._firebaseReady = true;
console.log("Firebase hazir!");
</script>
<style>
  :root {
    --bg: #0f0f0f;
    --surface: #1a1a1a;
    --surface2: #242424;
    --border: #2e2e2e;
    --accent: #f59e0b;
    --accent2: #ef4444;
    --green: #22c55e;
    --text: #f0f0f0;
    --muted: #888;
    --radius: 10px;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: var(--bg); color: var(--text); font-family: 'IBM Plex Sans', sans-serif; min-height: 100vh; }

  /* NAV */
  .nav { background: var(--surface); border-bottom: 2px solid var(--accent); padding: 0; display: flex; position: sticky; top: 0; z-index: 100; overflow-x: auto; }
  .nav button { flex: 1; min-width: 60px; padding: 14px 8px 10px; background: none; border: none; color: var(--muted); font-family: 'Bebas Neue', sans-serif; font-size: 15px; letter-spacing: 1px; cursor: pointer; border-bottom: 3px solid transparent; transition: all .2s; white-space: nowrap; }
  .nav button.active { color: var(--accent); border-bottom-color: var(--accent); }
  .sub-btn { flex: 1; padding: 10px 8px; background: none; border: none; color: var(--muted); font-family: 'Bebas Neue', sans-serif; font-size: 14px; letter-spacing: 1px; cursor: pointer; border-bottom: 3px solid transparent; transition: all .2s; white-space: nowrap; }
  .sub-btn.active { color: var(--accent); border-bottom-color: var(--accent); }

  /* PAGES */
  .page { display: none; padding: 16px; max-width: 600px; margin: 0 auto; }
  .page.active { display: block; }

  /* CARDS */
  .card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px; margin-bottom: 12px; }
  .card-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
  h2 { font-family: 'Bebas Neue'; font-size: 22px; letter-spacing: 1px; color: var(--accent); }
  h3 { font-size: 14px; font-weight: 600; color: var(--text); }

  /* FORM */
  .form-group { margin-bottom: 12px; }
  label { display: block; font-size: 11px; color: var(--muted); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px; }
  input, select, textarea { width: 100%; background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; padding: 10px 12px; color: var(--text); font-family: 'IBM Plex Sans', sans-serif; font-size: 14px; outline: none; transition: border .2s; }
  input:focus, select:focus, textarea:focus { border-color: var(--accent); }
  textarea { resize: vertical; min-height: 70px; }
  select option { background: var(--surface2); }

  /* BUTTONS */
  .btn { display: inline-flex; align-items: center; gap: 6px; padding: 10px 16px; border-radius: 6px; border: none; font-family: 'IBM Plex Sans', sans-serif; font-size: 14px; font-weight: 600; cursor: pointer; transition: all .2s; }
  .btn-primary { background: var(--accent); color: #000; width: 100%; justify-content: center; padding: 12px; }
  .btn-primary:hover { background: #f59e0b; opacity: .9; }
  .btn-sm { padding: 6px 10px; font-size: 12px; }
  .btn-danger { background: var(--accent2); color: #fff; }
  .btn-success { background: var(--green); color: #000; }
  .btn-ghost { background: var(--surface2); color: var(--text); border: 1px solid var(--border); }
  .btn-whatsapp { background: #25D366; color: #fff; }

  /* BADGES */
  .badge { display: inline-block; padding: 2px 8px; border-radius: 20px; font-size: 11px; font-weight: 600; }
  .badge-bekliyor { background: #f59e0b22; color: var(--accent); border: 1px solid #f59e0b44; }
  .badge-tamirde { background: #3b82f622; color: #60a5fa; border: 1px solid #3b82f644; }
  .badge-hazir { background: #22c55e22; color: var(--green); border: 1px solid #22c55e44; }
  .badge-teslim { background: #88888822; color: var(--muted); border: 1px solid #88888844; }
  .badge-borc { background: #ef444422; color: var(--accent2); border: 1px solid #ef444444; }
  .badge-alacak { background: #22c55e22; color: var(--green); border: 1px solid #22c55e44; }

  /* LIST ITEMS */
  .list-item { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px; margin-bottom: 10px; cursor: pointer; transition: border-color .2s; }
  .list-item:hover { border-color: var(--accent); }
  .list-item-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 6px; }
  .list-item-title { font-weight: 600; font-size: 15px; }
  .list-item-sub { font-size: 12px; color: var(--muted); margin-top: 2px; }
  .list-item-actions { display: flex; gap: 6px; margin-top: 10px; flex-wrap: wrap; }

  /* STATS */
  .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 16px; }
  .stat-card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px; text-align: center; }
  .stat-value { font-family: 'Bebas Neue'; font-size: 28px; color: var(--accent); }
  .stat-label { font-size: 11px; color: var(--muted); text-transform: uppercase; letter-spacing: 1px; margin-top: 2px; }

  /* MODAL */
  .modal-overlay { display: none; position: fixed; inset: 0; background: #000000cc; z-index: 200; padding: 16px; overflow-y: auto; }
  .modal-overlay.active { display: flex; align-items: flex-start; justify-content: center; padding-top: 40px; }
  .modal { background: var(--surface); border: 1px solid var(--border); border-radius: 14px; padding: 20px; width: 100%; max-width: 500px; }
  .modal-title { font-family: 'Bebas Neue'; font-size: 20px; color: var(--accent); margin-bottom: 16px; display: flex; justify-content: space-between; align-items: center; }
  .close-btn { background: none; border: none; color: var(--muted); font-size: 22px; cursor: pointer; line-height: 1; }

  /* SEARCH */
  .search-bar { position: relative; margin-bottom: 14px; }
  .search-bar input { padding-left: 36px; }
  .search-icon { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); color: var(--muted); font-size: 14px; }

  /* DIVIDER */
  .divider { border: none; border-top: 1px solid var(--border); margin: 14px 0; }

  /* EMPTY STATE */
  .empty { text-align: center; padding: 40px 20px; color: var(--muted); }
  .empty-icon { font-size: 40px; margin-bottom: 10px; }

  /* FILTER ROW */
  .filter-row { display: flex; gap: 6px; overflow-x: auto; margin-bottom: 14px; padding-bottom: 4px; }
  .filter-btn { flex-shrink: 0; padding: 6px 12px; border-radius: 20px; border: 1px solid var(--border); background: var(--surface2); color: var(--muted); font-size: 12px; cursor: pointer; transition: all .2s; }
  .filter-btn.active { background: var(--accent); color: #000; border-color: var(--accent); font-weight: 600; }

  .row { display: flex; gap: 10px; }
  .row .form-group { flex: 1; }

  /* BOTTOM SPACING */
  .pb { padding-bottom: 30px; }

  /* PROFIT INDICATOR */
  .profit-positive { color: var(--green); }
  .profit-negative { color: var(--accent2); }
</style>
</head>
<body>

<!-- NAV -->
<nav class="nav" id="main-nav">
  <button class="active" onclick="showPage('dashboard')">📊 Özet</button>
  <button onclick="showPage('servisler')">🔧 Servis</button>
  <button onclick="showPage('stok')">📦 Stok</button>
  <button onclick="showPage('musteriler')">👥 Müşteri</button>
  <button onclick="toggleFinans()" id="finans-btn">💼 Finans</button>
  <button onclick="showPage('grafik')">📈 Grafik</button>
  <button onclick="showPage('ayarlar')">⚙️ Ayarlar</button>
</nav>
<!-- FİNANS ALT MENÜ -->
<div id="finans-submenu" style="display:none;background:var(--surface2);border-bottom:2px solid var(--accent);padding:0;overflow-x:auto">
  <div style="display:flex;max-width:600px;margin:0 auto">
    <button onclick="showPage('cari')" class="sub-btn" id="sub-cari">💰 Cari</button>
    <button onclick="showPage('satis')" class="sub-btn" id="sub-satis">🛒 Satış</button>
    <button onclick="showPage('gider')" class="sub-btn" id="sub-gider">📉 Gider</button>
    <button onclick="showPage('kasa')" class="sub-btn" id="sub-kasa">🏦 Kasa</button>
  </div>
</div>



<!-- GİDER SAYFASI -->
<div id="page-gider" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>📉 Giderler</h2>
    <button class="btn btn-primary btn-sm" onclick="openModal('gider-modal')">+ Gider Ekle</button>
  </div>
  <div class="stats-grid" id="gider-stats"></div>
  <div class="filter-row" id="gider-filters">
    <button class="filter-btn active" onclick="filterGider('hepsi')">Hepsi</button>
    <button class="filter-btn" onclick="filterGider('kira')">🏠 Kira</button>
    <button class="filter-btn" onclick="filterGider('fatura')">💡 Fatura</button>
    <button class="filter-btn" onclick="filterGider('personel')">👤 Personel</button>
    <button class="filter-btn" onclick="filterGider('malzeme')">🔩 Malzeme</button>
    <button class="filter-btn" onclick="filterGider('diger')">📌 Diğer</button>
  </div>
  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="Gider ara..." oninput="renderGider()" id="gider-search">
  </div>
  <div id="gider-list"></div>
</div>

<!-- GİDER MODAL -->
<div class="modal-overlay" id="gider-modal">
  <div class="modal">
    <div class="modal-title">GİDER EKLE <button class="close-btn" onclick="closeModal('gider-modal')">✕</button></div>
    <div class="form-group">
      <label>Açıklama</label>
      <input type="text" id="g-aciklama" placeholder="Kira, elektrik faturası, usta ücreti...">
    </div>
    <div class="row">
      <div class="form-group">
        <label>Tutar (₺)</label>
        <input type="number" id="g-tutar" placeholder="0">
      </div>
      <div class="form-group">
        <label>Ödeme Yöntemi</label>
        <input type="text" id="g-odeme" placeholder="Nakit, Kredi, Havale...">
      </div>
    </div>
    <div class="form-group">
      <label>Kategori (otomatik tespit edilir, değiştirebilirsiniz)</label>
      <select id="g-kategori">
        <option value="kira">🏠 Kira</option>
        <option value="fatura">💡 Fatura</option>
        <option value="personel">👤 Personel</option>
        <option value="malzeme">🔩 Malzeme</option>
        <option value="diger">📌 Diğer</option>
      </select>
    </div>
    <button class="btn btn-primary" onclick="saveGider()">💾 Kaydet</button>
  </div>
</div>

<!-- KASA SAYFASI -->
<div id="page-kasa" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>🏦 Kasa</h2>
    <button class="btn btn-primary btn-sm" onclick="openModal('kasa-modal')">+ Hareket Ekle</button>
  </div>
  <div id="kasa-bakiye-card" style="margin-bottom:12px"></div>
  <div class="filter-row" id="kasa-filters">
    <button class="filter-btn active" onclick="filterKasa('hepsi')">Hepsi</button>
    <button class="filter-btn" onclick="filterKasa('giris')">⬆️ Giriş</button>
    <button class="filter-btn" onclick="filterKasa('cikis')">⬇️ Çıkış</button>
    <button class="filter-btn" onclick="filterKasa('nakit')">💵 Nakit</button>
    <button class="filter-btn" onclick="filterKasa('kredi')">💳 Kredi</button>
    <button class="filter-btn" onclick="filterKasa('havale')">🏧 Havale</button>
  </div>
  <div id="kasa-gunluk" style="margin-bottom:12px"></div>
  <div id="kasa-list"></div>
</div>

<!-- KASA MODAL -->
<div class="modal-overlay" id="kasa-modal">
  <div class="modal">
    <div class="modal-title">KASA HAREKETİ <button class="close-btn" onclick="closeModal('kasa-modal')">✕</button></div>
    <div class="form-group">
      <label>Tür</label>
      <select id="k-tur">
        <option value="giris">⬆️ Giriş (Tahsilat)</option>
        <option value="cikis">⬇️ Çıkış (Ödeme)</option>
      </select>
    </div>
    <div class="form-group">
      <label>Açıklama</label>
      <input type="text" id="k-aciklama" placeholder="Servis tahsilatı, kira ödemesi...">
    </div>
    <div class="row">
      <div class="form-group">
        <label>Tutar (₺)</label>
        <input type="number" id="k-tutar" placeholder="0">
      </div>
      <div class="form-group">
        <label>Ödeme Yöntemi</label>
        <input type="text" id="k-odeme" placeholder="Nakit, Kredi, Havale...">
      </div>
    </div>
    <div class="form-group">
      <label>Not</label>
      <input type="text" id="k-not" placeholder="İsteğe bağlı...">
    </div>
    <button class="btn btn-primary" onclick="saveKasa()">💾 Kaydet</button>
  </div>
</div>


<!-- AYARLAR SAYFASI -->
<div id="page-ayarlar" class="page pb">
  <div style="padding:16px 0 8px;">
    <div style="font-family:'Bebas Neue';font-size:24px;letter-spacing:2px;color:var(--accent)">⚙️ Ayarlar</div>
  </div>
  <div class="card">
    <div class="card-header"><h2>İşletme Bilgileri</h2></div>
    <div class="form-group">
      <label>İşletme Adı</label>
      <input type="text" id="ay-isletme-ad" placeholder="Servis adınız...">
    </div>
    <div class="form-group">
      <label>İşletme Telefonu (WhatsApp mesajları bu numaradan gider)</label>
      <input type="tel" id="ay-isletme-tel" placeholder="05XX XXX XX XX">
    </div>
    <div class="form-group">
      <label>Adres</label>
      <input type="text" id="ay-adres" placeholder="İşletme adresi...">
    </div>
    <button class="btn btn-primary" onclick="saveAyarlar()">💾 Kaydet</button>
  </div>
  <div class="card" style="margin-top:12px">
    <div class="card-header"><h2>Bildirim</h2></div>
    <div style="display:flex;justify-content:space-between;align-items:center">
      <div>
        <div style="font-size:14px;font-weight:600">Bekleyen servis uyarısı</div>
        <div style="font-size:12px;color:var(--muted)">3+ gün bekleyen servisler için uyarı göster</div>
      </div>
      <label style="position:relative;display:inline-block;width:44px;height:24px">
        <input type="checkbox" id="ay-uyari" style="opacity:0;width:0;height:0" onchange="saveAyarlar()">
        <span id="ay-uyari-span" style="position:absolute;cursor:pointer;inset:0;background:var(--border);border-radius:24px;transition:.3s"></span>
      </label>
    </div>
  </div>
</div>

<!-- GRAFİK SAYFASI -->
<div id="page-grafik" class="page pb">
  <div style="padding:16px 0 8px;">
    <div style="font-family:'Bebas Neue';font-size:24px;letter-spacing:2px;color:var(--accent)">📈 Aylık Kar / Zarar</div>
  </div>
  <div class="card" style="margin-bottom:12px">
    <canvas id="grafik-canvas" style="width:100%;max-height:260px"></canvas>
  </div>
  <div id="grafik-tablo"></div>
</div>


<!-- SATIŞ SAYFASI -->
<div id="page-satis" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>🛒 Satış / Alış</h2>
    <div style="display:flex;gap:6px">
      <button class="btn btn-primary btn-sm" onclick="openModal('satis-modal')">+ Satış</button>
      <button class="btn btn-ghost btn-sm" onclick="openModal('alis-modal')">+ Alış</button>
    </div>
  </div>
  <div class="stats-grid" id="satis-stats"></div>
  <div class="filter-row" id="satis-filters">
    <button class="filter-btn active" onclick="filterSatis('hepsi')">Hepsi</button>
    <button class="filter-btn" onclick="filterSatis('satis')">Satışlar</button>
    <button class="filter-btn" onclick="filterSatis('alis')">Alışlar</button>
  </div>
  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="Ürün veya kişi ara..." oninput="renderSatis()" id="satis-search">
  </div>
  <div id="satis-list"></div>
</div>

<!-- SATIŞ MODAL -->
<div class="modal-overlay" id="satis-modal">
  <div class="modal">
    <div class="modal-title">YENİ SATIŞ <button class="close-btn" onclick="closeModal('satis-modal')">✕</button></div>
    <div class="form-group">
      <label>Müşteri Adı</label>
      <input type="text" id="sat-musteri" placeholder="Ad Soyad (isteğe bağlı)" oninput="musteriOneri('sat')">
      <div id="sat-musteri-oneri" style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto"></div>
    </div>
    <div id="sat-kalemler-list"></div>
    <div style="background:var(--surface2);border-radius:8px;padding:12px;margin-bottom:12px;">
      <div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">Ürün Ekle</div>
      <div style="display:flex;gap:6px;margin-bottom:6px">
        <select id="sat-stok-sec" style="flex:1" onchange="satStokSec()">
          <option value="">Stoktan seç...</option>
        </select>
      </div>
      <div style="display:flex;gap:6px">
        <input type="text" id="sat-urun-ad" placeholder="Ürün adı" style="flex:2">
        <input type="number" id="sat-urun-adet" placeholder="Adet" style="width:60px" value="1" min="1">
        <input type="number" id="sat-urun-fiyat" placeholder="₺ Fiyat" style="width:80px">
        <button class="btn btn-ghost btn-sm" onclick="satKalemEkle()" style="white-space:nowrap">+ Ekle</button>
      </div>
    </div>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;padding:10px;background:var(--surface2);border-radius:8px">
      <span style="font-size:13px;color:var(--muted)">Toplam</span>
      <span id="sat-toplam" style="font-family:'Bebas Neue';font-size:22px;color:var(--accent)">₺0</span>
    </div>
    <div class="form-group">
      <label>Not</label>
      <input type="text" id="sat-not" placeholder="İsteğe bağlı not...">
    </div>
    <button class="btn btn-primary" onclick="saveSatis()">💾 Kaydet</button>
  </div>
</div>

<!-- ALIŞ MODAL -->
<div class="modal-overlay" id="alis-modal">
  <div class="modal">
    <div class="modal-title">YENİ ALIŞ <button class="close-btn" onclick="closeModal('alis-modal')">✕</button></div>
    <div class="form-group">
      <label>Tedarikçi</label>
      <input type="text" id="al-tedarikci" placeholder="Firma / kişi adı">
    </div>
    <div id="al-kalemler-list"></div>
    <div style="background:var(--surface2);border-radius:8px;padding:12px;margin-bottom:12px;">
      <div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">Ürün Ekle</div>
      <div style="display:flex;gap:6px">
        <input type="text" id="al-urun-ad" placeholder="Ürün adı" style="flex:2">
        <input type="number" id="al-urun-adet" placeholder="Adet" style="width:60px" value="1" min="1">
        <input type="number" id="al-urun-fiyat" placeholder="₺ Fiyat" style="width:80px">
        <button class="btn btn-ghost btn-sm" onclick="alKalemEkle()" style="white-space:nowrap">+ Ekle</button>
      </div>
    </div>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;padding:10px;background:var(--surface2);border-radius:8px">
      <span style="font-size:13px;color:var(--muted)">Toplam</span>
      <span id="al-toplam" style="font-family:'Bebas Neue';font-size:22px;color:var(--accent2)">₺0</span>
    </div>
    <div class="form-group">
      <label>Not</label>
      <input type="text" id="al-not" placeholder="İsteğe bağlı not...">
    </div>
    <button class="btn btn-primary" onclick="saveAlis()">💾 Kaydet</button>
  </div>
</div>

<!-- DASHBOARD -->
<div id="page-dashboard" class="page active pb">
  <div style="padding: 16px 0 8px;">
    <div style="font-family:'Bebas Neue';font-size:28px;letter-spacing:2px;">🔩 SERVİS TAKİP</div>
    <div style="font-size:12px;color:var(--muted);" id="dashboard-date"></div>
  </div>
  <div id="drive-bar" style="margin-bottom:12px"></div>
  <div id="bekleyen-uyari" style="margin-bottom:12px"></div>
  <div class="stats-grid" id="stats-grid"></div>
  <div class="card" style="margin-bottom:12px">
    <div class="card-header"><h2>Bu Ay</h2></div>
    <div id="bu-ay-ozet"></div>
  </div>
  <div class="card">
    <div class="card-header"><h2>Son İşlemler</h2></div>
    <div id="recent-list"></div>
  </div>
</div>

<!-- SERVİSLER -->
<div id="page-servisler" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>🔧 Servisler</h2>
    <button class="btn btn-primary btn-sm" onclick="openModal('servis-modal')">+ Yeni</button>
  </div>
  <div class="filter-row" id="servis-filters">
    <button class="filter-btn active" onclick="filterServis('hepsi')">Hepsi</button>
    <button class="filter-btn" onclick="filterServis('bekliyor')">Bekliyor</button>
    <button class="filter-btn" onclick="filterServis('tamirde')">Tamirde</button>
    <button class="filter-btn" onclick="filterServis('hazir')">Hazır</button>
    <button class="filter-btn" onclick="filterServis('teslim')">Teslim</button>
    <button class="filter-btn" onclick="filterServis('arsiv')">🗃️ Arşiv</button>
  </div>
  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="Müşteri veya alet ara..." oninput="renderServisler()" id="servis-search">
  </div>
  <div id="servis-list"></div>
</div>

<!-- CARİ -->
<div id="page-cari" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>💰 Cari Hesap</h2>
    <button class="btn btn-primary btn-sm" onclick="openModal('cari-modal')">+ Ekle</button>
  </div>
  <div class="stats-grid" id="cari-stats"></div>
  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="İsim veya açıklama ara..." oninput="renderCari()" id="cari-search">
  </div>
  <div class="filter-row">
    <button class="filter-btn active" onclick="filterCari('hepsi')">Hepsi</button>
    <button class="filter-btn" onclick="filterCari('borc')">Borçlular</button>
    <button class="filter-btn" onclick="filterCari('alacak')">Alacaklılar</button>
  </div>
  <div id="cari-list"></div>
</div>

<!-- STOK -->
<div id="page-stok" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>📦 Stok</h2>
    <button class="btn btn-primary btn-sm" onclick="openModal('stok-modal')">+ Ekle</button>
  </div>
  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="Parça ara..." oninput="renderStok()" id="stok-search">
  </div>
  <div id="stok-list"></div>
</div>

<!-- MÜŞTERİLER -->
<div id="page-musteriler" class="page pb">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px;padding-top:8px;">
    <h2>👥 Müşteriler</h2>
    <button class="btn btn-primary btn-sm" onclick="openModal('musteri-modal')">+ Ekle</button>
  </div>
  <div class="search-bar">
    <span class="search-icon">🔍</span>
    <input type="text" placeholder="Müşteri ara..." oninput="renderMusteriler()" id="musteri-search">
  </div>
  <div id="musteri-list"></div>
</div>

<!-- MODALS -->

<!-- SERVİS MODAL -->
<div class="modal-overlay" id="servis-modal">
  <div class="modal">
    <div class="modal-title">YENİ SERVİS <button class="close-btn" onclick="closeModal('servis-modal')">✕</button></div>
    <div class="form-group">
      <label>Müşteri Adı</label>
      <input type="text" id="s-musteri-ad" placeholder="Ad Soyad (zorunlu değil)" oninput="musteriOneri('s')">
      <div id="s-musteri-oneri" style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto"></div>
      <input type="hidden" id="s-musteri-id">
    </div>
    <div class="form-group">
      <label>Alet / Cihaz</label>
      <input type="text" id="s-alet" placeholder="Kaynak makinesi, matkap...">
    </div>
    <div class="form-group">
      <label>Marka / Model</label>
      <input type="text" id="s-marka" placeholder="Bosch, Makita...">
    </div>
    <div class="form-group">
      <label>Arıza Tanımı</label>
      <textarea id="s-ariza" placeholder="Müşterinin belirttiği arıza..."></textarea>
    </div>
    <div class="row">
      <div class="form-group">
        <label>Tamir Ücreti (₺)</label>
        <input type="number" id="s-ucret" placeholder="0">
      </div>
      <div class="form-group">
        <label>Parça Maliyeti (₺)</label>
        <input type="number" id="s-maliyet" placeholder="0">
      </div>
    </div>
    <div class="form-group">
      <label>Durum</label>
      <select id="s-durum">
        <option value="bekliyor">Bekliyor</option>
        <option value="tamirde">Tamirde</option>
        <option value="hazir">Hazır</option>
        <option value="teslim">Teslim Edildi</option>
      </select>
    </div>
    <div class="form-group">
      <label>Not</label>
      <textarea id="s-not" placeholder="İç not..."></textarea>
    </div>
    <!-- KULLANILAN PARÇALAR (YENİ SERVİS) -->
    <div style="border-top:1px solid var(--border);margin:14px 0;padding-top:14px;">
      <div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px;">📦 Kullanılan Parçalar (Stoktan Düş)</div>
      <div id="s-parcalar-list"></div>
      <div style="margin-top:8px;">
        <input type="text" id="s-parca-ara" placeholder="Parça ara..." style="width:100%;box-sizing:border-box;margin-bottom:6px" oninput="parcaAra('s')" autocomplete="off">
        <div id="s-parca-oneri" style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;max-height:150px;overflow-y:auto;margin-bottom:6px"></div>
        <input type="hidden" id="s-parca-sec">
        <div style="display:flex;gap:8px">
          <input type="number" id="s-parca-adet" placeholder="Adet" style="width:70px" min="1" value="1">
          <button class="btn btn-ghost btn-sm" onclick="parcaEkle('s')" style="white-space:nowrap">+ Ekle</button>
        </div>
      </div>
    </div>
    <button class="btn btn-primary" onclick="saveServis()">💾 Kaydet</button>
  </div>
</div>

<!-- SERVİS DÜZENLEME MODAL -->
<div class="modal-overlay" id="servis-edit-modal">
  <div class="modal">
    <div class="modal-title">SERVİS DÜZENLE <button class="close-btn" onclick="closeModal('servis-edit-modal')">✕</button></div>
    <div class="form-group">
      <label>Durum</label>
      <select id="se-durum">
        <option value="bekliyor">Bekliyor</option>
        <option value="tamirde">Tamirde</option>
        <option value="hazir">Hazır</option>
        <option value="teslim">Teslim Edildi</option>
      </select>
    </div>
    <div class="form-group">
      <label>Alet / Cihaz</label>
      <input type="text" id="se-alet">
    </div>
    <div class="form-group">
      <label>Arıza Tanımı</label>
      <textarea id="se-ariza"></textarea>
    </div>
    <div class="row">
      <div class="form-group">
        <label>Tamir Ücreti (₺)</label>
        <input type="number" id="se-ucret">
      </div>
      <div class="form-group">
        <label>Parça Maliyeti (₺)</label>
        <input type="number" id="se-maliyet" readonly style="background:var(--surface);color:var(--muted)">
      </div>
    </div>
    <!-- KULLANILAN PARÇALAR (DÜZENLEME) -->
    <div style="border-top:1px solid var(--border);margin:14px 0;padding-top:14px;">
      <div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px;">📦 Kullanılan Parçalar (Stoktan Düş)</div>
      <div id="se-parcalar-list"></div>
      <div style="margin-top:8px;">
        <input type="text" id="se-parca-ara" placeholder="Parça ara..." style="width:100%;box-sizing:border-box;margin-bottom:6px" oninput="parcaAra('se')" autocomplete="off">
        <div id="se-parca-oneri" style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;max-height:150px;overflow-y:auto;margin-bottom:6px"></div>
        <input type="hidden" id="se-parca-sec">
        <div style="display:flex;gap:8px">
          <input type="number" id="se-parca-adet" placeholder="Adet" style="width:70px" min="1" value="1">
          <button class="btn btn-ghost btn-sm" onclick="parcaEkle('se')" style="white-space:nowrap">+ Ekle</button>
        </div>
      </div>
    </div>
    <div class="form-group">
      <label>Not</label>
      <textarea id="se-not"></textarea>
    </div>
    <input type="hidden" id="se-id">
    <button class="btn btn-primary" onclick="updateServis()">💾 Güncelle</button>
  </div>
</div>

<!-- CARİ MODAL -->
<div class="modal-overlay" id="cari-modal">
  <div class="modal">
    <div class="modal-title">CARİ HAREKET <button class="close-btn" onclick="closeModal('cari-modal')">✕</button></div>
    <div class="form-group">
      <label>Müşteri / Tedarikçi</label>
      <input type="text" id="c-isim" placeholder="Ad Soyad veya Firma" oninput="musteriOneri('c')">
      <div id="c-musteri-oneri" style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto"></div>
    </div>
    <div class="form-group">
      <label>Tür</label>
      <select id="c-tur">
        <option value="alacak">Alacak (bize borçlu)</option>
        <option value="borc">Borç (biz borçluyuz)</option>
      </select>
    </div>
    <div class="form-group">
      <label>Tutar (₺)</label>
      <input type="number" id="c-tutar" placeholder="0">
    </div>
    <div class="form-group">
      <label>Açıklama</label>
      <input type="text" id="c-aciklama" placeholder="Tamir ücreti, parça alımı...">
    </div>
    <button class="btn btn-primary" onclick="saveCari()">💾 Kaydet</button>
  </div>
</div>

<!-- STOK MODAL -->
<div class="modal-overlay" id="stok-modal">
  <div class="modal">
    <div class="modal-title">STOK EKLE <button class="close-btn" onclick="closeModal('stok-modal')">✕</button></div>
    <div class="form-group">
      <label>Parça / Malzeme Adı</label>
      <input type="text" id="st-ad" placeholder="Karbon fırça, rulman, kablo...">
    </div>
    <div class="row">
      <div class="form-group">
        <label>Adet</label>
        <input type="number" id="st-adet" placeholder="0">
      </div>
      <div class="form-group">
        <label>Birim Maliyet (₺)</label>
        <input type="number" id="st-maliyet" placeholder="0">
      </div>
    </div>
    <div class="form-group">
      <label>Min. Stok Uyarısı</label>
      <input type="number" id="st-min" placeholder="5">
    </div>
    <button class="btn btn-primary" onclick="saveStok()">💾 Kaydet</button>
  </div>
</div>

<!-- MÜŞTERİ MODAL -->
<div class="modal-overlay" id="musteri-modal">
  <div class="modal">
    <div class="modal-title">MÜŞTERİ EKLE <button class="close-btn" onclick="closeModal('musteri-modal')">✕</button></div>
    <div class="form-group">
      <label>Ad Soyad</label>
      <input type="text" id="m-ad" placeholder="Ad Soyad">
    </div>
    <div class="form-group">
      <label>Telefon</label>
      <input type="tel" id="m-tel" placeholder="05XX XXX XX XX">
    </div>
    <div class="form-group">
      <label>Not</label>
      <input type="text" id="m-not" placeholder="Adres, ek bilgi...">
    </div>
    <button class="btn btn-primary" onclick="saveMusteri()">💾 Kaydet</button>
  </div>
</div>

<script>
// --- STATE ---
let state = {
  servisler: [],
  cari: [],
  stok: [],
  musteriler: [],
  satislar: [],
  giderler: [],
  kasa: [],
  ayarlar: { isletmeAd: '', isletmeTel: '', adres: '', uyariAktif: true },
  servisFilter: 'hepsi',
  cariFilter: 'hepsi'
};

function saveState() {
  try { localStorage.setItem('servis_app', JSON.stringify(state)); } catch(e) {}
  // Firebase'e kaydet (debounce 2 saniye)
  clearTimeout(window._fbSaveTimer);
  window._fbSaveTimer = setTimeout(function() { firebaseSave(); }, 2000);
}

async function firebaseSave() {
  if (!window._firebaseReady) return;
  try {
    const { doc, setDoc } = window._firestoreFns;
    await setDoc(doc(window._db, 'servis', 'veri'), state);
    console.log('Firebase kaydedildi:', new Date().toLocaleTimeString());
  } catch(e) {
    console.error('Firebase kayit hatasi:', e);
  }
}

async function firebaseLoad() {
  if (!window._firebaseReady) return false;
  try {
    const { doc, getDoc } = window._firestoreFns;
    const snap = await getDoc(doc(window._db, 'servis', 'veri'));
    if (snap.exists()) {
      state = snap.data();
      try { localStorage.setItem('servis_app', JSON.stringify(state)); } catch(e) {}
      return true;
    } else {
      // Firebase bos - localStorage verisini aktar
      console.log('Firebase bos, localStorage aktariliyor...');
      setTimeout(function() { firebaseSave(); }, 1000);
      return false;
    }
  } catch(e) {
    console.error('Firebase yukle hatasi:', e);
  }
  return false;
}

function firebaseGercekZamanli() {
  if (!window._firebaseReady) return;
  const { doc, onSnapshot } = window._firestoreFns;
  var ilkYukleme = true;
  onSnapshot(doc(window._db, 'servis', 'veri'), function(snap) {
    if (ilkYukleme) { ilkYukleme = false; return; }
    if (snap.exists()) {
      const yeniVeri = snap.data();
      if (JSON.stringify(yeniVeri) !== JSON.stringify(state)) {
        state = yeniVeri;
        try { localStorage.setItem('servis_app', JSON.stringify(state)); } catch(e) {}
        renderDashboard();
        console.log('Firebase guncellendi:', new Date().toLocaleTimeString());
      }
    }
  });
}
function loadState() {
  try {
    const d = localStorage.getItem('servis_app');
    if (d) state = JSON.parse(d);
  } catch(e) {}
}

// --- NAVIGATION ---
const finansPages = ['cari','satis','gider','kasa'];

function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav button').forEach(b => b.classList.remove('active'));
  document.querySelectorAll('.sub-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');

  if (finansPages.includes(id)) {
    // Finans alt sayfası
    document.getElementById('finans-submenu').style.display = 'block';
    document.getElementById('finans-btn').classList.add('active');
    const subBtn = document.getElementById('sub-' + id);
    if (subBtn) subBtn.classList.add('active');
  } else {
    document.getElementById('finans-submenu').style.display = 'none';
    const mainPages = ['dashboard','servisler','stok','musteriler','grafik','ayarlar'];
    const mainBtns = document.querySelectorAll('#main-nav button');
    const idx = mainPages.indexOf(id);
    if (idx >= 0 && mainBtns[idx]) mainBtns[idx].classList.add('active');
  }

  if (id === 'dashboard') renderDashboard();
  if (id === 'servisler') renderServisler();
  if (id === 'cari') renderCari();
  if (id === 'stok') renderStok();
  if (id === 'musteriler') renderMusteriler();
  if (id === 'satis') renderSatis();
  if (id === 'gider') renderGider();
  if (id === 'kasa') renderKasa();
  if (id === 'grafik') renderGrafik();
  if (id === 'ayarlar') renderAyarlar();
}

function toggleFinans() {
  const submenu = document.getElementById('finans-submenu');
  if (submenu.style.display === 'none') {
    submenu.style.display = 'block';
    document.getElementById('finans-btn').classList.add('active');
    // Varsayılan olarak Cari'yi aç
    if (!finansPages.some(p => document.getElementById('page-'+p).classList.contains('active'))) {
      showPage('cari');
    }
  } else {
    submenu.style.display = 'none';
    document.getElementById('finans-btn').classList.remove('active');
  }
}

// Geçici parça listesi (modal açıkken)
let tempParcalar = { s: [], se: [] };

function openModal(id) {
  if (id === 'satis-modal') { openSatisModal(); return; }
  if (id === 'alis-modal') { openAlisModal(); return; }
  if (id === 'servis-modal') {
    tempParcalar.s = [];
    populateParcaSelect('s-parca-sec');
    renderTempParcalar('s');
  }
  document.getElementById(id).classList.add('active');
}

function populateParcaSelect(elId) { /* artık kullanılmıyor */ }

function parcaAra(prefix) {
  const q = document.getElementById(prefix + '-parca-ara').value.toLowerCase();
  const oneriEl = document.getElementById(prefix + '-parca-oneri');
  if (!q || q.length < 1) { oneriEl.style.display = 'none'; return; }
  const eslesen = state.stok.filter(function(s) { return s.adet > 0 && s.ad.toLowerCase().includes(q); }).slice(0, 8);
  if (eslesen.length === 0) { oneriEl.style.display = 'none'; return; }
  oneriEl.style.display = 'block';
  oneriEl.innerHTML = eslesen.map(function(s) {
    return '<div onclick="parcaSec(' + JSON.stringify(prefix) + ',' + s.id + ')" style="padding:10px 12px;cursor:pointer;font-size:13px;border-bottom:1px solid var(--border)">' +
      s.ad + ' <span style="color:var(--muted);font-size:11px">(Stok: ' + s.adet + ') - ' + s.maliyet + ' TL</span>' +
    '</div>';
  }).join('');
}

function parcaSec(prefix, stokId) {
  const s = state.stok.find(function(x) { return x.id === stokId; });
  if (!s) return;
  document.getElementById(prefix + '-parca-ara').value = s.ad;
  document.getElementById(prefix + '-parca-sec').value = stokId;
  document.getElementById(prefix + '-parca-oneri').style.display = 'none';
}

function parcaEkle(prefix) {
  const secEl = document.getElementById(prefix + '-parca-sec');
  const adetEl = document.getElementById(prefix + '-parca-adet');
  const stokId = parseInt(secEl.value);
  const adet = parseInt(adetEl.value) || 1;
  if (!stokId) { alert('Parça seçiniz'); return; }
  const stok = state.stok.find(s => s.id === stokId);
  if (!stok) return;
  if (adet > stok.adet) { alert('Stokta sadece ' + stok.adet + ' adet var!'); return; }
  const mevcut = tempParcalar[prefix].find(p => p.stokId === stokId);
  if (mevcut) {
    if (mevcut.adet + adet > stok.adet) { alert('Toplam ' + stok.adet + ' adetten fazla ekleyemezsiniz!'); return; }
    mevcut.adet += adet;
  } else {
    tempParcalar[prefix].push({ stokId, ad: stok.ad, adet, birimMaliyet: stok.maliyet });
  }
  adetEl.value = 1;
  document.getElementById(prefix + '-parca-ara').value = '';
  document.getElementById(prefix + '-parca-sec').value = '';
  renderTempParcalar(prefix);
  if (prefix === 'se') {
    const toplamMaliyet = tempParcalar.se.reduce((a, p) => a + p.adet * p.birimMaliyet, 0);
    document.getElementById('se-maliyet').value = toplamMaliyet.toFixed(0);
  }
}

function parcaSil(prefix, stokId) {
  tempParcalar[prefix] = tempParcalar[prefix].filter(p => p.stokId !== stokId);
  renderTempParcalar(prefix);
  if (prefix === 'se') {
    const toplamMaliyet = tempParcalar.se.reduce((a, p) => a + p.adet * p.birimMaliyet, 0);
    document.getElementById('se-maliyet').value = toplamMaliyet.toFixed(0);
  }
}

function renderTempParcalar(prefix) {
  const el = document.getElementById(prefix + '-parcalar-list');
  if (!el) return;
  if (tempParcalar[prefix].length === 0) {
    el.innerHTML = '<div style="font-size:12px;color:var(--muted);margin-bottom:6px">Henüz parça eklenmedi</div>';
    return;
  }
  el.innerHTML = tempParcalar[prefix].map(p =>
    '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:6px;padding:8px 10px;margin-bottom:6px;">' +
      '<div>' +
        '<div style="font-size:13px;font-weight:600">' + p.ad + '</div>' +
        '<div style="font-size:11px;color:var(--muted)">' + p.adet + ' adet x ₺' + p.birimMaliyet + ' = ₺' + (p.adet*p.birimMaliyet).toFixed(0) + '</div>' +
      '</div>' +
      '<button onclick="parcaSil(\'' + prefix + '\', ' + p.stokId + ')" style="background:none;border:none;color:var(--accent2);font-size:18px;cursor:pointer">✕</button>' +
    '</div>'
  ).join('');
}
function closeModal(id) {
  document.getElementById(id).classList.remove('active');
}

// Close modal on overlay click
document.querySelectorAll('.modal-overlay').forEach(el => {
  el.addEventListener('click', function(e) {
    if (e.target === this) this.classList.remove('active');
  });
});

// --- DASHBOARD ---
function renderDashboard() {
  const now = new Date();
  renderDriveBar();
  document.getElementById('dashboard-date').textContent = now.toLocaleDateString('tr-TR', {weekday:'long', year:'numeric', month:'long', day:'numeric'});

  // --- BEKLEYEN UYARI ---
  const uyariAktif = !state.ayarlar || state.ayarlar.uyariAktif !== false;
  const bekleyenler = uyariAktif ? state.servisler.filter(function(s) {
    if (s.arsiv || s.durum === 'teslim') return false;
    const gun = Math.floor((now - new Date(s.tarih)) / 86400000);
    return gun >= 3;
  }) : [];
  const uyariEl = document.getElementById('bekleyen-uyari');
  if (bekleyenler.length > 0) {
    uyariEl.innerHTML = '<div style="background:#f59e0b22;border:1px solid #f59e0b66;border-radius:10px;padding:12px 14px;cursor:pointer" onclick="showPage(\"servisler\")">' +
      '<div style="font-weight:700;color:var(--accent);margin-bottom:4px">⚠️ ' + bekleyenler.length + ' servis 3+ gündür bekliyor!</div>' +
      '<div style="font-size:12px;color:var(--muted)">' + bekleyenler.map(function(s) {
        const gun = Math.floor((now - new Date(s.tarih)) / 86400000);
        return s.musteri + ' — ' + s.alet + ' (' + gun + ' gün)';
      }).join(', ') + '</div>' +
    '</div>';
  } else {
    uyariEl.innerHTML = '';
  }

  // --- BU AY ÖZETİ ---
  const buAyGelir = state.servisler.filter(function(s) {
    const d = new Date(s.tarih);
    return s.durum === 'teslim' && d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
  }).reduce(function(a, s) { return a + (parseFloat(s.ucret)||0); }, 0) +
  (state.satislar||[]).filter(function(s) {
    const d = new Date(s.tarih);
    return s.tur === 'satis' && d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
  }).reduce(function(a, s) { return a + s.toplam; }, 0);

  const buAyGider = (state.giderler||[]).filter(function(g) {
    const d = new Date(g.tarih);
    return d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
  }).reduce(function(a, g) { return a + g.tutar; }, 0);

  const kasaBakiye = (state.kasa||[]).reduce(function(a, k) {
    return a + (k.tur === 'giris' ? k.tutar : -k.tutar);
  }, 0);

  const buAyKar = buAyGelir - buAyGider;

  document.getElementById('bu-ay-ozet').innerHTML =
    '<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px">' +
      '<div style="text-align:center"><div style="font-family:sans-serif;font-size:20px;font-weight:700;color:var(--green)">TL' + buAyGelir.toFixed(0) + '</div><div style="font-size:10px;color:var(--muted);text-transform:uppercase">Gelir</div></div>' +
      '<div style="text-align:center"><div style="font-family:sans-serif;font-size:20px;font-weight:700;color:var(--accent2)">TL' + buAyGider.toFixed(0) + '</div><div style="font-size:10px;color:var(--muted);text-transform:uppercase">Gider</div></div>' +
      '<div style="text-align:center"><div style="font-family:sans-serif;font-size:20px;font-weight:700;color:' + (buAyKar >= 0 ? 'var(--green)' : 'var(--accent2)') + '">TL' + buAyKar.toFixed(0) + '</div><div style="font-size:10px;color:var(--muted);text-transform:uppercase">Net Kar</div></div>' +
    '</div>' +
    '<div style="border-top:1px solid var(--border);margin-top:10px;padding-top:10px;display:flex;justify-content:space-between;align-items:center">' +
      '<span style="font-size:12px;color:var(--muted)">🏦 Kasa Bakiyesi</span>' +
      '<span style="font-weight:700;color:' + (kasaBakiye >= 0 ? 'var(--green)' : 'var(--accent2)') + '">TL' + kasaBakiye.toFixed(0) + '</span>' +
    '</div>';

  // --- STATS ---
  const aktif = state.servisler.filter(s => s.durum !== 'teslim' && !s.arsiv).length;
  const bugun = state.servisler.filter(s => {
    const d = new Date(s.tarih);
    return d.toDateString() === now.toDateString();
  }).length;
  const toplamGelir = state.servisler.filter(s => s.durum === 'teslim').reduce((a, s) => a + (parseFloat(s.ucret)||0), 0) +
    (state.satislar || []).filter(s => s.tur === 'satis').reduce((a, s) => a + s.toplam, 0);
  const toplamMaliyet = state.servisler.reduce((a, s) => a + (parseFloat(s.maliyet)||0), 0);
  const kar = toplamGelir - toplamMaliyet;

  document.getElementById('stats-grid').innerHTML = `
    <div class="stat-card">
      <div class="stat-value">${aktif}</div>
      <div class="stat-label">Aktif Servis</div>
    </div>
    <div class="stat-card">
      <div class="stat-value">${bugun}</div>
      <div class="stat-label">Bugün Gelen</div>
    </div>
    <div class="stat-card">
      <div class="stat-value" style="font-size:20px">₺${toplamGelir.toFixed(0)}</div>
      <div class="stat-label">Toplam Gelir</div>
    </div>
    <div class="stat-card">
      <div class="stat-value ${kar>=0?'profit-positive':'profit-negative'}" style="font-size:20px">₺${kar.toFixed(0)}</div>
      <div class="stat-label">Net Kar</div>
    </div>
  `;

  const son = [...state.servisler].reverse().slice(0, 5);
  if (son.length === 0) {
    document.getElementById('recent-list').innerHTML = '<div class="empty"><div class="empty-icon">🔧</div><div>Henüz servis kaydı yok</div></div>';
    return;
  }
  document.getElementById('recent-list').innerHTML = son.map(s => `
    <div class="list-item" onclick="showPage('servisler')">
      <div class="list-item-top">
        <div>
          <div class="list-item-title">${s.musteri} — ${s.alet}</div>
          <div class="list-item-sub">${new Date(s.tarih).toLocaleDateString('tr-TR')} • ${s.marka||''}</div>
        </div>
        <span class="badge badge-${s.durum}">${durumLabel(s.durum)}</span>
      </div>
    </div>
  `).join('');
}

function durumLabel(d) {
  return {bekliyor:'Bekliyor', tamirde:'Tamirde', hazir:'Hazır', teslim:'Teslim'}[d] || d;
}

// --- SERVİS ---
function populateMusteriSelect(id) {
  // artık kullanılmıyor ama eski çağrılar için boş bırakıyoruz
}

function musteriOneri(prefix) {
  const inputId = prefix === 's' ? 's-musteri-ad' : (prefix === 'sat' ? 'sat-musteri' : 'c-isim');
  const oneriId = prefix === 's' ? 's-musteri-oneri' : (prefix === 'sat' ? 'sat-musteri-oneri' : 'c-musteri-oneri');
  const q = document.getElementById(inputId).value.toLowerCase();
  const oneriEl = document.getElementById(oneriId);
  if (!q || q.length < 1) { oneriEl.style.display = 'none'; return; }
  const eslesen = state.musteriler.filter(m => m.ad.toLowerCase().includes(q)).slice(0, 5);
  if (eslesen.length === 0) { oneriEl.style.display = 'none'; return; }
  oneriEl.style.display = 'block';
  oneriEl.innerHTML = eslesen.map(function(m) {
    var tel = m.tel ? ' <span style="color:#888;font-size:11px">('+m.tel+')</span>' : '';
    return '<div onclick="musteriSec(\''+prefix+'\','+m.id+')" style="padding:8px 12px;cursor:pointer;font-size:13px;border-bottom:1px solid #2e2e2e">'+m.ad+tel+'</div>';
  }).join('');
}

function musteriSec(prefix, id) {
  const m = state.musteriler.find(x => x.id === id);
  if (!m) return;
  if (prefix === 's') {
    document.getElementById('s-musteri-ad').value = m.ad;
    document.getElementById('s-musteri-id').value = m.id;
    document.getElementById('s-musteri-oneri').style.display = 'none';
  } else if (prefix === 'sat') {
    document.getElementById('sat-musteri').value = m.ad;
    document.getElementById('sat-musteri-oneri').style.display = 'none';
  } else {
    document.getElementById('c-isim').value = m.ad;
    document.getElementById('c-musteri-oneri').style.display = 'none';
  }
}

function saveServis() {
  const musteriId = document.getElementById('s-musteri-id').value;
  const musteriAd = document.getElementById('s-musteri-ad').value.trim();
  const musteri = state.musteriler.find(m => m.id == musteriId);
  const parcalar = tempParcalar.s;
  const toplamParcaMaliyet = parcalar.reduce((a, p) => a + p.adet * p.birimMaliyet, 0);
  const servis = {
    id: Date.now(),
    musteriId,
    musteri: musteriAd || 'Anonim',
    musteriTel: musteri ? musteri.tel : '',
    alet: document.getElementById('s-alet').value.trim(),
    marka: document.getElementById('s-marka').value.trim(),
    ariza: document.getElementById('s-ariza').value.trim(),
    ucret: document.getElementById('s-ucret').value,
    maliyet: toplamParcaMaliyet.toFixed(0),
    parcalar: parcalar.map(p => ({...p})),
    durum: document.getElementById('s-durum').value,
    not: document.getElementById('s-not').value.trim(),
    tarih: new Date().toISOString()
  };
  if (!servis.alet) { alert('Alet adı giriniz'); return; }
  // Stoktan düş
  parcalar.forEach(p => {
    const stok = state.stok.find(s => s.id === p.stokId);
    if (stok) stok.adet = Math.max(0, stok.adet - p.adet);
  });
  state.servisler.push(servis);
  saveState();
  closeModal('servis-modal');
  ['s-musteri-ad','s-musteri-id','s-alet','s-marka','s-ariza','s-ucret','s-not'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('s-durum').value = 'bekliyor';
  tempParcalar.s = [];
  renderServisler();
}

function filterServis(f) {
  state.servisFilter = f;
  document.querySelectorAll('#servis-filters .filter-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  renderServisler();
}

function arsivle(id) {
  const s = state.servisler.find(x => x.id === id);
  if (!s) return;
  s.arsiv = !s.arsiv;
  saveState();
  renderServisler();
}

function renderServisler() {
  const q = (document.getElementById('servis-search')?.value || '').toLowerCase();
  let list = state.servisler.filter(s => {
    if (state.servisFilter === 'arsiv') return !!s.arsiv;
    if (s.arsiv) return false;
    if (state.servisFilter !== 'hepsi' && s.durum !== state.servisFilter) return false;
    if (q && !s.musteri.toLowerCase().includes(q) && !s.alet.toLowerCase().includes(q) && !(s.marka||'').toLowerCase().includes(q)) return false;
    return true;
  }).reverse();

  if (list.length === 0) {
    document.getElementById('servis-list').innerHTML = '<div class="empty"><div class="empty-icon">🔧</div><div>Kayıt bulunamadı</div></div>';
    return;
  }
  document.getElementById('servis-list').innerHTML = list.map(s => `
    <div class="list-item">
      <div class="list-item-top">
        <div>
          <div class="list-item-title">${s.alet} ${s.marka ? '— '+s.marka : ''}</div>
          <div class="list-item-sub">👤 ${s.musteri} • ${new Date(s.tarih).toLocaleDateString('tr-TR')}</div>
          ${s.ariza ? `<div class="list-item-sub" style="margin-top:4px">🔩 ${s.ariza}</div>` : ''}
          ${s.ucret ? `<div class="list-item-sub" style="margin-top:4px;color:var(--accent)">₺${s.ucret} ${s.maliyet ? '• Maliyet: ₺'+s.maliyet : ''}</div>` : ''}
          ${s.parcalar && s.parcalar.length ? `<div class="list-item-sub" style="margin-top:4px">📦 ${s.parcalar.map(p=>p.ad+' x'+p.adet).join(', ')}</div>` : ''}
        </div>
        <span class="badge badge-${s.durum}">${durumLabel(s.durum)}</span>
      </div>
      <div class="list-item-actions">
        <button class="btn btn-ghost btn-sm" onclick="editServis(${s.id})">✏️ Düzenle</button>
        <button class="btn btn-ghost btn-sm" onclick="faturaCikart(${s.id})">🧾 Fiş</button>
        ${s.musteriTel ? `<button class="btn btn-whatsapp btn-sm" onclick="waServis(${s.id})">📲 WA</button>` : ''}
        <button class="btn btn-ghost btn-sm" onclick="arsivle(${s.id})">${s.arsiv ? '📤 Arşivden Çıkar' : '🗃️ Arşivle'}</button>
        <button class="btn btn-danger btn-sm" onclick="deleteServis(${s.id})">🗑️</button>
      </div>
    </div>
  `).join('');
}

function editServis(id) {
  const s = state.servisler.find(x => x.id === id);
  if (!s) return;
  document.getElementById('se-id').value = id;
  document.getElementById('se-durum').value = s.durum;
  document.getElementById('se-alet').value = s.alet;
  document.getElementById('se-ariza').value = s.ariza;
  document.getElementById('se-ucret').value = s.ucret;
  document.getElementById('se-maliyet').value = s.maliyet;
  document.getElementById('se-not').value = s.not || '';
  tempParcalar.se = s.parcalar ? s.parcalar.map(p => ({...p})) : [];
  populateParcaSelect('se-parca-sec');
  renderTempParcalar('se');
  openModal('servis-edit-modal');
}

function updateServis() {
  const id = parseInt(document.getElementById('se-id').value);
  const s = state.servisler.find(x => x.id === id);
  if (!s) return;
  // Eski parçaları stoka geri ekle
  if (s.parcalar) {
    s.parcalar.forEach(p => {
      const stok = state.stok.find(st => st.id === p.stokId);
      if (stok) stok.adet += p.adet;
    });
  }
  // Yeni parçaları stoktan düş
  const yeniParcalar = tempParcalar.se;
  yeniParcalar.forEach(p => {
    const stok = state.stok.find(st => st.id === p.stokId);
    if (stok) stok.adet = Math.max(0, stok.adet - p.adet);
  });
  const toplamMaliyet = yeniParcalar.reduce((a, p) => a + p.adet * p.birimMaliyet, 0);
  s.alet = document.getElementById('se-alet').value;
  s.ariza = document.getElementById('se-ariza').value;
  s.ucret = document.getElementById('se-ucret').value;
  s.maliyet = toplamMaliyet.toFixed(0);
  s.parcalar = yeniParcalar.map(p => ({...p}));
  s.not = document.getElementById('se-not').value;
  const eskiDurum = s.durum;
  s.durum = document.getElementById('se-durum').value;
  saveState();
  closeModal('servis-edit-modal');
  // Teslim edildi ise kasa sorusu
  if (s.durum === 'teslim' && eskiDurum !== 'teslim' && s.ucret && parseFloat(s.ucret) > 0) {
    setTimeout(function() {
      if (confirm('Servis teslim edildi. TL' + s.ucret + ' kasaya eklensin mi?')) {
        if (!state.kasa) state.kasa = [];
        state.kasa.push({
          id: Date.now(),
          tur: 'giris',
          aciklama: s.musteri + ' - ' + s.alet + ' tamir ucreti',
          tutar: parseFloat(s.ucret),
          odeme: 'Nakit',
          not: '',
          tarih: new Date().toISOString()
        });
        saveState();
      }
    }, 300);
  }
  renderServisler();
}

function deleteServis(id) {
  if (!confirm('Bu servisi silmek istediğinize emin misiniz?')) return;
  state.servisler = state.servisler.filter(s => s.id !== id);
  saveState();
  renderServisler();
}

function waServis(id) {
  const s = state.servisler.find(x => x.id === id);
  if (!s) return;
  const isletmeTel = getIsletmeTel();
  const hedefTel = isletmeTel || s.musteriTel;
  if (!hedefTel) { alert('Telefon numarası bulunamadi. Ayarlar sayfasindan isletme telefonunu girin.'); return; }
  const mesaj = 'Sayin ' + s.musteri + ', "' + s.alet + '" cihaziniz hakkinda bilgilendirme: Durum: ' + durumLabel(s.durum) + '. ' + (s.ucret ? 'Tamir ucreti: TL'+s.ucret+'.' : '') + ' Bilgi icin bizi arayabilirsiniz.';
  const tel = hedefTel.replace(/\D/g, '').replace(/^0/, '');
  window.open('https://wa.me/90' + tel + '?text=' + encodeURIComponent(mesaj));
}

// --- CARİ ---
function saveCari() {
  const cari = {
    id: Date.now(),
    isim: document.getElementById('c-isim').value.trim(),
    tur: document.getElementById('c-tur').value,
    tutar: parseFloat(document.getElementById('c-tutar').value) || 0,
    aciklama: document.getElementById('c-aciklama').value.trim(),
    tarih: new Date().toISOString()
  };
  if (!cari.isim) { alert('İsim giriniz'); return; }
  state.cari.push(cari);
  saveState();
  closeModal('cari-modal');
  ['c-isim','c-tutar','c-aciklama'].forEach(id => document.getElementById(id).value = '');
  renderCari();
}

function filterCari(f) {
  state.cariFilter = f;
  document.querySelectorAll('.filter-row .filter-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  renderCari();
}

function renderCari() {
  const q = (document.getElementById('cari-search')?.value || '').toLowerCase();
  let list = state.cari.filter(c => {
    if (state.cariFilter === 'borc' && c.tur !== 'borc') return false;
    if (state.cariFilter === 'alacak' && c.tur !== 'alacak') return false;
    if (q && !c.isim.toLowerCase().includes(q) && !c.aciklama.toLowerCase().includes(q)) return false;
    return true;
  }).reverse();

  const toplamAlacak = state.cari.filter(c => c.tur === 'alacak').reduce((a, c) => a + c.tutar, 0);
  const toplamBorc = state.cari.filter(c => c.tur === 'borc').reduce((a, c) => a + c.tutar, 0);
  document.getElementById('cari-stats').innerHTML = `
    <div class="stat-card">
      <div class="stat-value profit-positive" style="font-size:22px">₺${toplamAlacak.toFixed(0)}</div>
      <div class="stat-label">Toplam Alacak</div>
    </div>
    <div class="stat-card">
      <div class="stat-value profit-negative" style="font-size:22px">₺${toplamBorc.toFixed(0)}</div>
      <div class="stat-label">Toplam Borç</div>
    </div>
  `;

  if (list.length === 0) {
    document.getElementById('cari-list').innerHTML = '<div class="empty"><div class="empty-icon">💰</div><div>Kayıt bulunamadı</div></div>';
    return;
  }
  document.getElementById('cari-list').innerHTML = list.map(c => `
    <div class="list-item">
      <div class="list-item-top">
        <div>
          <div class="list-item-title">${c.isim}</div>
          <div class="list-item-sub">${c.aciklama || ''} • ${new Date(c.tarih).toLocaleDateString('tr-TR')}</div>
        </div>
        <div style="text-align:right">
          <div style="font-weight:700;font-size:16px;color:${c.tur==='alacak'?'var(--green)':'var(--accent2)'}">₺${c.tutar.toFixed(0)}</div>
          <span class="badge badge-${c.tur}">${c.tur==='alacak'?'Alacak':'Borç'}</span>
        </div>
      </div>
      <div class="list-item-actions">
        <button class="btn btn-success btn-sm" onclick="odendi(${c.id})">✅ Ödendi</button>
        <button class="btn btn-danger btn-sm" onclick="deleteCari(${c.id})">🗑️</button>
      </div>
    </div>
  `).join('');
}

function odendi(id) {
  if (!confirm('Bu kaydı ödendi olarak silmek istiyor musunuz?')) return;
  state.cari = state.cari.filter(c => c.id !== id);
  saveState();
  renderCari();
}

function deleteCari(id) {
  if (!confirm('Bu kaydı silmek istediğinize emin misiniz?')) return;
  state.cari = state.cari.filter(c => c.id !== id);
  saveState();
  renderCari();
}

// --- STOK ---
function saveStok() {
  const stok = {
    id: Date.now(),
    ad: document.getElementById('st-ad').value.trim(),
    adet: parseInt(document.getElementById('st-adet').value) || 0,
    maliyet: parseFloat(document.getElementById('st-maliyet').value) || 0,
    min: parseInt(document.getElementById('st-min').value) || 0,
    tarih: new Date().toISOString()
  };
  if (!stok.ad) { alert('Parça adı giriniz'); return; }
  state.stok.push(stok);
  saveState();
  closeModal('stok-modal');
  ['st-ad','st-adet','st-maliyet','st-min'].forEach(id => document.getElementById(id).value = '');
  renderStok();
}

function renderStok() {
  const q = (document.getElementById('stok-search') ? document.getElementById('stok-search').value : '').toLowerCase();
  const stokList = state.stok.filter(function(s) { return !q || s.ad.toLowerCase().includes(q); });
  if (stokList.length === 0) {
    document.getElementById('stok-list').innerHTML = '<div class="empty"><div class="empty-icon">📦</div><div>Stok kaydı yok</div></div>';
    return;
  }
  document.getElementById('stok-list').innerHTML = stokList.map(s => `
    <div class="list-item" style="${s.adet <= s.min ? 'border-color:var(--accent2)' : ''}">
      <div class="list-item-top">
        <div>
          <div class="list-item-title">${s.ad}</div>
          <div class="list-item-sub">Birim: ₺${s.maliyet} ${s.min ? '• Min: '+s.min : ''}</div>
          ${s.adet <= s.min ? '<div style="font-size:11px;color:var(--accent2);margin-top:4px">⚠️ Düşük stok!</div>' : ''}
        </div>
        <div style="text-align:right">
          <div style="font-family:\'Bebas Neue\';font-size:28px;color:${s.adet<=s.min?'var(--accent2)':'var(--accent)'}">${s.adet}</div>
          <div style="font-size:11px;color:var(--muted)">ADET</div>
        </div>
      </div>
      <div class="list-item-actions">
        <button class="btn btn-ghost btn-sm" onclick="editStok(${s.id})">✏️ Düzenle</button>
        <button class="btn btn-danger btn-sm" onclick="deleteStok(${s.id})">🗑️</button>
      </div>
    </div>
  `).join('');
}

function stokGuncelle(id, delta) {
  const s = state.stok.find(x => x.id === id);
  if (!s) return;
  s.adet = Math.max(0, s.adet + delta);
  saveState();
  renderStok();
}

function editStok(id) {
  const s = state.stok.find(x => x.id === id);
  if (!s) return;
  document.getElementById('ste-id').value = id;
  document.getElementById('ste-ad').value = s.ad;
  document.getElementById('ste-adet').value = s.adet;
  document.getElementById('ste-maliyet').value = s.maliyet;
  document.getElementById('ste-min').value = s.min || 0;
  document.getElementById('stok-edit-modal').classList.add('active');
}

function updateStok() {
  const id = parseInt(document.getElementById('ste-id').value);
  const s = state.stok.find(x => x.id === id);
  if (!s) return;
  const ad = document.getElementById('ste-ad').value.trim();
  if (!ad) { alert('Parça adı giriniz'); return; }
  s.ad = ad;
  s.adet = parseInt(document.getElementById('ste-adet').value) || 0;
  s.maliyet = parseFloat(document.getElementById('ste-maliyet').value) || 0;
  s.min = parseInt(document.getElementById('ste-min').value) || 0;
  saveState();
  closeModal('stok-edit-modal');
  renderStok();
}

function deleteStok(id) {
  if (!confirm('Bu stok kaydını silmek istediğinize emin misiniz?')) return;
  state.stok = state.stok.filter(s => s.id !== id);
  saveState();
  renderStok();
}

// --- MÜŞTERİLER ---
function saveMusteri() {
  const m = {
    id: Date.now(),
    ad: document.getElementById('m-ad').value.trim(),
    tel: document.getElementById('m-tel').value.trim(),
    not: document.getElementById('m-not').value.trim(),
    tarih: new Date().toISOString()
  };
  if (!m.ad) { alert('İsim giriniz'); return; }
  state.musteriler.push(m);
  saveState();
  closeModal('musteri-modal');
  ['m-ad','m-tel','m-not'].forEach(id => document.getElementById(id).value = '');
  renderMusteriler();
}

function renderMusteriler() {
  const q = (document.getElementById('musteri-search')?.value || '').toLowerCase();
  let list = state.musteriler.filter(m => {
    if (q && !m.ad.toLowerCase().includes(q) && !(m.tel||'').includes(q)) return false;
    return true;
  });

  if (list.length === 0) {
    document.getElementById('musteri-list').innerHTML = '<div class="empty"><div class="empty-icon">👥</div><div>Müşteri kaydı yok</div></div>';
    return;
  }
  document.getElementById('musteri-list').innerHTML = list.map(m => {
    const servisSayisi = state.servisler.filter(s => s.musteriId == m.id).length;
    return `
    <div class="list-item">
      <div class="list-item-top">
        <div>
          <div class="list-item-title">${m.ad}</div>
          <div class="list-item-sub">${m.tel || 'Telefon yok'} ${m.not ? '• '+m.not : ''}</div>
          <div class="list-item-sub" style="margin-top:4px">🔧 ${servisSayisi} servis kaydı</div>
        </div>
        <div style="display:flex;flex-direction:column;gap:6px;align-items:flex-end">
          ${m.tel ? `<button class="btn btn-whatsapp btn-sm" onclick="waMusteri('${m.tel}','${m.ad}')">📲</button>` : ''}
          <button class="btn btn-danger btn-sm" onclick="deleteMusteri(${m.id})">🗑️</button>
        </div>
      </div>
    </div>
  `}).join('');
}

function waMusteri(tel, ad) {
  const isletmeTel = getIsletmeTel();
  const hedefTel = isletmeTel || tel;
  const t = hedefTel.replace(/\D/g, '').replace(/^0/, '');
  window.open('https://wa.me/90' + t + '?text=' + encodeURIComponent('Sayin ' + ad + ', servisiniz hakkinda bilgi vermek istedik.'));
}

function deleteMusteri(id) {
  if (!confirm('Bu müşteriyi silmek istediğinize emin misiniz?')) return;
  state.musteriler = state.musteriler.filter(m => m.id !== id);
  saveState();
  renderMusteriler();
}


// --- FATURA ---
let aktivFaturaServisId = null;
function faturaCikart(id) {
  const s = state.servisler.find(x => x.id === id);
  if (!s) return;
  aktivFaturaServisId = id;
  const tarih = new Date(s.tarih).toLocaleDateString('tr-TR');
  const parcalarHtml = s.parcalar && s.parcalar.length
    ? s.parcalar.map(p => `  ${p.ad} x${p.adet}  ₺${(p.adet*p.birimMaliyet).toFixed(0)}`).join('<br>')
    : '  —';
  document.getElementById('fatura-content').innerHTML =
    '<div style="text-align:center;font-weight:bold;font-size:15px;margin-bottom:8px">⚙️ ' + ((state.ayarlar && state.ayarlar.isletmeAd) ? state.ayarlar.isletmeAd.toUpperCase() : 'EL ALETI TAMIR SERVISI') + '</div>' +
    '<div style="border-top:1px dashed #ccc;margin:6px 0"></div>' +
    `<b>Müşteri:</b> ${s.musteri}<br>` +
    `<b>Tarih:</b> ${tarih}<br>` +
    `<b>Alet:</b> ${s.alet}${s.marka ? ' / '+s.marka : ''}<br>` +
    `<b>Arıza:</b> ${s.ariza || '—'}<br>` +
    '<div style="border-top:1px dashed #ccc;margin:6px 0"></div>' +
    '<b>Kullanılan Parçalar:</b><br>' + parcalarHtml + '<br>' +
    '<div style="border-top:1px dashed #ccc;margin:6px 0"></div>' +
    `<b>Parça Maliyeti:</b>  ₺${parseFloat(s.maliyet||0).toFixed(0)}<br>` +
    `<b style="font-size:15px">TAMİR ÜCRETİ:  ₺${parseFloat(s.ucret||0).toFixed(0)}</b><br>` +
    '<div style="border-top:1px dashed #ccc;margin:6px 0"></div>' +
    `<b>Durum:</b> ${durumLabel(s.durum)}<br>` +
    (s.not ? `<b>Not:</b> ${s.not}<br>` : '') +
    '<div style="text-align:center;margin-top:8px;font-size:11px;color:#888">Teşekkürler 🙏</div>';
  openModal('fatura-modal');
}

function faturayiWAGonder() {
  const s = state.servisler.find(x => x.id === aktivFaturaServisId);
  if (!s || !s.musteriTel) { alert('Bu servis için telefon numarası yok'); return; }
  const tarih = new Date(s.tarih).toLocaleDateString('tr-TR');
  const parcalar = s.parcalar && s.parcalar.length
    ? s.parcalar.map(p => p.ad+' x'+p.adet+' = ₺'+(p.adet*p.birimMaliyet).toFixed(0)).join(', ')
    : '—';
  const metin =
    '⚙️ *EL ALETİ TAMİR SERVİSİ*\n' +
    '━━━━━━━━━━━━━━\n' +
    `👤 Müşteri: ${s.musteri}\n` +
    `📅 Tarih: ${tarih}\n` +
    `🔧 Alet: ${s.alet}${s.marka?' / '+s.marka:''}\n` +
    `🔩 Arıza: ${s.ariza||'—'}\n` +
    '━━━━━━━━━━━━━━\n' +
    `📦 Parçalar: ${parcalar}\n` +
    `💰 Tamir Ücreti: ₺${parseFloat(s.ucret||0).toFixed(0)}\n` +
    `📋 Durum: ${durumLabel(s.durum)}\n` +
    '━━━━━━━━━━━━━━\n' +
    'Teşekkürler 🙏';
  const tel = s.musteriTel.replace(/\D/g,'').replace(/^0/,'');
  window.open('https://wa.me/90'+tel+'?text='+encodeURIComponent(metin));
}

// --- GRAFİK ---
function renderGrafik() {
  const aylar = {};
  if (state.satislar) {
    state.satislar.forEach(function(s) {
      const d = new Date(s.tarih);
      const key = d.getFullYear()+'-'+(d.getMonth()+1).toString().padStart(2,'0');
      if (!aylar[key]) aylar[key] = { gelir: 0, maliyet: 0, adet: 0 };
      if (s.tur === 'satis') aylar[key].gelir += s.toplam;
      else aylar[key].maliyet += s.toplam;
    });
  }
  if (state.giderler) {
    state.giderler.forEach(function(g) {
      const d = new Date(g.tarih);
      const key = d.getFullYear()+'-'+(d.getMonth()+1).toString().padStart(2,'0');
      if (!aylar[key]) aylar[key] = { gelir: 0, maliyet: 0, adet: 0 };
      aylar[key].maliyet += g.tutar;
    });
  }
  state.servisler.forEach(s => {
    const d = new Date(s.tarih);
    const key = d.getFullYear()+'-'+(d.getMonth()+1).toString().padStart(2,'0');
    if (!aylar[key]) aylar[key] = { gelir: 0, maliyet: 0, adet: 0 };
    aylar[key].gelir += parseFloat(s.ucret||0);
    aylar[key].maliyet += parseFloat(s.maliyet||0);
    aylar[key].adet++;
  });

  const keys = Object.keys(aylar).sort().slice(-6);
  if (keys.length === 0) {
    document.getElementById('grafik-tablo').innerHTML = '<div class="empty"><div class="empty-icon">📈</div><div>Henüz veri yok</div></div>';
    document.getElementById('grafik-canvas').style.display = 'none';
    return;
  }
  document.getElementById('grafik-canvas').style.display = 'block';

  const canvas = document.getElementById('grafik-canvas');
  const ctx = canvas.getContext('2d');
  const W = canvas.offsetWidth || 340;
  const H = 220;
  canvas.width = W;
  canvas.height = H;

  const gelirler = keys.map(k => aylar[k].gelir);
  const karlar = keys.map(k => aylar[k].gelir - aylar[k].maliyet);
  const maxVal = Math.max(...gelirler, 1);
  const padL = 50, padR = 16, padT = 20, padB = 40;
  const chartW = W - padL - padR;
  const chartH = H - padT - padB;
  const barW = chartW / keys.length;

  ctx.clearRect(0, 0, W, H);

  // Grid
  ctx.strokeStyle = '#2e2e2e';
  ctx.lineWidth = 1;
  for (let i = 0; i <= 4; i++) {
    const y = padT + (chartH / 4) * i;
    ctx.beginPath(); ctx.moveTo(padL, y); ctx.lineTo(W - padR, y); ctx.stroke();
    const val = Math.round(maxVal * (1 - i/4));
    ctx.fillStyle = '#666'; ctx.font = '10px IBM Plex Sans'; ctx.textAlign = 'right';
    ctx.fillText('₺'+val, padL - 4, y + 3);
  }

  // Bars
  keys.forEach((k, i) => {
    const x = padL + i * barW;
    const gelir = aylar[k].gelir;
    const kar = karlar[i];

    // Gelir bar
    const gelirH = (gelir / maxVal) * chartH;
    ctx.fillStyle = '#f59e0b44';
    ctx.fillRect(x + barW*0.1, padT + chartH - gelirH, barW*0.38, gelirH);

    // Kar bar
    const karH = Math.abs(kar) / maxVal * chartH;
    ctx.fillStyle = kar >= 0 ? '#22c55e88' : '#ef444488';
    ctx.fillRect(x + barW*0.52, padT + chartH - (kar >= 0 ? karH : 0) - (kar < 0 ? 0 : 0), barW*0.38, karH);

    // X label
    const [y, m] = k.split('-');
    ctx.fillStyle = '#888'; ctx.font = '10px IBM Plex Sans'; ctx.textAlign = 'center';
    ctx.fillText(m+'/'+y.slice(2), x + barW/2, H - padB + 14);
  });

  // Legend
  ctx.fillStyle = '#f59e0b'; ctx.fillRect(padL, H - 12, 10, 8);
  ctx.fillStyle = '#aaa'; ctx.font = '10px IBM Plex Sans'; ctx.textAlign = 'left';
  ctx.fillText('Gelir', padL + 13, H - 5);
  ctx.fillStyle = '#22c55e'; ctx.fillRect(padL + 60, H - 12, 10, 8);
  ctx.fillText('Kar', padL + 73, H - 5);

  // Tablo
  let tabloHtml = '<div class="card"><table style="width:100%;border-collapse:collapse;font-size:13px">';
  tabloHtml += '<tr style="color:var(--muted);font-size:11px"><th style="text-align:left;padding:6px">AY</th><th style="text-align:right;padding:6px">ADET</th><th style="text-align:right;padding:6px">GELİR</th><th style="text-align:right;padding:6px">MALİYET</th><th style="text-align:right;padding:6px">KAR</th></tr>';
  keys.forEach(k => {
    const a = aylar[k];
    const kar = a.gelir - a.maliyet;
    const [y, m] = k.split('-');
    tabloHtml += `<tr style="border-top:1px solid var(--border)">
      <td style="padding:8px 6px">${m}/${y}</td>
      <td style="text-align:right;padding:8px 6px">${a.adet}</td>
      <td style="text-align:right;padding:8px 6px;color:var(--accent)">₺${a.gelir.toFixed(0)}</td>
      <td style="text-align:right;padding:8px 6px;color:var(--accent2)">₺${a.maliyet.toFixed(0)}</td>
      <td style="text-align:right;padding:8px 6px;color:${kar>=0?'var(--green)':'var(--accent2)'}">₺${kar.toFixed(0)}</td>
    </tr>`;
  });
  tabloHtml += '</table></div>';
  document.getElementById('grafik-tablo').innerHTML = tabloHtml;
}


// --- GOOGLE DRIVE ---
const GDRIVE_CLIENT_ID = '993693946658-2ds858f9ctq2vkfa8grnmetr3jgmo3u0.apps.googleusercontent.com';
const GDRIVE_SCOPES = 'https://www.googleapis.com/auth/drive.file';
const GDRIVE_FILE_NAME = 'servis_takip_yedek.json';
let gdriveToken = null;
let gdriveFileId = null;

function renderDriveBar() {
  const bar = document.getElementById('drive-bar');
  if (!bar) return;
  const durum = window._firebaseReady ? '🟢 Firebase bağlı — otomatik senkron aktif' : '🟡 Firebase bağlanıyor...';
  const renk = window._firebaseReady ? 'var(--green)' : 'var(--accent)';
  bar.innerHTML = '<div style="display:flex;gap:8px;align-items:center;background:var(--surface);border:1px solid ' + renk + ';border-radius:8px;padding:10px 14px;">' +
    '<div style="color:' + renk + ';font-size:13px;flex:1">' + durum + '</div>' +
    '</div>';
}

function driveGiris(sessiz) {
  if (typeof google === 'undefined' || !google.accounts) {
    if (!sessiz) alert('Google API yuklenemedi. Internet baglantinizi kontrol edin.');
    return;
  }
  const client = google.accounts.oauth2.initTokenClient({
    client_id: GDRIVE_CLIENT_ID,
    scope: GDRIVE_SCOPES,
    callback: function(resp) {
      if (resp.error) { if (!sessiz) alert('Giris basarisiz: ' + resp.error); return; }
      gdriveToken = resp.access_token;
      // Token süresini kaydet (55 dakika)
      const expire = Date.now() + 55 * 60 * 1000;
      try { localStorage.setItem('gdrive_token', resp.access_token); localStorage.setItem('gdrive_expire', expire); } catch(e) {}
      renderDriveBar();
      if (!sessiz) alert('Google Drive baglandi! Otomatik yedekleme aktif.');
    }
  });
  client.requestAccessToken();
}

function driveTokenKontrol() {
  // Kaydedilmiş token varsa ve süresi dolmamışsa yükle
  try {
    const token = localStorage.getItem('gdrive_token');
    const expire = parseInt(localStorage.getItem('gdrive_expire') || '0');
    if (token && Date.now() < expire) {
      gdriveToken = token;
      renderDriveBar();
      return true;
    }
  } catch(e) {}
  return false;
}

function driveCikis() {
  gdriveToken = null;
  gdriveFileId = null;
  try { localStorage.removeItem('gdrive_token'); localStorage.removeItem('gdrive_expire'); } catch(e) {}
  renderDriveBar();
}

async function driveDosyaBul() {
  const res = await fetch(
    "https://www.googleapis.com/drive/v3/files?q=name='" + GDRIVE_FILE_NAME + "'+and+trashed=false&fields=files(id,name)",
    { headers: { Authorization: 'Bearer ' + gdriveToken } }
  );
  const data = await res.json();
  if (data.files && data.files.length > 0) {
    gdriveFileId = data.files[0].id;
    return data.files[0].id;
  }
  return null;
}

async function driveyeYedekle(sessiz) {
  if (!gdriveToken) { if (!sessiz) alert('Once Google Drive baglantisi gerekli'); return; }
  try {
    const jsonStr = JSON.stringify(state, null, 2);
    const blob = new Blob([jsonStr], { type: 'application/json' });
    const fileId = await driveDosyaBul();

    let url, method;
    if (fileId) {
      url = 'https://www.googleapis.com/upload/drive/v3/files/' + fileId + '?uploadType=media';
      method = 'PATCH';
    } else {
      // Önce metadata ile dosya oluştur
      const meta = await fetch('https://www.googleapis.com/drive/v3/files', {
        method: 'POST',
        headers: { Authorization: 'Bearer ' + gdriveToken, 'Content-Type': 'application/json' },
        body: JSON.stringify({ name: GDRIVE_FILE_NAME, mimeType: 'application/json' })
      });
      const metaData = await meta.json();
      gdriveFileId = metaData.id;
      url = 'https://www.googleapis.com/upload/drive/v3/files/' + gdriveFileId + '?uploadType=media';
      method = 'PATCH';
    }

    const res = await fetch(url, {
      method,
      headers: { Authorization: 'Bearer ' + gdriveToken, 'Content-Type': 'application/json' },
      body: jsonStr
    });
    if (res.ok) {
      if (!sessiz) alert('Veriler Google Drive a yedeklendi!');
      else console.log('Otomatik yedek tamam:', new Date().toLocaleTimeString());
    } else {
      if (!sessiz) alert('Hata olustu: ' + res.status);
    }
  } catch(e) {
    if (!sessiz) alert('Yedekleme hatasi: ' + e.message);
  }
}

async function drivedenYukle() {
  if (!gdriveToken) { alert('Önce Google Drive bağlantısı gerekli'); return; }
  try {
    const fileId = await driveDosyaBul();
    if (!fileId) { alert('Drive da yedek dosyasi bulunamadi. Once yedek alin.'); return; }
    const res = await fetch('https://www.googleapis.com/drive/v3/files/' + fileId + '?alt=media', {
      headers: { Authorization: 'Bearer ' + gdriveToken }
    });
    const data = await res.json();
    if (!confirm('Driveda yedek yuklenecek. Mevcut veriler silinecek. Emin misiniz?')) return;
    state = data;
    saveState();
    renderDashboard();
    alert('Veriler Drive dan yuklendi!');
  } catch(e) {
    alert('Yükleme hatası: ' + e.message);
  }
}




// --- AYARLAR ---
function renderAyarlar() {
  if (!state.ayarlar) state.ayarlar = { isletmeAd: '', isletmeTel: '', adres: '', uyariAktif: true };
  document.getElementById('ay-isletme-ad').value = state.ayarlar.isletmeAd || '';
  document.getElementById('ay-isletme-tel').value = state.ayarlar.isletmeTel || '';
  document.getElementById('ay-adres').value = state.ayarlar.adres || '';
  const cb = document.getElementById('ay-uyari');
  cb.checked = state.ayarlar.uyariAktif !== false;
  document.getElementById('ay-uyari-span').style.background = cb.checked ? 'var(--accent)' : 'var(--border)';
}

function saveAyarlar() {
  if (!state.ayarlar) state.ayarlar = {};
  state.ayarlar.isletmeAd = document.getElementById('ay-isletme-ad').value.trim();
  state.ayarlar.isletmeTel = document.getElementById('ay-isletme-tel').value.trim();
  state.ayarlar.adres = document.getElementById('ay-adres').value.trim();
  state.ayarlar.uyariAktif = document.getElementById('ay-uyari').checked;
  document.getElementById('ay-uyari-span').style.background = state.ayarlar.uyariAktif ? 'var(--accent)' : 'var(--border)';
  saveState();
  alert('Ayarlar kaydedildi!');
}

function getIsletmeTel() {
  return (state.ayarlar && state.ayarlar.isletmeTel) ? state.ayarlar.isletmeTel : null;
}

// --- GİDER ---
const KATEGORI_ANAHTAR = {
  kira: ['kira', 'depozito', 'kiralik'],
  fatura: ['elektrik', 'su', 'dogalgaz', 'internet', 'fatura', 'aidat'],
  personel: ['maas', 'ucret', 'personel', 'isci', 'usta', 'calisan'],
  malzeme: ['malzeme', 'parca', 'sarf', 'temizlik', 'alet', 'ekipman']
};

function kategoriTahmin(aciklama) {
  const a = aciklama.toLowerCase().replace(/[ğüşıöç]/g, function(c) {
    return {g:'g',u:'u',s:'s',i:'i',o:'o',c:'c'}[c] || c;
  });
  for (const kat in KATEGORI_ANAHTAR) {
    if (KATEGORI_ANAHTAR[kat].some(function(k) { return a.includes(k); })) return kat;
  }
  return 'diger';
}

function kategoriLabel(k) {
  return {kira:'🏠 Kira', fatura:'💡 Fatura', personel:'👤 Personel', malzeme:'🔩 Malzeme', diger:'📌 Diğer'}[k] || k;
}

// Açıklama yazınca otomatik kategori seç
document.addEventListener('DOMContentLoaded', function() {
  const gAciklama = document.getElementById('g-aciklama');
  if (gAciklama) {
    gAciklama.addEventListener('input', function() {
      const kat = kategoriTahmin(this.value);
      document.getElementById('g-kategori').value = kat;
    });
  }
});

let giderFilter = 'hepsi';

function filterGider(f) {
  giderFilter = f;
  document.querySelectorAll('#gider-filters .filter-btn').forEach(function(b) { b.classList.remove('active'); });
  event.target.classList.add('active');
  renderGider();
}

function saveGider() {
  const aciklama = document.getElementById('g-aciklama').value.trim();
  const tutar = parseFloat(document.getElementById('g-tutar').value) || 0;
  if (!aciklama) { alert('Aciklama giriniz'); return; }
  if (!tutar) { alert('Tutar giriniz'); return; }
  const gider = {
    id: Date.now(),
    aciklama,
    tutar,
    odeme: document.getElementById('g-odeme').value.trim() || 'Nakit',
    kategori: document.getElementById('g-kategori').value,
    tarih: new Date().toISOString()
  };
  if (!state.giderler) state.giderler = [];
  state.giderler.push(gider);
  saveState();
  ['g-aciklama','g-tutar','g-odeme'].forEach(function(id) { document.getElementById(id).value = ''; });
  document.getElementById('g-kategori').value = 'diger';
  closeModal('gider-modal');
  renderGider();
}

function renderGider() {
  if (!state.giderler) state.giderler = [];
  const q = (document.getElementById('gider-search') ? document.getElementById('gider-search').value : '').toLowerCase();
  let list = state.giderler.filter(function(g) {
    if (giderFilter !== 'hepsi' && g.kategori !== giderFilter) return false;
    if (q && !g.aciklama.toLowerCase().includes(q)) return false;
    return true;
  }).reverse();

  const buAy = new Date();
  const ayGider = state.giderler.filter(function(g) {
    const d = new Date(g.tarih);
    return d.getMonth() === buAy.getMonth() && d.getFullYear() === buAy.getFullYear();
  }).reduce(function(a, g) { return a + g.tutar; }, 0);
  const toplamGider = state.giderler.reduce(function(a, g) { return a + g.tutar; }, 0);

  document.getElementById('gider-stats').innerHTML =
    '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">TL' + ayGider.toFixed(0) + '</div><div class="stat-label">Bu Ay Gider</div></div>' +
    '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">TL' + toplamGider.toFixed(0) + '</div><div class="stat-label">Toplam Gider</div></div>';

  if (list.length === 0) {
    document.getElementById('gider-list').innerHTML = '<div class="empty"><div class="empty-icon">📉</div><div>Gider kaydi yok</div></div>';
    return;
  }
  document.getElementById('gider-list').innerHTML = list.map(function(g) {
    return '<div class="list-item">' +
      '<div class="list-item-top">' +
        '<div>' +
          '<div class="list-item-title">' + g.aciklama + '</div>' +
          '<div class="list-item-sub">' + kategoriLabel(g.kategori) + ' • ' + g.odeme + ' • ' + new Date(g.tarih).toLocaleDateString('tr-TR') + '</div>' +
        '</div>' +
        '<div style="font-weight:700;font-size:16px;color:var(--accent2)">TL' + g.tutar.toFixed(0) + '</div>' +
      '</div>' +
      '<div class="list-item-actions">' +
        '<button class="btn btn-danger btn-sm" onclick="deleteGider(' + g.id + ')">🗑</button>' +
      '</div>' +
    '</div>';
  }).join('');
}

function deleteGider(id) {
  if (!confirm('Bu kaydi silmek istediginize emin misiniz?')) return;
  state.giderler = state.giderler.filter(function(g) { return g.id !== id; });
  saveState();
  renderGider();
}

// --- KASA ---
let kasaFilter = 'hepsi';

function filterKasa(f) {
  kasaFilter = f;
  document.querySelectorAll('#kasa-filters .filter-btn').forEach(function(b) { b.classList.remove('active'); });
  event.target.classList.add('active');
  renderKasa();
}

function saveKasa() {
  const aciklama = document.getElementById('k-aciklama').value.trim();
  const tutar = parseFloat(document.getElementById('k-tutar').value) || 0;
  if (!aciklama) { alert('Aciklama giriniz'); return; }
  if (!tutar) { alert('Tutar giriniz'); return; }
  const hareket = {
    id: Date.now(),
    tur: document.getElementById('k-tur').value,
    aciklama,
    tutar,
    odeme: document.getElementById('k-odeme').value.trim() || 'Nakit',
    not: document.getElementById('k-not').value.trim(),
    tarih: new Date().toISOString()
  };
  if (!state.kasa) state.kasa = [];
  state.kasa.push(hareket);
  saveState();
  ['k-aciklama','k-tutar','k-odeme','k-not'].forEach(function(id) { document.getElementById(id).value = ''; });
  document.getElementById('k-tur').value = 'giris';
  closeModal('kasa-modal');
  renderKasa();
}

function renderKasa() {
  if (!state.kasa) state.kasa = [];
  const toplamGiris = state.kasa.filter(function(k) { return k.tur === 'giris'; }).reduce(function(a, k) { return a + k.tutar; }, 0);
  const toplamCikis = state.kasa.filter(function(k) { return k.tur === 'cikis'; }).reduce(function(a, k) { return a + k.tutar; }, 0);
  const bakiye = toplamGiris - toplamCikis;

  // Nakit/Kredi/Havale bakiyeleri
  const odemeTurleri = {};
  state.kasa.forEach(function(k) {
    const o = (k.odeme || 'Nakit').toLowerCase();
    if (!odemeTurleri[o]) odemeTurleri[o] = 0;
    odemeTurleri[o] += k.tur === 'giris' ? k.tutar : -k.tutar;
  });
  const odemeHtml = Object.keys(odemeTurleri).map(function(o) {
    const val = odemeTurleri[o];
    return '<div style="display:flex;justify-content:space-between;padding:4px 0;font-size:13px">' +
      '<span style="color:var(--muted)">' + o.charAt(0).toUpperCase() + o.slice(1) + '</span>' +
      '<span style="color:' + (val >= 0 ? 'var(--green)' : 'var(--accent2)') + ';font-weight:600">TL' + val.toFixed(0) + '</span>' +
    '</div>';
  }).join('');

  document.getElementById('kasa-bakiye-card').innerHTML =
    '<div class="card">' +
      '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">' +
        '<div style="font-family:monospace;font-size:16px;color:var(--muted)">KASA BAKİYESİ</div>' +
        '<div style="font-family:sans-serif;font-size:32px;color:' + (bakiye >= 0 ? 'var(--green)' : 'var(--accent2)') + '">TL' + bakiye.toFixed(0) + '</div>' +
      '</div>' +
      '<div style="border-top:1px solid var(--border);padding-top:10px">' + odemeHtml + '</div>' +
    '</div>';

  // Günlük özet (bugün)
  const bugun = new Date().toDateString();
  const bugunHareketler = state.kasa.filter(function(k) { return new Date(k.tarih).toDateString() === bugun; });
  const bugunGiris = bugunHareketler.filter(function(k) { return k.tur === 'giris'; }).reduce(function(a, k) { return a + k.tutar; }, 0);
  const bugunCikis = bugunHareketler.filter(function(k) { return k.tur === 'cikis'; }).reduce(function(a, k) { return a + k.tutar; }, 0);
  document.getElementById('kasa-gunluk').innerHTML = bugunHareketler.length > 0 ?
    '<div style="display:flex;gap:8px;margin-bottom:4px">' +
      '<div class="stat-card" style="flex:1"><div class="stat-value profit-positive" style="font-size:18px">TL' + bugunGiris.toFixed(0) + '</div><div class="stat-label">Bugün Giriş</div></div>' +
      '<div class="stat-card" style="flex:1"><div class="stat-value profit-negative" style="font-size:18px">TL' + bugunCikis.toFixed(0) + '</div><div class="stat-label">Bugün Çıkış</div></div>' +
    '</div>' : '';

  // Liste filtresi
  let list = state.kasa.filter(function(k) {
    if (kasaFilter === 'giris' && k.tur !== 'giris') return false;
    if (kasaFilter === 'cikis' && k.tur !== 'cikis') return false;
    if (kasaFilter === 'nakit' && (k.odeme||'nakit').toLowerCase() !== 'nakit') return false;
    if (kasaFilter === 'kredi' && (k.odeme||'').toLowerCase() !== 'kredi') return false;
    if (kasaFilter === 'havale' && (k.odeme||'').toLowerCase() !== 'havale') return false;
    return true;
  }).reverse();

  if (list.length === 0) {
    document.getElementById('kasa-list').innerHTML = '<div class="empty"><div class="empty-icon">🏦</div><div>Hareket kaydi yok</div></div>';
    return;
  }
  document.getElementById('kasa-list').innerHTML = list.map(function(k) {
    const giris = k.tur === 'giris';
    return '<div class="list-item">' +
      '<div class="list-item-top">' +
        '<div>' +
          '<div class="list-item-title">' + (giris ? '⬆️ ' : '⬇️ ') + k.aciklama + '</div>' +
          '<div class="list-item-sub">' + (k.odeme||'Nakit') + ' • ' + new Date(k.tarih).toLocaleDateString('tr-TR') + (k.not ? ' • ' + k.not : '') + '</div>' +
        '</div>' +
        '<div style="font-weight:700;font-size:16px;color:' + (giris ? 'var(--green)' : 'var(--accent2)') + '">' + (giris ? '+' : '-') + 'TL' + k.tutar.toFixed(0) + '</div>' +
      '</div>' +
      '<div class="list-item-actions">' +
        '<button class="btn btn-danger btn-sm" onclick="deleteKasa(' + k.id + ')">🗑</button>' +
      '</div>' +
    '</div>';
  }).join('');
}

function deleteKasa(id) {
  if (!confirm('Bu kaydi silmek istediginize emin misiniz?')) return;
  state.kasa = state.kasa.filter(function(k) { return k.id !== id; });
  saveState();
  renderKasa();
}

// --- SATIS / ALIS ---
let satKalemler = [];
let alKalemler = [];
let saatisFilter = 'hepsi';

function openSatisModal() {
  satKalemler = [];
  populateSatStok();
  renderSatKalemler();
  document.getElementById('satis-modal').classList.add('active');
}

function openAlisModal() {
  alKalemler = [];
  renderAlKalemler();
  document.getElementById('alis-modal').classList.add('active');
}

function populateSatStok() {
  const el = document.getElementById('sat-stok-sec');
  if (!el) return;
  el.innerHTML = '<option value="">Stoktan sec...</option>' +
    state.stok.filter(s => s.adet > 0).map(s =>
      '<option value="' + s.id + '">' + s.ad + ' (Stok:' + s.adet + ') - urun</option>'
    ).join('');
}

function satStokSec() {
  const id = parseInt(document.getElementById('sat-stok-sec').value);
  if (!id) return;
  const s = state.stok.find(x => x.id === id);
  if (!s) return;
  document.getElementById('sat-urun-ad').value = s.ad;
  document.getElementById('sat-urun-fiyat').value = s.maliyet;
  document.getElementById('sat-urun-adet').value = 1;
}

function satKalemEkle() {
  const ad = document.getElementById('sat-urun-ad').value.trim();
  const adet = parseInt(document.getElementById('sat-urun-adet').value) || 1;
  const fiyat = parseFloat(document.getElementById('sat-urun-fiyat').value) || 0;
  const stokId = parseInt(document.getElementById('sat-stok-sec').value) || null;
  if (!ad) { alert('Urun adi giriniz'); return; }
  if (stokId) {
    const s = state.stok.find(x => x.id === stokId);
    if (s && adet > s.adet) { alert('Stokta sadece ' + s.adet + ' adet var!'); return; }
  }
  satKalemler.push({ ad, adet, fiyat, stokId });
  document.getElementById('sat-urun-ad').value = '';
  document.getElementById('sat-urun-fiyat').value = '';
  document.getElementById('sat-urun-adet').value = 1;
  document.getElementById('sat-stok-sec').value = '';
  renderSatKalemler();
}

function renderSatKalemler() {
  const el = document.getElementById('sat-kalemler-list');
  if (!el) return;
  const toplam = satKalemler.reduce((a, k) => a + k.adet * k.fiyat, 0);
  document.getElementById('sat-toplam').textContent = 'TL' + toplam.toFixed(0);
  if (satKalemler.length === 0) { el.innerHTML = ''; return; }
  el.innerHTML = '<div style="margin-bottom:10px">' + satKalemler.map(function(k, i) {
    return '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:6px;padding:8px 10px;margin-bottom:6px">' +
      '<div><div style="font-size:13px;font-weight:600">' + k.ad + '</div>' +
      '<div style="font-size:11px;color:#888">' + k.adet + ' adet x TL' + k.fiyat + ' = TL' + (k.adet*k.fiyat).toFixed(0) + '</div></div>' +
      '<button onclick="satKalemSil(' + i + ')" style="background:none;border:none;color:var(--accent2);font-size:18px;cursor:pointer">x</button>' +
    '</div>';
  }).join('') + '</div>';
}

function satKalemSil(i) {
  satKalemler.splice(i, 1);
  renderSatKalemler();
}

function alKalemEkle() {
  const ad = document.getElementById('al-urun-ad').value.trim();
  const adet = parseInt(document.getElementById('al-urun-adet').value) || 1;
  const fiyat = parseFloat(document.getElementById('al-urun-fiyat').value) || 0;
  if (!ad) { alert('Urun adi giriniz'); return; }
  alKalemler.push({ ad, adet, fiyat });
  document.getElementById('al-urun-ad').value = '';
  document.getElementById('al-urun-fiyat').value = '';
  document.getElementById('al-urun-adet').value = 1;
  renderAlKalemler();
}

function renderAlKalemler() {
  const el = document.getElementById('al-kalemler-list');
  if (!el) return;
  const toplam = alKalemler.reduce((a, k) => a + k.adet * k.fiyat, 0);
  document.getElementById('al-toplam').textContent = 'TL' + toplam.toFixed(0);
  if (alKalemler.length === 0) { el.innerHTML = ''; return; }
  el.innerHTML = '<div style="margin-bottom:10px">' + alKalemler.map(function(k, i) {
    return '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:6px;padding:8px 10px;margin-bottom:6px">' +
      '<div><div style="font-size:13px;font-weight:600">' + k.ad + '</div>' +
      '<div style="font-size:11px;color:#888">' + k.adet + ' adet x TL' + k.fiyat + ' = TL' + (k.adet*k.fiyat).toFixed(0) + '</div></div>' +
      '<button onclick="alKalemSil(' + i + ')" style="background:none;border:none;color:var(--accent2);font-size:18px;cursor:pointer">x</button>' +
    '</div>';
  }).join('') + '</div>';
}

function alKalemSil(i) {
  alKalemler.splice(i, 1);
  renderAlKalemler();
}

function saveSatis() {
  if (satKalemler.length === 0) { alert('En az bir urun ekleyin'); return; }
  const toplam = satKalemler.reduce((a, k) => a + k.adet * k.fiyat, 0);
  const kayit = {
    id: Date.now(),
    tur: 'satis',
    musteri: document.getElementById('sat-musteri').value.trim() || 'Anonim',
    kalemler: satKalemler.map(function(k) { return Object.assign({}, k); }),
    toplam,
    not: document.getElementById('sat-not').value.trim(),
    tarih: new Date().toISOString()
  };
  // Stoktan dus
  satKalemler.forEach(function(k) {
    if (k.stokId) {
      const s = state.stok.find(function(x) { return x.id === k.stokId; });
      if (s) s.adet = Math.max(0, s.adet - k.adet);
    }
  });
  state.satislar.push(kayit);
  saveState();
  satKalemler = [];
  document.getElementById('sat-musteri').value = '';
  document.getElementById('sat-not').value = '';
  closeModal('satis-modal');
  renderSatis();
}

function saveAlis() {
  if (alKalemler.length === 0) { alert('En az bir urun ekleyin'); return; }
  const toplam = alKalemler.reduce((a, k) => a + k.adet * k.fiyat, 0);
  const kayit = {
    id: Date.now(),
    tur: 'alis',
    tedarikci: document.getElementById('al-tedarikci').value.trim() || 'Belirsiz',
    kalemler: alKalemler.map(function(k) { return Object.assign({}, k); }),
    toplam,
    not: document.getElementById('al-not').value.trim(),
    tarih: new Date().toISOString()
  };
  // Stoka ekle (stokta varsa)
  alKalemler.forEach(function(k) {
    const s = state.stok.find(function(x) { return x.ad.toLowerCase() === k.ad.toLowerCase(); });
    if (s) s.adet += k.adet;
  });
  state.satislar.push(kayit);
  saveState();
  alKalemler = [];
  document.getElementById('al-tedarikci').value = '';
  document.getElementById('al-not').value = '';
  closeModal('alis-modal');
  renderSatis();
}

function filterSatis(f) {
  saatisFilter = f;
  document.querySelectorAll('#satis-filters .filter-btn').forEach(function(b) { b.classList.remove('active'); });
  event.target.classList.add('active');
  renderSatis();
}

function renderSatis() {
  if (!state.satislar) state.satislar = [];
  const q = (document.getElementById('satis-search') ? document.getElementById('satis-search').value : '').toLowerCase();
  let list = state.satislar.filter(function(s) {
    if (saatisFilter === 'satis' && s.tur !== 'satis') return false;
    if (saatisFilter === 'alis' && s.tur !== 'alis') return false;
    if (q && !(s.musteri||s.tedarikci||'').toLowerCase().includes(q) &&
        !s.kalemler.some(function(k) { return k.ad.toLowerCase().includes(q); })) return false;
    return true;
  }).reverse();

  const toplamSatis = state.satislar.filter(function(s) { return s.tur === 'satis'; }).reduce(function(a, s) { return a + s.toplam; }, 0);
  const toplamAlis = state.satislar.filter(function(s) { return s.tur === 'alis'; }).reduce(function(a, s) { return a + s.toplam; }, 0);

  document.getElementById('satis-stats').innerHTML =
    '<div class="stat-card"><div class="stat-value profit-positive" style="font-size:20px">TL' + toplamSatis.toFixed(0) + '</div><div class="stat-label">Toplam Satis</div></div>' +
    '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">TL' + toplamAlis.toFixed(0) + '</div><div class="stat-label">Toplam Alis</div></div>';

  if (list.length === 0) {
    document.getElementById('satis-list').innerHTML = '<div class="empty"><div class="empty-icon">🛒</div><div>Kayit bulunamadi</div></div>';
    return;
  }

  document.getElementById('satis-list').innerHTML = list.map(function(s) {
    const baslik = s.tur === 'satis' ? (s.musteri || 'Anonim') : (s.tedarikci || 'Belirsiz');
    const kalemOzet = s.kalemler.map(function(k) { return k.ad + ' x' + k.adet; }).join(', ');
    const renk = s.tur === 'satis' ? 'var(--green)' : 'var(--accent2)';
    const etiket = s.tur === 'satis' ? 'SATIS' : 'ALIS';
    return '<div class="list-item">' +
      '<div class="list-item-top">' +
        '<div>' +
          '<div class="list-item-title">' + baslik + '</div>' +
          '<div class="list-item-sub">' + kalemOzet + '</div>' +
          '<div class="list-item-sub" style="margin-top:2px">' + new Date(s.tarih).toLocaleDateString("tr-TR") + (s.not ? ' • ' + s.not : '') + '</div>' +
        '</div>' +
        '<div style="text-align:right">' +
          '<div style="font-weight:700;font-size:16px;color:' + renk + '">TL' + s.toplam.toFixed(0) + '</div>' +
          '<span class="badge" style="background:' + renk + '22;color:' + renk + ';border:1px solid ' + renk + '44">' + etiket + '</span>' +
        '</div>' +
      '</div>' +
      '<div class="list-item-actions">' +
        '<button class="btn btn-danger btn-sm" onclick="deleteSatis(' + s.id + ')">🗑</button>' +
      '</div>' +
    '</div>';
  }).join('');
}

function deleteSatis(id) {
  if (!confirm('Bu kaydi silmek istediginize emin misiniz?')) return;
  state.satislar = state.satislar.filter(function(s) { return s.id !== id; });
  saveState();
  renderSatis();
}

// --- INIT ---
loadState();
// Firebase hazır olunca veriyi çek
function initFirebase() {
  if (!window._firebaseReady) {
    setTimeout(initFirebase, 300);
    return;
  }
  firebaseLoad().then(function(yuklendi) {
    if (yuklendi) {
      renderDashboard();
      console.log('Veri Firebase dan yuklendi');
    }
    firebaseGercekZamanli();
  });
}
initFirebase();

// Varsayılan stok verilerini yükle (sadece stok boşsa)
if (state.stok.length === 0) {
  state.stok = [{"id": 1, "ad": "40N120 Mosfet", "adet": 29, "maliyet": 85.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 2, "ad": "4V 4 AH Kuru Akü", "adet": 0, "maliyet": 200.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 3, "ad": "Stanley 160A Kaynak Makinesi", "adet": 1, "maliyet": 7500.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 4, "ad": "Taşınabilir Aydınlatma", "adet": 2, "maliyet": 2000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 5, "ad": "60T65PES İGBT", "adet": 118, "maliyet": 105.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 6, "ad": "Batarya Kapasite Voltaj Göstergesi", "adet": 0, "maliyet": 385.66, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 7, "ad": "18V Büyük Matkap Motoru", "adet": 3, "maliyet": 700.0, "min": 6, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 8, "ad": "10-25 Priz (Dişi) Jak", "adet": 15, "maliyet": 52.89, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 9, "ad": "Marxlow 24V 90*90*25 Fan", "adet": 4, "maliyet": 100.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 10, "ad": "FZT851TA", "adet": 20, "maliyet": 19.5, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 11, "ad": "0.8 L25 Meme", "adet": 23, "maliyet": 25.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 12, "ad": "203CNQ100 Çıkış Diyotu", "adet": 1, "maliyet": 1402.42, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 13, "ad": "4 metre AK15 Torç", "adet": 1, "maliyet": 1500.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 14, "ad": "GBJ5010 50A 1000V Köprü Dİyot", "adet": 17, "maliyet": 42.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 15, "ad": "SKBPC5016 380V Köprü Diyot", "adet": 5, "maliyet": 200.0, "min": 8, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 16, "ad": "60N100 Mosfet", "adet": 18, "maliyet": 359.04, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 17, "ad": "820MF 400V Kondansatör", "adet": 0, "maliyet": 100.49, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 18, "ad": "Eurofix Yapıştırıcı", "adet": 32, "maliyet": 60.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 19, "ad": "Tunçmatik 5mh80 5kw 80A", "adet": 1, "maliyet": 25000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 20, "ad": "10-25 Fiş (Erkek) Jak", "adet": 7, "maliyet": 49.28, "min": 10, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 21, "ad": "3S Üçgen BMS", "adet": 10, "maliyet": 75.0, "min": 13, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 22, "ad": "1.0 L30 Zirkonyum Meme", "adet": 0, "maliyet": 35.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 23, "ad": "BT151", "adet": 225, "maliyet": 15.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 24, "ad": "Daly 13S 40A BMS", "adet": 0, "maliyet": 1105.27, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 25, "ad": "TR36 Deveboynu", "adet": 9, "maliyet": 350.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 26, "ad": "Class 12V 90*90*25 Fan", "adet": 2, "maliyet": 100.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 27, "ad": "35-70 Fiş (Erkek) Jak", "adet": 2, "maliyet": 85.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 28, "ad": "POWERMASTER 120X120X38 220V Fan", "adet": 0, "maliyet": 175.44, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 29, "ad": "680MF 450V Kondansatör", "adet": 4, "maliyet": 226.8, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 30, "ad": "Mexsun 1000W", "adet": 1, "maliyet": 5000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 31, "ad": "TR25 Meme Tutucu", "adet": 92, "maliyet": 11.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 32, "ad": "80N60 Mosfet", "adet": 0, "maliyet": 75.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 33, "ad": "12V 9AH Akü", "adet": 0, "maliyet": 780.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 34, "ad": "TR36 Yolluk", "adet": 10, "maliyet": 350.0, "min": 13, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 35, "ad": "TR15 Nozul", "adet": 91, "maliyet": 51.6, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 36, "ad": "KDV", "adet": 100, "maliyet": 0.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 37, "ad": "Potansiyometre", "adet": 3, "maliyet": 50.0, "min": 6, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 38, "ad": "CMC Tools Kaynak Pensesi 800A", "adet": 1, "maliyet": 100.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 39, "ad": "DMAX PZ2/S2 Matkap ucu", "adet": 8, "maliyet": 40.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 40, "ad": "Tunçmatik 1P50 1kw", "adet": 1, "maliyet": 9000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 41, "ad": "Torç Kabzası", "adet": 0, "maliyet": 80.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 42, "ad": "TR25 Nozul", "adet": 53, "maliyet": 68.25, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 43, "ad": "İşçilik (Matkap ve Batarya)", "adet": 945, "maliyet": 0.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 44, "ad": "FESF16JT - 16A. 600V . Ultrafast DİYOT Kategori", "adet": 8, "maliyet": 55.44, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 45, "ad": "FGW50N65WE (50n65 Mosfet)", "adet": 42, "maliyet": 90.5, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 46, "ad": "FGW60N65WE (60N65 Mosfet)", "adet": 0, "maliyet": 101.17, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 47, "ad": "TC4420", "adet": 8, "maliyet": 105.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 48, "ad": "Presleme Yüzük", "adet": 11, "maliyet": 20.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 49, "ad": "CMC Tools Kaynak Pensesi 300A", "adet": 8, "maliyet": 100.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 50, "ad": "Orion 2600 Mah Li-İon Pil", "adet": 124, "maliyet": 50.93, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 51, "ad": "İşçilik (Kaynak Makinesi)", "adet": 7659, "maliyet": 0.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 52, "ad": "40N60 80A600V Mosfet", "adet": 50, "maliyet": 264.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 53, "ad": "12V 2,5A Adaptör", "adet": 2, "maliyet": 120.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 54, "ad": "IXGH48N60C3D1 Mosfet", "adet": 40, "maliyet": 252.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 55, "ad": "Maximum Kaynak Makinesi", "adet": 2, "maliyet": 3500.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 56, "ad": "Marxlow 12V 90*90*25 Fan", "adet": 1, "maliyet": 100.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 57, "ad": "470MF 400V Kondansatör", "adet": 31, "maliyet": 300.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 58, "ad": "Mexxsun 2000W", "adet": 1, "maliyet": 11000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 59, "ad": "Marxlow 24V 120*120*25 Fan", "adet": 5, "maliyet": 200.0, "min": 8, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 60, "ad": "5S 100A BMS", "adet": 28, "maliyet": 160.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 61, "ad": "Ara Rekor", "adet": 77, "maliyet": 20.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 62, "ad": "Orion 21700 5000 Mah Li-İon Pil", "adet": 0, "maliyet": 127.34, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 63, "ad": "12 Volt Matkap Motoru", "adet": 4, "maliyet": 200.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 64, "ad": "16S 40A BMS", "adet": 1, "maliyet": 1000.14, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 65, "ad": "TR36 Nozul", "adet": 9, "maliyet": 125.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 66, "ad": "WPEC Darbeli Matkap", "adet": 1, "maliyet": 3600.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 67, "ad": "Gaz Dağıtıcı", "adet": 9, "maliyet": 20.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 68, "ad": "Anahtar 30A", "adet": 25, "maliyet": 25.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 69, "ad": "Marxlow 220V 120*120*38 Fan", "adet": 2, "maliyet": 196.56, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 70, "ad": "Class 220V 120*120*38 Fan", "adet": 1, "maliyet": 200.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 71, "ad": "Mervesan Trafo", "adet": 2, "maliyet": 400.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 72, "ad": "STTH12R06D Diyot", "adet": 10, "maliyet": 80.64, "min": 13, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 73, "ad": "Orion 3.2V 100AH LiFepo4", "adet": 8, "maliyet": 1733.19, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 74, "ad": "TRWELD Kaynak Makinesi Pastası", "adet": 8, "maliyet": 100.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 75, "ad": "MMPT", "adet": 0, "maliyet": 2300.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 76, "ad": "35-70 Priz (Dişi) Jak", "adet": 11, "maliyet": 101.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 77, "ad": "PowerXtra 1.2 V NiCd 1500 Mah", "adet": 3, "maliyet": 50.0, "min": 6, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 78, "ad": "Torç Tetik", "adet": 48, "maliyet": 30.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 79, "ad": "10,8 Volt Matkap Motoru", "adet": 1, "maliyet": 250.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 80, "ad": "Orion 3200 mAh Li-on Pil", "adet": 0, "maliyet": 106.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 81, "ad": "L4981BD SMD Entegre", "adet": 2, "maliyet": 235.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 82, "ad": "POWERMASTER 120X120X25 24V Fan", "adet": 0, "maliyet": 71.49, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 83, "ad": "TR15 Yaylı Meme Tutucu", "adet": 80, "maliyet": 35.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 84, "ad": "60UP200N Mosfet", "adet": 8, "maliyet": 250.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 85, "ad": "Orion 2200 mAh Li-on Pil", "adet": 0, "maliyet": 55.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 86, "ad": "Earth Clamp Kaynak Şasesi", "adet": 5, "maliyet": 100.0, "min": 8, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 87, "ad": "220V Fiş", "adet": 4, "maliyet": 35.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 88, "ad": "Orion 1500 mAh Li-on Pil", "adet": 304, "maliyet": 51.77, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 89, "ad": "4 metre AK25 Torç", "adet": 1, "maliyet": 1600.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 90, "ad": "Bosch Tetik", "adet": 0, "maliyet": 400.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 91, "ad": "Power-Xtra 1.2V 2000Mah 10C Pil", "adet": 50, "maliyet": 58.45, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 92, "ad": "4*2.5 Kablo", "adet": 4, "maliyet": 60.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 93, "ad": "Titex Kesme Taşı", "adet": 253, "maliyet": 10.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 94, "ad": "Marxlow 12V 120*120*25 Fan", "adet": 1, "maliyet": 200.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 95, "ad": "Tunçmatik 5P50 5kw", "adet": 1, "maliyet": 15000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 96, "ad": "Mervesan 12.6V 3S Şarj Aleti", "adet": 7, "maliyet": 210.0, "min": 10, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 97, "ad": "Bosch kömür", "adet": 1, "maliyet": 160.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 98, "ad": "Orion 2000 mAh Li-on Pil", "adet": 458, "maliyet": 57.61, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 99, "ad": "Şarjlı Matkap", "adet": 12, "maliyet": 750.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 100, "ad": "50T65FD1 İGBT", "adet": 2, "maliyet": 105.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 101, "ad": "1,2 L30 Meme", "adet": 9, "maliyet": 30.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 102, "ad": "Class 12V 1A Şarj Aleti", "adet": 0, "maliyet": 120.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 103, "ad": "Daly 13S 60A BMS", "adet": 0, "maliyet": 1487.86, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 104, "ad": "1.0 Meme", "adet": 18, "maliyet": 30.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 105, "ad": "Magmaweld Monostick 200İ", "adet": 0, "maliyet": 5350.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 106, "ad": "403CNQ040 Çıkış Diyotu", "adet": 1, "maliyet": 1495.7, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 107, "ad": "Stanley Tetik", "adet": 1, "maliyet": 1000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 108, "ad": "Solinved 12V 2000W", "adet": 1, "maliyet": 10000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 109, "ad": "Daly 8S 25.6V 60A LifePo4 BMS", "adet": 2, "maliyet": 1161.17, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 110, "ad": "3,5 metre AK15 Torç", "adet": 2, "maliyet": 1350.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 111, "ad": "TR36 Meme Tutucu", "adet": 4, "maliyet": 25.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 112, "ad": "LM2575HVS", "adet": 2, "maliyet": 265.95, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 113, "ad": "Stanley Motor", "adet": 0, "maliyet": 2500.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 114, "ad": "PowerXtra yassı Pil", "adet": 0, "maliyet": 300.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 115, "ad": "Orion 1.2V 4/5 NiCd", "adet": 2, "maliyet": 60.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 116, "ad": "75G65 Mosfet", "adet": 70, "maliyet": 200.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 117, "ad": "Matkap Tetik", "adet": 0, "maliyet": 250.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 118, "ad": "18 Volt Matkap Motoru", "adet": 0, "maliyet": 200.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 119, "ad": "3,5 metre Yolluk", "adet": 8, "maliyet": 150.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 120, "ad": "Power-Xtra 1.2V 1000Mah Ni-Cd Pil", "adet": 46, "maliyet": 31.5, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 121, "ad": "EVE 18650 3200 Mah Pil", "adet": 162, "maliyet": 103.49, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 122, "ad": "Titex Bits Ucu", "adet": 55, "maliyet": 25.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 123, "ad": "4,5 metre Yolluk", "adet": 9, "maliyet": 150.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 124, "ad": "SD6834", "adet": 0, "maliyet": 22.81, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 125, "ad": "BYC75W-1200PQ Çıkış Diyotu", "adet": 1, "maliyet": 214.33, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 126, "ad": "TR25 Deveboynu", "adet": 9, "maliyet": 300.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 127, "ad": "Mervesan 21V 5S Şarj Aleti", "adet": 14, "maliyet": 260.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 128, "ad": "KL Pro MMA200A Kaynak Makinesi", "adet": 1, "maliyet": 11000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 129, "ad": "Dyson BMS", "adet": 0, "maliyet": 1500.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 130, "ad": "75N60 İGBT", "adet": 0, "maliyet": 170.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 131, "ad": "HELL STELL Bits", "adet": 29, "maliyet": 70.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 132, "ad": "Assur Şarjlı Matkap Kartı", "adet": 1, "maliyet": 750.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 133, "ad": "Mervesan 16.8V 4S Şarj Aleti", "adet": 4, "maliyet": 220.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 134, "ad": "Tenpower 21700 3.7V Li-İon Pil", "adet": 10, "maliyet": 181.96, "min": 13, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 135, "ad": "0.8 Tombul Meme", "adet": 12, "maliyet": 20.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 136, "ad": "1S BMS", "adet": 4, "maliyet": 30.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z"}, {"id": 137, "ad": "3S 60 A BMS", "adet": 0, "maliyet": 150.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z"}];
  saveState();
}

renderDashboard();
setInterval(renderDriveBar, 2000); renderDriveBar();
</script>


<!-- STOK DÜZENLEME MODAL -->
<div class="modal-overlay" id="stok-edit-modal">
  <div class="modal">
    <div class="modal-title">STOK DÜZENLE <button class="close-btn" onclick="closeModal('stok-edit-modal')">✕</button></div>
    <div class="form-group">
      <label>Parça / Malzeme Adı</label>
      <input type="text" id="ste-ad">
    </div>
    <div class="row">
      <div class="form-group">
        <label>Adet</label>
        <input type="number" id="ste-adet" min="0">
      </div>
      <div class="form-group">
        <label>Birim Maliyet (₺)</label>
        <input type="number" id="ste-maliyet" min="0">
      </div>
    </div>
    <div class="form-group">
      <label>Min. Stok Uyarısı</label>
      <input type="number" id="ste-min" min="0">
    </div>
    <input type="hidden" id="ste-id">
    <button class="btn btn-primary" onclick="updateStok()">💾 Güncelle</button>
  </div>
</div>

<!-- FATURA MODAL -->
<div class="modal-overlay" id="fatura-modal">
  <div class="modal">
    <div class="modal-title">🧾 FİŞ / FATURA <button class="close-btn" onclick="closeModal('fatura-modal')">✕</button></div>
    <div id="fatura-content" style="background:#fff;color:#111;border-radius:8px;padding:18px;font-family:monospace;font-size:13px;line-height:1.8"></div>
    <div style="display:flex;gap:8px;margin-top:12px">
      <button class="btn btn-whatsapp" style="flex:1;justify-content:center" onclick="faturayiWAGonder()">📲 WhatsApp'a Gönder</button>
      <button class="btn btn-ghost btn-sm" onclick="closeModal('fatura-modal')">Kapat</button>
    </div>
  </div>
</div>

</body>
</html>
