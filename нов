<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>База знаний | Ветклиника «Надежда»</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Playfair+Display:ital@1&display=swap" rel="stylesheet">
  
  <!-- Firebase SDK -->
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

  <style>
    :root {
      --brand-blue: #0088D4;
      --brand-blue-hover: #0073B5;
      --brand-deep: #0B3558;
      --brand-light: #E1F1FB;
      --brand-border: #BAE0F7;
      --bg-main: #F4F9FD;
      --bg-card: #FFFFFF;
      --text-main: #0B253E;
      --text-muted: #5C7892;
      --accent-green: #059669;
      --accent-green-bg: #D1FAE5;
      --accent-red: #DC2626;
      --accent-red-bg: #FEE2E2;
      --accent-amber: #D97706;
      --accent-amber-bg: #FEF3C7;
      --ai-purple: #7C3AED;
      --ai-purple-light: #F3E8FF;
      --yandex-red: #FC3F1D;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      background: var(--bg-main);
      color: var(--text-main);
      display: flex;
      height: 100vh;
      overflow: hidden;
    }

    /* Экран входа */
    .auth-overlay {
      position: fixed; top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(11, 37, 62, 0.88); backdrop-filter: blur(6px);
      z-index: 3000; display: flex; align-items: center; justify-content: center; padding: 16px;
    }
    .auth-box {
      background: #FFFFFF; width: 100%; max-width: 440px; padding: 32px 24px;
      border-radius: 14px; box-shadow: 0 15px 35px rgba(11, 53, 88, 0.25);
      border-top: 5px solid var(--brand-blue); text-align: center;
    }
    .auth-logo-img { max-height: 64px; max-width: 220px; margin: 0 auto 14px; object-fit: contain; display: block; }
    .auth-box h2 { font-size: 1.35rem; color: var(--brand-deep); margin-bottom: 4px; font-weight: 800; }
    .auth-box p { font-size: 0.8rem; color: var(--text-muted); margin-bottom: 22px; text-transform: uppercase; letter-spacing: 0.5px; }
    .auth-form { text-align: left; }
    .auth-form label { display: block; font-size: 0.78rem; font-weight: 700; color: var(--brand-deep); margin-bottom: 6px; text-transform: uppercase; }
    .auth-form input {
      width: 100%; padding: 11px 14px; border: 1.5px solid var(--brand-border);
      border-radius: 8px; font-size: 0.95rem; outline: none; margin-bottom: 14px; font-family: inherit;
    }
    .auth-form input:focus { border-color: var(--brand-blue); box-shadow: 0 0 0 3px rgba(0, 136, 212, 0.15); }
    
    .pass-input-row { position: relative; margin-bottom: 14px; }
    .pass-input-row input { padding-right: 42px; margin-bottom: 0; }
    .pass-toggle-btn {
      position: absolute; right: 10px; top: 50%; transform: translateY(-50%);
      background: none; border: none; cursor: pointer; font-size: 1.1rem; opacity: 0.6;
    }

    /* Шапка сайта */
    .header {
      position: fixed; top: 0; left: 0; right: 0; height: 72px;
      background: #FFFFFF; border-bottom: 3px solid var(--brand-blue);
      display: flex; align-items: center; justify-content: space-between;
      padding: 0 18px; z-index: 1000; box-shadow: 0 2px 8px rgba(11, 53, 88, 0.05);
    }
    .header-left { display: flex; align-items: center; gap: 10px; }
    .btn-mobile-menu {
      display: none; background: none; border: 1px solid var(--brand-border);
      border-radius: 6px; font-size: 1.3rem; padding: 4px 9px; cursor: pointer; color: var(--brand-deep);
    }
    .header-logo { display: flex; align-items: center; cursor: pointer; }
    .header-logo-img { height: 48px; max-width: 210px; object-fit: contain; display: block; }

    /* Поиск в шапке */
    .header-search-container { display: flex; align-items: center; gap: 6px; position: relative; margin: 0 12px; }
    .header-search { width: 310px; position: relative; }
    .header-search input {
      width: 100%; padding: 8px 14px 8px 36px;
      border: 1.5px solid var(--brand-border); border-radius: 8px;
      font-size: 0.85rem; background: #FAFCFE; color: var(--text-main);
      outline: none; transition: all 0.2s;
    }
    .header-search input:focus { border-color: var(--brand-blue); background: #FFFFFF; }
    .header-search::before { content: "✨"; position: absolute; left: 10px; top: 50%; transform: translateY(-50%); font-size: 0.95rem; }

    .btn-ai-search {
      background: linear-gradient(135deg, var(--brand-blue), var(--ai-purple));
      color: white; border: none; padding: 8px 13px; border-radius: 8px;
      font-size: 0.8rem; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 5px; white-space: nowrap;
    }

    .header-actions { display: flex; align-items: center; gap: 8px; }
    .btn {
      padding: 7px 12px; border-radius: 7px; font-size: 0.8rem; font-weight: 600;
      cursor: pointer; display: inline-flex; align-items: center; gap: 6px; border: none; transition: all 0.15s; white-space: nowrap;
    }
    .btn-primary { background: var(--brand-blue); color: #fff; }
    .btn-primary:hover { background: var(--brand-blue-hover); }
    .btn-outline { background: transparent; border: 1.5px solid var(--brand-blue); color: var(--brand-blue); }
    .btn-outline:hover { background: var(--brand-light); }
    .btn-yandex { background: #FFFFFF; border: 1.5px solid var(--yandex-red); color: var(--yandex-red); }
    .btn-yandex:hover { background: #FFF4F2; }

    .btn-back {
      display: inline-flex; align-items: center; gap: 6px; background: #FFFFFF; border: 1px solid var(--brand-border);
      color: var(--brand-deep); padding: 6px 14px; border-radius: 6px; font-size: 0.85rem; font-weight: 700; cursor: pointer;
    }
    .btn-back:hover { background: var(--brand-light); color: var(--brand-blue); }

    .cloud-indicator {
      display: flex; align-items: center; gap: 5px; font-size: 0.72rem; color: var(--accent-green);
      background: var(--accent-green-bg); padding: 4px 8px; border-radius: 6px; font-weight: 600;
    }

    .user-profile-badge {
      display: flex; align-items: center; gap: 8px; padding-left: 8px; border-left: 1px solid var(--brand-border); position: relative;
    }
    .user-avatar {
      width: 34px; height: 34px; border-radius: 50%; background: var(--brand-deep); color: white;
      font-weight: 700; font-size: 0.85rem; display: flex; align-items: center; justify-content: center;
    }
    .user-info { font-size: 0.8rem; text-align: left; }
    .user-name { font-weight: 700; color: var(--brand-deep); }
    .user-role { font-size: 0.7rem; color: var(--text-muted); }

    /* Сайдбар */
    .sidebar {
      width: 300px; background: #FFFFFF; border-right: 1px solid var(--brand-border); margin-top: 72px;
      height: calc(100vh - 72px); overflow-y: auto; padding: 14px 0; flex-shrink: 0;
      display: flex; flex-direction: column; justify-content: space-between;
      transition: transform 0.25s ease; z-index: 1200;
    }
    .sidebar-overlay {
      display: none; position: fixed; top: 72px; left: 0; right: 0; bottom: 0;
      background: rgba(11,37,62,0.5); z-index: 1100;
    }
    .sidebar-content { flex: 1; }
    .nav-category { margin-bottom: 14px; }
    .nav-cat-header {
      display: flex; align-items: center; justify-content: space-between;
      padding: 6px 16px;
    }
    .nav-cat-title { font-size: 0.73rem; font-weight: 800; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; }

    .nav-item {
      display: flex; align-items: center; justify-content: space-between; padding: 9px 16px; font-size: 0.86rem;
      color: var(--brand-deep); cursor: pointer; border-left: 4px solid transparent; transition: all 0.15s;
    }
    .nav-item:hover { background: var(--brand-light); color: var(--brand-blue); }
    .nav-item.active { background: var(--brand-light); color: var(--brand-blue); font-weight: 700; border-left-color: var(--brand-blue); }
    .nav-item-title { flex: 1; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }

    .sidebar-footer { padding: 14px 16px; border-top: 1px solid var(--brand-border); background: #FAFCFE; }
    .sidebar-footer button { width: 100%; margin-bottom: 6px; font-size: 0.78rem; justify-content: center; }

    /* Контентная зона */
    .main-content { flex: 1; margin-top: 72px; height: calc(100vh - 72px); overflow-y: auto; padding: 24px 32px; }
    .content-wrap { max-width: 1100px; margin: 0 auto; }

    .doc-nav-row { display: flex; align-items: center; gap: 12px; margin-bottom: 10px; }
    .breadcrumbs { font-size: 0.85rem; color: var(--text-muted); }
    .breadcrumbs a { color: var(--brand-blue); text-decoration: none; cursor: pointer; }
    .breadcrumbs a:hover { text-decoration: underline; }

    .doc-header {
      border-bottom: 2px solid var(--brand-border); padding-bottom: 16px; margin-bottom: 22px;
      display: flex; justify-content: space-between; align-items: flex-start; gap: 14px;
    }
    .doc-title { font-size: 1.7rem; font-weight: 800; color: var(--brand-deep); }
    .doc-meta { display: flex; gap: 8px; margin-top: 8px; font-size: 0.8rem; flex-wrap: wrap; }

    .tag { padding: 3px 8px; border-radius: 4px; font-weight: 600; font-size: 0.75rem; }
    .tag-blue { background: var(--brand-light); color: var(--brand-blue); }
    .tag-green { background: var(--accent-green-bg); color: var(--accent-green); }

    /* Плиточная сетка карточек */
    .dashboard-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(310px, 1fr));
      gap: 20px;
      margin-bottom: 24px;
    }
    .dash-card {
      background: #FFFFFF; border-radius: 12px; border: 1.5px solid var(--brand-border); overflow: hidden;
      display: flex; flex-direction: column; box-shadow: 0 2px 8px rgba(11, 53, 88, 0.05); position: relative; transition: all 0.2s ease;
      cursor: pointer; user-select: none;
    }
    .dash-card:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(11, 53, 88, 0.12); border-color: var(--brand-blue); }
    .dash-card-img { height: 110px; display: flex; align-items: center; justify-content: center; font-size: 2.8rem; color: white; pointer-events: none; }
    .dash-card-content { padding: 16px; flex: 1; display: flex; flex-direction: column; pointer-events: none; }
    .dash-card-title { font-size: 1.05rem; font-weight: 700; color: var(--brand-deep); margin-bottom: 6px; }
    .dash-card-desc { font-size: 0.82rem; color: var(--text-muted); line-height: 1.4; margin-bottom: 12px; flex: 1; }
    .dash-card-footer { font-size: 0.82rem; font-weight: 700; color: var(--brand-blue); display: flex; justify-content: space-between; align-items: center; }
    
    .dash-card-actions {
      position: absolute; top: 8px; right: 8px; display: flex; gap: 3px;
      background: rgba(255, 255, 255, 0.95); padding: 4px 6px; border-radius: 6px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.15); z-index: 20;
    }
    .card-tool-btn {
      background: none; border: none; font-size: 0.85rem; cursor: pointer; padding: 2px 5px; border-radius: 4px;
      color: var(--brand-deep); transition: background 0.15s; font-weight: 700;
    }
    .card-tool-btn:hover { background: #E2E8F0; }

    /* Красная фирменная плашка Яндекс Диска */
    .yandex-integration-card {
      background: #FFFFFF; border: 1.5px solid #FCA5A5; border-left: 5px solid var(--yandex-red);
      border-radius: 10px; padding: 16px 20px; display: flex; justify-content: space-between; align-items: center;
      margin: 16px 0 24px; box-shadow: 0 2px 8px rgba(252, 63, 29, 0.08); gap: 14px;
    }

    /* Блоки статьи */
    .page-block-wrapper { position: relative; margin-bottom: 22px; border-radius: 8px; }
    .page-block-wrapper:hover { outline: 1.5px dashed var(--brand-blue); outline-offset: 4px; }
    .page-block-tools {
      position: absolute; top: -12px; right: 12px; display: none; gap: 4px; background: #FFFFFF;
      border: 1px solid var(--brand-border); box-shadow: 0 2px 8px rgba(0,0,0,0.08); border-radius: 6px; padding: 2px 6px; z-index: 10;
    }
    .page-block-wrapper:hover .page-block-tools { display: flex; }

    .info-banner {
      background: #FFFFFF; border-left: 4px solid var(--brand-blue); padding: 18px 20px; border-radius: 0 8px 8px 0;
      box-shadow: 0 1px 3px rgba(11, 53, 88, 0.04); border-top: 1px solid #E2E8F0; border-right: 1px solid #E2E8F0; border-bottom: 1px solid #E2E8F0;
      font-size: 0.95rem; line-height: 1.6;
    }
    .checklist { background: #FFFFFF; border: 1px solid var(--brand-border); border-radius: 8px; padding: 14px 20px; margin: 12px 0; }
    .check-item { display: flex; align-items: flex-start; gap: 12px; padding: 10px 0; border-bottom: 1px solid #EEF5FA; font-size: 0.92rem; }
    .check-item:last-child { border-bottom: none; }
    .check-item input[type="checkbox"] { margin-top: 3px; accent-color: var(--brand-blue); width: 17px; height: 17px; cursor: pointer; }
    .check-item.done span { text-decoration: line-through; color: var(--text-muted); }

    /* Медиа */
    .media-card {
      background: #FFFFFF; border: 1px solid var(--brand-border); border-radius: 10px; overflow: hidden;
      margin: 14px 0; box-shadow: 0 2px 6px rgba(11, 53, 88, 0.04);
    }
    .media-card img { width: 100%; max-height: 460px; object-fit: contain; display: block; background: #F8FAFD; }
    .media-video-wrap { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; background: #000; }
    .media-video-wrap iframe, .media-video-wrap video { position: absolute; top:0; left: 0; width: 100%; height: 100%; border: 0; }
    .media-card-title { padding: 10px 16px; font-weight: 700; font-size: 0.9rem; color: var(--brand-deep); border-bottom: 1px solid #E2E8F0; }
    .file-attachment-box {
      background: #FFFFFF; border: 1.5px solid var(--brand-border); border-radius: 8px;
      padding: 12px 16px; display: flex; align-items: center; justify-content: space-between; margin: 10px 0;
    }

    /* Таблица матрицы прав Ветменеджер */
    .vetmanager-tabs { display: flex; gap: 8px; border-bottom: 2px solid var(--brand-border); margin-bottom: 16px; }
    .vm-tab {
      padding: 8px 16px; font-size: 0.85rem; font-weight: 700; color: var(--text-muted); cursor: pointer;
      border-radius: 6px 6px 0 0; background: #F1F5F9; border: 1px solid var(--brand-border); border-bottom: none;
    }
    .vm-tab.active { background: #FFFFFF; color: var(--brand-blue); border-top: 3px solid var(--brand-blue); }
    .perm-grid-table { width: 100%; border-collapse: collapse; font-size: 0.82rem; background: #FFFFFF; border: 1px solid #CBD5E1; }
    .perm-grid-table th { background: #E2E8F0; padding: 8px 10px; color: var(--brand-deep); text-align: center; border: 1px solid #CBD5E1; }
    .perm-grid-table th:first-child { text-align: left; }
    .perm-grid-table td { padding: 6px 8px; border: 1px solid #E2E8F0; text-align: center; }
    .perm-grid-table td:first-child { text-align: left; font-weight: 600; }
    .cell-perm { background: #FEE2E2; cursor: pointer; transition: all 0.1s; }
    .cell-perm.checked { background: #D1FAE5; }

    /* Модальные окна */
    .modal-overlay {
      display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(11, 37, 62, 0.55); z-index: 2500; align-items: center; justify-content: center; backdrop-filter: blur(2px);
      padding: 14px;
    }
    .modal-overlay.active { display: flex; }
    .modal-window {
      background: #FFFFFF; width: 100%; max-width: 760px; border-radius: 12px; box-shadow: 0 10px 30px rgba(0,0,0,0.18);
      border-top: 4px solid var(--brand-blue); padding: 22px; max-height: 90vh; overflow-y: auto;
    }
    .modal-title { font-size: 1.25rem; font-weight: 700; color: var(--brand-deep); margin-bottom: 16px; }
    .form-group { margin-bottom: 14px; }
    .form-group label { display: block; font-size: 0.78rem; font-weight: 600; color: var(--brand-deep); margin-bottom: 5px; text-transform: uppercase; }
    .form-group input, .form-group select, .form-group textarea {
      width: 100%; padding: 9px 12px; border: 1.5px solid var(--brand-border); border-radius: 6px;
      font-size: 0.9rem; font-family: inherit; outline: none;
    }
    .form-group textarea { min-height: 80px; resize: vertical; }
    .modal-actions { display: flex; justify-content: flex-end; gap: 10px; margin-top: 18px; }

    .styled-table { width: 100%; border-collapse: collapse; font-size: 0.85rem; margin-top: 12px; }
    .styled-table th { background: #EBF4FA; padding: 9px 12px; text-align: left; color: var(--brand-deep); }
    .styled-table td { padding: 9px 12px; border-bottom: 1px solid #E2E8F0; }

    @media (max-width: 900px) {
      .header { padding: 0 12px; }
      .btn-mobile-menu { display: inline-flex; }
      .header-search-container { display: none; }
      .header-logo-img { height: 38px; max-width: 140px; }
      .cloud-indicator, #headerYandexBtn, #usersManageBtn, #btnUploadLogo, .user-info { display: none; }
      .sidebar {
        position: fixed; left: 0; top: 0; bottom: 0; margin-top: 72px;
        transform: translateX(-100%); box-shadow: 4px 0 16px rgba(0,0,0,0.15);
      }
      .sidebar.open { transform: translateX(0); }
      .sidebar-overlay.active { display: block; }
      .main-content { padding: 18px 14px; }
      .doc-header { flex-direction: column; align-items: stretch; }
      .dashboard-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

  <!-- Авторизация -->
  <div class="auth-overlay" id="authScreen">
    <div class="auth-box">
      <img id="authLogoImg" class="auth-logo-img" src="" alt="Логотип Надежда">
      <h2>Клиника «Надежда»</h2>
      <p>Корпоративная база знаний</p>
      
      <form class="auth-form" onsubmit="handleLogin(event)">
        <label>Логин или Email</label>
        <input type="text" id="loginUsername" placeholder="admin или korotets" required autocomplete="username">
        
        <label>Пароль</label>
        <div class="pass-input-row">
          <input type="password" id="loginPassword" placeholder="••••••••" required autocomplete="current-password">
          <button type="button" class="pass-toggle-btn" onclick="togglePassVisibility('loginPassword', this)">👁️</button>
        </div>

        <button type="submit" id="loginSubmitBtn" class="btn btn-primary" style="width: 100%; padding: 12px; justify-content: center; font-size: 0.95rem;">Войти в систему</button>
      </form>
    </div>
  </div>

  <!-- Шапка -->
  <header class="header">
    <div class="header-left">
      <button class="btn-mobile-menu" onclick="toggleMobileSidebar()" title="Меню разделов">☰</button>
      <div class="header-logo" onclick="openDoc('home')">
        <img id="headerLogoImg" class="header-logo-img" src="" alt="Логотип Надежда">
      </div>
    </div>

    <!-- ИИ Поиск по разделам -->
    <div class="header-search-container">
      <div class="header-search">
        <input type="text" id="searchInput" placeholder="ИИ поиск: «у кота судороги», «наркоз диета»..." onkeydown="handleSearchKeyDown(event)">
      </div>
      <button class="btn-ai-search" onclick="runAISearch()" title="Найти по смыслу с помощью нейросети">
        ✨ ИИ Поиск
      </button>
    </div>

    <div class="header-actions">
      <div class="cloud-indicator" id="cloudStatusBadge">☁️ Облако онлайн</div>

      <!-- Кнопка смены логотипа для администратора -->
      <button class="btn btn-outline" id="btnUploadLogo" style="display:none;" onclick="document.getElementById('logoFileInput').click()" title="Загрузить изображение логотипа">
        🖼️ Сменить логотип
      </button>
      <input type="file" id="logoFileInput" style="display:none;" accept="image/*" onchange="handleLogoUpload(event)">

      <!-- Кнопка допуска к разделам по ролям и пользователей -->
      <button class="btn btn-outline" id="usersManageBtn" style="display:none;" onclick="openUsersModal()">
        👥 Сотрудники и права
      </button>

      <a id="headerYandexBtn" href="https://disk.yandex.ru/d/5HlCdgS2idp2Gg" target="_blank" class="btn btn-yandex" title="Открыть диск клиники">
        📁 Яндекс Диск
      </a>
      
      <div class="user-profile-badge">
        <div class="user-avatar" id="headerAvatar">?</div>
        <div class="user-info">
          <div class="user-name" id="headerName">Имя</div>
          <div class="user-role" id="headerRole">Должность</div>
        </div>
        <button class="btn btn-outline" style="padding: 4px 7px; font-size: 0.75rem;" onclick="logout()">Выход</button>
      </div>
    </div>
  </header>

  <div class="sidebar-overlay" id="sidebarOverlay" onclick="toggleMobileSidebar()"></div>

  <!-- Сайдбар -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-content" id="navContainer"></div>
    <div class="sidebar-footer" id="adminSidebarFooter" style="display:none;">
      <button class="btn btn-primary" onclick="openAllPagesManagerModal()">📑 Все существующие страницы</button>
      <button class="btn btn-outline" onclick="exportData()">📥 Бэкап системы (JSON)</button>
      <button class="btn btn-outline" onclick="document.getElementById('importFile').click()">📤 Восстановить базу</button>
      <input type="file" id="importFile" style="display:none" onchange="importData(event)" accept=".json">
    </div>
  </aside>

  <!-- Рабочая зона -->
  <main class="main-content">
    <div class="content-wrap" id="documentArea"></div>
  </main>

  <!-- МОДАЛЬНЫЕ ОКНА КОНСТРУКТОРА -->
  <!-- 1. Карточка направления / блока -->
  <div class="modal-overlay" id="moduleModal">
    <div class="modal-window">
      <div class="modal-title" id="moduleModalTitle">Карточка направления / блока</div>
      <input type="hidden" id="modalCardId">

      <div class="form-group">
        <label>Название направления</label>
        <input type="text" id="modalTitleInput" placeholder="Заведующие отделениями">
      </div>
      <div class="form-group">
        <label>Краткое описание</label>
        <textarea id="modalDescInput" placeholder="Контроль историй болезни, аудит смен..."></textarea>
      </div>
      
      <div style="display:grid; grid-template-columns: 1fr 1fr; gap:12px;">
        <div class="form-group">
          <label>Иконка / Эмодзи</label>
          <input type="text" id="modalIconInput" placeholder="🏛️, 🔪, 🎧">
        </div>
        <div class="form-group">
          <label>Цвет градиента шапки</label>
          <select id="modalColorSelect">
            <option value="linear-gradient(135deg, #0088D4, #00A6FF)">Голубой (Надежда)</option>
            <option value="linear-gradient(135deg, #0B3558, #185285)">Глубокий синий (Руководство)</option>
            <option value="linear-gradient(135deg, #0F766E, #14B8A6)">Изумрудный (Хирургия)</option>
            <option value="linear-gradient(135deg, #7C3AED, #A78BFA)">Фиолетовый</option>
            <option value="linear-gradient(135deg, #6366F1, #818CF8)">Индиго</option>
          </select>
        </div>
      </div>

      <div class="form-group" style="background:var(--brand-light); padding:14px; border-radius:8px; border:1.5px solid var(--brand-border);">
        <label style="color:var(--brand-deep); font-weight:800;">Ссылка на страницу (Куда ведёт клик):</label>
        <select id="modalPageSelect" style="background:#fff;"></select>
      </div>

      <div class="modal-actions">
        <button class="btn btn-outline" onclick="closeModuleModal()">Отмена</button>
        <button class="btn btn-primary" onclick="saveCardItem()">Сохранить карточку</button>
      </div>
    </div>
  </div>

  <!-- 2. Реестр всех страниц -->
  <div class="modal-overlay" id="allPagesModal">
    <div class="modal-window" style="max-width: 860px;">
      <div class="modal-title">Все существующие страницы базы знаний</div>
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
        <span style="font-size:0.85rem; color:var(--text-muted);">Управляйте привязками и видимостью в боковом меню:</span>
        <button class="btn btn-primary" onclick="openCreateStandalonePageModal()">+ Создать новую страницу</button>
      </div>
      <table class="styled-table" style="margin-top:0;">
        <thead>
          <tr>
            <th>Название страницы</th>
            <th>ID (для ссылок в тексте)</th>
            <th>Раздел</th>
            <th style="text-align:center;">В боковой панели</th>
            <th>Действия</th>
          </tr>
        </thead>
        <tbody id="allPagesTableBody"></tbody>
      </table>
      <div class="modal-actions">
        <button class="btn btn-outline" onclick="document.getElementById('allPagesModal').classList.remove('active')">Закрыть</button>
      </div>
    </div>
  </div>

  <!-- 3. Создание/редактирование страницы -->
  <div class="modal-overlay" id="pageEditModal" style="z-index: 2600;">
    <div class="modal-window">
      <div class="modal-title" id="pageEditModalTitle">Параметры страницы</div>
      <input type="hidden" id="editPageIdInput">
      
      <div class="form-group">
        <label>Название страницы</label>
        <input type="text" id="editPageTitleInput" placeholder="Название регламента...">
      </div>
      <div class="form-group">
        <label>Категория / Раздел</label>
        <input type="text" id="editPageCategoryInput" placeholder="Хирургия или Общие сведения">
      </div>
      <div class="form-group" style="display:flex; align-items:center; gap:10px; background:#F8FAFD; padding:10px; border-radius:6px; border:1px solid #E2E8F0;">
        <input type="checkbox" id="editPageShowInSidebar" style="width:18px; height:18px; accent-color:var(--brand-blue); cursor:pointer;">
        <label for="editPageShowInSidebar" style="margin:0; text-transform:none; font-weight:700; cursor:pointer;">
          Показывать эту страницу в боковой панели (сайдбаре)
        </label>
      </div>

      <div class="modal-actions">
        <button class="btn btn-outline" onclick="document.getElementById('pageEditModal').classList.remove('active')">Отмена</button>
        <button class="btn btn-primary" onclick="savePageData()">Сохранить страницу</button>
      </div>
    </div>
  </div>

  <!-- 4. Добавление пункта с текстом, ссылкой, фото, видео или файлом -->
  <div class="modal-overlay" id="articleBlockModal">
    <div class="modal-window">
      <div class="modal-title" id="articleBlockModalTitle">Пункт регламента / Материал</div>
      <input type="hidden" id="articleBlockIndex">
      
      <div class="form-group">
        <label>Тип материала</label>
        <select id="articleBlockTypeSelect" onchange="toggleArticleBlockFields()">
          <option value="banner">Текстовый регламент / Алгоритм</option>
          <option value="checklist">Контрольный чек-лист</option>
          <option value="image">Изображение / Инфографика / Фото</option>
          <option value="video">Обучающее видео (YouTube, Rutube, Ссылка)</option>
          <option value="file">Файл / Документ / Бланк для скачивания</option>
        </select>
      </div>

      <div class="form-group">
        <label>Заголовок / Название пункта</label>
        <input type="text" id="articleBlockTitleInput">
      </div>

      <div class="form-group" id="grpBlockText">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:5px;">
          <label style="margin:0;">Текст описания / Инструкция</label>
          <button type="button" class="btn btn-outline" style="padding:2px 8px; font-size:0.75rem;" onclick="openLinkHelperModal()">🔗 Вставить ссылку на страницу</button>
        </div>
        <textarea id="articleBlockTextInput" style="min-height:120px;"></textarea>
      </div>

      <div class="form-group" id="grpBlockUrl" style="display:none;">
        <label>Ссылка на медиа / файл (URL)</label>
        <input type="text" id="articleBlockUrlInput" placeholder="https://... (прямая ссылка, YouTube или диск)">
      </div>

      <div class="modal-actions">
        <button class="btn btn-outline" onclick="closeArticleBlockModal()">Отмена</button>
        <button class="btn btn-primary" onclick="saveArticleBlock()">Сохранить блок</button>
      </div>
    </div>
  </div>

  <!-- Помощник вставки ссылки в текст -->
  <div class="modal-overlay" id="linkHelperModal" style="z-index: 2800;">
    <div class="modal-window" style="max-width:480px;">
      <div class="modal-title">Вставить ссылку на страницу базы</div>
      <div class="form-group">
        <label>Текст, который станет ссылкой:</label>
        <input type="text" id="helperLinkText" placeholder="Например: алгоритм подготовки оперблока">
      </div>
      <div class="form-group">
        <label>На какую страницу переводить:</label>
        <select id="helperLinkTargetPage"></select>
      </div>
      <div class="modal-actions">
        <button class="btn btn-outline" onclick="document.getElementById('linkHelperModal').classList.remove('active')">Отмена</button>
        <button class="btn btn-primary" onclick="insertLinkCodeIntoTextarea()">Вставить в текст</button>
      </div>
    </div>
  </div>

  <!-- 5. МОДАЛЬНОЕ ОКНО: СОТРУДНИКИ И ДОПУСК ПО РОЛЯМ (МАТРИЦА ВЕТМЕНЕДЖЕР) -->
  <div class="modal-overlay" id="usersModal">
    <div class="modal-window" style="max-width: 860px;">
      <div class="modal-title">Сотрудники клиники и допуск к разделам</div>
      
      <!-- Вкладки допуска по ролям и пользователей -->
      <div class="vetmanager-tabs">
        <div class="vm-tab active" id="tabRolesBtn" onclick="switchVmTab('roles')">Допуск к разделам по ролям</div>
        <div class="vm-tab" id="tabUsersBtn" onclick="switchVmTab('users')">Список пользователей</div>
      </div>

      <!-- Вкладка 1: Матрица допуска по ролям -->
      <div id="vmRolesTabContent">
        <p style="font-size:0.8rem; color:var(--text-muted); margin-bottom:12px;">
          Нажмите на ячейку для переключения допуска (зелёный — разрешено, красный — запрещено).
        </p>
        <div style="margin-bottom:12px;">
          <label style="font-size:0.8rem; font-weight:700;">Выберите должность / роль:</label>
          <select id="vmSelectRole" onchange="renderRolePermissionsMatrix()" style="padding:6px 10px; border-radius:6px; border:1px solid var(--brand-border); margin-left:8px;">
            <option value="operator">Операторы колл-центра</option>
            <option value="reception">Администраторы рецепции</option>
            <option value="assistant">Ассистенты врачей</option>
            <option value="doctor">Ветеринарные врачи</option>
            <option value="head">Заведующие отделениями</option>
          </select>
        </div>
        <table class="perm-grid-table" id="vmRolePermsTable"></table>
      </div>

      <!-- Вкладка 2: Пользователи -->
      <div id="vmUsersTabContent" style="display:none;">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
          <span style="font-size:0.85rem; color:var(--text-muted);">Зарегистрированные пользователи:</span>
          <button class="btn btn-primary" onclick="openCreateUserForm()">+ Зарегистрировать сотрудника</button>
        </div>
        <table class="styled-table" style="margin-top:0;">
          <thead><tr><th>ФИО</th><th>Логин</th><th>Email</th><th>Роль</th><th>Действие</th></tr></thead>
          <tbody id="usersTableBody"></tbody>
        </table>
      </div>

      <div class="modal-actions">
        <button class="btn btn-outline" onclick="closeUsersModal()">Закрыть</button>
      </div>
    </div>
  </div>

  <!-- Создание нового пользователя -->
  <div class="modal-overlay" id="newUserModal" style="z-index: 2900;">
    <div class="modal-window" style="max-width: 440px;">
      <div class="modal-title">Новый сотрудник</div>
      <div class="form-group"><label>ФИО</label><input type="text" id="newFullName" required></div>
      <div class="form-group"><label>Email</label><input type="email" id="newEmail" placeholder="employee@mail.ru" required></div>
      <div class="form-group"><label>Логин</label><input type="text" id="newUsername" required></div>
      <div class="form-group"><label>Пароль</label><input type="password" id="newPassword" required></div>
      <div class="form-group">
        <label>Роль в системе</label>
        <select id="newRole">
          <option value="operator">Оператор колл-центра</option>
          <option value="reception">Администратор рецепции</option>
          <option value="assistant">Ассистент врача</option>
          <option value="doctor">Ветеринарный врач</option>
          <option value="head">Заведующий отделением</option>
          <option value="admin">Управляющий (Полный доступ)</option>
        </select>
      </div>
      <div class="modal-actions">
        <button class="btn btn-outline" onclick="document.getElementById('newUserModal').classList.remove('active')">Отмена</button>
        <button class="btn btn-primary" onclick="saveNewUser()">Зарегистрировать</button>
      </div>
    </div>
  </div>

  <script>
    /* ПАРАМЕТРЫ FIREBASE */
    const firebaseConfig = {
      apiKey: "AIzaSyD_jmZbvNN73hL4fOiSbSpzH-v43wLSkGw",
      authDomain: "wikivet-nadezhda.firebaseapp.com",
      databaseURL: "https://wikivet-nadezhda-default-rtdb.europe-west1.firebasedatabase.app",
      projectId: "wikivet-nadezhda",
      storageBucket: "wikivet-nadezhda.firebasestorage.app",
      messagingSenderId: "832981921004",
      appId: "1:832981921004:web:411a7d5302018a47f9c9c9",
      measurementId: "G-MBJTPYW46H"
    };

    let firebaseDb = null;
    let isCloudOnline = false;

    try {
      firebase.initializeApp(firebaseConfig);
      firebaseDb = firebase.database();
      isCloudOnline = true;
    } catch(err) {
      console.warn("Firebase error:", err);
    }

    const DEFAULT_LOGO_DATA_URL = `data:image/svg+xml;utf8,<svg viewBox="0 0 460 120" xmlns="http://www.w3.org/2000/svg"><path d="M46 8C48 3 53 1 58 4C63 7 60 14 62 18C65 19 69 19 72 22C77 26 81 33 76 39C72 44 65 44 63 46C60 48 60 52 61 55C62 58 64 61 62 65C60 70 56 74 53 78C50 82 46 87 40 90C35 93 28 95 23 94C18 93 14 91 10 88C5 84 2 79 1 74C-1 67 2 61 6 56C10 52 14 47 17 41C20 35 23 27 28 21C32 16 39 12 46 8Z" fill="%230088D4"/><path d="M74 21C77 15 81 12 85 16C89 20 86 27 88 32C92 34 97 38 98 43C100 48 98 54 98 59C97 64 99 69 102 73C106 79 112 85 116 91C119 96 118 102 113 105C108 108 101 107 96 104C91 101 87 97 84 93C82 89 80 84 79 79C78 74 76 69 75 64Z" fill="%230088D4"/><path d="M12 70C14 85 24 100 42 106C58 111 76 109 90 102C102 96 112 85 115 72C117 62 116 52 112 42C108 32 101 24 93 18C90 16 88 18 87 22C85 27 82 32 78 35C74 38 69 39 64 36C60 33 58 28 58 23C58 18 55 12 51 9C46 6 41 8 38 12C34 18 29 25 25 33C20 42 16 52 13 62Z" fill="%230088D4"/><path d="M45 42H71V59H88V85H71V102H45V85H28V59H45V42Z" fill="%23FFFFFF"/><text x="135" y="42" font-family="'Playfair Display', Georgia, serif" font-style="italic" font-size="19" fill="%230088D4">ветеринарная  клиника</text><text x="135" y="86" font-family="'Inter', sans-serif" font-weight="800" font-size="44" fill="%230088D4" letter-spacing="3.5">НАДЕЖДА</text></svg>`;

    const DEFAULT_USERS = [
      { id: "u_korotets", fullName: "korotets", email: "korotets@mail.ru", username: "korotets", password: "korotets", role: "operator", roleName: "Оператор колл-центра" },
      { id: "u_admin", fullName: "Анастасия Евгеньевна", email: "admin@nadezhda.vet", username: "admin", password: "admin123", role: "admin", roleName: "Управляющая клиникой" },
      { id: "u_head", fullName: "Елена Валерьевна", email: "head@nadezhda.vet", username: "head_med", password: "1234", role: "head", roleName: "Заведующая отделением" }
    ];

    const VM_MODULES = [
      { id: "mod_callcenter", name: "Колл-центр и операторы" },
      { id: "mod_heads", name: "Заведующие отделениями" },
      { id: "mod_surgery", name: "Хирургия и оперблок" },
      { id: "mod_admin", name: "Администраторы и служба заботы" },
      { id: "mod_therapy", name: "Терапевтическое отделение" },
      { id: "mod_assistants", name: "Ассистенты врачей" },
      { id: "mod_mri", name: "Отделение МРТ/КТ" },
      { id: "mod_regulations", name: "Регламенты работы" },
      { id: "mod_anesthesia", name: "Анестезиология" },
      { id: "mod_laboratory", name: "Лаборатория" }
    ];

    /* СТРАНИЦЫ БАЗЫ ЗНАНИЙ */
    const DEFAULT_PAGES = [
      {
        id: "home",
        title: "Главная страница базы знаний",
        category: "ОБЩИЕ СВЕДЕНИЯ",
        badge: "Актуально на 2026 г.",
        showInSidebar: true,
        blocks: [
          { type: "banner", title: "Единая корпоративная база знаний клиники «Надежда»", text: "Портал стандартов, стандартных операционных процедур (СОП), чек-листов и обучающих программ." },
          { type: "yandex", title: "Корпоративное хранилище документов на Яндекс Диске", url: "https://disk.yandex.ru/d/5HlCdgS2idp2Gg" }
        ]
      },
      {
        id: "page_operators",
        title: "Скрипты звонков и консультаций",
        category: "ОПЕРАТОРЫ (КОЛЛ-ЦЕНТР)",
        badge: "Колл-центр",
        showInSidebar: true,
        blocks: [
          { type: "banner", title: "Золотое правило оператора", text: "Снятие трубки до третьего гудка. Всегда уточняйте наличие экстренных симптомов у питомца в первые 30 секунд разговора. При подозрении на хирургию переходите в [Предоперационную подготовку -> page_surgery]." },
          { type: "checklist", title: "Контрольный чек-лист звонка", items: ["Приветствие с представлением клиники", "Уточнить кличку, возраст и породу", "Проверить одышку, судороги и рвоту", "Предупредить о голодной диете 6-8 часов"] }
        ]
      },
      {
        id: "page_heads",
        title: "Регламент заведующих отделениями",
        category: "ЗАВЕДУЮЩИЕ ОТДЕЛЕНИЯМИ",
        badge: "Руководство",
        showInSidebar: true,
        blocks: [
          { type: "banner", title: "Стандарты курации смен", text: "Ежедневный аудит электронных карт в Ветменеджере, разбор спорных клинических случаев, консилиумы." }
        ]
      },
      {
        id: "page_surgery",
        title: "Хирургическое отделение и оперблок",
        category: "ХИРУРГИЯ И ОПЕРБЛОК",
        badge: "Оперблок",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Предоперационная подготовка", text: "Животные брахицефалических пород и пациенты старше 6 лет допускаются строго после ЭхоКГ сердца. Смотрите также [правила асептики ассистентов -> page_assistants]." },
          { type: "image", title: "Схема фиксации пациента на операционном столе", url: "https://images.unsplash.com/photo-1576201836106-db1758fd1c97?w=1000&auto=format&fit=crop&q=80" }
        ]
      },
      {
        id: "page_admin",
        title: "Администраторы и служба заботы",
        category: "АДМИНИСТРАТОРЫ И РЕЦЕПЦИЯ",
        badge: "Рецепция",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Стандарты встречи клиентов", text: "Встреча клиента стоя, приветствие и зрительный контакт в первые 5 секунд после входа в холл клиники." }
        ]
      },
      {
        id: "page_therapy",
        title: "Терапевтическое отделение",
        category: "ТЕРАПИЯ",
        badge: "Терапия",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Доказательные алгоритмы", text: "Обязательный диагностический минимум: общий и биохимический анализ крови, УЗИ обзорное." }
        ]
      },
      {
        id: "page_assistants",
        title: "Ассистенты ветеринарного врача",
        category: "АССИСТЕНТЫ ВРАЧЕЙ",
        badge: "Процедурный кабинет",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Постановка венозных катетеров", text: "Шерсть выбривается с запасом, обработка антисептиком 30 секунд. Гепариновый замок обновляется каждые 8 часов." }
        ]
      },
      {
        id: "page_mri_ct",
        title: "Отделение МРТ и КТ диагностики",
        category: "ТОМОГРАФИЯ",
        badge: "Томография",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Безопасность томографа", text: "Категорически запрещён вход с ферромагнитными предметами. Все ошейники и карабины снимаются до зоны сканирования." }
        ]
      },
      {
        id: "page_regulations",
        title: "Общеклинические регламенты работы",
        category: "РЕГЛАМЕНТЫ РАБОТЫ",
        badge: "Внутренний распорядок",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Трудовой распорядок", text: "Смена начинается за 15 минут до открытия для приёма стационара, осмотра боксов и проверки оборудования." }
        ]
      },
      {
        id: "page_anesthesia",
        title: "Анестезиология и реанимация",
        category: "АНЕСТЕЗИОЛОГИЯ",
        badge: "ОРИТ",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Мониторинг витальных функций", text: "Капнография, пульсоксиметрия, ЭКГ и артериальное давление фиксируются в наркозной карте каждые 5 минут." }
        ]
      },
      {
        id: "page_laboratory",
        title: "Клиническая лаборатория",
        category: "ЛАБОРАТОРИЯ",
        badge: "Анализы",
        showInSidebar: false,
        blocks: [
          { type: "banner", title: "Преаналитический этап", text: "Маркировка пробирок (ЭДТА, цитрат, биохимия) производится строго в присутствии владельца сразу после забора крови." }
        ]
      }
    ];

    /* КАРТОЧКИ НА ГЛАВНОЙ СТРАНИЦЕ */
    const DEFAULT_DASH_CARDS = [
      { id: "c_operators", title: "Колл-центр и операторы", desc: "Скрипты консультаций, запись к узким специалистам, триаж.", icon: "🎧", pageId: "page_operators", color: "linear-gradient(135deg, #0088D4, #00A6FF)" },
      { id: "c_heads", title: "Заведующие отделениями", desc: "Контроль историй болезни, аудит смен, консилиумы.", icon: "🏛️", pageId: "page_heads", color: "linear-gradient(135deg, #0B3558, #185285)" },
      { id: "c_surgery", title: "Хирургия и оперблок", desc: "Предоперационный чек-лист, наркозный протокол, стерилизация.", icon: "🔪", pageId: "page_surgery", color: "linear-gradient(135deg, #0F766E, #14B8A6)" },
      { id: "c_admin", title: "Администраторы и служба заботы", desc: "Встреча клиентов, оформление в Ветменеджере, сервис.", icon: "💻", pageId: "page_admin", color: "linear-gradient(135deg, #0088D4, #0284C7)" },
      { id: "c_therapy", title: "Терапия", desc: "Протоколы доказательной терапии, анализы, диагностика.", icon: "🩺", pageId: "page_therapy", color: "linear-gradient(135deg, #0284C7, #38BDF8)" },
      { id: "c_assistants", title: "Ассистенты", desc: "Забор крови, катетеры, асептика, подготовка процедурных.", icon: "🩸", pageId: "page_assistants", color: "linear-gradient(135deg, #7C3AED, #A78BFA)" },
      { id: "c_mri_ct", title: "Отделение МРТ/КТ", desc: "Подготовка к томографии, укладки, контрастные протоколы.", icon: "🏥", pageId: "page_mri_ct", color: "linear-gradient(135deg, #6366F1, #818CF8)" },
      { id: "c_regulations", title: "Регламенты работы", desc: "Общеклинические правила, график, дисциплина, безопасность.", icon: "📋", pageId: "page_regulations", color: "linear-gradient(135deg, #64748B, #94A3B8)" },
      { id: "c_anesthesia", title: "Анестезиология", desc: "Протоколы седации, мониторинг витальных функций, реанимация.", icon: "💉", pageId: "page_anesthesia", color: "linear-gradient(135deg, #9333EA, #C084FC)" },
      { id: "c_laboratory", title: "Лаборатория", desc: "Правила взятия биоматериала, хранение, экспресс-тесты.", icon: "🔬", pageId: "page_laboratory", color: "linear-gradient(135deg, #059669, #34D399)" }
    ];

    let pagesList = JSON.parse(localStorage.getItem('nadezhda_pages_v70')) || DEFAULT_PAGES;
    let dashCards = JSON.parse(localStorage.getItem('nadezhda_cards_v70')) || DEFAULT_DASH_CARDS;
    let usersList = JSON.parse(localStorage.getItem('nadezhda_users_v70')) || DEFAULT_USERS;
    let rolePermissions = JSON.parse(localStorage.getItem('nadezhda_role_perms_v70')) || {};
    let customLogo = localStorage.getItem('nadezhda_uploaded_logo') || DEFAULT_LOGO_DATA_URL;

    let currentUser = JSON.parse(sessionStorage.getItem('nadezhda_active_user')) || null;
    let currentPageId = "home";
    let navHistory = [];

    /* ОБЛАЧНАЯ СИНХРОНИЗАЦИЯ */
    function syncToCloud(key, data) {
      localStorage.setItem('nadezhda_' + key + '_v70', JSON.stringify(data));
      if (firebaseDb && isCloudOnline) {
        firebaseDb.ref(key + '_v70').set(data).catch(e => console.error("Firebase write error:", e));
      }
    }

    function initCloudListeners() {
      if (!firebaseDb || !isCloudOnline) {
        const badge = document.getElementById('cloudStatusBadge');
        if (badge) { badge.innerText = "💾 Локально"; badge.style.background = "var(--accent-amber-bg)"; badge.style.color = "var(--accent-amber)"; }
        return;
      }

      firebaseDb.ref('pages_v70').on('value', s => { if (s.val()) { pagesList = s.val(); renderPage(currentPageId); renderSidebar(); } });
      firebaseDb.ref('cards_v70').on('value', s => { if (s.val()) { dashCards = s.val(); if (currentPageId === 'home') renderPage('home'); } });
      firebaseDb.ref('users_v70').on('value', s => { if (s.val()) { usersList = s.val(); } });
      firebaseDb.ref('perms_v70').on('value', s => { if (s.val()) { rolePermissions = s.val(); } });
      firebaseDb.ref('logo').on('value', s => { if (s.val()) { customLogo = s.val(); applyCurrentLogo(); } });
    }

    function initApp() {
      applyCurrentLogo();
      initCloudListeners();

      if (!currentUser) {
        document.getElementById('authScreen').style.display = 'flex';
      } else {
        document.getElementById('authScreen').style.display = 'none';
        applyUserSession();
        renderSidebar();
        openDoc('home');
      }
    }

    function applyCurrentLogo() {
      document.getElementById('authLogoImg').src = customLogo;
      document.getElementById('headerLogoImg').src = customLogo;
    }

    function handleLogoUpload(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(evt) {
        customLogo = evt.target.result;
        localStorage.setItem('nadezhda_uploaded_logo', customLogo);
        if (firebaseDb && isCloudOnline) firebaseDb.ref('logo').set(customLogo);
        applyCurrentLogo();
        alert('Логотип клиники успешно обновлен!');
      };
      reader.readAsDataURL(file);
    }

    function toggleMobileSidebar() {
      document.getElementById('sidebar').classList.toggle('open');
      document.getElementById('sidebarOverlay').classList.toggle('active');
    }

    function togglePassVisibility(inputId, btnEl) {
      const el = document.getElementById(inputId);
      if (el.type === 'password') { el.type = 'text'; btnEl.innerText = '🔒'; }
      else { el.type = 'password'; btnEl.innerText = '👁️'; }
    }

    async function handleLogin(e) {
      e.preventDefault();
      const submitBtn = document.getElementById('loginSubmitBtn');
      submitBtn.innerText = 'Проверка...';
      submitBtn.disabled = true;

      const loginVal = document.getElementById('loginUsername').value.trim().toLowerCase();
      const passVal = document.getElementById('loginPassword').value.trim();

      let targetList = usersList;
      if (firebaseDb && isCloudOnline) {
        try {
          const snap = await firebaseDb.ref('users_v70').once('value');
          if (snap.val()) targetList = snap.val();
        } catch(err) {}
      }

      const user = targetList.find(x => {
        const uName = (x.username || '').trim().toLowerCase();
        const uMail = (x.email || '').trim().toLowerCase();
        return (uName === loginVal || uMail === loginVal) && x.password === passVal;
      });

      submitBtn.innerText = 'Войти в систему';
      submitBtn.disabled = false;

      if (user) {
        currentUser = user;
        sessionStorage.setItem('nadezhda_active_user', JSON.stringify(currentUser));
        document.getElementById('authScreen').style.display = 'none';
        applyUserSession();
        renderSidebar();
        openDoc('home');
      } else {
        alert('Неверный логин или пароль!');
      }
    }

    function logout() {
      sessionStorage.removeItem('nadezhda_active_user');
      location.reload();
    }

    function applyUserSession() {
      document.getElementById('headerName').innerText = currentUser.fullName;
      document.getElementById('headerRole').innerText = currentUser.roleName;
      document.getElementById('headerAvatar').innerText = currentUser.fullName.charAt(0);

      const canManage = currentUser.role === 'admin' || currentUser.role === 'head';
      document.getElementById('usersManageBtn').style.display = canManage ? 'inline-flex' : 'none';
      document.getElementById('btnUploadLogo').style.display = (currentUser.role === 'admin') ? 'inline-flex' : 'none';
      document.getElementById('adminSidebarFooter').style.display = (currentUser.role === 'admin') ? 'block' : 'none';
    }

    /* САЙДБАР */
    function renderSidebar() {
      const nav = document.getElementById('navContainer');
      nav.innerHTML = '';

      const testItem = document.createElement('div');
      testItem.className = `nav-item ${currentPageId === 'my_tests' ? 'active' : ''}`;
      testItem.onclick = () => { openDoc('my_tests'); if (window.innerWidth <= 900) toggleMobileSidebar(); };
      testItem.innerHTML = `<span class="nav-item-title">🎓 Мои тестирования</span>`;
      nav.appendChild(testItem);

      const visiblePages = pagesList.filter(p => p.showInSidebar || p.id === 'home');
      const grouped = {};

      visiblePages.forEach(p => {
        const cat = p.category || 'ОБЩИЕ СВЕДЕНИЯ';
        if (!grouped[cat]) grouped[cat] = [];
        grouped[cat].push(p);
      });

      for (const [catName, catPages] of Object.entries(grouped)) {
        const section = document.createElement('div');
        section.className = 'nav-category';
        section.innerHTML = `<div class="nav-cat-header"><span class="nav-cat-title">${catName}</span></div>`;

        catPages.forEach(p => {
          const item = document.createElement('div');
          item.className = `nav-item ${p.id === currentPageId ? 'active' : ''}`;
          item.onclick = () => {
            openDoc(p.id);
            if (window.innerWidth <= 900) toggleMobileSidebar();
          };
          item.innerHTML = `<span class="nav-item-title" title="${p.title}">${p.title}</span>`;
          section.appendChild(item);
        });

        nav.appendChild(section);
      }
    }

    /* КЛИК ПО КАРТОЧКЕ */
    function handleCardClick(cardId) {
      const card = dashCards.find(c => c.id === cardId);
      if (!card) return;

      let targetPageId = card.pageId;

      if (!targetPageId || targetPageId === 'home' || !pagesList.some(p => p.id === targetPageId)) {
        targetPageId = 'page_' + card.id.replace('c_', '');
        pagesList.push({
          id: targetPageId,
          title: card.title,
          category: card.title.toUpperCase(),
          badge: 'Регламент',
          showInSidebar: false,
          blocks: [
            { type: 'banner', title: 'Основное положение: ' + card.title, text: card.desc || 'Опишите стандарты и алгоритмы действий отделения...' }
          ]
        });
        card.pageId = targetPageId;
        syncToCloud('pages_v70', pagesList);
        syncToCloud('cards_v70', dashCards);
      }

      openDoc(targetPageId);
    }

    /* НАВИГАЦИЯ */
    function openDoc(pageId, isBackAction = false) {
      if (!isBackAction && currentPageId && currentPageId !== pageId) {
        navHistory.push(currentPageId);
      }
      currentPageId = pageId;
      renderSidebar();
      renderPage(pageId);
    }

    function goBackPage() {
      if (navHistory.length > 0) {
        openDoc(navHistory.pop(), true);
      } else {
        openDoc('home', true);
      }
    }

    function parseInternalWikiLinks(rawText) {
      if (!rawText) return '';
      return rawText.replace(/\[(.*?)->(.*?)\]/g, function(match, linkText, targetPageId) {
        const cleanText = linkText.trim();
        const cleanId = targetPageId.trim();
        return `<a class="wiki-internal-link" onclick="openDoc('${cleanId}')" title="Перейти на страницу">${cleanText} ↗</a>`;
      });
    }

    /* КАРТОЧКИ НА ГЛАВНОЙ */
    function moveCard(index, direction, e) {
      if (e) e.stopPropagation();
      const newIndex = index + direction;
      if (newIndex < 0 || newIndex >= dashCards.length) return;
      const temp = dashCards[index];
      dashCards[index] = dashCards[newIndex];
      dashCards[newIndex] = temp;
      syncToCloud('cards_v70', dashCards);
      renderPage('home');
    }

    function duplicateCard(cardId, e) {
      if (e) e.stopPropagation();
      const original = dashCards.find(c => c.id === cardId);
      if (!original) return;

      const originalPage = pagesList.find(p => p.id === original.pageId) || { blocks: [] };
      const newPageId = 'page_' + Date.now();
      pagesList.push({
        id: newPageId,
        title: original.title + ' (Копия)',
        category: originalPage.category || 'ОБЩИЕ СВЕДЕНИЯ',
        badge: 'Регламент',
        showInSidebar: false,
        blocks: JSON.parse(JSON.stringify(originalPage.blocks || []))
      });

      const newCardId = 'card_' + Date.now();
      dashCards.push({
        id: newCardId,
        title: original.title + ' (Копия)',
        desc: original.desc,
        icon: original.icon,
        pageId: newPageId,
        color: original.color
      });

      syncToCloud('pages_v70', pagesList);
      syncToCloud('cards_v70', dashCards);
      renderPage('home');
    }

    function moveArticleBlock(index, direction) {
      const page = pagesList.find(p => p.id === currentPageId);
      if (!page || !page.blocks) return;
      const newIndex = index + direction;
      if (newIndex < 0 || newIndex >= page.blocks.length) return;
      const temp = page.blocks[index];
      page.blocks[index] = page.blocks[newIndex];
      page.blocks[newIndex] = temp;
      syncToCloud('pages_v70', pagesList);
      renderPage(currentPageId);
    }

    function duplicateArticleBlock(index) {
      const page = pagesList.find(p => p.id === currentPageId);
      if (!page || !page.blocks[index]) return;
      const copy = JSON.parse(JSON.stringify(page.blocks[index]));
      copy.title = (copy.title || '') + ' (Копия)';
      page.blocks.splice(index + 1, 0, copy);
      syncToCloud('pages_v70', pagesList);
      renderPage(currentPageId);
    }

    /* ИИ ПОИСК ПО РАЗДЕЛАМ */
    function handleSearchKeyDown(e) { if (e.key === 'Enter') runAISearch(); }
    function runAISearch() {
      const q = document.getElementById('searchInput').value.trim().toLowerCase();
      if (!q) return;

      const scored = pagesList.map(p => {
        let text = (p.title + ' ' + (p.category || '')).toLowerCase();
        (p.blocks || []).forEach(b => { text += ' ' + (b.title || '') + ' ' + (b.text || '') + ' ' + (b.items ? b.items.join(' ') : ''); });
        let s = 0;
        if (text.includes(q)) s += 10;
        if (q.includes('судорог') && text.includes('триаж')) s += 8;
        if (q.includes('наркоз') && text.includes('подготовк')) s += 8;
        if (q.includes('диет') && text.includes('голод')) s += 8;
        return { page: p, score: s };
      }).filter(x => x.score > 0);

      const area = document.getElementById('documentArea');
      let resHtml = scored.map(r => `
        <div class="dash-card" onclick="openDoc('${r.page.id}')" style="margin-bottom:14px; cursor:pointer;">
          <div class="dash-card-content">
            <h3 style="color:var(--brand-deep);">${r.page.title}</h3>
            <small style="color:var(--text-muted);">${r.page.category || 'Регламент'}</small>
          </div>
        </div>
      `).join('');

      area.innerHTML = `
        <div class="doc-header">
          <div>
            <button class="btn-back" onclick="goBackPage()">← Назад</button>
            <h1 class="doc-title" style="margin-top:10px;">ИИ поиск: «${q}»</h1>
          </div>
        </div>
        <div class="doc-body">${resHtml || '<p style="color:var(--text-muted); padding:20px; background:#fff; border-radius:8px;">По данному запросу ничего не найдено.</p>'}</div>
      `;
    }

    /* РЕНДЕР СТРАНИЦЫ */
    function renderPage(pageId) {
      const area = document.getElementById('documentArea');
      const canEdit = currentUser && (currentUser.role === 'admin' || currentUser.role === 'head');

      // 1. Главная страница
      if (pageId === 'home') {
        const cardsHtml = dashCards.map((c, idx) => {
          const editTools = canEdit ? `
            <div class="dash-card-actions" onclick="event.stopPropagation();">
              <button class="card-tool-btn" title="Сдвинуть влево" onclick="moveCard(${idx}, -1, event)">◀</button>
              <button class="card-tool-btn" title="Сдвинуть вправо" onclick="moveCard(${idx}, 1, event)">▶</button>
              <button class="card-tool-btn" title="Копировать блок" onclick="duplicateCard('${c.id}', event)">📋</button>
              <button class="card-tool-btn" title="Редактировать карточку и ссылку" onclick="openEditCardModal('${c.id}', event)">✏️</button>
              <button class="card-tool-btn" title="Удалить" style="color:var(--accent-red);" onclick="deleteCard('${c.id}', event)">🗑️</button>
            </div>
          ` : '';

          return `
            <div class="dash-card" onclick="handleCardClick('${c.id}')">
              ${editTools}
              <div class="dash-card-img" style="background:${c.color || 'var(--brand-blue)'};">${c.icon || '📌'}</div>
              <div class="dash-card-content">
                <div class="dash-card-title">${c.title}</div>
                <div class="dash-card-desc">${c.desc}</div>
                <div class="dash-card-footer">
                  <span>Перейти в модуль</span>
                  <span>→</span>
                </div>
              </div>
            </div>
          `;
        }).join('');

        area.innerHTML = `
          <div class="doc-header">
            <div>
              <div class="breadcrumbs">База знаний клиники «Надежда»</div>
              <h1 class="doc-title">Операционные направления клиники</h1>
              <div class="doc-meta"><span class="tag tag-blue">Актуально на 2026 г.</span></div>
            </div>
            ${canEdit ? `
              <div style="display:flex; gap:8px;">
                <button class="btn btn-primary" onclick="openCreateCardModal()">+ Добавить направление</button>
              </div>
            ` : ''}
          </div>
          
          <!-- Красная фирменная карточка Яндекс Диска -->
          <div class="yandex-integration-card">
            <div>
              <strong style="color:var(--yandex-red); font-size:1.05rem;">📁 Корпоративное хранилище документов на Яндекс Диске</strong>
              <div style="font-size:0.83rem; color:var(--text-muted); margin-top:3px;">Официальные бланки, договоры и нормативная документация клиники «Надежда»</div>
            </div>
            <a href="https://disk.yandex.ru/d/5HlCdgS2idp2Gg" target="_blank" class="btn btn-yandex" style="font-weight:700;">Перейти к файлам</a>
          </div>

          <div class="dashboard-grid">${cardsHtml}</div>
        `;
        return;
      }

      // 2. Внутренняя страница
      const page = pagesList.find(p => p.id === pageId) || pagesList[0];

      let blocksHtml = (page.blocks || []).map((b, idx) => {
        const editBlockTools = canEdit ? `
          <div class="page-block-tools" onclick="event.stopPropagation();">
            <button class="card-tool-btn" title="Вверх" onclick="moveArticleBlock(${idx}, -1)">▲</button>
            <button class="card-tool-btn" title="Вниз" onclick="moveArticleBlock(${idx}, 1)">▼</button>
            <button class="card-tool-btn" title="Копировать пункт" onclick="duplicateArticleBlock(${idx})">📋</button>
            <button class="card-tool-btn" title="Изменить" onclick="openEditArticleBlockModal(${idx})">✏️</button>
            <button class="card-tool-btn" title="Удалить" style="color:var(--accent-red);" onclick="deleteArticleBlock(${idx})">🗑️</button>
          </div>
        ` : '';

        let contentHtml = '';
        if (b.type === 'checklist') {
          const listItems = (b.items || []).map(i => `<label class="check-item"><input type="checkbox"> <span>${parseInternalWikiLinks(i)}</span></label>`).join('');
          contentHtml = `<div><h3 style="color:var(--brand-deep); margin-bottom:10px;">${b.title}</h3><div class="checklist">${listItems}</div></div>`;
        } else if (b.type === 'image') {
          contentHtml = `
            <div class="media-card">
              ${b.title ? `<div class="media-card-title">${b.title}</div>` : ''}
              <img src="${b.url}" alt="${b.title || 'Изображение'}">
              ${b.text ? `<div style="padding:10px 16px; font-size:0.88rem; color:var(--text-muted);">${parseInternalWikiLinks(b.text)}</div>` : ''}
            </div>
          `;
        } else if (b.type === 'video') {
          let embedUrl = b.url || '';
          if (embedUrl.includes('watch?v=')) embedUrl = embedUrl.replace('watch?v=', 'embed/');
          contentHtml = `
            <div class="media-card">
              ${b.title ? `<div class="media-card-title">🎥 ${b.title}</div>` : ''}
              <div class="media-video-wrap"><iframe src="${embedUrl}" allowfullscreen></iframe></div>
              ${b.text ? `<div style="padding:10px 16px; font-size:0.88rem; color:var(--text-muted);">${parseInternalWikiLinks(b.text)}</div>` : ''}
            </div>
          `;
        } else if (b.type === 'file') {
          contentHtml = `
            <div class="file-attachment-box">
              <div>
                <strong style="color:var(--brand-deep); font-size:0.95rem;">📄 ${b.title || 'Документ для ознакомления'}</strong>
                ${b.text ? `<div style="font-size:0.8rem; color:var(--text-muted); margin-top:2px;">${parseInternalWikiLinks(b.text)}</div>` : ''}
              </div>
              <a href="${b.url || '#'}" target="_blank" class="btn btn-outline">Скачать файл 📥</a>
            </div>
          `;
        } else if (b.type === 'yandex') {
          contentHtml = `
            <div class="yandex-integration-card" style="margin: 10px 0;">
              <div>
                <strong style="color:var(--yandex-red); font-size:1.05rem;">📁 ${b.title || 'Корпоративное хранилище документов на Яндекс Диске'}</strong>
                <div style="font-size:0.83rem; color:var(--text-muted); margin-top:3px;">Официальные файлы и бланки</div>
              </div>
              <a href="${b.url || 'https://disk.yandex.ru/d/5HlCdgS2idp2Gg'}" target="_blank" class="btn btn-yandex" style="font-weight:700;">Перейти к файлам</a>
            </div>
          `;
        } else {
          contentHtml = `<div class="info-banner"><strong>${b.title}</strong><br><div style="margin-top:6px;">${parseInternalWikiLinks(b.text)}</div></div>`;
        }

        return `<div class="page-block-wrapper">${editBlockTools}${contentHtml}</div>`;
      }).join('');

      area.innerHTML = `
        <div class="doc-header">
          <div>
            <div class="doc-nav-row">
              <button class="btn-back" onclick="goBackPage()">← Назад</button>
              <div class="breadcrumbs"><a onclick="openDoc('home')">База знаний</a> / ${page.category || 'Регламент'}</div>
            </div>
            <h1 class="doc-title">${page.title}</h1>
            <div class="doc-meta">
              <span class="tag tag-blue">${page.category || 'Регламент'}</span>
              <span class="tag tag-green">Актуально на 2026 г.</span>
            </div>
          </div>
          ${canEdit ? `
            <div style="display:flex; gap:8px;">
              <button class="btn btn-primary" onclick="openCreateArticleBlockModal()">+ Добавить пункт</button>
              <button class="btn btn-outline" style="color:var(--accent-red); border-color:var(--accent-red);" onclick="deletePage('${page.id}')">🗑️ Удалить страницу</button>
            </div>
          ` : ''}
        </div>
        <div class="doc-body">${blocksHtml || '<div style="padding:24px; background:#fff; border-radius:10px; border:1px solid var(--brand-border); text-align:center; color:var(--text-muted);">На этой странице пока нет пунктов. Нажмите «+ Добавить пункт», чтобы добавить текст, чек-лист, видео или фото.</div>'}</div>
      `;

      area.querySelectorAll('.check-item input').forEach(input => {
        input.addEventListener('change', (e) => {
          if (e.target.checked) e.target.parentElement.classList.add('done');
          else e.target.parentElement.classList.remove('done');
        });
      });
    }

    /* УПРАВЛЕНИЕ КАРТОЧКАМИ НА ГЛАВНОЙ */
    function populatePageSelect(selectEl, selectedPageId) {
      let html = `<option value="CREATE_NEW" style="font-weight:800; color:var(--brand-blue);">✨ + Создать новую отдельную страницу под этот блок</option>`;
      pagesList.filter(p => p.id !== 'home').forEach(p => {
        html += `<option value="${p.id}" ${p.id === selectedPageId ? 'selected' : ''}>${p.title} (${p.category || 'Раздел'})</option>`;
      });
      selectEl.innerHTML = html;
    }

    function openCreateCardModal() {
      document.getElementById('modalCardId').value = '';
      document.getElementById('moduleModalTitle').innerText = 'Новое операционное направление';
      document.getElementById('modalTitleInput').value = '';
      document.getElementById('modalDescInput').value = '';
      document.getElementById('modalIconInput').value = '📌';
      populatePageSelect(document.getElementById('modalPageSelect'), 'CREATE_NEW');
      document.getElementById('moduleModal').classList.add('active');
    }

    function openEditCardModal(cardId, e) {
      if (e) e.stopPropagation();
      const c = dashCards.find(x => x.id === cardId);
      if (!c) return;

      document.getElementById('modalCardId').value = c.id;
      document.getElementById('moduleModalTitle').innerText = 'Редактировать направление';
      document.getElementById('modalTitleInput').value = c.title;
      document.getElementById('modalDescInput').value = c.desc;
      document.getElementById('modalIconInput').value = c.icon || '📌';
      document.getElementById('modalColorSelect').value = c.color || 'linear-gradient(135deg, #0088D4, #00A6FF)';
      
      populatePageSelect(document.getElementById('modalPageSelect'), c.pageId);
      document.getElementById('moduleModal').classList.add('active');
    }

    function closeModuleModal() {
      document.getElementById('moduleModal').classList.remove('active');
    }

    function saveCardItem() {
      const id = document.getElementById('modalCardId').value;
      const title = document.getElementById('modalTitleInput').value.trim();
      const desc = document.getElementById('modalDescInput').value.trim();
      const icon = document.getElementById('modalIconInput').value.trim() || '📌';
      const color = document.getElementById('modalColorSelect').value;
      let pageChoice = document.getElementById('modalPageSelect').value;

      if (!title) return alert('Введите название направления!');

      let finalPageId = pageChoice;

      if (pageChoice === 'CREATE_NEW' || !pageChoice || pageChoice === 'home') {
        finalPageId = 'page_' + Date.now();
        pagesList.push({
          id: finalPageId,
          title: title,
          category: title.toUpperCase(),
          badge: 'Регламент',
          showInSidebar: false,
          blocks: [{ type: 'banner', title: 'Основное положение: ' + title, text: desc || 'Заполните содержание регламента...' }]
        });
        syncToCloud('pages', pagesList);
      }

      if (id) {
        const idx = dashCards.findIndex(x => x.id === id);
        if (idx !== -1) dashCards[idx] = { id, title, desc, icon, pageId: finalPageId, color };
      } else {
        dashCards.push({ id: 'card_' + Date.now(), title, desc, icon, pageId: finalPageId, color });
      }

      syncToCloud('cards', dashCards);
      closeModuleModal();
      renderPage('home');
      renderSidebar();
    }

    function deleteCard(cardId, e) {
      if (e) e.stopPropagation();
      if (confirm('Удалить эту карточку направления?')) {
        dashCards = dashCards.filter(c => c.id !== cardId);
        syncToCloud('cards', dashCards);
        renderPage('home');
      }
    }

    /* РЕЕСТР: ВСЕ СУЩЕСТВУЮЩИЕ СТРАНИЦЫ */
    function openAllPagesManagerModal() {
      renderAllPagesTable();
      document.getElementById('allPagesModal').classList.add('active');
    }

    function renderAllPagesTable() {
      const tbody = document.getElementById('allPagesTableBody');
      tbody.innerHTML = '';

      pagesList.forEach(p => {
        const isHome = p.id === 'home';
        const attachedCard = dashCards.find(c => c.pageId === p.id);

        tbody.innerHTML += `
          <tr>
            <td><strong>${p.title}</strong> ${attachedCard ? `<br><small style="color:var(--brand-blue);">🔗 Карточка: ${attachedCard.title}</small>` : ''}</td>
            <td><code>${p.id}</code></td>
            <td><span class="tag tag-blue">${p.category || '—'}</span></td>
            <td style="text-align:center;">
              ${isHome ? 'Всегда' : `
                <input type="checkbox" ${p.showInSidebar ? 'checked' : ''} onchange="togglePageSidebarVisibility('${p.id}', this.checked)" style="width:17px; height:17px; accent-color:var(--brand-blue); cursor:pointer;">
              `}
            </td>
            <td>
              <button class="btn btn-outline" style="padding:2px 6px;" onclick="openDoc('${p.id}'); document.getElementById('allPagesModal').classList.remove('active');">Открыть</button>
              ${!isHome ? `
                <button class="btn btn-outline" style="padding:2px 6px;" onclick="openEditPageDataModal('${p.id}')">✏️</button>
                <button class="btn btn-outline" style="color:var(--accent-red); padding:2px 6px;" onclick="deletePage('${p.id}')">🗑️</button>
              ` : ''}
            </td>
          </tr>
        `;
      });
    }

    function togglePageSidebarVisibility(pageId, isChecked) {
      const page = pagesList.find(p => p.id === pageId);
      if (page) {
        page.showInSidebar = isChecked;
        syncToCloud('pages', pagesList);
        renderSidebar();
      }
    }

    function openCreateStandalonePageModal() {
      document.getElementById('editPageIdInput').value = '';
      document.getElementById('pageEditModalTitle').innerText = 'Создать новую страницу';
      document.getElementById('editPageTitleInput').value = '';
      document.getElementById('editPageCategoryInput').value = 'ОБЩИЕ СВЕДЕНИЯ';
      document.getElementById('editPageShowInSidebar').checked = false;
      document.getElementById('pageEditModal').classList.add('active');
    }

    function openEditPageDataModal(pageId) {
      const page = pagesList.find(p => p.id === pageId);
      if (!page) return;
      document.getElementById('editPageIdInput').value = page.id;
      document.getElementById('pageEditModalTitle').innerText = 'Редактировать страницу';
      document.getElementById('editPageTitleInput').value = page.title;
      document.getElementById('editPageCategoryInput').value = page.category || '';
      document.getElementById('editPageShowInSidebar').checked = !!page.showInSidebar;
      document.getElementById('pageEditModal').classList.add('active');
    }

    function savePageData() {
      const id = document.getElementById('editPageIdInput').value;
      const title = document.getElementById('editPageTitleInput').value.trim();
      const category = document.getElementById('editPageCategoryInput').value.trim().toUpperCase() || 'ОБЩИЕ СВЕДЕНИЯ';
      const showInSidebar = document.getElementById('editPageShowInSidebar').checked;

      if (!title) return alert('Введите название страницы!');

      if (id) {
        const page = pagesList.find(p => p.id === id);
        if (page) {
          page.title = title;
          page.category = category;
          page.showInSidebar = showInSidebar;
        }
      } else {
        const newId = 'page_' + Date.now();
        pagesList.push({
          id: newId,
          title: title,
          category: category,
          badge: 'Регламент',
          showInSidebar: showInSidebar,
          blocks: [{ type: 'banner', title: 'Основное положение: ' + title, text: 'Заполните содержание регламента...' }]
        });
      }

      syncToCloud('pages', pagesList);
      document.getElementById('pageEditModal').classList.remove('active');
      renderAllPagesTable();
      renderSidebar();
      if (id && currentPageId === id) renderPage(id);
    }

    function deletePage(pageId) {
      if (pageId === 'home') return alert('Главную страницу удалить нельзя!');
      if (confirm('Удалить эту страницу регламента?')) {
        pagesList = pagesList.filter(p => p.id !== pageId);
        dashCards.forEach(c => {
          if (c.pageId === pageId) c.pageId = 'home';
        });
        syncToCloud('pages', pagesList);
        syncToCloud('cards', dashCards);
        renderSidebar();
        renderAllPagesTable();
        openDoc('home');
      }
    }

    /* РЕДАКТИРОВАНИЕ ПУНКТОВ РЕГЛАМЕНТА */
    function toggleArticleBlockFields() {
      const type = document.getElementById('articleBlockTypeSelect').value;
      const grpUrl = document.getElementById('grpBlockUrl');
      grpUrl.style.display = (type === 'image' || type === 'video' || type === 'file') ? 'block' : 'none';
    }

    function openCreateArticleBlockModal() {
      document.getElementById('articleBlockIndex').value = '';
      document.getElementById('articleBlockModalTitle').innerText = 'Добавить новый пункт регламента';
      document.getElementById('articleBlockTitleInput').value = '';
      document.getElementById('articleBlockTextInput').value = '';
      document.getElementById('articleBlockUrlInput').value = '';
      document.getElementById('articleBlockTypeSelect').value = 'banner';
      toggleArticleBlockFields();
      document.getElementById('articleBlockModal').classList.add('active');
    }

    function openEditArticleBlockModal(idx) {
      const page = pagesList.find(p => p.id === currentPageId);
      if (!page || !page.blocks[idx]) return;
      const b = page.blocks[idx];

      document.getElementById('articleBlockIndex').value = idx;
      document.getElementById('articleBlockModalTitle').innerText = 'Редактировать пункт';
      document.getElementById('articleBlockTypeSelect').value = b.type || 'banner';
      document.getElementById('articleBlockTitleInput').value = b.title || '';
      document.getElementById('articleBlockTextInput').value = b.text || (b.items ? b.items.join('\n') : '');
      document.getElementById('articleBlockUrlInput').value = b.url || '';
      toggleArticleBlockFields();
      document.getElementById('articleBlockModal').classList.add('active');
    }

    function closeArticleBlockModal() {
      document.getElementById('articleBlockModal').classList.remove('active');
    }

    function saveArticleBlock() {
      const page = pagesList.find(p => p.id === currentPageId);
      if (!page) return;

      const idxStr = document.getElementById('articleBlockIndex').value;
      const type = document.getElementById('articleBlockTypeSelect').value;
      const title = document.getElementById('articleBlockTitleInput').value.trim();
      const text = document.getElementById('articleBlockTextInput').value;
      const url = document.getElementById('articleBlockUrlInput').value.trim();

      page.blocks = page.blocks || [];

      const newBlock = { type, title, text, url };
      if (type === 'checklist') {
        newBlock.items = text.split('\n').filter(x => x.trim());
      }

      if (idxStr !== '') {
        page.blocks[parseInt(idxStr)] = newBlock;
      } else {
        page.blocks.push(newBlock);
      }

      syncToCloud('pages', pagesList);
      closeArticleBlockModal();
      renderPage(currentPageId);
    }

    function deleteArticleBlock(idx) {
      const page = pagesList.find(p => p.id === currentPageId);
      if (!page) return;
      if (confirm('Удалить этот пункт?')) {
        page.blocks.splice(idx, 1);
        syncToCloud('pages', pagesList);
        renderPage(currentPageId);
      }
    }

    /* ПОМОЩНИК ВСТАВКИ ССЫЛКИ В ТЕКСТ */
    function openLinkHelperModal() {
      document.getElementById('helperLinkText').value = '';
      const sel = document.getElementById('helperLinkTargetPage');
      sel.innerHTML = pagesList.map(p => `<option value="${p.id}">${p.title} (${p.category || 'Раздел'})</option>`).join('');
      document.getElementById('linkHelperModal').classList.add('active');
    }

    function insertLinkCodeIntoTextarea() {
      const linkText = document.getElementById('helperLinkText').value.trim() || 'перейти к регламенту';
      const targetId = document.getElementById('helperLinkTargetPage').value;
      const textarea = document.getElementById('articleBlockTextInput');

      const tag = `[${linkText} -> ${targetId}]`;
      textarea.value += (textarea.value ? ' ' : '') + tag;

      document.getElementById('linkHelperModal').classList.remove('active');
    }

    /* ДОПУСК ПО РОЛЯМ И ПОЛЬЗОВАТЕЛИ */
    function openUsersModal() {
      renderRolePermissionsMatrix();
      renderUsersTable();
      document.getElementById('usersModal').classList.add('active');
    }
    function closeUsersModal() { document.getElementById('usersModal').classList.remove('active'); }

    function switchVmTab(tab) {
      document.getElementById('tabRolesBtn').classList.toggle('active', tab === 'roles');
      document.getElementById('tabUsersBtn').classList.toggle('active', tab === 'users');
      document.getElementById('vmRolesTabContent').style.display = (tab === 'roles') ? 'block' : 'none';
      document.getElementById('vmUsersTabContent').style.display = (tab === 'users') ? 'block' : 'none';
    }

    function renderRolePermissionsMatrix() {
      const role = document.getElementById('vmSelectRole').value;
      const table = document.getElementById('vmRolePermsTable');

      rolePermissions[role] = rolePermissions[role] || {};

      let html = `
        <thead>
          <tr>
            <th style="width:34%;">Модуль / Раздел</th>
            <th>Просмотр</th>
            <th>Редактирование</th>
            <th>Удаление</th>
            <th>Администрирование</th>
          </tr>
        </thead>
        <tbody>
      `;

      VM_MODULES.forEach(mod => {
        const p = rolePermissions[role][mod.id] || { view: true, edit: false, del: false, admin: false };
        html += `
          <tr>
            <td>${mod.name}</td>
            <td class="cell-perm ${p.view ? 'checked' : ''}" onclick="togglePerm('${role}', '${mod.id}', 'view')">
              <input type="checkbox" ${p.view ? 'checked' : ''} onclick="event.stopPropagation(); togglePerm('${role}', '${mod.id}', 'view')">
            </td>
            <td class="cell-perm ${p.edit ? 'checked' : ''}" onclick="togglePerm('${role}', '${mod.id}', 'edit')">
              <input type="checkbox" ${p.edit ? 'checked' : ''} onclick="event.stopPropagation(); togglePerm('${role}', '${mod.id}', 'edit')">
            </td>
            <td class="cell-perm ${p.del ? 'checked' : ''}" onclick="togglePerm('${role}', '${mod.id}', 'del')">
              <input type="checkbox" ${p.del ? 'checked' : ''} onclick="event.stopPropagation(); togglePerm('${role}', '${mod.id}', 'del')">
            </td>
            <td class="cell-perm ${p.admin ? 'checked' : ''}" onclick="togglePerm('${role}', '${mod.id}', 'admin')">
              <input type="checkbox" ${p.admin ? 'checked' : ''} onclick="event.stopPropagation(); togglePerm('${role}', '${mod.id}', 'admin')">
            </td>
          </tr>
        `;
      });

      html += '</tbody>';
      table.innerHTML = html;
    }

    function togglePerm(role, modId, permType) {
      rolePermissions[role] = rolePermissions[role] || {};
      rolePermissions[role][modId] = rolePermissions[role][modId] || { view: true, edit: false, del: false, admin: false };
      rolePermissions[role][modId][permType] = !rolePermissions[role][modId][permType];

      syncToCloud('perms', rolePermissions);
      renderRolePermissionsMatrix();
    }

    function renderUsersTable() {
      const tbody = document.getElementById('usersTableBody');
      tbody.innerHTML = '';
      usersList.forEach(u => {
        tbody.innerHTML += `
          <tr>
            <td><strong>${u.fullName}</strong></td><td><code>${u.username}</code></td><td>${u.email||'—'}</td><td>${u.roleName}</td>
            <td>${u.username !== 'admin' ? `<button class="btn btn-outline" style="color:var(--accent-red); padding:2px 6px;" onclick="deleteUser('${u.id}')">Удалить</button>` : 'Администратор'}</td>
          </tr>
        `;
      });
    }

    function openCreateUserForm() { document.getElementById('newUserModal').classList.add('active'); }
    function saveNewUser() {
      const fullName = document.getElementById('newFullName').value.trim();
      const email = document.getElementById('newEmail').value.trim();
      const username = document.getElementById('newUsername').value.trim();
      const password = document.getElementById('newPassword').value.trim();
      const role = document.getElementById('newRole').value;
      const roleName = document.getElementById('newRole').options[document.getElementById('newRole').selectedIndex].text;

      if (!fullName || !username || !password || !email) return alert('Заполните все поля!');
      usersList.push({ id: 'u_' + Date.now(), fullName, email, username, password, role, roleName });
      syncToCloud('users', usersList);
      document.getElementById('newUserModal').classList.remove('active');
      renderUsersTable();
      alert('Сотрудник зарегистрирован!');
    }

    function deleteUser(id) {
      if (confirm('Удалить сотрудника?')) {
        usersList = usersList.filter(u => u.id !== id);
        syncToCloud('users', usersList);
        renderUsersTable();
      }
    }

    function exportData() {
      const blob = new Blob([JSON.stringify({ pages: pagesList, cards: dashCards, users: usersList, perms: rolePermissions }, null, 2)], { type: 'application/json' });
      const a = document.createElement('a'); a.href = URL.createObjectURL(blob);
      a.download = `nadezhda_full_${new Date().toISOString().slice(0,10)}.json`; a.click();
    }

    function importData(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(evt) {
        try {
          const d = JSON.parse(evt.target.result);
          if (d.pages) {
            pagesList = d.pages;
            dashCards = d.cards || dashCards;
            usersList = d.users || usersList;
            rolePermissions = d.perms || rolePermissions;
            syncToCloud('pages', pagesList);
            syncToCloud('cards', dashCards);
            syncToCloud('users', usersList);
            syncToCloud('perms', rolePermissions);
            location.reload();
          }
        } catch(err) { alert('Ошибка импорта'); }
      };
      reader.readAsText(file);
    }

    initApp();
  </script>
</body>
</html>
