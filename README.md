<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مركز آراي التعليمي - النظام المتكامل والمالي</title>
    <!-- استدعاء أيقونات Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- استدعاء خط Cairo المميز -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&display=swap" rel="stylesheet">
    
    <!-- مكتبات توليد وقراءة الـ QR Code المدمجة للنظام الجديد -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://unpkg.com/html5-qrcode"></script>

    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #f5f7fa 0%, #e4e8f0 100%);
            --text-main: #2d3748;
            --text-muted: #718096;
            --card-bg: #ffffff;
            
            --color-student: linear-gradient(135deg, #00b4db 0%, #0083b0 100%);
            --color-parent: linear-gradient(135deg, #4e54c8 0%, #8f94fb 100%);
            --color-admin: linear-gradient(135deg, #8a2387 0%, #e94057 100%);
            --color-teacher: linear-gradient(135deg, #f12711 0%, #f5af19 100%);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Cairo', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: var(--bg-gradient);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            color: var(--text-main);
            overflow-x: hidden;
        }

        /* حاوية الصفحات */
        .page {
            width: 100%;
            max-width: 420px;
            display: none;
            animation: fadeIn 0.3s ease-in-out;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* الهيدر العام */
        .header-section {
            text-align: center;
            margin-top: 10px;
            margin-bottom: 25px;
        }

        .logo-container {
            width: 85px;
            height: 85px;
            background: #ffffff;
            border-radius: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto 15px auto;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
        }

        .logo-placeholder {
            display: flex;
            flex-direction: column;
            align-items: center;
            font-weight: 800;
            font-size: 14px;
            color: #4e54c8;
        }

        .welcome-msg {
            font-size: 22px;
            font-weight: 700;
            color: #2d3748;
        }

        .subtitle {
            font-size: 15px;
            color: var(--text-muted);
            font-weight: 600;
            margin-top: 4px;
        }

        /* قائمة الكروت الرئيسية */
        .cards-container {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .role-card {
            background: var(--card-bg);
            border-radius: 22px;
            padding: 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.8);
            cursor: pointer;
        }

        .role-card:active { transform: scale(0.98); background: #fafafa; }
        .arrow-icon { color: #a0aec0; font-size: 16px; }
        .card-details { flex-grow: 1; text-align: right; padding-right: 18px; }
        .card-title { font-size: 18px; font-weight: 700; color: #1a202c; }
        .card-desc { font-size: 13px; color: var(--text-muted); line-height: 1.4; }
        .icon-box { width: 56px; height: 56px; border-radius: 16px; display: flex; justify-content: center; align-items: center; color: #ffffff; font-size: 22px; box-shadow: 0 8px 15px rgba(0, 0, 0, 0.08); }

        .student-bg { background: var(--color-student); }
        .parent-bg { background: var(--color-parent); }
        .admin-bg { background: var(--color-admin); }
        .teacher-bg { background: var(--color-teacher); }

        /* تدوين واجهات الدخول واللوحات */
        .login-box, .dashboard-box {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 24px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.04);
            border: 1px solid rgba(255, 255, 255, 0.9);
            margin-bottom: 20px;
        }

        .login-box-title, .box-title {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .input-group { margin-bottom: 16px; text-align: right; }
        .input-group label { display: block; font-size: 14px; font-weight: 600; margin-bottom: 6px; color: #4a5568; }
        .input-wrapper { position: relative; display: flex; align-items: center; }
        .input-wrapper i { position: absolute; right: 14px; color: #a0aec0; font-size: 16px; z-index: 2; }
        .input-wrapper input, .input-wrapper select { width: 100%; padding: 12px 42px 12px 14px; border: 1.5px solid #e2e8f0; border-radius: 14px; font-size: 15px; outline: none; background: #f7fafc; appearance: none; position: relative; }
        .input-wrapper input:focus, .input-wrapper select:focus { border-color: #8a2387; background: #ffffff; box-shadow: 0 0 0 3px rgba(138, 35, 135, 0.1); }
        
        #studentPage .input-wrapper input:focus { border-color: #0083b0; box-shadow: 0 0 0 3px rgba(0, 131, 176, 0.1); }
        #teacherPage .input-wrapper input:focus { border-color: #f12711; box-shadow: 0 0 0 3px rgba(241, 39, 17, 0.1); }
        #parentPage .input-wrapper input:focus { border-color: #4e54c8; box-shadow: 0 0 0 3px rgba(78, 84, 200, 0.1); }

        /* حاوية الأيام متعددة الاختيارات */
        .days-selector {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 6px;
            background: #f7fafc;
            padding: 8px;
            border: 1.5px solid #e2e8f0;
            border-radius: 14px;
        }
        .day-checkbox {
            display: none;
        }
        .day-label {
            display: block;
            text-align: center;
            padding: 6px 0;
            background: #fff;
            border: 1px solid #cbd5e0;
            border-radius: 8px;
            font-size: 12px;
            font-weight: 700;
            cursor: pointer;
            color: var(--text-muted);
        }
        .day-checkbox:checked + .day-label {
            background: #0d9488;
            color: #fff;
            border-color: #0d9488;
        }

        .btn-login { width: 100%; padding: 14px; border: none; border-radius: 14px; color: white; font-size: 16px; font-weight: 700; cursor: pointer; box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1); margin-top: 10px; }
        .btn-login:active { transform: scale(0.98); }
        .btn-back { display: flex; align-items: center; justify-content: center; gap: 8px; width: 100%; padding: 12px; background: transparent; border: 1.5px dashed #cbd5e0; border-radius: 14px; color: var(--text-muted); font-size: 14px; font-weight: 600; cursor: pointer; }

        /* واجهة لوحة تحكم الإدارة السريعة والإحصائيات */
        .admin-profile, .user-profile-header {
            display: flex;
            align-items: center;
            gap: 12px;
            background: #f7fafc;
            padding: 12px;
            border-radius: 16px;
            margin-bottom: 20px;
            border: 1px solid #edf2f7;
        }
        .admin-avatar, .user-avatar { width: 45px; height: 45px; border-radius: 12px; display: flex; justify-content: center; align-items: center; color: white; font-size: 20px; }
        .admin-avatar { background: var(--color-admin); }
        .admin-info, .user-info { text-align: right; }
        .admin-info p, .user-info p { font-size: 14px; font-weight: 700; }
        .admin-info span, .user-info span { font-size: 11px; color: var(--text-muted); }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }
        .stat-item { background: #f7fafc; padding: 10px; border-radius: 14px; text-align: center; border: 1px solid #edf2f7; }
        .stat-item span { font-size: 11px; color: var(--text-muted); font-weight: 600; }
        .stat-item p { font-size: 18px; font-weight: 800; color: #1a202c; }

        /* الأقسام الفرعية التبويبية لحسابات المدير */
        .accounts-tabs {
            display: flex;
            gap: 4px;
            margin-top: 15px;
            margin-bottom: 10px;
            flex-wrap: wrap;
        }
        .tab-btn {
            flex: 1;
            min-width: 80px;
            padding: 8px 4px;
            border: 1px solid #e2e8f0;
            background: #f8fafc;
            border-radius: 10px;
            font-size: 11px;
            font-weight: 700;
            cursor: pointer;
            color: var(--text-muted);
        }
        .tab-btn.active {
            background: #8a2387;
            color: white;
            border-color: #8a2387;
        }

        /* الحسابات الموزعة */
        .users-list {
            margin-top: 5px;
            max-height: 250px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 10px;
            padding-left: 5px;
        }
        .user-badge {
            display: flex;
            flex-direction: column;
            align-items: stretch;
            gap: 8px;
            padding: 12px;
            background: #f7fafc;
            border-radius: 12px;
            border-right: 4px solid #cbd5e0;
            font-size: 13px;
        }
        .badge-student { border-right-color: #0083b0; }
        .badge-teacher { border-right-color: #f12711; }
        .badge-parent { border-right-color: #4e54c8; }

        .user-badge-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .user-badge-info { text-align: right; }
        .user-badge-info p { font-weight: 700; font-size: 13px; }
        .user-badge-info span { font-size: 11px; color: var(--text-muted); display: block; line-height: 1.4; }
        .user-badge-meta { font-family: monospace; font-weight: 700; color: #4a5568; font-size: 11px; background: #e2e8f0; padding: 2px 6px; border-radius: 6px; }

        /* تصميم Bento Grid للمنهج العراقي في لوحة الطالب */
        .bento-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-bottom: 15px;
        }

        .bento-item {
            background: #ffffff;
            border: 1px solid #e2e8f0;
            border-radius: 18px;
            padding: 16px;
            text-align: right;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            gap: 12px;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.01);
        }

        .bento-item:active { transform: scale(0.96); background: #fcfcfc; }

        .bento-item.featured {
            grid-column: span 2;
            flex-direction: row;
            align-items: center;
            background: linear-gradient(135deg, #ffffff 60%, #f0fdf4 100%);
            border-color: #bbf7d0;
        }

        .subject-icon-wrapper {
            width: 44px;
            height: 44px;
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            color: white;
        }

        .subject-meta h3 { font-size: 15px; font-weight: 700; color: #1a202c; margin-bottom: 2px; }
        .subject-meta p { font-size: 11px; color: var(--text-muted); font-weight: 600; margin-top: 2px; }
        .subject-arrow { font-size: 12px; color: #cbd5e0; align-self: flex-end; }
        .featured .subject-arrow { align-self: center; }

        /* ألوان أيقونات المواد المعتمدة السبعة */
        .bg-islamic { background: #10b981; }
        .bg-arabic { background: #f59e0b; }
        .bg-english { background: #3b82f6; }
        .bg-math { background: #ef4444; }
        .bg-chemistry { background: #8b5cf6; }
        .bg-physics { background: #06b6d4; }
        .bg-biology { background: #ec4899; }

        /* مساحة عرض المحتوى والمحاضرات الديناميكية */
        .content-viewer-box {
            background: #f7fafc;
            border: 1px dashed #cbd5e0;
            border-radius: 16px;
            padding: 14px;
            margin-top: 15px;
            max-height: 260px;
            overflow-y: auto;
        }
        .lecture-card-item {
            background: white;
            padding: 12px;
            border-radius: 12px;
            box-shadow: 0 2px 6px rgba(0,0,0,0.02);
            border: 1px solid #e2e8f0;
            margin-bottom: 10px;
            text-align: right;
        }
        .lecture-card-item h4 { font-size: 14px; font-weight: 700; color: #2d3748; margin-bottom: 4px;}
        .lecture-card-item p { font-size: 12px; color: var(--text-muted); margin-bottom: 6px; }
        .lecture-links { display: flex; gap: 8px; flex-wrap: wrap; }
        .lecture-links a { font-size: 11px; text-decoration: none; padding: 6px 10px; border-radius: 8px; font-weight: bold; color: white; display: inline-flex; align-items: center; gap: 4px; }
        .link-vid { background: #ef4444; }
        .link-pdf { background: #3b82f6; }
        .link-exam { background: #10b981; }

        /* قسم التنبيهات */
        .alert-box {
            background: #f0fdf4;
            border: 1.5px solid #bbf7d0;
            border-radius: 16px;
            padding: 12px;
            margin-bottom: 15px;
            animation: fadeIn 0.4s ease-in-out;
            text-align: right;
        }
        .alert-box h4 { font-size: 13px; color: #166534; font-weight: 700; display: flex; align-items: center; gap: 6px; }
        .alert-box p { font-size: 11px; color: #1f2937; margin-top: 4px; font-weight: 600; }
        .alert-scroll { max-height: 120px; overflow-y: auto; display: flex; flex-direction: column; gap: 6px; margin-top: 6px; }
        .alert-item-node { background: #ffffff; padding: 6px 10px; border-radius: 8px; border-right: 3px solid #0d9488; font-size: 11px; }

        .footer-section { text-align: center; font-size: 12px; color: var(--text-muted); font-weight: 600; margin-top: auto; padding-top: 20px; }

        /* نظام الإشعارات المنبثقة */
        #toast-container {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 9999;
            width: calc(100% - 40px);
            max-width: 380px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            pointer-events: none;
        }
        .toast-notification {
            background: #2d3748;
            color: #ffffff;
            padding: 14px 20px;
            border-radius: 14px;
            font-size: 14px;
            font-weight: 600;
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
            display: flex;
            align-items: center;
            gap: 10px;
            text-align: right;
            direction: rtl;
            animation: slideUpToast 0.3s ease-out forwards;
        }
        @keyframes slideUpToast {
            from { opacity: 0; transform: translateY(40px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .toast-success { background: linear-gradient(135deg, #10b981 0%, #059669 100%); }
        .toast-error { background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%); }
        .toast-info { background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%); }

        /* حاوية المحفظة والجدول الدراسي البنتو */
        .finance-card, .schedule-card {
            background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);
            border: 1px solid #e2e8f0;
            border-radius: 18px;
            padding: 14px;
            margin-bottom: 15px;
            text-align: right;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.02);
        }
        .finance-title, .schedule-title {
            font-size: 13px;
            font-weight: 700;
            color: #4a5568;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .course-loop-container {
            display: flex;
            flex-direction: column;
            gap: 10px;
            max-height: 180px;
            overflow-y: auto;
        }
        .course-loop-item {
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            padding: 10px;
            border-radius: 12px;
        }
        .schedule-row {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
        }
        .schedule-box-item {
            padding: 8px;
            border-radius: 10px;
            text-align: center;
            font-size: 11px;
            font-weight: 700;
        }
        .finance-box-item {
            padding: 8px;
            border-radius: 10px;
            text-align: center;
            font-size: 11px;
            font-weight: 700;
        }
        .fin-total { background: #edf2f7; color: #2d3748; }
        .fin-paid { background: #e6fffa; color: #047481; }
        .fin-due { background: #fff5f5; color: #c53030; }
        .finance-box-item p, .schedule-box-item p {
            font-size: 12px;
            margin-top: 2px;
            font-weight: 800;
        }

        /* تنسيقات جدول المدرس والتقارير */
        .finance-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
            font-size: 11px;
            text-align: center;
        }
        .finance-table th {
            background: #8a2387;
            color: white;
            padding: 6px;
            font-weight: 700;
        }
        .finance-table td {
            border: 1px solid #e2e8f0;
            padding: 6px;
            background: white;
            font-weight: 600;
        }
        .btn-pdf-receipt, .btn-print-action {
            background: #0284c7;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 10px;
            font-size: 12px;
            font-weight: 700;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 4px;
            margin-top: 10px;
            width: 100%;
            justify-content: center;
        }
        .btn-print-action.danger-btn {
            background: #ef4444;
        }

        /* عناصر إضافية للـ QR وقارئ الكود */
        .qr-wrapper {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 12px;
            background: #f8fafc;
            border: 1px dashed #cbd5e0;
            border-radius: 14px;
            margin-top: 10px;
        }
        #reader {
            width: 100%;
            background: #000;
            border-radius: 14px;
            overflow: hidden;
        }

        /* تصميم نسخة الطباعة الورقية A4 الصارمة جداً */
        @media print {
            body {
                background: #ffffff !important;
                color: #000000 !important;
                padding: 0 !important;
            }
            .page {
                display: none !important;
            }
            #printPageTemplate {
                display: block !important;
                width: 210mm;
                min-height: 297mm;
                padding: 20mm;
                margin: 0 auto;
                background: #ffffff !important;
                direction: rtl !important;
            }
            #toast-container, .footer-section, .btn-print-action {
                display: none !important;
            }
        }
        
        #printPageTemplate {
            display: none;
        }
    </style>
</head>
<body>

    <!-- 1. الصفحة الرئيسية -->
    <div id="mainPage" class="page active">
        <div class="header-section">
            <div class="logo-container">
                <div class="logo-placeholder">
                    <span style="font-size: 28px; margin-bottom:2px;">📖</span>
                    <span>آراي</span>
                </div>
            </div>
            <div class="welcome-msg">مرحباً بك في مركز آراي</div>
            <div class="subtitle">اختر نوع حسابك للمتابعة</div>
        </div>

        <div class="cards-container">
            <div class="role-card" onclick="navigateTo('studentPage')">
                <div class="arrow-icon"><i class="fa-solid fa-arrow-left"></i></div>
                <div class="card-details">
                    <div class="card-title">طالب</div>
                    <div class="card-desc">عرض دوراتك وجلساتك وسجل حضورك الدراسي والمالي</div>
                </div>
                <div class="icon-box student-bg"><i class="fa-solid fa-user-graduate"></i></div>
            </div>

            <div class="role-card" onclick="navigateTo('parentPage')">
                <div class="arrow-icon"><i class="fa-solid fa-arrow-left"></i></div>
                <div class="card-details">
                    <div class="card-title">ولي الأمر</div>
                    <div class="card-desc">تابع ابنك ودوراته وحضوره في المعهد أولاً بأول</div>
                </div>
                <div class="icon-box parent-bg"><i class="fa-solid fa-users"></i></div>
            </div>

            <div class="role-card" onclick="navigateTo('adminPage')">
                <div class="arrow-icon"><i class="fa-solid fa-arrow-left"></i></div>
                <div class="card-details">
                    <div class="card-title">المعهد / المدير</div>
                    <div class="card-desc">أدر معهدك ودوراته ومدربيه وطلابك وأقساطهم المالية</div>
                </div>
                <div class="icon-box admin-bg"><i class="fa-solid fa-bolt"></i></div>
            </div>

            <div class="role-card" onclick="navigateTo('teacherPage')">
                <div class="arrow-icon"><i class="fa-solid fa-arrow-left"></i></div>
                <div class="card-details">
                    <div class="card-title">مدرب / مدرس</div>
                    <div class="card-desc">أدر دوراتك وجلساتك وسجل حضور الطلاب والمالية</div>
                </div>
                <div class="icon-box teacher-bg"><i class="fa-solid fa-book-open"></i></div>
            </div>
        </div>
    </div>


    <!-- 2. واجهة دخول المدير -->
    <div id="adminPage" class="page">
        <div class="login-box">
            <div class="login-box-title" style="color: #8a2387;">
                <i class="fa-solid fa-bolt"></i> بوابة الإدارة الآمنة
            </div>
            <div class="input-group">
                <label>البريد الإلكتروني المعتمد للمدير</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-envelope"></i>
                    <input type="email" id="adminEmail" placeholder="manager@arai.com" value="arai.manager@gmail.com">
                </div>
            </div>
            <div class="input-group">
                <label>رقم الحساب السري (رقم الحفظ)</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-key"></i>
                    <input type="password" id="adminKey" placeholder="أدخل رقم الحساب" value="123456">
                </div>
            </div>
            <button class="btn-login admin-bg" onclick="verifyAdminLogin()">دخول لوحة التحكم</button>
        </div>
        <button class="btn-back" onclick="navigateTo('mainPage')"><i class="fa-solid fa-arrow-right"></i> العودة للقائمة</button>
    </div>


    <!-- 3. لوحة تحكم المدير المتكاملة مع التقارير والمصاريف والحضور -->
    <div id="adminDashboard" class="page">
        <div class="dashboard-box">
            <div class="admin-profile">
                <div class="admin-avatar"><i class="fa-solid fa-user-gear"></i></div>
                <div class="admin-info">
                    <p>مدير مركز آراي التعليمي</p>
                    <span id="displayAdminEmail"></span>
                </div>
            </div>

            <div class="stats-grid">
                <div class="stat-item"><span>طلاب</span><p id="countStudents">0</p></div>
                <div class="stat-item"><span>مدرسين</span><p id="countTeachers">0</p></div>
                <div class="stat-item"><span>أولياء أمور</span><p id="countParents">0</p></div>
            </div>

            <!-- 💰 قسم إدارة المصاريف للمركز -->
            <div style="background: #fff5f5; border: 1px solid #feb2b2; padding: 12px; border-radius: 14px; margin-bottom: 16px;">
                <div style="font-size: 13px; font-weight: 700; color: #c53030; margin-bottom: 8px;">
                    <i class="fa-solid fa-wallet"></i> إضافة مصروفات تشغيلية للمركز
                </div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 11px;">بيان المصروف (السبب)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-file-invoice-dollar"></i>
                        <input type="text" id="expenseTitle" placeholder="مثال: أجور كهرباء، قرطاسية">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 11px;">المبلغ المصروف (د.ع)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-money-bill-wave"></i>
                        <input type="number" id="expenseAmount" placeholder="0">
                    </div>
                </div>
                <button class="btn-login" style="background: #e53e3e; padding: 8px; font-size: 12px;" onclick="addExpenseItem()">تسجيل المصروف فوراً</button>
            </div>

            <div class="box-title" style="font-size: 16px; color:#8a2387; margin-bottom:12px;">
                <i class="fa-solid fa-user-plus"></i> توليد وتوزيع حساب جديد
            </div>

            <div class="input-group">
                <label>نوع الحساب المستهدف</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-address-book"></i>
                    <select id="newUserType" onchange="toggleSpecialtyField()">
                        <option value="student">طالب جديد / إضافة لدورة</option>
                        <option value="teacher">مدرب / مدرس جديد</option>
                        <option value="parent">ولي أمر</option>
                    </select>
                </div>
            </div>

            <div class="input-group" id="specialtyGroup" style="display: none;">
                <label>المادة / اختصاص المدرس الدراسي</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-tags"></i>
                    <select id="newUserSpecialty">
                        <option value="الكيمياء">الكيمياء</option>
                        <option value="الرياضيات">الرياضيات</option>
                        <option value="الفيزياء">الفيزياء</option>
                        <option value="الأحياء">الأحياء</option>
                        <option value="اللغة العربية">اللغة العربية</option>
                        <option value="اللغة الإنكليزية">اللغة الإنكليزية</option>
                        <option value="التربية الإسلامية">التربية الإسلامية</option>
                    </select>
                </div>
            </div>

            <div id="courseDetailsInputs" style="background: #f0fdf4; border: 1px dashed #0d9488; padding: 12px; border-radius: 14px; margin-bottom: 16px;">
                <div style="font-size: 12px; font-weight: 700; color: #0d9488; margin-bottom: 8px;"><i class="fa-solid fa-calendar-days"></i> تفاصيل وجدولة الدورة التعليمية:</div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 12px;">اسم الدورة الدراسية أو المجموعة</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-graduation-cap"></i>
                        <input type="text" id="newUserCourse" placeholder="مثال: دورة السادس العلمي A1">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 8px;" id="courseTeacherSubGroup">
                    <label style="font-size: 12px;">أستاذ الدورة المسؤول</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-chalkboard-user"></i>
                        <input type="text" id="courseTeacherName" placeholder="مثال: الأستاذ شبر حسن الحمامي">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 8px;" id="courseDateSubGroup">
                    <label style="font-size: 12px;">أيام الدورة الإسبوعية (اختر أيام المحاضرات)</label>
                    <div class="days-selector">
                        <input type="checkbox" id="day_sat" class="day-checkbox" value="السبت"><label for="day_sat" class="day-label">السبت</label>
                        <input type="checkbox" id="day_sun" class="day-checkbox" value="الأحد"><label for="day_sun" class="day-label">الأحد</label>
                        <input type="checkbox" id="day_mon" class="day-checkbox" value="الإثنين"><label for="day_mon" class="day-label">الإثنين</label>
                        <input type="checkbox" id="day_tue" class="day-checkbox" value="الثلاثاء"><label for="day_tue" class="day-label">الثلاثاء</label>
                        <input type="checkbox" id="day_wed" class="day-checkbox" value="الأربعاء"><label for="day_wed" class="day-label">الأربعاء</label>
                        <input type="checkbox" id="day_thu" class="day-checkbox" value="الخميس"><label for="day_thu" class="day-label">الخميس</label>
                        <input type="checkbox" id="day_fri" class="day-checkbox" value="الجمعة"><label for="day_fri" class="day-label">الجمعة</label>
                    </div>
                </div>
                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 8px;" id="courseTimeSubGroup">
                    <div class="input-group" style="margin-bottom: 0;">
                        <label style="font-size: 11px;">وقت البدء (منبه المحاضرة)</label>
                        <div class="input-wrapper">
                            <i class="fa-solid fa-clock"></i>
                            <input type="time" id="courseTime">
                        </div>
                    </div>
                    <div class="input-group" style="margin-bottom: 0;">
                        <label style="font-size: 11px;">مدة المحاضرة (بالدقائق)</label>
                        <div class="input-wrapper">
                            <i class="fa-solid fa-hourglass-half"></i>
                            <input type="number" id="courseDuration" placeholder="مثال: 120">
                        </div>
                    </div>
                </div>
            </div>

            <div id="studentFinanceInputs" style="background: #f8fafc; border: 1px dashed #cbd5e0; padding: 12px; border-radius: 14px; margin-bottom: 16px;">
                <div style="font-size: 12px; font-weight: 700; color: #8a2387; margin-bottom: 8px;"><i class="fa-solid fa-wallet"></i> الحسابات المالية للطالب الحالي:</div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 12px;">القسط الكلي للدورة (دينار عراقي)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-money-bill-wave"></i>
                        <input type="number" id="totalFee" placeholder="500000" oninput="calculateRemainingFee()">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 12px;">المبلغ المدفوع حالياً عند التسجيل</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-cash-register"></i>
                        <input type="number" id="paidFee" placeholder="200000" oninput="calculateRemainingFee()">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 0;">
                    <label style="font-size: 12px;">المبلغ المتبقي بذمة الطالب (يحتسب تلقائياً)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-calculator"></i>
                        <input type="number" id="remainingFee" placeholder="0" readonly style="background: #edf2f7; font-weight: bold; color: #c53030;">
                    </div>
                </div>
            </div>

            <div id="teacherFinanceInputs" style="background: #fffaf0; border: 1px dashed #f6ad55; padding: 12px; border-radius: 14px; margin-bottom: 16px; display: none;">
                <div style="font-size: 12px; font-weight: 700; color: #dd6b20; margin-bottom: 8px;"><i class="fa-solid fa-percentage"></i> الحسابات والنسب المالية للمدرس:</div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 12px;">نسبة المدرس من الدورة (%)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-percent"></i>
                        <input type="number" id="teacherPercent" placeholder="مثال: 50">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 0;">
                    <label style="font-size: 12px;">سعر الدورة المعتمد لحساب النسبة</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-sack-dollar"></i>
                        <input type="number" id="teacherCoursePrice" placeholder="مثال: 300000">
                    </div>
                </div>
            </div>

            <div class="input-group">
                <label>كود المعرف للمنصة ثابت (ID / الهاتف)</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-phone-flip"></i>
                    <input type="text" id="newUserIdentifier" placeholder="رقم الهاتف أو كود ثابت">
                </div>
            </div>

            <div class="input-group">
                <label>اسم المستخدم الكامل</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-user"></i>
                    <input type="text" id="newUserName" placeholder="الاسم الثنائي أو الثلاثي">
                </div>
            </div>

            <button class="btn-login admin-bg" onclick="generateUserAccount()" style="margin-bottom: 15px;">إنشاء وتفعيل الحساب</button>

            <div class="box-title" style="font-size: 15px; margin-bottom:5px; border-top: 1px solid #edf2f7; padding-top:15px;">
                <i class="fa-solid fa-users-viewfinder"></i> أقسام النظام المالي والتقارير
            </div>
            
            <div class="accounts-tabs">
                <button class="tab-btn active" id="tabStudents" onclick="switchAccountsTab('student')">الطلاب</button>
                <button class="tab-btn" id="tabTeachers" onclick="switchAccountsTab('teacher')">المدرسين</button>
                <button class="tab-btn" id="tabParents" onclick="switchAccountsTab('parent')">أولياء الأمور</button>
                <button class="tab-btn" id="tabAttendanceReport" onclick="switchAccountsTab('attendanceReport')">📋 تقرير الحضور</button>
                <button class="tab-btn" id="tabGeneralReport" onclick="switchAccountsTab('generalReport')">📊 تقرير المركز</button>
            </div>
            
            <div class="users-list" id="allocatedUsersContainer">
                <div style="text-align: center; color: var(--text-muted); font-size:12px; padding:15px;" id="noUsersText">
                    لا توجد حسابات مسجلة في هذا قسم حالياً.
                </div>
            </div>
        </div>
        <button class="btn-back" onclick="logoutAdmin()"><i class="fa-solid fa-right-from-bracket"></i> تسجيل الخروج بأمان</button>
    </div>


    <!-- 4. واجهة دخول المدرس -->
    <div id="teacherPage" class="page">
        <div class="login-box">
            <div class="login-box-title" style="color: #f12711;">
                <i class="fa-solid fa-book-open"></i> بوابة الأستاذ / المدرب
            </div>
            <div class="input-group">
                <label>كود المدرس أو رقم الهاتف المعتمد</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-id-card"></i>
                    <input type="text" id="teacherIdInput" placeholder="أدخل الكود المستلم من المدير">
                </div>
            </div>
            <button class="btn-login teacher-bg" onclick="verifyTeacherLogin()">تسجيل الدخول للمنصة</button>
        </div>
        <button class="btn-back" onclick="navigateTo('mainPage')"><i class="fa-solid fa-arrow-right"></i> العودة للخلف</button>
    </div>


    <!-- 5. لوحة تحكم المدرس (مضاف لها قارئ QR للحضور والغياب) -->
    <div id="teacherDashboard" class="page">
        <div class="dashboard-box">
            <div class="user-profile-header" style="border-color: #f12711;">
                <div class="user-avatar teacher-bg"><i class="fa-solid fa-chalkboard-user"></i></div>
                <div class="user-info">
                    <p id="displayTeacherName">الأستاذ</p>
                    <span id="displayTeacherSpecialty" style="color:#f12711; font-weight: bold;">المادة: </span>
                </div>
            </div>

            <!-- 📷 نظام مسجل وقارئ QR لتسجيل حضور الطلاب فوراً -->
            <div style="background: #f0fdf4; border: 1px dashed #10b981; padding: 14px; border-radius: 16px; margin-bottom: 16px; text-align: right;">
                <div style="font-size: 14px; font-weight: 700; color: #15803d; margin-bottom: 10px;">
                    <i class="fa-solid fa-qrcode"></i> جهاز مسح وقراءة QR لتسجيل الحضور
                </div>
                <button class="btn-login" style="background: #16a34a; padding: 8px; font-size: 12px; margin-bottom: 10px;" onclick="startQRScanner()"><i class="fa-solid fa-camera"></i> تشغيل كاميرا حضور الطلاب</button>
                <div id="reader" style="display: none;"></div>
            </div>

            <div style="background: #fffaf0; border: 1px dashed #f6ad55; padding: 14px; border-radius: 16px; margin-bottom: 16px; text-align: right;">
                <div style="font-size: 14px; font-weight: 700; color: #dd6b20; margin-bottom: 10px;">
                    <i class="fa-solid fa-marker"></i> رصد درجات امتحانات الطلاب والوزاريات
                </div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 11px;">كود الطالب المستهدف (ID)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-fingerprint"></i>
                        <input type="text" id="gradeStudentId" placeholder="مثال: 07700000">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 11px;">عنوان الامتحان أو المادة</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-file-signature"></i>
                        <input type="text" id="gradeTitle" placeholder="مثال: امتحان الشهر الأول الكيمياء">
                    </div>
                </div>
                <div class="input-group" style="margin-bottom: 8px;">
                    <label style="font-size: 11px;">الدرجة المستحقة (من 100)</label>
                    <div class="input-wrapper">
                        <i class="fa-solid fa-star"></i>
                        <input type="number" id="gradeScore" placeholder="100">
                    </div>
                </div>
                <button class="btn-login teacher-bg" style="padding: 10px; font-size: 13px;" onclick="teacherAddGrade()">رصد وإرسال الدرجة</button>
            </div>

            <div class="box-title" style="font-size: 15px; color:#f12711; margin-bottom:12px;">
                <i class="fa-solid fa-cloud-arrow-up"></i> رفع محاضرة ومحتوى جديد للمنصة
            </div>

            <div class="input-group">
                <label>عنوان المحاضرة أو الفصل</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-heading"></i>
                    <input type="text" id="lecTitle" placeholder="مثال: الفصل الأول - المحاضرة 1">
                </div>
            </div>

            <div class="input-group">
                <label>رابط الفيديو الشرح (يوتيوب / سيرفر)</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-video"></i>
                    <input type="text" id="lecVideo" placeholder="https://youtube.com/...">
                </div>
            </div>

            <div class="input-group">
                <label>رابط ملخص أو ملزمة الفصل (PDF)</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-file-pdf"></i>
                    <input type="text" id="lecPdf" placeholder="https://drive.google.com/...">
                </div>
            </div>

            <div class="input-group">
                <label>رابط الأسئلة الوزارية والامتحانات الوزارية</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-graduation-cap"></i>
                    <input type="text" id="lecExam" placeholder="رابط الاختبار أو الوزاريات">
                </div>
            </div>

            <button class="btn-login teacher-bg" onclick="teacherUploadContent()">نشر المحاضرة للمادة فوراً</button>
        </div>
        <button class="btn-back" onclick="logoutTeacher()"><i class="fa-solid fa-right-from-bracket"></i> تسجيل خروج بأمان</button>
    </div>


    <!-- 6. واجهة دخول الطالب -->
    <div id="studentPage" class="page">
        <div class="login-box">
            <div class="login-box-title" style="color: #0083b0;">
                <i class="fa-solid fa-user-graduate"></i> دخول الطالب
            </div>
            <div class="input-group">
                <label>كود الطالب الدراسي (ID)</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-id-card"></i>
                    <input type="text" id="studentIdInput" placeholder="أدخل الكود المستلم من المدير">
                </div>
            </div>
            <button class="btn-login student-bg" onclick="verifyStudentLogin()">تسجيل الدخول للمنصة</button>
        </div>
        <button class="btn-back" onclick="navigateTo('mainPage')"><i class="fa-solid fa-arrow-right"></i> العودة للخلف</button>
    </div>


    <!-- 7. لوحة تحكم الطالب المشتركة (مضاف لها كرت الهوية الرقمية QR) -->
    <div id="studentDashboard" class="page">
        <div class="dashboard-box">
            <div class="user-profile-header">
                <div class="user-avatar student-bg"><i class="fa-solid fa-graduation-cap"></i></div>
                <div class="user-info">
                    <p id="displayStudentName">طالب مركز آراي</p>
                    <span id="displayStudentId">المعرف: لا يوجد</span>
                </div>
            </div>

            <!-- 🪪 كرت بطاقة الهوية الرقمية QR المضافة للطالب ليقوم المدرس بمسحها -->
            <div class="schedule-card" id="studentQRCardSection" style="border-color: #0d9488; background: linear-gradient(135deg, #ffffff 0%, #f0fdf4 100%); text-align: center;">
                <div class="schedule-title" style="color: #0f766e; justify-content: center;">
                    <i class="fa-solid fa-id-badge"></i> بطاقة الهوية الرقمية لتسجيل الحضور
                </div>
                <div class="qr-wrapper">
                    <div id="qrcodeCanvas"></div>
                    <p style="font-size: 11px; color: var(--text-muted); margin-top: 8px; font-weight: bold;">تعرض هذا الكود للمدرس عند دخول القاعة لتسجيل الحضور</p>
                </div>
            </div>

            <div class="alert-box" id="studentAlertNotification">
                <h4><i class="fa-solid fa-bell"></i> جدار تنبيهات الدورات والمحاضرات</h4>
                <div class="alert-scroll" id="alertScrollContainer"></div>
            </div>

            <div class="schedule-card" style="border-color: #0083b0; background: linear-gradient(135deg, #ffffff 0%, #f0f9ff 100%);">
                <div class="schedule-title" style="color: #0369a1;">
                    <i class="fa-solid fa-calendar-week"></i> جداول ومواعيد دوراتك المسجلة
                </div>
                <div class="course-loop-container" id="studentCoursesLoop"></div>
            </div>

            <div class="schedule-card" style="border-color: #f59e0b; background: linear-gradient(135deg, #ffffff 0%, #fffbeb 100%);">
                <div class="schedule-title" style="color: #b45309;">
                    <i class="fa-solid fa-star"></i> لوحة درجات الامتحانات والوزاريات المسجلة
                </div>
                <div class="course-loop-container" id="studentGradesLoop">
                    <div style="text-align: center; color: var(--text-muted); font-size:11px; padding:10px;">لا توجد درجات مرصودة حالياً.</div>
                </div>
            </div>

            <div class="finance-card" id="studentFinanceCardSection">
                <div class="finance-title">
                    <i class="fa-solid fa-receipt" style="color: #0083b0;"></i> إجمالي الموقف المالي لكل الأقساط
                </div>
                <div class="finance-row">
                    <div class="finance-box-item fin-total">القسط الكلي<p id="stuFinTotal">0 د.ع</p></div>
                    <div class="finance-box-item fin-paid">المدفوع<p id="stuFinPaid">0 د.ع</p></div>
                    <div class="finance-box-item fin-due">المتبقي<p id="stuFinDue">0 د.ع</p></div>
                </div>
            </div>

            <div id="studentBentoGridSection">
                <div class="box-title" style="font-size: 16px; color:#0083b0; margin-bottom:15px;">
                    <i class="fa-solid fa-book-bookmark"></i> المنهج العراقي المعتمد (المواد السبعة)
                </div>

                <div class="bento-grid">
                    <div class="bento-item featured" onclick="openSubject('الكيمياء')">
                        <div style="display: flex; align-items: center; gap: 12px;">
                            <div class="subject-icon-wrapper bg-chemistry"><i class="fa-solid fa-flask-vial"></i></div>
                            <div class="subject-meta"><h3>الكيمياء</h3><p id="badge-count-الكيمياء">المحاضرات، الملازم والوزاريات</p></div>
                        </div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                    <div class="bento-item" onclick="openSubject('الرياضيات')">
                        <div class="subject-icon-wrapper bg-math"><i class="fa-solid fa-calculator"></i></div>
                        <div class="subject-meta"><h3>الرياضيات</h3><p id="badge-count-الرياضيات">الفصول والدروس</p></div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                    <div class="bento-item" onclick="openSubject('الفيزياء')">
                        <div class="subject-icon-wrapper bg-physics"><i class="fa-solid fa-atom"></i></div>
                        <div class="subject-meta"><h3>الفيزياء</h3><p id="badge-count-الفيزياء">الدروس والتجارب</p></div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                    <div class="bento-item" onclick="openSubject('الأحياء')">
                        <div class="subject-icon-wrapper bg-biology"><i class="fa-solid fa-dna"></i></div>
                        <div class="subject-meta"><h3>الأحياء</h3><p id="badge-count-الأحياء">الرسومات والأنسجة</p></div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                    <div class="bento-item" onclick="openSubject('اللغة العربية')">
                        <div class="subject-icon-wrapper bg-arabic"><i class="fa-solid fa-book"></i></div>
                        <div class="subject-meta"><h3>اللغة العربية</h3><p id="badge-count-اللغة العربية">القواعد والأدب</p></div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                    <div class="bento-item" onclick="openSubject('اللغة الإنكليزية')">
                        <div class="subject-icon-wrapper bg-english"><i class="fa-solid fa-language"></i></div>
                        <div class="subject-meta"><h3>اللغة الإنكليزية</h3><p id="badge-count-اللغة الإنكليزية">القطع والقواعد</p></div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                    <div class="bento-item" style="grid-column: span 2;" onclick="openSubject('التربية الإسلامية')">
                        <div style="display: flex; align-items: center; gap: 12px;">
                            <div class="subject-icon-wrapper bg-islamic"><i class="fa-solid fa-mosque"></i></div>
                            <div class="subject-meta"><h3>التربية الإسلامية</h3><p id="badge-count-التربية الإسلامية">الأحكام والوزاريات</p></div>
                        </div>
                        <div class="subject-arrow"><i class="fa-solid fa-chevron-left"></i></div>
                    </div>
                </div>

                <div class="box-title" id="selectedSubjectTitle" style="font-size: 14px; margin-top:15px; display:none; color: #2d3748;">محتويات المادة:</div>
                <div class="content-viewer-box" id="studentContentViewer" style="display: none;"></div>
            </div>
        </div>
        <button class="btn-back" id="btnStudentLogout" onclick="logoutStudent()"><i class="fa-solid fa-right-from-bracket"></i> تسجيل الخروج بأمان</button>
    </div>


    <!-- 8. واجهة دخول ولي الأمر -->
    <div id="parentPage" class="page">
        <div class="login-box">
            <div class="login-box-title" style="color: #4e54c8;">
                <i class="fa-solid fa-users"></i> بوابة ولي الأمر لمتابعة الأبناء
            </div>
            <div class="input-group">
                <label>أدخل كود الطالب الدراسي الخاص بابنك (ID)</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-id-card"></i>
                    <input type="text" id="parentStudentIdInput" placeholder="مثال: رقم الهاتف أو الكود المعتمد">
                </div>
            </div>
            <button class="btn-login parent-bg" onclick="verifyParentLogin()">متابعة حالة الابن فوراً</button>
        </div>
        <button class="btn-back" onclick="navigateTo('mainPage')"><i class="fa-solid fa-arrow-right"></i> العودة للقائمة</button>
    </div>

    <div id="toast-container"></div>
    <div class="footer-section">منصة مركز آراي التعليمية المتكاملة</div>

    <!-- 🖨️ قالب المعاينة والطباعة الخاص بورقة A4 للتقارير المعتمدة -->
    <div id="printPageTemplate">
        <div style="text-align: center; border-bottom: 3px double #000; padding-bottom: 15px; margin-bottom: 20px;">
            <h1 style="font-size: 24px; font-weight: 800;">مركز آراي التعليمي المتكامل</h1>
            <p style="font-size: 14px; color: #555; margin-top: 5px;">نظام الحضور والمالية المعتمد - تقرير رسمي مطبوع (A4)</p>
            <p style="font-size: 12px; margin-top: 5px;" id="printReportDate">التاريخ: </p>
        </div>
        <div id="printPageBody"></div>
        <div style="margin-top: 50px; display: flex; justify-content: space-between; font-weight: bold; font-size: 14px;">
            <div>توقيع الحسابات: ............................</div>
            <div>مصادقة إدارة المركز: ............................</div>
        </div>
    </div>

    <script>
        const MASTER_ADMIN_EMAIL = "arai.manager@gmail.com"; 
        const MASTER_ADMIN_KEY = "123456"; 

        let distributedAccounts = JSON.parse(localStorage.getItem('arai_accounts')) || [];
        let globalLecturesDatabase = JSON.parse(localStorage.getItem('arai_lectures')) || []; 
        let expensesDatabase = JSON.parse(localStorage.getItem('arai_expenses')) || []; 
        let studentGradesDatabase = JSON.parse(localStorage.getItem('arai_grades')) || []; 
        
        // قاعدة الحضور المحدثة المحفوظة تلقائياً
        let attendanceDatabase = JSON.parse(localStorage.getItem('arai_attendance')) || []; 
        
        let currentActiveTeacher = null;  
        let lastUploadedLecture = JSON.parse(localStorage.getItem('arai_last_lecture')) || null;   
        let currentSelectedTab = 'student';
        let isParentMode = false; 
        let html5QrcodeScanner = null;

        if(globalLecturesDatabase.length === 0) {
            globalLecturesDatabase = [
                { subject: "الكيمياء", teacherName: "الأستاذ شبر حسن الحمامي", title: "الفصل الأول - علم الثرموداينمك (المحاضرة 1)", videoUrl: "https://youtube.com/", pdfUrl: "https://drive.google.com/", examUrl: "https://forms.google.com/" },
                { subject: "الرياضيات", teacherName: "مدرس المادة المعتمد", title: "الفصل الأول - الأعداد المركبة", videoUrl: "https://youtube.com/", pdfUrl: "#", examUrl: "#" }
            ];
            localStorage.setItem('arai_lectures', JSON.stringify(globalLecturesDatabase));
        }

        function navigateTo(pageId) {
            const pages = document.querySelectorAll('.page');
            pages.forEach(page => page.classList.remove('active'));
            const targetPage = document.getElementById(pageId);
            if (targetPage) targetPage.classList.add('active');
            
            // إيقاف الكاميرا تلقائياً إذا خرج المدرس من اللوحة للحفاظ على أداء الجهاز
            if(pageId !== 'teacherDashboard' && html5QrcodeScanner) {
                html5QrcodeScanner.clear();
                document.getElementById('reader').style.display = 'none';
            }
        }

        function calculateRemainingFee() {
            const total = parseFloat(document.getElementById('totalFee').value) || 0;
            const paid = parseFloat(document.getElementById('paidFee').value) || 0;
            const remaining = total - paid;
            document.getElementById('remainingFee').value = remaining >= 0 ? remaining : 0;
        }

        function getSelectedDays() {
            const days = ['sat', 'sun', 'mon', 'tue', 'wed', 'thu', 'fri'];
            let chosen = [];
            days.forEach(d => {
                const cb = document.getElementById('day_' + d);
                if(cb && cb.checked) chosen.push(cb.value);
            });
            return chosen.join(' و ');
        }

        function clearSelectedDays() {
            const days = ['sat', 'sun', 'mon', 'tue', 'wed', 'thu', 'fri'];
            days.forEach(d => {
                const cb = document.getElementById('day_' + d);
                if(cb) cb.checked = false;
            });
        }

        function toggleSpecialtyField() {
            const type = document.getElementById('newUserType').value;
            const specialtyGroup = document.getElementById('specialtyGroup');
            const courseDetails = document.getElementById('courseDetailsInputs');
            const studentFinance = document.getElementById('studentFinanceInputs');
            const teacherFinance = document.getElementById('teacherFinanceInputs');
            
            if(type === 'teacher') {
                specialtyGroup.style.display = 'block';
                courseDetails.style.display = 'none'; 
                studentFinance.style.display = 'none';
                teacherFinance.style.display = 'block';
            } else if(type === 'student') {
                specialtyGroup.style.display = 'none';
                courseDetails.style.display = 'block'; 
                studentFinance.style.display = 'block';
                teacherFinance.style.display = 'none';
            } else {
                specialtyGroup.style.display = 'none';
                courseDetails.style.display = 'none';
                studentFinance.style.display = 'none';
                teacherFinance.style.display = 'none';
            }
        }

        function addExpenseItem() {
            const title = document.getElementById('expenseTitle').value.trim();
            const amount = parseFloat(document.getElementById('expenseAmount').value) || 0;
            if(!title || amount <= 0) {
                showToast("⚠️ يرجى إدخال بيان المصروف والقيمة بشكل صحيح!", "error");
                return;
            }
            expensesDatabase.push({ title: title, amount: amount, date: new Date().toLocaleDateString('ar-EG') });
            localStorage.setItem('arai_expenses', JSON.stringify(expensesDatabase));
            showToast("📉 تم تسجيل المصروف المالي بنجاح", "success");
            document.getElementById('expenseTitle').value = "";
            document.getElementById('expenseAmount').value = "";
            updateDashboardUI();
        }

        function verifyAdminLogin() {
            const enteredEmail = document.getElementById('adminEmail').value.trim();
            const enteredKey = document.getElementById('adminKey').value.trim();
            if(enteredEmail === MASTER_ADMIN_EMAIL && enteredKey === MASTER_ADMIN_KEY) {
                document.getElementById('displayAdminEmail').innerText = enteredEmail;
                updateDashboardUI();
                navigateTo('adminDashboard');
                showToast("🔓 تم دخول المدير بنجاح", "success");
            } else {
                showToast("❌ بيانات الدخول خاطئة!", "error");
            }
        }

        function logoutAdmin() {
            navigateTo('mainPage');
            showToast("🔒 تم تسجيل خروج الإدارة بأمان", "info");
        }

        function convertTimeTo12h(timeStr) {
            if(!timeStr) return "غير محدد";
            let [hours, minutes] = timeStr.split(':');
            hours = parseInt(hours);
            let ampm = hours >= 12 ? 'مساءً' : 'صباحاً';
            hours = hours % 12;
            hours = hours ? hours : 12; 
            return `${hours}:${minutes} ${ampm}`;
        }

        function generateUserAccount() {
            const type = document.getElementById('newUserType').value;
            const name = document.getElementById('newUserName').value.trim();
            const identifier = document.getElementById('newUserIdentifier').value.trim();
            const specialty = document.getElementById('newUserSpecialty').value;

            if(!name || !identifier) {
                showToast("⚠️ يرجى ملء الحقول المطلوبة!", "error");
                return;
            }

            if(type === 'student') {
                const courseName = document.getElementById('newUserCourse').value.trim() || "دورة عامة";
                const teacherName = document.getElementById('courseTeacherName').value.trim() || "المدرس العام";
                const daysChose = getSelectedDays() || "لم تحدد";
                const rawTime = document.getElementById('courseTime').value;
                const cTime = convertTimeTo12h(rawTime);
                const cDuration = document.getElementById('courseDuration').value.trim() || "0";

                const total = parseFloat(document.getElementById('totalFee').value) || 0;
                const paid = parseFloat(document.getElementById('paidFee').value) || 0;
                const remaining = total - paid;

                let existingStudentIndex = distributedAccounts.findIndex(acc => acc.type === 'student' && acc.id === identifier);

                if(existingStudentIndex !== -1) {
                    let oldAcc = distributedAccounts[existingStudentIndex];
                    oldAcc.coursesList = oldAcc.coursesList || [];
                    oldAcc.coursesList.push({ name: courseName, teacher: teacherName, date: daysChose, time: cTime, duration: cDuration + " دقيقة" });
                    oldAcc.finance.total = (parseFloat(oldAcc.finance.total) + total).toString();
                    oldAcc.finance.paid = (parseFloat(oldAcc.finance.paid) + paid).toString();
                    oldAcc.finance.remaining = (parseFloat(oldAcc.finance.remaining) + remaining).toString();
                    showToast(`🔄 تم إضافة الدورة الجديدة للطالب وتراكم الحساب!`, "success");
                } else {
                    distributedAccounts.push({
                        type: 'student', name: name, id: identifier,
                        coursesList: [{ name: courseName, teacher: teacherName, date: daysChose, time: cTime, duration: cDuration + " دقيقة" }],
                        finance: { total: total.toString(), paid: paid.toString(), remaining: remaining.toString() },
                        timestamp: new Date().toLocaleTimeString('ar-EG', {hour: '2-digit', minute:'2-digit'})
                    });
                    showToast(`✅ تم إنشاء حساب طالب جديد!`, "success");
                }
            } else if(type === 'teacher') {
                const percent = parseFloat(document.getElementById('teacherPercent').value) || 0;
                const coursePrice = parseFloat(document.getElementById('teacherCoursePrice').value) || 0;
                distributedAccounts.push({ type: 'teacher', name: name, id: identifier, specialty: specialty, finance: { percent: percent, coursePrice: coursePrice } });
                showToast(`✅ تم تفعيل حساب المدرس المعتمد!`, "success");
            } else {
                distributedAccounts.push({ type: 'parent', name: name, id: identifier });
                showToast(`✅ تم تفعيل حساب ولي الأمر!`, "success");
            }

            localStorage.setItem('arai_accounts', JSON.stringify(distributedAccounts));
            
            document.getElementById('newUserName').value = "";
            document.getElementById('newUserIdentifier').value = "";
            document.getElementById('newUserCourse').value = "";
            document.getElementById('courseTeacherName').value = "";
            document.getElementById('totalFee').value = "";
            document.getElementById('paidFee').value = "";
            document.getElementById('remainingFee').value = "";
            clearSelectedDays();
            updateDashboardUI();
        }

        function switchAccountsTab(tabType) {
            currentSelectedTab = tabType;
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            document.getElementById('tab' + tabType.charAt(0).toUpperCase() + tabType.slice(1)).classList.add('active');
            updateDashboardUI();
        }

        function updateDashboardUI() {
            const container = document.getElementById('allocatedUsersContainer');
            container.innerHTML = "";

            let sCount = 0, tCount = 0, pCount = 0;
            distributedAccounts.forEach(acc => {
                if(acc.type === 'student') sCount++;
                if(acc.type === 'teacher') tCount++;
                if(acc.type === 'parent') pCount++;
            });
            document.getElementById('countStudents').innerText = sCount;
            document.getElementById('countTeachers').innerText = tCount;
            document.getElementById('countParents').innerText = pCount;

            // تقرير الحضور والغياب للمدير (يومي وشهري مدمج ومحفوظ)
            if(currentSelectedTab === 'attendanceReport') {
                let rowsHtml = "";
                attendanceDatabase.forEach((record, index) => {
                    rowsHtml += `
                        <tr>
                            <td>${record.date}</td>
                            <td>${record.studentName}</td>
                            <td>${record.studentId}</td>
                            <td>${record.teacherName}</td>
                            <td><span style="color:green; font-weight:bold;"><i class="fa-solid fa-circle-check"></i> حاضر</span></td>
                        </tr>
                    `;
                });

                container.innerHTML = `
                    <div style="background: #ffffff; padding: 10px; border-radius: 14px; border: 1px solid #e2e8f0; text-align: right;">
                        <h4 style="font-size:13px; color:#0f766e; margin-bottom:8px;"><i class="fa-solid fa-clipboard-user"></i> سجل حضور وغياب الطلاب اليومي والشهري</h4>
                        <table class="finance-table" style="margin-bottom: 10px;">
                            <thead>
                                <tr style="background:#0f766e; color:white;">
                                    <th>التاريخ</th>
                                    <th>الطالب</th>
                                    <th>الكود</th>
                                    <th>بإشراف</th>
                                    <th>الحالة</th>
                                </tr>
                            </thead>
                            <tbody>
                                ${rowsHtml || '<tr><td colspan="5">لا توجد سجلات حضور لليوم. جميع الطلاب في حالة غياب مؤقت.</td></tr>'}
                            </tbody>
                        </table>
                        <button class="btn-print-action" style="background:#0f766e;" onclick="printAttendanceReport()"><i class="fa-solid fa-print"></i> طباعة كشف الحضور الدوري (A4)</button>
                    </div>
                `;
                return;
            }

            if(currentSelectedTab === 'generalReport') {
                let totalStudentIncomes = 0;
                distributedAccounts.forEach(a => { if(a.type === 'student' && a.finance) totalStudentIncomes += parseFloat(a.finance.paid) || 0; });
                let totalExpenses = 0;
                expensesDatabase.forEach(e => totalExpenses += e.amount || 0);
                let netProfit = totalStudentIncomes - totalExpenses;

                container.innerHTML = `
                    <div style="background: #f8fafc; padding: 14px; border-radius: 16px; border: 1px solid #e2e8f0; text-align: right;">
                        <h4 style="font-size:14px; color:#8a2387; margin-bottom:10px;"><i class="fa-solid fa-chart-line"></i> التقرير المالي العام للمركز</h4>
                        <p style="font-size:13px; margin-bottom:4px;">إجمالي واردات الطلاب: <strong>${totalStudentIncomes.toLocaleString()} د.ع</strong></p>
                        <p style="font-size:13px; margin-bottom:4px;">إجمالي مصروفات المركز: <strong style="color:#ef4444;">${totalExpenses.toLocaleString()} د.ع</strong></p>
                        <hr style="margin: 8px 0; border: 0; border-top: 1px solid #cbd5e0;">
                        <p style="font-size:14px; font-weight:800; color:#10b981;">صافي أرباح المركز الكلية: <span>${netProfit.toLocaleString()} د.ع</span></p>
                        <button class="btn-print-action" onclick="printGeneralReport()"><i class="fa-solid fa-print"></i> طباعة التقرير العام (A4 PDF)</button>
                    </div>
                `;
                return;
            }

            const filtered = distributedAccounts.filter(acc => acc.type === currentSelectedTab);
            if(filtered.length === 0) {
                container.innerHTML = `<div style="text-align: center; color: var(--text-muted); font-size:12px; padding:15px;">لا توجد بيانات مسجلة حالياً.</div>`;
                return;
            }

            filtered.forEach(acc => {
                if(acc.type === 'student') {
                    container.innerHTML += `
                        <div class="user-badge badge-student">
                            <div class="user-badge-info">
                                <p>${acc.name}</p>
                                <span>المعرف: ${acc.id} | المدفوع: ${(acc.finance?parseInt(acc.finance.paid):0).toLocaleString()} د.ع</span>
                            </div>
                        </div>
                    `;
                }
                if(acc.type === 'teacher') {
                    let studentsForThisTeacher = distributedAccounts.filter(st => st.type === 'student' && st.coursesList && st.coursesList.some(c => c.teacher === acc.name));
                    let countStudents = studentsForThisTeacher.length;
                    let calculatedTotalIncome = countStudents * (acc.finance.coursePrice || 0);
                    let teacherShare = calculatedTotalIncome * ((acc.finance.percent || 0) / 100);

                    container.innerHTML += `
                        <div class="user-badge badge-teacher">
                            <div class="user-badge-info">
                                <p>${acc.name} (${acc.specialty})</p>
                                <span>النسبة المتفق عليها: ${acc.finance.percent}% | عدد الطلاب: ${countStudents} طالباً</span>
                                <span style="color:#10b981; font-weight:bold; margin-top:4px;">مستحقات المدرس الكلية: ${teacherShare.toLocaleString()} د.ع</span>
                            </div>
                            <button class="btn-print-action" style="padding:4px; font-size:11px;" onclick="printTeacherReport('${acc.name}', '${acc.specialty}', ${acc.finance.percent}, ${countStudents}, ${teacherShare})"><i class="fa-solid fa-print"></i> طباعة كشف المدرس الورقي</button>
                        </div>
                    `;
                }
                if(acc.type === 'parent') {
                    container.innerHTML += `<div class="user-badge badge-parent"><div class="user-badge-info"><p>${acc.name}</p><span>رقم الهاتف/المعرف للابن: ${acc.id}</span></div></div>`;
                }
            });
        }

        // طباعة سجلات الحضور للمدير
        function printAttendanceReport() {
            let rows = "";
            attendanceDatabase.forEach((record, idx) => {
                rows += `<tr><td>${idx+1}</td><td>${record.date}</td><td>${record.studentName}</td><td>${record.studentId}</td><td>${record.teacherName}</td><td>حاضر (بصمة QR)</td></tr>`;
            });
            const bodyHtml = `
                <h3 style="text-align:center; margin-bottom:15px;">تقرير الحضور والغياب والالتزام الدراسي</h3>
                <table class="finance-table" style="font-size:13px;">
                    <thead>
                        <tr style="background:#0f766e; color:#fff;">
                            <th>ت</th>
                            <th>التاريخ واليوم</th>
                            <th>اسم الطالب</th>
                            <th>كود الطالب ID</th>
                            <th>المدرس المستلم</th>
                            <th>حالة الحضور</th>
                        </tr>
                    </thead>
                    <tbody>${rows || '<tr><td colspan="6">لا توجد بيانات حضور مسجلة في التقارير لهذا اليوم.</td></tr>'}</tbody>
                </table>
            `;
            executePrintA4(bodyHtml);
        }

        function printGeneralReport() {
            let totalStudentIncomes = 0;
            distributedAccounts.forEach(a => { if(a.type === 'student' && a.finance) totalStudentIncomes += parseFloat(a.finance.paid) || 0; });
            let totalExpenses = 0;
            expensesDatabase.forEach(e => totalExpenses += e.amount || 0);
            let netProfit = totalStudentIncomes - totalExpenses;

            let expensesRows = "";
            expensesDatabase.forEach((e, index) => {
                expensesRows += `<tr><td>${index+1}</td><td>${e.title}</td><td>${e.date}</td><td>${e.amount.toLocaleString()} د.ع</td></tr>`;
            });

            const bodyHtml = `
                <h3 style="text-align:center; margin-bottom:15px; color:#333;">تقرير الخزينة والموقف المالي العام للمركز</h3>
                <table class="finance-table" style="font-size:14px; margin-bottom:20px;">
                    <tr style="background:#f4f4f4;"><th>البيان المالي الكلي</th><th>القيمة بالدينار العراقي</th></tr>
                    <tr><td>إجمالي المبالغ المستلمة من الطلاب</td><td style="color:green; font-weight:bold;">${totalStudentIncomes.toLocaleString()} د.ع</td></tr>
                    <tr><td>إجمالي المصروفات التشغيلية والخدمية للمركز</td><td style="color:red; font-weight:bold;">${totalExpenses.toLocaleString()} د.ع</td></tr>
                    <tr style="background:#e6fffa; font-weight:bold;"><td>صافي الأرباح النهائية للمركز</td><td style="color:#0d9488; font-size:16px;">${netProfit.toLocaleString()} د.ع</td></tr>
                </table>
                <h4 style="margin-bottom:8px; border-bottom:1px solid #ccc; padding-bottom:4px;">سجل المصروفات التفصيلي:</h4>
                <table class="finance-table">
                    <thead><tr style="background:#8a2387; color:#fff;"><th>ت</th><th>بيان وتفاصيل المصروف</th><th>التاريخ</th><th>المبلغ</th></tr></thead>
                    <tbody>${expensesRows || '<tr><td colspan="4">لم يتم تسجيل أي مصروفات تشغيلية بعد.</td></tr>'}</tbody>
                </table>
            `;
            executePrintA4(bodyHtml);
        }

        function printTeacherReport(name, specialty, percent, studentsCount, totalShare) {
            let studentsRows = "";
            let idx = 1;
            distributedAccounts.forEach(st => {
                if(st.type === 'student' && st.coursesList && st.coursesList.some(c => c.teacher === name)) {
                    studentsRows += `<tr><td>${idx++}</td><td>${st.name}</td><td>${st.id}</td><td>مسجل ومثبت الحضور</td></tr>`;
                }
            });

            const bodyHtml = `
                <h3 style="text-align:center; margin-bottom:15px; color:#333;">كشف حساب ومستحقات الأستاذ</h3>
                <div style="background:#f9f9f9; padding:12px; border:1px solid #ddd; border-radius:8px; margin-bottom:15px; line-height:1.6;">
                    <p>اسم المدرس: <strong>${name}</strong></p>
                    <p>المادة والاختصاص الدراسي: <strong>${specialty}</strong></p>
                    <p>النسبة المالية المعتمدة للمدرس: <strong>${percent}%</strong> من قيمة الدورة</p>
                    <p>عدد الطلاب النشطين التابعين للمدرس: <strong>${studentsCount} طالب</strong></p>
                    <p style="font-size:16px; margin-top:5px; color:#b45309;">صافي مستحقات المدرس الحالية: <strong>${totalShare.toLocaleString()} د.ع</strong></p>
                </div>
                <h4 style="margin-bottom:8px;">قائمة الطلاب المسجلين بالدورة:</h4>
                <table class="finance-table">
                    <thead><tr style="background:#333; color:#fff;"><th>ت</th><th>اسم الطالب الثلاثي</th><th>كود الطالب (ID)</th><th>حالة الحساب والتثبيت</th></tr></thead>
                    <tbody>${studentsRows || '<tr><td colspan="4">لا يوجد طلاب مسجلين بداخل دورات هذا الأستاذ حالياً.</td></tr>'}</tbody>
                </table>
            `;
            executePrintA4(bodyHtml);
        }

        function executePrintA4(htmlContent) {
            document.getElementById('printReportDate').innerText = "تاريخ إصدار التقرير: " + new Date().toLocaleString('ar-EG');
            document.getElementById('printPageBody').innerHTML = htmlContent;
            window.print();
        }

        function verifyTeacherLogin() {
            const teacherId = document.getElementById('teacherIdInput').value.trim();
            if(!teacherId) return;
            const foundTeacher = distributedAccounts.find(acc => acc.type === 'teacher' && acc.id === teacherId);
            if(foundTeacher) {
                currentActiveTeacher = foundTeacher; 
                document.getElementById('displayTeacherName').innerText = "الأستاذ: " + foundTeacher.name;
                document.getElementById('displayTeacherSpecialty').innerText = "المادة والاختصاص: " + foundTeacher.specialty;
                navigateTo('teacherDashboard');
                showToast(`👋 أهلاً بك أستاذ ${foundTeacher.name}`, "success");
            } else {
                showToast("❌ كود المدرس غير مسجل بالمنظومة!", "error");
            }
        }

        function logoutTeacher() {
            if(html5QrcodeScanner) html5QrcodeScanner.clear();
            navigateTo('mainPage');
            showToast("🔒 تم تسجيل خروج المدرس بأمان", "info");
        }

        // 🚀 نظام تشغيل الكاميرا ومسح الـ QR للطلاب من واجهة المدرس
        function startQRScanner() {
            document.getElementById('reader').style.display = 'block';
            html5QrcodeScanner = new Html5QrcodeScanner("reader", { fps: 10, qrbox: 250 });
            html5QrcodeScanner.render((decodedText) => {
                // عند نجاح القراءة العثور على الطالب وتسجيله حضور
                const foundStudent = distributedAccounts.find(acc => acc.type === 'student' && acc.id === decodedText);
                if(foundStudent) {
                    // التحقق من عدم تسجيله مرتين في نفس اليوم
                    let todayStr = new Date().toLocaleDateString('ar-EG');
                    let alreadyChecked = attendanceDatabase.some(rec => rec.studentId === decodedText && rec.date === todayStr);
                    
                    if(alreadyChecked) {
                        showToast(`⚠️ الطالب ${foundStudent.name} مسجل حضور مسبقاً اليوم!`, "info");
                    } else {
                        attendanceDatabase.push({
                            date: todayStr,
                            studentId: foundStudent.id,
                            studentName: foundStudent.name,
                            teacherName: currentActiveTeacher.name
                        });
                        localStorage.setItem('arai_attendance', JSON.stringify(attendanceDatabase));
                        showToast(`🎯 تم تسجيل حضور الطالب: ${foundStudent.name}`, "success");
                    }
                    html5QrcodeScanner.clear();
                    document.getElementById('reader').style.display = 'none';
                } else {
                    showToast("❌ رمز كود QR غير معترف به في المركز!", "error");
                }
            }, (error) => { /* الحفاظ على استمرار الفحص الصامت */ });
        }

        function teacherAddGrade() {
            const studentId = document.getElementById('gradeStudentId').value.trim();
            const title = document.getElementById('gradeTitle').value.trim();
            const score = document.getElementById('gradeScore').value.trim();

            if(!studentId || !title || !score) {
                showToast("⚠️ يرجى ملء حقول رصد الدرجات بالكامل!", "error");
                return;
            }

            studentGradesDatabase.push({
                studentId: studentId, title: title, score: score,
                teacherName: currentActiveTeacher.name, date: new Date().toLocaleDateString('ar-EG')
            });

            localStorage.setItem('arai_grades', JSON.stringify(studentGradesDatabase));
            showToast(`🎖️ تم رصد درجة الطالب ${studentId} بنجاح!`, "success");
            document.getElementById('gradeStudentId').value = "";
            document.getElementById('gradeTitle').value = "";
            document.getElementById('gradeScore').value = "";
        }

        function teacherUploadContent() {
            const title = document.getElementById('lecTitle').value.trim();
            const video = document.getElementById('lecVideo').value.trim();
            const pdf = document.getElementById('lecPdf').value.trim();
            const exam = document.getElementById('lecExam').value.trim();

            if(!title) return;
            const newLecture = { subject: currentActiveTeacher.specialty, teacherName: currentActiveTeacher.name, title: title, videoUrl: video || "#", pdfUrl: pdf || "#", examUrl: exam || "#" };
            globalLecturesDatabase.push(newLecture);
            lastUploadedLecture = newLecture; 
            localStorage.setItem('arai_lectures', JSON.stringify(globalLecturesDatabase));
            localStorage.setItem('arai_last_lecture', JSON.stringify(lastUploadedLecture));
            showToast(`✅ تم نشر المحاضرة بنجاح!`, "success");
            
            document.getElementById('lecTitle').value = "";
            document.getElementById('lecVideo').value = "";
            document.getElementById('lecPdf').value = "";
            document.getElementById('lecExam').value = "";
        }

        function verifyParentLogin() {
            const parentStudentId = document.getElementById('parentStudentIdInput').value.trim();
            if(!parentStudentId) {
                showToast("⚠️ يرجى إدخال كود الابن للمتابعة!", "error");
                return;
            }

            const foundStudent = distributedAccounts.find(acc => acc.type === 'student' && acc.id === parentStudentId);
            if(foundStudent) {
                isParentMode = true; 
                document.getElementById('displayStudentName').innerText = "متابعة الابن: " + foundStudent.name;
                document.getElementById('displayStudentId').innerText = "كود الطالب الدراسي: " + foundStudent.id;
                
                document.getElementById('studentFinanceCardSection').style.display = "none";
                document.getElementById('studentBentoGridSection').style.display = "none";
                document.getElementById('studentAlertNotification').style.display = "none";
                document.getElementById('studentQRCardSection').style.display = "none"; // حجب الهوية عن ولي الأمر
                
                const logoutBtn = document.getElementById('btnStudentLogout');
                logoutBtn.innerHTML = `<i class="fa-solid fa-arrow-right"></i> إنهاء المتابعة والأمان`;
                
                renderStudentDataToDashboard(foundStudent);
                navigateTo('studentDashboard');
                showToast(`👨‍👩‍👦 تم الدخول بوضع المتابعة للابن ${foundStudent.name}`, "success");
            } else {
                showToast("❌ كود الطالب (الابن) غير مسجل في النظام!", "error");
            }
        }

        function verifyStudentLogin() {
            const studentId = document.getElementById('studentIdInput').value.trim();
            const foundStudent = distributedAccounts.find(acc => acc.type === 'student' && acc.id === studentId);
            if(foundStudent) {
                isParentMode = false;
                document.getElementById('displayStudentName').innerText = foundStudent.name;
                document.getElementById('displayStudentId').innerText = "كود الطالب الدراسي: " + foundStudent.id;
                
                document.getElementById('studentFinanceCardSection').style.display = "block";
                document.getElementById('studentBentoGridSection').style.display = "block";
                document.getElementById('studentAlertNotification').style.display = "block";
                document.getElementById('studentQRCardSection').style.display = "block";

                // 🪪 توليد الـ QR الخاص بالطالب تلقائياً داخل الحاوية
                document.getElementById('qrcodeCanvas').innerHTML = "";
                new QRCode(document.getElementById("qrcodeCanvas"), {
                    text: foundStudent.id,
                    width: 140,
                    height: 140,
                    colorDark : "#2d3748",
                    colorLight : "#ffffff",
                    correctLevel : QRCode.CorrectLevel.H
                });

                if(foundStudent.finance) {
                    document.getElementById('stuFinTotal').innerText = parseInt(foundStudent.finance.total).toLocaleString() + " د.ع";
                    document.getElementById('stuFinPaid').innerText = parseInt(foundStudent.finance.paid).toLocaleString() + " د.ع";
                    document.getElementById('stuFinDue').innerText = parseInt(foundStudent.finance.remaining).toLocaleString() + " د.ع";
                }
                
                renderStudentDataToDashboard(foundStudent);
                buildStudentAlertsUI(foundStudent.coursesList || []); 
                updateSubjectBadgesCount();     
                navigateTo('studentDashboard');
            } else {
                showToast("❌ كود الطالب غير صحيح!", "error");
            }
        }

        function logoutStudent() {
            if(isParentMode) {
                navigateTo('parentPage');
                showToast("🔒 تم إنهاء وضع المتابعة الأبوية", "info");
            } else {
                navigateTo('mainPage');
                showToast("🔒 تم تسجيل خروج الطالب بأمان", "info");
            }
        }

        function renderStudentDataToDashboard(studentObj) {
            const loopsContainer = document.getElementById('studentCoursesLoop');
            loopsContainer.innerHTML = "";
            let listCourses = studentObj.coursesList || [];
            if(listCourses.length === 0) {
                loopsContainer.innerHTML = `<div style="text-align: center; color: var(--text-muted); font-size:11px; padding:10px;">لا توجد دورات مسجلة حالياً.</div>`;
            } else {
                listCourses.forEach(c => {
                    loopsContainer.innerHTML += `
                        <div class="course-loop-item">
                            <div style="font-size: 12px; font-weight: 800; color: #0369a1; margin-bottom:4px;">💻 ${c.name}</div>
                            <div class="schedule-row">
                                <div class="schedule-box-item" style="background:#e0f2fe; color:#0369a1;">أستاذ الدورة<p style="font-size:10px;">${c.teacher}</p></div>
                                <div class="schedule-box-item" style="background:#f0fdf4; color:#166534;">الأيام<p style="font-size:10px;">${c.date}</p></div>
                                <div class="schedule-box-item" style="background:#fff7ed; color:#9a3412;">الوقت<p style="font-size:10px;">${c.time}</p></div>
                            </div>
                        </div>
                    `;
                });
            }

            const gradesContainer = document.getElementById('studentGradesLoop');
            gradesContainer.innerHTML = "";
            let filteredGrades = studentGradesDatabase.filter(g => g.studentId === studentObj.id);
            if(filteredGrades.length === 0) {
                gradesContainer.innerHTML = `<div style="text-align: center; color: var(--text-muted); font-size:11px; padding:10px;">لا توجد درجات مرصودة لهذا الطالب حتى الآن.</div>`;
            } else {
                filteredGrades.forEach(g => {
                    let badgeColor = g.score >= 50 ? '#10b981' : '#ef4444'; 
                    gradesContainer.innerHTML += `
                        <div class="course-loop-item" style="border-right: 4px solid ${badgeColor};">
                            <div style="display:flex; justify-content:space-between; align-items:center;">
                                <div style="font-size: 12px; font-weight: 700; color: #2d3748;">📝 ${g.title}</div>
                                <div style="font-size: 14px; font-weight: 800; color: ${badgeColor};">${g.score} / 100</div>
                            </div>
                            <div style="font-size:10px; color:var(--text-muted); margin-top:4px;">بإشراف: ${g.teacherName} | التاريخ: ${g.date}</div>
                        </div>
                    `;
                });
            }
        }

        function buildStudentAlertsUI(studentCourses) {
            const container = document.getElementById('alertScrollContainer');
            container.innerHTML = "";
            if(studentCourses.length === 0) {
                container.innerHTML = `<div class="alert-item-node">لا توجد تنبيهات جديدة.</div>`;
            } else {
                studentCourses.forEach(c => { container.innerHTML += `<div class="alert-item-node">🔔 مثبت بدورة: <strong>${c.name}</strong></div>`; });
            }
        }

        function updateSubjectBadgesCount() {
            ['الكيمياء', 'الرياضيات', 'الفيزياء', 'الأحياء', 'اللغة العربية', 'اللغة الإنكليزية', 'التربية الإسلامية'].forEach(sub => {
                const count = globalLecturesDatabase.filter(lec => lec.subject === sub).length;
                const badgeElement = document.getElementById(`badge-count-${sub}`);
                if(badgeElement) {
                    if(count > 0) {
                        badgeElement.innerHTML = `<span style="color:#10b981;"><i class="fa-solid fa-circle-check"></i> متوفر (${count}) محتوى</span>`;
                    } else {
                        if(sub === 'الكيمياء') badgeElement.innerText = "المحاضرات، الملازم والوزاريات";
                        else if(sub === 'الرياضيات') badgeElement.innerText = "الفصول والدروس";
                        else if(sub === 'الفيزياء') badgeElement.innerText = "الدروس والتجارب";
                        else if(sub === 'الأحياء') badgeElement.innerText = "الرسومات والأنسجة";
                        else if(sub === 'اللغة العربية') badgeElement.innerText = "القواعد والأدب";
                        else if(sub === 'اللغة الإنكليزية') badgeElement.innerText = "القطع والقواعد";
                        else if(sub === 'التربية الإسلامية') badgeElement.innerText = "الأحكام والوزاريات";
                    }
                }
            });
        }

        function openSubject(subjectName) {
            const titleBox = document.getElementById('selectedSubjectTitle');
            const viewerBox = document.getElementById('studentContentViewer');
            titleBox.style.display = "block"; viewerBox.style.display = "block";
            titleBox.innerHTML = `محتويات مادة ${subjectName}:`;
            const filtered = globalLecturesDatabase.filter(lec => lec.subject === subjectName);
            if(filtered.length === 0) {
                viewerBox.innerHTML = `<div style="text-align:center; color:var(--text-muted); font-size:12px; padding:10px;">لا توجد محاضرات حالياً لهذه المادة.</div>`;
                return;
            }
            viewerBox.innerHTML = "";
            filtered.forEach(lec => {
                viewerBox.innerHTML += `
                    <div class="lecture-card-item">
                        <h4>${lec.title}</h4>
                        <p>الأستاذ: ${lec.teacherName}</p>
                        <div class="lecture-links">
                            ${lec.videoUrl !== "#" ? `<a href="${lec.videoUrl}" target="_blank" class="link-vid"><i class="fa-solid fa-video"></i> مشاهدة المحاضرة</a>` : ''}
                            ${lec.pdfUrl !== "#" ? `<a href="${lec.pdfUrl}" target="_blank" class="link-pdf"><i class="fa-solid fa-file-pdf"></i> تحميل الملزمة</a>` : ''}
                            ${lec.examUrl !== "#" ? `<a href="${lec.examUrl}" target="_blank" class="link-exam"><i class="fa-solid fa-graduation-cap"></i> الاختبار / الوزاريات</a>` : ''}
                        </div>
                    </div>
                `;
            });
        }

        function showToast(message, type = "info") {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = `toast-notification toast-${type}`;
            
            let icon = "💡";
            if(type === "success") icon = "✨";
            if(type === "error") icon = "⚠️";
            
            toast.innerHTML = `<span>${icon}</span> <span>${message}</span>`;
            container.appendChild(toast);
            
            setTimeout(() => {
                toast.style.animation = "fadeIn 0.3s ease-in reverse forwards";
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>

