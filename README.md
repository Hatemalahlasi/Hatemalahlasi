<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>معمل أبو محمد | نظام المحاسبة والمبيعات</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

    <!-- مكتبات Firebase السحابية -->
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
    <!-- مكتبة تصدير PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

    <style>
        :root {
            --bg-page: #eef2f6;
            --bg-surface: #f8fafc;
            --bg-card: #ffffff;
            --primary: #0f4c81;
            --primary-hover: #0a355c;
            --primary-soft: #e8f1f8;
            --accent: #0d9488;
            --border: #dbe3ec;
            --text-main: #111827;
            --text-muted: #6b7280;
            --success: #15803d;
            --success-bg: #dcfce7;
            --warning: #b45309;
            --warning-bg: #fef3c7;
            --danger: #b91c1c;
            --danger-bg: #fee2e2;
            --purple: #5b21b6;
            --purple-bg: #ede9fe;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: 'Cairo', sans-serif;
            background: linear-gradient(160deg, #e6ecf5 0%, #f4f7fb 100%);
            color: var(--text-main);
            min-height: 100vh;
            padding: 10px;
        }

        .app-shell {
            max-width: 1140px;
            margin: 0 auto;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 22px;
            padding: 14px 16px 20px;
            box-shadow: 0 20px 45px -15px rgba(15, 76, 129, 0.12);
            min-height: calc(100vh - 20px);
        }

        @media (min-width: 768px) {
            .app-shell { padding: 24px 30px; }
        }

        /* لون صفحة الدخول: أخضر وأحمر */
        .login-wrapper {
            max-width: 400px;
            margin: 36px auto;
            background: linear-gradient(180deg, #dcfce7 0%, #ffffff 50%, #fee2e2 100%);
            border: 2px solid #15803d;
            border-radius: 22px;
            padding: 26px 20px;
        }

        .login-wrapper h1 {
            text-align: center;
            font-size: 22px;
            font-weight: 800;
            color: #15803d;
            margin-bottom: 4px;
        }

        .login-wrapper p {
            text-align: center;
            color: #b91c1c;
            font-weight: 700;
            font-size: 13px;
            margin-bottom: 20px;
        }

        .login-wrapper .form-control:focus {
            border-color: #15803d;
            box-shadow: 0 0 0 3px rgba(21, 128, 61, 0.16);
        }

        .login-btn-color {
            background: linear-gradient(90deg, #15803d 0%, #b91c1c 100%);
            color: #fff;
        }

        .brand-logo {
            width: 84px;
            height: 84px;
            border-radius: 16px;
            background: #ffffff;
            border: 1.5px solid #b91c1c;
            color: #15803d;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            margin: 0 auto 14px;
            padding: 6px;
            overflow: hidden;
        }

        .brand-logo img {
            width: 100%;
            height: 100%;
            object-fit: contain;
            display: block;
        }

        .top-utility-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 8px;
            margin-bottom: 10px;
        }

        .header-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            padding-bottom: 14px;
            border-bottom: 1.5px solid var(--border);
            margin-bottom: 14px;
        }

        .header-brand {
            display: flex;
            align-items: center;
            gap: 12px;
            min-width: 0;
            flex: 1;
        }

        .header-logo-square {
            width: 48px;
            height: 48px;
            border-radius: 12px;
            background: #ffffff;
            border: 1.5px solid var(--border);
            color: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            padding: 4px;
            overflow: hidden;
            flex-shrink: 0;
            box-shadow: 0 2px 8px rgba(15, 76, 129, 0.08);
        }

        .header-logo-square img {
            width: 100%;
            height: 100%;
            object-fit: contain;
            display: block;
        }

        .form-group { margin-bottom: 12px; }
        .form-group label {
            display: block;
            font-size: 13px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .form-control {
            width: 100%;
            padding: 11px 13px;
            border: 1.5px solid var(--border);
            border-radius: 12px;
            background: #ffffff;
            font-family: 'Cairo', sans-serif;
            font-size: 14px;
            color: var(--text-main);
        }

        .form-control:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(15, 76, 129, 0.12);
        }

        .num-input {
            font-family: 'JetBrains Mono', 'Cairo', sans-serif;
            font-weight: 700;
        }

        .statement-builder {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 8px;
            background: #ffffff;
            border: 1.5px solid var(--border);
            border-radius: 12px;
            padding: 9px 12px;
        }

        .statement-prefix {
            font-size: 13.5px;
            font-weight: 700;
            color: var(--text-main);
        }

        .statement-num-box {
            width: 130px;
            padding: 8px 10px;
        }

        .statement-preview {
            margin-top: 6px;
            font-size: 12px;
            color: var(--text-muted);
            font-weight: 700;
        }

        .perm-box {
            display: flex;
            flex-wrap: wrap;
            gap: 14px;
            background: #fff;
            border: 1.5px solid var(--border);
            border-radius: 12px;
            padding: 10px 14px;
            margin-top: 10px;
        }

        .perm-check {
            display: inline-flex;
            align-items: center;
            gap: 7px;
            font-size: 13px;
            font-weight: 700;
            cursor: pointer;
        }

        .perm-check input {
            width: 17px;
            height: 17px;
            accent-color: var(--primary);
        }

        .btn {
            padding: 11px 15px;
            border-radius: 12px;
            border: none;
            font-family: 'Cairo', sans-serif;
            font-weight: 700;
            font-size: 14px;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.18s ease;
        }

        .btn:disabled { opacity: 0.65; cursor: not-allowed; }
        .btn-full { width: 100%; padding: 13px; font-size: 15px; }
        .btn-primary { background: var(--primary); color: #fff; }
        .btn-primary:hover { background: var(--primary-hover); }
        .btn-accent { background: var(--accent); color: #fff; }
        .btn-success { background: var(--success-bg); color: var(--success); }
        .btn-warning { background: var(--warning-bg); color: var(--warning); }
        .btn-danger { background: var(--danger-bg); color: var(--danger); }
        .btn-outline { background: #fff; color: var(--text-main); border: 1.5px solid var(--border); }
        .btn-sm { padding: 7px 11px; font-size: 12px; border-radius: 9px; }

        .db-status {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 11.5px;
            font-weight: 700;
            padding: 3px 10px;
            border-radius: 999px;
            background: var(--success-bg);
            color: var(--success);
        }

        .db-status.demo {
            background: var(--warning-bg);
            color: var(--warning);
        }

        .quick-nav {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-bottom: 16px;
        }

        @media (min-width: 768px) {
            .quick-nav {
                grid-template-columns: repeat(4, 1fr);
                gap: 12px;
            }
        }

        .nav-tab {
            padding: 15px 10px;
            border-radius: 16px;
            border: 1.5px solid var(--border);
            background: var(--bg-surface);
            color: var(--text-main);
            font-family: 'Cairo', sans-serif;
            font-weight: 800;
            font-size: 14px;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.18s ease;
        }

        .nav-tab i { font-size: 21px; color: var(--primary); }
        .nav-tab.accent-tab i { color: var(--accent); }
        .nav-tab.profit-tab i { color: var(--success); }
        .nav-tab.supplier-tab i { color: var(--warning); }
        .nav-tab.expense-tab i { color: var(--danger); }
        .nav-tab:hover {
            border-color: var(--primary);
            background: var(--primary-soft);
        }

        .fullpage-topbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            background: var(--primary-soft);
            border: 1.5px solid #c7dcef;
            border-radius: 15px;
            padding: 10px 14px;
            margin-bottom: 14px;
        }

        .fullpage-title {
            font-size: 16.5px;
            font-weight: 800;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .summary-strip {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 14px;
        }

        @media (min-width: 768px) {
            .summary-strip { grid-template-columns: repeat(4, 1fr); }
        }

        .mini-stat {
            background: var(--bg-surface);
            border: 1.5px solid var(--border);
            border-radius: 14px;
            padding: 12px;
        }

        .mini-stat-label { font-size: 12px; color: var(--text-muted); font-weight: 700; }
        .mini-stat-val { font-size: 17px; font-weight: 800; margin-top: 3px; color: var(--primary); }

        .card-box {
            background: var(--bg-surface);
            border: 1.5px solid var(--border);
            border-radius: 16px;
            padding: 15px;
            margin-bottom: 14px;
        }

        .card-title {
            font-size: 14.5px;
            font-weight: 800;
            color: var(--primary);
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 8px;
            flex-wrap: wrap;
        }

        .grid-2, .grid-3, .grid-4 { display: grid; grid-template-columns: 1fr; gap: 12px; }
        @media (min-width: 700px) {
            .grid-2 { grid-template-columns: 1fr 1fr; }
            .grid-3 { grid-template-columns: 1fr 1fr 1fr; }
            .grid-4 { grid-template-columns: repeat(4, 1fr); }
        }

        .branches-chips {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 12px;
        }

        .branch-chip {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: #ffffff;
            border: 1.5px solid var(--border);
            border-radius: 11px;
            padding: 7px 11px;
            font-size: 13px;
            font-weight: 700;
        }

        .table-responsive {
            width: 100%;
            overflow-x: auto;
            background: #fff;
            border-radius: 12px;
            border: 1.5px solid var(--border);
        }

        table { width: 100%; border-collapse: collapse; font-size: 13px; }
        th, td { padding: 10px 12px; text-align: right; border-bottom: 1px solid #eef2f6; }
        th { background: #f8fafc; color: var(--text-muted); font-weight: 800; white-space: nowrap; }

        .badge {
            display: inline-flex;
            align-items: center;
            padding: 3px 9px;
            border-radius: 999px;
            font-size: 11px;
            font-weight: 700;
        }
        .badge-cash { background: var(--success-bg); color: var(--success); }
        .badge-credit { background: var(--warning-bg); color: var(--warning); }
        .badge-expense { background: var(--danger-bg); color: var(--danger); }
        .badge-role { background: var(--purple-bg); color: var(--purple); }
        .badge-sup { background: #e0f2fe; color: #0369a1; }
        .badge-unit { background: #f1f5f9; color: #334155; }

        .mono {
            font-family: 'JetBrains Mono', monospace;
            font-weight: 700;
            direction: ltr;
            display: inline-block;
        }

        .stock-picker-box {
            background: #fff;
            border: 1.5px solid var(--border);
            border-radius: 14px;
            padding: 12px;
            margin-bottom: 12px;
        }

        .invoice-item-row {
            display: grid;
            grid-template-columns: 2fr 1fr 0.9fr 1fr auto;
            gap: 8px;
            align-items: center;
            margin-bottom: 8px;
        }

        @media (max-width: 680px) {
            .invoice-item-row {
                grid-template-columns: 1fr 1fr;
                background: #fff;
                padding: 10px;
                border-radius: 12px;
                border: 1px solid var(--border);
            }
            .invoice-item-row .item-name {
                grid-column: span 2;
            }
        }

        .summary-bar {
            background: #fff;
            border: 1.5px solid var(--primary);
            border-radius: 12px;
            padding: 12px 14px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 12px;
        }

        .statement-summary-box {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-bottom: 12px;
        }

        @media (max-width: 600px) {
            .statement-summary-box { grid-template-columns: 1fr; }
        }

        .statement-kpi {
            background: #fff;
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 9px 11px;
        }

        .statement-kpi span {
            display: block;
            font-size: 11.5px;
            color: var(--text-muted);
            font-weight: 700;
        }

        .statement-kpi strong {
            font-size: 15px;
            font-weight: 800;
        }

        .pdf-export-sheet {
            background: #ffffff;
            padding: 18px;
            border-radius: 12px;
            border: 1px solid var(--border);
        }

        .modal-backdrop {
            position: fixed;
            inset: 0;
            background: rgba(15, 23, 42, 0.55);
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 14px;
            z-index: 1200;
        }

        .modal-card {
            background: #fff;
            border-radius: 18px;
            max-width: 580px;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            padding: 20px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
        }

        .print-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            border-bottom: 2px solid var(--primary);
            padding-bottom: 12px;
            margin-bottom: 14px;
        }

        .toast {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -40%);
            background: var(--primary);
            color: #fff;
            padding: 9px 16px;
            border-radius: 11px;
            font-size: 13px;
            font-weight: 700;
            text-align: center;
            width: fit-content;
            max-width: 88vw;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            box-shadow: 0 12px 28px rgba(15, 23, 42, 0.25);
            opacity: 0;
            pointer-events: none;
            transition: all 0.18s ease;
            z-index: 1300;
        }

        .toast.show {
            opacity: 1;
            transform: translate(-50%, -50%);
        }

        .hidden { display: none !important; }

        @media print {
            body {
                background: #fff !important;
                padding: 0 !important;
            }
            .app-shell, .toast, #loginView, #mainAppView {
                display: none !important;
            }
            #printInvoiceModal, #customerStatementModal {
                display: block !important;
                position: static !important;
                background: transparent !important;
                padding: 0 !important;
            }
            .modal-card {
                box-shadow: none !important;
                max-height: none !important;
                max-width: 100% !important;
                padding: 10px !important;
            }
            .no-print {
                display: none !important;
            }
        }
    </style>
</head>
<body>

<div class="app-shell">

    <!-- شاشة الدخول -->
    <div id="loginView" class="login-wrapper">
        <div class="brand-logo">
            <img src="logo.png" alt="شعار معمل أبو محمد" onerror="this.style.display='none'; this.nextElementSibling.style.display='inline-flex';">
            <i class="fa-solid fa-industry" style="display:none;"></i>
        </div>
        <h1>معمل أبو محمد</h1>
        <p>نظام محاسبة ومبيعات متكامل</p>

        <div class="form-group">
            <label>اسم المستخدم</label>
            <input type="text" id="loginUser" class="form-control num-input" inputmode="numeric" autocomplete="off" onkeydown="if(event.key==='Enter') handleLogin()">
        </div>
        <div class="form-group">
            <label>كلمة المرور</label>
            <input type="password" id="loginPass" class="form-control num-input" inputmode="numeric" autocomplete="new-password" onkeydown="if(event.key==='Enter') handleLogin()">
        </div>

        <button id="loginSubmitBtn" class="btn login-btn-color btn-full" onclick="handleLogin()">
            <i class="fa-solid fa-right-to-bracket"></i> <span id="loginBtnText">دخول</span>
        </button>
    </div>

    <!-- واجهة النظام -->
    <div id="mainAppView" class="hidden">

        <div class="top-utility-row">
            <div style="display:flex; align-items:center; gap:6px; flex-wrap:wrap;">
                <span id="connectionStatusBadge" class="db-status"><i class="fa-solid fa-bolt"></i> متصل مباشر</span>
                <span id="currentUserRoleBadge" class="badge badge-role">مدير</span>
            </div>
            <button type="button" class="btn btn-danger btn-sm" onclick="confirmLogout()">
                <i class="fa-solid fa-right-from-bracket"></i> خروج
            </button>
        </div>

        <div class="header-bar">
            <div class="header-brand">
                <div class="header-logo-square">
                    <img src="logo.png" alt="شعار معمل أبو محمد" onerror="this.style.display='none'; this.nextElementSibling.style.display='inline-flex';">
                    <i class="fa-solid fa-industry" style="display:none;"></i>
                </div>
                <div style="min-width:0;">
                    <h2 id="headerWelcome" style="font-size:16.5px; font-weight:800; line-height:1.35;">معمل أبو محمد</h2>
                </div>
            </div>

            <button id="refreshDataBtn" type="button" class="btn btn-outline btn-sm" onclick="reloadAllData(true)">
                <i class="fa-solid fa-rotate"></i> تحديث
            </button>
        </div>

        <!-- القائمة الرئيسية -->
        <div id="homeMenuContainer">
            <div id="summaryStatsStrip" class="summary-strip">
                <div class="mini-stat">
                    <div class="mini-stat-label">المبيعات</div>
                    <div class="mini-stat-val mono" id="kpiTotalSales">0.00</div>
                </div>
                <div class="mini-stat">
                    <div class="mini-stat-label">رصيد الصندوق</div>
                    <div class="mini-stat-val mono" id="kpiTotalCash" style="color:var(--success);">0.00</div>
                </div>
                <div class="mini-stat">
                    <div class="mini-stat-label">ديون العملاء</div>
                    <div class="mini-stat-val mono" id="kpiTotalReceivables" style="color:var(--warning);">0.00</div>
                </div>
                <div class="mini-stat">
                    <div class="mini-stat-label">المخزون (إجمالي الوحدات)</div>
                    <div class="mini-stat-val mono" id="kpiWarehouseStock" style="color:var(--accent);">0</div>
                </div>
            </div>

            <div class="quick-nav">
                <button class="nav-tab" onclick="openFullPage('salesTab')">
                    <i class="fa-solid fa-file-invoice-dollar"></i>
                    <span>المبيعات والفواتير</span>
                </button>
                <button class="nav-tab supplier-tab" onclick="openFullPage('purchasesTab')">
                    <i class="fa-solid fa-truck-field"></i>
                    <span>المشتروات وحساب الموردين</span>
                </button>
                <button class="nav-tab expense-tab" onclick="openFullPage('expensesTab')">
                    <i class="fa-solid fa-money-bill-trend-down"></i>
                    <span>المصروفات</span>
                </button>
                <button class="nav-tab" onclick="openFullPage('vouchersTab')">
                    <i class="fa-solid fa-file-signature"></i>
                    <span>الأسناد</span>
                </button>
                <button class="nav-tab" onclick="openFullPage('cashboxTab')">
                    <i class="fa-solid fa-vault"></i>
                    <span>الصندوق</span>
                </button>
                <button class="nav-tab" onclick="openFullPage('warehouseTab')">
                    <i class="fa-solid fa-boxes-stacked"></i>
                    <span>المخازن والفروع</span>
                </button>
                <button class="nav-tab" onclick="openFullPage('customersTab')">
                    <i class="fa-solid fa-users"></i>
                    <span>العملاء</span>
                </button>
                <button class="nav-tab accent-tab" onclick="openAddItemModal()">
                    <i class="fa-solid fa-box-open"></i>
                    <span>إضافة أصناف</span>
                </button>
                <button class="nav-tab accent-tab" onclick="openTransferModal()">
                    <i class="fa-solid fa-right-left"></i>
                    <span>نقل مخازن</span>
                </button>
                <button class="nav-tab profit-tab" onclick="openFullPage('profitsTab')">
                    <i class="fa-solid fa-chart-line"></i>
                    <span>الأرباح</span>
                </button>
                <button id="employeesNavBtn" class="nav-tab" onclick="openFullPage('employeesTab')">
                    <i class="fa-solid fa-user-tie"></i>
                    <span>الموظفون</span>
                </button>
            </div>
        </div>

        <!-- 1. صفحة المبيعات والفواتير الكاملة -->
        <section id="salesTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title"><i class="fa-solid fa-file-invoice-dollar"></i> الفواتير والمبيعات</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span>إصدار فاتورة مبيعات</span></div>

                <div class="grid-4">
                    <div class="form-group">
                        <label>الفرع</label>
                        <select id="invBranchSelect" class="form-control" onchange="renderWarehouseCatalogDropdown()"></select>
                    </div>
                    <div class="form-group">
                        <label>نوع الفاتورة</label>
                        <select id="invPaymentType" class="form-control" onchange="toggleInvoicePaymentFields()">
                            <option value="cash">نقدي (على الصندوق)</option>
                            <option value="credit">آجل (على العميل)</option>
                        </select>
                    </div>
                    <div class="form-group" id="invCashboxGroup">
                        <label>الصندوق</label>
                        <select id="invCashboxSelect" class="form-control"></select>
                    </div>
                    <div class="form-group">
                        <label>العميل</label>
                        <select id="invCustomerSelect" class="form-control"></select>
                    </div>
                </div>

                <!-- بحث واختيار الأصناف من المخازن -->
                <div class="stock-picker-box">
                    <div style="font-size:13px; font-weight:800; color:var(--primary); margin-bottom:8px;">
                        <i class="fa-solid fa-magnifying-glass"></i> بحث واختيار صنف من المخازن
                    </div>
                    <div class="grid-2" style="margin-bottom:0;">
                        <div class="form-group" style="margin-bottom:0;">
                            <div style="display:flex; gap:6px;">
                                <input type="text" id="warehouseItemSearch" class="form-control" placeholder="اكتب اسم الصنف للبحث..." oninput="renderWarehouseCatalogDropdown()">
                                <button type="button" class="btn btn-outline btn-sm" onclick="document.getElementById('warehouseItemSearch').value=''; renderWarehouseCatalogDropdown();" title="مسح البحث">
                                    <i class="fa-solid fa-xmark"></i>
                                </button>
                            </div>
                        </div>
                        <div class="form-group" style="margin-bottom:0;">
                            <div style="display:flex; gap:6px;">
                                <select id="warehouseCatalogSelect" class="form-control"></select>
                                <button type="button" class="btn btn-accent btn-sm" onclick="addSelectedWarehouseItemToInvoice()">
                                    <i class="fa-solid fa-plus"></i> إضافة
                                </button>
                            </div>
                        </div>
                    </div>
                </div>

                <div style="margin: 8px 0; display:flex; justify-content:space-between; align-items:center;">
                    <strong style="font-size:13px;">أصناف الفاتورة (حبة / شدة):</strong>
                    <button type="button" class="btn btn-outline btn-sm" onclick="addInvoiceItemRow()">
                        <i class="fa-solid fa-plus"></i> سطر صنف يدوي
                    </button>
                </div>

                <div id="invoiceItemsContainer"></div>

                <div class="grid-2">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الخصم</label>
                        <input type="number" id="invDiscount" class="form-control num-input" value="0" min="0" oninput="recalculateInvoiceTotal()">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>البيان لكشف الحساب (رقم الفاتورة)</label>
                        <div class="statement-builder">
                            <span class="statement-prefix">عليكم فاتورة مبيعات برقم</span>
                            <input type="text" id="invRefNumber" class="form-control num-input statement-num-box" inputmode="numeric" placeholder="رقم الفاتورة" oninput="updateInvoiceStatementPreview()">
                        </div>
                        <div id="invStatementPreview" class="statement-preview">النص في الكشف: عليكم فاتورة مبيعات برقم —</div>
                    </div>
                </div>

                <div class="summary-bar">
                    <div>
                        <span style="font-size:12px; color:var(--text-muted); font-weight:700;">الإجمالي الصافي:</span>
                        <div class="mono" id="invNetTotalDisplay" style="font-size:20px; color:var(--primary);">0.00</div>
                    </div>
                    <button id="saveInvoiceBtn" class="btn btn-primary" onclick="saveSalesInvoice()">
                        <i class="fa-solid fa-print"></i> حفظ وطباعة الفاتورة
                    </button>
                </div>
            </div>

            <div class="card-box">
                <div class="card-title">
                    <span><i class="fa-solid fa-receipt"></i> سجل الفواتير</span>
                    <input type="text" id="invoiceSearchInput" class="form-control" style="max-width:220px; padding:7px 10px;" placeholder="بحث برقم أو عميل..." oninput="renderInvoicesTable()">
                </div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>الرقم</th>
                                <th>الفرع</th>
                                <th>العميل</th>
                                <th>الأصناف</th>
                                <th>البيان</th>
                                <th>النوع</th>
                                <th>الصافي</th>
                                <th>الموظف</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="invoicesTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- قسم المشتروات وحساب الموردين (نقدي أو دين على المورد) -->
        <section id="purchasesTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title" style="color:var(--warning);"><i class="fa-solid fa-truck-field"></i> المشتروات وحساب الموردين</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span>إضافة مورد جديد</span></div>
                <div class="grid-3">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>اسم المورد</label>
                        <input type="text" id="newSupplierName" class="form-control" placeholder="اسم المورد">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الهاتف</label>
                        <input type="text" id="newSupplierPhone" class="form-control num-input" inputmode="numeric" placeholder="77xxxxxxx">
                    </div>
                    <div style="display:flex; align-items:flex-end;">
                        <button id="saveSupplierBtn" class="btn btn-outline btn-full" onclick="createSupplier()">
                            <i class="fa-solid fa-user-plus"></i> حفظ المورد
                        </button>
                    </div>
                </div>
            </div>

            <div class="card-box">
                <div class="card-title" style="color:var(--warning);">
                    <span>تسجيل فاتورة مشتروات (نقدي أو دين على المورد)</span>
                    <span class="badge badge-credit">ديون الموردين: <span class="mono" id="suppliersDebtTotal" style="margin-right:4px;">0.00</span></span>
                </div>

                <div class="grid-4">
                    <div class="form-group">
                        <label>الفرع / المخزن</label>
                        <select id="purBranchSelect" class="form-control"></select>
                    </div>
                    <div class="form-group">
                        <label>المورد</label>
                        <select id="purSupplierSelect" class="form-control"></select>
                    </div>
                    <div class="form-group">
                        <label>طريقة الشراء</label>
                        <select id="purPaymentType" class="form-control" onchange="togglePurchaseCashboxField()">
                            <option value="credit">آجل (دين على المورد)</option>
                            <option value="cash">نقدي (من الصندوق)</option>
                        </select>
                    </div>
                    <div class="form-group" id="purCashboxGroup">
                        <label>الصندوق</label>
                        <select id="purCashboxSelect" class="form-control"></select>
                    </div>
                </div>

                <div class="grid-3">
                    <div class="form-group">
                        <label>الصنف / المادة المشتراة</label>
                        <input type="text" id="purTitle" class="form-control" placeholder="اسم المادة أو الصنف">
                    </div>
                    <div class="form-group">
                        <label>إضافة للمخزن (الكمية / الوحدة)</label>
                        <div style="display:grid; grid-template-columns:1fr 1fr; gap:6px;">
                            <input type="number" id="purAddQty" class="form-control num-input" value="1" min="0" placeholder="الكمية">
                            <select id="purUnit" class="form-control">
                                <option value="حبة">حبة</option>
                                <option value="شدة">شدة</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>المبلغ الإجمالي</label>
                        <input type="number" id="purAmount" class="form-control num-input" min="0" placeholder="0.00">
                    </div>
                </div>

                <div class="form-group">
                    <label>ملاحظة</label>
                    <input type="text" id="purNotes" class="form-control" placeholder="اختياري">
                </div>

                <button id="savePurchaseBtn" class="btn btn-primary btn-full" onclick="createPurchaseOrder()">
                    <i class="fa-solid fa-check"></i> حفظ المشتروات
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-address-book"></i> حسابات الموردين (الأرصدة المستحقة لهم)</span></div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>المورد</th>
                                <th>الهاتف</th>
                                <th>الرصيد المستحق (دين)</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="suppliersTableBody"></tbody>
                    </table>
                </div>
            </div>

            <div class="card-box">
                <div class="card-title">
                    <span><i class="fa-solid fa-list-check"></i> سجل المشتروات</span>
                    <input type="text" id="purchaseSearchInput" class="form-control" style="max-width:220px; padding:7px 10px;" placeholder="بحث بمورد أو صنف..." oninput="renderPurchasesTable()">
                </div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>التاريخ</th>
                                <th>الفرع</th>
                                <th>المورد</th>
                                <th>الصنف</th>
                                <th>الكمية</th>
                                <th>النوع</th>
                                <th>المبلغ</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="purchasesTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- قسم المصروفات المستقل -->
        <section id="expensesTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title" style="color:var(--danger);"><i class="fa-solid fa-money-bill-trend-down"></i> المصروفات</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title" style="color:var(--danger);">
                    <span>تسجيل مصروف</span>
                    <span class="badge badge-expense">إجمالي المصروفات: <span class="mono" id="expensesTabTotal" style="margin-right:4px;">0.00</span></span>
                </div>

                <div class="grid-3">
                    <div class="form-group">
                        <label>الصندوق</label>
                        <select id="expCashboxSelect" class="form-control"></select>
                    </div>
                    <div class="form-group">
                        <label>نوع / بيان المصروف</label>
                        <input type="text" id="expTitle" class="form-control" placeholder="مثال: كهرباء / صيانة / إيجار">
                    </div>
                    <div class="form-group">
                        <label>المبلغ</label>
                        <input type="number" id="expAmount" class="form-control num-input" min="0" placeholder="0.00">
                    </div>
                </div>

                <div class="form-group">
                    <label>ملاحظة</label>
                    <input type="text" id="expNotes" class="form-control" placeholder="تفاصيل المصروف...">
                </div>

                <button id="saveExpenseBtn" class="btn btn-danger btn-full" onclick="createExpenseRecord()">
                    <i class="fa-solid fa-check"></i> حفظ المصروف
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-receipt"></i> سجل المصروفات</span></div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>التاريخ</th>
                                <th>الصندوق</th>
                                <th>البيان</th>
                                <th>المبلغ</th>
                                <th>الموظف</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="expensesTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 2. صفحة الأسناد الكاملة -->
        <section id="vouchersTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title"><i class="fa-solid fa-file-signature"></i> الأسناد</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span>إصدار سند قبض / صرف</span></div>
                <div class="grid-2">
                    <div class="form-group">
                        <label>نوع السند</label>
                        <select id="voucherType" class="form-control" onchange="toggleVoucherPartyFields()">
                            <option value="receipt">سند قبض</option>
                            <option value="payment">سند صرف</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>الصندوق</label>
                        <select id="voucherCashboxSelect" class="form-control"></select>
                    </div>
                </div>
                <div class="grid-2">
                    <div class="form-group" id="voucherCustomerGroup">
                        <label>العميل (اختياري)</label>
                        <select id="voucherCustomerSelect" class="form-control"></select>
                    </div>
                    <div class="form-group hidden" id="voucherSupplierGroup">
                        <label>المورد (لسند الصرف / التسديد)</label>
                        <select id="voucherSupplierSelect" class="form-control"></select>
                    </div>
                    <div class="form-group">
                        <label>المبلغ</label>
                        <input type="number" id="voucherAmount" class="form-control num-input" min="0" placeholder="0.00">
                    </div>
                </div>
                <div class="form-group">
                    <label>البيان لكشف الحساب (رقم السند)</label>
                    <div class="statement-builder">
                        <span id="voucherStatementPrefix" class="statement-prefix">لكم سند قبض برقم</span>
                        <input type="text" id="voucherRefNumber" class="form-control num-input statement-num-box" inputmode="numeric" placeholder="رقم السند" oninput="updateVoucherStatementPreview()">
                    </div>
                    <div id="voucherStatementPreview" class="statement-preview">النص في الكشف: لكم سند قبض برقم —</div>
                </div>
                <button id="saveVoucherBtn" class="btn btn-primary btn-full" onclick="createVoucher()">
                    <i class="fa-solid fa-check"></i> حفظ السند
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-list"></i> سجل الأسناد</span></div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>النوع</th>
                                <th>الصندوق</th>
                                <th>الجهة</th>
                                <th>البيان</th>
                                <th>المبلغ</th>
                                <th>الموظف</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="vouchersTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 3. صفحة الصندوق الكاملة -->
        <section id="cashboxTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title"><i class="fa-solid fa-vault"></i> الصندوق</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span>الصناديق والأرصدة النظامية</span></div>
                <div id="dashboardCashboxesList" style="margin-bottom:14px;"></div>
                <div class="grid-2">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>اسم الصندوق الجديد</label>
                        <input type="text" id="newCashboxName" class="form-control" placeholder="مثال: صندوق المعمل">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الرصيد الافتتاحي</label>
                        <input type="number" id="newCashboxOpening" class="form-control num-input" value="0" min="0">
                    </div>
                </div>
                <button id="saveCashboxBtn" class="btn btn-primary btn-full" onclick="createCashbox()" style="margin-top:12px;">
                    <i class="fa-solid fa-plus"></i> إضافة صندوق
                </button>
            </div>
        </section>

        <!-- 4. صفحة المخازن والفروع + النقل بين المخازن -->
        <section id="warehouseTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title"><i class="fa-solid fa-boxes-stacked"></i> المخازن والفروع</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title">
                    <span><i class="fa-solid fa-code-branch"></i> الفروع وإضافة فرع</span>
                    <span id="warehouseTotalValueBadge" class="badge badge-cash">قيمة المخزون: 0.00</span>
                </div>
                <div class="grid-2">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>عرض مخزون فرع</label>
                        <select id="activeBranchFilter" class="form-control" onchange="renderWarehouseTable()"></select>
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>اسم فرع جديد</label>
                        <div style="display:flex; gap:8px;">
                            <input type="text" id="newBranchName" class="form-control" placeholder="مثال: فرع إب">
                            <button id="saveBranchBtn" class="btn btn-outline" onclick="createBranch()">
                                <i class="fa-solid fa-plus"></i> إضافة
                            </button>
                        </div>
                    </div>
                </div>
                <div id="branchesChipsList" class="branches-chips"></div>
            </div>

            <div class="card-box" style="border-color: var(--accent);">
                <div class="card-title" style="color: var(--accent);">
                    <span><i class="fa-solid fa-right-left"></i> نقل من مخزن إلى مخزن</span>
                </div>

                <div class="grid-2">
                    <div class="form-group">
                        <label>من مخزن / فرع</label>
                        <select id="transferFromBranch" class="form-control" onchange="populateTransferItems()"></select>
                    </div>
                    <div class="form-group">
                        <label>إلى مخزن / فرع</label>
                        <select id="transferToBranch" class="form-control"></select>
                    </div>
                </div>

                <div class="grid-2">
                    <div class="form-group">
                        <label>الصنف المراد نقله</label>
                        <select id="transferItemSelect" class="form-control"></select>
                    </div>
                    <div class="form-group">
                        <label>الكمية للنقل</label>
                        <input type="number" id="transferQty" class="form-control num-input" value="1" min="1">
                    </div>
                </div>

                <button id="executeTransferBtn" class="btn btn-accent btn-full" onclick="transferWarehouseStock()">
                    <i class="fa-solid fa-dolly"></i> تنفيذ النقل بين المخازن
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-box-open"></i> إضافة / تحديث صنف في مخزن</span></div>
                <div class="grid-4">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الفرع</label>
                        <select id="whItemBranchSelect" class="form-control"></select>
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>اسم الصنف</label>
                        <input type="text" id="newItemName" class="form-control" placeholder="اسم المادة أو المنتج">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الوحدة</label>
                        <select id="newItemUnit" class="form-control">
                            <option value="حبة">حبة</option>
                            <option value="شدة">شدة</option>
                        </select>
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الكمية / السعر</label>
                        <div style="display:grid; grid-template-columns:1fr 1fr; gap:6px;">
                            <input type="number" id="newItemQty" class="form-control num-input" value="1" min="0" title="الكمية">
                            <input type="number" id="newItemPrice" class="form-control num-input" value="0" min="0" title="السعر">
                        </div>
                    </div>
                </div>
                <button id="saveWarehouseItemBtn" class="btn btn-primary btn-full" onclick="saveWarehouseItem()" style="margin-top:12px;">
                    <i class="fa-solid fa-box"></i> حفظ في المخزن
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-warehouse"></i> جرد مخازن الفروع</span></div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>الفرع</th>
                                <th>الصنف</th>
                                <th>الوحدة</th>
                                <th>الكمية</th>
                                <th>السعر</th>
                                <th>الإجمالي</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="warehouseTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- 5. صفحة العملاء الكاملة -->
        <section id="customersTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title"><i class="fa-solid fa-users"></i> العملاء</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span>إضافة عميل</span></div>
                <div class="grid-3">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>اسم العميل</label>
                        <input type="text" id="newCustomerName" class="form-control" placeholder="اسم العميل">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الهاتف</label>
                        <input type="text" id="newCustomerPhone" class="form-control num-input" inputmode="numeric" placeholder="77xxxxxxx">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>حد الائتمان</label>
                        <input type="number" id="newCustomerLimit" class="form-control num-input" value="100000" min="0">
                    </div>
                </div>
                <button id="saveCustomerBtn" class="btn btn-primary btn-full" onclick="createCustomer()" style="margin-top:12px;">
                    <i class="fa-solid fa-check"></i> حفظ العميل
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-address-book"></i> قائمة العملاء وأرصدتهم النظامية</span></div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>الاسم</th>
                                <th>الهاتف</th>
                                <th>الرصيد المستحق</th>
                                <th>إجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="customersTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- صفحة الأرباح -->
        <section id="profitsTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title" style="color:var(--success);"><i class="fa-solid fa-chart-line"></i> الأرباح</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="summary-strip">
                <div class="mini-stat">
                    <div class="mini-stat-label">إجمالي المبيعات</div>
                    <div class="mini-stat-val mono" id="profTotalSales">0.00</div>
                </div>
                <div class="mini-stat">
                    <div class="mini-stat-label">إجمالي المشتروات</div>
                    <div class="mini-stat-val mono" id="profTotalPurchases" style="color:var(--warning);">0.00</div>
                </div>
                <div class="mini-stat">
                    <div class="mini-stat-label">إجمالي المصروفات</div>
                    <div class="mini-stat-val mono" id="profTotalExpenses" style="color:var(--danger);">0.00</div>
                </div>
                <div class="mini-stat">
                    <div class="mini-stat-label">صافي الربح التقديري</div>
                    <div class="mini-stat-val mono" id="profNetProfit" style="color:var(--success);">0.00</div>
                </div>
            </div>

            <div class="card-box">
                <div class="card-title"><span>ملخص الربحية حسب الفواتير والمصروفات والمشتروات</span></div>
                <p style="font-size:13px; color:var(--text-muted); line-height:1.7;">
                    يُحسب صافي الربح التقديري من إجمالي المبيعات مطروحاً منه إجمالي المشتروات والمصروفات المسجلة في النظام.
                </p>
            </div>
        </section>

        <!-- 6. صفحة الموظفون والصلاحيات الكاملة -->
        <section id="employeesTab" class="tab-content hidden">
            <div class="fullpage-topbar">
                <div class="fullpage-title"><i class="fa-solid fa-user-tie"></i> الموظفون والصلاحيات</div>
                <button type="button" class="btn btn-outline btn-sm" onclick="goBackHome()">
                    <i class="fa-solid fa-arrow-right"></i> رجوع
                </button>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-user-shield"></i> إضافة حساب جديد</span></div>
                <div class="grid-3">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الاسم</label>
                        <input type="text" id="newEmpFullName" class="form-control" placeholder="اسم الموظف أو المشرف">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>اسم الدخول</label>
                        <input type="text" id="newEmpUsername" class="form-control num-input" placeholder="مثال: 12007">
                    </div>
                    <div class="form-group" style="margin-bottom:0;">
                        <label>كلمة المرور</label>
                        <input type="text" id="newEmpPassword" class="form-control num-input" placeholder="كلمة المرور">
                    </div>
                </div>
                <div class="grid-2" style="margin-top:12px;">
                    <div class="form-group" style="margin-bottom:0;">
                        <label>الصلاحية</label>
                        <select id="newEmpRole" class="form-control" onchange="toggleEmployeePermBox()">
                            <option value="cashier">موظف (صلاحيات محددة)</option>
                            <option value="supervisor">مشرف عام (معه كل شيء + حذف المستخدمين)</option>
                            <option value="admin">مدير</option>
                        </select>
                    </div>
                    <div style="display:flex; align-items:flex-end;">
                        <button id="saveEmployeeBtn" class="btn btn-primary btn-full" onclick="createEmployee()">
                            <i class="fa-solid fa-user-check"></i> حفظ الحساب
                        </button>
                    </div>
                </div>

                <div id="empPermissionsBox" class="perm-box">
                    <label class="perm-check">
                        <input type="checkbox" id="newEmpCanEdit">
                        <span>سماح بالتعديل</span>
                    </label>
                    <label class="perm-check">
                        <input type="checkbox" id="newEmpCanDelete">
                        <span>سماح بالحذف</span>
                    </label>
                </div>
            </div>

            <div class="card-box">
                <div class="card-title"><span><i class="fa-solid fa-users-gear"></i> المستخدمون والصلاحيات</span></div>
                <div class="table-responsive">
                    <table>
                        <thead>
                            <tr>
                                <th>الاسم</th>
                                <th>الدخول</th>
                                <th>الصلاحية</th>
                                <th>تعديل / حذف</th>
                                <th>الحالة</th>
                                <th>تحكم</th>
                            </tr>
                        </thead>
                        <tbody id="employeesTableBody"></tbody>
                    </table>
                </div>
            </div>
        </section>

    </div>
</div>

<!-- نافذة إضافة أصناف سريعة من القائمة الرئيسية -->
<div id="quickAddItemModal" class="modal-backdrop hidden">
    <div class="modal-card">
        <div class="card-title">
            <span><i class="fa-solid fa-box-open"></i> إضافة / تحديث صنف في المخزن</span>
            <button type="button" class="btn btn-outline btn-sm" onclick="closeQuickAddItemModal()">إغلاق</button>
        </div>
        <div class="grid-2">
            <div class="form-group">
                <label>الفرع</label>
                <select id="modalWhBranchSelect" class="form-control"></select>
            </div>
            <div class="form-group">
                <label>اسم الصنف</label>
                <input type="text" id="modalItemName" class="form-control" placeholder="اسم المادة أو المنتج">
            </div>
        </div>
        <div class="grid-3">
            <div class="form-group">
                <label>الوحدة</label>
                <select id="modalItemUnit" class="form-control">
                    <option value="حبة">حبة</option>
                    <option value="شدة">شدة</option>
                </select>
            </div>
            <div class="form-group">
                <label>الكمية</label>
                <input type="number" id="modalItemQty" class="form-control num-input" value="1" min="0">
            </div>
            <div class="form-group">
                <label>السعر</label>
                <input type="number" id="modalItemPrice" class="form-control num-input" value="0" min="0">
            </div>
        </div>
        <button type="button" class="btn btn-primary btn-full" onclick="saveQuickWarehouseItem()">
            <i class="fa-solid fa-box"></i> حفظ الصنف
        </button>
    </div>
</div>

<!-- نافذة نقل مخازن سريعة من القائمة الرئيسية -->
<div id="quickTransferModal" class="modal-backdrop hidden">
    <div class="modal-card">
        <div class="card-title" style="color:var(--accent);">
            <span><i class="fa-solid fa-right-left"></i> نقل من مخزن إلى مخزن</span>
            <button type="button" class="btn btn-outline btn-sm" onclick="closeQuickTransferModal()">إغلاق</button>
        </div>
        <div class="grid-2">
            <div class="form-group">
                <label>من مخزن / فرع</label>
                <select id="modalTransferFromBranch" class="form-control" onchange="populateModalTransferItems()"></select>
            </div>
            <div class="form-group">
                <label>إلى مخزن / فرع</label>
                <select id="modalTransferToBranch" class="form-control"></select>
            </div>
        </div>
        <div class="grid-2">
            <div class="form-group">
                <label>الصنف المراد نقله</label>
                <select id="modalTransferItemSelect" class="form-control"></select>
            </div>
            <div class="form-group">
                <label>الكمية للنقل</label>
                <input type="number" id="modalTransferQty" class="form-control num-input" value="1" min="1">
            </div>
        </div>
        <button type="button" class="btn btn-accent btn-full" onclick="executeModalTransfer()">
            <i class="fa-solid fa-dolly"></i> تنفيذ النقل
        </button>
    </div>
</div>

<!-- نافذة كشف حساب العميل -->
<div id="customerStatementModal" class="modal-backdrop hidden">
    <div class="modal-card" style="max-width:720px;">
        <div id="customerStatementExportArea" class="pdf-export-sheet">
            <div class="print-header">
                <div>
                    <h2 style="font-size:18px; font-weight:800; color:var(--primary);">معمل أبو محمد</h2>
                    <p style="font-size:12px; color:var(--text-muted);">كشف حساب عميل تفصيلي</p>
                </div>
                <div style="text-align:left; font-size:12px;">
                    <div>العميل: <strong id="stCustName">-</strong></div>
                    <div>الهاتف: <span class="mono" id="stCustPhone">-</span></div>
                    <div>التاريخ: <span class="mono" id="stDate">-</span></div>
                </div>
            </div>

            <div class="statement-summary-box">
                <div class="statement-kpi">
                    <span>إجمالي المبيعات الآجلة</span>
                    <strong class="mono" id="stTotalInvoices" style="color:var(--primary);">0.00</strong>
                </div>
                <div class="statement-kpi">
                    <span>إجمالي السندات المقبوضة</span>
                    <strong class="mono" id="stTotalReceipts" style="color:var(--success);">0.00</strong>
                </div>
                <div class="statement-kpi">
                    <span>الرصيد المستحق</span>
                    <strong class="mono" id="stBalanceDue" style="color:var(--warning);">0.00</strong>
                </div>
            </div>

            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>التاريخ</th>
                            <th>البيان</th>
                            <th>مدين (عليه)</th>
                            <th>دائن (له)</th>
                            <th>الرصيد</th>
                        </tr>
                    </thead>
                    <tbody id="stTransactionsBody"></tbody>
                </table>
            </div>
        </div>

        <div class="no-print" style="display:flex; gap:8px; flex-wrap:wrap; margin-top:14px;">
            <button type="button" class="btn btn-primary" onclick="window.print()">
                <i class="fa-solid fa-print"></i> طباعة
            </button>
            <button type="button" class="btn btn-accent" onclick="downloadCustomerStatementPDF()">
                <i class="fa-solid fa-file-pdf"></i> تصدير PDF
            </button>
            <button type="button" class="btn btn-outline" onclick="closeCustomerStatementModal()">
                إغلاق
            </button>
        </div>
    </div>
</div>

<!-- نافذة طباعة الفاتورة النظامية -->
<div id="printInvoiceModal" class="modal-backdrop hidden">
    <div class="modal-card">
        <div class="print-header">
            <div>
                <h2 style="font-size:19px; font-weight:800; color:var(--primary);">معمل أبو محمد</h2>
                <p style="font-size:12px; color:var(--text-muted);">فاتورة مبيعات نظامية</p>
            </div>
            <div style="text-align:left; font-size:12px;">
                <div>رقم الفاتورة: <span class="mono" id="prInvId">-</span></div>
                <div>التاريخ: <span class="mono" id="prInvDate">-</span></div>
                <div>الفرع: <strong id="prInvBranch">-</strong></div>
            </div>
        </div>

        <div style="display:flex; justify-content:space-between; flex-wrap:wrap; gap:8px; font-size:13px; margin-bottom:12px; background:#f8fafc; padding:10px; border-radius:10px;">
            <div>العميل: <strong id="prInvCustomer">-</strong></div>
            <div>النوع: <strong id="prInvType">-</strong></div>
            <div>الموظف: <strong id="prInvEmp">-</strong></div>
        </div>

        <div class="table-responsive" style="margin-bottom:12px;">
            <table>
                <thead>
                    <tr>
                        <th>الصنف</th>
                        <th>الوحدة</th>
                        <th>الكمية</th>
                        <th>السعر</th>
                        <th>الإجمالي</th>
                    </tr>
                </thead>
                <tbody id="prInvItemsBody"></tbody>
            </table>
        </div>

        <div style="background:#f8fafc; padding:12px; border-radius:12px; font-size:13px;">
            <div style="display:flex; justify-content:space-between; margin-bottom:4px;">
                <span>الخصم:</span>
                <span class="mono" id="prInvDiscount">0.00</span>
            </div>
            <div style="display:flex; justify-content:space-between; font-size:16px; font-weight:800; color:var(--primary); border-top:1px solid var(--border); padding-top:6px;">
                <span>الصافي المطلوب:</span>
                <span class="mono" id="prInvNet">0.00</span>
            </div>
            <div id="prInvNotesRow" style="margin-top:8px; font-size:12px; color:var(--text-muted);"></div>
        </div>

        <div class="no-print" style="display:flex; gap:10px; margin-top:16px;">
            <button type="button" class="btn btn-primary btn-full" onclick="window.print()">
                <i class="fa-solid fa-print"></i> طباعة الفاتورة
            </button>
            <button type="button" class="btn btn-outline" onclick="closePrintModal()">
                إغلاق
            </button>
        </div>
    </div>
</div>

<div id="toast" class="toast"><span id="toastText">تم</span></div>

<script>
    const ADMIN_USER = "12006";
    const ADMIN_PASS = "5028611";

    const firebaseConfig = {
        apiKey: "AIzaSyDDm0KDSEHzwPJXAKPyhqQc3EtmN7zDVIY",
        authDomain: "abu-mohammad-accounting-223c8.firebaseapp.com",
        projectId: "abu-mohammad-accounting-223c8",
        storageBucket: "abu-mohammad-accounting-223c8.firebasestorage.app",
        messagingSenderId: "469928137766",
        appId: "1:469928137766:web:cd5526796ef3b4e0fb02e7",
        measurementId: "G-VX90LCEBKM"
    };

    firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();
    let isDemoMode = false;
    let isBusy = false;
    let liveListeners = [];
    let renderDebounceTimer = null;
    let activeStatementCustomer = null;

    let currentUser = null;
    let state = {
        branches: [],
        cashboxes: [],
        customers: [],
        suppliers: [],
        invoices: [],
        purchases: [],
        expenses: [],
        vouchers: [],
        employees: [],
        warehouse: []
    };

    function openFullPage(tabId) {
        if (tabId === 'employeesTab' && !hasFullAccess(currentUser)) {
            showToast('هذا القسم للمشرف العام والمدير فقط');
            return;
        }
        document.getElementById('homeMenuContainer').classList.add('hidden');
        document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
        document.getElementById(tabId).classList.remove('hidden');
        if (tabId === 'salesTab') {
            renderWarehouseCatalogDropdown();
            updateInvoiceStatementPreview();
        }
        if (tabId === 'vouchersTab') {
            toggleVoucherPartyFields();
            updateVoucherStatementPreview();
        }
        if (tabId === 'warehouseTab') populateTransferItems();
        if (tabId === 'profitsTab') renderProfitsTab();
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function goBackHome() {
        document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
        document.getElementById('homeMenuContainer').classList.remove('hidden');
        renderStats();
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function updateInvoiceStatementPreview() {
        const num = (document.getElementById('invRefNumber')?.value || '').trim();
        const el = document.getElementById('invStatementPreview');
        if (el) {
            el.textContent = `النص في الكشف: عليكم فاتورة مبيعات برقم ${num || '—'}`;
        }
    }

    function updateVoucherStatementPreview() {
        const type = document.getElementById('voucherType')?.value || 'receipt';
        const num = (document.getElementById('voucherRefNumber')?.value || '').trim();
        const prefix = type === 'receipt' ? 'لكم سند قبض برقم' : 'عليكم سند صرف برقم';
        const prefixEl = document.getElementById('voucherStatementPrefix');
        const prevEl = document.getElementById('voucherStatementPreview');
        if (prefixEl) prefixEl.textContent = prefix;
        if (prevEl) prevEl.textContent = `النص في الكشف: ${prefix} ${num || '—'}`;
    }

    function scheduleRender() {
        if (renderDebounceTimer) clearTimeout(renderDebounceTimer);
        renderDebounceTimer = setTimeout(() => {
            if (currentUser && currentUser.id) {
                const updatedMe = state.employees.find(e => e.id === currentUser.id);
                if (updatedMe) {
                    currentUser = updatedMe;
                    document.getElementById('headerWelcome').textContent = `${currentUser.fullName}`;
                    const roleBadge = document.getElementById('currentUserRoleBadge');
                    roleBadge.textContent = roleLabel(currentUser.role);
                    roleBadge.className = `badge ${roleBadgeClass(currentUser.role)}`;
                    document.getElementById('employeesNavBtn').classList.toggle('hidden', !hasFullAccess(currentUser));
                }
            }
            renderAllViews();
        }, 80);
    }

    function startRealtimeListeners() {
        stopRealtimeListeners();
        const cols = ['branches', 'cashboxes', 'customers', 'suppliers', 'invoices', 'purchases', 'expenses', 'vouchers', 'employees', 'warehouse'];
        cols.forEach(colName => {
            const unsub = db.collection(colName).onSnapshot(
                snap => {
                    const list = [];
                    snap.forEach(doc => list.push({ id: doc.id, ...doc.data() }));
                    state[colName] = list;
                    isDemoMode = false;
                    const badge = document.getElementById('connectionStatusBadge');
                    if (badge) {
                        badge.className = 'db-status';
                        badge.innerHTML = '<i class="fa-solid fa-bolt"></i> متصل مباشر';
                    }
                    scheduleRender();
                },
                err => {
                    console.warn(`Listener error on ${colName}:`, err);
                    isDemoMode = true;
                    const badge = document.getElementById('connectionStatusBadge');
                    if (badge) {
                        badge.className = 'db-status demo';
                        badge.innerHTML = '<i class="fa-solid fa-triangle-exclamation"></i> تحقق من القاعدة';
                    }
                }
            );
            liveListeners.push(unsub);
        });
    }

    function stopRealtimeListeners() {
        liveListeners.forEach(unsub => {
            try { unsub(); } catch (e) {}
        });
        liveListeners = [];
    }

    function hasFullAccess(user = currentUser) {
        if (!user) return false;
        return user.role === 'admin' || user.role === 'supervisor';
    }

    function canManageUsers(user = currentUser) {
        if (!user) return false;
        return user.role === 'admin' || user.role === 'supervisor';
    }

    function canEditRecord() {
        if (!currentUser) return false;
        if (hasFullAccess(currentUser)) return true;
        return Boolean(currentUser.canEdit);
    }

    function canDeleteRecord() {
        if (!currentUser) return false;
        if (hasFullAccess(currentUser)) return true;
        return Boolean(currentUser.canDelete);
    }

    function roleLabel(role) {
        if (role === 'admin') return 'مدير';
        if (role === 'supervisor') return 'مشرف عام';
        return 'موظف';
    }

    function roleBadgeClass(role) {
        if (role === 'admin') return 'badge-role';
        if (role === 'supervisor') return 'badge-sup';
        return 'badge-cash';
    }

    function toggleEmployeePermBox() {
        const role = document.getElementById('newEmpRole').value;
        document.getElementById('empPermissionsBox').classList.toggle('hidden', role !== 'cashier');
    }

    function showToast(msg) {
        const el = document.getElementById('toast');
        document.getElementById('toastText').textContent = msg;
        el.classList.add('show');
        setTimeout(() => el.classList.remove('show'), 2200);
    }

    function formatMoney(num) {
        return Number(num || 0).toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    }

    function getCashboxOpening(cb) {
        if (cb.openingBalance !== undefined && cb.openingBalance !== null) {
            return Number(cb.openingBalance || 0);
        }
        return Number(cb.balance || 0);
    }

    // حساب نظامي لرصيد الصندوق: رصيد افتتاحي + مبيعات نقدية + سندات قبض - سندات صرف - مشتروات نقدية - مصروفات
    function computeSystemCashboxBalance(cb) {
        const opening = getCashboxOpening(cb);
        const cashSales = state.invoices
            .filter(i => i.paymentType === 'cash' && i.cashboxId === cb.id)
            .reduce((s, i) => s + Number(i.netTotal || 0), 0);

        const receipts = state.vouchers
            .filter(v => v.type === 'receipt' && v.cashboxId === cb.id)
            .reduce((s, v) => s + Number(v.amount || 0), 0);

        const payments = state.vouchers
            .filter(v => v.type === 'payment' && v.cashboxId === cb.id)
            .reduce((s, v) => s + Number(v.amount || 0), 0);

        const cashPurchases = state.purchases
            .filter(p => p.paymentType === 'cash' && p.cashboxId === cb.id)
            .reduce((s, p) => s + Number(p.amount || 0), 0);

        const cashExpenses = state.expenses
            .filter(e => e.cashboxId === cb.id)
            .reduce((s, e) => s + Number(e.amount || 0), 0);

        return opening + cashSales + receipts - payments - cashPurchases - cashExpenses;
    }

    // حساب نظامي لمديونية العميل: فواتير آجلة باسم العميل - سندات قبض باسم العميل
    function computeSystemCustomerBalance(cust) {
        const creditInvoices = state.invoices
            .filter(i => i.paymentType === 'credit' && (
                (cust.id && i.customerId === cust.id) ||
                (!i.customerId && i.customerName && cust.name && i.customerName.trim() === cust.name.trim())
            ))
            .reduce((s, i) => s + Number(i.netTotal || 0), 0);

        const receipts = state.vouchers
            .filter(v => v.type === 'receipt' && (
                (cust.id && v.customerId === cust.id) ||
                (!v.customerId && v.customerName && cust.name && v.customerName.trim() === cust.name.trim())
            ))
            .reduce((s, v) => s + Number(v.amount || 0), 0);

        return Math.max(0, creditInvoices - receipts);
    }

    // حساب نظامي لمديونية المورد (دين علينا): مشتروات آجلة باسم المورد - سندات صرف باسم المورد
    function computeSystemSupplierBalance(sup) {
        const creditPurchases = state.purchases
            .filter(p => p.paymentType === 'credit' && (
                (sup.id && p.supplierId === sup.id) ||
                (!p.supplierId && p.supplierName && sup.name && p.supplierName.trim() === sup.name.trim())
            ))
            .reduce((s, p) => s + Number(p.amount || 0), 0);

        const paidVouchers = state.vouchers
            .filter(v => v.type === 'payment' && (
                (sup.id && v.supplierId === sup.id) ||
                (!v.supplierId && v.supplierName && sup.name && v.supplierName.trim() === sup.name.trim())
            ))
            .reduce((s, v) => s + Number(v.amount || 0), 0);

        return Math.max(0, creditPurchases - paidVouchers);
    }

    async function loadCollection(name) {
        const snap = await db.collection(name).get();
        const list = [];
        snap.forEach(doc => list.push({ id: doc.id, ...doc.data() }));
        return list;
    }

    async function reloadAllData(showMsg = false) {
        try {
            const [branches, cashboxes, customers, suppliers, invoices, purchases, expenses, vouchers, employees, warehouse] = await Promise.all([
                loadCollection('branches'),
                loadCollection('cashboxes'),
                loadCollection('customers'),
                loadCollection('suppliers'),
                loadCollection('invoices'),
                loadCollection('purchases'),
                loadCollection('expenses'),
                loadCollection('vouchers'),
                loadCollection('employees'),
                loadCollection('warehouse')
            ]);
            state = { branches, cashboxes, customers, suppliers, invoices, purchases, expenses, vouchers, employees, warehouse };
            if (currentUser && currentUser.id) {
                const updatedMe = state.employees.find(e => e.id === currentUser.id);
                if (updatedMe) currentUser = updatedMe;
            }
            isDemoMode = false;
            if (showMsg) showToast('تم التحديث');
        } catch (err) {
            console.warn('Firestore error:', err);
            isDemoMode = true;
        }
        renderAllViews();
    }

    async function handleLogin() {
        if (isBusy) return;
        const btn = document.getElementById('loginSubmitBtn');
        const btnText = document.getElementById('loginBtnText');
        const u = document.getElementById('loginUser').value.trim();
        const p = document.getElementById('loginPass').value.trim();

        if (!u || !p) {
            showToast('أدخل اسم المستخدم وكلمة المرور');
            return;
        }

        isBusy = true;
        btn.disabled = true;
        btnText.textContent = 'جاري الدخول...';

        try {
            let employees = [];
            try {
                employees = await loadCollection('employees');
                isDemoMode = false;
            } catch (e) {
                isDemoMode = true;
            }
            state.employees = employees;

            let found = state.employees.find(
                e => String(e.username || '').trim() === u && String(e.password || '').trim() === p
            );

            if (!found && u === ADMIN_USER && p === ADMIN_PASS) {
                found = {
                    id: 'emp_admin',
                    fullName: 'المدير العام',
                    username: ADMIN_USER,
                    password: ADMIN_PASS,
                    role: 'admin',
                    canEdit: true,
                    canDelete: true,
                    active: true
                };
                if (!isDemoMode && db) {
                    db.collection('employees').doc('emp_admin').set(found, { merge: true }).catch(() => {});
                }
            }

            if (!found) {
                showToast('بيانات الدخول غير صحيحة');
                return;
            }
            if (found.active === false) {
                showToast('الحساب موقوف');
                return;
            }

            currentUser = found;
            document.getElementById('headerWelcome').textContent = `${currentUser.fullName}`;
            const roleBadge = document.getElementById('currentUserRoleBadge');
            roleBadge.textContent = roleLabel(currentUser.role);
            roleBadge.className = `badge ${roleBadgeClass(currentUser.role)}`;

            document.getElementById('employeesNavBtn').classList.toggle('hidden', !hasFullAccess(currentUser));

            document.getElementById('loginView').classList.add('hidden');
            document.getElementById('mainAppView').classList.remove('hidden');
            goBackHome();

            if (document.getElementById('invoiceItemsContainer').children.length === 0) {
                addInvoiceItemRow();
            }

            renderAllViews();
            startRealtimeListeners();
        } finally {
            isBusy = false;
            btn.disabled = false;
            btnText.textContent = 'دخول';
        }
    }

    function confirmLogout() {
        if (!confirm('هل تريد تسجيل الخروج من النظام؟')) return;
        handleLogout();
    }

    function handleLogout() {
        stopRealtimeListeners();
        currentUser = null;
        document.getElementById('loginUser').value = '';
        document.getElementById('loginPass').value = '';
        document.getElementById('mainAppView').classList.add('hidden');
        document.getElementById('loginView').classList.remove('hidden');
    }

    function renderAllViews() {
        populateDropdowns();
        renderBranchesChips();
        renderStats();
        renderInvoicesTable();
        renderSuppliersTable();
        renderPurchasesTable();
        renderExpensesTable();
        renderVouchersTable();
        renderCashboxesList();
        renderWarehouseTable();
        renderCustomersTable();
        renderProfitsTab();
        renderEmployeesTable();
    }

    function populateDropdowns() {
        const branchList = state.branches.length
            ? state.branches
            : [{ id: 'main_branch', name: 'الفرع الرئيسي' }];

        const invBrSel = document.getElementById('invBranchSelect');
        const purBrSel = document.getElementById('purBranchSelect');
        const whBrSel = document.getElementById('whItemBranchSelect');
        const modalWhBrSel = document.getElementById('modalWhBranchSelect');
        const filterBrSel = document.getElementById('activeBranchFilter');
        const fromBrSel = document.getElementById('transferFromBranch');
        const toBrSel = document.getElementById('transferToBranch');
        const modalFromBrSel = document.getElementById('modalTransferFromBranch');
        const modalToBrSel = document.getElementById('modalTransferToBranch');

        const prevInvBr = invBrSel.value;
        const prevPurBr = purBrSel.value;
        const prevWhBr = whBrSel.value;
        const prevModalWhBr = modalWhBrSel.value;
        const prevFilterBr = filterBrSel.value;
        const prevFromBr = fromBrSel.value;
        const prevToBr = toBrSel.value;
        const prevModalFromBr = modalFromBrSel.value;
        const prevModalToBr = modalToBrSel.value;

        const brOpts = branchList.map(b => `<option value="${b.id}">${b.name}</option>`).join('');
        invBrSel.innerHTML = brOpts;
        purBrSel.innerHTML = brOpts;
        whBrSel.innerHTML = brOpts;
        modalWhBrSel.innerHTML = brOpts;
        filterBrSel.innerHTML = '<option value="ALL">جميع الفروع</option>' + brOpts;
        fromBrSel.innerHTML = brOpts;
        toBrSel.innerHTML = brOpts;
        modalFromBrSel.innerHTML = brOpts;
        modalToBrSel.innerHTML = brOpts;

        if (prevInvBr && branchList.some(b => b.id === prevInvBr)) invBrSel.value = prevInvBr;
        if (prevPurBr && branchList.some(b => b.id === prevPurBr)) purBrSel.value = prevPurBr;
        if (prevWhBr && branchList.some(b => b.id === prevWhBr)) whBrSel.value = prevWhBr;
        if (prevModalWhBr && branchList.some(b => b.id === prevModalWhBr)) modalWhBrSel.value = prevModalWhBr;
        if (prevFilterBr) filterBrSel.value = prevFilterBr;
        if (prevFromBr && branchList.some(b => b.id === prevFromBr)) fromBrSel.value = prevFromBr;
        if (prevToBr && branchList.some(b => b.id === prevToBr)) toBrSel.value = prevToBr;
        else if (branchList.length > 1) toBrSel.value = branchList[1].id;

        if (prevModalFromBr && branchList.some(b => b.id === prevModalFromBr)) modalFromBrSel.value = prevModalFromBr;
        if (prevModalToBr && branchList.some(b => b.id === prevModalToBr)) modalToBrSel.value = prevModalToBr;
        else if (branchList.length > 1) modalToBrSel.value = branchList[1].id;

        renderWarehouseCatalogDropdown();
        populateTransferItems();
        populateModalTransferItems();

        const cbSelInv = document.getElementById('invCashboxSelect');
        const cbSelPur = document.getElementById('purCashboxSelect');
        const cbSelExp = document.getElementById('expCashboxSelect');
        const cbSelVch = document.getElementById('voucherCashboxSelect');
        const prevCbInv = cbSelInv.value;
        const prevCbPur = cbSelPur.value;
        const prevCbExp = cbSelExp.value;
        const prevCbVch = cbSelVch.value;

        const cbOpts = state.cashboxes.length
            ? state.cashboxes.map(c => `<option value="${c.id}">${c.name} (${formatMoney(computeSystemCashboxBalance(c))})</option>`).join('')
            : '<option value="">أضف صندوقاً أولاً</option>';
        cbSelInv.innerHTML = cbOpts;
        cbSelPur.innerHTML = cbOpts;
        cbSelExp.innerHTML = cbOpts;
        cbSelVch.innerHTML = cbOpts;
        if (prevCbInv && state.cashboxes.some(c => c.id === prevCbInv)) cbSelInv.value = prevCbInv;
        if (prevCbPur && state.cashboxes.some(c => c.id === prevCbPur)) cbSelPur.value = prevCbPur;
        if (prevCbExp && state.cashboxes.some(c => c.id === prevCbExp)) cbSelExp.value = prevCbExp;
        if (prevCbVch && state.cashboxes.some(c => c.id === prevCbVch)) cbSelVch.value = prevCbVch;

        const custSelInv = document.getElementById('invCustomerSelect');
        const custSelVch = document.getElementById('voucherCustomerSelect');
        const prevCustInv = custSelInv.value;
        const prevCustVch = custSelVch.value;

        const custOpts = state.customers.length
            ? state.customers.map(c => `<option value="${c.id}">${c.name} (${formatMoney(computeSystemCustomerBalance(c))})</option>`).join('')
            : '<option value="">لا يوجد عملاء</option>';
        custSelInv.innerHTML = custOpts;
        custSelVch.innerHTML = '<option value="">بدون عميل</option>' + custOpts;
        if (prevCustInv && state.customers.some(c => c.id === prevCustInv)) custSelInv.value = prevCustInv;
        if (prevCustVch) custSelVch.value = prevCustVch;

        const supSelPur = document.getElementById('purSupplierSelect');
        const supSelVch = document.getElementById('voucherSupplierSelect');
        const prevSupPur = supSelPur.value;
        const prevSupVch = supSelVch.value;

        const supOpts = state.suppliers.length
            ? state.suppliers.map(s => `<option value="${s.id}">${s.name} (${formatMoney(computeSystemSupplierBalance(s))})</option>`).join('')
            : '<option value="">أضف مورداً أولاً</option>';
        supSelPur.innerHTML = supOpts;
        supSelVch.innerHTML = '<option value="">بدون مورد</option>' + supOpts;
        if (prevSupPur && state.suppliers.some(s => s.id === prevSupPur)) supSelPur.value = prevSupPur;
        if (prevSupVch) supSelVch.value = prevSupVch;
    }

    function renderBranchesChips() {
        const el = document.getElementById('branchesChipsList');
        if (!el) return;
        const list = state.branches.length ? state.branches : [{ id: 'main_branch', name: 'الفرع الرئيسي' }];
        el.innerHTML = list.map(b => {
            const canDel = canDeleteRecord() && b.id !== 'main_branch' && list.length > 1;
            return `
                <div class="branch-chip">
                    <i class="fa-solid fa-store" style="color:var(--primary);"></i>
                    <span>${b.name}</span>
                    ${canDel ? `<button type="button" class="btn btn-danger btn-sm" style="padding:3px 7px;" onclick="deleteBranchItem('${b.id}')" title="حذف الفرع"><i class="fa-solid fa-xmark"></i></button>` : ''}
                </div>
            `;
        }).join('');
    }

    async function deleteBranchItem(brId) {
        if (isBusy || !canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        const br = state.branches.find(b => b.id === brId);
        if (!br) return;
        if (!confirm(`تأكيد حذف الفرع (${br.name})؟`)) return;
        isBusy = true;
        try {
            await db.collection('branches').doc(brId).delete();
            showToast('تم حذف الفرع');
        } finally {
            isBusy = false;
        }
    }

    function renderWarehouseCatalogDropdown() {
        const sel = document.getElementById('warehouseCatalogSelect');
        if (!sel) return;
        const branchId = document.getElementById('invBranchSelect').value || 'main_branch';
        const q = (document.getElementById('warehouseItemSearch').value || '').trim().toLowerCase();

        let items = state.warehouse.filter(w => (w.branchId || 'main_branch') === branchId);
        if (!items.length) items = state.warehouse.slice();

        if (q) {
            items = items.filter(w => (w.name || '').toLowerCase().includes(q));
        }

        const prevVal = sel.value;
        sel.innerHTML = items.length
            ? items.map(w => `<option value="${w.id}">${w.name} (${w.unit || 'حبة'}) — متاح: ${w.qty || 0} — سعر: ${formatMoney(w.price)}</option>`).join('')
            : '<option value="">لا توجد أصناف مطابقة في المخازن</option>';

        if (prevVal && items.some(w => w.id === prevVal)) {
            sel.value = prevVal;
        }
    }

    function addSelectedWarehouseItemToInvoice() {
        const sel = document.getElementById('warehouseCatalogSelect');
        const item = state.warehouse.find(w => w.id === sel.value);
        if (!item) {
            showToast('اختر صنفاً من المخازن أولاً');
            return;
        }
        addInvoiceItemRow({
            name: item.name,
            unit: item.unit || 'حبة',
            qty: 1,
            price: Number(item.price || 0)
        });
        showToast(`تمت إضافة ${item.name}`);
    }

    function openAddItemModal() {
        populateDropdowns();
        document.getElementById('quickAddItemModal').classList.remove('hidden');
    }

    function closeQuickAddItemModal() {
        document.getElementById('quickAddItemModal').classList.add('hidden');
    }

    async function saveQuickWarehouseItem() {
        if (isBusy) return;
        const branchId = document.getElementById('modalWhBranchSelect').value || 'main_branch';
        const branchObj = state.branches.find(b => b.id === branchId);
        const branchName = branchObj ? branchObj.name : 'الفرع الرئيسي';
        const name = document.getElementById('modalItemName').value.trim();
        const unit = document.getElementById('modalItemUnit').value || 'حبة';
        const qty = Number(document.getElementById('modalItemQty').value || 0);
        const price = Number(document.getElementById('modalItemPrice').value || 0);
        if (!name) {
            showToast('أدخل اسم الصنف');
            return;
        }
        isBusy = true;
        try {
            const existing = state.warehouse.find(
                w => (w.branchId || 'main_branch') === branchId &&
                     w.name.toLowerCase() === name.toLowerCase() &&
                     (w.unit || 'حبة') === unit
            );
            if (existing) {
                if (!canEditRecord()) {
                    showToast('ليس لديك صلاحية التعديل على المخزون');
                    return;
                }
                await db.collection('warehouse').doc(existing.id).update({ qty, price, unit, branchId, branchName });
            } else {
                const id = `wh_${Date.now()}`;
                await db.collection('warehouse').doc(id).set({ id, branchId, branchName, name, unit, qty, price });
            }
            document.getElementById('modalItemName').value = '';
            document.getElementById('modalItemQty').value = '1';
            document.getElementById('modalItemPrice').value = '0';
            closeQuickAddItemModal();
            showToast('تم حفظ الصنف في المخزن');
        } finally {
            isBusy = false;
        }
    }

    function openTransferModal() {
        populateDropdowns();
        document.getElementById('quickTransferModal').classList.remove('hidden');
    }

    function closeQuickTransferModal() {
        document.getElementById('quickTransferModal').classList.add('hidden');
    }

    function populateModalTransferItems() {
        const fromBranchId = document.getElementById('modalTransferFromBranch')?.value || 'main_branch';
        const sel = document.getElementById('modalTransferItemSelect');
        if (!sel) return;
        const availableItems = state.warehouse.filter(
            w => (w.branchId || 'main_branch') === fromBranchId && Number(w.qty || 0) > 0
        );
        sel.innerHTML = availableItems.length
            ? availableItems.map(w => `<option value="${w.id}">${w.name} — متاح: ${w.qty} ${w.unit || 'حبة'}</option>`).join('')
            : '<option value="">لا توجد أصناف متاحة في هذا المخزن</option>';
    }

    async function executeModalTransfer() {
        if (isBusy) return;
        const fromBranchId = document.getElementById('modalTransferFromBranch').value || 'main_branch';
        const toBranchId = document.getElementById('modalTransferToBranch').value || 'main_branch';
        const itemId = document.getElementById('modalTransferItemSelect').value;
        const qtyToMove = Number(document.getElementById('modalTransferQty').value || 0);
        if (fromBranchId === toBranchId) {
            showToast('اختر مخزناً مختلفاً للنقل إليه');
            return;
        }
        const sourceItem = state.warehouse.find(w => w.id === itemId);
        if (!sourceItem) {
            showToast('اختر الصنف المراد نقله');
            return;
        }
        const currentQty = Number(sourceItem.qty || 0);
        if (qtyToMove <= 0 || qtyToMove > currentQty) {
            showToast(`الكمية غير صحيحة (المتاح: ${currentQty})`);
            return;
        }
        const toBranchObj = state.branches.find(b => b.id === toBranchId);
        const toBranchName = toBranchObj ? toBranchObj.name : 'الفرع المستهدف';
        const unit = sourceItem.unit || 'حبة';
        const price = Number(sourceItem.price || 0);

        isBusy = true;
        try {
            await db.collection('warehouse').doc(sourceItem.id).update({ qty: currentQty - qtyToMove });
            const targetItem = state.warehouse.find(
                w => (w.branchId || 'main_branch') === toBranchId &&
                     w.name.toLowerCase() === sourceItem.name.toLowerCase() &&
                     (w.unit || 'حبة') === unit
            );
            if (targetItem) {
                await db.collection('warehouse').doc(targetItem.id).update({ qty: Number(targetItem.qty || 0) + qtyToMove });
            } else {
                const newId = `wh_${Date.now()}`;
                await db.collection('warehouse').doc(newId).set({ id: newId, branchId: toBranchId, branchName: toBranchName, name: sourceItem.name, unit, qty: qtyToMove, price });
            }
            document.getElementById('modalTransferQty').value = '1';
            closeQuickTransferModal();
            showToast(`تم نقل ${qtyToMove} ${unit} إلى ${toBranchName}`);
        } finally {
            isBusy = false;
        }
    }

    function populateTransferItems() {
        const fromBranchId = document.getElementById('transferFromBranch').value || 'main_branch';
        const sel = document.getElementById('transferItemSelect');
        const prevVal = sel.value;

        const availableItems = state.warehouse.filter(
            w => (w.branchId || 'main_branch') === fromBranchId && Number(w.qty || 0) > 0
        );

        sel.innerHTML = availableItems.length
            ? availableItems.map(w => `<option value="${w.id}">${w.name} — متاح: ${w.qty} ${w.unit || 'حبة'}</option>`).join('')
            : '<option value="">لا توجد أصناف متاحة في هذا المخزن</option>';

        if (prevVal && availableItems.some(w => w.id === prevVal)) {
            sel.value = prevVal;
        }
    }

    async function transferWarehouseStock() {
        if (isBusy) return;
        const btn = document.getElementById('executeTransferBtn');
        const fromBranchId = document.getElementById('transferFromBranch').value || 'main_branch';
        const toBranchId = document.getElementById('transferToBranch').value || 'main_branch';
        const itemId = document.getElementById('transferItemSelect').value;
        const qtyToMove = Number(document.getElementById('transferQty').value || 0);

        if (fromBranchId === toBranchId) {
            showToast('اختر مخزناً مختلفاً للنقل إليه');
            return;
        }

        const sourceItem = state.warehouse.find(w => w.id === itemId);
        if (!sourceItem) {
            showToast('اختر الصنف المراد نقله');
            return;
        }

        const currentQty = Number(sourceItem.qty || 0);
        if (qtyToMove <= 0 || qtyToMove > currentQty) {
            showToast(`الكمية غير صحيحة (المتاح: ${currentQty})`);
            return;
        }

        const toBranchObj = state.branches.find(b => b.id === toBranchId);
        const toBranchName = toBranchObj ? toBranchObj.name : 'الفرع المستهدف';
        const unit = sourceItem.unit || 'حبة';
        const price = Number(sourceItem.price || 0);

        isBusy = true;
        btn.disabled = true;

        try {
            await db.collection('warehouse').doc(sourceItem.id).update({ qty: currentQty - qtyToMove });

            const targetItem = state.warehouse.find(
                w => (w.branchId || 'main_branch') === toBranchId &&
                     w.name.toLowerCase() === sourceItem.name.toLowerCase() &&
                     (w.unit || 'حبة') === unit
            );

            if (targetItem) {
                await db.collection('warehouse').doc(targetItem.id).update({
                    qty: Number(targetItem.qty || 0) + qtyToMove
                });
            } else {
                const newId = `wh_${Date.now()}`;
                await db.collection('warehouse').doc(newId).set({
                    id: newId,
                    branchId: toBranchId,
                    branchName: toBranchName,
                    name: sourceItem.name,
                    unit,
                    qty: qtyToMove,
                    price
                });
            }

            document.getElementById('transferQty').value = '1';
            showToast(`تم نقل ${qtyToMove} ${unit} إلى ${toBranchName}`);
        } catch (e) {
            showToast('تعذر إتمام النقل');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    function renderStats() {
        const sales = state.invoices.reduce((s, i) => s + Number(i.netTotal || 0), 0);
        const cash = state.cashboxes.reduce((s, c) => s + computeSystemCashboxBalance(c), 0);
        const debts = state.customers.reduce((s, c) => s + computeSystemCustomerBalance(c), 0);
        const supDebts = state.suppliers.reduce((s, sup) => s + computeSystemSupplierBalance(sup), 0);
        const expTotal = state.expenses.reduce((s, e) => s + Number(e.amount || 0), 0);
        const totalUnits = state.warehouse.reduce((s, w) => s + Number(w.qty || 0), 0);
        const totalStockVal = state.warehouse.reduce((s, w) => s + (Number(w.qty || 0) * Number(w.price || 0)), 0);

        document.getElementById('kpiTotalSales').textContent = formatMoney(sales);
        document.getElementById('kpiTotalCash').textContent = formatMoney(cash);
        document.getElementById('kpiTotalReceivables').textContent = formatMoney(debts);
        document.getElementById('kpiWarehouseStock').textContent = Number(totalUnits).toLocaleString('en-US');
        document.getElementById('suppliersDebtTotal').textContent = formatMoney(supDebts);
        document.getElementById('expensesTabTotal').textContent = formatMoney(expTotal);
        document.getElementById('warehouseTotalValueBadge').textContent = `قيمة المخزون: ${formatMoney(totalStockVal)}`;
    }

    function renderProfitsTab() {
        const sales = state.invoices.reduce((s, i) => s + Number(i.netTotal || 0), 0);
        const purchasesTotal = state.purchases.reduce((s, p) => s + Number(p.amount || 0), 0);
        const expensesTotal = state.expenses.reduce((s, e) => s + Number(e.amount || 0), 0);
        const netProfit = sales - purchasesTotal - expensesTotal;

        const sEl = document.getElementById('profTotalSales');
        const pEl = document.getElementById('profTotalPurchases');
        const eEl = document.getElementById('profTotalExpenses');
        const nEl = document.getElementById('profNetProfit');
        if (sEl) sEl.textContent = formatMoney(sales);
        if (pEl) pEl.textContent = formatMoney(purchasesTotal);
        if (eEl) eEl.textContent = formatMoney(expensesTotal);
        if (nEl) {
            nEl.textContent = formatMoney(netProfit);
            nEl.style.color = netProfit >= 0 ? 'var(--success)' : 'var(--danger)';
        }
    }

    // الموردون والمشتروات
    function togglePurchaseCashboxField() {
        const isCash = document.getElementById('purPaymentType').value === 'cash';
        document.getElementById('purCashboxGroup').classList.toggle('hidden', !isCash);
    }

    async function createSupplier() {
        if (isBusy) return;
        const btn = document.getElementById('saveSupplierBtn');
        const name = document.getElementById('newSupplierName').value.trim();
        const phone = document.getElementById('newSupplierPhone').value.trim();
        if (!name) {
            showToast('أدخل اسم المورد');
            return;
        }
        isBusy = true;
        btn.disabled = true;
        try {
            const id = `sup_${Date.now()}`;
            await db.collection('suppliers').doc(id).set({ id, name, phone: phone || '-' });
            document.getElementById('newSupplierName').value = '';
            document.getElementById('newSupplierPhone').value = '';
            showToast('تم حفظ المورد');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function editSupplierItem(supId) {
        if (!canEditRecord()) {
            showToast('ليس لديك صلاحية التعديل');
            return;
        }
        const s = state.suppliers.find(x => x.id === supId);
        if (!s) return;
        const nextName = prompt('تعديل اسم المورد:', s.name);
        if (nextName === null || !nextName.trim()) return;
        const nextPhone = prompt('تعديل رقم الهاتف:', s.phone || '');
        if (nextPhone === null) return;
        await db.collection('suppliers').doc(supId).update({
            name: nextName.trim(),
            phone: nextPhone.trim() || '-'
        });
        showToast('تم تعديل المورد');
    }

    async function deleteSupplierItem(supId) {
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        if (!confirm('تأكيد حذف المورد؟')) return;
        await db.collection('suppliers').doc(supId).delete();
        showToast('تم حذف المورد');
    }

    function renderSuppliersTable() {
        const tbody = document.getElementById('suppliersTableBody');
        if (!tbody) return;
        tbody.innerHTML = state.suppliers.length
            ? state.suppliers.map(s => {
                const sysBal = computeSystemSupplierBalance(s);
                return `
                    <tr>
                        <td><strong>${s.name}</strong></td>
                        <td>${s.phone || '-'}</td>
                        <td><span class="mono" style="color:${sysBal > 0 ? 'var(--danger)' : 'var(--success)'};">${formatMoney(sysBal)}</span></td>
                        <td style="white-space:nowrap;">
                            ${canEditRecord() ? `<button class="btn btn-outline btn-sm" onclick="editSupplierItem('${s.id}')"><i class="fa-solid fa-pen"></i></button>` : ''}
                            ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deleteSupplierItem('${s.id}')"><i class="fa-solid fa-trash"></i></button>` : ''}
                        </td>
                    </tr>
                `;
            }).join('')
            : '<tr><td colspan="4" style="text-align:center; color:var(--text-muted);">لا يوجد موردون</td></tr>';
    }

    async function createPurchaseOrder() {
        if (isBusy) return;
        const btn = document.getElementById('savePurchaseBtn');
        const branchId = document.getElementById('purBranchSelect').value || 'main_branch';
        const branchObj = state.branches.find(b => b.id === branchId);
        const branchName = branchObj ? branchObj.name : 'الفرع الرئيسي';

        const supplierId = document.getElementById('purSupplierSelect').value;
        const supplierObj = state.suppliers.find(s => s.id === supplierId);
        const paymentType = document.getElementById('purPaymentType').value;
        const cashboxId = document.getElementById('purCashboxSelect').value;
        const title = document.getElementById('purTitle').value.trim();
        const addQty = Number(document.getElementById('purAddQty').value || 0);
        const unit = document.getElementById('purUnit').value || 'حبة';
        const amount = Number(document.getElementById('purAmount').value || 0);
        const notes = document.getElementById('purNotes').value.trim();

        if (!title || amount <= 0) {
            showToast('أدخل اسم الصنف والمبلغ الصحيح');
            return;
        }
        if (!supplierObj) {
            showToast('اختر المورد أو أضف مورداً أولاً');
            return;
        }

        const cashbox = paymentType === 'cash' ? state.cashboxes.find(c => c.id === cashboxId) : null;
        if (paymentType === 'cash' && !cashbox) {
            showToast('اختر الصندوق');
            return;
        }

        isBusy = true;
        btn.disabled = true;

        try {
            const purId = `PUR-${Date.now()}`;
            const unitCost = addQty > 0 ? Number((amount / addQty).toFixed(2)) : 0;

            await db.collection('purchases').doc(purId).set({
                id: purId,
                date: new Date().toISOString().split('T')[0],
                branchId,
                branchName,
                supplierId: supplierObj.id,
                supplierName: supplierObj.name,
                paymentType,
                cashboxId: cashbox ? cashbox.id : '',
                cashboxName: cashbox ? cashbox.name : 'آجل (دين)',
                title,
                addQty,
                unit,
                amount,
                notes,
                employee: currentUser.fullName
            });

            if (addQty > 0) {
                const existing = state.warehouse.find(
                    w => (w.branchId || 'main_branch') === branchId &&
                         w.name.toLowerCase() === title.toLowerCase() &&
                         (w.unit || 'حبة') === unit
                );
                if (existing) {
                    await db.collection('warehouse').doc(existing.id).update({
                        qty: Number(existing.qty || 0) + addQty
                    });
                } else {
                    const whId = `wh_${Date.now()}`;
                    await db.collection('warehouse').doc(whId).set({
                        id: whId,
                        branchId,
                        branchName,
                        name: title,
                        unit,
                        qty: addQty,
                        price: unitCost
                    });
                }
            }

            document.getElementById('purTitle').value = '';
            document.getElementById('purAddQty').value = '1';
            document.getElementById('purAmount').value = '';
            document.getElementById('purNotes').value = '';
            showToast('تم حفظ المشتروات');
        } catch (e) {
            showToast('تعذر حفظ المشتروات');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function deletePurchaseRecord(purId) {
        if (isBusy) return;
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        const p = state.purchases.find(x => x.id === purId);
        if (!p) return;
        if (!confirm(`تأكيد حذف فاتورة المشتروات (${p.title})؟`)) return;

        isBusy = true;
        try {
            await db.collection('purchases').doc(purId).delete();
            showToast('تم حذف السجل');
        } finally {
            isBusy = false;
        }
    }

    function renderPurchasesTable() {
        const tbody = document.getElementById('purchasesTableBody');
        if (!tbody) return;
        const q = (document.getElementById('purchaseSearchInput')?.value || '').toLowerCase().trim();
        const list = state.purchases
            .filter(p =>
                (p.title || '').toLowerCase().includes(q) ||
                (p.supplierName || '').toLowerCase().includes(q) ||
                (p.branchName || '').toLowerCase().includes(q)
            )
            .slice().reverse();

        tbody.innerHTML = list.length
            ? list.map(p => `
                <tr>
                    <td><span class="mono">${p.date || '-'}</span></td>
                    <td>${p.branchName || 'الفرع الرئيسي'}</td>
                    <td><strong>${p.supplierName || '-'}</strong></td>
                    <td>${p.title}</td>
                    <td>${Number(p.addQty || 0) > 0 ? `<span class="mono">${p.addQty}</span> ${p.unit || 'حبة'}` : '-'}</td>
                    <td>${p.paymentType === 'cash' ? '<span class="badge badge-cash">نقدي</span>' : '<span class="badge badge-credit">دين (آجل)</span>'}</td>
                    <td><span class="mono">${formatMoney(p.amount)}</span></td>
                    <td>
                        ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deletePurchaseRecord('${p.id}')"><i class="fa-solid fa-trash"></i></button>` : '<span style="color:var(--text-muted); font-size:11px;">عرض فقط</span>'}
                    </td>
                </tr>
            `).join('')
            : '<tr><td colspan="8" style="text-align:center; color:var(--text-muted);">لا توجد مشتروات مسجلة</td></tr>';
    }

    // المصروفات المستقلة
    async function createExpenseRecord() {
        if (isBusy) return;
        const btn = document.getElementById('saveExpenseBtn');
        const cashboxId = document.getElementById('expCashboxSelect').value;
        const title = document.getElementById('expTitle').value.trim();
        const amount = Number(document.getElementById('expAmount').value || 0);
        const notes = document.getElementById('expNotes').value.trim();

        const cashbox = state.cashboxes.find(c => c.id === cashboxId);
        if (!cashbox || !title || amount <= 0) {
            showToast('اختر الصندوق وأدخل البيان والمبلغ');
            return;
        }

        isBusy = true;
        btn.disabled = true;

        try {
            const expId = `EXP-${Date.now()}`;
            await db.collection('expenses').doc(expId).set({
                id: expId,
                date: new Date().toISOString().split('T')[0],
                cashboxId: cashbox.id,
                cashboxName: cashbox.name,
                title,
                amount,
                notes,
                employee: currentUser.fullName
            });

            document.getElementById('expTitle').value = '';
            document.getElementById('expAmount').value = '';
            document.getElementById('expNotes').value = '';
            showToast('تم حفظ المصروف');
        } catch (e) {
            showToast('تعذر حفظ المصروف');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function deleteExpenseRecord(expId) {
        if (isBusy) return;
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        if (!confirm('تأكيد حذف المصروف؟')) return;
        isBusy = true;
        try {
            await db.collection('expenses').doc(expId).delete();
            showToast('تم حذف المصروف');
        } finally {
            isBusy = false;
        }
    }

    function renderExpensesTable() {
        const tbody = document.getElementById('expensesTableBody');
        if (!tbody) return;
        const list = state.expenses.slice().reverse();
        tbody.innerHTML = list.length
            ? list.map(e => `
                <tr>
                    <td><span class="mono">${e.date || '-'}</span></td>
                    <td>${e.cashboxName || '-'}</td>
                    <td>
                        <strong>${e.title}</strong>
                        ${e.notes ? `<div style="font-size:11px; color:var(--text-muted);">${e.notes}</div>` : ''}
                    </td>
                    <td><span class="mono" style="color:var(--danger);">${formatMoney(e.amount)}</span></td>
                    <td>${e.employee || '-'}</td>
                    <td>
                        ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deleteExpenseRecord('${e.id}')"><i class="fa-solid fa-trash"></i></button>` : '<span style="color:var(--text-muted); font-size:11px;">عرض فقط</span>'}
                    </td>
                </tr>
            `).join('')
            : '<tr><td colspan="6" style="text-align:center; color:var(--text-muted);">لا توجد مصروفات مسجلة</td></tr>';
    }

    function toggleInvoicePaymentFields() {
        const isCash = document.getElementById('invPaymentType').value === 'cash';
        document.getElementById('invCashboxGroup').classList.toggle('hidden', !isCash);
    }

    function addInvoiceItemRow(prefill = null) {
        const container = document.getElementById('invoiceItemsContainer');
        const nameVal = prefill ? prefill.name : '';
        const unitVal = prefill ? (prefill.unit || 'حبة') : 'حبة';
        const qtyVal = prefill ? (prefill.qty || 1) : 1;
        const priceVal = prefill ? (prefill.price || 0) : 0;

        const rows = container.querySelectorAll('.invoice-item-row');
        if (prefill && rows.length === 1 && !rows[0].querySelector('.item-name').value.trim()) {
            rows[0].querySelector('.item-name').value = nameVal;
            rows[0].querySelector('.item-unit').value = unitVal;
            rows[0].querySelector('.item-qty').value = qtyVal;
            rows[0].querySelector('.item-price').value = priceVal;
            recalculateInvoiceTotal();
            return;
        }

        const row = document.createElement('div');
        row.className = 'invoice-item-row';
        row.innerHTML = `
            <input type="text" class="form-control item-name" placeholder="اسم الصنف" value="${nameVal}">
            <select class="form-control item-unit">
                <option value="حبة" ${unitVal === 'حبة' ? 'selected' : ''}>حبة</option>
                <option value="شدة" ${unitVal === 'شدة' ? 'selected' : ''}>شدة</option>
            </select>
            <input type="number" class="form-control item-qty num-input" value="${qtyVal}" min="1" placeholder="الكمية" oninput="recalculateInvoiceTotal()">
            <input type="number" class="form-control item-price num-input" value="${priceVal}" min="0" placeholder="السعر" oninput="recalculateInvoiceTotal()">
            <button type="button" class="btn btn-danger btn-sm" onclick="this.parentElement.remove(); recalculateInvoiceTotal();">
                <i class="fa-solid fa-trash"></i>
            </button>
        `;
        container.appendChild(row);
        recalculateInvoiceTotal();
    }

    function recalculateInvoiceTotal() {
        let subtotal = 0;
        document.querySelectorAll('#invoiceItemsContainer .invoice-item-row').forEach(r => {
            subtotal += Number(r.querySelector('.item-qty').value || 0) * Number(r.querySelector('.item-price').value || 0);
        });
        const discount = Number(document.getElementById('invDiscount').value || 0);
        const net = Math.max(0, subtotal - discount);
        document.getElementById('invNetTotalDisplay').textContent = formatMoney(net);
        return net;
    }

    function openPrintModal(inv) {
        if (!inv) return;
        document.getElementById('prInvId').textContent = inv.id || '-';
        document.getElementById('prInvDate').textContent = inv.date || '-';
        document.getElementById('prInvBranch').textContent = inv.branchName || 'الفرع الرئيسي';
        document.getElementById('prInvCustomer').textContent = inv.customerName || '-';
        document.getElementById('prInvType').textContent = inv.paymentType === 'cash' ? `نقدي (${inv.cashboxName || 'الصندوق'})` : 'آجل';
        document.getElementById('prInvEmp').textContent = inv.employee || '-';

        const items = Array.isArray(inv.items) ? inv.items : [];
        document.getElementById('prInvItemsBody').innerHTML = items.length
            ? items.map(it => {
                const rowTotal = Number(it.qty || 0) * Number(it.price || 0);
                return `
                    <tr>
                        <td>${it.name}</td>
                        <td>${it.unit || 'حبة'}</td>
                        <td><span class="mono">${it.qty}</span></td>
                        <td><span class="mono">${formatMoney(it.price)}</span></td>
                        <td><span class="mono">${formatMoney(rowTotal)}</span></td>
                    </tr>
                `;
            }).join('')
            : '<tr><td colspan="5" style="text-align:center;">لا توجد أصناف</td></tr>';

        document.getElementById('prInvDiscount').textContent = formatMoney(inv.discount || 0);
        document.getElementById('prInvNet').textContent = formatMoney(inv.netTotal || 0);

        const notesRow = document.getElementById('prInvNotesRow');
        if (inv.notes) {
            notesRow.textContent = `البيان: ${inv.notes}`;
            notesRow.classList.remove('hidden');
        } else {
            notesRow.textContent = '';
            notesRow.classList.add('hidden');
        }

        document.getElementById('printInvoiceModal').classList.remove('hidden');
    }

    function closePrintModal() {
        document.getElementById('printInvoiceModal').classList.add('hidden');
    }

    function printInvoiceById(invId) {
        const inv = state.invoices.find(i => i.id === invId);
        if (inv) openPrintModal(inv);
    }

    async function saveSalesInvoice() {
        if (isBusy) return;
        const btn = document.getElementById('saveInvoiceBtn');
        const branchId = document.getElementById('invBranchSelect').value || 'main_branch';
        const branchObj = state.branches.find(b => b.id === branchId);
        const branchName = branchObj ? branchObj.name : 'الفرع الرئيسي';

        const paymentType = document.getElementById('invPaymentType').value;
        const cashboxId = document.getElementById('invCashboxSelect').value;
        const customerId = document.getElementById('invCustomerSelect').value;
        const discount = Number(document.getElementById('invDiscount').value || 0);
        const refNum = (document.getElementById('invRefNumber')?.value || '').trim();
        const notes = `عليكم فاتورة مبيعات برقم ${refNum || '—'}`;

        const items = [];
        document.querySelectorAll('#invoiceItemsContainer .invoice-item-row').forEach(r => {
            const name = r.querySelector('.item-name').value.trim();
            const unit = r.querySelector('.item-unit').value || 'حبة';
            const qty = Number(r.querySelector('.item-qty').value || 0);
            const price = Number(r.querySelector('.item-price').value || 0);
            if (name && qty > 0) items.push({ name, unit, qty, price });
        });

        if (items.length === 0) {
            showToast('أضف صنفاً واحداً على الأقل');
            return;
        }

        const customer = state.customers.find(c => c.id === customerId);
        if (!customer) {
            showToast('اختر العميل');
            return;
        }

        const cashbox = paymentType === 'cash' ? state.cashboxes.find(c => c.id === cashboxId) : null;
        if (paymentType === 'cash' && !cashbox) {
            showToast('اختر الصندوق');
            return;
        }

        isBusy = true;
        btn.disabled = true;

        try {
            const subtotal = items.reduce((s, x) => s + x.qty * x.price, 0);
            const netTotal = Math.max(0, subtotal - discount);
            const invId = `INV-${Date.now()}`;

            const invoiceDoc = {
                id: invId,
                date: new Date().toISOString().split('T')[0],
                branchId,
                branchName,
                customerId: customer.id,
                customerName: customer.name,
                paymentType,
                cashboxId: cashbox ? cashbox.id : '',
                cashboxName: cashbox ? cashbox.name : 'آجل',
                items,
                discount,
                netTotal,
                employee: currentUser.fullName,
                employeeRole: currentUser.role,
                notes
            };

            await db.collection('invoices').doc(invId).set(invoiceDoc);

            document.getElementById('invoiceItemsContainer').innerHTML = '';
            addInvoiceItemRow();
            document.getElementById('invDiscount').value = '0';
            if (document.getElementById('invRefNumber')) document.getElementById('invRefNumber').value = '';
            updateInvoiceStatementPreview();
            showToast('تم حفظ الفاتورة');
            openPrintModal(invoiceDoc);
        } catch (e) {
            showToast('تعذر حفظ الفاتورة');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function editInvoiceNote(invId) {
        if (!canEditRecord()) {
            showToast('ليس لديك صلاحية التعديل');
            return;
        }
        const inv = state.invoices.find(i => i.id === invId);
        if (!inv) return;
        const nextNote = prompt('تعديل بيان الفاتورة:', inv.notes || '');
        if (nextNote === null) return;
        await db.collection('invoices').doc(invId).update({ notes: nextNote.trim() });
        showToast('تم تعديل الفاتورة');
    }

    async function deleteInvoiceRecord(invId) {
        if (isBusy) return;
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        const inv = state.invoices.find(i => i.id === invId);
        if (!inv) return;
        if (!confirm(`تأكيد حذف الفاتورة (${inv.id})؟`)) return;

        isBusy = true;
        try {
            await db.collection('invoices').doc(invId).delete();
            showToast('تم حذف الفاتورة وتحديث الأرصدة');
        } catch (e) {
            showToast('تعذر حذف الفاتورة');
        } finally {
            isBusy = false;
        }
    }

    function renderInvoicesTable() {
        const q = (document.getElementById('invoiceSearchInput').value || '').toLowerCase().trim();
        const list = state.invoices
            .filter(i => (i.id || '').toLowerCase().includes(q) || (i.customerName || '').toLowerCase().includes(q))
            .slice().reverse();

        document.getElementById('invoicesTableBody').innerHTML = list.length
            ? list.map(i => {
                const itemsSummary = Array.isArray(i.items) && i.items.length
                    ? i.items.map(it => `${it.name} (${it.qty} ${it.unit || 'حبة'})`).join('، ')
                    : '-';
                return `
                    <tr>
                        <td><span class="mono">${i.id}</span></td>
                        <td>${i.branchName || 'الفرع الرئيسي'}</td>
                        <td>${i.customerName || '-'}</td>
                        <td style="max-width:200px;">${itemsSummary}</td>
                        <td>${i.notes || '-'}</td>
                        <td>${i.paymentType === 'cash' ? '<span class="badge badge-cash">نقدي</span>' : '<span class="badge badge-credit">آجل</span>'}</td>
                        <td><span class="mono">${formatMoney(i.netTotal)}</span></td>
                        <td>${i.employee || '-'}</td>
                        <td style="white-space:nowrap;">
                            <button class="btn btn-outline btn-sm" onclick="printInvoiceById('${i.id}')" title="طباعة"><i class="fa-solid fa-print"></i></button>
                            ${canEditRecord() ? `<button class="btn btn-outline btn-sm" onclick="editInvoiceNote('${i.id}')"><i class="fa-solid fa-pen"></i></button>` : ''}
                            ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deleteInvoiceRecord('${i.id}')"><i class="fa-solid fa-trash"></i></button>` : ''}
                        </td>
                    </tr>
                `;
            }).join('')
            : '<tr><td colspan="9" style="text-align:center; color:var(--text-muted);">لا توجد فواتير</td></tr>';
    }

    function toggleVoucherPartyFields() {
        const isReceipt = document.getElementById('voucherType').value === 'receipt';
        document.getElementById('voucherCustomerGroup').classList.toggle('hidden', !isReceipt);
        document.getElementById('voucherSupplierGroup').classList.toggle('hidden', isReceipt);
        updateVoucherStatementPreview();
    }

    async function createVoucher() {
        if (isBusy) return;
        const btn = document.getElementById('saveVoucherBtn');
        const type = document.getElementById('voucherType').value;
        const cashboxId = document.getElementById('voucherCashboxSelect').value;
        const customerId = type === 'receipt' ? document.getElementById('voucherCustomerSelect').value : '';
        const supplierId = type === 'payment' ? document.getElementById('voucherSupplierSelect').value : '';
        const amount = Number(document.getElementById('voucherAmount').value || 0);
        const refNum = (document.getElementById('voucherRefNumber')?.value || '').trim();
        const note = type === 'receipt' ? `لكم سند قبض برقم ${refNum || '—'}` : `عليكم سند صرف برقم ${refNum || '—'}`;

        const cashbox = state.cashboxes.find(c => c.id === cashboxId);
        if (!cashbox || amount <= 0) {
            showToast('اختر الصندوق وأدخل مبلغاً صحيحاً');
            return;
        }
        const currentCbBal = computeSystemCashboxBalance(cashbox);
        if (type === 'payment' && currentCbBal < amount) {
            showToast('رصيد الصندوق غير كافٍ');
            return;
        }

        isBusy = true;
        btn.disabled = true;

        try {
            const customer = customerId ? state.customers.find(c => c.id === customerId) : null;
            const supplier = supplierId ? state.suppliers.find(s => s.id === supplierId) : null;
            const partyName = customer ? customer.name : (supplier ? supplier.name : 'عام');

            const vchId = `VCH-${Date.now()}`;
            await db.collection('vouchers').doc(vchId).set({
                id: vchId,
                type,
                date: new Date().toISOString().split('T')[0],
                cashboxId: cashbox.id,
                cashboxName: cashbox.name,
                customerId: customer ? customer.id : '',
                customerName: customer ? customer.name : '',
                supplierId: supplier ? supplier.id : '',
                supplierName: supplier ? supplier.name : '',
                partyName,
                amount,
                note,
                employee: currentUser.fullName
            });

            document.getElementById('voucherAmount').value = '';
            if (document.getElementById('voucherRefNumber')) document.getElementById('voucherRefNumber').value = '';
            updateVoucherStatementPreview();
            showToast('تم حفظ السند');
        } catch (e) {
            showToast('تعذر حفظ السند');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function editVoucherNote(vchId) {
        if (!canEditRecord()) {
            showToast('ليس لديك صلاحية التعديل');
            return;
        }
        const v = state.vouchers.find(x => x.id === vchId);
        if (!v) return;
        const nextNote = prompt('تعديل البيان:', v.note || '');
        if (nextNote === null) return;
        await db.collection('vouchers').doc(vchId).update({ note: nextNote.trim() });
        showToast('تم تعديل السند');
    }

    async function deleteVoucherRecord(vchId) {
        if (isBusy) return;
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        const v = state.vouchers.find(x => x.id === vchId);
        if (!v) return;
        if (!confirm('تأكيد حذف السند؟')) return;

        isBusy = true;
        try {
            await db.collection('vouchers').doc(vchId).delete();
            showToast('تم حذف السند');
        } finally {
            isBusy = false;
        }
    }

    function renderVouchersTable() {
        const list = state.vouchers.slice().reverse();
        document.getElementById('vouchersTableBody').innerHTML = list.length
            ? list.map(v => `
                <tr>
                    <td>${v.type === 'receipt' ? '<span class="badge badge-cash">قبض</span>' : '<span class="badge badge-expense">صرف</span>'}</td>
                    <td>${v.cashboxName || '-'}</td>
                    <td>${v.partyName || v.customerName || v.supplierName || '-'}</td>
                    <td>${v.note || '-'}</td>
                    <td><span class="mono">${formatMoney(v.amount)}</span></td>
                    <td>${v.employee || '-'}</td>
                    <td>
                        ${canEditRecord() ? `<button class="btn btn-outline btn-sm" onclick="editVoucherNote('${v.id}')"><i class="fa-solid fa-pen"></i></button>` : ''}
                        ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deleteVoucherRecord('${v.id}')"><i class="fa-solid fa-trash"></i></button>` : ''}
                        ${(!canEditRecord() && !canDeleteRecord()) ? '<span style="color:var(--text-muted); font-size:11px;">عرض فقط</span>' : ''}
                    </td>
                </tr>
            `).join('')
            : '<tr><td colspan="7" style="text-align:center; color:var(--text-muted);">لا توجد أسناد</td></tr>';
    }

    async function createCashbox() {
        if (isBusy) return;
        const btn = document.getElementById('saveCashboxBtn');
        const name = document.getElementById('newCashboxName').value.trim();
        const opening = Number(document.getElementById('newCashboxOpening').value || 0);
        if (!name) {
            showToast('أدخل اسم الصندوق');
            return;
        }

        isBusy = true;
        btn.disabled = true;
        try {
            const id = `cb_${Date.now()}`;
            await db.collection('cashboxes').doc(id).set({
                id,
                name,
                openingBalance: opening,
                balance: opening
            });
            document.getElementById('newCashboxName').value = '';
            document.getElementById('newCashboxOpening').value = '0';
            showToast('تمت إضافة الصندوق');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function editCashboxOpening(cbId) {
        if (isBusy) return;
        if (!canEditRecord()) {
            showToast('ليس لديك صلاحية التعديل');
            return;
        }
        const cb = state.cashboxes.find(x => x.id === cbId);
        if (!cb) return;
        const currentOpen = getCashboxOpening(cb);
        const nextVal = prompt(`الرصيد الافتتاحي لـ (${cb.name}):`, currentOpen);
        if (nextVal === null) return;
        const parsed = Number(nextVal);
        if (isNaN(parsed) || parsed < 0) {
            showToast('أدخل رقماً صحيحاً');
            return;
        }
        isBusy = true;
        try {
            await db.collection('cashboxes').doc(cbId).update({
                openingBalance: parsed,
                balance: parsed
            });
            showToast('تم تحديث الرصيد الافتتاحي');
        } finally {
            isBusy = false;
        }
    }

    function renderCashboxesList() {
        const el = document.getElementById('dashboardCashboxesList');
        el.innerHTML = state.cashboxes.length
            ? state.cashboxes.map(c => {
                const opening = getCashboxOpening(c);
                const sysBal = computeSystemCashboxBalance(c);
                return `
                    <div style="background:#fff; border:1px solid var(--border); border-radius:12px; padding:10px 12px; display:flex; justify-content:space-between; align-items:center; gap:8px; margin-bottom:8px;">
                        <div>
                            <strong>${c.name}</strong>
                            <div style="font-size:11px; color:var(--text-muted);">رصيد افتتاحي: <span class="mono">${formatMoney(opening)}</span></div>
                        </div>
                        <div style="display:flex; align-items:center; gap:8px;">
                            <span class="mono" style="color:var(--success); font-size:15px;">${formatMoney(sysBal)}</span>
                            ${canEditRecord() ? `<button type="button" class="btn btn-outline btn-sm" onclick="editCashboxOpening('${c.id}')" title="تعديل الرصيد الافتتاحي"><i class="fa-solid fa-pen"></i></button>` : ''}
                        </div>
                    </div>
                `;
            }).join('')
            : '<p style="color:var(--text-muted); font-size:13px;">لا توجد صناديق</p>';
    }

    async function createBranch() {
        if (isBusy) return;
        const btn = document.getElementById('saveBranchBtn');
        const name = document.getElementById('newBranchName').value.trim();
        if (!name) {
            showToast('أدخل اسم الفرع');
            return;
        }
        isBusy = true;
        btn.disabled = true;
        try {
            const id = `br_${Date.now()}`;
            await db.collection('branches').doc(id).set({ id, name });
            document.getElementById('newBranchName').value = '';
            showToast('تمت إضافة الفرع');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function saveWarehouseItem() {
        if (isBusy) return;
        const btn = document.getElementById('saveWarehouseItemBtn');
        const branchId = document.getElementById('whItemBranchSelect').value || 'main_branch';
        const branchObj = state.branches.find(b => b.id === branchId);
        const branchName = branchObj ? branchObj.name : 'الفرع الرئيسي';

        const name = document.getElementById('newItemName').value.trim();
        const unit = document.getElementById('newItemUnit').value || 'حبة';
        const qty = Number(document.getElementById('newItemQty').value || 0);
        const price = Number(document.getElementById('newItemPrice').value || 0);
        if (!name) {
            showToast('أدخل اسم الصنف');
            return;
        }

        isBusy = true;
        btn.disabled = true;
        try {
            const existing = state.warehouse.find(
                w => (w.branchId || 'main_branch') === branchId &&
                     w.name.toLowerCase() === name.toLowerCase() &&
                     (w.unit || 'حبة') === unit
            );
            if (existing) {
                if (!canEditRecord()) {
                    showToast('ليس لديك صلاحية التعديل على المخزون');
                    return;
                }
                await db.collection('warehouse').doc(existing.id).update({ qty, price, unit, branchId, branchName });
            } else {
                const id = `wh_${Date.now()}`;
                await db.collection('warehouse').doc(id).set({ id, branchId, branchName, name, unit, qty, price });
            }
            document.getElementById('newItemName').value = '';
            document.getElementById('newItemQty').value = '1';
            document.getElementById('newItemPrice').value = '0';
            showToast('تم حفظ الصنف في المخزن');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function editWarehouseItem(itemId) {
        if (!canEditRecord()) {
            showToast('ليس لديك صلاحية التعديل');
            return;
        }
        const item = state.warehouse.find(w => w.id === itemId);
        if (!item) return;
        const nextQty = prompt(`تعديل كمية (${item.name} - ${item.unit || 'حبة'}):`, item.qty);
        if (nextQty === null) return;
        const nextPrice = prompt(`تعديل سعر (${item.name}):`, item.price);
        if (nextPrice === null) return;
        await db.collection('warehouse').doc(itemId).update({
            qty: Number(nextQty || 0),
            price: Number(nextPrice || 0)
        });
        showToast('تم تعديل الصنف');
    }

    async function deleteWarehouseItem(itemId) {
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        if (!confirm('تأكيد حذف الصنف من المخزون؟')) return;
        await db.collection('warehouse').doc(itemId).delete();
        showToast('تم حذف الصنف');
    }

    function renderWarehouseTable() {
        const tbody = document.getElementById('warehouseTableBody');
        const selectedBranch = document.getElementById('activeBranchFilter').value || 'ALL';
        const filtered = selectedBranch === 'ALL'
            ? state.warehouse
            : state.warehouse.filter(w => (w.branchId || 'main_branch') === selectedBranch);

        tbody.innerHTML = filtered.length
            ? filtered.map(w => {
                const q = Number(w.qty || 0);
                const p = Number(w.price || 0);
                return `
                    <tr>
                        <td>${w.branchName || 'الفرع الرئيسي'}</td>
                        <td><strong>${w.name}</strong></td>
                        <td><span class="badge badge-unit">${w.unit || 'حبة'}</span></td>
                        <td><span class="badge ${q > 0 ? 'badge-cash' : 'badge-expense'} mono">${q}</span></td>
                        <td><span class="mono">${formatMoney(p)}</span></td>
                        <td><span class="mono">${formatMoney(q * p)}</span></td>
                        <td>
                            ${canEditRecord() ? `<button class="btn btn-outline btn-sm" onclick="editWarehouseItem('${w.id}')"><i class="fa-solid fa-pen"></i></button>` : ''}
                            ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deleteWarehouseItem('${w.id}')"><i class="fa-solid fa-trash"></i></button>` : ''}
                            ${(!canEditRecord() && !canDeleteRecord()) ? '<span style="color:var(--text-muted); font-size:11px;">عرض فقط</span>' : ''}
                        </td>
                    </tr>
                `;
            }).join('')
            : '<tr><td colspan="7" style="text-align:center; color:var(--text-muted);">لا توجد أصناف في هذا الفرع</td></tr>';
    }

    async function createCustomer() {
        if (isBusy) return;
        const btn = document.getElementById('saveCustomerBtn');
        const name = document.getElementById('newCustomerName').value.trim();
        const phone = document.getElementById('newCustomerPhone').value.trim();
        const creditLimit = Number(document.getElementById('newCustomerLimit').value || 0);
        if (!name) {
            showToast('أدخل اسم العميل');
            return;
        }

        isBusy = true;
        btn.disabled = true;
        try {
            const id = `cust_${Date.now()}`;
            await db.collection('customers').doc(id).set({ id, name, phone: phone || '-', creditLimit, balance: 0 });
            document.getElementById('newCustomerName').value = '';
            document.getElementById('newCustomerPhone').value = '';
            showToast('تم حفظ العميل');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    function openCustomerStatement(custId) {
        const cust = state.customers.find(c => c.id === custId);
        if (!cust) return;
        activeStatementCustomer = cust;

        document.getElementById('stCustName').textContent = cust.name || '-';
        document.getElementById('stCustPhone').textContent = cust.phone || '-';
        document.getElementById('stDate').textContent = new Date().toISOString().split('T')[0];

        const matchesCust = (rec) =>
            (cust.id && rec.customerId === cust.id) ||
            (!rec.customerId && rec.customerName && cust.name && rec.customerName.trim() === cust.name.trim());

        const events = [];
        state.invoices
            .filter(i => i.paymentType === 'credit' && matchesCust(i))
            .forEach(i => {
                events.push({
                    date: i.date || '',
                    sortKey: i.id || '',
                    desc: i.notes || `عليكم فاتورة مبيعات برقم ${i.id}`,
                    debit: Number(i.netTotal || 0),
                    credit: 0
                });
            });

        state.vouchers
            .filter(v => v.type === 'receipt' && matchesCust(v))
            .forEach(v => {
                events.push({
                    date: v.date || '',
                    sortKey: v.id || '',
                    desc: v.note || `لكم سند قبض برقم ${v.id}`,
                    debit: 0,
                    credit: Number(v.amount || 0)
                });
            });

        events.sort((a, b) => String(a.date).localeCompare(String(b.date)) || String(a.sortKey).localeCompare(String(b.sortKey)));

        let running = 0;
        let totalDebit = 0;
        let totalCredit = 0;

        const rowsHtml = events.length
            ? events.map(ev => {
                totalDebit += ev.debit;
                totalCredit += ev.credit;
                running += ev.debit - ev.credit;
                return `
                    <tr>
                        <td><span class="mono">${ev.date || '-'}</span></td>
                        <td>${ev.desc}</td>
                        <td>${ev.debit > 0 ? `<span class="mono" style="color:var(--warning);">${formatMoney(ev.debit)}</span>` : '<span style="color:var(--text-muted);">-</span>'}</td>
                        <td>${ev.credit > 0 ? `<span class="mono" style="color:var(--success);">${formatMoney(ev.credit)}</span>` : '<span style="color:var(--text-muted);">-</span>'}</td>
                        <td><span class="mono">${formatMoney(running)}</span></td>
                    </tr>
                `;
            }).join('')
            : '<tr><td colspan="5" style="text-align:center; color:var(--text-muted);">لا توجد حركات آجلة أو سندات لهذا العميل</td></tr>';

        document.getElementById('stTransactionsBody').innerHTML = rowsHtml;
        document.getElementById('stTotalInvoices').textContent = formatMoney(totalDebit);
        document.getElementById('stTotalReceipts').textContent = formatMoney(totalCredit);
        document.getElementById('stBalanceDue').textContent = formatMoney(Math.max(0, totalDebit - totalCredit));

        document.getElementById('customerStatementModal').classList.remove('hidden');
    }

    function closeCustomerStatementModal() {
        document.getElementById('customerStatementModal').classList.add('hidden');
        activeStatementCustomer = null;
    }

    function downloadCustomerStatementPDF() {
        const el = document.getElementById('customerStatementExportArea');
        if (!el || typeof html2pdf === 'undefined') {
            window.print();
            return;
        }
        const custLabel = (activeStatementCustomer?.name || 'customer').replace(/\s+/g, '_');
        html2pdf().set({
            margin: 8,
            filename: `statement_${custLabel}.pdf`,
            image: { type: 'jpeg', quality: 0.96 },
            html2canvas: { scale: 2, useCORS: true },
            jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
        }).from(el).save();
    }

    async function editCustomerItem(custId) {
        if (!canEditRecord()) {
            showToast('ليس لديك صلاحية التعديل');
            return;
        }
        const c = state.customers.find(x => x.id === custId);
        if (!c) return;
        const nextName = prompt('تعديل اسم العميل:', c.name);
        if (nextName === null || !nextName.trim()) return;
        const nextPhone = prompt('تعديل رقم الهاتف:', c.phone || '');
        if (nextPhone === null) return;
        await db.collection('customers').doc(custId).update({
            name: nextName.trim(),
            phone: nextPhone.trim() || '-'
        });
        showToast('تم تعديل العميل');
    }

    async function deleteCustomerItem(custId) {
        if (!canDeleteRecord()) {
            showToast('ليس لديك صلاحية الحذف');
            return;
        }
        if (!confirm('تأكيد حذف العميل؟')) return;
        await db.collection('customers').doc(custId).delete();
        showToast('تم حذف العميل');
    }

    function renderCustomersTable() {
        const tbody = document.getElementById('customersTableBody');
        tbody.innerHTML = state.customers.length
            ? state.customers.map(c => {
                const sysBal = computeSystemCustomerBalance(c);
                return `
                    <tr>
                        <td><strong>${c.name}</strong></td>
                        <td>${c.phone || '-'}</td>
                        <td><span class="mono" style="color:${sysBal > 0 ? 'var(--warning)' : 'var(--success)'};">${formatMoney(sysBal)}</span></td>
                        <td style="white-space:nowrap;">
                            <button class="btn btn-outline btn-sm" onclick="openCustomerStatement('${c.id}')" title="كشف حساب"><i class="fa-solid fa-file-lines"></i> كشف</button>
                            ${canEditRecord() ? `<button class="btn btn-outline btn-sm" onclick="editCustomerItem('${c.id}')"><i class="fa-solid fa-pen"></i></button>` : ''}
                            ${canDeleteRecord() ? `<button class="btn btn-danger btn-sm" onclick="deleteCustomerItem('${c.id}')"><i class="fa-solid fa-trash"></i></button>` : ''}
                        </td>
                    </tr>
                `;
            }).join('')
            : '<tr><td colspan="4" style="text-align:center; color:var(--text-muted);">لا يوجد عملاء</td></tr>';
    }

    async function createEmployee() {
        if (isBusy) return;
        const btn = document.getElementById('saveEmployeeBtn');
        const fullName = document.getElementById('newEmpFullName').value.trim();
        const username = document.getElementById('newEmpUsername').value.trim();
        const password = document.getElementById('newEmpPassword').value.trim();
        const role = document.getElementById('newEmpRole').value;
        const isFull = role === 'admin' || role === 'supervisor';
        const canEdit = isFull ? true : document.getElementById('newEmpCanEdit').checked;
        const canDelete = isFull ? true : document.getElementById('newEmpCanDelete').checked;

        if (!fullName || !username || !password) {
            showToast('أدخل جميع بيانات الحساب');
            return;
        }

        isBusy = true;
        btn.disabled = true;

        try {
            if (state.employees.some(e => String(e.username).trim() === username)) {
                showToast('اسم الدخول موجود مسبقاً');
                return;
            }
            const id = `emp_${Date.now()}`;
            await db.collection('employees').doc(id).set({
                id,
                fullName,
                username,
                password,
                role,
                canEdit,
                canDelete,
                active: true
            });
            document.getElementById('newEmpFullName').value = '';
            document.getElementById('newEmpUsername').value = '';
            document.getElementById('newEmpPassword').value = '';
            document.getElementById('newEmpCanEdit').checked = false;
            document.getElementById('newEmpCanDelete').checked = false;
            showToast('تم حفظ الحساب');
        } finally {
            isBusy = false;
            btn.disabled = false;
        }
    }

    async function toggleEmployeePerm(empId, field) {
        if (isBusy || !canManageUsers()) return;
        const emp = state.employees.find(e => e.id === empId);
        if (!emp || emp.role === 'admin' || emp.role === 'supervisor') return;
        isBusy = true;
        try {
            await db.collection('employees').doc(empId).update({ [field]: !Boolean(emp[field]) });
            showToast('تم تحديث الصلاحية');
        } finally {
            isBusy = false;
        }
    }

    async function toggleEmployeeStatus(empId) {
        if (isBusy || !canManageUsers()) return;
        const emp = state.employees.find(e => e.id === empId);
        if (!emp) return;
        isBusy = true;
        try {
            await db.collection('employees').doc(empId).update({ active: !emp.active });
            showToast('تم تحديث الحالة');
        } finally {
            isBusy = false;
        }
    }

    async function deleteEmployeeAccount(empId) {
        if (isBusy) return;
        if (!canManageUsers()) {
            showToast('صلاحية حذف المستخدمين للمشرف العام والمدير فقط');
            return;
        }
        const emp = state.employees.find(e => e.id === empId);
        if (!emp) return;
        if (emp.id === 'emp_admin' || emp.username === ADMIN_USER) {
            showToast('لا يمكن حذف حساب المدير العام الأساسي');
            return;
        }
        if (currentUser && emp.id === currentUser.id) {
            showToast('لا يمكنك حذف حسابك الحالي أثناء الدخول');
            return;
        }
        if (!confirm(`هل أنت متأكد من حذف المستخدم (${emp.fullName})؟`)) return;

        isBusy = true;
        try {
            await db.collection('employees').doc(empId).delete();
            showToast('تم حذف المستخدم');
        } catch (e) {
            showToast('تعذر حذف المستخدم');
        } finally {
            isBusy = false;
        }
    }

    function renderEmployeesTable() {
        const tbody = document.getElementById('employeesTableBody');
        const allowDeleteUsers = canManageUsers();
        tbody.innerHTML = state.employees.map(emp => {
            const full = emp.role === 'admin' || emp.role === 'supervisor';
            const isProtectedAdmin = emp.id === 'emp_admin' || emp.username === ADMIN_USER;
            const permsHtml = full
                ? '<span class="badge badge-sup">تعديل + حذف (كامل)</span>'
                : `
                    <button class="btn ${emp.canEdit ? 'btn-success' : 'btn-outline'} btn-sm" onclick="toggleEmployeePerm('${emp.id}', 'canEdit')">
                        ${emp.canEdit ? 'تعديل ✓' : 'تعديل ✕'}
                    </button>
                    <button class="btn ${emp.canDelete ? 'btn-danger' : 'btn-outline'} btn-sm" onclick="toggleEmployeePerm('${emp.id}', 'canDelete')">
                        ${emp.canDelete ? 'حذف ✓' : 'حذف ✕'}
                    </button>
                  `;
            const deleteBtnHtml = (allowDeleteUsers && !isProtectedAdmin)
                ? `<button class="btn btn-danger btn-sm" onclick="deleteEmployeeAccount('${emp.id}')" title="حذف المستخدم"><i class="fa-solid fa-trash"></i></button>`
                : '';
            return `
                <tr>
                    <td><strong>${emp.fullName}</strong></td>
                    <td><span class="mono">${emp.username}</span></td>
                    <td><span class="badge ${roleBadgeClass(emp.role)}">${roleLabel(emp.role)}</span></td>
                    <td>${permsHtml}</td>
                    <td>${emp.active ? '<span class="badge badge-cash">نشط</span>' : '<span class="badge badge-expense">موقوف</span>'}</td>
                    <td style="white-space:nowrap;">
                        <button class="btn ${emp.active ? 'btn-warning' : 'btn-success'} btn-sm" onclick="toggleEmployeeStatus('${emp.id}')">
                            ${emp.active ? 'إيقاف' : 'تفعيل'}
                        </button>
                        ${deleteBtnHtml}
                    </td>
                </tr>
            `;
        }).join('');
    }

    togglePurchaseCashboxField();
    toggleVoucherPartyFields();
</script>
</body>
</html>
