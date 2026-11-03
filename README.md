<html lang="am">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Oyaya Bet - Agent Portal</title>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
  <style>
    :root {
      --primary: #020617;
      --accent: #1e40af;
      --bg-body: #090d16;
      --card-bg: #0f172a;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --border: #1e293b;
      --success: #16a34a;
      --warning: #d97706;
      --danger: #dc2626;
      --radius: 10px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    html, body {
      width: 100%;
      height: 100%;
      overflow-x: hidden;
      background-color: var(--bg-body);
      color: var(--text-main);
    }

    body {
      padding-bottom: 40px;
    }

    /* Auth Views (Login & Register) */
    .auth-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: var(--bg-body);
      z-index: 500;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 16px;
    }

    .auth-card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 12px;
      width: 100%;
      max-width: 380px;
      padding: 24px 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.7);
    }

    .auth-brand {
      font-size: 24px;
      font-weight: 800;
      color: #3b82f6;
      text-align: center;
      margin-bottom: 6px;
    }

    .auth-sub {
      font-size: 13px;
      color: var(--text-muted);
      text-align: center;
      margin-bottom: 20px;
    }

    .auth-toggle-link {
      color: #60a5fa;
      font-weight: 600;
      cursor: pointer;
      text-decoration: underline;
    }

    .app-wrapper {
      display: none; /* Hidden until logged in */
    }

    /* Top Navigation Header */
    .app-header {
      background-color: var(--card-bg);
      border-bottom: 1px solid var(--border);
      position: sticky;
      top: 0;
      z-index: 50;
    }

    .header-content {
      width: 100%;
      padding: 12px 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .header-left {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .icon-btn {
      background: transparent;
      border: none;
      font-size: 20px;
      color: var(--text-main);
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .portal-title {
      font-size: 15px;
      font-weight: 600;
      color: var(--text-muted);
    }

    .header-right {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .balance-pill {
      display: flex;
      align-items: center;
      gap: 6px;
      background: #020617;
      padding: 6px 12px;
      border-radius: 20px;
      font-weight: 700;
      font-size: 13px;
      border: 1px solid var(--border);
      color: var(--text-main);
    }

    .status-badge {
      display: flex;
      align-items: center;
      gap: 5px;
      font-size: 12px;
      font-weight: 600;
      color: #4ade80;
      background: rgba(22, 163, 74, 0.2);
      padding: 4px 10px;
      border-radius: 14px;
      border: 1px solid rgba(22, 163, 74, 0.4);
    }

    .status-dot {
      width: 7px;
      height: 7px;
      background-color: #4ade80;
      border-radius: 50%;
    }

    /* Side Navigation Drawer */
    .drawer-overlay {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.8);
      z-index: 100;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
    }

    .drawer-overlay.active {
      opacity: 1;
      pointer-events: auto;
    }

    .drawer {
      position: fixed;
      top: 0;
      left: -280px;
      width: 280px;
      height: 100%;
      background: var(--card-bg);
      z-index: 101;
      transition: left 0.3s ease;
      display: flex;
      flex-direction: column;
      border-right: 1px solid var(--border);
    }

    .drawer.active { left: 0; }

    .drawer-header {
      padding: 16px;
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: #020617;
    }

    .drawer-brand {
      font-size: 18px;
      font-weight: 800;
      color: #3b82f6;
    }

    .drawer-nav {
      padding: 12px 0;
      flex: 1;
      overflow-y: auto;
    }

    .drawer-item {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 14px 18px;
      color: var(--text-main);
      font-weight: 500;
      font-size: 14px;
      cursor: pointer;
      text-decoration: none;
    }

    .drawer-item:hover, .drawer-item.active {
      background: #1e293b;
      color: #60a5fa;
    }

    /* Main Container */
    .container {
      width: 100%;
      padding: 12px;
      max-width: 600px;
      margin: 0 auto;
    }

    .tab-content { display: none; }
    .tab-content.active { display: block; }

    /* Card Component */
    .card {
      background: var(--card-bg);
      border-radius: var(--radius);
      border: 1px solid var(--border);
      padding: 16px;
      margin-bottom: 12px;
      box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.5);
    }

    .card-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 12px;
    }

    .card-title {
      font-size: 15px;
      font-weight: 700;
      color: var(--text-main);
    }

    /* Forms */
    .form-group { margin-bottom: 12px; }

    .form-label {
      display: block;
      font-size: 12px;
      font-weight: 600;
      color: var(--text-muted);
      margin-bottom: 4px;
    }

    .form-control {
      width: 100%;
      padding: 11px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font-size: 14px;
      background: #020617;
      color: var(--text-main);
    }

    .form-control:focus {
      outline: none;
      border-color: #3b82f6;
    }

    /* Buttons */
    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      padding: 12px 16px;
      border-radius: 8px;
      font-weight: 600;
      font-size: 14px;
      cursor: pointer;
      border: none;
      width: 100%;
    }

    .btn-primary { background-color: #1d4ed8; color: white; }
    .btn-secondary { background-color: #1e293b; color: var(--text-main); border: 1px solid var(--border); }
    .btn-danger { background-color: var(--danger); color: white; }
    .btn-sm { padding: 6px 12px; font-size: 12px; width: auto; }

    /* Stats Layout */
    .stat-card {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px;
      background: #020617;
      border: 1px solid var(--border);
      border-radius: 8px;
      margin-bottom: 10px;
    }

    .stat-info { display: flex; flex-direction: column; }
    .stat-label { font-size: 13px; color: var(--text-muted); font-weight: 500; }
    .stat-value { font-size: 18px; font-weight: 700; color: var(--text-main); margin-top: 2px; }
    .stat-sub { font-size: 12px; color: var(--text-muted); }
    .stat-icon { font-size: 20px; }

    /* Dynamic Mobile Table */
    .table-container { overflow-x: auto; }
    table { width: 100%; border-collapse: collapse; text-align: left; font-size: 13px; }
    th { background: #020617; padding: 10px 12px; color: var(--text-muted); font-weight: 600; border-bottom: 1px solid var(--border); white-space: nowrap; }
    td { padding: 12px; border-bottom: 1px solid var(--border); white-space: nowrap; color: var(--text-main); }

    .badge-status { padding: 3px 8px; border-radius: 12px; font-size: 11px; font-weight: 700; }
    .badge-active { background: rgba(22, 163, 74, 0.2); color: #4ade80; border: 1px solid rgba(22, 163, 74, 0.4); }
    .badge-inactive { background: rgba(220, 38, 38, 0.2); color: #f87171; border: 1px solid rgba(220, 38, 38, 0.4); }

    /* Modal Backdrop */
    .modal-backdrop {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.8);
      z-index: 200;
      display: none;
      align-items: center;
      justify-content: center;
      padding: 16px;
    }

    .modal-backdrop.active { display: flex; }
    .modal { background: var(--card-bg); border-radius: 12px; width: 100%; max-width: 400px; overflow: hidden; border: 1px solid var(--border); }
    .modal-header { padding: 14px 16px; border-bottom: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; background: #020617; }
    .modal-title { font-weight: 700; font-size: 15px; color: var(--text-main); }
    .modal-body { padding: 16px; }
    .modal-footer { padding: 12px 16px; background: #020617; border-top: 1px solid var(--border); display: flex; gap: 10px; justify-content: flex-end; }
  </style>
</head>
<body>

  <!-- AUTH / LOGIN OVERLAY -->
  <div class="auth-overlay" id="authOverlay">
    <div class="auth-card" id="loginBox">
      <div class="auth-brand">Oyaya Bet</div>
      <div class="auth-sub">Agent Portal Login</div>
      <form id="loginForm">
        <div class="form-group">
          <label class="form-label">Username</label>
          <input type="text" class="form-control" id="loginUser" placeholder="Enter username" required>
        </div>
        <div class="form-group">
          <label class="form-label">Password</label>
          <input type="password" class="form-control" id="loginPass" placeholder="Enter password" required>
        </div>
        <button type="submit" class="btn btn-primary" style="margin-top: 10px;">Sign In</button>
      </form>
      <div style="font-size: 12px; text-align: center; margin-top: 16px; color: var(--text-muted);">
        Don't have an account? <span class="auth-toggle-link" id="showRegister">Register here</span>
      </div>
    </div>

    <div class="auth-card" id="registerBox" style="display: none;">
      <div class="auth-brand">Oyaya Bet</div>
      <div class="auth-sub">Create Agent Account</div>
      <form id="registerForm">
        <div class="form-group">
          <label class="form-label">Full Name</label>
          <input type="text" class="form-control" placeholder="Enter full name" required>
        </div>
        <div class="form-group">
          <label class="form-label">Username</label>
          <input type="text" class="form-control" placeholder="Choose username" required>
        </div>
        <div class="form-group">
          <label class="form-label">Phone Number</label>
          <input type="text" class="form-control" placeholder="09..." required>
        </div>
        <div class="form-group">
          <label class="form-label">Password</label>
          <input type="password" class="form-control" placeholder="Create password" required>
        </div>
        <button type="submit" class="btn btn-primary" style="margin-top: 10px;">Register Account</button>
      </form>
      <div style="font-size: 12px; text-align: center; margin-top: 16px; color: var(--text-muted);">
        Already registered? <span class="auth-toggle-link" id="showLogin">Sign in</span>
      </div>
    </div>
  </div>

  <!-- MAIN APPLICATION WRAPPER -->
  <div class="app-wrapper" id="appWrapper">
    <!-- Top Navigation Header -->
    <header class="app-header">
      <div class="header-content">
        <div class="header-left">
          <button class="icon-btn" id="menuToggle"><i class="fa-solid fa-bars"></i></button>
          <span class="portal-title">agent-portal</span>
        </div>
        <div class="header-right">
          <div class="balance-pill">
            <i class="fa-regular fa-envelope" style="color:#94a3b8;"></i>
            <span>ETB 0.00</span>
            <i class="fa-solid fa-caret-down" style="font-size: 10px; color:#94a3b8;"></i>
          </div>
          <div class="status-badge">
            <span class="status-dot"></span>
            <span>Active</span>
          </div>
        </div>
      </div>
    </header>

    <!-- Side Navigation Drawer -->
    <div class="drawer-overlay" id="drawerOverlay"></div>
    <aside class="drawer" id="drawer">
      <div class="drawer-header">
        <span class="drawer-brand">Oyaya Bet</span>
        <button class="icon-btn" id="drawerClose"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <nav class="drawer-nav">
        <a class="drawer-item active" data-target="payment-requests">
          <i class="fa-solid fa-credit-card"></i> <span>Payment Requests</span>
        </a>
        <a class="drawer-item" data-target="sms-verification">
          <i class="fa-solid fa-message"></i> <span>SMS Verification</span>
        </a>
        <a class="drawer-item" data-target="banks">
          <i class="fa-solid fa-building-columns"></i> <span>Banks</span>
        </a>
        <a class="drawer-item" data-target="achievements">
          <i class="fa-solid fa-trophy"></i> <span>Achievements</span>
        </a>
        <a class="drawer-item" data-target="reports">
          <i class="fa-solid fa-chart-line"></i> <span>Reports</span>
        </a>
        <a class="drawer-item" data-target="account">
          <i class="fa-regular fa-user"></i> <span>Account</span>
        </a>
        <a class="drawer-item" id="logoutBtn" style="color: var(--danger); margin-top: 20px;">
          <i class="fa-solid fa-right-from-bracket"></i> <span>Logout</span>
        </a>
      </nav>
    </aside>

    <!-- Main View Sections -->
    <main class="container">

      <!-- Payment Requests Tab -->
      <section id="payment-requests" class="tab-content active">
        <div class="card">
          <div class="card-header"><span class="card-title">Payment Requests</span></div>
          <div class="form-group"><input type="text" class="form-control" placeholder="Player / phone"></div>
          <div class="form-group"><select class="form-control"><option>All methods</option></select></div>
          <div class="form-group"><select class="form-control"><option>Select payment method first</option></select></div>
          <div class="form-group"><select class="form-control"><option>All types</option></select></div>
          <div class="form-group"><select class="form-control"><option>All request statuses</option></select></div>
          <div class="form-group" style="display: flex; gap: 8px;">
            <input type="text" class="form-control" value="11/03/2026">
            <input type="text" class="form-control" value="11/03/2026">
          </div>
          <div class="form-group"><select class="form-control"><option>Today</option></select></div>
          <div style="display: flex; gap: 10px;">
            <button class="btn btn-primary"><i class="fa-solid fa-magnifying-glass"></i> Search</button>
            <button class="btn btn-secondary" style="width: auto;"><i class="fa-solid fa-rotate"></i></button>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <span class="card-title">Summary</span>
            <i class="fa-solid fa-angle-up"></i>
          </div>
          <div class="stat-card">
            <div class="stat-info"><span class="stat-label">Successful</span><span class="stat-value">0</span><span class="stat-sub"># 0.00</span></div>
            <i class="fa-solid fa-check stat-icon" style="color: #4ade80;"></i>
          </div>
          <div class="stat-card">
            <div class="stat-info"><span class="stat-label">Pending</span><span class="stat-value">0</span><span class="stat-sub"># 0.00</span></div>
            <i class="fa-regular fa-circle stat-icon" style="color: var(--warning);"></i>
          </div>
          <div class="stat-card">
            <div class="stat-info"><span class="stat-label">Failed</span><span class="stat-value">0</span><span class="stat-sub"># 0.00</span></div>
            <i class="fa-solid fa-xmark stat-icon" style="color: var(--danger);"></i>
          </div>
        </div>
      </section>

      <!-- SMS Verification Tab -->
      <section id="sms-verification" class="tab-content">
        <div class="card">
          <div class="card-header"><span class="card-title">SMS Verification</span></div>
          <div class="form-group">
            <label class="form-label">SMS content</label>
            <textarea class="form-control" rows="4" placeholder="Paste your bank SMS notification here..."></textarea>
          </div>
          <button class="btn btn-primary">Verify SMS</button>
        </div>
      </section>

      <!-- Banks & Wallets Tab -->
      <section id="banks" class="tab-content">
        <div class="card">
          <div class="card-header">
            <span class="card-title">Banks & Wallets</span>
            <button class="btn btn-primary btn-sm" id="openAttachBankModal"><i class="fa-solid fa-plus"></i> Attach Bank</button>
          </div>
          <div class="table-container">
            <table>
              <thead>
                <tr>
                  <th>METHOD</th>
                  <th>ACC NUMBER</th>
                  <th>ACC NAME</th>
                  <th>STATUS</th>
                  <th>ACTIONS</th>
                </tr>
              </thead>
              <tbody id="bankTableBody">
                <!-- Dynamically populated -->
              </tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- Achievements Tab -->
      <section id="achievements" class="tab-content">
        <div class="card">
          <div class="card-header"><span class="card-title">Achievements</span></div>
          <p style="color: var(--text-muted); text-align: center; padding: 20px;">Achievements are not enabled</p>
        </div>
      </section>

      <!-- Reports Tab -->
      <section id="reports" class="tab-content">
        <div class="card">
          <div class="card-header"><span class="card-title">Summary by period</span></div>
          <button class="btn btn-primary"><i class="fa-solid fa-magnifying-glass"></i> Search</button>
        </div>
      </section>

      <!-- Account Tab (with Agent Monitoring Controls) -->
      <section id="account" class="tab-content">
        <div class="card">
          <div class="card-header"><span class="card-title">Attendance</span></div>
          <div style="background: rgba(22, 163, 74, 0.15); padding: 12px; border-radius: 8px; margin-bottom: 10px; border: 1px solid rgba(22, 163, 74, 0.3);">
            <span style="font-size: 11px; color: #4ade80; font-weight: 700;">CURRENT STATUS</span>
            <div style="font-weight: 700; color: #4ade80; font-size: 15px;">Clocked in</div>
          </div>
        </div>

        <div class="card">
          <div class="card-header"><span class="card-title"><i class="fa-solid fa-shield-halved"></i> Agent Monitoring & Controls</span></div>
          
          <div style="display: flex; flex-direction: column; gap: 12px;">
            <div style="background: #020617; padding: 10px; border-radius: 8px; border: 1px solid var(--border);">
              <div style="font-size: 13px; font-weight: 700; color: #60a5fa;">1. Float & Limit Monitoring</div>
              <div style="font-size: 12px; color: var(--text-muted); margin-top: 2px;">Max daily deposit/withdrawal cap: <strong>500,000 ETB</strong></div>
            </div>

            <div style="background: #020617; padding: 10px; border-radius: 8px; border: 1px solid var(--border);">
              <div style="font-size: 13px; font-weight: 700; color: #60a5fa;">2. Auto-Reconciliation Status</div>
              <div style="font-size: 12px; color: #4ade80; margin-top: 2px;"><i class="fa-solid fa-circle-check"></i> Bank statement matched in real-time</div>
            </div>

            <div style="background: #020617; padding: 10px; border-radius: 8px; border: 1px solid var(--border);">
              <div style="font-size: 13px; font-weight: 700; color: #60a5fa;">3. Security & Device Binding</div>
              <div style="font-size: 12px; color: var(--text-muted); margin-top: 2px;">Current Session IP: <strong>196.188.xx.xx (Secure)</strong></div>
            </div>

            <div style="background: #020617; padding: 10px; border-radius: 8px; border: 1px solid var(--border);">
              <div style="font-size: 13px; font-weight: 700; color: #60a5fa;">4. Payout Speed Index</div>
              <div style="font-size: 12px; color: var(--text-muted); margin-top: 2px;">Average response time: <strong>45 seconds</strong></div>
            </div>

            <div style="background: #020617; padding: 10px; border-radius: 8px; border: 1px solid var(--border);">
              <div style="font-size: 13px; font-weight: 700; color: #60a5fa;">5. Active Dispute Log</div>
              <div style="font-size: 12px; color: var(--text-muted); margin-top: 2px;">Pending player tickets: <strong>0</strong></div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Attach Bank Modal -->
    <div class="modal-backdrop" id="bankModal">
      <div class="modal">
        <div class="modal-header">
          <span class="modal-title" id="bankModalTitle">Attach Bank</span>
          <button class="icon-btn" id="closeBankModal"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div class="modal-body">
          <form id="bankForm">
            <input type="hidden" id="editIndex" value="-1">
            <div class="form-group">
              <label class="form-label">Payment Method</label>
              <select class="form-control" id="modalMethod">
                <option value="telebirr">telebirr</option>
                <option value="Commercial Bank of Ethiopia">Commercial Bank of Ethiopia</option>
                <option value="Bank of Abyssinia">Bank of Abyssinia</option>
              </select>
            </div>
            <div class="form-group">
              <label class="form-label">Account Number</label>
              <input type="text" class="form-control" id="modalAccNum" placeholder="Account number" required>
            </div>
            <div class="form-group">
              <label class="form-label">Account Name</label>
              <input type="text" class="form-control" id="modalAccName" placeholder="Account name" required>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button class="btn btn-secondary btn-sm" id="cancelBankModal">Cancel</button>
          <button class="btn btn-primary btn-sm" id="saveBankBtn">Save Account</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    // Authentication Logic (Switching views)
    const authOverlay = document.getElementById('authOverlay');
    const appWrapper = document.getElementById('appWrapper');
    const loginBox = document.getElementById('loginBox');
    const registerBox = document.getElementById('registerBox');

    document.getElementById('showRegister').addEventListener('click', () => {
      loginBox.style.display = 'none';
      registerBox.style.display = 'block';
    });

    document.getElementById('showLogin').addEventListener('click', () => {
      registerBox.style.display = 'none';
      loginBox.style.display = 'block';
    });

    document.getElementById('loginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      authOverlay.style.display = 'none';
      appWrapper.style.display = 'block';
    });

    document.getElementById('registerForm').addEventListener('submit', (e) => {
      e.preventDefault();
      alert('Registration successful! Logging in...');
      authOverlay.style.display = 'none';
      appWrapper.style.display = 'block';
    });

    document.getElementById('logoutBtn').addEventListener('click', () => {
      appWrapper.style.display = 'none';
      authOverlay.style.display = 'flex';
      closeDrawer();
    });

    // Navigation Drawer Toggle
    const menuToggle = document.getElementById('menuToggle');
    const drawer = document.getElementById('drawer');
    const drawerOverlay = document.getElementById('drawerOverlay');
    const drawerClose = document.getElementById('drawerClose');

    menuToggle.addEventListener('click', () => { drawer.classList.add('active'); drawerOverlay.classList.add('active'); });
    const closeDrawer = () => { drawer.classList.remove('active'); drawerOverlay.classList.remove('active'); };
    drawerClose.addEventListener('click', closeDrawer);
    drawerOverlay.addEventListener('click', closeDrawer);

    // Tab Logic
    const drawerItems = document.querySelectorAll('.drawer-item[data-target]');
    const tabContents = document.querySelectorAll('.tab-content');

    drawerItems.forEach(item => {
      item.addEventListener('click', () => {
        const target = item.getAttribute('data-target');
        drawerItems.forEach(i => i.classList.remove('active'));
        item.classList.add('active');
        tabContents.forEach(tab => tab.id === target ? tab.classList.add('active') : tab.classList.remove('active'));
        closeDrawer();
      });
    });

    // Accounts Logic
    let bankAccounts = [];
    const bankTableBody = document.getElementById('bankTableBody');
    const bankModal = document.getElementById('bankModal');

    function renderBankTable() {
      bankTableBody.innerHTML = '';
      if (bankAccounts.length === 0) {
        bankTableBody.innerHTML = `<tr><td colspan="5" style="text-align:center; color: var(--text-muted); padding: 16px;">No bank accounts added yet.</td></tr>`;
        return;
      }
      bankAccounts.forEach((acc, idx) => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td><strong>${acc.method}</strong></td>
          <td>${acc.accNum}</td>
          <td>${acc.accName}</td>
          <td><span class="badge-status badge-active">Active</span></td>
          <td style="display:flex; gap:6px;">
            <button class="btn btn-secondary btn-sm" onclick="deleteAccount(${idx})"><i class="fa-solid fa-trash"></i></button>
          </td>
        `;
        bankTableBody.appendChild(tr);
      });
    }

    document.getElementById('openAttachBankModal').addEventListener('click', () => bankModal.classList.add('active'));
    document.getElementById('closeBankModal').addEventListener('click', () => bankModal.classList.remove('active'));
    document.getElementById('cancelBankModal').addEventListener('click', () => bankModal.classList.remove('active'));

    document.getElementById('saveBankBtn').addEventListener('click', (e) => {
      e.preventDefault();
      const method = document.getElementById('modalMethod').value;
      const accNum = document.getElementById('modalAccNum').value;
      const accName = document.getElementById('modalAccName').value;
      if (!accNum || !accName) return;
      bankAccounts.push({ method, accNum, accName });
      renderBankTable();
      bankModal.classList.remove('active');
    });

    window.deleteAccount = function(idx) {
      bankAccounts.splice(idx, 1);
      renderBankTable();
    };

    renderBankTable();
  </script>
</body>
</html>
