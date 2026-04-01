[servis-takip4.html](https://github.com/user-attachments/files/26403587/servis-takip4.html)
<!DOCTYPE html>
<html lang="tr">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
    <title>Servis Takip</title>
    <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=IBM+Plex+Sans:wght@400;500;600&display=swap"
        rel="stylesheet">
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

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background: var(--bg);
            color: var(--text);
            font-family: 'IBM Plex Sans', sans-serif;
            min-height: 100vh;
        }

        /* NAV */
        .nav {
            background: var(--surface);
            border-bottom: 2px solid var(--accent);
            padding: 0;
            display: flex;
            position: sticky;
            top: 0;
            z-index: 100;
            overflow-x: auto;
        }

        .nav button {
            flex: 1;
            min-width: 60px;
            padding: 14px 8px 10px;
            background: none;
            border: none;
            color: var(--muted);
            font-family: 'Bebas Neue', sans-serif;
            font-size: 15px;
            letter-spacing: 1px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all .2s;
            white-space: nowrap;
        }

        .nav button.active {
            color: var(--accent);
            border-bottom-color: var(--accent);
        }

        .sub-btn {
            flex: 1;
            padding: 10px 8px;
            background: none;
            border: none;
            color: var(--muted);
            font-family: 'Bebas Neue', sans-serif;
            font-size: 14px;
            letter-spacing: 1px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all .2s;
            white-space: nowrap;
        }

        .sub-btn.active {
            color: var(--accent);
            border-bottom-color: var(--accent);
        }

        /* PAGES */
        .page {
            display: none;
            padding: 16px;
            max-width: 600px;
            margin: 0 auto;
        }

        .page.active {
            display: block;
        }

        /* CARDS */
        .card {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 16px;
            margin-bottom: 12px;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        h2 {
            font-family: 'Bebas Neue';
            font-size: 22px;
            letter-spacing: 1px;
            color: var(--accent);
        }

        h3 {
            font-size: 14px;
            font-weight: 600;
            color: var(--text);
        }

        /* FORM */
        .form-group {
            margin-bottom: 12px;
        }

        label {
            display: block;
            font-size: 11px;
            color: var(--muted);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 4px;
        }

        input,
        select,
        textarea {
            width: 100%;
            background: var(--surface2);
            border: 1px solid var(--border);
            border-radius: 6px;
            padding: 10px 12px;
            color: var(--text);
            font-family: 'IBM Plex Sans', sans-serif;
            font-size: 14px;
            outline: none;
            transition: border .2s;
        }

        input:focus,
        select:focus,
        textarea:focus {
            border-color: var(--accent);
        }

        textarea {
            resize: vertical;
            min-height: 70px;
        }

        select option {
            background: var(--surface2);
        }

        /* BUTTONS */
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 10px 16px;
            border-radius: 6px;
            border: none;
            font-family: 'IBM Plex Sans', sans-serif;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all .2s;
        }

        .btn-primary {
            background: var(--accent);
            color: #000;
            width: 100%;
            justify-content: center;
            padding: 12px;
        }

        .btn-primary:hover {
            background: #f59e0b;
            opacity: .9;
        }

        .btn-sm {
            padding: 6px 10px;
            font-size: 12px;
        }

        .btn-danger {
            background: var(--accent2);
            color: #fff;
        }

        .btn-success {
            background: var(--green);
            color: #000;
        }

        .btn-ghost {
            background: var(--surface2);
            color: var(--text);
            border: 1px solid var(--border);
        }

        .btn-whatsapp {
            background: #25D366;
            color: #fff;
        }

        /* BADGES */
        .badge {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        .badge-bekliyor {
            background: #f59e0b22;
            color: var(--accent);
            border: 1px solid #f59e0b44;
        }

        .badge-tamirde {
            background: #3b82f622;
            color: #60a5fa;
            border: 1px solid #3b82f644;
        }

        .badge-hazir {
            background: #22c55e22;
            color: var(--green);
            border: 1px solid #22c55e44;
        }

        .badge-teslim {
            background: #88888822;
            color: var(--muted);
            border: 1px solid #88888844;
        }

        .badge-borc {
            background: #ef444422;
            color: var(--accent2);
            border: 1px solid #ef444444;
        }

        .badge-alacak {
            background: #22c55e22;
            color: var(--green);
            border: 1px solid #22c55e44;
        }

        /* LIST ITEMS */
        .list-item {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 14px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: border-color .2s;
        }

        .list-item:hover {
            border-color: var(--accent);
        }

        .list-item-top {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 6px;
        }

        .list-item-title {
            font-weight: 600;
            font-size: 15px;
        }

        .list-item-sub {
            font-size: 12px;
            color: var(--muted);
            margin-top: 2px;
        }

        .list-item-actions {
            display: flex;
            gap: 6px;
            margin-top: 10px;
            flex-wrap: wrap;
        }

        /* STATS */
        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 16px;
        }

        .stat-card {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 14px;
            text-align: center;
        }

        .stat-value {
            font-family: 'Bebas Neue';
            font-size: 28px;
            color: var(--accent);
        }

        .stat-label {
            font-size: 11px;
            color: var(--muted);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 2px;
        }

        /* MODAL */
        .modal-overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: #000000cc;
            z-index: 200;
            padding: 16px;
            overflow-y: auto;
        }

        .modal-overlay.active {
            display: flex;
            align-items: flex-start;
            justify-content: center;
            padding-top: 40px;
        }

        .modal {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 20px;
            width: 100%;
            max-width: 500px;
        }

        .modal-title {
            font-family: 'Bebas Neue';
            font-size: 20px;
            color: var(--accent);
            margin-bottom: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .close-btn {
            background: none;
            border: none;
            color: var(--muted);
            font-size: 22px;
            cursor: pointer;
            line-height: 1;
        }

        /* SEARCH */
        .search-bar {
            position: relative;
            margin-bottom: 14px;
        }

        .search-bar input {
            padding-left: 36px;
        }

        .search-icon {
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--muted);
            font-size: 14px;
        }

        /* DIVIDER */
        .divider {
            border: none;
            border-top: 1px solid var(--border);
            margin: 14px 0;
        }

        /* EMPTY STATE */
        .empty {
            text-align: center;
            padding: 40px 20px;
            color: var(--muted);
        }

        .empty-icon {
            font-size: 40px;
            margin-bottom: 10px;
        }

        /* FILTER ROW */
        .filter-row {
            display: flex;
            gap: 6px;
            overflow-x: auto;
            margin-bottom: 14px;
            padding-bottom: 4px;
        }

        .filter-btn {
            flex-shrink: 0;
            padding: 6px 12px;
            border-radius: 20px;
            border: 1px solid var(--border);
            background: var(--surface2);
            color: var(--muted);
            font-size: 12px;
            cursor: pointer;
            transition: all .2s;
        }

        .filter-btn.active {
            background: var(--accent);
            color: #000;
            border-color: var(--accent);
            font-weight: 600;
        }

        .row {
            display: flex;
            gap: 10px;
        }

        .row .form-group {
            flex: 1;
        }

        /* BOTTOM SPACING */
        .pb {
            padding-bottom: 30px;
        }

        /* PROFIT INDICATOR */
        .profit-positive {
            color: var(--green);
        }

        .profit-negative {
            color: var(--accent2);
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
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
    <div id="finans-submenu"
        style="display:none;background:var(--surface2);border-bottom:2px solid var(--accent);padding:0;overflow-x:auto">
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
            <div class="modal-title">GİDER EKLE <button class="close-btn" onclick="closeModal('gider-modal')">✕</button>
            </div>
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
            <div style="display:flex;gap:6px">
                <button class="btn btn-ghost btn-sm" onclick="openModal('kasa-yonet-modal')">⚙️ Kasalar</button>
                <button class="btn btn-ghost btn-sm" onclick="openModal('transfer-modal')">🔄 Transfer</button>
                <button class="btn btn-primary btn-sm" onclick="openModal('kasa-modal')">+ Hareket</button>
            </div>
        </div>
        <div id="kasa-bakiye-card" style="margin-bottom:12px"></div>
        <div class="filter-row" id="kasa-filters">
            <button class="filter-btn active" onclick="filterKasa('hepsi')">Hepsi</button>
            <button class="filter-btn" onclick="filterKasa('giris')">⬆️ Giriş</button>
            <button class="filter-btn" onclick="filterKasa('cikis')">⬇️ Çıkış</button>
            <button class="filter-btn" onclick="filterKasa('transfer')">🔄 Transfer</button>
        </div>
        <div id="kasa-gunluk" style="margin-bottom:12px"></div>
        <div id="kasa-list"></div>
    </div>

    <!-- KASA MODAL -->
    <div class="modal-overlay" id="kasa-modal">
        <div class="modal">
            <div class="modal-title">KASA HAREKETİ <button class="close-btn"
                    onclick="closeModal('kasa-modal')">✕</button></div>
            <div class="form-group">
                <label>Kasa</label>
                <select id="k-kasa-id"></select>
            </div>
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
                    <label>Not</label>
                    <input type="text" id="k-not" placeholder="İsteğe bağlı...">
                </div>
            </div>
            <button class="btn btn-primary" onclick="saveKasa()">💾 Kaydet</button>
        </div>
    </div>

    <!-- KASA YÖNET MODAL -->
    <div class="modal-overlay" id="kasa-yonet-modal">
        <div class="modal">
            <div class="modal-title">KASALARI YÖNET <button class="close-btn"
                    onclick="closeModal('kasa-yonet-modal')">✕</button></div>
            <div id="kasa-yonet-list" style="margin-bottom:14px"></div>
            <hr class="divider">
            <div style="font-size:13px;font-weight:600;margin-bottom:10px;color:var(--accent)">Yeni Kasa Ekle</div>
            <div class="row">
                <div class="form-group">
                    <label>Kasa Adı</label>
                    <input type="text" id="yeni-kasa-ad" placeholder="Nakit, Banka, Pos...">
                </div>
                <div class="form-group">
                    <label>Başlangıç Bakiyesi (₺)</label>
                    <input type="number" id="yeni-kasa-bakiye" placeholder="0">
                </div>
            </div>
            <button class="btn btn-primary" onclick="kasaEkle()">+ Kasa Ekle</button>
        </div>
    </div>

    <!-- TRANSFER MODAL -->
    <div class="modal-overlay" id="transfer-modal">
        <div class="modal">
            <div class="modal-title">KASALAR ARASI TRANSFERi <button class="close-btn"
                    onclick="closeModal('transfer-modal')">✕</button></div>
            <div class="form-group">
                <label>Çıkış Kasası</label>
                <select id="tr-cikis"></select>
            </div>
            <div class="form-group">
                <label>Giriş Kasası</label>
                <select id="tr-giris"></select>
            </div>
            <div class="form-group">
                <label>Tutar (₺)</label>
                <input type="number" id="tr-tutar" placeholder="0">
            </div>
            <div class="form-group">
                <label>Not</label>
                <input type="text" id="tr-not" placeholder="İsteğe bağlı...">
            </div>
            <button class="btn btn-primary" onclick="saveTransfer()">🔄 Transfer Et</button>
        </div>
    </div>

    <!-- KASA SEÇ MODAL (Satış/Servis için) -->
    <div class="modal-overlay" id="kasa-sec-modal">
        <div class="modal">
            <div class="modal-title">HANGİ KASAYA? <button class="close-btn"
                    onclick="closeModal('kasa-sec-modal')">✕</button></div>
            <div style="font-size:13px;color:var(--muted);margin-bottom:12px" id="kasa-sec-aciklama"></div>
            <div class="form-group">
                <label>Kasa Seç</label>
                <select id="kasa-sec-id"></select>
            </div>
            <button class="btn btn-primary" onclick="kasaSecOnayla()">✅ Onayla</button>
        </div>
    </div>

    <!-- ÖDEME MODAL -->
    <div class="modal-overlay" id="odeme-modal">
        <div class="modal">
            <div class="modal-title">💳 ÖDEME AL <button class="close-btn"
                    onclick="closeModal('odeme-modal')">✕</button></div>
            <div id="odeme-servis-bilgi"
                style="background:var(--surface2);border-radius:8px;padding:10px;margin-bottom:14px;font-size:13px;color:var(--muted)">
            </div>
            <div style="font-size:13px;font-weight:600;margin-bottom:10px">Toplam: <span id="odeme-toplam"
                    style="color:var(--accent);font-family:'Bebas Neue';font-size:20px"></span></div>

            <div id="odeme-kalemler" style="margin-bottom:12px"></div>

            <div style="background:var(--surface2);border-radius:8px;padding:12px;margin-bottom:12px">
                <div
                    style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">
                    Ödeme Ekle</div>
                <div class="row">
                    <div class="form-group">
                        <label>Yöntem</label>
                        <select id="op-yontem" onchange="odemeYontemDegis()">
                            <option value="nakit">💵 Nakit</option>
                            <option value="kredi">💳 Kredi Kartı</option>
                            <option value="havale">🏧 Havale/EFT</option>
                            <option value="veresiye">📋 Veresiye (Cariye Yaz)</option>
                            <option value="ucretsiz">🎁 Ücretsiz</option>
                        </select>
                    </div>
                    <div class="form-group" id="op-tutar-group">
                        <label>Tutar (₺)</label>
                        <input type="number" id="op-tutar" placeholder="0">
                    </div>
                </div>
                <div class="form-group" id="op-kasa-group">
                    <label>Kasa</label>
                    <select id="op-kasa-id"></select>
                </div>
                <button class="btn btn-ghost btn-sm" onclick="odemeKalemEkle()" style="width:100%">+ Ekle</button>
            </div>

            <div
                style="display:flex;justify-content:space-between;align-items:center;padding:10px;background:var(--surface2);border-radius:8px;margin-bottom:12px">
                <span style="font-size:13px;color:var(--muted)">Kalan</span>
                <span id="odeme-kalan" style="font-family:'Bebas Neue';font-size:22px;color:var(--accent2)">₺0</span>
            </div>

            <button class="btn btn-primary" onclick="odemeKaydet()">💾 Ödemeyi Tamamla</button>
        </div>
    </div>


    <!-- AYARLAR SAYFASI -->
    <div id="page-ayarlar" class="page pb">
        <div style="padding:16px 0 8px;">
            <div style="font-family:'Bebas Neue';font-size:24px;letter-spacing:2px;color:var(--accent)">⚙️ Ayarlar</div>
        </div>
        <div class="card">
            <div class="card-header">
                <h2>İşletme Bilgileri</h2>
            </div>
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
            <div class="card-header">
                <h2>Bildirim</h2>
            </div>
            <div style="display:flex;justify-content:space-between;align-items:center">
                <div>
                    <div style="font-size:14px;font-weight:600">Bekleyen servis uyarısı</div>
                    <div style="font-size:12px;color:var(--muted)">3+ gün bekleyen servisler için uyarı göster</div>
                </div>
                <label style="position:relative;display:inline-block;width:44px;height:24px">
                    <input type="checkbox" id="ay-uyari" style="opacity:0;width:0;height:0" onchange="saveAyarlar()">
                    <span id="ay-uyari-span"
                        style="position:absolute;cursor:pointer;inset:0;background:var(--border);border-radius:24px;transition:.3s"></span>
                </label>
            </div>
        </div>
        <div class="card" style="margin-top:12px">
            <div class="card-header">
                <h2>Veri Yönetimi & Yedekleme</h2>
            </div>
            <div style="display:flex;flex-direction:column;gap:12px;">
                <button class="btn btn-ghost" onclick="yedekIndir()" style="width:100%">📥 Tüm Verileri Yedekle
                    (Cihazınıza İndir)</button>
                <div style="border:1px dashed var(--border);padding:14px;border-radius:8px;text-align:center;">
                    <div style="font-size:13px;color:var(--muted);margin-bottom:10px">Elinizdeki JSON yedeğini sisteme
                        yükleyin</div>
                    <input type="file" id="yedek-dosya" accept=".json" style="display:none"
                        onchange="yedekYukle(event)">
                    <button class="btn btn-primary" onclick="document.getElementById('yedek-dosya').click()"
                        style="width:100%">🔗 Yedeği Yükle (JSON)</button>
                    <div id="yedek-yukle-durum" style="font-size:12px;margin-top:8px"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- GRAFİK SAYFASI -->
    <div id="page-grafik" class="page pb">
        <div style="padding:16px 0 8px;">
            <div style="font-family:'Bebas Neue';font-size:24px;letter-spacing:2px;color:var(--accent)">📈 Aylık Kar /
                Zarar</div>
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
            <div class="modal-title">YENİ SATIŞ <button class="close-btn" onclick="closeModal('satis-modal')">✕</button>
            </div>
            <div class="form-group">
                <label>Müşteri Adı</label>
                <input type="text" id="sat-musteri" placeholder="Ad Soyad (isteğe bağlı)" oninput="musteriOneri('sat')">
                <div id="sat-musteri-oneri"
                    style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto">
                </div>
            </div>
            <div id="sat-kalemler-list"></div>
            <div style="background:var(--surface2);border-radius:8px;padding:12px;margin-bottom:12px;">
                <div
                    style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">
                    Ürün Ekle</div>
                <div style="display:flex;gap:6px;margin-bottom:6px">
                    <select id="sat-stok-sec" style="flex:1" onchange="satStokSec()">
                        <option value="">Stoktan seç...</option>
                    </select>
                </div>
                <div style="display:flex;gap:6px">
                    <input type="text" id="sat-urun-ad" placeholder="Ürün adı" style="flex:2">
                    <input type="number" id="sat-urun-adet" placeholder="Adet" style="width:60px" value="1" min="1">
                    <input type="number" id="sat-urun-fiyat" placeholder="₺ Fiyat" style="width:80px">
                    <button class="btn btn-ghost btn-sm" onclick="satKalemEkle()" style="white-space:nowrap">+
                        Ekle</button>
                </div>
            </div>
            <div
                style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;padding:10px;background:var(--surface2);border-radius:8px">
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
            <div class="modal-title">YENİ ALIŞ <button class="close-btn" onclick="closeModal('alis-modal')">✕</button>
            </div>
            <div class="form-group">
                <label>Tedarikçi</label>
                <input type="text" id="al-tedarikci" placeholder="Firma / kişi adı" oninput="musteriOneri('al')">
                <div id="al-tedarikci-oneri"
                    style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto">
                </div>
            </div>
            <div id="al-kalemler-list"></div>
            <div style="background:var(--surface2);border-radius:8px;padding:12px;margin-bottom:12px;">
                <div
                    style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">
                    Ürün Ekle</div>
                <div style="margin-bottom:6px">
                    <input type="text" id="al-stok-ara" placeholder="Stoktan ara (isteğe bağlı)..." style="width:100%"
                        oninput="alStokAra()" autocomplete="off">
                    <div id="al-stok-oneri"
                        style="display:none;background:var(--surface);border:1px solid var(--border);border-radius:6px;max-height:130px;overflow-y:auto;margin-top:2px">
                    </div>
                </div>
                <div style="display:flex;gap:6px">
                    <input type="text" id="al-urun-ad" placeholder="Ürün adı" style="flex:2">
                    <input type="number" id="al-urun-adet" placeholder="Adet" style="width:60px" value="1" min="1">
                    <input type="number" id="al-urun-fiyat" placeholder="₺ Fiyat" style="width:80px">
                    <button class="btn btn-ghost btn-sm" onclick="alKalemEkle()" style="white-space:nowrap">+
                        Ekle</button>
                </div>
            </div>
            <div
                style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;padding:10px;background:var(--surface2);border-radius:8px">
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
        <div id="yedek-uyari" style="display:none"></div>
        <div id="drive-bar" style="margin-bottom:12px"></div>
        <div id="bekleyen-uyari" style="margin-bottom:12px"></div>
        <div class="stats-grid" id="stats-grid"></div>
        <div class="card" style="margin-bottom:12px">
            <div class="card-header">
                <h2>Bu Ay</h2>
            </div>
            <div id="bu-ay-ozet"></div>
        </div>
        <div class="card">
            <div class="card-header">
                <h2>Son İşlemler</h2>
            </div>
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
        <div id="cari-ozet-kartlar" style="margin-bottom:14px"></div>
        <div class="search-bar">
            <span class="search-icon">🔍</span>
            <input type="text" placeholder="İsim ara..." oninput="renderCari()" id="cari-search">
        </div>
        <div class="filter-row">
            <button class="filter-btn active" onclick="filterCari('hepsi')">Hepsi</button>
            <button class="filter-btn" onclick="filterCari('alacak')">📥 Alacaklılar</button>
            <button class="filter-btn" onclick="filterCari('borc')">📤 Borçlular</button>
            <button class="filter-btn" onclick="filterCari('kapali')">✅ Kapandı</button>
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
        <div class="stats-grid" id="musteri-stats"></div>
        <div class="search-bar">
            <span class="search-icon">🔍</span>
            <input type="text" placeholder="Müşteri ara..." oninput="renderMusteriler()" id="musteri-search">
        </div>
        <div class="filter-row">
            <button class="filter-btn active" onclick="filterMusteri('aktif')">Aktif</button>
            <button class="filter-btn" onclick="filterMusteri('hepsi')">Hepsi</button>
            <button class="filter-btn" onclick="filterMusteri('arsiv')">🗃️ Arşiv</button>
        </div>
        <div id="musteri-list"></div>
    </div>

    <!-- MODALS -->

    <!-- SERVİS MODAL -->
    <div class="modal-overlay" id="servis-modal">
        <div class="modal">
            <div class="modal-title">YENİ SERVİS <button class="close-btn"
                    onclick="closeModal('servis-modal')">✕</button></div>
            <div class="form-group">
                <label>Müşteri Adı</label>
                <input type="text" id="s-musteri-ad" placeholder="Ad Soyad (zorunlu değil)" oninput="musteriOneri('s')">
                <div id="s-musteri-oneri"
                    style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto">
                </div>
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
                <div
                    style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px;">
                    📦 Kullanılan Parçalar (Stoktan Düş)</div>
                <div id="s-parcalar-list"></div>
                <div style="margin-top:8px;">
                    <input type="text" id="s-parca-ara" placeholder="Parça ara..."
                        style="width:100%;box-sizing:border-box;margin-bottom:6px" oninput="parcaAra('s')"
                        autocomplete="off">
                    <div id="s-parca-oneri"
                        style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;max-height:150px;overflow-y:auto;margin-bottom:6px">
                    </div>
                    <input type="hidden" id="s-parca-sec">
                    <div style="display:flex;gap:8px">
                        <input type="number" id="s-parca-adet" placeholder="Adet" style="width:70px" min="1" value="1">
                        <button class="btn btn-ghost btn-sm" onclick="parcaEkle('s')" style="white-space:nowrap">+
                            Ekle</button>
                    </div>
                </div>
            </div>
            <button class="btn btn-primary" onclick="saveServis()">💾 Kaydet</button>
        </div>
    </div>

    <!-- SERVİS DÜZENLEME MODAL -->
    <div class="modal-overlay" id="servis-edit-modal">
        <div class="modal">
            <div class="modal-title">SERVİS DÜZENLE <button class="close-btn"
                    onclick="closeModal('servis-edit-modal')">✕</button></div>
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
                <div
                    style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px;">
                    📦 Kullanılan Parçalar (Stoktan Düş)</div>
                <div id="se-parcalar-list"></div>
                <div style="margin-top:8px;">
                    <input type="text" id="se-parca-ara" placeholder="Parça ara..."
                        style="width:100%;box-sizing:border-box;margin-bottom:6px" oninput="parcaAra('se')"
                        autocomplete="off">
                    <div id="se-parca-oneri"
                        style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;max-height:150px;overflow-y:auto;margin-bottom:6px">
                    </div>
                    <input type="hidden" id="se-parca-sec">
                    <div style="display:flex;gap:8px">
                        <input type="number" id="se-parca-adet" placeholder="Adet" style="width:70px" min="1" value="1">
                        <button class="btn btn-ghost btn-sm" onclick="parcaEkle('se')" style="white-space:nowrap">+
                            Ekle</button>
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
            <div class="modal-title">CARİ HAREKET <button class="close-btn"
                    onclick="closeModal('cari-modal')">✕</button></div>
            <div class="form-group">
                <label>Müşteri / Tedarikçi</label>
                <input type="text" id="c-isim" placeholder="Ad Soyad veya Firma" oninput="musteriOneri('c')">
                <div id="c-musteri-oneri"
                    style="display:none;background:var(--surface2);border:1px solid var(--border);border-radius:6px;margin-top:4px;max-height:120px;overflow-y:auto">
                </div>
            </div>
            <div class="form-group">
                <label>Tür</label>
                <select id="c-tur">
                    <option value="alacak">📥 Alacak (bize borçlu)</option>
                    <option value="borc">📤 Borç (biz borçluyuz)</option>
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

    <!-- CARİ DETAY MODAL -->
    <div class="modal-overlay" id="cari-detay-modal">
        <div class="modal">
            <div class="modal-title" id="cari-detay-baslik">CARİ DETAY <button class="close-btn"
                    onclick="closeModal('cari-detay-modal')">✕</button></div>
            <div id="cari-detay-ozet" style="margin-bottom:14px"></div>
            <div id="cari-detay-liste" style="max-height:300px;overflow-y:auto;margin-bottom:14px"></div>
            <div style="display:flex;gap:8px">
                <button class="btn btn-success btn-sm" style="flex:1" onclick="cariTahsilat()">💵 Tahsilat Al</button>
                <button class="btn btn-danger btn-sm" style="flex:1" onclick="cariOdeme()">💸 Ödeme Yap</button>
            </div>
        </div>
    </div>

    <!-- CARİ TAHSILAT/ÖDEME MODAL -->
    <div class="modal-overlay" id="cari-islem-modal">
        <div class="modal">
            <div class="modal-title" id="cari-islem-baslik">TAHSİLAT <button class="close-btn"
                    onclick="closeModal('cari-islem-modal')">✕</button></div>
            <div id="cari-islem-kisi" style="font-size:13px;color:var(--muted);margin-bottom:12px"></div>
            <div class="form-group">
                <label>Tutar (₺)</label>
                <input type="number" id="ci-tutar" placeholder="0">
            </div>
            <div class="form-group">
                <label>Kasa</label>
                <select id="ci-kasa-id"></select>
            </div>
            <div class="form-group">
                <label>Not</label>
                <input type="text" id="ci-not" placeholder="İsteğe bağlı...">
            </div>
            <button class="btn btn-primary" onclick="cariIslemKaydet()">💾 Kaydet</button>
        </div>
    </div>

    <!-- STOK MODAL -->
    <div class="modal-overlay" id="stok-modal">
        <div class="modal">
            <div class="modal-title">STOK EKLE <button class="close-btn" onclick="closeModal('stok-modal')">✕</button>
            </div>
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
            <div class="modal-title">MÜŞTERİ EKLE <button class="close-btn"
                    onclick="closeModal('musteri-modal')">✕</button></div>
            <div class="form-group">
                <label>Ad Soyad</label>
                <input type="text" id="m-ad" placeholder="Ad Soyad">
            </div>
            <div class="form-group">
                <label>Telefon</label>
                <input type="tel" id="m-tel" placeholder="05XX XXX XX XX">
            </div>
            <div class="form-group">
                <label>Not / Adres</label>
                <input type="text" id="m-not" placeholder="Adres, ek bilgi...">
            </div>
            <button class="btn btn-primary" onclick="saveMusteri()">💾 Kaydet</button>
        </div>
    </div>

    <!-- MÜŞTERİ DETAY MODAL -->
    <div class="modal-overlay" id="musteri-detay-modal">
        <div class="modal">
            <div class="modal-title" id="musteri-detay-baslik">MÜŞTERİ <button class="close-btn"
                    onclick="closeModal('musteri-detay-modal')">✕</button></div>
            <div id="musteri-detay-bilgi" style="margin-bottom:14px"></div>
            <div id="musteri-detay-servisler" style="max-height:250px;overflow-y:auto;margin-bottom:12px"></div>
            <div id="musteri-detay-cari" style="margin-bottom:12px"></div>
            <div style="display:flex;gap:8px;flex-wrap:wrap">
                <button class="btn btn-ghost btn-sm" id="musteri-detay-wa" style="display:none" onclick="musteriWA()">📲
                    WhatsApp</button>
                <button class="btn btn-ghost btn-sm" onclick="musteriDuzenle()">✏️ Düzenle</button>
                <button class="btn btn-ghost btn-sm" id="musteri-arsiv-btn" onclick="musteriArsivToggle()">🗃️
                    Arşivle</button>
                <button class="btn btn-danger btn-sm" onclick="musteriSil()">🗑️ Sil</button>
            </div>
        </div>
    </div>

    <!-- MÜŞTERİ DÜZENLE MODAL -->
    <div class="modal-overlay" id="musteri-edit-modal">
        <div class="modal">
            <div class="modal-title">MÜŞTERİ DÜZENLE <button class="close-btn"
                    onclick="closeModal('musteri-edit-modal')">✕</button></div>
            <div class="form-group">
                <label>Ad Soyad</label>
                <input type="text" id="me-ad">
            </div>
            <div class="form-group">
                <label>Telefon</label>
                <input type="tel" id="me-tel">
            </div>
            <div class="form-group">
                <label>Not / Adres</label>
                <input type="text" id="me-not">
            </div>
            <input type="hidden" id="me-id">
            <button class="btn btn-primary" onclick="musteriGuncelle()">💾 Güncelle</button>
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
            kasalar: [], // Birden fazla kasa desteği
            ayarlar: { isletmeAd: '', isletmeTel: '', adres: '', uyariAktif: true },
            servisFilter: 'hepsi',
            cariFilter: 'hepsi'
        };

        function saveState() {
            // Her zaman localStorage'a kaydet
            try { localStorage.setItem('servis_app', JSON.stringify(state)); } catch (e) { }
            // Firebase'e kaydet - debounce 800ms
            clearTimeout(window._fbSaveTimer);
            window._fbSaveTimer = setTimeout(function () {
                firebaseSaveRetry(0);
            }, 800);
        }

        function firebaseSaveRetry(deneme) {
            if (deneme > 5) {
                console.error('Firebase 5 denemede kaydedemedik!');
                const el = document.getElementById('firebase-durum');
                if (el) { el.textContent = '🔴'; el.title = 'Bağlantı yok'; }
                return;
            }
            if (!window._firebaseReady) {
                // Firebase henüz hazır değil, bekle
                setTimeout(function () { firebaseSaveRetry(deneme + 1); }, 1000);
                return;
            }
            firebaseSave().catch(function () {
                setTimeout(function () { firebaseSaveRetry(deneme + 1); }, 2000);
            });
        }

        // Sayfa kapanırken hemen kaydet
        window.addEventListener('beforeunload', function () {
            clearTimeout(window._fbSaveTimer);
            if (window._firebaseReady) {
                firebaseSave();
            }
        });

        // Uygulama arka plana geçince kaydet (mobil için önemli)
        document.addEventListener('visibilitychange', function () {
            if (document.visibilityState === 'hidden') {
                clearTimeout(window._fbSaveTimer);
                if (window._firebaseReady) firebaseSave();
            }
        });

        async function firebaseSave() {
            if (!window._firebaseReady) {
                console.warn('Firebase hazir degil, kayit atlanıyor');
                return;
            }
            try {
                const { doc, setDoc } = window._firestoreFns;
                // state'i temizle - undefined değerleri kaldır
                const temizState = JSON.parse(JSON.stringify(state));
                await setDoc(doc(window._db, 'servis', 'veri'), temizState);
                console.log('✅ Firebase kaydedildi:', new Date().toLocaleTimeString());
                // Durum göstergesi yeşil yap
                const el = document.getElementById('firebase-durum');
                if (el) { el.textContent = '🟢'; el.title = 'Son kayıt: ' + new Date().toLocaleTimeString(); el.style.opacity = '1'; }
            } catch (e) {
                console.error('❌ Firebase kayit hatasi:', e);
                const el = document.getElementById('firebase-durum');
                if (el) { el.textContent = '🔴'; el.title = 'Kayıt hatası: ' + e.message; el.style.opacity = '1'; }
                // Hata durumunda 5 saniye sonra tekrar dene
                setTimeout(function () { firebaseSave(); }, 5000);
            }
        }

        async function firebaseLoad() {
            if (!window._firebaseReady) return false;
            try {
                const { doc, getDoc } = window._firestoreFns;
                const snap = await getDoc(doc(window._db, 'servis', 'veri'));
                if (snap.exists()) {
                    const fbVeri = snap.data();
                    // Firebase'deki veri gerçekten dolu mu kontrol et
                    const fbDolu = (fbVeri.servisler && fbVeri.servisler.length > 0) ||
                        (fbVeri.satislar && fbVeri.satislar.length > 0) ||
                        (fbVeri.musteriler && fbVeri.musteriler.length > 0) ||
                        (fbVeri.giderler && fbVeri.giderler.length > 0) ||
                        (fbVeri.cari && fbVeri.cari.length > 0) ||
                        (fbVeri.stok && fbVeri.stok.length > 0);
                    if (fbDolu) {
                        state = fbVeri;
                        try { localStorage.setItem('servis_app', JSON.stringify(state)); } catch (e) { }
                        console.log("Firebase den yuklen di");
                        return true;
                    } else {
                        // Firebase bos - localStorage da veri var mi?
                        console.log("Firebase bos array, localStorage kontrol ediliyor...");
                        const lsVeri = localStorageYukle();
                        if (lsVeri) {
                            state = lsVeri;
                            console.log('localStorage veri yuklendi, Firebase aktariliyor...');
                            setTimeout(function () { firebaseSave(); }, 1000);
                            return true;
                        }
                        // Her ikisi de boş - Firebase'e kaydet
                        setTimeout(function () { firebaseSave(); }, 1000);
                        return false;
                    }
                } else {
                    // Firebase de hic dokuman yok
                    console.log("Firebase dokumani yok, localStorage kontrol ediliyor...");
                    const lsVeri = localStorageYukle();
                    if (lsVeri) {
                        state = lsVeri;
                        setTimeout(function () { firebaseSave(); }, 1000);
                        return true;
                    }
                    setTimeout(function () { firebaseSave(); }, 1000);
                    return false;
                }
            } catch (e) {
                console.error('Firebase yükleme hatası:', e);
                // Firebase hata verdi - localStorage dan yukle
                const lsVeri = localStorageYukle();
                if (lsVeri) { state = lsVeri; return true; }
            }
            return false;
        }

        function localStorageYukle() {
            try {
                const ls = localStorage.getItem('servis_app');
                if (!ls) return null;
                const veri = JSON.parse(ls);
                const dolu = (veri.servisler && veri.servisler.length > 0) ||
                    (veri.satislar && veri.satislar.length > 0) ||
                    (veri.musteriler && veri.musteriler.length > 0);
                return dolu ? veri : null;
            } catch (e) { return null; }
        }

        function firebaseGercekZamanli() {
            if (!window._firebaseReady) return;
            const { doc, onSnapshot } = window._firestoreFns;
            var ilkYukleme = true;
            onSnapshot(doc(window._db, 'servis', 'veri'), function (snap) {
                if (ilkYukleme) { ilkYukleme = false; return; }
                if (snap.exists()) {
                    const yeniVeri = snap.data();
                    if (JSON.stringify(yeniVeri) !== JSON.stringify(state)) {
                        state = yeniVeri;
                        try { localStorage.setItem('servis_app', JSON.stringify(state)); } catch (e) { }
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
            } catch (e) { }
        }

        // --- NAVIGATION ---
        const finansPages = ['cari', 'satis', 'gider', 'kasa'];

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
                const mainPages = ['dashboard', 'servisler', 'stok', 'musteriler', 'grafik', 'ayarlar'];
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
                if (!finansPages.some(p => document.getElementById('page-' + p).classList.contains('active'))) {
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
            if (id === 'kasa-modal') {
                kasalariBaslat();
                kasaSelectDoldur('k-kasa-id');
            }
            if (id === 'kasa-yonet-modal') {
                kasalariBaslat();
                renderKasaYonet();
            }
            if (id === 'transfer-modal') {
                kasalariBaslat();
                kasaSelectDoldur('tr-cikis');
                kasaSelectDoldur('tr-giris');
            }
            document.getElementById(id).classList.add('active');
        }

        function populateParcaSelect(elId) { /* artık kullanılmıyor */ }

        function parcaAra(prefix) {
            const q = document.getElementById(prefix + '-parca-ara').value.toLowerCase();
            const oneriEl = document.getElementById(prefix + '-parca-oneri');
            if (!q || q.length < 1) { oneriEl.style.display = 'none'; return; }
            const eslesen = state.stok.filter(function (s) { return s.adet > 0 && s.ad.toLowerCase().includes(q); }).slice(0, 8);
            if (eslesen.length === 0) { oneriEl.style.display = 'none'; return; }
            oneriEl.style.display = 'block';
            oneriEl.innerHTML = '';
            eslesen.forEach(function (s) {
                var div = document.createElement('div');
                div.style.cssText = 'padding:10px 12px;cursor:pointer;font-size:13px;border-bottom:1px solid #2e2e2e';
                div.innerHTML = s.ad + ' <span style="color:#888;font-size:11px">(Stok: ' + s.adet + ') - ' + s.maliyet + ' TL</span>';
                (function (sid) { div.addEventListener('mousedown', function (e) { e.preventDefault(); e.stopPropagation(); parcaSec(prefix, sid); }); })(s.id);
                oneriEl.appendChild(div);
            });
        }

        function parcaSec(prefix, stokId) {
            const s = state.stok.find(function (x) { return String(x.id) === String(stokId); });
            if (!s) { alert('Parça bulunamadı: ' + stokId); return; }
            document.getElementById(prefix + '-parca-ara').value = s.ad;
            document.getElementById(prefix + '-parca-sec').value = String(s.id);
            document.getElementById(prefix + '-parca-oneri').style.display = 'none';
            // Seçildi bildirimi
            const araEl = document.getElementById(prefix + '-parca-ara');
            araEl.style.borderColor = 'var(--green)';
            setTimeout(function () { araEl.style.borderColor = ''; }, 1500);
        }

        function parcaEkle(prefix) {
            const secEl = document.getElementById(prefix + '-parca-sec');
            const adetEl = document.getElementById(prefix + '-parca-adet');
            const stokIdStr = secEl.value;
            const stokId = parseInt(stokIdStr);
            const adet = parseInt(adetEl.value) || 1;
            if (!stokIdStr || !stokId) { alert('Önce parça arayıp seçiniz'); return; }
            const stok = state.stok.find(function (s) { return String(s.id) === String(stokId); });
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
                '<div style="font-size:11px;color:var(--muted)">' + p.adet + ' adet x ₺' + p.birimMaliyet + ' = ₺' + (p.adet * p.birimMaliyet).toFixed(0) + '</div>' +
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
            el.addEventListener('click', function (e) {
                if (e.target === this) this.classList.remove('active');
            });
        });

        // --- DASHBOARD ---
        function renderDashboard() {
            const now = new Date();
            renderDriveBar();
            yedekKontrol();
            document.getElementById('dashboard-date').textContent = now.toLocaleDateString('tr-TR', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });

            // --- BEKLEYEN UYARI ---
            const uyariAktif = !state.ayarlar || state.ayarlar.uyariAktif !== false;
            const bekleyenler = uyariAktif ? state.servisler.filter(function (s) {
                if (s.arsiv || s.durum === 'teslim') return false;
                const gun = Math.floor((now - new Date(s.tarih)) / 86400000);
                return gun >= 3;
            }) : [];
            const uyariEl = document.getElementById('bekleyen-uyari');
            if (bekleyenler.length > 0) {
                uyariEl.innerHTML = '<div style="background:#f59e0b22;border:1px solid #f59e0b66;border-radius:10px;padding:12px 14px;cursor:pointer" onclick="showPage(\"servisler\")">' +
                    '<div style="font-weight:700;color:var(--accent);margin-bottom:4px">⚠️ ' + bekleyenler.length + ' servis 3+ gündür bekliyor!</div>' +
                    '<div style="font-size:12px;color:var(--muted)">' + bekleyenler.map(function (s) {
                        const gun = Math.floor((now - new Date(s.tarih)) / 86400000);
                        return s.musteri + ' — ' + s.alet + ' (' + gun + ' gün)';
                    }).join(', ') + '</div>' +
                    '</div>';
            } else {
                uyariEl.innerHTML = '';
            }

            // --- BU AY ÖZETİ ---
            const buAyGelir = state.servisler.filter(function (s) {
                const d = new Date(s.tarih);
                return s.durum === 'teslim' && d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
            }).reduce(function (a, s) { return a + (parseFloat(s.ucret) || 0); }, 0) +
                (state.satislar || []).filter(function (s) {
                    const d = new Date(s.tarih);
                    return s.tur === 'satis' && d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
                }).reduce(function (a, s) { return a + s.toplam; }, 0);

            const buAyGider = (state.giderler || []).filter(function (g) {
                const d = new Date(g.tarih);
                return d.getMonth() === now.getMonth() && d.getFullYear() === now.getFullYear();
            }).reduce(function (a, g) { return a + g.tutar; }, 0);

            const kasaBakiye = (state.kasa || []).reduce(function (a, k) {
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
            const toplamGelir = state.servisler.filter(s => s.durum === 'teslim').reduce((a, s) => a + (parseFloat(s.ucret) || 0), 0) +
                (state.satislar || []).filter(s => s.tur === 'satis').reduce((a, s) => a + s.toplam, 0);
            const toplamMaliyet = state.servisler.reduce((a, s) => a + (parseFloat(s.maliyet) || 0), 0);
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
      <div class="stat-value ${kar >= 0 ? 'profit-positive' : 'profit-negative'}" style="font-size:20px">₺${kar.toFixed(0)}</div>
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
          <div class="list-item-sub">${new Date(s.tarih).toLocaleDateString('tr-TR')} • ${s.marka || ''}</div>
        </div>
        <span class="badge badge-${s.durum}">${durumLabel(s.durum)}</span>
      </div>
    </div>
  `).join('');
        }

        function durumLabel(d) {
            return { bekliyor: 'Bekliyor', tamirde: 'Tamirde', hazir: 'Hazır', teslim: 'Teslim' }[d] || d;
        }

        // --- SERVİS ---
        function populateMusteriSelect(id) {
            // artık kullanılmıyor ama eski çağrılar için boş bırakıyoruz
        }

        function musteriOneri(prefix) {
            const inputId = prefix === 's' ? 's-musteri-ad' : (prefix === 'sat' ? 'sat-musteri' : (prefix === 'al' ? 'al-tedarikci' : 'c-isim'));
            const oneriId = prefix === 's' ? 's-musteri-oneri' : (prefix === 'sat' ? 'sat-musteri-oneri' : (prefix === 'al' ? 'al-tedarikci-oneri' : 'c-musteri-oneri'));
            const q = document.getElementById(inputId).value.toLowerCase();
            const oneriEl = document.getElementById(oneriId);
            if (!q || q.length < 1) { oneriEl.style.display = 'none'; return; }
            const eslesen = state.musteriler.filter(m => m.ad.toLowerCase().includes(q)).slice(0, 5);
            if (eslesen.length === 0) { oneriEl.style.display = 'none'; return; }
            oneriEl.style.display = 'block';
            oneriEl.innerHTML = eslesen.map(function (m) {
                var tel = m.tel ? ' <span style="color:#888;font-size:11px">(' + m.tel + ')</span>' : '';
                return '<div onclick="musteriSec(\'' + prefix + '\',' + m.id + ')" style="padding:8px 12px;cursor:pointer;font-size:13px;border-bottom:1px solid #2e2e2e">' + m.ad + tel + '</div>';
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
            } else if (prefix === 'al') {
                document.getElementById('al-tedarikci').value = m.ad;
                document.getElementById('al-tedarikci-oneri').style.display = 'none';
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
                parcalar: parcalar.map(p => ({ ...p })),
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
            ['s-musteri-ad', 's-musteri-id', 's-alet', 's-marka', 's-ariza', 's-ucret', 's-not'].forEach(id => document.getElementById(id).value = '');
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
                if (q && !s.musteri.toLowerCase().includes(q) && !s.alet.toLowerCase().includes(q) && !(s.marka || '').toLowerCase().includes(q)) return false;
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
          <div class="list-item-title">${s.alet} ${s.marka ? '— ' + s.marka : ''}</div>
          <div class="list-item-sub">👤 ${s.musteri} • ${new Date(s.tarih).toLocaleDateString('tr-TR')}</div>
          ${s.ariza ? `<div class="list-item-sub" style="margin-top:4px">🔩 ${s.ariza}</div>` : ''}
          ${s.ucret ? `<div class="list-item-sub" style="margin-top:4px;color:var(--accent)">₺${s.ucret} ${s.maliyet ? '• Maliyet: ₺' + s.maliyet : ''}</div>` : ''}
          ${s.parcalar && s.parcalar.length ? `<div class="list-item-sub" style="margin-top:4px">📦 ${s.parcalar.map(p => p.ad + ' x' + p.adet).join(', ')}</div>` : ''}
        </div>
        <span class="badge badge-${s.durum}">${durumLabel(s.durum)}</span>
      </div>
      <div class="list-item-actions">
        <button class="btn btn-ghost btn-sm" onclick="editServis(${s.id})">✏️ Düzenle</button>
        <button class="btn btn-ghost btn-sm" onclick="faturaCikart(${s.id})">🧾 Fiş</button>
        <button class="btn btn-whatsapp btn-sm" onclick="waServisHazir(${s.id})">📲 Hazır</button>
        <button class="btn btn-ghost btn-sm" onclick="waServisAlinsin(${s.id})">💬 Bilgi</button>
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
            tempParcalar.se = s.parcalar ? s.parcalar.map(p => ({ ...p })) : [];
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
            s.parcalar = yeniParcalar.map(p => ({ ...p }));
            s.not = document.getElementById('se-not').value;
            const eskiDurum = s.durum;
            s.durum = document.getElementById('se-durum').value;
            saveState();
            closeModal('servis-edit-modal');
            // Teslim edildi ise ödeme al
            if (s.durum === 'teslim' && eskiDurum !== 'teslim' && s.ucret && parseFloat(s.ucret) > 0) {
                setTimeout(function () {
                    odemeModalAc(s);
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

        function waServis(id) { waServisHazir(id); }

        function waServisTelAl(s) {
            const m = (state.musteriler || []).find(function (x) { return x.ad === s.musteri; });
            return m && m.tel ? m.tel.replace(/\D/g, '').replace(/^0/, '') : null;
        }

        function waServisHazir(id) {
            const s = state.servisler.find(function (x) { return x.id === id; });
            if (!s) return;
            const tel = waServisTelAl(s);
            const parcalar = s.parcalar && s.parcalar.length
                ? s.parcalar.map(function (p) { return p.ad + ' x' + p.adet; }).join(', ')
                : '';
            const mesaj = 'Sayın ' + s.musteri + ',\n\n'
                + s.alet + (s.marka ? ' (' + s.marka + ')' : '') + ' cihazınızın tamiri tamamlandı, teslim almak için gelebilirsiniz.\n'
                + (parcalar ? '\nKullanılan parçalar: ' + parcalar + '\n' : '')
                + '\nTamir Ücreti: ₺' + parseFloat(s.ucret || 0).toFixed(0)
                + '\n\nDüka Enerji 🔧';
            if (tel) {
                window.open('https://wa.me/90' + tel + '?text=' + encodeURIComponent(mesaj));
            } else {
                if (confirm('Telefon kayıtlı değil.\n\nMesajı kopyalamak ister misiniz?')) {
                    navigator.clipboard && navigator.clipboard.writeText(mesaj);
                    alert('Kopyalandı!');
                }
            }
        }

        function waServisAlinsin(id) {
            const s = state.servisler.find(function (x) { return x.id === id; });
            if (!s) return;
            const tel = waServisTelAl(s);
            const mesaj = 'Sayın ' + s.musteri + ',\n\n'
                + s.alet + (s.marka ? ' (' + s.marka + ')' : '') + ' cihazınız servisimizde incelendi.\n'
                + (s.ariza ? 'Arıza: ' + s.ariza + '\n' : '')
                + '\nDetaylar için lütfen bizimle iletişime geçiniz.'
                + '\n\nDüka Enerji 🔧';
            if (tel) {
                window.open('https://wa.me/90' + tel + '?text=' + encodeURIComponent(mesaj));
            } else {
                alert('Müşteri telefonu kayıtlı değil.');
            }
        }

        // --- CARİ ---
        // Yeni cari sistemi: kişi bazında bakiye, işlem geçmişi, tahsilat/ödeme

        let cariFilter = 'hepsi';
        let _aktifCariKisi = null; // Detay modalı için

        // Kişi bazında cari özet hesapla
        function cariKisiBakiye(isim) {
            const hareketler = state.cari.filter(function (c) { return c.isim === isim; });
            const alacak = hareketler.filter(function (c) { return c.tur === 'alacak'; }).reduce(function (a, c) { return a + c.tutar; }, 0);
            const borc = hareketler.filter(function (c) { return c.tur === 'borc'; }).reduce(function (a, c) { return a + c.tutar; }, 0);
            const tahsilat = hareketler.filter(function (c) { return c.tur === 'tahsilat'; }).reduce(function (a, c) { return a + c.tutar; }, 0);
            const odeme = hareketler.filter(function (c) { return c.tur === 'odeme'; }).reduce(function (a, c) { return a + c.tutar; }, 0);
            // Net: alacak - tahsilat (bize borçlu kaldığı) - (borc - odeme) (biz borçlu kaldığımız)
            const netAlacak = alacak - tahsilat;
            const netBorc = borc - odeme;
            return { alacak, borc, tahsilat, odeme, netAlacak, netBorc, net: netAlacak - netBorc, hareketler };
        }

        // Benzersiz kişileri listele
        function cariKisileri() {
            const kisiler = {};
            state.cari.forEach(function (c) {
                if (!kisiler[c.isim]) kisiler[c.isim] = true;
            });
            return Object.keys(kisiler);
        }

        function saveCari() {
            const isim = document.getElementById('c-isim').value.trim();
            const tutar = parseFloat(document.getElementById('c-tutar').value) || 0;
            if (!isim) { alert('İsim giriniz'); return; }
            if (!tutar) { alert('Tutar giriniz'); return; }
            const cari = {
                id: Date.now(),
                isim,
                tur: document.getElementById('c-tur').value,
                tutar,
                aciklama: document.getElementById('c-aciklama').value.trim(),
                tarih: new Date().toISOString()
            };
            state.cari.push(cari);
            saveState();
            closeModal('cari-modal');
            ['c-isim', 'c-tutar', 'c-aciklama'].forEach(function (id) { document.getElementById(id).value = ''; });
            renderCari();
        }

        function filterCari(f) {
            cariFilter = f;
            document.querySelectorAll('.filter-row .filter-btn').forEach(function (b) { b.classList.remove('active'); });
            event.target.classList.add('active');
            renderCari();
        }

        function renderCari() {
            const q = (document.getElementById('cari-search') ? document.getElementById('cari-search').value : '').toLowerCase();

            // Toplam istatistikler
            const kisiler = cariKisileri();
            let toplamAlacak = 0, toplamBorc = 0;
            kisiler.forEach(function (k) {
                const b = cariKisiBakiye(k);
                if (b.net > 0) toplamAlacak += b.net;
                else toplamBorc += Math.abs(b.net);
            });

            document.getElementById('cari-stats').innerHTML =
                '<div class="stat-card"><div class="stat-value profit-positive" style="font-size:20px">₺' + toplamAlacak.toFixed(0) + '</div><div class="stat-label">Toplam Alacak</div></div>' +
                '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">₺' + toplamBorc.toFixed(0) + '</div><div class="stat-label">Toplam Borç</div></div>';

            // Kişi bazında özet kartlar (en büyük bakiyeler)
            const kisiBakiyeler = kisiler.map(function (k) {
                return { isim: k, bakiye: cariKisiBakiye(k) };
            }).filter(function (x) { return Math.abs(x.bakiye.net) > 0; })
                .sort(function (a, b) { return Math.abs(b.bakiye.net) - Math.abs(a.bakiye.net); })
                .slice(0, 5);

            if (kisiBakiyeler.length > 0) {
                // Özet kartlar - addEventListener ile
                const ozet_el = document.getElementById('cari-ozet-kartlar');
                ozet_el.innerHTML = '<div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">En Yüksek Bakiyeler</div><div id="cari-ozet-ic" style="display:flex;flex-direction:column;gap:6px"></div>';
                const ozet_ic = document.getElementById('cari-ozet-ic');
                kisiBakiyeler.forEach(function (x) {
                    const net = x.bakiye.net;
                    const renk = net > 0 ? 'var(--green)' : 'var(--accent2)';
                    const etiket = net > 0 ? 'Alacak' : 'Borç';
                    var div = document.createElement('div');
                    div.style.cssText = 'display:flex;justify-content:space-between;align-items:center;background:var(--surface);border:1px solid var(--border);border-radius:8px;padding:10px 14px;cursor:pointer';
                    div.innerHTML = '<div style="font-weight:600;font-size:14px">' + x.isim + '</div><div style="text-align:right"><div style="font-weight:700;color:' + renk + '">₺' + Math.abs(net).toFixed(0) + '</div><div style="font-size:10px;color:' + renk + '">' + etiket + '</div></div>';
                    (function (isim) { div.addEventListener('click', function () { cariDetayAc(isim); }); })(x.isim);
                    ozet_ic.appendChild(div);
                });
            } else {
                document.getElementById('cari-ozet-kartlar').innerHTML = '';
            }

            // Kişi listesi
            let filtreliKisiler = kisiler.filter(function (k) {
                if (q && !k.toLowerCase().includes(q)) return false;
                const b = cariKisiBakiye(k);
                if (cariFilter === 'alacak' && b.net <= 0) return false;
                if (cariFilter === 'borc' && b.net >= 0) return false;
                if (cariFilter === 'kapali' && Math.abs(b.net) > 0.01) return false;
                return true;
            });

            if (filtreliKisiler.length === 0) {
                document.getElementById('cari-list').innerHTML = '<div class="empty"><div class="empty-icon">💰</div><div>Kayıt bulunamadı</div></div>';
                return;
            }

            const listEl2 = document.getElementById('cari-list');
            listEl2.innerHTML = '';
            filtreliKisiler.forEach(function (k) {
                const bk = cariKisiBakiye(k);
                const net = bk.net;
                const renk = net > 0 ? 'var(--green)' : (net < 0 ? 'var(--accent2)' : 'var(--muted)');
                const etiket = net > 0 ? '📥 Alacak' : (net < 0 ? '📤 Borç' : '✅ Kapandı');
                const sonH = [...bk.hareketler].sort(function (a, bb) { return new Date(bb.tarih) - new Date(a.tarih); })[0];
                var item = document.createElement('div');
                item.className = 'list-item';
                (function (isim) { item.addEventListener('click', function () { cariDetayAc(isim); }); })(k);
                item.innerHTML =
                    '<div class="list-item-top">' +
                    '<div>' +
                    '<div class="list-item-title">' + k + '</div>' +
                    '<div class="list-item-sub">' + bk.hareketler.length + ' işlem' + (sonH ? ' • Son: ' + new Date(sonH.tarih).toLocaleDateString("tr-TR") : '') + '</div>' +
                    '</div>' +
                    '<div style="text-align:right">' +
                    '<div style="font-weight:700;font-size:16px;color:' + renk + '">₺' + Math.abs(net).toFixed(0) + '</div>' +
                    '<div style="font-size:11px;color:' + renk + '">' + etiket + '</div>' +
                    '</div>' +
                    '</div>';
                listEl2.appendChild(item);
            });
        }

        function cariDetayAc(isim) {
            _aktifCariKisi = isim;
            const b = cariKisiBakiye(isim);
            const net = b.net;
            const renk = net > 0 ? 'var(--green)' : (net < 0 ? 'var(--accent2)' : 'var(--muted)');

            document.getElementById('cari-detay-baslik').innerHTML =
                '👤 ' + isim + ' <button class="close-btn" onclick="closeModal(&#39;cari-detay-modal&#39;)">✕</button>';

            document.getElementById('cari-detay-ozet').innerHTML =
                '<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px">' +
                '<div class="stat-card"><div class="stat-value profit-positive" style="font-size:18px">₺' + b.alacak.toFixed(0) + '</div><div class="stat-label">Alacak</div></div>' +
                '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:18px">₺' + b.borc.toFixed(0) + '</div><div class="stat-label">Borç</div></div>' +
                '<div class="stat-card"><div class="stat-value" style="font-size:18px;color:#60a5fa">₺' + b.tahsilat.toFixed(0) + '</div><div class="stat-label">Tahsilat</div></div>' +
                '<div class="stat-card"><div class="stat-value" style="font-size:18px;color:#a78bfa">₺' + b.odeme.toFixed(0) + '</div><div class="stat-label">Ödeme</div></div>' +
                '</div>' +
                '<div style="background:var(--surface2);border-radius:8px;padding:12px;display:flex;justify-content:space-between;align-items:center">' +
                '<span style="font-size:13px;font-weight:600">Net Bakiye</span>' +
                '<span style="font-family:sans-serif;font-weight:700;font-size:22px;color:' + renk + '">₺' + Math.abs(net).toFixed(0) + ' <span style="font-size:13px">' + (net > 0 ? 'Alacak' : net < 0 ? 'Borç' : 'Kapandı') + '</span></span>' +
                '</div>';

            // İşlem geçmişi
            const sirali = b.hareketler.sort(function (a, b) { return new Date(b.tarih) - new Date(a.tarih); });
            const turLabel = { alacak: '📥 Alacak', borc: '📤 Borç', tahsilat: '💵 Tahsilat', odeme: '💸 Ödeme' };
            const turRenk = { alacak: 'var(--green)', borc: 'var(--accent2)', tahsilat: '#60a5fa', odeme: '#a78bfa' };

            document.getElementById('cari-detay-liste').innerHTML = sirali.length === 0 ?
                '<div style="color:var(--muted);text-align:center;padding:20px">İşlem yok</div>' :
                sirali.map(function (h) {
                    return '<div style="display:flex;justify-content:space-between;align-items:center;padding:10px 0;border-bottom:1px solid var(--border)">' +
                        '<div>' +
                        '<div style="font-size:13px;font-weight:600;color:' + (turRenk[h.tur] || 'var(--text)') + '">' + (turLabel[h.tur] || h.tur) + '</div>' +
                        '<div style="font-size:11px;color:var(--muted)">' + (h.aciklama || '') + ' • ' + new Date(h.tarih).toLocaleDateString("tr-TR") + '</div>' +
                        '</div>' +
                        '<div style="display:flex;align-items:center;gap:8px">' +
                        '<span style="font-weight:700;color:' + (turRenk[h.tur] || 'var(--text)') + '">₺' + h.tutar.toFixed(0) + '</span>' +
                        '<button onclick="deleteCariHareket(' + h.id + ');event.stopPropagation();" style="background:none;border:none;color:var(--muted);cursor:pointer;font-size:14px">🗑️</button>' +
                        '</div>' +
                        '</div>';
                }).join('');

            document.getElementById('cari-detay-modal').classList.add('active');
        }

        function cariTahsilat() {
            kasalariBaslat();
            const b = cariKisiBakiye(_aktifCariKisi);
            document.getElementById('cari-islem-baslik').innerHTML = '💵 TAHSİLAT AL <button class="close-btn" onclick="closeModal(&#39;cari-islem-modal&#39;)">✕</button>';
            document.getElementById('cari-islem-kisi').textContent = _aktifCariKisi + ' — Net alacak: ₺' + b.net.toFixed(0);
            document.getElementById('ci-tutar').value = b.net > 0 ? b.net.toFixed(0) : '';
            kasaSelectDoldur('ci-kasa-id');
            document.getElementById('ci-not').value = '';
            document.getElementById('cari-islem-modal').dataset.tur = 'tahsilat';
            document.getElementById('cari-islem-modal').classList.add('active');
        }

        function cariOdeme() {
            kasalariBaslat();
            const b = cariKisiBakiye(_aktifCariKisi);
            document.getElementById('cari-islem-baslik').innerHTML = '💸 ÖDEME YAP <button class="close-btn" onclick="closeModal(&#39;cari-islem-modal&#39;)">✕</button>';
            document.getElementById('cari-islem-kisi').textContent = _aktifCariKisi + ' — Net borç: ₺' + Math.abs(b.net).toFixed(0);
            document.getElementById('ci-tutar').value = b.net < 0 ? Math.abs(b.net).toFixed(0) : '';
            kasaSelectDoldur('ci-kasa-id');
            document.getElementById('ci-not').value = '';
            document.getElementById('cari-islem-modal').dataset.tur = 'odeme';
            document.getElementById('cari-islem-modal').classList.add('active');
        }

        function cariIslemKaydet() {
            const tutar = parseFloat(document.getElementById('ci-tutar').value) || 0;
            if (!tutar) { alert('Tutar giriniz'); return; }
            const tur = document.getElementById('cari-islem-modal').dataset.tur;
            const kasaId = parseInt(document.getElementById('ci-kasa-id').value);
            const not = document.getElementById('ci-not').value.trim();

            state.cari.push({
                id: Date.now(),
                isim: _aktifCariKisi,
                tur: tur,
                tutar,
                aciklama: not || (tur === 'tahsilat' ? 'Tahsilat' : 'Ödeme'),
                tarih: new Date().toISOString()
            });

            // Kasaya da yansıt
            if (tur === 'tahsilat') {
                kasaHareketEkle(kasaId, 'giris', _aktifCariKisi + ' tahsilatı', tutar, not);
            } else {
                kasaHareketEkle(kasaId, 'cikis', _aktifCariKisi + ' ödemesi', tutar, not);
            }

            saveState();
            closeModal('cari-islem-modal');
            cariDetayAc(_aktifCariKisi); // Detayı yenile
            renderCari();
        }

        function deleteCariHareket(id) {
            if (!confirm('Bu hareketi silmek istiyor musunuz?')) return;
            state.cari = state.cari.filter(function (c) { return c.id !== id; });
            saveState();
            if (_aktifCariKisi) cariDetayAc(_aktifCariKisi);
            renderCari();
        }

        function deleteCari(id) {
            if (!confirm('Bu kaydı silmek istediğinize emin misiniz?')) return;
            state.cari = state.cari.filter(function (c) { return c.id !== id; });
            saveState();
            renderCari();
        }

        // Eski odendi fonksiyonu - geriye dönük uyumluluk
        function odendi(id) {
            deleteCari(id);
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
            ['st-ad', 'st-adet', 'st-maliyet', 'st-min'].forEach(id => document.getElementById(id).value = '');
            renderStok();
        }

        function renderStok() {
            const q = (document.getElementById('stok-search') ? document.getElementById('stok-search').value : '').toLowerCase();
            const stokList = state.stok.filter(function (s) { return !q || s.ad.toLowerCase().includes(q); });
            if (stokList.length === 0) {
                document.getElementById('stok-list').innerHTML = '<div class="empty"><div class="empty-icon">📦</div><div>Stok kaydı yok</div></div>';
                return;
            }
            document.getElementById('stok-list').innerHTML = stokList.map(s => `
    <div class="list-item" style="${s.adet <= s.min ? 'border-color:var(--accent2)' : ''}">
      <div class="list-item-top">
        <div>
          <div class="list-item-title">${s.ad}</div>
          <div class="list-item-sub">Birim: ₺${s.maliyet} ${s.min ? '• Min: ' + s.min : ''}</div>
          ${s.adet <= s.min ? '<div style="font-size:11px;color:var(--accent2);margin-top:4px">⚠️ Düşük stok!</div>' : ''}
        </div>
        <div style="text-align:right">
          <div style="font-family:\'Bebas Neue\';font-size:28px;color:${s.adet <= s.min ? 'var(--accent2)' : 'var(--accent)'}">${s.adet}</div>
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
            document.getElementById('ste-maliyet').value = s.maliyet || 0;
            document.getElementById('ste-satis').value = s.satisFiyati || 0;
            document.getElementById('ste-min').value = s.min || 0;
            hesaplaMarj();
            document.getElementById('stok-edit-modal').classList.add('active');
        }

        function hesaplaMarj() {
            const maliyet = parseFloat(document.getElementById('ste-maliyet').value) || 0;
            const satis = parseFloat(document.getElementById('ste-satis').value) || 0;
            const el = document.getElementById('marj-goster');
            if (!el) return;
            if (maliyet > 0 && satis > 0) {
                const marj = ((satis - maliyet) / maliyet * 100).toFixed(0);
                const kar = (satis - maliyet).toFixed(0);
                el.textContent = marj >= 0
                    ? '✅ Kar: ₺' + kar + ' (%' + marj + ')'
                    : '❌ Zarar: ₺' + Math.abs(kar) + ' (%' + Math.abs(marj) + ')';
                el.style.color = marj >= 0 ? 'var(--green)' : 'var(--accent2)';
            } else {
                el.textContent = '';
            }
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
            s.satisFiyati = parseFloat(document.getElementById('ste-satis').value) || 0;
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
        let musteriFilter = 'aktif';
        let _aktifMusteriId = null;

        function filterMusteri(f) {
            musteriFilter = f;
            document.querySelectorAll('#page-musteriler .filter-btn').forEach(function (b) { b.classList.remove('active'); });
            event.target.classList.add('active');
            renderMusteriler();
        }

        function saveMusteri() {
            const ad = document.getElementById('m-ad').value.trim();
            if (!ad) { alert('İsim giriniz'); return; }
            const m = {
                id: Date.now(),
                ad,
                tel: document.getElementById('m-tel').value.trim(),
                not: document.getElementById('m-not').value.trim(),
                arsiv: false,
                tarih: new Date().toISOString()
            };
            state.musteriler.push(m);
            saveState();
            closeModal('musteri-modal');
            ['m-ad', 'm-tel', 'm-not'].forEach(function (id) { document.getElementById(id).value = ''; });
            renderMusteriler();
        }

        function musteriGuncelle() {
            const id = parseInt(document.getElementById('me-id').value);
            const m = state.musteriler.find(function (x) { return x.id === id; });
            if (!m) return;
            m.ad = document.getElementById('me-ad').value.trim();
            m.tel = document.getElementById('me-tel').value.trim();
            m.not = document.getElementById('me-not').value.trim();
            saveState();
            closeModal('musteri-edit-modal');
            musteriDetayAc(id);
            renderMusteriler();
        }

        function musteriDuzenle() {
            const m = state.musteriler.find(function (x) { return x.id === _aktifMusteriId; });
            if (!m) return;
            document.getElementById('me-id').value = m.id;
            document.getElementById('me-ad').value = m.ad;
            document.getElementById('me-tel').value = m.tel || '';
            document.getElementById('me-not').value = m.not || '';
            document.getElementById('musteri-edit-modal').classList.add('active');
        }

        function musteriArsivToggle() {
            const m = state.musteriler.find(function (x) { return x.id === _aktifMusteriId; });
            if (!m) return;
            m.arsiv = !m.arsiv;
            saveState();
            closeModal('musteri-detay-modal');
            renderMusteriler();
        }

        function musteriSil() {
            if (!confirm('Bu müşteriyi silmek istediğinize emin misiniz?')) return;
            state.musteriler = state.musteriler.filter(function (m) { return m.id !== _aktifMusteriId; });
            saveState();
            closeModal('musteri-detay-modal');
            renderMusteriler();
        }

        function musteriWA() {
            const m = state.musteriler.find(function (x) { return x.id === _aktifMusteriId; });
            if (!m || !m.tel) return;
            const t = m.tel.replace(/\D/g, '').replace(/^0/, '');
            window.open('https://wa.me/90' + t + '?text=' + encodeURIComponent('Sayın ' + m.ad + ', servisiniz hakkında bilgi vermek istedik.'));
        }

        function musteriDetayAc(id) {
            const m = state.musteriler.find(function (x) { return x.id === id; });
            if (!m) return;
            _aktifMusteriId = id;

            // Başlık
            document.getElementById('musteri-detay-baslik').innerHTML =
                '👤 ' + m.ad + ' <button class="close-btn" onclick="closeModal(&#39;musteri-detay-modal&#39;)">✕</button>';

            // Bilgi kartı
            document.getElementById('musteri-detay-bilgi').innerHTML =
                '<div style="background:var(--surface2);border-radius:8px;padding:12px">' +
                (m.tel ? '<div style="font-size:13px;margin-bottom:4px">📞 ' + m.tel + '</div>' : '') +
                (m.not ? '<div style="font-size:13px;color:var(--muted)">📝 ' + m.not + '</div>' : '') +
                '<div style="font-size:11px;color:var(--muted);margin-top:6px">Kayıt: ' + new Date(m.tarih).toLocaleDateString("tr-TR") + '</div>' +
                '</div>';

            // Servis geçmişi
            const servisler = state.servisler.filter(function (s) {
                return String(s.musteriId) === String(id) || s.musteri === m.ad;
            }).reverse();

            const waBt = document.getElementById('musteri-detay-wa');
            if (m.tel) { waBt.style.display = 'inline-flex'; } else { waBt.style.display = 'none'; }

            const arsivBtn = document.getElementById('musteri-arsiv-btn');
            arsivBtn.textContent = m.arsiv ? '📤 Arşivden Çıkar' : '🗃️ Arşivle';

            if (servisler.length === 0) {
                document.getElementById('musteri-detay-servisler').innerHTML =
                    '<div style="font-size:12px;color:var(--muted);padding:8px 0">Servis kaydı yok</div>';
            } else {
                document.getElementById('musteri-detay-servisler').innerHTML =
                    '<div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:8px">Servis Geçmişi (' + servisler.length + ')</div>' +
                    servisler.map(function (s) {
                        return '<div style="display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid var(--border)">' +
                            '<div>' +
                            '<div style="font-size:13px;font-weight:600">' + s.alet + (s.marka ? ' / ' + s.marka : '') + '</div>' +
                            '<div style="font-size:11px;color:var(--muted)">' + new Date(s.tarih).toLocaleDateString("tr-TR") + ' • ' + durumLabel(s.durum) + '</div>' +
                            '</div>' +
                            '<div style="font-weight:700;color:var(--accent)">₺' + (s.ucret || 0) + '</div>' +
                            '</div>';
                    }).join('');
            }

            // Cari bakiye
            const carik = cariKisiBakiye(m.ad);
            if (Math.abs(carik.net) > 0.01 || carik.hareketler.length > 0) {
                const renk = carik.net > 0 ? 'var(--green)' : 'var(--accent2)';
                document.getElementById('musteri-detay-cari').innerHTML =
                    '<div style="background:var(--surface2);border-radius:8px;padding:12px;cursor:pointer" id="md-cari-link">' +
                    '<div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:4px">Cari Bakiye</div>' +
                    '<div style="font-size:20px;font-weight:700;color:' + renk + '">₺' + Math.abs(carik.net).toFixed(0) + ' <span style="font-size:12px">' + (carik.net > 0 ? 'Alacak' : 'Borç') + '</span></div>' +
                    '</div>';
            } else {
                document.getElementById('musteri-detay-cari').innerHTML = '';
            }

            document.getElementById('musteri-detay-modal').classList.add('active');
        }

        function renderMusteriler() {
            const q = (document.getElementById('musteri-search') ? document.getElementById('musteri-search').value : '').toLowerCase();

            // İstatistikler
            const toplamMusteri = state.musteriler.filter(function (m) { return !m.arsiv; }).length;
            const arsivMusteri = state.musteriler.filter(function (m) { return m.arsiv; }).length;
            document.getElementById('musteri-stats').innerHTML =
                '<div class="stat-card"><div class="stat-value">' + toplamMusteri + '</div><div class="stat-label">Aktif Müşteri</div></div>' +
                '<div class="stat-card"><div class="stat-value" style="color:var(--muted)">' + arsivMusteri + '</div><div class="stat-label">Arşivlenen</div></div>';

            let list = state.musteriler.filter(function (m) {
                if (musteriFilter === 'aktif' && m.arsiv) return false;
                if (musteriFilter === 'arsiv' && !m.arsiv) return false;
                if (q && !m.ad.toLowerCase().includes(q) && !(m.tel || '').includes(q)) return false;
                return true;
            });

            if (list.length === 0) {
                document.getElementById('musteri-list').innerHTML = '<div class="empty"><div class="empty-icon">👥</div><div>Müşteri bulunamadı</div></div>';
                return;
            }

            const el = document.getElementById('musteri-list');
            el.innerHTML = '';
            list.forEach(function (m) {
                const servisSayisi = state.servisler.filter(function (s) {
                    return String(s.musteriId) === String(m.id) || s.musteri === m.ad;
                }).length;
                const carik = cariKisiBakiye(m.ad);
                const netBakiye = carik.net;

                var item = document.createElement('div');
                item.className = 'list-item';
                if (m.arsiv) item.style.opacity = '0.6';
                (function (mid) { item.addEventListener('click', function () { musteriDetayAc(mid); }); })(m.id);

                item.innerHTML =
                    '<div class="list-item-top">' +
                    '<div>' +
                    '<div class="list-item-title">' + m.ad + (m.arsiv ? ' <span style="font-size:10px;color:var(--muted)">[Arşiv]</span>' : '') + '</div>' +
                    '<div class="list-item-sub">' +
                    (m.tel ? '📞 ' + m.tel + ' • ' : '') +
                    '🔧 ' + servisSayisi + ' servis' +
                    (Math.abs(netBakiye) > 0.01 ? ' • <span style="color:' + (netBakiye > 0 ? 'var(--green)' : 'var(--accent2)') + ';font-weight:600">₺' + Math.abs(netBakiye).toFixed(0) + ' ' + (netBakiye > 0 ? 'Alacak' : 'Borç') + '</span>' : '') +
                    '</div>' +
                    '</div>' +
                    (m.tel ? '<span class="wa-placeholder" data-tel="x" data-ad="x">📲</span>' : '') +
                    '</div>';

                // WA butonunu düzgün ekle
                if (m.tel) {
                    var placeholder = item.querySelector('.wa-placeholder');
                    if (placeholder) {
                        var waBtn = document.createElement('button');
                        waBtn.className = 'btn btn-whatsapp btn-sm';
                        waBtn.textContent = '📲';
                        (function (tel, ad) {
                            waBtn.addEventListener('click', function (e) { e.stopPropagation(); waMusteri(tel, ad); });
                        })(m.tel, m.ad);
                        placeholder.replaceWith(waBtn);
                    }
                }
                el.appendChild(item);
            });
        }

        function deleteMusteri(id) {
            if (!confirm('Bu müşteriyi silmek istediğinize emin misiniz?')) return;
            state.musteriler = state.musteriler.filter(function (m) { return m.id !== id; });
            saveState();
            renderMusteriler();
        }

        function waMusteri(tel, ad) {
            var t = tel.replace(/\D/g, '').replace(/^0/, '');
            window.open('https://wa.me/90' + t + '?text=' + encodeURIComponent('Sayın ' + ad + ', servisiniz hakkında bilgi vermek istedik.'));
        }

        // --- FATURA ---
        let aktivFaturaServisId = null;
        function faturaCikart(id) {
            const s = state.servisler.find(x => x.id === id);
            if (!s) return;
            aktivFaturaServisId = id;
            const isletme = (state.ayarlar && state.ayarlar.isletmeAd) ? state.ayarlar.isletmeAd : 'Düka Enerji';
            const isletmeTel = (state.ayarlar && state.ayarlar.isletmeTel) ? state.ayarlar.isletmeTel : '';
            const tarih = new Date(s.tarih).toLocaleDateString('tr-TR');
            const parcalarHtml = s.parcalar && s.parcalar.length
                ? s.parcalar.map(function (p) {
                    return '<tr><td style="padding:5px 8px;border-bottom:1px solid #eee">' + p.ad + '</td><td style="padding:5px 8px;border-bottom:1px solid #eee;text-align:center">' + p.adet + ' adet</td></tr>';
                }).join('')
                : '<tr><td colspan="2" style="padding:5px 8px;color:#999;font-style:italic">Parça kullanılmadı</td></tr>';

            document.getElementById('fatura-content').innerHTML =
                '<div style="font-family:Arial,sans-serif;color:#111;max-width:320px;margin:0 auto">' +
                // LOGO + BAŞLIK
                '<div style="text-align:center;padding-bottom:12px;border-bottom:2px solid #111;margin-bottom:14px">' +
                '<img src="data:image/png;base64,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" style="width:70px;height:70px;object-fit:contain;border-radius:8px;background:#111;padding:4px">' +
                '<div style="font-size:20px;font-weight:900;letter-spacing:2px;margin-top:6px">' + isletme.toUpperCase() + '</div>' +
                (isletmeTel ? '<div style="font-size:12px;color:#555;margin-top:2px">📞 ' + isletmeTel + '</div>' : '') +
                '</div>' +
                // MÜŞTERİ & TARİH
                '<div style="display:flex;justify-content:space-between;margin-bottom:12px">' +
                '<div><div style="font-size:10px;color:#888;text-transform:uppercase;letter-spacing:1px">Müşteri</div><div style="font-size:13px;font-weight:700">' + s.musteri + '</div></div>' +
                '<div style="text-align:right"><div style="font-size:10px;color:#888;text-transform:uppercase;letter-spacing:1px">Tarih</div><div style="font-size:13px;font-weight:700">' + tarih + '</div></div>' +
                '</div>' +
                // CİHAZ BİLGİSİ
                '<div style="background:#f5f5f5;border-radius:8px;padding:10px 12px;margin-bottom:12px">' +
                '<div style="font-size:10px;color:#888;text-transform:uppercase;letter-spacing:1px;margin-bottom:4px">Cihaz Bilgisi</div>' +
                '<div style="font-size:13px;font-weight:700">' + s.alet + (s.marka ? ' / ' + s.marka : '') + '</div>' +
                (s.ariza ? '<div style="font-size:12px;color:#555;margin-top:3px">Arıza: ' + s.ariza + '</div>' : '') +
                (s.not ? '<div style="font-size:12px;color:#555;margin-top:3px">Not: ' + s.not + '</div>' : '') +
                '</div>' +
                // KULLANILAN PARÇALAR
                '<div style="margin-bottom:12px">' +
                '<div style="font-size:10px;color:#888;text-transform:uppercase;letter-spacing:1px;margin-bottom:6px">Kullanılan Parçalar</div>' +
                '<table style="width:100%;font-size:12px;border-collapse:collapse">' +
                '<tbody>' + parcalarHtml + '</tbody>' +
                '</table>' +
                '</div>' +
                // TAMİR ÜCRETİ
                '<div style="border-top:2px solid #111;padding-top:10px;display:flex;justify-content:space-between;align-items:center">' +
                '<span style="font-size:14px;font-weight:900;letter-spacing:1px">TAMİR ÜCRETİ</span>' +
                '<span style="font-size:22px;font-weight:900">₺' + parseFloat(s.ucret || 0).toFixed(0) + '</span>' +
                '</div>' +
                // TEŞEKKÜR
                '<div style="text-align:center;margin-top:14px;padding-top:10px;border-top:1px dashed #ccc;font-size:11px;color:#888">Bizi tercih ettiğiniz için teşekkürler 🙏</div>' +
                '</div>';
            openModal('fatura-modal');
        }

        function fisResimCek(callback) {
            const el = document.getElementById('fatura-content');
            html2canvas(el, {
                backgroundColor: '#ffffff',
                scale: 2,
                useCORS: true,
                allowTaint: true
            }).then(function (canvas) {
                callback(canvas);
            }).catch(function (err) {
                alert('Resim oluşturulamadı: ' + err);
            });
        }

        function fisResimIndir() {
            fisResimCek(function (canvas) {
                const link = document.createElement('a');
                link.download = 'fis-' + Date.now() + '.png';
                link.href = canvas.toDataURL('image/png');
                link.click();
            });
        }

        function fisWAPaylas() {
            const s = state.servisler.find(function (x) { return x.id === aktivFaturaServisId; });
            fisResimCek(function (canvas) {
                canvas.toBlob(function (blob) {
                    // Web Share API ile paylaş (mobilde çalışır)
                    if (navigator.share && navigator.canShare) {
                        const file = new File([blob], 'fis.png', { type: 'image/png' });
                        if (navigator.canShare({ files: [file] })) {
                            navigator.share({
                                files: [file],
                                title: 'Servis Fişi',
                                text: s ? 'Sayın ' + s.musteri + ', servis fişiniz ekte.' : 'Servis fişi'
                            }).catch(function (e) { if (e.name !== 'AbortError') alert('Paylaşım hatası: ' + e); });
                            return;
                        }
                    }
                    // Mobil değilse veya share API yoksa indir
                    const url = URL.createObjectURL(blob);
                    const link = document.createElement('a');
                    link.href = url;
                    link.download = 'fis.png';
                    link.click();
                    URL.revokeObjectURL(url);
                    alert('Fiş indirildi! WhatsApp\'ta müşteriye gönderebilirsiniz.');
                }, 'image/png');
            });
        }

        function faturayiWAGonder() { fisWAPaylas(); }

        function renderGrafik() {
            const aylar = {};
            if (state.satislar) {
                state.satislar.forEach(function (s) {
                    const d = new Date(s.tarih);
                    const key = d.getFullYear() + '-' + (d.getMonth() + 1).toString().padStart(2, '0');
                    if (!aylar[key]) aylar[key] = { gelir: 0, maliyet: 0, adet: 0 };
                    if (s.tur === 'satis') aylar[key].gelir += s.toplam;
                    else aylar[key].maliyet += s.toplam;
                });
            }
            if (state.giderler) {
                state.giderler.forEach(function (g) {
                    const d = new Date(g.tarih);
                    const key = d.getFullYear() + '-' + (d.getMonth() + 1).toString().padStart(2, '0');
                    if (!aylar[key]) aylar[key] = { gelir: 0, maliyet: 0, adet: 0 };
                    aylar[key].maliyet += g.tutar;
                });
            }
            state.servisler.forEach(s => {
                const d = new Date(s.tarih);
                const key = d.getFullYear() + '-' + (d.getMonth() + 1).toString().padStart(2, '0');
                if (!aylar[key]) aylar[key] = { gelir: 0, maliyet: 0, adet: 0 };
                aylar[key].gelir += parseFloat(s.ucret || 0);
                aylar[key].maliyet += parseFloat(s.maliyet || 0);
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
                const val = Math.round(maxVal * (1 - i / 4));
                ctx.fillStyle = '#666'; ctx.font = '10px IBM Plex Sans'; ctx.textAlign = 'right';
                ctx.fillText('₺' + val, padL - 4, y + 3);
            }

            // Bars
            keys.forEach((k, i) => {
                const x = padL + i * barW;
                const gelir = aylar[k].gelir;
                const kar = karlar[i];

                // Gelir bar
                const gelirH = (gelir / maxVal) * chartH;
                ctx.fillStyle = '#f59e0b44';
                ctx.fillRect(x + barW * 0.1, padT + chartH - gelirH, barW * 0.38, gelirH);

                // Kar bar
                const karH = Math.abs(kar) / maxVal * chartH;
                ctx.fillStyle = kar >= 0 ? '#22c55e88' : '#ef444488';
                ctx.fillRect(x + barW * 0.52, padT + chartH - (kar >= 0 ? karH : 0) - (kar < 0 ? 0 : 0), barW * 0.38, karH);

                // X label
                const [y, m] = k.split('-');
                ctx.fillStyle = '#888'; ctx.font = '10px IBM Plex Sans'; ctx.textAlign = 'center';
                ctx.fillText(m + '/' + y.slice(2), x + barW / 2, H - padB + 14);
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
      <td style="text-align:right;padding:8px 6px;color:${kar >= 0 ? 'var(--green)' : 'var(--accent2)'}">₺${kar.toFixed(0)}</td>
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
                callback: function (resp) {
                    if (resp.error) { if (!sessiz) alert('Giris basarisiz: ' + resp.error); return; }
                    gdriveToken = resp.access_token;
                    // Token süresini kaydet (55 dakika)
                    const expire = Date.now() + 55 * 60 * 1000;
                    try { localStorage.setItem('gdrive_token', resp.access_token); localStorage.setItem('gdrive_expire', expire); } catch (e) { }
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
            } catch (e) { }
            return false;
        }

        function driveCikis() {
            gdriveToken = null;
            gdriveFileId = null;
            try { localStorage.removeItem('gdrive_token'); localStorage.removeItem('gdrive_expire'); } catch (e) { }
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
            } catch (e) {
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
            } catch (e) {
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
            const a = aciklama.toLowerCase().replace(/[ğüşıöç]/g, function (c) {
                return { g: 'g', u: 'u', s: 's', i: 'i', o: 'o', c: 'c' }[c] || c;
            });
            for (const kat in KATEGORI_ANAHTAR) {
                if (KATEGORI_ANAHTAR[kat].some(function (k) { return a.includes(k); })) return kat;
            }
            return 'diger';
        }

        function kategoriLabel(k) {
            return { kira: '🏠 Kira', fatura: '💡 Fatura', personel: '👤 Personel', malzeme: '🔩 Malzeme', diger: '📌 Diğer' }[k] || k;
        }

        // Açıklama yazınca otomatik kategori seç
        document.addEventListener('DOMContentLoaded', function () {
            const gAciklama = document.getElementById('g-aciklama');
            if (gAciklama) {
                gAciklama.addEventListener('input', function () {
                    const kat = kategoriTahmin(this.value);
                    document.getElementById('g-kategori').value = kat;
                });
            }
        });

        let giderFilter = 'hepsi';

        function filterGider(f) {
            giderFilter = f;
            document.querySelectorAll('#gider-filters .filter-btn').forEach(function (b) { b.classList.remove('active'); });
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
            ['g-aciklama', 'g-tutar', 'g-odeme'].forEach(function (id) { document.getElementById(id).value = ''; });
            document.getElementById('g-kategori').value = 'diger';
            closeModal('gider-modal');
            renderGider();
            // Kasaya yansıt
            setTimeout(function () {
                kasaSecModal('Gider ₺' + tutar.toFixed(0) + ' hangi kasadan ödensin?', function (kasaId) {
                    kasaHareketEkle(kasaId, 'cikis', aciklama, tutar, '');
                    saveState();
                    renderKasa();
                });
            }, 300);
        }

        function renderGider() {
            if (!state.giderler) state.giderler = [];
            const q = (document.getElementById('gider-search') ? document.getElementById('gider-search').value : '').toLowerCase();
            let list = state.giderler.filter(function (g) {
                if (giderFilter !== 'hepsi' && g.kategori !== giderFilter) return false;
                if (q && !g.aciklama.toLowerCase().includes(q)) return false;
                return true;
            }).reverse();

            const buAy = new Date();
            const ayGider = state.giderler.filter(function (g) {
                const d = new Date(g.tarih);
                return d.getMonth() === buAy.getMonth() && d.getFullYear() === buAy.getFullYear();
            }).reduce(function (a, g) { return a + g.tutar; }, 0);
            const toplamGider = state.giderler.reduce(function (a, g) { return a + g.tutar; }, 0);

            document.getElementById('gider-stats').innerHTML =
                '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">TL' + ayGider.toFixed(0) + '</div><div class="stat-label">Bu Ay Gider</div></div>' +
                '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">TL' + toplamGider.toFixed(0) + '</div><div class="stat-label">Toplam Gider</div></div>';

            if (list.length === 0) {
                document.getElementById('gider-list').innerHTML = '<div class="empty"><div class="empty-icon">📉</div><div>Gider kaydi yok</div></div>';
                return;
            }
            document.getElementById('gider-list').innerHTML = list.map(function (g) {
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
            state.giderler = state.giderler.filter(function (g) { return g.id !== id; });
            saveState();
            renderGider();
        }

        // --- KASA ---
        let kasaFilter = 'hepsi';
        let _kasaSecCallback = null; // Kasa seç modal callback

        // Varsayılan kasaları oluştur
        function kasalariBaslat() {
            if (!state.kasalar) state.kasalar = [];
            if (state.kasalar.length === 0) {
                state.kasalar = [
                    { id: 1, ad: 'Nakit Kasa', baslangic: 0, tarih: new Date().toISOString() },
                    { id: 2, ad: 'Banka', baslangic: 0, tarih: new Date().toISOString() }
                ];
                saveState();
            }
        }

        function kasaBakiyeHesapla(kasaId) {
            const k = state.kasalar.find(function (x) { return x.id === kasaId; });
            const baslangic = k ? (k.baslangic || 0) : 0;
            const hareketler = (state.kasa || []).filter(function (h) { return h.kasaId === kasaId; });
            return baslangic + hareketler.reduce(function (a, h) {
                if (h.tur === 'giris') return a + h.tutar;
                if (h.tur === 'cikis') return a - h.tutar;
                if (h.tur === 'transfer-giris') return a + h.tutar;
                if (h.tur === 'transfer-cikis') return a - h.tutar;
                return a;
            }, 0);
        }

        function kasaSelectDoldur(elId, seciliId) {
            const el = document.getElementById(elId);
            if (!el) return;
            el.innerHTML = state.kasalar.map(function (k) {
                return '<option value="' + k.id + '"' + (k.id === seciliId ? ' selected' : '') + '>' + k.ad + ' — ₺' + kasaBakiyeHesapla(k.id).toFixed(0) + '</option>';
            }).join('');
        }

        // Kasa seç modal (satış/servis için)
        function kasaSecModal(aciklama, callback) {
            kasalariBaslat();
            _kasaSecCallback = callback;
            document.getElementById('kasa-sec-aciklama').textContent = aciklama;
            kasaSelectDoldur('kasa-sec-id');
            document.getElementById('kasa-sec-modal').classList.add('active');
        }

        // Genel ödeme seç: kasaya mı veresiyeye mi
        function odemeSecModal(baslik, tutar, musteriAd, aciklama, islemTuru = 'satis', extraNot = '') {
            kasalariBaslat();
            // Basit: önce kasa seç, veresiye seçeneği de sunulacak
            const islemMetni = islemTuru === 'satis' ? 'Kasaya ekle (Tahsilat)' : 'Kasadan öde (Nakit Çıkış)';
            const sahisMetni = islemTuru === 'satis' ? 'Müşteri: ' : 'Tedarikçi: ';
            const secenek = confirm(baslik + '\n\n"Tamam" = ' + islemMetni + '\n"İptal" = Veresiye / Cariye yaz\n\n' + sahisMetni + musteriAd);
            if (secenek) {
                kasaSecModal(baslik + (islemTuru === 'satis' ? ' hangi kasaya?' : ' hangi kasadan?'), function (kasaId) {
                    const kasaTur = islemTuru === 'satis' ? 'giris' : 'cikis';
                    kasaHareketEkle(kasaId, kasaTur, musteriAd + ' - ' + aciklama, tutar, extraNot);
                    saveState();
                    renderKasa();
                });
            } else {
                // Cariye yaz
                if (!state.cari) state.cari = [];
                const cariTur = islemTuru === 'satis' ? 'alacak' : 'borc';
                state.cari.push({
                    id: Date.now(),
                    isim: musteriAd,
                    tur: cariTur,
                    tutar: tutar,
                    aciklama: aciklama + ' (veresiye)',
                    tarih: new Date().toISOString()
                });
                saveState();
                renderCari();
                if (islemTuru === 'satis') {
                    alert(musteriAd + ' adına ₺' + tutar.toFixed(0) + ' cari alacak açıldı!');
                } else {
                    alert(musteriAd + ' adına ₺' + tutar.toFixed(0) + ' cari borç açıldı (Ödenecek)!');
                }
            }
        }

        function kasaSecOnayla() {
            const kasaId = parseInt(document.getElementById('kasa-sec-id').value);
            closeModal('kasa-sec-modal');
            if (_kasaSecCallback) _kasaSecCallback(kasaId);
            _kasaSecCallback = null;
        }

        // --- ÖDEME SİSTEMİ ---
        let _odemeServis = null;
        let _odemeKalemler = [];

        function odemeModalAc(servis) {
            kasalariBaslat();
            _odemeServis = servis;
            _odemeKalemler = [];
            const ucret = parseFloat(servis.ucret) || 0;
            document.getElementById('odeme-servis-bilgi').innerHTML =
                '<b>' + servis.musteri + '</b> — ' + servis.alet + (servis.marka ? ' / ' + servis.marka : '');
            document.getElementById('odeme-toplam').textContent = '₺' + ucret.toFixed(0);
            kasaSelectDoldur('op-kasa-id');
            document.getElementById('op-tutar').value = ucret.toFixed(0);
            renderOdemeKalemler();
            document.getElementById('odeme-modal').classList.add('active');
        }

        function odemeYontemDegis() {
            const yontem = document.getElementById('op-yontem').value;
            const kasaGroup = document.getElementById('op-kasa-group');
            const tutarGroup = document.getElementById('op-tutar-group');
            if (yontem === 'veresiye' || yontem === 'ucretsiz') {
                kasaGroup.style.display = 'none';
                if (yontem === 'ucretsiz') tutarGroup.style.display = 'none';
                else tutarGroup.style.display = 'block';
            } else {
                kasaGroup.style.display = 'block';
                tutarGroup.style.display = 'block';
            }
        }

        function odemeKalemEkle() {
            const yontem = document.getElementById('op-yontem').value;
            const ucret = parseFloat(_odemeServis.ucret) || 0;
            const odenmis = _odemeKalemler.reduce(function (a, k) { return a + k.tutar; }, 0);
            const kalan = ucret - odenmis;

            if (yontem === 'ucretsiz') {
                _odemeKalemler = [{ yontem: 'ucretsiz', tutar: ucret, kasaId: null, label: '🎁 Ücretsiz' }];
                renderOdemeKalemler();
                return;
            }

            const tutar = parseFloat(document.getElementById('op-tutar').value) || 0;
            if (!tutar) { alert('Tutar giriniz'); return; }
            if (tutar > kalan + 0.01) { alert('Kalan tutardan fazla girilemez! Kalan: ₺' + kalan.toFixed(0)); return; }

            const kasaId = yontem !== 'veresiye' ? parseInt(document.getElementById('op-kasa-id').value) : null;
            const kasaAd = kasaId ? (state.kasalar.find(function (k) { return k.id === kasaId; }) || { ad: '?' }).ad : '';
            const label = yontem === 'nakit' ? '💵 Nakit' :
                yontem === 'kredi' ? '💳 Kredi' :
                    yontem === 'havale' ? '🏧 Havale' : '📋 Veresiye';

            _odemeKalemler.push({ yontem, tutar, kasaId, label: label + (kasaAd ? ' (' + kasaAd + ')' : '') });
            renderOdemeKalemler();
            // Kalan tutarı otomatik doldur
            const yeniKalan = ucret - _odemeKalemler.reduce(function (a, k) { return a + k.tutar; }, 0);
            document.getElementById('op-tutar').value = yeniKalan > 0 ? yeniKalan.toFixed(0) : '';
        }

        function odemeKalemSil(i) {
            _odemeKalemler.splice(i, 1);
            renderOdemeKalemler();
            const ucret = parseFloat(_odemeServis.ucret) || 0;
            const odenmis = _odemeKalemler.reduce(function (a, k) { return a + k.tutar; }, 0);
            document.getElementById('op-tutar').value = (ucret - odenmis).toFixed(0);
        }

        function renderOdemeKalemler() {
            const ucret = parseFloat(_odemeServis ? _odemeServis.ucret : 0) || 0;
            const odenmis = _odemeKalemler.reduce(function (a, k) { return a + k.tutar; }, 0);
            const kalan = ucret - odenmis;
            document.getElementById('odeme-kalan').textContent = '₺' + kalan.toFixed(0);
            document.getElementById('odeme-kalan').style.color = kalan <= 0 ? 'var(--green)' : 'var(--accent2)';

            const el = document.getElementById('odeme-kalemler');
            if (_odemeKalemler.length === 0) { el.innerHTML = ''; return; }
            el.innerHTML = _odemeKalemler.map(function (k, i) {
                return '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:6px;padding:8px 12px;margin-bottom:6px">' +
                    '<span style="font-size:13px">' + k.label + '</span>' +
                    '<div style="display:flex;align-items:center;gap:8px">' +
                    '<span style="font-weight:700;color:var(--green)">₺' + k.tutar.toFixed(0) + '</span>' +
                    '<button onclick="odemeKalemSil(' + i + ')" style="background:none;border:none;color:var(--accent2);font-size:16px;cursor:pointer">✕</button>' +
                    '</div>' +
                    '</div>';
            }).join('');
        }

        function odemeKaydet() {
            if (!_odemeServis) return;
            if (_odemeKalemler.length === 0) { alert('En az bir ödeme yöntemi ekleyiniz'); return; }
            const ucret = parseFloat(_odemeServis.ucret) || 0;
            const odenmis = _odemeKalemler.reduce(function (a, k) { return a + k.tutar; }, 0);

            _odemeKalemler.forEach(function (k) {
                if (k.yontem === 'ucretsiz') return;
                if (k.yontem === 'veresiye') {
                    // Cari'ye borç yaz
                    if (!state.cari) state.cari = [];
                    state.cari.push({
                        id: Date.now() + Math.random(),
                        isim: _odemeServis.musteri || 'Anonim',
                        tur: 'alacak',
                        tutar: k.tutar,
                        aciklama: _odemeServis.alet + ' tamir ücreti (veresiye)',
                        tarih: new Date().toISOString()
                    });
                } else {
                    // Kasaya ekle
                    kasaHareketEkle(k.kasaId, 'giris',
                        _odemeServis.musteri + ' - ' + _odemeServis.alet + ' (' + k.label + ')',
                        k.tutar, '');
                }
            });

            saveState();
            closeModal('odeme-modal');
            _odemeServis = null;
            _odemeKalemler = [];
            renderKasa();
            renderCari();
        }

        function kasaHareketEkle(kasaId, tur, aciklama, tutar, not) {
            if (!state.kasa) state.kasa = [];
            state.kasa.push({
                id: Date.now() + Math.floor(Math.random() * 1000),
                kasaId: kasaId,
                tur: tur,
                aciklama: aciklama,
                tutar: tutar,
                not: not || '',
                tarih: new Date().toISOString()
            });
        }

        function kasaEkle() {
            const ad = document.getElementById('yeni-kasa-ad').value.trim();
            const baslangic = parseFloat(document.getElementById('yeni-kasa-bakiye').value) || 0;
            if (!ad) { alert('Kasa adı giriniz'); return; }
            const yeniId = Date.now();
            state.kasalar.push({ id: yeniId, ad: ad, baslangic: baslangic, tarih: new Date().toISOString() });
            saveState();
            document.getElementById('yeni-kasa-ad').value = '';
            document.getElementById('yeni-kasa-bakiye').value = '';
            renderKasaYonet();
        }

        function kasaSil(id) {
            const hareketVar = (state.kasa || []).some(function (h) { return h.kasaId === id; });
            if (hareketVar) { alert('Bu kasada hareket var, silinemez!'); return; }
            if (!confirm('Kasayı silmek istiyor musunuz?')) return;
            state.kasalar = state.kasalar.filter(function (k) { return k.id !== id; });
            saveState();
            renderKasaYonet();
            renderKasa();
        }

        function kasaBakiyeAyarla(id) {
            const k = state.kasalar.find(function (x) { return x.id === id; });
            if (!k) return;
            const yeni = prompt(k.ad + ' başlangıç bakiyesini girin:', k.baslangic || 0);
            if (yeni === null) return;
            k.baslangic = parseFloat(yeni) || 0;
            saveState();
            renderKasaYonet();
            renderKasa();
        }

        function renderKasaYonet() {
            kasalariBaslat();
            const el = document.getElementById('kasa-yonet-list');
            if (!el) return;
            if (state.kasalar.length === 0) {
                el.innerHTML = '<div style="color:var(--muted);font-size:13px">Henüz kasa yok</div>';
                return;
            }
            el.innerHTML = state.kasalar.map(function (k) {
                const bakiye = kasaBakiyeHesapla(k.id);
                return '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:8px;padding:12px;margin-bottom:8px">' +
                    '<div>' +
                    '<div style="font-weight:600;font-size:14px">' + k.ad + '</div>' +
                    '<div style="font-size:12px;color:' + (bakiye >= 0 ? 'var(--green)' : 'var(--accent2)') + ';font-weight:700">₺' + bakiye.toFixed(0) + '</div>' +
                    '</div>' +
                    '<div style="display:flex;gap:6px">' +
                    '<button class="btn btn-ghost btn-sm" onclick="kasaBakiyeAyarla(' + k.id + ')">✏️ Bakiye</button>' +
                    '<button class="btn btn-danger btn-sm" onclick="kasaSil(' + k.id + ')">🗑️</button>' +
                    '</div>' +
                    '</div>';
            }).join('');
        }

        function saveTransfer() {
            const cikisId = parseInt(document.getElementById('tr-cikis').value);
            const girisId = parseInt(document.getElementById('tr-giris').value);
            const tutar = parseFloat(document.getElementById('tr-tutar').value) || 0;
            const not = document.getElementById('tr-not').value.trim();
            if (cikisId === girisId) { alert('Aynı kasaya transfer yapılamaz!'); return; }
            if (!tutar) { alert('Tutar giriniz'); return; }
            const cikisKasa = state.kasalar.find(function (k) { return k.id === cikisId; });
            const girisKasa = state.kasalar.find(function (k) { return k.id === girisId; });
            if (kasaBakiyeHesapla(cikisId) < tutar) { alert('Yetersiz bakiye!'); return; }
            const zaman = new Date().toISOString();
            const transferId = Date.now();
            if (!state.kasa) state.kasa = [];
            state.kasa.push({ id: transferId, kasaId: cikisId, tur: 'transfer-cikis', aciklama: girisKasa.ad + ' kasasına transfer', tutar: tutar, not: not, tarih: zaman });
            state.kasa.push({ id: transferId + 1, kasaId: girisId, tur: 'transfer-giris', aciklama: cikisKasa.ad + ' kasasından transfer', tutar: tutar, not: not, tarih: zaman });
            saveState();
            document.getElementById('tr-tutar').value = '';
            document.getElementById('tr-not').value = '';
            closeModal('transfer-modal');
            renderKasa();
        }

        function filterKasa(f) {
            kasaFilter = f;
            document.querySelectorAll('#kasa-filters .filter-btn').forEach(function (b) { b.classList.remove('active'); });
            event.target.classList.add('active');
            renderKasa();
        }

        function saveKasa() {
            const aciklama = document.getElementById('k-aciklama').value.trim();
            const tutar = parseFloat(document.getElementById('k-tutar').value) || 0;
            if (!aciklama) { alert('Açıklama giriniz'); return; }
            if (!tutar) { alert('Tutar giriniz'); return; }
            const kasaId = parseInt(document.getElementById('k-kasa-id').value);
            kasaHareketEkle(kasaId, document.getElementById('k-tur').value, aciklama, tutar, document.getElementById('k-not').value.trim());
            saveState();
            ['k-aciklama', 'k-tutar', 'k-not'].forEach(function (id) { document.getElementById(id).value = ''; });
            document.getElementById('k-tur').value = 'giris';
            closeModal('kasa-modal');
            renderKasa();
        }

        function renderKasa() {
            kasalariBaslat();
            if (!state.kasa) state.kasa = [];

            // Kasa kartları
            const kasaKartlar = state.kasalar.map(function (k) {
                const bakiye = kasaBakiyeHesapla(k.id);
                return '<div style="background:var(--surface);border:1px solid ' + (bakiye < 0 ? 'var(--accent2)' : 'var(--border)') + ';border-radius:var(--radius);padding:14px;flex:1;min-width:130px;text-align:center">' +
                    '<div style="font-size:11px;color:var(--muted);text-transform:uppercase;margin-bottom:4px">' + k.ad + '</div>' +
                    '<div style="font-family:sans-serif;font-weight:700;font-size:26px;color:' + (bakiye >= 0 ? 'var(--green)' : 'var(--accent2)') + '">₺' + bakiye.toFixed(0) + '</div>' +
                    '</div>';
            }).join('');

            const toplamBakiye = state.kasalar.reduce(function (a, k) { return a + kasaBakiyeHesapla(k.id); }, 0);

            document.getElementById('kasa-bakiye-card').innerHTML =
                '<div class="card">' +
                '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">' +
                '<div style="font-size:12px;color:var(--muted);text-transform:uppercase;letter-spacing:1px">Toplam Bakiye</div>' +
                '<div style="font-family:sans-serif;font-weight:700;font-size:30px;color:' + (toplamBakiye >= 0 ? 'var(--green)' : 'var(--accent2)') + '">₺' + toplamBakiye.toFixed(0) + '</div>' +
                '</div>' +
                '<div style="display:flex;gap:8px;flex-wrap:wrap">' + kasaKartlar + '</div>' +
                '</div>';

            // Günlük özet
            const bugun = new Date().toDateString();
            const bugunHareketler = state.kasa.filter(function (k) { return new Date(k.tarih).toDateString() === bugun; });
            const bugunGiris = bugunHareketler.filter(function (k) { return k.tur === 'giris'; }).reduce(function (a, k) { return a + k.tutar; }, 0);
            const bugunCikis = bugunHareketler.filter(function (k) { return k.tur === 'cikis'; }).reduce(function (a, k) { return a + k.tutar; }, 0);
            document.getElementById('kasa-gunluk').innerHTML = bugunHareketler.length > 0 ?
                '<div style="display:flex;gap:8px;margin-bottom:4px">' +
                '<div class="stat-card" style="flex:1"><div class="stat-value profit-positive" style="font-size:18px">₺' + bugunGiris.toFixed(0) + '</div><div class="stat-label">Bugün Giriş</div></div>' +
                '<div class="stat-card" style="flex:1"><div class="stat-value profit-negative" style="font-size:18px">₺' + bugunCikis.toFixed(0) + '</div><div class="stat-label">Bugün Çıkış</div></div>' +
                '</div>' : '';

            // Liste filtresi
            let list = state.kasa.filter(function (k) {
                if (kasaFilter === 'giris' && k.tur !== 'giris') return false;
                if (kasaFilter === 'cikis' && k.tur !== 'cikis') return false;
                if (kasaFilter === 'transfer' && k.tur !== 'transfer-giris' && k.tur !== 'transfer-cikis') return false;
                return true;
            }).reverse();

            if (list.length === 0) {
                document.getElementById('kasa-list').innerHTML = '<div class="empty"><div class="empty-icon">🏦</div><div>Hareket kaydı yok</div></div>';
                return;
            }

            document.getElementById('kasa-list').innerHTML = list.map(function (k) {
                const kasaAd = (state.kasalar.find(function (x) { return x.id === k.kasaId; }) || { ad: '?' }).ad;
                const giris = k.tur === 'giris' || k.tur === 'transfer-giris';
                const transfer = k.tur === 'transfer-giris' || k.tur === 'transfer-cikis';
                const renk = transfer ? '#60a5fa' : (giris ? 'var(--green)' : 'var(--accent2)');
                const ikon = transfer ? '🔄' : (giris ? '⬆️' : '⬇️');
                return '<div class="list-item">' +
                    '<div class="list-item-top">' +
                    '<div>' +
                    '<div class="list-item-title">' + ikon + ' ' + k.aciklama + '</div>' +
                    '<div class="list-item-sub">🏦 ' + kasaAd + ' • ' + new Date(k.tarih).toLocaleDateString("tr-TR") + (k.not ? ' • ' + k.not : '') + '</div>' +
                    '</div>' +
                    '<div style="font-weight:700;font-size:16px;color:' + renk + '">' + (giris ? '+' : '-') + '₺' + k.tutar.toFixed(0) + '</div>' +
                    '</div>' +
                    (!transfer ? '<div class="list-item-actions"><button class="btn btn-danger btn-sm" onclick="deleteKasa(' + k.id + ')">🗑️</button></div>' : '') +
                    '</div>';
            }).join('');
        }


        function deleteKasa(id) {
            if (!confirm('Bu kaydi silmek istediginize emin misiniz?')) return;
            state.kasa = state.kasa.filter(function (k) { return k.id !== id; });
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
            document.getElementById('al-stok-ara').value = '';
            document.getElementById('al-stok-oneri').style.display = 'none';
            document.getElementById('alis-modal').classList.add('active');
        }

        function alStokAra() {
            const q = document.getElementById('al-stok-ara').value.toLowerCase();
            const oneriEl = document.getElementById('al-stok-oneri');
            if (!q || q.length < 1) { oneriEl.style.display = 'none'; return; }
            const eslesen = state.stok.filter(function (s) { return s.ad.toLowerCase().includes(q); }).slice(0, 8);
            if (eslesen.length === 0) { oneriEl.style.display = 'none'; return; }
            oneriEl.style.display = 'block';
            oneriEl.innerHTML = '';
            eslesen.forEach(function (s) {
                var div = document.createElement('div');
                div.style.cssText = 'padding:9px 12px;cursor:pointer;font-size:13px;border-bottom:1px solid #2e2e2e';
                div.innerHTML = s.ad + ' <span style="color:#888;font-size:11px">(Mevcut: ' + s.adet + ' adet, Maliyet: ₺' + s.maliyet + ')</span>';
                (function (stok) {
                    div.addEventListener('mousedown', function (e) {
                        e.preventDefault();
                        document.getElementById('al-urun-ad').value = stok.ad;
                        document.getElementById('al-urun-fiyat').value = stok.maliyet;
                        document.getElementById('al-urun-adet').value = 1;
                        document.getElementById('al-stok-ara').value = stok.ad;
                        oneriEl.style.display = 'none';
                        // Stok ID'sini sakla
                        document.getElementById('al-stok-ara').dataset.stokId = stok.id;
                    });
                })(s);
                oneriEl.appendChild(div);
            });
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
            el.innerHTML = '<div style="margin-bottom:10px">' + satKalemler.map(function (k, i) {
                return '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:6px;padding:8px 10px;margin-bottom:6px">' +
                    '<div><div style="font-size:13px;font-weight:600">' + k.ad + '</div>' +
                    '<div style="font-size:11px;color:#888">' + k.adet + ' adet x TL' + k.fiyat + ' = TL' + (k.adet * k.fiyat).toFixed(0) + '</div></div>' +
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
            const stokIdStr = document.getElementById('al-stok-ara').dataset.stokId || '';
            const stokId = stokIdStr ? parseInt(stokIdStr) : null;
            if (!ad) { alert('Ürün adı giriniz'); return; }
            alKalemler.push({ ad, adet, fiyat, stokId });
            document.getElementById('al-urun-ad').value = '';
            document.getElementById('al-urun-fiyat').value = '';
            document.getElementById('al-urun-adet').value = 1;
            document.getElementById('al-stok-ara').value = '';
            document.getElementById('al-stok-ara').dataset.stokId = '';
            document.getElementById('al-stok-oneri').style.display = 'none';
            renderAlKalemler();
        }

        function renderAlKalemler() {
            const el = document.getElementById('al-kalemler-list');
            if (!el) return;
            const toplam = alKalemler.reduce((a, k) => a + k.adet * k.fiyat, 0);
            document.getElementById('al-toplam').textContent = 'TL' + toplam.toFixed(0);
            if (alKalemler.length === 0) { el.innerHTML = ''; return; }
            el.innerHTML = '<div style="margin-bottom:10px">' + alKalemler.map(function (k, i) {
                return '<div style="display:flex;justify-content:space-between;align-items:center;background:var(--surface2);border-radius:6px;padding:8px 10px;margin-bottom:6px">' +
                    '<div><div style="font-size:13px;font-weight:600">' + k.ad + '</div>' +
                    '<div style="font-size:11px;color:#888">' + k.adet + ' adet x TL' + k.fiyat + ' = TL' + (k.adet * k.fiyat).toFixed(0) + '</div></div>' +
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
                kalemler: satKalemler.map(function (k) { return Object.assign({}, k); }),
                toplam,
                not: document.getElementById('sat-not').value.trim(),
                tarih: new Date().toISOString()
            };
            // Stoktan dus
            satKalemler.forEach(function (k) {
                if (k.stokId) {
                    const s = state.stok.find(function (x) { return x.id === k.stokId; });
                    if (s) s.adet = Math.max(0, s.adet - k.adet);
                }
            });
            state.satislar.push(kayit);
            saveState();
            satKalemler = [];
            const _satMusteri = document.getElementById('sat-musteri').value.trim() || 'Anonim';
            document.getElementById('sat-musteri').value = '';
            document.getElementById('sat-not').value = '';
            closeModal('satis-modal');
            renderSatis();
            // Ödeme seçeneği sun
            setTimeout(function () {
                odemeSecModal('Satış ₺' + toplam.toFixed(0), toplam, _satMusteri, kayit.kalemler.map(function (k) { return k.ad; }).join(', '), 'satis', kayit.not || '');
            }, 300);
        }

        function saveAlis() {
            if (alKalemler.length === 0) { alert('En az bir urun ekleyin'); return; }
            const toplam = alKalemler.reduce((a, k) => a + k.adet * k.fiyat, 0);
            const kayit = {
                id: Date.now(),
                tur: 'alis',
                tedarikci: document.getElementById('al-tedarikci').value.trim() || 'Belirsiz',
                kalemler: alKalemler.map(function (k) { return Object.assign({}, k); }),
                toplam,
                not: document.getElementById('al-not').value.trim(),
                tarih: new Date().toISOString()
            };
            // Stoka ekle
            alKalemler.forEach(function (k) {
                if (k.stokId) {
                    // Stok ID ile bul
                    const s = state.stok.find(function (x) { return x.id === k.stokId; });
                    if (s) { s.adet += k.adet; return; }
                }
                // İsimle bul
                const s = state.stok.find(function (x) { return x.ad.toLowerCase() === k.ad.toLowerCase(); });
                if (s) s.adet += k.adet;
            });
            state.satislar.push(kayit);
            saveState();
            alKalemler = [];
            const _alTedarikci = kayit.tedarikci;
            document.getElementById('al-tedarikci').value = '';
            document.getElementById('al-not').value = '';
            closeModal('alis-modal');
            renderSatis();
            // Hangi kasadan çıkış sorusu veya veresiye seçeneği
            setTimeout(function () {
                odemeSecModal('Alış ₺' + toplam.toFixed(0), toplam, _alTedarikci, kayit.kalemler.map(function (k) { return k.ad; }).join(', '), 'alis', kayit.not || '');
            }, 300);
        }

        function filterSatis(f) {
            saatisFilter = f;
            document.querySelectorAll('#satis-filters .filter-btn').forEach(function (b) { b.classList.remove('active'); });
            event.target.classList.add('active');
            renderSatis();
        }

        function renderSatis() {
            if (!state.satislar) state.satislar = [];
            const q = (document.getElementById('satis-search') ? document.getElementById('satis-search').value : '').toLowerCase();
            let list = state.satislar.filter(function (s) {
                if (saatisFilter === 'satis' && s.tur !== 'satis') return false;
                if (saatisFilter === 'alis' && s.tur !== 'alis') return false;
                if (q && !(s.musteri || s.tedarikci || '').toLowerCase().includes(q) &&
                    !s.kalemler.some(function (k) { return k.ad.toLowerCase().includes(q); })) return false;
                return true;
            }).reverse();

            const toplamSatis = state.satislar.filter(function (s) { return s.tur === 'satis'; }).reduce(function (a, s) { return a + s.toplam; }, 0);
            const toplamAlis = state.satislar.filter(function (s) { return s.tur === 'alis'; }).reduce(function (a, s) { return a + s.toplam; }, 0);

            document.getElementById('satis-stats').innerHTML =
                '<div class="stat-card"><div class="stat-value profit-positive" style="font-size:20px">TL' + toplamSatis.toFixed(0) + '</div><div class="stat-label">Toplam Satis</div></div>' +
                '<div class="stat-card"><div class="stat-value profit-negative" style="font-size:20px">TL' + toplamAlis.toFixed(0) + '</div><div class="stat-label">Toplam Alis</div></div>';

            if (list.length === 0) {
                document.getElementById('satis-list').innerHTML = '<div class="empty"><div class="empty-icon">🛒</div><div>Kayit bulunamadi</div></div>';
                return;
            }

            document.getElementById('satis-list').innerHTML = list.map(function (s) {
                const baslik = s.tur === 'satis' ? (s.musteri || 'Anonim') : (s.tedarikci || 'Belirsiz');
                const kalemOzet = s.kalemler.map(function (k) { return k.ad + ' x' + k.adet; }).join(', ');
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
            state.satislar = state.satislar.filter(function (s) { return s.id !== id; });
            saveState();
            renderSatis();
        }

        // --- INIT ---
        loadState();
        kasalariBaslat();
        // Firebase hazır olunca veriyi çek
        // --- YEDEK SİSTEMİ ---
        function yedegiIndir() {
            const tarih = new Date().toLocaleDateString('tr-TR').replace(/\./g, '-');
            const veri = JSON.stringify(state, null, 2);
            const blob = new Blob([veri], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'duka-yedek-' + tarih + '.json';
            a.click();
            URL.revokeObjectURL(url);
            // Son yedek tarihini kaydet
            localStorage.setItem('son_yedek', new Date().toDateString());
        }

        function yedekKontrol() {
            const sonYedek = localStorage.getItem('son_yedek');
            const bugun = new Date().toDateString();
            if (sonYedek === bugun) return;
            const veriVar = state.servisler.length > 0 || state.satislar.length > 0 ||
                state.giderler.length > 0 || state.musteriler.length > 0;
            if (!veriVar) return;
            const uyari = document.getElementById('yedek-uyari');
            if (!uyari) return;
            uyari.style.display = 'block';
            var div = document.createElement('div');
            div.style.cssText = 'background:#3b82f622;border:1px solid #3b82f666;border-radius:10px;padding:12px 14px;display:flex;justify-content:space-between;align-items:center;margin-bottom:12px';
            div.innerHTML = '<div><div style="font-weight:700;color:#60a5fa;margin-bottom:2px">💾 Günlük Yedek</div><div style="font-size:12px;color:var(--muted)">Verilerinizi yedeklemek ister misiniz?</div></div><div id="yedek-btn-grup" style="display:flex;gap:6px"></div>';
            uyari.innerHTML = '';
            uyari.appendChild(div);
            var indirBtn = document.createElement('button');
            indirBtn.className = 'btn btn-primary btn-sm';
            indirBtn.textContent = '⬇️ İndir';
            indirBtn.addEventListener('click', function () { yedegiIndir(); uyari.innerHTML = ''; uyari.style.display = 'none'; });
            var atlaBtn = document.createElement('button');
            atlaBtn.className = 'btn btn-ghost btn-sm';
            atlaBtn.textContent = 'Atla';
            atlaBtn.addEventListener('click', function () { localStorage.setItem('son_yedek', new Date().toDateString()); uyari.innerHTML = ''; uyari.style.display = 'none'; });
            var grup = div.querySelector('#yedek-btn-grup');
            grup.appendChild(indirBtn);
            grup.appendChild(atlaBtn);
        }

        function initFirebase() {
            if (!window._firebaseReady) {
                const el = document.getElementById('firebase-durum');
                if (el) { el.textContent = '🟡'; el.title = 'Bağlanıyor...'; }
                setTimeout(initFirebase, 300);
                return;
            }
            firebaseLoad().then(function (yuklendi) {
                // Varsayılan stok sadece Firebase'den veri gelmedi VE stok boşsa yükle
                if (state.stok.length === 0) {
                    state.stok = [{ "id": 1, "ad": "40N120 Mosfet", "adet": 29, "maliyet": 85.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 2, "ad": "4V 4 AH Kuru Akü", "adet": 0, "maliyet": 200.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 3, "ad": "Stanley 160A Kaynak Makinesi", "adet": 1, "maliyet": 7500.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 4, "ad": "Taşınabilir Aydınlatma", "adet": 2, "maliyet": 2000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 5, "ad": "60T65PES İGBT", "adet": 118, "maliyet": 105.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 6, "ad": "Batarya Kapasite Voltaj Göstergesi", "adet": 0, "maliyet": 385.66, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 7, "ad": "18V Büyük Matkap Motoru", "adet": 3, "maliyet": 700.0, "min": 6, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 8, "ad": "10-25 Priz (Dişi) Jak", "adet": 15, "maliyet": 52.89, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 9, "ad": "Marxlow 24V 90*90*25 Fan", "adet": 4, "maliyet": 100.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 10, "ad": "FZT851TA", "adet": 20, "maliyet": 19.5, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 11, "ad": "0.8 L25 Meme", "adet": 23, "maliyet": 25.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 12, "ad": "203CNQ100 Çıkış Diyotu", "adet": 1, "maliyet": 1402.42, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 13, "ad": "4 metre AK15 Torç", "adet": 1, "maliyet": 1500.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 14, "ad": "GBJ5010 50A 1000V Köprü Dİyot", "adet": 17, "maliyet": 42.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 15, "ad": "SKBPC5016 380V Köprü Diyot", "adet": 5, "maliyet": 200.0, "min": 8, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 16, "ad": "60N100 Mosfet", "adet": 18, "maliyet": 359.04, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 17, "ad": "820MF 400V Kondansatör", "adet": 0, "maliyet": 100.49, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 18, "ad": "Eurofix Yapıştırıcı", "adet": 32, "maliyet": 60.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 19, "ad": "Tunçmatik 5mh80 5kw 80A", "adet": 1, "maliyet": 25000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 20, "ad": "10-25 Fiş (Erkek) Jak", "adet": 7, "maliyet": 49.28, "min": 10, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 21, "ad": "3S Üçgen BMS", "adet": 10, "maliyet": 75.0, "min": 13, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 22, "ad": "1.0 L30 Zirkonyum Meme", "adet": 0, "maliyet": 35.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 23, "ad": "BT151", "adet": 225, "maliyet": 15.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 24, "ad": "Daly 13S 40A BMS", "adet": 0, "maliyet": 1105.27, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 25, "ad": "TR36 Deveboynu", "adet": 9, "maliyet": 350.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 26, "ad": "Class 12V 90*90*25 Fan", "adet": 2, "maliyet": 100.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 27, "ad": "35-70 Fiş (Erkek) Jak", "adet": 2, "maliyet": 85.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 28, "ad": "POWERMASTER 120X120X38 220V Fan", "adet": 0, "maliyet": 175.44, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 29, "ad": "680MF 450V Kondansatör", "adet": 4, "maliyet": 226.8, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 30, "ad": "Mexsun 1000W", "adet": 1, "maliyet": 5000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 31, "ad": "TR25 Meme Tutucu", "adet": 92, "maliyet": 11.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 32, "ad": "80N60 Mosfet", "adet": 0, "maliyet": 75.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 33, "ad": "12V 9AH Akü", "adet": 0, "maliyet": 780.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 34, "ad": "TR36 Yolluk", "adet": 10, "maliyet": 350.0, "min": 13, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 35, "ad": "TR15 Nozul", "adet": 91, "maliyet": 51.6, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 36, "ad": "KDV", "adet": 100, "maliyet": 0.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 37, "ad": "Potansiyometre", "adet": 3, "maliyet": 50.0, "min": 6, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 38, "ad": "CMC Tools Kaynak Pensesi 800A", "adet": 1, "maliyet": 100.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 39, "ad": "DMAX PZ2/S2 Matkap ucu", "adet": 8, "maliyet": 40.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 40, "ad": "Tunçmatik 1P50 1kw", "adet": 1, "maliyet": 9000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 41, "ad": "Torç Kabzası", "adet": 0, "maliyet": 80.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 42, "ad": "TR25 Nozul", "adet": 53, "maliyet": 68.25, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 43, "ad": "İşçilik (Matkap ve Batarya)", "adet": 945, "maliyet": 0.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 44, "ad": "FESF16JT - 16A. 600V . Ultrafast DİYOT Kategori", "adet": 8, "maliyet": 55.44, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 45, "ad": "FGW50N65WE (50n65 Mosfet)", "adet": 42, "maliyet": 90.5, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 46, "ad": "FGW60N65WE (60N65 Mosfet)", "adet": 0, "maliyet": 101.17, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 47, "ad": "TC4420", "adet": 8, "maliyet": 105.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 48, "ad": "Presleme Yüzük", "adet": 11, "maliyet": 20.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 49, "ad": "CMC Tools Kaynak Pensesi 300A", "adet": 8, "maliyet": 100.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 50, "ad": "Orion 2600 Mah Li-İon Pil", "adet": 124, "maliyet": 50.93, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 51, "ad": "İşçilik (Kaynak Makinesi)", "adet": 7659, "maliyet": 0.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 52, "ad": "40N60 80A600V Mosfet", "adet": 50, "maliyet": 264.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 53, "ad": "12V 2,5A Adaptör", "adet": 2, "maliyet": 120.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 54, "ad": "IXGH48N60C3D1 Mosfet", "adet": 40, "maliyet": 252.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 55, "ad": "Maximum Kaynak Makinesi", "adet": 2, "maliyet": 3500.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 56, "ad": "Marxlow 12V 90*90*25 Fan", "adet": 1, "maliyet": 100.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 57, "ad": "470MF 400V Kondansatör", "adet": 31, "maliyet": 300.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 58, "ad": "Mexxsun 2000W", "adet": 1, "maliyet": 11000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 59, "ad": "Marxlow 24V 120*120*25 Fan", "adet": 5, "maliyet": 200.0, "min": 8, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 60, "ad": "5S 100A BMS", "adet": 28, "maliyet": 160.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 61, "ad": "Ara Rekor", "adet": 77, "maliyet": 20.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 62, "ad": "Orion 21700 5000 Mah Li-İon Pil", "adet": 0, "maliyet": 127.34, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 63, "ad": "12 Volt Matkap Motoru", "adet": 4, "maliyet": 200.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 64, "ad": "16S 40A BMS", "adet": 1, "maliyet": 1000.14, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 65, "ad": "TR36 Nozul", "adet": 9, "maliyet": 125.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 66, "ad": "WPEC Darbeli Matkap", "adet": 1, "maliyet": 3600.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 67, "ad": "Gaz Dağıtıcı", "adet": 9, "maliyet": 20.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 68, "ad": "Anahtar 30A", "adet": 25, "maliyet": 25.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 69, "ad": "Marxlow 220V 120*120*38 Fan", "adet": 2, "maliyet": 196.56, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 70, "ad": "Class 220V 120*120*38 Fan", "adet": 1, "maliyet": 200.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 71, "ad": "Mervesan Trafo", "adet": 2, "maliyet": 400.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 72, "ad": "STTH12R06D Diyot", "adet": 10, "maliyet": 80.64, "min": 13, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 73, "ad": "Orion 3.2V 100AH LiFepo4", "adet": 8, "maliyet": 1733.19, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 74, "ad": "TRWELD Kaynak Makinesi Pastası", "adet": 8, "maliyet": 100.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 75, "ad": "MMPT", "adet": 0, "maliyet": 2300.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 76, "ad": "35-70 Priz (Dişi) Jak", "adet": 11, "maliyet": 101.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 77, "ad": "PowerXtra 1.2 V NiCd 1500 Mah", "adet": 3, "maliyet": 50.0, "min": 6, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 78, "ad": "Torç Tetik", "adet": 48, "maliyet": 30.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 79, "ad": "10,8 Volt Matkap Motoru", "adet": 1, "maliyet": 250.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 80, "ad": "Orion 3200 mAh Li-on Pil", "adet": 0, "maliyet": 106.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 81, "ad": "L4981BD SMD Entegre", "adet": 2, "maliyet": 235.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 82, "ad": "POWERMASTER 120X120X25 24V Fan", "adet": 0, "maliyet": 71.49, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 83, "ad": "TR15 Yaylı Meme Tutucu", "adet": 80, "maliyet": 35.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 84, "ad": "60UP200N Mosfet", "adet": 8, "maliyet": 250.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 85, "ad": "Orion 2200 mAh Li-on Pil", "adet": 0, "maliyet": 55.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 86, "ad": "Earth Clamp Kaynak Şasesi", "adet": 5, "maliyet": 100.0, "min": 8, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 87, "ad": "220V Fiş", "adet": 4, "maliyet": 35.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 88, "ad": "Orion 1500 mAh Li-on Pil", "adet": 304, "maliyet": 51.77, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 89, "ad": "4 metre AK25 Torç", "adet": 1, "maliyet": 1600.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 90, "ad": "Bosch Tetik", "adet": 0, "maliyet": 400.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 91, "ad": "Power-Xtra 1.2V 2000Mah 10C Pil", "adet": 50, "maliyet": 58.45, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 92, "ad": "4*2.5 Kablo", "adet": 4, "maliyet": 60.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 93, "ad": "Titex Kesme Taşı", "adet": 253, "maliyet": 10.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 94, "ad": "Marxlow 12V 120*120*25 Fan", "adet": 1, "maliyet": 200.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 95, "ad": "Tunçmatik 5P50 5kw", "adet": 1, "maliyet": 15000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 96, "ad": "Mervesan 12.6V 3S Şarj Aleti", "adet": 7, "maliyet": 210.0, "min": 10, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 97, "ad": "Bosch kömür", "adet": 1, "maliyet": 160.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 98, "ad": "Orion 2000 mAh Li-on Pil", "adet": 458, "maliyet": 57.61, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 99, "ad": "Şarjlı Matkap", "adet": 12, "maliyet": 750.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 100, "ad": "50T65FD1 İGBT", "adet": 2, "maliyet": 105.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 101, "ad": "1,2 L30 Meme", "adet": 9, "maliyet": 30.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 102, "ad": "Class 12V 1A Şarj Aleti", "adet": 0, "maliyet": 120.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 103, "ad": "Daly 13S 60A BMS", "adet": 0, "maliyet": 1487.86, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 104, "ad": "1.0 Meme", "adet": 18, "maliyet": 30.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 105, "ad": "Magmaweld Monostick 200İ", "adet": 0, "maliyet": 5350.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 106, "ad": "403CNQ040 Çıkış Diyotu", "adet": 1, "maliyet": 1495.7, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 107, "ad": "Stanley Tetik", "adet": 1, "maliyet": 1000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 108, "ad": "Solinved 12V 2000W", "adet": 1, "maliyet": 10000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 109, "ad": "Daly 8S 25.6V 60A LifePo4 BMS", "adet": 2, "maliyet": 1161.17, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 110, "ad": "3,5 metre AK15 Torç", "adet": 2, "maliyet": 1350.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 111, "ad": "TR36 Meme Tutucu", "adet": 4, "maliyet": 25.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 112, "ad": "LM2575HVS", "adet": 2, "maliyet": 265.95, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 113, "ad": "Stanley Motor", "adet": 0, "maliyet": 2500.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 114, "ad": "PowerXtra yassı Pil", "adet": 0, "maliyet": 300.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 115, "ad": "Orion 1.2V 4/5 NiCd", "adet": 2, "maliyet": 60.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 116, "ad": "75G65 Mosfet", "adet": 70, "maliyet": 200.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 117, "ad": "Matkap Tetik", "adet": 0, "maliyet": 250.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 118, "ad": "18 Volt Matkap Motoru", "adet": 0, "maliyet": 200.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 119, "ad": "3,5 metre Yolluk", "adet": 8, "maliyet": 150.0, "min": 11, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 120, "ad": "Power-Xtra 1.2V 1000Mah Ni-Cd Pil", "adet": 46, "maliyet": 31.5, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 121, "ad": "EVE 18650 3200 Mah Pil", "adet": 162, "maliyet": 103.49, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 122, "ad": "Titex Bits Ucu", "adet": 55, "maliyet": 25.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 123, "ad": "4,5 metre Yolluk", "adet": 9, "maliyet": 150.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 124, "ad": "SD6834", "adet": 0, "maliyet": 22.81, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 125, "ad": "BYC75W-1200PQ Çıkış Diyotu", "adet": 1, "maliyet": 214.33, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 126, "ad": "TR25 Deveboynu", "adet": 9, "maliyet": 300.0, "min": 12, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 127, "ad": "Mervesan 21V 5S Şarj Aleti", "adet": 14, "maliyet": 260.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 128, "ad": "KL Pro MMA200A Kaynak Makinesi", "adet": 1, "maliyet": 11000.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 129, "ad": "Dyson BMS", "adet": 0, "maliyet": 1500.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 130, "ad": "75N60 İGBT", "adet": 0, "maliyet": 170.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 131, "ad": "HELL STELL Bits", "adet": 29, "maliyet": 70.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 132, "ad": "Assur Şarjlı Matkap Kartı", "adet": 1, "maliyet": 750.0, "min": 5, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 133, "ad": "Mervesan 16.8V 4S Şarj Aleti", "adet": 4, "maliyet": 220.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 134, "ad": "Tenpower 21700 3.7V Li-İon Pil", "adet": 10, "maliyet": 181.96, "min": 13, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 135, "ad": "0.8 Tombul Meme", "adet": 12, "maliyet": 20.0, "min": 2, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 136, "ad": "1S BMS", "adet": 4, "maliyet": 30.0, "min": 7, "tarih": "2025-01-01T00:00:00.000Z" }, { "id": 137, "ad": "3S 60 A BMS", "adet": 0, "maliyet": 150.0, "min": 3, "tarih": "2025-01-01T00:00:00.000Z" }];
                    saveState();
                }
                if (yuklendi) {
                    console.log("Veri Firebase dan yuklendi");
                }
                renderDashboard();
                firebaseGercekZamanli();
            });
        }

        function yedekIndir() {
            var dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(state));
            var downloadAnchorNode = document.createElement('a');
            downloadAnchorNode.setAttribute("href", dataStr);
            downloadAnchorNode.setAttribute("download", "servis_yedek_" + new Date().toISOString().split('T')[0] + ".json");
            document.body.appendChild(downloadAnchorNode); // Firefox için gerekli
            downloadAnchorNode.click();
            downloadAnchorNode.remove();
        }

        function yedekYukle(event) {
            var file = event.target.files[0];
            if (!file) return;

            var reader = new FileReader();
            reader.onload = function (e) {
                try {
                    var icerik = e.target.result;
                    var yeniVeri = JSON.parse(icerik);

                    if (yeniVeri && typeof yeniVeri === 'object') {
                        if (confirm('DİKKAT! Yedeği yüklemek mevcut tüm verilerinizin üzerine yazılacaktır. Emin misiniz?')) {
                            // Olası eski yedeklerden eksik kalabilecek arrayleri boş liste ile tamamlayalım ki filtre/döngü hatası (undefined) oluşturmasın.
                            state.servisler = yeniVeri.servisler || [];
                            state.cari = yeniVeri.cari || [];
                            state.stok = yeniVeri.stok || [];
                            state.musteriler = yeniVeri.musteriler || [];
                            state.satislar = yeniVeri.satislar || [];
                            state.giderler = yeniVeri.giderler || [];
                            state.kasa = yeniVeri.kasa || [];
                            state.kasalar = yeniVeri.kasalar || [];
                            state.ayarlar = yeniVeri.ayarlar || { isletmeAd: '', isletmeTel: '', adres: '', uyariAktif: true };
                            state.servisFilter = 'hepsi';
                            state.cariFilter = 'hepsi';

                            saveState(); // Firebase ve LocalStorage'a kaydet
                            renderDashboard();

                            var durumEl = document.getElementById('yedek-yukle-durum');
                            if (durumEl) {
                                durumEl.textContent = '✅ Yedek başarıyla yüklendi!';
                                durumEl.style.color = 'var(--green)';
                                setTimeout(function () { durumEl.textContent = ''; }, 4000);
                            } else {
                                alert('Yedek başarıyla yüklendi!');
                                window.location.reload();
                            }
                        }
                    } else {
                        throw new Error('Geçersiz dosya formatı');
                    }
                } catch (error) {
                    console.error('Yedek yükleme hatası:', error);
                    alert('Yedek yüklenirken bir hata oluştu. Dosyanın geçerli bir JSON olduğundan emin olun.');
                }
            };
            reader.readAsText(file);
            event.target.value = ''; // Input'u resetle aynı dosyayı tekrar yükleyebilmek için
        }

        initFirebase();

        renderDashboard();
        setInterval(renderDriveBar, 2000); renderDriveBar();
    </script>


    <!-- STOK DÜZENLEME MODAL -->
    <div class="modal-overlay" id="stok-edit-modal">
        <div class="modal">
            <div class="modal-title">STOK DÜZENLE <button class="close-btn"
                    onclick="closeModal('stok-edit-modal')">✕</button></div>
            <div class="form-group">
                <label>Parça / Malzeme Adı</label>
                <input type="text" id="ste-ad">
            </div>
            <div class="row">
                <div class="form-group">
                    <label>Maliyet (₺)</label>
                    <input type="number" id="ste-maliyet" min="0" oninput="hesaplaMarj()">
                </div>
                <div class="form-group">
                    <label>Satış Fiyatı (₺)</label>
                    <input type="number" id="ste-satis" min="0" oninput="hesaplaMarj()">
                </div>
            </div>
            <div id="marj-goster" style="font-size:12px;margin-bottom:8px;min-height:16px"></div>
            <div class="row">
                <div class="form-group">
                    <label>Adet</label>
                    <input type="number" id="ste-adet" min="0">
                </div>
                <div class="form-group">
                    <label>Min. Stok</label>
                    <input type="number" id="ste-min" min="0">
                </div>
            </div>
            <input type="hidden" id="ste-id">
            <button class="btn btn-primary" onclick="updateStok()">💾 Güncelle</button>
        </div>
    </div>

    <!-- FATURA MODAL -->
    <div class="modal-overlay" id="fatura-modal">
        <div class="modal">
            <div class="modal-title">🧾 FİŞ / FATURA <button class="close-btn"
                    onclick="closeModal('fatura-modal')">✕</button></div>
            <div id="fatura-content"
                style="background:#fff;color:#111;border-radius:8px;padding:18px;font-family:monospace;font-size:13px;line-height:1.8">
            </div>
            <div style="display:flex;gap:8px;margin-top:12px">
                <button class="btn btn-whatsapp" style="flex:1;justify-content:center" onclick="fisWAPaylas()">📲 WA'ya
                    Gönder</button>
                <button class="btn btn-ghost btn-sm" onclick="fisResimIndir()">💾 Kaydet</button>
                <button class="btn btn-ghost btn-sm" onclick="closeModal('fatura-modal')">✕</button>
            </div>
        </div>
    </div>

</body>

</html>
