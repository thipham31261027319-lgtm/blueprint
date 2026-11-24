[blueprintctdueh.html](https://github.com/user-attachments/files/35323585/blueprintctdueh.html)
<!DOCTYPE html>
<html lang="vi" class="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>BLUEPRINT — UEH CTD Career, Assessment &amp; Mentorship Ecosystem</title>

  <!-- Google Fonts: Plus Jakarta Sans & JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@500;600;700&family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet" />

  <!-- Supabase JS v2 SDK (Real UEH Student OTP & OAuth SSO) -->
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'system-ui', 'sans-serif'],
            mono: ['"JetBrains Mono"', 'monospace'],
          },
          colors: {
            ueh: {
              50: '#eff6ff',
              100: '#dbeafe',
              200: '#bfdbfe',
              300: '#93c5fd',
              400: '#60a5fa',
              500: '#3b82f6',
              600: '#2563eb',
              700: '#1d4ed8',
              800: '#1e40af',
              900: '#1e3a8a',
              950: '#172554',
            }
          },
          boxShadow: {
            'card': '0 4px 20px -2px rgba(15, 23, 42, 0.05), 0 1px 3px 0 rgba(15, 23, 42, 0.03)',
            'blue-glow': '0 10px 28px -6px rgba(37, 99, 235, 0.35)',
          }
        }
      }
    };
  </script>

  <style>
    /* Clean Figma Cool-Sky Canvas Background */
    .figma-canvas {
      background-color: #f3f6fc;
      background-image:
        radial-gradient(at 0% 0%, rgba(37, 99, 235, 0.06) 0px, transparent 48%),
        radial-gradient(at 100% 0%, rgba(59, 130, 246, 0.05) 0px, transparent 48%);
    }
    .dark .figma-canvas {
      background-color: #0b1120;
      background-image:
        radial-gradient(at 0% 0%, rgba(37, 99, 235, 0.14) 0px, transparent 50%),
        radial-gradient(at 100% 0%, rgba(79, 70, 229, 0.12) 0px, transparent 50%);
    }

    /* Smooth View Transitions */
    .view-section {
      animation: fadeSlideUp 0.25s cubic-bezier(0.16, 1, 0.3, 1);
    }
    @keyframes fadeSlideUp {
      from {
        opacity: 0;
        transform: translateY(8px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    /* Likert Circle Transitions */
    .likert-btn {
      transition: transform 0.18s cubic-bezier(0.34, 1.56, 0.64, 1);
    }
    .likert-btn:hover {
      transform: scale(1.08);
    }
    .likert-btn:active {
      transform: scale(0.95);
    }

    /* Hide Scrollbar on Horizontal Filter Pills */
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
  </style>
</head>
<body class="figma-canvas font-sans text-slate-800 dark:text-slate-100 antialiased min-h-screen flex flex-col selection:bg-ueh-600 selection:text-white">

  <!-- ===================================================================== -->
  <!-- TOP HEADER BAR (MATCHING FIGMA TOP BAR ACROSS ALL 5 SCREENS)          -->
  <!-- ===================================================================== -->
  <header id="mainAppHeader" class="sticky top-0 z-40 backdrop-blur-md bg-white/90 dark:bg-slate-900/90 border-b border-slate-200/80 dark:border-slate-800 transition-colors">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 h-14 sm:h-16 flex items-center justify-between gap-2">
      <!-- Left: Brand Logo (Matching Figma Screen 2, 4, 5) -->
      <div class="flex items-center gap-2.5 cursor-pointer" onclick="handleBrandClick()">
        <div class="w-8 h-8 sm:w-9 sm:h-9 rounded-xl bg-gradient-to-br from-ueh-500 to-ueh-700 flex items-center justify-center text-white shadow-blue-glow shrink-0">
          <svg class="w-4 h-4 sm:w-5 sm:h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 3L4 20h3.5l1.6-3.6h5.8L16.5 20H20L12 3z" />
            <path d="M9.8 13.2h4.4" />
            <circle cx="12" cy="8.2" r="1" fill="currentColor" />
          </svg>
        </div>
        <div class="flex items-center gap-1.5">
          <span class="font-extrabold tracking-tight text-slate-900 dark:text-white text-base sm:text-lg">BLUEPRINT</span>
          <span class="px-1.5 py-0.5 text-[10px] font-mono font-bold rounded bg-ueh-100 text-ueh-700 dark:bg-ueh-900/60 dark:text-ueh-300">CTD</span>
        </div>
      </div>

      <!-- Center Desktop Navigation Tabs (Visible when logged in) -->
      <nav id="desktopNav" class="hidden lg:flex items-center gap-1 bg-slate-100/90 dark:bg-slate-800/90 p-1 rounded-xl border border-slate-200/70 dark:border-slate-700/70">
        <button onclick="switchTab('dashboard')" data-tab="dashboard" class="nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5">
          <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/></svg>
          <span data-i18n="navOverview">AI Match</span>
        </button>
        <button onclick="switchTab('profile')" data-tab="profile" class="nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5">
          <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
          <span data-i18n="navProfile">Hồ sơ CTD</span>
        </button>
        <button onclick="switchTab('mbti')" data-tab="mbti" class="nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5">
          <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2a7 7 0 0 1 7 7c0 2.38-1.19 4.47-3 5.74V17a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2v-2.26C6.19 13.47 5 11.38 5 9a7 7 0 0 1 7-7z"/><path d="M9 21h6"/></svg>
          <span data-i18n="navMbti">MBTI Test</span>
        </button>
        <button onclick="switchTab('simulation')" data-tab="simulation" class="nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5">
          <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg>
          <span data-i18n="navSimulation">Simulation</span>
        </button>
        <button onclick="switchTab('community')" data-tab="community" class="nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5">
          <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
          <span data-i18n="navCommunity">Cohort &amp; Mentor</span>
        </button>
      </nav>

      <!-- Right Controls: VI/EN Pill, Theme Sun/Moon Pill, Student Avatar -->
      <div class="flex items-center gap-2">
        <!-- Bilingual Pill (Figma Exact) -->
        <div class="flex items-center bg-slate-100 dark:bg-slate-800 p-0.5 rounded-full border border-slate-200/90 dark:border-slate-700 text-[11px] font-extrabold">
          <button id="langViBtn" onclick="setLanguage('vi')" class="px-2.5 py-1 rounded-full transition-all bg-ueh-600 text-white shadow-sm">VI</button>
          <button id="langEnBtn" onclick="setLanguage('en')" class="px-2.5 py-1 rounded-full transition-all text-slate-500 dark:text-slate-300">EN</button>
        </div>

        <!-- Theme Pill (Figma Exact) -->
        <button id="themeToggleBtn" onclick="toggleTheme()" class="flex items-center gap-1 px-2.5 py-1.5 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs font-bold text-slate-700 dark:text-slate-200 shadow-sm hover:border-ueh-400 transition-all">
          <span id="themeIcon">☀️</span>
          <span id="themeLabel" class="hidden sm:inline" data-i18n="themeLight">Sáng</span>
        </button>

        <!-- Student Avatar & Logout (When Logged In) -->
        <div id="headerUserArea" class="hidden items-center gap-1.5">
          <button onclick="switchTab('profile')" class="flex items-center gap-2 bg-ueh-50 dark:bg-slate-800 border border-ueh-200/80 dark:border-slate-700 rounded-full p-0.5 pr-2.5 hover:bg-ueh-100 transition-colors">
            <div id="headerAvatarCircle" class="w-7 h-7 rounded-full bg-gradient-to-tr from-ueh-600 to-indigo-500 text-white text-[11px] font-extrabold flex items-center justify-center">LN</div>
            <span id="headerStudentName" class="text-xs font-bold text-slate-800 dark:text-slate-100 hidden md:inline">Lê Minh Ngọc</span>
          </button>
          <button onclick="logoutUser()" data-i18n-title="logoutTitle" title="Đăng xuất" class="p-1.5 rounded-full text-slate-400 hover:text-rose-500 hover:bg-rose-50 dark:hover:bg-rose-950/40 transition-colors">
            <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
          </button>
        </div>
      </div>
    </div>
  </header>

  <!-- ===================================================================== -->
  <!-- MAIN CONTENT WORKSPACE                                                -->
  <!-- ===================================================================== -->
  <main class="flex-1 max-w-6xl w-full mx-auto px-4 sm:px-6 py-5 sm:py-7 pb-24 lg:pb-12">

    <!-- =================================================================== -->
    <!-- SCREEN 1: AUTH / LOGIN WITH REAL UEH MSSV + OTP & SSO (FIGMA 1)     -->
    <!-- =================================================================== -->
    <section id="view-auth" class="view-section max-w-5xl mx-auto">
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

        <!-- Left / Top Column: Figma Brand Hero + White Login Card -->
        <div class="lg:col-span-6 space-y-5">
          <!-- Figma Screen 1 Centered Brand Hero -->
          <div class="text-center space-y-2.5 pt-1">
            <div class="w-16 h-16 mx-auto rounded-2xl bg-gradient-to-br from-ueh-500 via-ueh-600 to-ueh-700 flex items-center justify-center text-white shadow-blue-glow border border-white/25">
              <svg class="w-9 h-9" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.3" stroke-linecap="round" stroke-linejoin="round">
                <path d="M12 3L4 20h3.5l1.6-3.6h5.8L16.5 20H20L12 3z" />
                <path d="M9.8 13.2h4.4" />
                <circle cx="12" cy="8.2" r="1.2" fill="currentColor" />
              </svg>
            </div>

            <div>
              <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-ueh-100/90 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 text-[10px] font-extrabold tracking-wider uppercase">
                <span class="w-1.5 h-1.5 rounded-full bg-ueh-600"></span>
                UEH COLLEGE OF TECHNOLOGY AND DESIGN
              </span>
            </div>

            <h1 class="text-3xl font-extrabold tracking-tight text-slate-900 dark:text-white">BLUEPRINT</h1>
            <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400" data-i18n="authSubtitle">
              Định hình tương lai nghề nghiệp với Trí tuệ Nhân tạo
            </p>
          </div>

          <!-- Figma Screen 1 White Auth Card -->
          <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 sm:p-7 shadow-card border border-slate-200/80 dark:border-slate-800 space-y-4">
            <!-- Segmented Tab: Đăng nhập | Đăng ký -->
            <div class="grid grid-cols-2 bg-slate-100 dark:bg-slate-800 p-1 rounded-xl">
              <button id="authTabLogin" type="button" onclick="setAuthMode('login')" data-i18n="authLoginTab" class="py-2 rounded-lg text-xs sm:text-sm font-bold bg-white dark:bg-slate-900 text-ueh-600 dark:text-ueh-400 shadow-sm transition-all">
                Đăng nhập
              </button>
              <button id="authTabRegister" type="button" onclick="setAuthMode('register')" data-i18n="authRegisterTab" class="py-2 rounded-lg text-xs sm:text-sm font-semibold text-slate-500 dark:text-slate-400 transition-all">
                Đăng ký
              </button>
            </div>

            <!-- Primary UEH SSO Button (Figma Exact) -->
            <div class="space-y-1.5">
              <button type="button" onclick="loginWithUEHOAuth('azure')" class="w-full py-3 px-4 rounded-xl bg-gradient-to-r from-ueh-600 to-ueh-700 hover:from-ueh-700 hover:to-ueh-800 text-white font-bold text-xs sm:text-sm shadow-blue-glow flex items-center justify-center gap-2 transition-all">
                <svg class="w-4 h-4 shrink-0" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><rect x="3" y="4" width="18" height="16" rx="2"/><path d="M3 8l9 6 9-6"/></svg>
                <span data-i18n="authSsoBtn">Đăng nhập với Email UEH</span>
                <span>→</span>
              </button>
              <div class="text-center text-[11px] text-slate-400 flex items-center justify-center gap-1">
                <span>🔒</span>
                <span data-i18n="authSsoSub">Cổng chứng thực sinh viên trực tuyến CTD</span>
              </div>
            </div>

            <!-- Divider -->
            <div class="flex items-center gap-3">
              <div class="h-px flex-1 bg-slate-200 dark:bg-slate-800"></div>
              <span class="text-[11px] font-semibold text-slate-400" data-i18n="authDividerOtp">Hoặc xác thực MSSV &amp; Email UEH</span>
              <div class="h-px flex-1 bg-slate-200 dark:bg-slate-800"></div>
            </div>

            <!-- STEP 1: MSSV + Email @st.ueh.edu.vn Verification Form -->
            <form id="uehStep1Form" onsubmit="handleSendUehOtpSubmit(event)" class="space-y-3.5">
              <div id="registerNameWrap" class="hidden">
                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 mb-1" data-i18n="authFullNameLabel">Họ và tên sinh viên</label>
                <input id="authFullName" type="text" data-i18n-placeholder="authFullNamePlaceholder" placeholder="VD: Lê Minh Ngọc" oninput="handleLiveUehInput()" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-sm focus:outline-none focus:ring-2 focus:ring-ueh-500" />
              </div>

              <div>
                <div class="flex items-center justify-between mb-1">
                  <label for="authMssvInput" class="block text-xs font-bold text-slate-700 dark:text-slate-300" data-i18n="authMssvLabel">Mã sinh viên (MSSV)</label>
                </div>
                <input id="authMssvInput" type="text" inputmode="numeric" maxlength="11" value="" oninput="handleLiveUehInput()" placeholder="3123102xxxx" required class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-sm font-mono font-semibold focus:outline-none focus:ring-2 focus:ring-ueh-500" />
              </div>

              <div>
                <label for="authUehEmailInput" class="block text-xs font-bold text-slate-700 dark:text-slate-300 mb-1" data-i18n="authEmailLabel">Email sinh viên UEH</label>
                <input id="authUehEmailInput" type="email" value="" oninput="handleLiveUehInput()" placeholder="ten.3123102xxxx@st.ueh.edu.vn" required class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-sm font-mono focus:outline-none focus:ring-2 focus:ring-ueh-500" />
              </div>

              <!-- Live Student ID Verification Badge -->
              <div id="uehLiveValidationBox" class="p-2.5 rounded-xl bg-ueh-50/90 dark:bg-ueh-950/40 border border-ueh-200/80 dark:border-ueh-800/60 text-xs flex items-start gap-2">
                <span id="uehLiveStatusIcon" class="text-ueh-600 font-extrabold mt-0.5">i</span>
                <div id="uehLiveStatusContent" class="space-y-0.5">
                  <div class="font-bold text-ueh-800 dark:text-ueh-300">Nhập MSSV &amp; Email sinh viên UEH để xác thực</div>
                  <div class="text-[11px] text-ueh-700 dark:text-ueh-400">Hệ thống tự động kiểm tra định dạng 11 chữ số và đối chiếu hộp thư @st.ueh.edu.vn.</div>
                </div>
              </div>

              <div class="flex items-center justify-between text-xs pt-0.5">
                <label class="flex items-center gap-1.5 text-slate-600 dark:text-slate-300 cursor-pointer">
                  <input type="checkbox" checked class="rounded border-slate-300 text-ueh-600 focus:ring-ueh-500" />
                  <span data-i18n="authRemember">Ghi nhớ đăng nhập</span>
                </label>
                <button type="button" onclick="showSupabaseSqlGuide()" data-i18n="authLiveOtpGuide" class="font-bold text-ueh-600 hover:underline">Cấu hình Live OTP?</button>
              </div>

              <button id="sendOtpSubmitBtn" type="submit" class="w-full py-3 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white font-bold text-xs sm:text-sm shadow-blue-glow transition-all flex items-center justify-center gap-2">
                <span data-i18n="authContinueBtn">Tiếp tục khám phá (Gửi OTP)</span>
                <span>→</span>
              </button>
            </form>

            <!-- STEP 2: 6-DIGIT OTP VERIFICATION -->
            <div id="uehStep2OtpView" class="hidden space-y-4">
              <div class="p-3 rounded-2xl bg-ueh-50 dark:bg-ueh-950/60 border border-ueh-200 dark:border-ueh-800 text-xs space-y-1">
                <div class="flex items-center justify-between">
                  <span class="font-extrabold text-ueh-700 dark:text-ueh-300" data-i18n="otpStepTitle">📩 Nhập mã OTP 6 số từ Email UEH</span>
                  <button type="button" onclick="backToUehEmailStep()" data-i18n="otpChangeMssv" class="text-[11px] font-bold text-ueh-600 hover:underline">Đổi MSSV</button>
                </div>
                <p class="text-slate-600 dark:text-slate-300">
                  <span data-i18n="otpSentTo">Mã xác thực đã được gửi tới</span> <strong id="maskedUehEmailLabel" class="font-mono text-slate-900 dark:text-white">mi***@st.ueh.edu.vn</strong>
                </p>
              </div>

              <!-- Sandbox Preview OTP Quick-Fill Helper -->
              <div id="sandboxOtpHelperBanner" class="hidden p-3 rounded-2xl bg-emerald-50 dark:bg-emerald-950/60 border border-emerald-300 dark:border-emerald-800 flex items-center justify-between text-xs">
                <div>
                  <div class="font-bold text-emerald-800 dark:text-emerald-300" data-i18n="otpSandboxTitle">🧪 Mã OTP Sandbox Preview:</div>
                  <div class="text-[11px] text-emerald-700 dark:text-emerald-400" data-i18n="otpSandboxHint">Nhấn vào mã bên cạnh để điền tự động.</div>
                </div>
                <button type="button" onclick="autoFillSandboxOtp()" class="px-3 py-1.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-mono font-extrabold text-sm tracking-widest shadow-sm">
                  <span id="sandboxOtpCodeDisplay">482910</span>
                </button>
              </div>

              <div class="grid grid-cols-6 gap-2 max-w-xs mx-auto" onpaste="handleOtpPaste(event)">
                <input id="otp-digit-0" type="text" inputmode="numeric" maxlength="1" oninput="handleOtpDigitInput(0, this)" onkeydown="handleOtpKeyDown(0, event)" class="w-full h-11 text-center text-base font-mono font-extrabold rounded-xl bg-slate-50 dark:bg-slate-800 border-2 border-slate-200 dark:border-slate-700 focus:border-ueh-600 focus:outline-none" />
                <input id="otp-digit-1" type="text" inputmode="numeric" maxlength="1" oninput="handleOtpDigitInput(1, this)" onkeydown="handleOtpKeyDown(1, event)" class="w-full h-11 text-center text-base font-mono font-extrabold rounded-xl bg-slate-50 dark:bg-slate-800 border-2 border-slate-200 dark:border-slate-700 focus:border-ueh-600 focus:outline-none" />
                <input id="otp-digit-2" type="text" inputmode="numeric" maxlength="1" oninput="handleOtpDigitInput(2, this)" onkeydown="handleOtpKeyDown(2, event)" class="w-full h-11 text-center text-base font-mono font-extrabold rounded-xl bg-slate-50 dark:bg-slate-800 border-2 border-slate-200 dark:border-slate-700 focus:border-ueh-600 focus:outline-none" />
                <input id="otp-digit-3" type="text" inputmode="numeric" maxlength="1" oninput="handleOtpDigitInput(3, this)" onkeydown="handleOtpKeyDown(3, event)" class="w-full h-11 text-center text-base font-mono font-extrabold rounded-xl bg-slate-50 dark:bg-slate-800 border-2 border-slate-200 dark:border-slate-700 focus:border-ueh-600 focus:outline-none" />
                <input id="otp-digit-4" type="text" inputmode="numeric" maxlength="1" oninput="handleOtpDigitInput(4, this)" onkeydown="handleOtpKeyDown(4, event)" class="w-full h-11 text-center text-base font-mono font-extrabold rounded-xl bg-slate-50 dark:bg-slate-800 border-2 border-slate-200 dark:border-slate-700 focus:border-ueh-600 focus:outline-none" />
                <input id="otp-digit-5" type="text" inputmode="numeric" maxlength="1" oninput="handleOtpDigitInput(5, this)" onkeydown="handleOtpKeyDown(5, event)" class="w-full h-11 text-center text-base font-mono font-extrabold rounded-xl bg-slate-50 dark:bg-slate-800 border-2 border-slate-200 dark:border-slate-700 focus:border-ueh-600 focus:outline-none" />
              </div>

              <button id="verifyOtpSubmitBtn" type="button" onclick="handleVerifyOtpClick()" data-i18n="otpVerifyBtn" class="w-full py-3 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white font-bold text-xs sm:text-sm shadow-blue-glow transition-all">
                ✓ Xác nhận OTP &amp; Vào BLUEPRINT
              </button>

              <div class="flex items-center justify-between text-xs">
                <span id="otpCountdownText" class="text-slate-400 font-mono">Gửi lại mã sau: 60s</span>
                <button id="resendOtpBtn" type="button" onclick="resendUehOtp()" disabled data-i18n="otpResendBtn" class="font-bold text-ueh-600 disabled:opacity-40 hover:underline">Gửi lại mã</button>
              </div>
            </div>

            <!-- Divider & Social Quick Login (Figma Screen 1 Bottom) -->
            <div class="space-y-2.5 pt-1">
              <div class="flex items-center gap-3">
                <div class="h-px flex-1 bg-slate-200 dark:bg-slate-800"></div>
                <span class="text-[11px] font-semibold text-slate-400" data-i18n="authQuickLogin">Đăng nhập nhanh với</span>
                <div class="h-px flex-1 bg-slate-200 dark:bg-slate-800"></div>
              </div>
              <div class="grid grid-cols-2 gap-2.5">
                <button type="button" onclick="loginWithUEHOAuth('google')" class="py-2.5 px-3 rounded-xl border border-slate-200 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-800 text-xs font-bold flex items-center justify-center gap-2 transition-colors">
                  <span class="text-rose-500 font-extrabold">G</span>
                  <span>Google</span>
                </button>
                <button type="button" onclick="loginWithUEHOAuth('apple')" class="py-2.5 px-3 rounded-xl border border-slate-200 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-800 text-xs font-bold flex items-center justify-center gap-2 transition-colors">
                  <span></span>
                  <span>Apple ID</span>
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Right / Bottom Column: Figma "Đặc quyền Sinh viên CTD UEH" Blue Card -->
        <div class="lg:col-span-6 lg:pt-12 space-y-5">
          <div class="bg-gradient-to-br from-ueh-600 via-ueh-700 to-ueh-900 rounded-3xl p-6 sm:p-7 text-white shadow-blue-glow space-y-4">
            <div class="flex items-start gap-3">
              <div class="w-10 h-10 rounded-xl bg-white/15 flex items-center justify-center text-lg shrink-0">🎓</div>
              <div>
                <h2 class="font-extrabold text-base sm:text-lg" data-i18n="perksBadge">Đặc quyền Sinh viên CTD UEH</h2>
                <p class="text-xs text-ueh-100/90" data-i18n="perksSub">Hành trang định hướng sự nghiệp cá nhân hóa</p>
              </div>
            </div>

            <div class="space-y-3">
              <!-- Perk 1 -->
              <div class="p-3.5 rounded-2xl bg-white/10 backdrop-blur-sm border border-white/15 flex items-start gap-3">
                <div class="w-8 h-8 rounded-xl bg-white/15 flex items-center justify-center text-sm shrink-0">🧭</div>
                <div class="text-xs">
                  <div class="font-bold" data-i18n="perk1Title">Trắc nghiệm MBTI &amp; Holland chuẩn quốc tế</div>
                  <p class="text-ueh-100/85 text-[11px] mt-0.5" data-i18n="perk1Desc">Đo lường năng lực và tính cách nghề nghiệp chuẩn hóa theo định hướng Typologytesting.</p>
                </div>
              </div>

              <!-- Perk 2 -->
              <div class="p-3.5 rounded-2xl bg-white/10 backdrop-blur-sm border border-white/15 flex items-start gap-3">
                <div class="w-8 h-8 rounded-xl bg-white/15 flex items-center justify-center text-sm shrink-0">💼</div>
                <div class="text-xs">
                  <div class="font-bold" data-i18n="perk2Title">Mô phỏng nhiệm vụ nghề thực tế &amp; Xử lý tình huống</div>
                  <p class="text-ueh-100/85 text-[11px] mt-0.5" data-i18n="perk2Desc">Phân tích điểm mạnh/yếu khi đối mặt khách hàng khó tính và đo lường % Job Fit.</p>
                </div>
              </div>

              <!-- Perk 3 -->
              <div class="p-3.5 rounded-2xl bg-white/10 backdrop-blur-sm border border-white/15 flex items-start gap-3">
                <div class="w-8 h-8 rounded-xl bg-white/15 flex items-center justify-center text-sm shrink-0">🤝</div>
                <div class="text-xs">
                  <div class="font-bold" data-i18n="perk3Title">Cộng đồng Nhỏ (10–20 SV) &amp; Cố vấn Mentor</div>
                  <p class="text-ueh-100/85 text-[11px] mt-0.5" data-i18n="perk3Desc">Ghép nhóm cùng các bạn đồng mục tiêu dưới sự dẫn dắt trực tiếp của Phó Giáo sư &amp; Chuyên gia.</p>
                </div>
              </div>
            </div>

            <div class="pt-2 border-t border-white/15 flex items-center justify-between text-[11px] text-ueh-100">
              <span id="authConnectionModeText" data-i18n="authReadyStatus">● Sẵn sàng xác thực MSSV &amp; Email @st.ueh.edu.vn</span>
              <button type="button" onclick="showSupabaseSqlGuide()" class="font-mono font-bold underline">Supabase SQL</button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- =================================================================== -->
    <!-- SCREEN 2: HỒ SƠ SINH VIÊN CTD (FIGMA SCREEN 2 EXACT LAYOUT)         -->
    <!-- =================================================================== -->
    <section id="view-profile" class="view-section hidden max-w-2xl mx-auto space-y-5">
      <!-- Top Step & Title (Figma Screen 2) -->
      <div class="space-y-1.5">
        <div class="inline-flex items-center gap-1.5 text-[11px] font-extrabold uppercase tracking-wider text-ueh-600 dark:text-ueh-400">
          <span class="w-2 h-2 rounded-full bg-ueh-600"></span>
          <span data-i18n="profStepTag">BƯỚC 1/2 • KHỞI TẠO NĂNG LỰC CTD</span>
        </div>
        <h1 class="text-2xl sm:text-3xl font-extrabold text-slate-900 dark:text-white tracking-tight" data-i18n="profTitle">Hồ sơ Sinh viên CTD</h1>
        <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400" data-i18n="profSubtitle">
          Chọn chuyên ngành và kỹ năng hiện tại để AI BLUEPRINT cá nhân hóa lộ trình nghề nghiệp.
        </p>
      </div>

      <!-- Student Identity Badge Card (Figma Screen 2) -->
      <div class="bg-white dark:bg-slate-900 rounded-2xl p-4 border border-slate-200/80 dark:border-slate-800 shadow-card flex items-center gap-3.5">
        <div class="relative shrink-0">
          <div id="profileCardAvatar" class="w-12 h-12 rounded-full bg-gradient-to-br from-ueh-500 to-indigo-600 text-white font-extrabold text-sm flex items-center justify-center shadow">LN</div>
          <span class="absolute -bottom-0.5 -right-0.5 w-4 h-4 rounded-full bg-ueh-600 text-white text-[9px] flex items-center justify-center ring-2 ring-white dark:ring-slate-900">✓</span>
        </div>
        <div class="min-w-0 flex-1">
          <div class="flex flex-wrap items-center gap-1.5">
            <span id="profileCardName" class="font-extrabold text-sm sm:text-base text-slate-900 dark:text-white">Lê Minh Ngọc</span>
            <span class="w-4 h-4 rounded-full bg-ueh-600 text-white text-[9px] inline-flex items-center justify-center">✓</span>
          </div>
          <div class="flex flex-wrap items-center gap-1.5 mt-0.5">
            <span id="profileCohortBadge" class="px-2 py-0.5 rounded bg-ueh-100 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 font-mono text-[10px] font-bold">K49 CTD</span>
            <span id="profileCardMeta" class="text-[11px] font-mono text-slate-500">MSSV: 31231024567</span>
          </div>
          <div id="profileCardEmail" class="text-[11px] text-slate-400 truncate mt-0.5">Trường Công nghệ và Thiết kế UEH • minhngoc.31231024567@st.ueh.edu.vn</div>
        </div>
      </div>

      <!-- Section 1: Chuyên ngành của bạn tại CTD (5 Major Cards from Figma) -->
      <div class="space-y-2.5">
        <div class="flex items-center justify-between">
          <h2 class="text-sm font-extrabold text-slate-900 dark:text-white" data-i18n="profMajorHeading">• Chuyên ngành của bạn tại CTD</h2>
          <span class="text-xs font-bold text-ueh-600" data-i18n="profPickOne">Chọn 1 ngành</span>
        </div>
        <div id="majorCardsList" class="space-y-2.5">
          <!-- Populated dynamically -->
        </div>
      </div>

      <!-- Section 2: Kỹ năng & Điểm mạnh sở trường (Figma Pills + Tip) -->
      <div class="space-y-2.5">
        <div class="flex items-center justify-between">
          <h2 class="text-sm font-extrabold text-slate-900 dark:text-white" data-i18n="profSkillsHeading">• Kỹ năng &amp; Điểm mạnh sở trường</h2>
          <span class="text-xs font-semibold text-slate-400" data-i18n="profPickMany">Chọn nhiều kỹ năng</span>
        </div>
        <div id="skillPillsList" class="flex flex-wrap gap-2">
          <!-- Populated dynamically -->
        </div>
        <p class="text-[11px] text-slate-400 flex items-center gap-1.5 pt-0.5">
          <span>💡</span>
          <span data-i18n="profSkillTip">Chọn ít nhất 3 kỹ năng để AI đánh giá chính xác độ tương thích công việc.</span>
        </p>
      </div>

      <!-- Section 3: Mục tiêu sau tốt nghiệp (Figma 3 Cards) -->
      <div class="space-y-2.5">
        <div class="flex items-center justify-between">
          <h2 class="text-sm font-extrabold text-slate-900 dark:text-white" data-i18n="profGoalsHeading">• Mục tiêu sau tốt nghiệp</h2>
          <span class="text-xs font-bold text-ueh-600" data-i18n="profPriorityOne">Ưu tiên số 1</span>
        </div>
        <div id="goalCardsList" class="space-y-2.5">
          <!-- Populated dynamically -->
        </div>
      </div>

      <!-- Sync Info Box (Figma Screen 2) -->
      <div class="p-3.5 rounded-2xl bg-ueh-50/90 dark:bg-ueh-950/60 border border-ueh-200/80 dark:border-ueh-800/70 flex items-start gap-2.5 text-xs text-slate-600 dark:text-slate-300">
        <span class="w-5 h-5 rounded-full bg-ueh-600 text-white text-[11px] font-bold flex items-center justify-center shrink-0 mt-0.5">i</span>
        <span data-i18n="profSyncNote">Dữ liệu chuyên ngành sẽ được đồng bộ hóa trực tiếp với đề xuất nghề nghiệp từ Viện UEH CTD</span>
      </div>

      <!-- Primary Save CTA + Skip Link (Figma Screen 2) -->
      <div class="space-y-2.5 text-center pt-1">
        <button onclick="saveStudentProfile()" data-i18n="profSaveBtn" class="w-full py-3.5 rounded-2xl bg-gradient-to-r from-ueh-600 to-ueh-700 hover:from-ueh-700 hover:to-ueh-800 text-white font-bold text-sm shadow-blue-glow transition-all">
          Lưu &amp; Bắt đầu làm bài test MBTI →
        </button>
        <button onclick="switchTab('dashboard')" data-i18n="profSkipBtn" class="text-xs font-semibold text-slate-400 hover:text-slate-600 dark:hover:text-slate-200">
          Bỏ qua bước này, thiết lập sau
        </button>
      </div>
    </section>

    <!-- =================================================================== -->
    <!-- SCREEN 3: MBTI PERSONALITY TEST (FIGMA SCREEN 3 EXACT LAYOUT)       -->
    <!-- =================================================================== -->
    <section id="view-mbti" class="view-section hidden max-w-2xl mx-auto space-y-4">
      <!-- Top Back & Counter Strip (Figma Screen 3) -->
      <div class="flex items-center justify-between">
        <button onclick="switchTab('profile')" class="inline-flex items-center gap-1.5 text-xs font-bold text-slate-600 dark:text-slate-300 hover:text-ueh-600">
          <span>←</span>
          <span data-i18n="mbtiBackBtn">Quay lại Hồ sơ</span>
        </button>
        <div class="flex items-center gap-2">
          <span id="mbtiCounter" class="text-sm font-extrabold font-mono text-slate-900 dark:text-white">Câu 1 / 12</span>
          <span class="px-2 py-0.5 rounded bg-ueh-100 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 font-mono text-[10px] font-extrabold">XAI</span>
        </div>
        <button onclick="autoCompleteMbtiDemo()" data-i18n="mbtiQuickDemo" class="text-xs font-bold text-ueh-600 hover:underline">
          Điền nhanh Demo →
        </button>
      </div>

      <!-- Progress Bar & Dimension Pill (Figma Screen 3) -->
      <div class="space-y-2">
        <div class="flex items-center justify-between text-[11px] font-semibold">
          <span id="mbtiPercentText" class="text-ueh-600 font-bold">Đã hoàn thành 8%</span>
          <span class="text-slate-400" data-i18n="mbtiSteadyPace">Tiến triển ổn định</span>
        </div>
        <div class="w-full h-2 bg-slate-200/80 dark:bg-slate-800 rounded-full overflow-hidden">
          <div id="mbtiProgressBar" class="h-full bg-ueh-600 rounded-full transition-all duration-300" style="width: 8.33%"></div>
        </div>
        <div class="pt-1">
          <span id="mbtiDimensionBadge" class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-ueh-50 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 border border-ueh-200/70 dark:border-ueh-800 text-[11px] font-bold">
            ⚡ Năng lượng &amp; Xu hướng tương tác xã hội
          </span>
        </div>
      </div>

      <!-- Main Question Card (Figma Screen 3 Exact White Card) -->
      <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 sm:p-7 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-5">
        <div class="space-y-2">
          <div class="text-[10px] font-mono font-extrabold tracking-wider text-ueh-600 uppercase">UEH CTD × BLUEPRINT MBTI MATRIX</div>
          <h2 id="mbtiQuestionVi" class="text-lg sm:text-xl font-extrabold text-slate-900 dark:text-white leading-snug">
            Khi gặp một dự án công nghệ mới, bạn có xu hướng muốn thảo luận nhóm sôi nổi ngay lập tức thay vì suy ngẫm độc lập một mình?
          </h2>
          <p id="mbtiQuestionEn" class="text-xs text-slate-400 leading-relaxed">
            When facing a new tech project, do you tend to dive into dynamic team brainstorming immediately rather than reflecting deeply on your own first?
          </p>
        </div>

        <!-- 👍 ĐỒNG Ý vs PHẢN ĐỐI 👎 + 5 Likert Circles (Figma Screen 3) -->
        <div class="space-y-3 pt-2">
          <div class="flex items-center justify-between text-[10px] font-extrabold uppercase tracking-wider px-1">
            <span class="text-ueh-600" data-i18n="mbtiAgreeSide">👍 ĐỒNG Ý</span>
            <span class="text-rose-500" data-i18n="mbtiDisagreeSide">PHẢN ĐỐI 👎</span>
          </div>

          <div class="flex items-center justify-between gap-1.5 sm:gap-3 px-1">
            <!-- +2: Rất đồng ý (Solid Blue Circle) -->
            <button type="button" onclick="selectMbtiOption(2)" data-score="2" class="likert-btn flex flex-col items-center gap-1.5 group">
              <div class="likert-circle w-12 h-12 sm:w-14 sm:h-14 rounded-full bg-ueh-600 text-white flex items-center justify-center shadow-md">
                <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6"><polyline points="20 6 9 17 4 12"/></svg>
              </div>
              <span data-i18n="likertStronglyAgree" class="text-[11px] font-bold text-ueh-600 text-center leading-tight">Rất đồng ý</span>
            </button>

            <!-- +1: Đồng ý (Outlined Blue Circle) -->
            <button type="button" onclick="selectMbtiOption(1)" data-score="1" class="likert-btn flex flex-col items-center gap-1.5 group">
              <div class="likert-circle w-10 h-10 sm:w-11 sm:h-11 rounded-full border-2 border-ueh-400 bg-ueh-50/60 dark:bg-ueh-950/50 text-ueh-600 flex items-center justify-center">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6"><polyline points="20 6 9 17 4 12"/></svg>
              </div>
              <span data-i18n="likertAgree" class="text-[11px] font-semibold text-slate-600 dark:text-slate-300 text-center leading-tight">Đồng ý</span>
            </button>

            <!-- 0: Trung lập (Neutral Grey Circle) -->
            <button type="button" onclick="selectMbtiOption(0)" data-score="0" class="likert-btn flex flex-col items-center gap-1.5 group">
              <div class="likert-circle w-8 h-8 sm:w-9 sm:h-9 rounded-full border-2 border-slate-300 dark:border-slate-600 bg-slate-100 dark:bg-slate-800 text-slate-400 flex items-center justify-center">
                <span class="text-xs font-bold">•</span>
              </div>
              <span data-i18n="likertNeutral" class="text-[11px] font-semibold text-slate-400 text-center leading-tight">Trung lập</span>
            </button>

            <!-- -1: Không đồng ý (Outlined Rose Circle) -->
            <button type="button" onclick="selectMbtiOption(-1)" data-score="-1" class="likert-btn flex flex-col items-center gap-1.5 group">
              <div class="likert-circle w-10 h-10 sm:w-11 sm:h-11 rounded-full border-2 border-rose-300 bg-rose-50/60 dark:bg-rose-950/40 text-rose-500 flex items-center justify-center">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
              </div>
              <span data-i18n="likertDisagree" class="text-[11px] font-semibold text-slate-600 dark:text-slate-300 text-center leading-tight">Không đồng ý</span>
            </button>

            <!-- -2: Hoàn toàn phản đối (Solid Rose Circle) -->
            <button type="button" onclick="selectMbtiOption(-2)" data-score="-2" class="likert-btn flex flex-col items-center gap-1.5 group">
              <div class="likert-circle w-12 h-12 sm:w-14 sm:h-14 rounded-full bg-rose-600 text-white flex items-center justify-center shadow-md">
                <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
              </div>
              <span data-i18n="likertStronglyDisagree" class="text-[11px] font-bold text-rose-600 text-center leading-tight">Hoàn toàn phản đối</span>
            </button>
          </div>

          <!-- Auto-advance toggle (Figma Screen 3) -->
          <div class="pt-1 flex justify-center">
            <label class="inline-flex items-center gap-2 text-xs text-slate-500 dark:text-slate-400 cursor-pointer">
              <input id="mbtiAutoAdvanceChk" type="checkbox" checked class="rounded border-slate-300 text-ueh-600 focus:ring-ueh-500" />
              <span data-i18n="mbtiAutoAdvance">Tự động chuyển câu sau khi chọn mức độ</span>
            </label>
          </div>
        </div>
      </div>

      <!-- Phân tích từ BLUEPRINT AI Box (Figma Screen 3) -->
      <div class="p-4 rounded-2xl bg-ueh-50/90 dark:bg-ueh-950/60 border border-ueh-200/80 dark:border-ueh-800/70 flex items-start gap-3">
        <div class="w-8 h-8 rounded-xl bg-ueh-600 text-white flex items-center justify-center text-xs font-extrabold shrink-0 mt-0.5">AI</div>
        <div class="text-xs leading-relaxed">
          <div class="font-bold text-ueh-700 dark:text-ueh-300 mb-0.5" data-i18n="mbtiAiBoxTitle">Phân tích từ BLUEPRINT AI</div>
          <p id="mbtiLiveInsight" class="text-slate-600 dark:text-slate-300">
            Hãy chọn theo phản xạ tự nhiên nhất của bạn. Không có đáp án đúng hay sai — chỉ có góc nhìn phù hợp nhất với bản sắc năng lực của bạn tại UEH CTD!
          </p>
        </div>
      </div>

      <!-- Bottom Prev / Next Buttons (Figma Screen 3) -->
      <div class="grid grid-cols-2 gap-3 pt-1">
        <button id="mbtiPrevBtn" onclick="prevMbtiQuestion()" data-i18n="mbtiPrevBtn" class="py-3 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-xs sm:text-sm font-bold text-slate-600 dark:text-slate-300 hover:bg-slate-50 disabled:opacity-40 transition-all">
          ← Câu trước
        </button>
        <button id="mbtiNextBtn" onclick="nextMbtiQuestion()" class="py-3 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white text-xs sm:text-sm font-bold shadow-blue-glow transition-all">
          Tiếp tục →
        </button>
      </div>

      <!-- MBTI Result Summary Card -->
      <div id="mbtiResultCard" class="hidden bg-white dark:bg-slate-900 rounded-3xl p-6 border border-ueh-200 dark:border-ueh-800 shadow-card space-y-5">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 pb-4 border-b border-slate-100 dark:border-slate-800">
          <div>
            <span data-i18n="mbtiDoneBadge" class="px-2.5 py-1 rounded-full bg-emerald-100 dark:bg-emerald-950 text-emerald-700 dark:text-emerald-300 text-xs font-bold">✓ Hoàn thành Đánh giá MBTI</span>
            <h3 id="mbtiResultTitle" class="text-2xl font-extrabold text-slate-900 dark:text-white mt-2">ENTP — Visionary Innovator</h3>
            <p id="mbtiResultDesc" class="text-xs text-slate-600 dark:text-slate-300 mt-1"></p>
          </div>
          <div class="flex flex-col gap-2 shrink-0">
            <button onclick="switchTab('dashboard')" data-i18n="mbtiViewMatchBtn" class="px-4 py-2.5 rounded-xl bg-ueh-600 text-white text-xs font-bold shadow-sm">
              Xem AI Match &amp; Nghề nghiệp →
            </button>
            <button onclick="resetMbtiTest()" data-i18n="mbtiRetakeBtn" class="px-4 py-2 rounded-xl border border-slate-200 dark:border-slate-700 text-xs font-semibold text-slate-500">
              Làm lại bài test
            </button>
          </div>
        </div>
        <div id="mbtiResultBars" class="grid grid-cols-1 sm:grid-cols-2 gap-3"></div>
      </div>
    </section>

    <!-- =================================================================== -->
    <!-- SCREEN 4: AI MATCH / DASHBOARD & CAREER RECOMMENDATIONS (FIGMA 4)   -->
    <!-- =================================================================== -->
    <section id="view-dashboard" class="view-section hidden space-y-6">
      <!-- Top Figma Screen 4 Hero Card: ENTP • Visionary Innovator -->
      <div class="bg-gradient-to-br from-ueh-600 via-ueh-700 to-indigo-800 rounded-3xl p-5 sm:p-7 text-white shadow-blue-glow relative overflow-hidden">
        <div class="relative z-10 space-y-4">
          <div class="flex items-center justify-between gap-2">
            <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white/15 text-[11px] font-bold">
              <span>✨</span>
              <span data-i18n="dashReportBadge">Báo cáo Chân dung Cá nhân</span>
            </span>
            <button onclick="showToast(t('toastCopiedLink'))" class="w-8 h-8 rounded-full bg-white/15 hover:bg-white/25 flex items-center justify-center text-xs transition-colors" data-i18n-title="shareProfileTitle" title="Chia sẻ hồ sơ">
              ↗
            </button>
          </div>

          <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
            <div class="space-y-1">
              <h1 id="dashArchetypeTitle" class="text-2xl sm:text-3xl font-extrabold tracking-tight">
                ENTP • Visionary Innovator
              </h1>
              <p id="dashArchetypeDesc" class="text-xs sm:text-sm text-ueh-100/90">
                Người kiến tạo tầm nhìn đa năng • Kết quả tổng hợp từ MBTI &amp; Xử lý Tình huống CTD
              </p>
            </div>

            <!-- Inner White-Tinted Gauge Pill (Exact Figma Screen 4 Visual) -->
            <div class="flex items-center gap-3.5 bg-white/15 backdrop-blur-md border border-white/20 rounded-2xl px-4 py-3 shrink-0">
              <div class="relative w-14 h-14 flex items-center justify-center shrink-0">
                <svg class="w-14 h-14 -rotate-90" viewBox="0 0 100 100">
                  <circle cx="50" cy="50" r="42" stroke="rgba(255,255,255,0.25)" stroke-width="10" fill="none" />
                  <circle id="heroFitRing" cx="50" cy="50" r="42" stroke="#ffffff" stroke-width="10" stroke-linecap="round" fill="none" stroke-dasharray="263.89" stroke-dashoffset="15.8" />
                </svg>
                <span id="heroFitPercent" class="absolute text-sm font-extrabold font-mono">94%</span>
              </div>
              <div class="text-xs">
                <div class="font-extrabold" data-i18n="dashAiCompatTitle">Chỉ số tương thích AI</div>
                <div id="dashAiCompatSubText" class="text-[11px] text-ueh-100/90">Rất cao với nhóm nghề công nghệ sáng tạo</div>
              </div>
            </div>
          </div>

          <!-- 3 Dynamic Strength Pills (Synchronized with Major, MBTI & Simulation) -->
          <div id="dashHeroPills" class="flex flex-wrap gap-2 pt-1">
            <span class="px-3 py-1 rounded-full bg-white/15 text-[11px] font-semibold">✦ Tư duy liên ngành</span>
            <span class="px-3 py-1 rounded-full bg-white/15 text-[11px] font-semibold">✦ Đột phá ý tưởng</span>
            <span class="px-3 py-1 rounded-full bg-white/15 text-[11px] font-semibold">✦ Logic &amp; Thẩm mỹ số</span>
          </div>
        </div>
      </div>

      <!-- Brief Integration Row: Problem-Solving Strengths/Weaknesses + 10-20 Cohort & Mentor -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-5">
        <!-- Strengths & Weaknesses from Difficult Client Case (7 Cols) -->
        <div class="lg:col-span-7 bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card flex flex-col justify-between space-y-3">
          <div class="flex items-center justify-between">
            <span class="text-xs font-extrabold uppercase tracking-wider text-ueh-600" data-i18n="dashBehaviorHeading">📊 Phân tích Hành vi Xử lý Tình huống</span>
            <button onclick="switchTab('simulation')" data-i18n="dashTryClientCase" class="text-xs font-bold text-ueh-600 hover:underline">Thử tình huống khách hàng →</button>
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-xs">
            <div class="p-3 rounded-2xl bg-emerald-50/80 dark:bg-emerald-950/30 border border-emerald-200/70 dark:border-emerald-800/50">
              <div class="font-bold text-emerald-700 dark:text-emerald-300 mb-1" data-i18n="dashStrengthLabel">✓ Điểm mạnh (Strengths)</div>
              <p id="dashStrengthText" class="text-slate-600 dark:text-slate-300 leading-relaxed"></p>
            </div>
            <div class="p-3 rounded-2xl bg-amber-50/80 dark:bg-amber-950/30 border border-amber-200/70 dark:border-amber-800/50">
              <div class="font-bold text-amber-700 dark:text-amber-300 mb-1" data-i18n="dashWeaknessLabel">⚠ Điểm cần rèn luyện (Weaknesses)</div>
              <p id="dashWeaknessText" class="text-slate-600 dark:text-slate-300 leading-relaxed"></p>
            </div>
          </div>
          <div class="flex items-center justify-between text-xs pt-1 border-t border-slate-100 dark:border-slate-800">
            <span class="text-slate-400" data-i18n="dashBestRoleLabel">Vị trí phù hợp nhất theo hành vi:</span>
            <span id="dashBestRoleBadge" class="font-extrabold text-ueh-600">Product Designer (94%)</span>
          </div>
        </div>

        <!-- Dynamic Mentor & Small Community (10-20 SV) Match Card (5 Cols) -->
        <div id="dashMentorSlot" class="lg:col-span-5 bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card flex flex-col justify-between space-y-3">
          <!-- Dynamically rendered based on MBTI + Simulation completion status -->
        </div>
      </div>

      <!-- Khuyến nghị Nghề nghiệp + BLUEPRINT AI Advisor (Exact Figma Screen 4 Layout) -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
        <!-- Left 8 Cols: Khuyến nghị Nghề nghiệp -->
        <div class="lg:col-span-8 space-y-4">
          <div class="flex items-center justify-between">
            <h2 class="text-lg font-extrabold text-slate-900 dark:text-white" data-i18n="dashCareerHeading">Khuyến nghị Nghề nghiệp</h2>
            <span class="text-xs font-semibold text-slate-400" data-i18n="dashUpdatedTag">Cập nhật 2025</span>
          </div>

          <!-- Figma Filter Pills -->
          <div class="flex items-center gap-2 overflow-x-auto no-scrollbar pb-1">
            <button onclick="filterCareers('all')" id="careerFilterAll" class="px-3.5 py-1.5 rounded-full bg-ueh-600 text-white text-xs font-bold shrink-0">Tất cả (5)</button>
            <button onclick="filterCareers('top')" id="careerFilterTop" data-i18n="filterTopMatch" class="px-3.5 py-1.5 rounded-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-xs font-semibold shrink-0">Hợp nhất (≥85%)</button>
            <button onclick="filterCareers('trending')" id="careerFilterTrend" data-i18n="filterTrending" class="px-3.5 py-1.5 rounded-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-xs font-semibold shrink-0">Xu hướng tuyển</button>
          </div>

          <div id="careerCardsGrid" class="space-y-4">
            <!-- Populated dynamically with exact Figma Screen 4 cards -->
          </div>
        </div>

        <!-- Right 4 Cols: BLUEPRINT AI Advisor Dark Blue Card (Exact Figma Screen 4) -->
        <div class="lg:col-span-4">
          <div class="bg-gradient-to-b from-ueh-700 via-ueh-800 to-slate-950 text-white rounded-3xl p-5 shadow-blue-glow flex flex-col justify-between space-y-4 sticky top-20">
            <div class="space-y-3">
              <div class="flex items-center gap-2.5">
                <div class="w-9 h-9 rounded-xl bg-white/15 flex items-center justify-center text-base">🤖</div>
                <div>
                  <div class="font-extrabold text-sm">BLUEPRINT AI Advisor</div>
                  <div class="text-[11px] text-emerald-300 flex items-center gap-1.5">
                    <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-ping"></span>
                    <span data-i18n="aiAdvisorReady">Sẵn sàng giải đáp thị trường việc làm</span>
                  </div>
                </div>
              </div>

              <div id="aiChatMessages" class="space-y-2.5 max-h-60 overflow-y-auto pr-1 text-xs">
                <div data-i18n="aiAdvisorWelcome" class="p-3.5 rounded-2xl bg-white/10 border border-white/10 leading-relaxed">
                  Đã phân tích! Các studio công nghệ &amp; tập đoàn Fintech tại TP.HCM đang tuyển mạnh vị trí Product Designer. Bạn muốn hỏi gì về lộ trình ứng tuyển vào vị trí này trong quý này?
                </div>
              </div>

              <!-- 2 Suggested Question Pills (Exact Figma Screen 4) -->
              <div class="space-y-2">
                <button type="button" onclick="askAiAdvisor(t('aiPrompt1'))" data-i18n="aiPrompt1" class="w-full text-left p-2.5 rounded-xl bg-white/10 hover:bg-white/20 border border-white/10 text-[11px] font-medium transition-colors">
                  "Năng lực cốt lõi để làm Product Designer tại Big Tech là gì?"
                </button>
                <button type="button" onclick="askAiAdvisor(t('aiPrompt2'))" data-i18n="aiPrompt2" class="w-full text-left p-2.5 rounded-xl bg-white/10 hover:bg-white/20 border border-white/10 text-[11px] font-medium transition-colors">
                  "CTD có hỗ trợ portfolio review để ứng tuyển AI Product Manager?"
                </button>
              </div>
            </div>

            <!-- Input Field + Blue Send Button (Exact Figma Screen 4) -->
            <form onsubmit="handleAiChatSubmit(event)" class="flex items-center gap-2 bg-white rounded-xl p-1.5 text-slate-800">
              <input id="aiChatInput" type="text" data-i18n-placeholder="aiInputPlaceholder" placeholder="Hỏi BLUEPRINT AI bất kỳ điều gì..." class="flex-1 bg-transparent px-2.5 py-1 text-xs text-slate-800 placeholder-slate-400 focus:outline-none" />
              <button type="submit" class="w-8 h-8 rounded-lg bg-ueh-600 hover:bg-ueh-700 text-white flex items-center justify-center shrink-0 transition-colors">
                <svg class="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- =================================================================== -->
    <!-- SCREEN 5: THỬ SỨC NGHỀ THỰC CHIẾN & CASE SIMULATOR (FIGMA SCREEN 5) -->
    <!-- =================================================================== -->
    <section id="view-simulation" class="view-section hidden space-y-6">
      <!-- Top Hero Banner (Exact Figma Screen 5) -->
      <div class="bg-gradient-to-br from-ueh-600 via-ueh-700 to-ueh-900 rounded-3xl p-5 sm:p-7 text-white shadow-blue-glow space-y-4">
        <div class="space-y-1.5">
          <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white/15 text-[11px] font-bold">
            <span>⚡</span>
            <span data-i18n="simBadge">Mô phỏng nghề thực tế</span>
          </span>
          <h1 class="text-2xl sm:text-3xl font-extrabold tracking-tight" data-i18n="simTitle">Thử sức Nghề thực chiến</h1>
          <p class="text-xs sm:text-sm text-ueh-100/90 max-w-2xl" data-i18n="simSubtitle">
            Trải nghiệm các mini-task thực tế từ doanh nghiệp đối tác UEH CTD để khám phá tốc độ yêu thích và năng lực của bạn.
          </p>
        </div>

        <!-- 3-Column Metrics Strip (Exact Figma Screen 5) -->
        <div class="grid grid-cols-3 gap-2 sm:gap-4 bg-white/10 backdrop-blur-md border border-white/15 rounded-2xl p-3.5 text-center">
          <div>
            <div class="text-lg sm:text-xl font-extrabold">12+</div>
            <div class="text-[11px] text-ueh-100" data-i18n="simMetricCases">Case studies</div>
          </div>
          <div class="border-x border-white/15">
            <div id="simXpBadge" class="text-lg sm:text-xl font-extrabold font-mono">850 XP</div>
            <div class="text-[11px] text-ueh-100" data-i18n="simMetricXp">Đã tích lũy</div>
          </div>
          <div>
            <div class="text-lg sm:text-xl font-extrabold text-amber-300">Top 5%</div>
            <div class="text-[11px] text-ueh-100" data-i18n="simMetricRank">Bảng xếp hạng</div>
          </div>
        </div>
      </div>

      <!-- Section 1: Đang thử sức (Active Challenge Card — Exact Figma Screen 5) -->
      <div class="space-y-3">
        <div class="flex items-center justify-between">
          <h2 class="text-sm font-extrabold text-slate-900 dark:text-white flex items-center gap-1.5">
            <span class="w-2 h-2 rounded-full bg-ueh-600"></span>
            <span data-i18n="simActiveHeading">Đang thử sức</span>
          </h2>
          <span class="text-xs font-bold text-ueh-600" data-i18n="simDeadline">Hạn chót: Còn 2 ngày</span>
        </div>

        <div class="bg-white dark:bg-slate-900 rounded-3xl p-4 sm:p-6 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-4">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-4 items-center">
            <!-- Custom SVG Illustrated Banner (GreenGo Vietnam Mobility) -->
            <div class="md:col-span-5 rounded-2xl overflow-hidden bg-gradient-to-br from-emerald-500 via-teal-600 to-ueh-700 p-4 text-white relative h-36 flex flex-col justify-between">
              <svg class="absolute right-2 bottom-2 w-24 h-24 opacity-25" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6">
                <circle cx="12" cy="12" r="10"/><path d="M8 14s1.5 2 4 2 4-2 4-2"/><path d="M9 9h.01M15 9h.01"/>
              </svg>
              <span class="self-start px-2.5 py-0.5 rounded-full bg-black/25 text-[10px] font-bold">UI/UX &amp; Interaction Designer</span>
              <div>
                <div class="font-extrabold text-sm">GreenGo Mobility App</div>
                <div class="text-[11px] text-emerald-100">GreenGo Vietnam &amp; GreenCorp 2026</div>
              </div>
            </div>

            <div class="md:col-span-7 space-y-3">
              <h3 class="text-base sm:text-lg font-extrabold text-slate-900 dark:text-white" data-i18n="simGreenGoTitle">
                Redesign Luồng Đặt xe Xanh cho Ứng dụng Di chuyển
              </h3>

              <div class="space-y-1.5">
                <div class="flex items-center justify-between text-xs">
                  <span class="text-slate-500 font-medium" data-i18n="simProgressLabel">Tiến độ hoàn thành</span>
                  <span id="activeTaskProgressText" class="font-mono font-bold text-ueh-600">2/4 Nhiệm vụ (50%)</span>
                </div>
                <div class="w-full h-2 bg-slate-100 dark:bg-slate-800 rounded-full overflow-hidden">
                  <div id="activeTaskProgressBar" class="h-full bg-ueh-600 rounded-full transition-all duration-300" style="width: 50%"></div>
                </div>
                <div class="text-[11px] text-emerald-600 dark:text-emerald-400 font-semibold" data-i18n="simCurrentMilestone">
                  ✓ User Journey Map • Đang: High-Fidelity Prototype
                </div>
              </div>

              <button onclick="openTaskModal('greengo')" data-i18n="simContinueBtn" class="w-full py-3 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white text-xs font-bold shadow-blue-glow transition-all">
                ▶ Tiếp tục làm bài thử sức
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Section 2: Multi-Industry Problem-Solving Case Simulator (Core Brief Feature) -->
      <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 sm:p-7 border-2 border-ueh-200 dark:border-ueh-800/80 shadow-card space-y-5">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-2 pb-3 border-b border-slate-100 dark:border-slate-800">
          <div>
            <span data-i18n="caseBadge" class="px-2.5 py-0.5 rounded-full bg-rose-50 dark:bg-rose-950/60 text-rose-600 dark:text-rose-400 text-[11px] font-bold">
              🔥 Case Thực chiến Đa ngành • Đánh giá Kỹ năng Giải quyết Vấn đề
            </span>
            <h2 data-i18n="caseSectionHeading" class="text-base sm:text-lg font-extrabold text-slate-900 dark:text-white mt-1">
              Chọn Ngành nghề &amp; Giải quyết Tình huống Thực tế
            </h2>
          </div>
          <button onclick="togglePersonaComparison()" data-i18n="caseCompareBtn" class="px-3.5 py-2 rounded-xl bg-ueh-50 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 text-xs font-bold hover:bg-ueh-100 shrink-0">
            ⚖️ So sánh Person A vs Person B
          </button>
        </div>

        <!-- Step 1: Career Track / Industry Filter Pills -->
        <div class="space-y-2">
          <div class="flex items-center justify-between text-[11px] font-bold text-slate-400 uppercase tracking-wider">
            <span data-i18n="caseIndustryStepLabel">1. Nhóm ngành nghề định hướng</span>
            <span id="solvedCasesCounterBadge" class="text-ueh-600 font-mono">0/9 Cases</span>
          </div>
          <div id="industryCaseTrackPills" class="flex items-center gap-2 overflow-x-auto no-scrollbar pb-1">
            <!-- Populated dynamically by renderSimulationView() -->
          </div>
        </div>

        <!-- Step 2: Case Selector within Selected Career Track -->
        <div id="industryCaseSelectorPills" class="flex flex-wrap items-center gap-2">
          <!-- Populated dynamically by renderSimulationView() -->
        </div>

        <!-- Active Scenario Prompt Box -->
        <div class="p-4 rounded-2xl bg-slate-50 dark:bg-slate-800/60 border border-slate-200/70 dark:border-slate-700/70 space-y-2">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <span id="activeCaseTag" class="px-2.5 py-0.5 rounded-md bg-ueh-100 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 text-[11px] font-bold">
              Marketing &amp; Brand Strategy • Case 1
            </span>
            <span class="text-[11px] font-mono font-bold text-emerald-600">+50 XP / Case</span>
          </div>
          <h3 id="activeCaseTitle" class="text-sm sm:text-base font-extrabold text-slate-900 dark:text-white">
            Tình huống: Khách hàng Khó tính cắt giảm 40% Ngân sách sát ngày Ra mắt
          </h3>
          <p id="activeCasePromptDesc" class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed">
            Khách hàng Fintech yêu cầu thay đổi toàn bộ concept chiến dịch Marketing &amp; Landing Page chỉ 5 ngày trước ngày ra mắt, đồng thời cắt giảm 40% ngân sách nhưng vẫn giữ nguyên KPI người dùng mới.
          </p>
        </div>

        <!-- Step 3: 3 Strategic Approaches (A / B / C) -->
        <div id="approachCardsContainer" class="grid grid-cols-1 md:grid-cols-3 gap-3.5">
          <!-- Populated dynamically by renderActiveIndustryCase() -->
        </div>

        <!-- Real-time AI Strengths, Weaknesses & % Job Fit Output -->
        <div id="approachAnalysisOutput" class="p-4 sm:p-5 rounded-2xl bg-gradient-to-br from-slate-900 to-ueh-950 text-white space-y-3.5"></div>

        <!-- Person A vs Person B Comparison Drawer -->
        <div id="personaComparisonPanel" class="hidden p-4 rounded-2xl bg-ueh-50/90 dark:bg-ueh-950/50 border border-ueh-200 dark:border-ueh-800 space-y-2.5 text-xs">
          <div class="flex items-center justify-between font-extrabold text-ueh-800 dark:text-ueh-200">
            <span data-i18n="personaCompTitle">📊 So sánh Person A vs Person B cùng gặp 1 Khách hàng khó tính</span>
            <button onclick="togglePersonaComparison()">✕</button>
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
            <div class="p-3 rounded-xl bg-white dark:bg-slate-900">
              <div class="font-bold text-ueh-600" data-i18n="personaATitle">👤 Person A (Chọn Hướng A - Dữ liệu ROI)</div>
              <p class="text-slate-600 dark:text-slate-300 mt-1" data-i18n="personaADesc">Điểm mạnh: Tư duy định lượng, quản trị ngân sách → Hợp AI Product Manager (95%).</p>
            </div>
            <div class="p-3 rounded-xl bg-white dark:bg-slate-900">
              <div class="font-bold text-indigo-600" data-i18n="personaBTitle">👤 Person B (Chọn Hướng B - Co-Creation &amp; Storytelling)</div>
              <p class="text-slate-600 dark:text-slate-300 mt-1" data-i18n="personaBDesc">Điểm mạnh: Trí tuệ cảm xúc EQ, thấu cảm &amp; sáng tạo → Hợp Brand Strategist (96%).</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Section 3: Khám phá Mini-tasks (Exact Figma Screen 5 Cards) -->
      <div class="space-y-3">
        <div class="flex items-center justify-between">
          <h2 class="text-base font-extrabold text-slate-900 dark:text-white" data-i18n="miniTasksHeading">Khám phá Mini-tasks</h2>
          <span class="text-xs font-semibold text-slate-400" data-i18n="miniTasksSub">Chọn theo chuyên ngành</span>
        </div>

        <div class="flex items-center gap-2 overflow-x-auto no-scrollbar pb-1">
          <button onclick="filterMiniTasks('all')" id="taskFilterAll" data-i18n="taskFilterAll" class="px-3.5 py-1.5 rounded-full bg-ueh-600 text-white text-xs font-bold shrink-0">Tất cả</button>
          <button onclick="filterMiniTasks('design')" id="taskFilterDesign" data-i18n="taskFilterDesign" class="px-3.5 py-1.5 rounded-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-xs font-semibold shrink-0">Thiết kế &amp; Đồ họa</button>
          <button onclick="filterMiniTasks('tech')" id="taskFilterTech" data-i18n="taskFilterTech" class="px-3.5 py-1.5 rounded-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-xs font-semibold shrink-0">Lập trình &amp; AI</button>
        </div>

        <div id="miniTasksGrid" class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <!-- Populated dynamically with Figma Screen 5 visual banners -->
        </div>
      </div>

      <!-- Section 4: Bảng xếp hạng Thử sức + Huy hiệu tích lũy (Exact Figma Screen 5) -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-5">
        <div class="lg:col-span-7 bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-3">
          <div class="flex items-center justify-between">
            <h3 class="font-extrabold text-sm sm:text-base text-slate-900 dark:text-white" data-i18n="leaderboardHeading">🏆 Bảng xếp hạng Thử sức</h3>
            <span class="text-xs font-semibold text-ueh-600" data-i18n="leaderboardWeek">Tuần 42 • Tháng 10</span>
          </div>

          <div class="space-y-2 text-xs">
            <div class="flex items-center justify-between p-3 rounded-2xl bg-amber-50/70 dark:bg-amber-950/30 border border-amber-200/70 dark:border-amber-800/40">
              <div class="flex items-center gap-2.5">
                <span class="w-6 h-6 rounded-full bg-amber-500 text-white font-extrabold flex items-center justify-center">1</span>
                <div>
                  <div class="font-bold text-slate-900 dark:text-white">Minh Khang (K48 - CTD)</div>
                  <div class="text-[11px] text-slate-500">6 Mini-tasks • 1,420 XP</div>
                </div>
              </div>
              <span class="px-2.5 py-0.5 rounded-full bg-amber-500 text-white font-bold text-[10px]">Top 1</span>
            </div>

            <div class="flex items-center justify-between p-3 rounded-2xl bg-slate-50 dark:bg-slate-800/70">
              <div class="flex items-center gap-2.5">
                <span class="w-6 h-6 rounded-full bg-slate-400 text-white font-extrabold flex items-center justify-center">2</span>
                <div>
                  <div class="font-bold text-slate-900 dark:text-white">Phương Uyên (K49 - BIT)</div>
                  <div class="text-[11px] text-slate-500">4 Mini-tasks • 1,190 XP</div>
                </div>
              </div>
              <span class="font-mono font-bold text-slate-500">1,190 XP</span>
            </div>

            <div class="flex items-center justify-between p-3 rounded-2xl bg-ueh-50 dark:bg-ueh-950/60 border border-ueh-200 dark:border-ueh-800">
              <div class="flex items-center gap-2.5">
                <span class="w-6 h-6 rounded-full bg-ueh-600 text-white font-extrabold flex items-center justify-center">14</span>
                <div>
                  <div class="font-bold text-ueh-700 dark:text-ueh-300" data-i18n="leaderboardYou">Bạn (Hồ sơ hiện tại)</div>
                  <div id="leaderboardUserXp" class="text-[11px] text-slate-500">3 Mini-tasks • 850 XP</div>
                </div>
              </div>
              <span class="font-bold text-ueh-600" data-i18n="leaderboardRank14">Hạng #14</span>
            </div>
          </div>

          <!-- Huy hiệu tích lũy của cá nhân (Exact Figma Screen 5) -->
          <div class="pt-3 border-t border-slate-100 dark:border-slate-800 space-y-2.5">
            <div class="flex items-center justify-between text-xs">
              <span class="font-bold text-slate-700 dark:text-slate-200" data-i18n="badgesHeading">🎖️ Huy hiệu tích lũy của cá nhân</span>
              <span class="text-ueh-600 font-bold" data-i18n="badgesCount">3/8 huy hiệu ›</span>
            </div>
            <div class="grid grid-cols-3 gap-2 text-center text-[11px]">
              <div class="p-2.5 rounded-2xl bg-slate-50 dark:bg-slate-800 border border-slate-200/60 dark:border-slate-700">
                <div class="text-lg">🎨</div>
                <div class="font-bold text-slate-800 dark:text-slate-100">UX Pioneer</div>
                <div class="text-[10px] text-slate-400">Mobile Hub</div>
              </div>
              <div class="p-2.5 rounded-2xl bg-slate-50 dark:bg-slate-800 border border-slate-200/60 dark:border-slate-700">
                <div class="text-lg">📊</div>
                <div class="font-bold text-slate-800 dark:text-slate-100">Data Explorer</div>
                <div class="text-[10px] text-slate-400">UEH Core</div>
              </div>
              <div class="p-2.5 rounded-2xl bg-slate-50 dark:bg-slate-800 border border-slate-200/60 dark:border-slate-700">
                <div class="text-lg">🚀</div>
                <div class="font-bold text-slate-800 dark:text-slate-100">Agile Sprint</div>
                <div class="text-[10px] text-slate-400">UEH Core</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Right 5 Cols: Sẵn sàng bứt phá giới hạn? CTA Card (Exact Figma Screen 5 Bottom) -->
        <div class="lg:col-span-5 bg-gradient-to-br from-ueh-600 via-ueh-700 to-indigo-800 rounded-3xl p-6 text-white shadow-blue-glow flex flex-col items-center justify-center text-center space-y-4">
          <div class="w-12 h-12 rounded-2xl bg-white/15 flex items-center justify-center text-xl">⚡</div>
          <div class="space-y-1.5">
            <h3 class="text-lg sm:text-xl font-extrabold" data-i18n="simCtaTitle">Sẵn sàng bứt phá giới hạn?</h3>
            <p class="text-xs text-ueh-100/90 leading-relaxed max-w-sm" data-i18n="simCtaDesc">
              Hệ thống AI sẽ tự động ghép bạn vào dự án thực tế phù hợp nhất với kết quả trắc nghiệm hướng nghiệp.
            </p>
          </div>
          <button type="button" onclick="openTaskModal('rec-algo')" data-i18n="simCtaBtn" class="w-full py-3 px-4 rounded-xl bg-sky-400 hover:bg-sky-300 text-slate-950 font-extrabold text-xs sm:text-sm shadow-md transition-all">
            ▶ Bắt đầu Thử thách Mới ngay
          </button>
        </div>
      </div>
    </section>

    <!-- =================================================================== -->
    <!-- SCREEN 6: SMALL COHORT (10-20 STUDENTS) & MENTORSHIP HUB            -->
    <!-- =================================================================== -->
    <section id="view-community" class="view-section hidden space-y-6">
      <!-- Dynamically rendered: Assessment Gate (MBTI + Simulation) -> AI Mentor Matching -> Matched Cohort & Mentor Hub -->
      <div id="communityDynamicRoot" class="space-y-6"></div>
    </section>
  </main>

  <!-- ===================================================================== -->
  <!-- MOBILE BOTTOM NAVIGATION BAR (FIGMA SCREENS 2, 4, 5 EXACT FOOTER)     -->
  <!-- ===================================================================== -->
  <nav id="mobileBottomNav" class="hidden lg:hidden fixed bottom-0 inset-x-0 z-40 bg-white/95 dark:bg-slate-900/95 backdrop-blur-md border-t border-slate-200 dark:border-slate-800 px-2 py-1.5">
    <div class="grid grid-cols-5 gap-1 max-w-md mx-auto">
      <button onclick="switchTab('dashboard')" data-tab="dashboard" class="mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-bold text-slate-400">
        <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/></svg>
        <span data-i18n="mobOverview">Tổng quan</span>
      </button>
      <button onclick="switchTab('profile')" data-tab="profile" class="mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-bold text-slate-400">
        <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
        <span>Hồ sơ</span>
      </button>
      <button onclick="switchTab('mbti')" data-tab="mbti" class="mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-bold text-slate-400">
        <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2a7 7 0 0 1 7 7c0 2.38-1.19 4.47-3 5.74V17a2 2 0 0 1-2 2h-4a2 2 0 0 1-2-2v-2.26C6.19 13.47 5 11.38 5 9a7 7 0 0 1 7-7z"/><path d="M9 21h6"/></svg>
        <span>MBTI Test</span>
      </button>
      <button onclick="switchTab('simulation')" data-tab="simulation" class="mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-bold text-slate-400">
        <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg>
        <span>Simulation</span>
      </button>
      <button onclick="switchTab('community')" data-tab="community" class="mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-bold text-slate-400">
        <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
        <span>Cohort</span>
      </button>
    </div>
  </nav>

  <!-- ===================================================================== -->
  <!-- UNIVERSAL MODAL & TOAST NOTIFICATION                                  -->
  <!-- ===================================================================== -->
  <div id="universalModal" class="hidden fixed inset-0 z-50 bg-slate-950/60 backdrop-blur-sm flex items-center justify-center p-4" onclick="if(event.target===this) closeModal()">
    <div class="bg-white dark:bg-slate-900 rounded-3xl max-w-lg w-full p-5 sm:p-6 border border-slate-200 dark:border-slate-800 shadow-2xl space-y-4">
      <div class="flex items-start justify-between gap-3">
        <div>
          <span id="modalTag" class="px-2.5 py-0.5 rounded-full bg-ueh-100 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 font-mono text-[10px] font-extrabold">BRIEF</span>
          <h3 id="modalTitle" class="text-base sm:text-lg font-extrabold text-slate-900 dark:text-white mt-1">Modal Title</h3>
        </div>
        <button type="button" onclick="closeModal()" class="w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-500 hover:text-slate-900 flex items-center justify-center font-bold">✕</button>
      </div>
      <div id="modalBody" class="text-xs sm:text-sm text-slate-600 dark:text-slate-300 leading-relaxed"></div>
    </div>
  </div>

  <div id="toastBanner" class="fixed bottom-20 lg:bottom-6 right-4 left-4 sm:left-auto sm:max-w-sm z-50 bg-slate-900 text-white px-4 py-3 rounded-2xl shadow-xl border border-slate-700 flex items-center gap-2.5 text-xs font-semibold transition-all duration-300 translate-y-24 opacity-0 pointer-events-none">
    <span class="w-2 h-2 rounded-full bg-emerald-400 shrink-0"></span>
    <span id="toastMessage">Thông báo hệ thống</span>
  </div>

  <!-- ===================================================================== -->
  <!-- APPLICATION JAVASCRIPT ENGINE                                         -->
  <!-- ===================================================================== -->
  <script>
    // =========================================================================
    // 0. SUPABASE CLIENT CONFIG (SANDBOX + LIVE @st.ueh.edu.vn OTP/SSO)
    // =========================================================================
    const SUPABASE_URL = 'https://YOUR_PROJECT_ID.supabase.co';
    const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
    const IS_LIVE_SUPABASE =
      SUPABASE_URL.startsWith('https://') &&
      !SUPABASE_URL.includes('YOUR_PROJECT_ID') &&
      SUPABASE_ANON_KEY !== 'YOUR_SUPABASE_ANON_KEY';

    const supabaseClient =
      IS_LIVE_SUPABASE && window.supabase
        ? window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY)
        : null;

    // =========================================================================
    // 1. MASTER DATASETS (CTD MAJORS, MBTI MATRIX, MULTI-INDUSTRY CASES)
    // =========================================================================
    const CTD_MAJORS = [
      {
        id: 'tech-innov',
        title: 'Công nghệ & Đổi mới sáng tạo',
        en: 'Technology & Innovation',
        icon: '🚀',
        iconBg: 'bg-ueh-100 dark:bg-ueh-950 text-ueh-600',
        tags: ['Product Design', 'Agile Studio']
      },
      {
        id: 'digital-media',
        title: 'Thiết kế Truyền thông số',
        en: 'Digital Media Design & Multimedia',
        icon: '🎨',
        iconBg: 'bg-indigo-100 dark:bg-indigo-950 text-indigo-600',
        tags: ['Creative Arts', 'UI/Visual']
      },
      {
        id: 'ai-robotics',
        title: 'Trí tuệ Nhân tạo & Robot',
        en: 'AI Technology & Robotics System',
        icon: '🤖',
        iconBg: 'bg-sky-100 dark:bg-sky-950 text-sky-600',
        tags: ['Machine Learning', 'Deep Tech']
      },
      {
        id: 'fintech',
        title: 'Công nghệ Tài chính (Fintech)',
        en: 'Financial Technology & Web3',
        icon: '💳',
        iconBg: 'bg-emerald-100 dark:bg-emerald-950 text-emerald-600',
        tags: ['Algorithmic Trade', 'Blockchain']
      },
      {
        id: 'smart-city',
        title: 'Kiến trúc Đô thị Thông minh',
        en: 'Smart City, GIS & Urban Tech',
        icon: '🏙️',
        iconBg: 'bg-amber-100 dark:bg-amber-950 text-amber-600',
        tags: ['Urban IoT', 'Sustainable Tech']
      }
    ];

    const CTD_SKILLS = [
      { vi: 'Lập trình Python / Web', en: 'Python / Web Coding' },
      { vi: 'UI/UX Design', en: 'UI/UX Design' },
      { vi: '3D Modeling & Blender', en: '3D Modeling & Blender' },
      { vi: 'Data Analytics', en: 'Data Analytics' },
      { vi: 'Tư duy phản biện', en: 'Critical Thinking' },
      { vi: 'Quản lý dự án Agile', en: 'Agile Project Management' },
      { vi: 'Giao tiếp quốc tế (IELTS 6.5+)', en: 'Global Communication (IELTS 6.5+)' }
    ];

    const POST_GRAD_GOALS = [
      {
        id: 'big-tech',
        icon: '🏢',
        title: 'Big Tech & Đa quốc gia',
        titleEn: 'Big Tech & Multinationals',
        desc: 'Môi trường toàn cầu, đãi ngộ cạnh tranh',
        descEn: 'Global tech culture & competitive compensation'
      },
      {
        id: 'startup',
        icon: '⚡',
        title: 'Khởi nghiệp Startup Công nghệ',
        titleEn: 'Tech Startup & Venture Building',
        desc: 'Sáng tạo sản phẩm mới, tăng trưởng đột phá',
        descEn: 'Build 0-to-1 products with rapid growth'
      },
      {
        id: 'grad-rnd',
        icon: '🎓',
        title: 'Du học & Nghiên cứu R&D',
        titleEn: 'Graduate Study & R&D Labs',
        desc: 'Thạc sĩ, Tiến sĩ và phòng lab quốc tế',
        descEn: 'Master’s, PhD & international research hubs'
      }
    ];

    const MBTI_QUESTIONS = [
      {
        dim: 'EI',
        dimLabel: '⚡ Năng lượng & Xu hướng tương tác xã hội',
        dimLabelEn: '⚡ Energy & Social Interaction Orientation',
        vi: 'Khi gặp một dự án công nghệ mới, bạn có xu hướng muốn thảo luận nhóm sôi nổi ngay lập tức thay vì suy ngẫm độc lập một mình?',
        en: 'When facing a new tech project, do you tend to dive into dynamic team brainstorming immediately rather than reflecting deeply on your own first?',
        insightPos: 'Bạn nạp năng lượng từ tương tác nhóm nhanh — điểm cộng lớn cho vai trò Product Manager và Workshop Facilitator.',
        insightPosEn: 'You gain energy from rapid group ideation — a key asset for Product Manager and Workshop Facilitator roles.',
        insightNeg: 'Bạn ưu tiên chiều sâu tư duy độc lập trước khi chia sẻ — rất phù hợp cho System Architect và UX Researcher.',
        insightNegEn: 'You value deep independent reflection before sharing — ideal for System Architect and UX Researcher roles.'
      },
      {
        dim: 'EI',
        dimLabel: '⚡ Năng lượng & Xu hướng tương tác xã hội',
        dimLabelEn: '⚡ Energy & Social Interaction Orientation',
        vi: 'Trong các sự kiện kết nối doanh nghiệp tại UEH CTD, bạn cảm thấy hào hứng khi chủ động bắt chuyện với nhiều mentor và bạn mới?',
        en: 'At UEH CTD industry networking events, do you feel energized proactively starting conversations with mentors and new peers?',
        insightPos: 'Khả năng mở rộng mạng lưới tự nhiên giúp bạn nổi bật trong các vị trí Growth, Partnership và Product Strategy.',
        insightPosEn: 'Natural networking agility makes you stand out in Growth, Partnership, and Product Strategy roles.',
        insightNeg: 'Bạn thích kết nối sâu sắc 1-1 chất lượng hơn giao tiếp đám đông — lợi thế khi phỏng vấn người dùng sâu.',
        insightNegEn: 'You prefer high-trust 1-on-1 conversations over large crowds — a major strength in deep user interviews.'
      },
      {
        dim: 'EI',
        dimLabel: '⚡ Năng lượng & Xu hướng tương tác xã hội',
        dimLabelEn: '⚡ Energy & Social Interaction Orientation',
        vi: 'Bạn thường suy nghĩ rõ ràng nhất trong lúc trình bày ý tưởng thành lời trước mọi người?',
        en: 'Do you often clarify your best ideas while articulating them out loud to teammates?',
        insightPos: 'Tư duy diễn đạt trực tiếp giúp bạn dẫn dắt buổi pitching ý tưởng và thuyết phục khách hàng hiệu quả.',
        insightPosEn: 'Verbal ideation helps you lead pitch sessions and persuade clients effectively.',
        insightNeg: 'Bạn thích tổng hợp cấu trúc bằng văn bản/sơ đồ trước khi phát biểu — đảm bảo độ chính xác cao.',
        insightNegEn: 'You prefer structuring ideas in writing or diagrams before speaking — ensuring high precision.'
      },
      {
        dim: 'SN',
        dimLabel: '🔭 Cách tiếp nhận thông tin & Tầm nhìn',
        dimLabelEn: '🔭 Information Processing & Vision',
        vi: 'Bạn bị cuốn hút bởi những ý tưởng đột phá, xu hướng tương lai (AI, Spatial Web) hơn là tối ưu quy trình vận hành quen thuộc?',
        en: 'Are you drawn more to breakthrough future concepts (AI, Spatial Web) than optimizing established operational routines?',
        insightPos: 'Trực giác chiến lược (N) mạnh mẽ giúp bạn kiến tạo sản phẩm mới 0-to-1 và định vị tầm nhìn dài hạn.',
        insightPosEn: 'Strong strategic intuition (N) empowers you to build 0-to-1 products and shape long-term vision.',
        insightNeg: 'Tư duy thực tế chi tiết (S) giúp bạn kiểm soát chất lượng sản phẩm và triển khai dự án không sai sót.',
        insightNegEn: 'Grounded attention to detail (S) ensures zero-defect execution and operational reliability.'
      },
      {
        dim: 'SN',
        dimLabel: '🔭 Cách tiếp nhận thông tin & Tầm nhìn',
        dimLabelEn: '🔭 Information Processing & Vision',
        vi: 'Khi phân tích một bài toán thiết kế, bạn thường nhìn bức tranh tổng thể và mối liên kết ẩn trước khi đi vào từng chi tiết UI?',
        en: 'When solving a design problem, do you map the big-picture ecosystem and hidden patterns before refining individual UI pixels?',
        insightPos: 'Khả năng nhìn hệ thống tổng thể là nền tảng cốt lõi của Product Architect và Design Lead.',
        insightPosEn: 'Systems-level pattern recognition is the core foundation of Product Architects and Design Leads.',
        insightNeg: 'Sự tỉ mỉ từng điểm chạm giúp giao diện và trải nghiệm người dùng của bạn đạt độ hoàn thiện cao.',
        insightNegEn: 'Meticulous touchpoint focus elevates your interface craft and usability polish.'
      },
      {
        dim: 'SN',
        dimLabel: '🔭 Cách tiếp nhận thông tin & Tầm nhìn',
        dimLabelEn: '🔭 Information Processing & Vision',
        vi: 'Bạn thích thử nghiệm các phương pháp tiếp cận hoàn toàn mới ngay cả khi chưa có tiền lệ rõ ràng?',
        en: 'Do you enjoy experimenting with novel approaches even when no established playbook exists yet?',
        insightPos: 'Tinh thần tiên phong đổi mới giúp bạn bứt phá trong môi trường Startup và R&D công nghệ.',
        insightPosEn: 'Pioneering curiosity helps you thrive in Tech Startups and R&D innovation labs.',
        insightNeg: 'Bạn tin tưởng các chuẩn mực đã được kiểm chứng thực tế — giúp giảm thiểu rủi ro dự án.',
        insightNegEn: 'You rely on proven best practices — minimizing execution risk on critical deliverables.'
      },
      {
        dim: 'TF',
        dimLabel: '⚖️ Nguyên tắc ra quyết định & Đánh giá',
        dimLabelEn: '⚖️ Decision-Making & Evaluation Principles',
        vi: 'Khi khách hàng và đội ngũ bất đồng quan điểm, bạn ưu tiên dựa trên dữ liệu định lượng (ROI, Conversion) hơn là cảm xúc hài lòng tức thời?',
        en: 'When clients and teams disagree, do you prioritize quantitative metrics (ROI, Conversion) over immediate emotional harmony?',
        insightPos: 'Tư duy phân tích khách quan (T) giúp bạn bảo vệ hiệu quả kinh doanh và đàm phán sắc bén.',
        insightPosEn: 'Objective analytical rigor (T) sharpens your business judgment and client negotiations.',
        insightNeg: 'Sự thấu cảm con người (F) giúp bạn gắn kết đội ngũ và xây dựng niềm tin bền vững với khách hàng.',
        insightNegEn: 'Human-centered empathy (F) builds team cohesion and lasting stakeholder trust.'
      },
      {
        dim: 'TF',
        dimLabel: '⚖️ Nguyên tắc ra quyết định & Đánh giá',
        dimLabelEn: '⚖️ Decision-Making & Evaluation Principles',
        vi: 'Bạn đánh giá cao những góp ý thẳng thắn, chỉ thẳng lỗ hổng logic hơn là lời khen khéo léo mang tính động viên?',
        en: 'Do you value candid feedback that pinpoints logical flaws over diplomatic encouragement?',
        insightPos: 'Tư duy phản biện sắc sảo giúp sản phẩm của bạn liên tục được nâng cấp về mặt kỹ thuật và chiến lược.',
        insightPosEn: 'Sharp critical thinking drives continuous technical and strategic product improvement.',
        insightNeg: 'Bạn chú trọng văn hóa phản hồi tích cực, giữ động lực sáng tạo cho cả nhóm trong giai đoạn căng thẳng.',
        insightNegEn: 'You foster psychologically safe feedback loops that sustain team morale under pressure.'
      },
      {
        dim: 'TF',
        dimLabel: '⚖️ Nguyên tắc ra quyết định & Đánh giá',
        dimLabelEn: '⚖️ Decision-Making & Evaluation Principles',
        vi: 'Trong thiết kế sản phẩm số, bạn xem tính hiệu quả và tốc độ hoàn thành tác vụ quan trọng hơn yếu tố cảm xúc thẩm mỹ?',
        en: 'In digital product design, do you prioritize functional efficiency and task speed over emotional delight?',
        insightPos: 'Bạn có tố chất mạnh mẽ cho Fintech Product, Data Dashboard và Enterprise SaaS.',
        insightPosEn: 'You possess strong instincts for Fintech Products, Data Dashboards, and Enterprise SaaS.',
        insightNeg: 'Bạn có thiên hướng xuất sắc cho Brand Storytelling, Consumer App và Creative Media.',
        insightNegEn: 'You shine in Brand Storytelling, Consumer Apps, and Creative Media experiences.'
      },
      {
        dim: 'JP',
        dimLabel: '🧭 Phong cách tổ chức & Thích ứng thay đổi',
        dimLabelEn: '🧭 Work Organization & Adaptability',
        vi: 'Khi khách hàng thay đổi yêu cầu sát hạn chót, bạn cảm thấy hứng thú ứng biến linh hoạt thay vì khó chịu vì phá vỡ kế hoạch?',
        en: 'When a client changes requirements near a deadline, do you feel energized improvising rather than frustrated by broken plans?',
        insightPos: 'Tính linh hoạt cao (P) giúp bạn tỏa sáng trong các môi trường Agile Sprint và khủng hoảng thực chiến.',
        insightPosEn: 'High adaptability (P) helps you excel in fast-paced Agile Sprints and live client pivots.',
        insightNeg: 'Tính kỷ luật kế hoạch (J) giúp bạn đảm bảo tiến độ bàn giao đúng hạn và quản trị rủi ro chặt chẽ.',
        insightNegEn: 'Structured planning discipline (J) ensures on-time delivery and tight scope governance.'
      },
      {
        dim: 'JP',
        dimLabel: '🧭 Phong cách tổ chức & Thích ứng thay đổi',
        dimLabelEn: '🧭 Work Organization & Adaptability',
        vi: 'Bạn thích giữ nhiều phương án mở để tiếp tục khám phá ý tưởng mới cho đến sát thời điểm chốt cuối cùng?',
        en: 'Do you prefer keeping multiple options open to explore new ideas right up until the final decision point?',
        insightPos: 'Khả năng mở rộng không gian giải pháp giúp bạn tìm ra những hướng đi sáng tạo bất ngờ.',
        insightPosEn: 'Keeping the solution space open helps you uncover unexpected creative breakthroughs.',
        insightNeg: 'Bạn thích chốt phương án sớm để tập trung tối đa nguồn lực hoàn thiện sản phẩm chỉn chu.',
        insightNegEn: 'You prefer locking decisions early to focus maximum energy on polished execution.'
      },
      {
        dim: 'JP',
        dimLabel: '🧭 Phong cách tổ chức & Thích ứng thay đổi',
        dimLabelEn: '🧭 Work Organization & Adaptability',
        vi: 'Bạn làm việc bùng nổ và sáng tạo nhất dưới áp lực thời gian ngắn hạn (Hackathon / Design Sprint)?',
        en: 'Do you do your most creative, high-output work under short-term sprint pressure (Hackathons / Design Sprints)?',
        insightPos: 'Bạn rất hợp với nhịp độ tăng trưởng nhanh của các Tech Studio và Product Innovation Labs.',
        insightPosEn: 'You thrive in the high-velocity rhythm of Tech Studios and Product Innovation Labs.',
        insightNeg: 'Bạn duy trì hiệu suất ổn định bền bỉ theo lộ trình dài hạn — thế mạnh của các tập đoàn lớn.',
        insightNegEn: 'You sustain steady, reliable output over long roadmaps — a key strength in enterprise teams.'
      }
    ];

    const INDUSTRY_CASE_BANK = [
      {
        id: 'marketing',
        nameVi: '📣 Marketing & Brand Strategy',
        nameEn: '📣 Marketing & Brand Strategy',
        cases: [
          {
            id: 'mkt-1',
            tagVi: 'Case 1 • Khủng hoảng Ngân sách & Khách hàng Khó tính',
            tagEn: 'Case 1 • Budget Cut & Difficult Client Crisis',
            titleVi: 'Khách hàng Khó tính cắt giảm 40% Ngân sách sát ngày Ra mắt',
            titleEn: 'Difficult Client Cuts Budget by 40% Five Days Before Launch',
            promptVi: 'Khách hàng Fintech yêu cầu đổi toàn bộ concept chiến dịch Marketing & Landing Page chỉ 5 ngày trước ngày ra mắt, đồng thời cắt giảm 40% ngân sách nhưng vẫn giữ nguyên KPI người dùng mới. Bạn sẽ xử lý thế nào?',
            promptEn: 'A Fintech client demands a full overhaul of the marketing campaign & landing page 5 days before launch while slashing budget by 40% with unchanged acquisition KPIs. How do you respond?',
            options: {
              A: {
                tag: 'Data & ROI',
                titleVi: 'Tái cấu trúc Phễu Chuyển đổi theo Dữ liệu & Đàm phán KPI',
                titleEn: 'Data-Driven Funnel Restructuring & KPI Alignment',
                descVi: 'Chứng minh kênh CAC/LTV hiệu quả nhất bằng số liệu lịch sử và dồn ngân sách vào Landing Page tối ưu CRO.',
                descEn: 'Prove highest-converting CAC/LTV channels with historical data and focus budget on CRO landing pages.',
                strengthsVi: 'Tư duy phân tích định lượng (CAC/LTV), đàm phán dựa trên bằng chứng và tối ưu chuyển đổi dưới áp lực.',
                strengthsEn: 'Quantitative analytical rigor (CAC/LTV), evidence-based negotiation, and conversion optimization under pressure.',
                weaknessesVi: 'Dễ khiến khách hàng cảm thấy thiếu sự lắng nghe cảm xúc thương hiệu trong 10 phút đầu đàm phán.',
                weaknessesEn: 'May make stakeholders feel emotionally unheard during initial friction if jumping to metrics too fast.',
                bestRole: 'Growth & Performance Marketer (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'Growth Marketer', score: 95 },
                  { role: 'AI Product Manager', score: 92 },
                  { role: 'Brand Strategist', score: 86 },
                  { role: 'Product Designer', score: 88 }
                ]
              },
              B: {
                tag: 'Empathy & Storytelling',
                titleVi: 'Workshop Đồng sáng tạo (Co-Creation) & Chiến dịch Viral UGC',
                titleEn: 'Empathetic Co-Creation Workshop & Viral UGC Campaign',
                descVi: 'Tổ chức phiên đồng sáng tạo 60 phút để xoa dịu khách hàng, chuyển hướng sang nội dung UGC & Micro-KOL chi phí thấp.',
                descEn: 'Host a 60-min co-creation session to align vision and pivot to lean-budget UGC & Micro-KOL storytelling.',
                strengthsVi: 'Trí tuệ cảm xúc (EQ) cao, thấu cảm nỗi lo khách hàng và sáng tạo nội dung lan tỏa tự nhiên với ngân sách thấp.',
                strengthsEn: 'High emotional intelligence (EQ), deep stakeholder empathy, and lean organic viral storytelling.',
                weaknessesVi: 'Cần bổ sung khung đo lường chuyển đổi ngắn hạn (Attribution) để thuyết phục giám đốc tài chính.',
                weaknessesEn: 'Needs stronger short-term conversion attribution metrics to convince CFO-level stakeholders.',
                bestRole: 'Brand & Marketing Strategist (96%)',
                heroFit: 96,
                fitScores: [
                  { role: 'Brand Strategist', score: 96 },
                  { role: 'Creative Director', score: 92 },
                  { role: 'Product Designer', score: 89 },
                  { role: 'Growth Marketer', score: 84 }
                ]
              },
              C: {
                tag: 'Agile Experimentation',
                titleVi: 'Rapid Prototyping 2 Concept & Chạy A/B Test 48h',
                titleEn: 'Rapid Prototyping 2 Concepts & 48h Live A/B Test',
                descVi: 'Dựng nhanh 2 phiên bản thông điệp & Landing Page trong 24h, chạy thử nghiệm nhỏ để lấy số liệu thực tế chốt phương án.',
                descEn: 'Ship 2 rapid message & landing page prototypes in 24h and run a live micro-test to let real data decide.',
                strengthsVi: 'Tốc độ thực thi Agile cực nhanh, biến tranh luận cảm tính thành kiểm chứng giả thuyết thực tế.',
                strengthsEn: 'Rapid Agile execution speed, turning subjective debates into live hypothesis validation.',
                weaknessesVi: 'Dễ gây quá tải cho đội ngũ thiết kế/content nếu không giới hạn phạm vi thử nghiệm rõ ràng.',
                weaknessesEn: 'Risk of burning out creative/tech teams if experiment boundaries are not tightly scoped.',
                bestRole: 'Product Marketing Manager (94%)',
                heroFit: 94,
                fitScores: [
                  { role: 'Product Marketing', score: 94 },
                  { role: 'Product Designer', score: 93 },
                  { role: 'Growth Marketer', score: 91 },
                  { role: 'Brand Strategist', score: 87 }
                ]
              }
            }
          },
          {
            id: 'mkt-2',
            tagVi: 'Case 2 • Truyền thông Khủng hoảng Mạng xã hội',
            tagEn: 'Case 2 • Social Media PR Crisis',
            titleVi: 'Chiến dịch Viral bị Phản ứng Trái chiều từ Cộng đồng Gen Z',
            titleEn: 'Viral Campaign Faces Backlash from Gen Z Community',
            promptVi: 'Một thông điệp quảng cáo vừa đăng tải 3 giờ bị cộng đồng mạng hiểu nhầm là thiếu tinh tế, lượng bình luận tiêu cực tăng nhanh. Bạn đề xuất bước đi đầu tiên nào?',
            promptEn: 'A newly launched ad campaign is misinterpreted as insensitive by online communities within 3 hours, sparking negative comments. What is your first move?',
            options: {
              A: {
                tag: 'Social Listening',
                titleVi: 'Đo lường Sentiment Dữ liệu & Phân loại Nhóm Phản ứng',
                titleEn: 'Sentiment Data Audit & Audience Cluster Mapping',
                descVi: 'Tạm dừng quảng cáo trả phí, phân tích tỷ trọng bình luận thật vs seeding để đánh giá đúng mức độ rủi ro trước khi phát ngôn.',
                descEn: 'Pause paid amplification and analyze organic vs bot sentiment ratios to gauge true risk before responding.',
                strengthsVi: 'Bình tĩnh phân tích dữ liệu khủng hoảng, tránh phản ứng vội vàng làm leo thang truyền thông.',
                strengthsEn: 'Calm crisis data triage, preventing knee-jerk statements that escalate media backlash.',
                weaknessesVi: 'Nếu phân tích quá lâu (>4 tiếng) có thể bỏ lỡ khung giờ vàng xoa dịu cộng đồng.',
                weaknessesEn: 'Over-analyzing beyond 4 hours risks missing the golden window to de-escalate public sentiment.',
                bestRole: 'Digital Marketing Analyst (94%)',
                heroFit: 94,
                fitScores: [
                  { role: 'Marketing Analyst', score: 94 },
                  { role: 'Brand Strategist', score: 91 },
                  { role: 'AI Product Manager', score: 88 },
                  { role: 'Creative Tech', score: 83 }
                ]
              },
              B: {
                tag: 'Transparent Apology',
                titleVi: 'Phát ngôn Cầu thị Minh bạch & Lắng nghe Trực tiếp',
                titleEn: 'Transparent Public Statement & Community Dialogue',
                descVi: 'Công khai nhận trách nhiệm thiện chí, giải thích bối cảnh sáng tạo và mời đại diện cộng đồng đóng góp chỉnh sửa.',
                descEn: 'Issue an authentic, accountable response explaining creative intent and inviting community co-editing.',
                strengthsVi: 'Bản lĩnh giao tiếp chân thành, biến khủng hoảng thành cơ hội củng cố niềm tin thương hiệu.',
                strengthsEn: 'Authentic crisis communication leadership, turning backlash into long-term brand trust.',
                weaknessesVi: 'Cần phối hợp chặt với bộ phận Pháp chế để tránh cam kết vượt thẩm quyền.',
                weaknessesEn: 'Requires tight legal alignment to avoid over-promising remediation commitments.',
                bestRole: 'Brand Communications Lead (96%)',
                heroFit: 96,
                fitScores: [
                  { role: 'Brand Comms Lead', score: 96 },
                  { role: 'Brand Strategist', score: 94 },
                  { role: 'Product Designer', score: 87 },
                  { role: 'AI Product Manager', score: 85 }
                ]
              },
              C: {
                tag: 'Creative Pivot',
                titleVi: 'Chuyển hóa Thành Chiến dịch Sáng tạo Cùng Người dùng',
                titleEn: 'Pivot into User-Generated Remix Challenge',
                descVi: 'Thừa nhận góc nhìn hài hước/góp ý của Gen Z và mở chiến dịch để chính người dùng viết lại thông điệp chuẩn nhất.',
                descEn: 'Acknowledge Gen Z feedback with humility and launch an interactive remix challenge for users to rewrite the tagline.',
                strengthsVi: 'Tư duy ứng biến sáng tạo linh hoạt, biến tương tác tiêu cực thành làn sóng đồng sáng tạo tích cực.',
                strengthsEn: 'Agile creative reframing, converting negative engagement into positive participatory momentum.',
                weaknessesVi: 'Đòi hỏi kiểm duyệt nội dung chặt chẽ để tránh phát sinh thêm thông điệp nhạy cảm.',
                weaknessesEn: 'Demands strict moderation guardrails to prevent secondary off-brand submissions.',
                bestRole: 'Creative Campaign Strategist (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'Creative Strategist', score: 95 },
                  { role: 'Creative Technologist', score: 91 },
                  { role: 'Brand Strategist', score: 90 },
                  { role: 'Product Designer', score: 88 }
                ]
              }
            }
          }
        ]
      },
      {
        id: 'design',
        nameVi: '🎨 Product & UI/UX Design',
        nameEn: '🎨 Product & UI/UX Design',
        cases: [
          {
            id: 'ux-1',
            tagVi: 'Case 1 • Xung đột UX vs Yêu cầu Kinh doanh',
            tagEn: 'Case 1 • UX Friction vs Stakeholder Feature Request',
            titleVi: 'Ban Giám đốc Muốn Chèn 3 Banner Khuyến mãi Vào Màn hình Thanh toán',
            titleEn: 'Executives Demand 3 Promo Banners Inside the Checkout Flow',
            promptVi: 'Tỷ lệ bỏ giỏ hàng (Cart Abandonment) đang là 62%, nhưng phòng Kinh doanh yêu cầu thêm 3 pop-up bán chéo ngay bước thanh toán để tăng doanh thu ngắn hạn. Bạn bảo vệ trải nghiệm người dùng thế nào?',
            promptEn: 'Cart abandonment is already at 62%, yet Business Stakeholders want 3 cross-sell pop-ups inside the checkout step to boost short-term revenue. How do you defend UX?',
            options: {
              A: {
                tag: 'UX Metrics & Funnel',
                titleVi: 'Mô phỏng Tác động Doanh thu Ròng từ Tỷ lệ Rớt Đơn',
                titleEn: 'Model Net Revenue Impact of Checkout Drop-off',
                descVi: 'Dùng dữ liệu Heatmap & Funnel chỉ ra rằng thêm bước cản sẽ làm mất nhiều doanh thu hơn phần bán chéo mang lại.',
                descEn: 'Use funnel & heatmap analytics to prove added friction loses more checkout revenue than cross-sells gain.',
                strengthsVi: 'Kết hợp xuất sắc tư duy UX với ngôn ngữ kinh doanh (Revenue Impact), thuyết phục lãnh đạo bằng số liệu.',
                strengthsEn: 'Bridges UX craft with business revenue language, convincing executives through hard funnel evidence.',
                weaknessesVi: 'Cần đề xuất giải pháp thay thế tích cực thay vì chỉ chứng minh phương án cũ không hiệu quả.',
                weaknessesEn: 'Must pair risk warnings with a constructive alternative placement so stakeholders feel supported.',
                bestRole: 'Senior Product Designer (96%)',
                heroFit: 96,
                fitScores: [
                  { role: 'Product Designer', score: 96 },
                  { role: 'AI Product Manager', score: 93 },
                  { role: 'Growth Analyst', score: 90 },
                  { role: 'Creative Tech', score: 85 }
                ]
              },
              B: {
                tag: 'Post-Purchase UX',
                titleVi: 'Thiết kế Lại Điểm Chạm Bán chéo Sau Thanh toán (1-Tap Upsell)',
                titleEn: 'Redesign Cross-Sell Touchpoint Post-Checkout (1-Tap Upsell)',
                descVi: 'Giữ luồng thanh toán tối giản 1 chạm, đồng thời thiết kế thẻ ưu đãi cá nhân hóa ngay màn hình xác nhận đặt hàng thành công.',
                descEn: 'Keep checkout friction-free and place a personalized 1-tap add-on card on the order confirmation screen.',
                strengthsVi: 'Giải quyết trọn vẹn bài toán Win-Win: bảo vệ tỷ lệ hoàn tất đơn hàng mà vẫn đạt KPI bán chéo.',
                strengthsEn: 'Delivers a true Win-Win flow: protects checkout completion while hitting cross-sell KPIs.',
                weaknessesVi: 'Cần phối hợp kỹ với đội Backend để xử lý gộp đơn sau khi đã thanh toán.',
                weaknessesEn: 'Requires close backend coordination to bundle post-payment add-ons seamlessly.',
                bestRole: 'UI/UX & Interaction Designer (97%)',
                heroFit: 97,
                fitScores: [
                  { role: 'Product Designer', score: 97 },
                  { role: 'UX Architect', score: 94 },
                  { role: 'AI Product Manager', score: 89 },
                  { role: 'Brand Strategist', score: 86 }
                ]
              },
              C: {
                tag: 'Usability Prototype',
                titleVi: 'Dựng Prototype Tương tác & Test Nhanh với 8 Người dùng Thật',
                titleEn: 'Build Interactive Prototype & Run 8-User Guerrilla Test',
                descVi: 'Quay video phản ứng thực tế của 8 người dùng khi gặp pop-up lúc thanh toán để trình chiếu trực tiếp trong cuộc họp.',
                descEn: 'Record 8 real users struggling with checkout pop-ups and play the highlight reel in the stakeholder review.',
                strengthsVi: 'Trực quan hóa tiếng nói người dùng (User Empathy) đầy sức thuyết phục, phá vỡ định kiến nội bộ.',
                strengthsEn: 'Visualizes authentic user pain points with undeniable empathy, breaking internal stakeholder bias.',
                weaknessesVi: 'Tốn thêm 1–2 ngày chuẩn bị kịch bản test khi tiến độ sprint đang gấp.',
                weaknessesEn: 'Requires an extra 1–2 days for test recruitment during tight sprint timelines.',
                bestRole: 'UX Researcher & Designer (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'UX Researcher', score: 95 },
                  { role: 'Product Designer', score: 94 },
                  { role: 'Creative Tech', score: 88 },
                  { role: 'Brand Strategist', score: 87 }
                ]
              }
            }
          }
        ]
      },
      {
        id: 'ai-tech',
        nameVi: '🤖 AI, Data & Tech Innovation',
        nameEn: '🤖 AI, Data & Tech Innovation',
        cases: [
          {
            id: 'ai-1',
            tagVi: 'Case 1 • Đánh đổi Độ chính xác AI vs Tốc độ Phản hồi',
            tagEn: 'Case 1 • AI Accuracy vs Latency Trade-off',
            titleVi: 'Trợ lý AI Tư vấn Tuyển sinh Phản hồi Chậm (7 giây) hoặc Đôi khi Sai Lệch',
            titleEn: 'AI Admissions Advisor Takes 7s to Respond or Occasionally Hallucinates',
            promptVi: 'Hệ thống AI Chatbot của trường trả lời rất chuẩn khi dùng mô hình lớn + RAG sâu nhưng mất 7 giây khiến sinh viên thoát trang. Nếu chuyển sang mô hình nhẹ thì nhanh (1.2s) nhưng dễ sai thông tin học bổng. Bạn chọn kiến trúc nào?',
            promptEn: 'The university AI chatbot is accurate with deep RAG + large LLM but takes 7s, causing user drop-off. A smaller model responds in 1.2s but risks scholarship hallucinations. What architecture do you choose?',
            options: {
              A: {
                tag: 'Hybrid Routing',
                titleVi: 'Kiến trúc Phân luồng Lai (Semantic Router + Streaming UI)',
                titleEn: 'Hybrid Semantic Router + Token Streaming Architecture',
                descVi: 'Dùng Semantic Cache trả lời ngay (<0.5s) cho câu hỏi phổ biến và stream từng chữ kết hợp trích dẫn nguồn cho câu hỏi phức tạp.',
                descEn: 'Serve FAQs via Semantic Cache (<0.5s) and stream cited RAG responses for complex queries.',
                strengthsVi: 'Tư duy kiến trúc hệ thống tối ưu cả trải nghiệm người dùng (Perceived Latency) lẫn độ tin cậy dữ liệu.',
                strengthsEn: 'Systems architecture mastery optimizing both perceived UX latency and factual reliability.',
                weaknessesVi: 'Tăng độ phức tạp khi bảo trì pipeline cache và cập nhật dữ liệu học bổng mới.',
                weaknessesEn: 'Increases pipeline maintenance complexity when invalidating stale scholarship caches.',
                bestRole: 'AI Product Manager & Architect (96%)',
                heroFit: 96,
                fitScores: [
                  { role: 'AI Product Manager', score: 96 },
                  { role: 'AI/ML Engineer', score: 94 },
                  { role: 'Product Designer', score: 89 },
                  { role: 'Data Analyst', score: 88 }
                ]
              },
              B: {
                tag: 'Guardrails & Trust',
                titleVi: 'Ưu tiên Độ chính xác 100% Kèm Ngưỡng Từ chối An toàn',
                titleEn: 'Prioritize 100% Grounded Accuracy with Confidence Thresholds',
                descVi: 'Thiết lập ngưỡng tin cậy nghiêm ngặt: khi thiếu dữ liệu chuẩn, AI chủ động kết nối sinh viên tới Cố vấn học tập thay vì đoán.',
                descEn: 'Enforce strict grounding thresholds: escalate low-confidence queries to human advisors instead of guessing.',
                strengthsVi: 'Đề cao đạo đức AI (AI Ethics & Safety) và bảo vệ uy tín tổ chức trước rủi ro thông tin sai lệch.',
                strengthsEn: 'Strong AI Ethics & Safety governance, protecting institutional trust against misinformation.',
                weaknessesVi: 'Tỷ lệ chuyển tiếp sang nhân sự hỗ trợ thủ công ban đầu có thể cao hơn kỳ vọng.',
                weaknessesEn: 'Initial human handoff escalation rate may be higher until knowledge base coverage expands.',
                bestRole: 'AI Governance & Product Lead (94%)',
                heroFit: 94,
                fitScores: [
                  { role: 'AI Product Manager', score: 94 },
                  { role: 'Data Strategist', score: 91 },
                  { role: 'Product Designer', score: 88 },
                  { role: 'Brand Strategist', score: 85 }
                ]
              },
              C: {
                tag: 'UX Feedback Loop',
                titleVi: 'Thiết kế Trạng thái Chờ Thông minh & Đánh giá Phản hồi 1 Chạm',
                titleEn: 'Design Interactive Progress States & 1-Tap Fact Verification',
                descVi: 'Hiển thị từng bước AI đang tra cứu quy chế UEH kèm nút xác minh nguồn trực tiếp để biến thời gian chờ thành sự tin tưởng.',
                descEn: 'Display live retrieval steps ("Checking UEH Scholarship Rules...") with source badges to build trust during wait time.',
                strengthsVi: 'Kết hợp tinh tế giữa kỹ thuật AI và tâm lý học giao diện (Human-AI Interaction).',
                strengthsEn: 'Seamless blend of AI engineering awareness and Human-AI Interaction (HAI) psychology.',
                weaknessesVi: 'Cần phối hợp chặt giữa Frontend và AI Engineer để đồng bộ sự kiện trạng thái.',
                weaknessesEn: 'Requires tight Frontend-AI engineering sync for real-time retrieval status events.',
                bestRole: 'AI UX & Product Designer (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'Product Designer', score: 95 },
                  { role: 'AI Product Manager', score: 93 },
                  { role: 'Creative Tech', score: 90 },
                  { role: 'Data Analyst', score: 86 }
                ]
              }
            }
          }
        ]
      },
      {
        id: 'fintech',
        nameVi: '💳 Fintech & Business Analytics',
        nameEn: '💳 Fintech & Business Analytics',
        cases: [
          {
            id: 'fin-1',
            tagVi: 'Case 1 • Bảo mật eKYC vs Tỷ lệ Mở Tài khoản',
            tagEn: 'Case 1 • eKYC Fraud Security vs Onboarding Conversion',
            titleVi: 'Siết Chặt Xác thực Khuôn mặt Làm Giảm 28% Tỷ lệ Sinh viên Mở Ví Mới',
            titleEn: 'Strict Facial eKYC Drops New Student Wallet Onboarding by 28%',
            promptVi: 'Sau khi nâng cấp bước xác thực eKYC 3 góc quay để chống gian lận, tỷ lệ hoàn tất đăng ký ví điện tử giảm 28% do camera điện thoại đời cũ khó nhận diện. Bạn đề xuất phương án cân bằng nào?',
            promptEn: 'After adding 3-angle facial liveness checks to prevent fraud, wallet onboarding completion fell 28% due to older phone cameras. How do you balance security and growth?',
            options: {
              A: {
                tag: 'Risk-Based Tiering',
                titleVi: 'Phân tầng Rủi ro Động (Risk-Based eKYC Tiering)',
                titleEn: 'Dynamic Risk-Based eKYC Tiering',
                descVi: 'Cho phép mở ví hạn mức nhỏ (<2 triệu/ngày) với eKYC 1 bước nhanh, chỉ yêu cầu xác thực nâng cao khi giao dịch giá trị lớn.',
                descEn: 'Allow fast 1-step onboarding for low daily limits (<2M VND) and trigger multi-angle eKYC only for high-value transfers.',
                strengthsVi: 'Tư duy quản trị rủi ro định lượng (Risk-Reward Optimization), tối đa hóa tăng trưởng mà vẫn khóa chặt gian lận lớn.',
                strengthsEn: 'Quantitative risk-reward optimization, maximizing onboarding conversion while containing high-value fraud.',
                weaknessesVi: 'Cần đảm bảo tuân thủ chặt quy định định danh của Ngân hàng Nhà nước cho từng hạn mức.',
                weaknessesEn: 'Must verify strict regulatory compliance with central bank eKYC tier limits.',
                bestRole: 'Fintech Product Manager (96%)',
                heroFit: 96,
                fitScores: [
                  { role: 'Fintech PM', score: 96 },
                  { role: 'Business Analyst', score: 94 },
                  { role: 'Product Designer', score: 90 },
                  { role: 'Data Analyst', score: 89 }
                ]
              },
              B: {
                tag: 'Guided Camera UX',
                titleVi: 'Cải tiến Giao diện Hướng dẫn Ánh sáng & Khung Nhận diện Thông minh',
                titleEn: 'Smart Lighting Guidance & Adaptive Camera Frame UX',
                descVi: 'Thêm thanh phản hồi ánh sáng thời gian thực và tự động chụp khi rõ nét để người dùng máy cấu hình thấp hoàn tất trong 5 giây.',
                descEn: 'Add real-time lighting prompts and auto-capture so entry-level phones complete verification in 5 seconds.',
                strengthsVi: 'Giải quyết điểm nghẽn kỹ thuật bằng thiết kế bao trùm (Inclusive UX Design), không hy sinh lớp bảo mật.',
                strengthsEn: 'Solves hardware friction via Inclusive UX Design without weakening security layers.',
                weaknessesVi: 'Cần thêm thời gian phát triển SDK camera trên cả iOS và Android.',
                weaknessesEn: 'Requires additional mobile SDK engineering effort across iOS and Android.',
                bestRole: 'Fintech Product Designer (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'Product Designer', score: 95 },
                  { role: 'Fintech PM', score: 92 },
                  { role: 'Creative Tech', score: 87 },
                  { role: 'Business Analyst', score: 86 }
                ]
              },
              C: {
                tag: 'Cohort Funnel Audit',
                titleVi: 'Phân tích Dữ liệu Rớt Bước Theo Thiết bị & Khung Giờ',
                titleEn: 'Device & Time-of-Day Funnel Drop-off Cohort Analysis',
                descVi: 'Tách dữ liệu lỗi theo dòng máy và điều kiện ánh sáng ban đêm để tối ưu ngưỡng AI nhận diện cho nhóm thiết bị yếu.',
                descEn: 'Segment failure logs by device model and low-light hours to recalibrate liveness thresholds for older devices.',
                strengthsVi: 'Tư duy phân tích dữ liệu sâu sắc (Root-Cause Analytics), khoanh vùng chính xác nguyên nhân thay vì sửa dàn trải.',
                strengthsEn: 'Deep root-cause data analytics, pinpointing exact device bottlenecks instead of broad guesswork.',
                weaknessesVi: 'Cần phối hợp chặt với đối tác cung cấp lõi AI eKYC để tinh chỉnh ngưỡng.',
                weaknessesEn: 'Depends on vendor API flexibility to tune confidence thresholds.',
                bestRole: 'Fintech Data & Business Analyst (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'Data & Business Analyst', score: 95 },
                  { role: 'Fintech PM', score: 93 },
                  { role: 'AI Product Manager', score: 90 },
                  { role: 'Product Designer', score: 85 }
                ]
              }
            }
          }
        ]
      },
      {
        id: 'creative-media',
        nameVi: '🌐 Digital Media & Creative Tech',
        nameEn: '🌐 Digital Media & Creative Tech',
        cases: [
          {
            id: 'med-1',
            tagVi: 'Case 1 • Sự cố Kỹ thuật Triển lãm Tương tác Trực tiếp',
            tagEn: 'Case 1 • Live Interactive Exhibition Hardware Failure',
            titleVi: 'Cảm biến LiDAR Của Triển lãm Nghệ thuật Số Gặp Lỗi 2 Giờ Trước Khai mạc',
            titleEn: 'LiDAR Sensor Fails 2 Hours Before Interactive Digital Art Opening',
            promptVi: 'Khu vực trình diễn 3D tương tác theo chuyển động khách tham quan tại sự kiện UEH CTD bị nhiễu cảm biến LiDAR do ánh sáng sân khấu. Bạn xử lý thế nào để giữ trọn trải nghiệm khán giả?',
            promptEn: 'The motion-reactive 3D installation at UEH CTD suffers LiDAR sensor interference from stage lights 2 hours before opening. How do you rescue the audience experience?',
            options: {
              A: {
                tag: 'WebCam Fallback',
                titleVi: 'Chuyển Đổi Sang Computer Vision Qua Camera & WebGL Dự phòng',
                titleEn: 'Switch to Optical Camera Pose Tracking + WebGL Fallback',
                descVi: 'Kích hoạt pipeline nhận diện chuyển động bằng camera chuẩn kết hợp bộ lọc ánh sáng để giữ hiệu ứng tương tác thời gian thực.',
                descEn: 'Activate standard RGB camera pose tracking with light-filtering shaders to preserve real-time interaction.',
                strengthsVi: 'Bản lĩnh xử lý sự cố kỹ thuật trực tiếp (Live Tech Troubleshooting) và linh hoạt chuyển đổi công nghệ thay thế.',
                strengthsEn: 'Composure under live technical pressure and agile fallback engineering across vision pipelines.',
                weaknessesVi: 'Độ sâu không gian 3D giảm nhẹ so với LiDAR nếu khán giả đứng quá xa vùng camera.',
                weaknessesEn: 'Slightly reduced Z-depth precision compared to LiDAR when visitors stand far from the lens.',
                bestRole: 'Creative Technologist (96%)',
                heroFit: 96,
                fitScores: [
                  { role: 'Creative Technologist', score: 96 },
                  { role: 'AI/CV Engineer', score: 93 },
                  { role: 'Product Designer', score: 89 },
                  { role: 'Brand Strategist', score: 84 }
                ]
              },
              B: {
                tag: 'Interactive Mobile Sync',
                titleVi: 'Biến Điện thoại Khán giả Thành Bộ Điều khiển Ánh sáng Tương tác',
                titleEn: 'Turn Visitors’ Smartphones into Live WebSocket Controllers',
                descVi: 'Mở mã QR WebApp để hàng trăm khán giả cùng quét và điều khiển hiệu ứng 3D trên màn hình lớn theo thời gian thực.',
                descEn: 'Launch a QR WebApp so hundreds of attendees simultaneously steer the 3D installation from their phones.',
                strengthsVi: 'Tư duy biến giới hạn phần cứng thành trải nghiệm cộng đồng bùng nổ, tăng mạnh mức độ tương tác sự kiện.',
                strengthsEn: 'Transforms hardware failure into a viral multi-user participatory experience.',
                weaknessesVi: 'Phụ thuộc vào độ ổn định Wi-Fi/4G tại khu vực sảnh triển lãm đông người.',
                weaknessesEn: 'Depends on venue Wi-Fi/cellular stability during peak attendee traffic.',
                bestRole: 'Interactive Media Designer (95%)',
                heroFit: 95,
                fitScores: [
                  { role: 'Interactive Designer', score: 95 },
                  { role: 'Creative Technologist', score: 94 },
                  { role: 'Product Designer', score: 91 },
                  { role: 'Brand Strategist', score: 88 }
                ]
              },
              C: {
                tag: 'Curated Generative Loop',
                titleVi: 'Chuyển Sang Trình diễn Generative Audio-Reactive Theo Âm thanh Sân khấu',
                titleEn: 'Switch to Stage Audio-Reactive Generative Visuals',
                descVi: 'Kết nối tín hiệu âm thanh trực tiếp từ bàn mixer để tác phẩm 3D biến đổi theo nhịp điệu âm nhạc và giọng nói diễn giả.',
                descEn: 'Feed live mixer audio into the 3D shader engine so visuals morph dynamically with music and speaker cadence.',
                strengthsVi: 'Nhạy bén thẩm mỹ đa giác quan (Audio-Visual Craft) và đảm bảo tính ổn định tuyệt đối cho lễ khai mạc.',
                strengthsEn: 'Strong multi-sensory audio-visual craft while guaranteeing rock-solid stability for the opening ceremony.',
                weaknessesVi: 'Giảm tính tương tác cá nhân hóa của từng khách tham quan riêng lẻ.',
                weaknessesEn: 'Reduces individual visitor motion interactivity compared to spatial tracking.',
                bestRole: 'Digital Media Director (94%)',
                heroFit: 94,
                fitScores: [
                  { role: 'Digital Media Director', score: 94 },
                  { role: 'Creative Technologist', score: 92 },
                  { role: 'Brand Strategist', score: 89 },
                  { role: 'Product Designer', score: 86 }
                ]
              }
            }
          }
        ]
      }
    ];

    const CAREER_DATABASE = [
      {
        id: 'product-designer',
        title: 'Product Designer',
        sub: 'UI/UX Lead Track • CTD',
        trending: true,
        primaryMajors: ['digital-media', 'tech-innov', 'smart-city'],
        matchingSkills: ['UI/UX Design', 'Tư duy phản biện', '3D Modeling & Blender'],
        preferredIndustries: ['design', 'creative-media', 'marketing'],
        preferredApproaches: ['B', 'C'],
        preferredGoals: ['big-tech', 'startup'],
        mbtiBias: { N: 0.45, F: 0.3, P: 0.25 },
        desc: 'Kết hợp tư duy thiết kế hệ thống và trải nghiệm số sáng tạo công nghệ. Phù hợp với sinh viên có khả năng phân tích hành vi người dùng và tạo mẫu nhanh.',
        descEn: 'Blends systems design thinking with creative digital experiences. Ideal for students skilled in user behavior analysis and rapid prototyping.',
        demand: 'Rất cao (TP.HCM)',
        demandEn: 'Very High (HCMC)',
        salary: '18M – 35M VND',
        skills: ['Design System', 'User Research', 'Micro-interactions', 'Figma'],
        roadmap: [
          'Làm chủ Design System, Auto Layout & Design Tokens trên Figma.',
          'Thực hiện 2 UX Case Study thực chiến (GreenGo Mobility & Fintech Checkout).',
          'Tham gia Portfolio Critique cùng Mentor và ứng tuyển Product Studio / Big Tech.'
        ],
        roadmapEn: [
          'Master Design Systems, Auto Layout & Design Tokens in Figma.',
          'Complete 2 end-to-end UX Case Studies (GreenGo Mobility & Fintech Checkout).',
          'Join Mentor Portfolio Clinics and apply to Product Studios / Big Tech.'
        ]
      },
      {
        id: 'ai-product-manager',
        title: 'AI Product Manager',
        sub: 'Tech–Product Synergy • CTD',
        trending: true,
        primaryMajors: ['tech-innov', 'ai-robotics', 'fintech'],
        matchingSkills: ['Data Analytics', 'Quản lý dự án Agile', 'Tư duy phản biện', 'Giao tiếp quốc tế (IELTS 6.5+)'],
        preferredIndustries: ['ai-tech', 'fintech', 'marketing'],
        preferredApproaches: ['A', 'C'],
        preferredGoals: ['big-tech', 'startup'],
        mbtiBias: { E: 0.3, N: 0.4, T: 0.3 },
        desc: 'Cầu nối chiến lược giữa kỹ thuật AI hiện đại và trải nghiệm người dùng. Định hình lộ trình sản phẩm thực tiễn từ dữ liệu doanh nghiệp.',
        descEn: 'Strategic bridge between modern AI engineering and user experience, shaping data-backed product roadmaps.',
        demand: 'Bùng nổ 2025',
        demandEn: 'Surging 2025',
        salary: '22M – 45M VND',
        skills: ['LLM Prompting', 'Product Strategy', 'Data Metrics', 'RAG Flows'],
        roadmap: [
          'Nắm vững vòng đời sản phẩm AI, đánh giá độ trễ (Latency) và độ chính xác RAG.',
          'Hoàn thành bài tập định lượng CAC/LTV và thiết kế A/B Testing thực tế.',
          'Xây dựng 1 MVP tích hợp AI giải quyết bài toán doanh nghiệp tại UEH CTD.'
        ],
        roadmapEn: [
          'Master AI product lifecycles, latency trade-offs, and RAG grounding evaluation.',
          'Complete quantitative CAC/LTV modeling and live A/B testing experiments.',
          'Ship 1 AI-powered MVP solving a real business problem at UEH CTD.'
        ]
      },
      {
        id: 'ai-ml-engineer',
        title: 'AI & Machine Learning Engineer',
        sub: 'Applied AI, RAG & Robotics Systems',
        trending: true,
        primaryMajors: ['ai-robotics', 'tech-innov', 'fintech'],
        matchingSkills: ['Lập trình Python / Web', 'Data Analytics', 'Tư duy phản biện'],
        preferredIndustries: ['ai-tech', 'fintech'],
        preferredApproaches: ['A'],
        preferredGoals: ['grad-rnd', 'big-tech'],
        mbtiBias: { I: 0.35, N: 0.35, T: 0.3 },
        desc: 'Thiết kế, huấn luyện và tối ưu hóa các mô hình học máy, hệ thống RAG và tác nhân tự động hóa thông minh cho bài toán quy mô lớn.',
        descEn: 'Designs, trains, and optimizes machine learning models, RAG pipelines, and intelligent autonomous agents at scale.',
        demand: 'Rất cao (AI Labs)',
        demandEn: 'Very High (AI Labs)',
        salary: '25M – 50M VND',
        skills: ['PyTorch / Python', 'RAG & Vector DB', 'Model Evaluation', 'MLOps'],
        roadmap: [
          'Thành thạo Python, PyTorch và kiến trúc Transformer / Retrieval-Augmented Generation.',
          'Tối ưu hóa độ trễ suy luận (Latency) và xây dựng bộ kiểm thử độ chính xác mô hình.',
          'Tham gia nghiên cứu tại UEH Smart Lab hoặc thực tập AI Engineer tại doanh nghiệp.'
        ],
        roadmapEn: [
          'Master Python, PyTorch, and Transformer / Retrieval-Augmented Generation architectures.',
          'Optimize inference latency and build automated hallucination evaluation suites.',
          'Join research at UEH Smart Lab or intern as an AI Engineer at partner tech firms.'
        ]
      },
      {
        id: 'fintech-quant-analyst',
        title: 'Fintech Product & Risk Analyst',
        sub: 'Digital Banking, Web3 & Quant Analytics',
        trending: true,
        primaryMajors: ['fintech', 'tech-innov'],
        matchingSkills: ['Data Analytics', 'Lập trình Python / Web', 'Tư duy phản biện'],
        preferredIndustries: ['fintech', 'ai-tech'],
        preferredApproaches: ['A', 'C'],
        preferredGoals: ['big-tech', 'startup'],
        mbtiBias: { T: 0.5, J: 0.3, N: 0.2 },
        desc: 'Phân tích dữ liệu giao dịch số, tối ưu tỷ lệ chuyển đổi eKYC và xây dựng mô hình quản trị rủi ro định lượng cho các nền tảng tài chính.',
        descEn: 'Analyzes digital payment funnels, optimizes eKYC onboarding conversion, and builds quantitative risk models for financial platforms.',
        demand: 'Tăng trưởng mạnh',
        demandEn: 'Strong Growth',
        salary: '20M – 42M VND',
        skills: ['SQL & Python Quant', 'Risk-Based eKYC', 'Funnel Analytics', 'FinTech Compliance'],
        roadmap: [
          'Làm chủ phân tích phễu chuyển đổi tài chính (Cohort Funnel) bằng SQL & Python.',
          'Thực hành thiết kế cơ chế phân tầng rủi ro eKYC cân bằng tăng trưởng và bảo mật.',
          'Hoàn thiện dự án sản phẩm tài chính số cùng Mentor Cohort #CTD-FIN05.'
        ],
        roadmapEn: [
          'Master financial cohort funnel modeling using SQL & Python.',
          'Practice designing risk-based eKYC tiers balancing growth and fraud defense.',
          'Build a digital finance product capstone with your #CTD-FIN05 Mentor.'
        ]
      },
      {
        id: 'brand-strategist',
        title: 'Digital Brand & Growth Strategist',
        sub: 'Creative Growth & MarTech Storytelling',
        trending: false,
        primaryMajors: ['digital-media', 'tech-innov'],
        matchingSkills: ['Giao tiếp quốc tế (IELTS 6.5+)', 'Quản lý dự án Agile', 'UI/UX Design'],
        preferredIndustries: ['marketing', 'creative-media'],
        preferredApproaches: ['B', 'C'],
        preferredGoals: ['startup', 'big-tech'],
        mbtiBias: { E: 0.4, F: 0.35, N: 0.25 },
        desc: 'Kiến tạo định vị thương hiệu số, chiến lược tăng trưởng đa kênh và kể chuyện truyền cảm hứng cho các startup công nghệ và Gen Z.',
        descEn: 'Crafts digital brand positioning, omnichannel growth campaigns, and resonant storytelling for tech startups and Gen Z audiences.',
        demand: 'Ổn định cao',
        demandEn: 'Strong & Steady',
        salary: '16M – 32M VND',
        skills: ['Brand Positioning', 'Growth Funnel (CAC/LTV)', 'Social Listening', 'Storytelling'],
        roadmap: [
          'Xây dựng khung Brand Persona & Customer Journey đa điểm chạm.',
          'Thực chiến xử lý khủng hoảng truyền thông và tối ưu phễu chuyển đổi ngân sách tinh gọn.',
          'Triển khai chiến dịch ra mắt sản phẩm thực tế cùng nhóm Cohort CTD.'
        ],
        roadmapEn: [
          'Architect Brand Personas and omnichannel Customer Journey maps.',
          'Practice crisis communications and lean-budget growth funnel optimization.',
          'Launch a live go-to-market campaign with your CTD Cohort.'
        ]
      },
      {
        id: 'creative-technologist',
        title: 'Creative Technologist',
        sub: 'Interactive Media, 3D & Spatial Web',
        trending: true,
        primaryMajors: ['digital-media', 'smart-city', 'ai-robotics'],
        matchingSkills: ['3D Modeling & Blender', 'Lập trình Python / Web', 'UI/UX Design'],
        preferredIndustries: ['creative-media', 'design'],
        preferredApproaches: ['A', 'B'],
        preferredGoals: ['startup', 'grad-rnd'],
        mbtiBias: { N: 0.5, P: 0.5 },
        desc: 'Ứng dụng công nghệ không gian 3D, WebGL, AR/VR và nghệ thuật thị giác số để kiến tạo không gian trải nghiệm tương tác mới tại UEH.',
        descEn: 'Applies 3D spatial computing, WebGL, AR/VR, and generative visual arts to craft next-generation interactive experiences.',
        demand: 'Đang tăng trưởng',
        demandEn: 'Fast Growing',
        salary: '20M – 42M VND',
        skills: ['Three.js / WebGL', 'Blender 3D', 'Computer Vision / Sensors', 'Interactive Audio'],
        roadmap: [
          'Thành thạo WebGL / Three.js, Blender 3D và tương tác cảm biến thời gian thực.',
          'Tham gia thiết kế triển lãm số tương tác tại UEH ArtTech Fusion.',
          'Phát triển bộ sưu tập Interactive Prototypes trên nền tảng web.'
        ],
        roadmapEn: [
          'Build fluency in WebGL / Three.js, Blender 3D, and real-time sensor interactions.',
          'Co-create interactive digital installations at UEH ArtTech Fusion.',
          'Publish a web-based portfolio of interactive 3D prototypes.'
        ]
      },
      {
        id: 'smart-city-architect',
        title: 'Smart City & Urban Tech Specialist',
        sub: 'Urban IoT, GIS & Sustainable Systems',
        trending: false,
        primaryMajors: ['smart-city', 'ai-robotics', 'tech-innov'],
        matchingSkills: ['3D Modeling & Blender', 'Data Analytics', 'Quản lý dự án Agile'],
        preferredIndustries: ['design', 'ai-tech'],
        preferredApproaches: ['A', 'C'],
        preferredGoals: ['grad-rnd', 'big-tech'],
        mbtiBias: { N: 0.4, T: 0.35, J: 0.25 },
        desc: 'Tích hợp dữ liệu không gian GIS, cảm biến IoT và mô hình mô phỏng 3D để quy hoạch hạ tầng đô thị thông minh và giao thông xanh.',
        descEn: 'Integrates GIS spatial data, IoT sensors, and 3D digital twins to design sustainable smart city infrastructure and green mobility.',
        demand: 'Tiềm năng dài hạn',
        demandEn: 'Long-Term Demand',
        salary: '18M – 38M VND',
        skills: ['GIS & Spatial Data', 'Digital Twin 3D', 'Urban IoT', 'Sustainability Metrics'],
        roadmap: [
          'Nắm vững phân tích dữ liệu bản đồ GIS và mô hình hóa không gian đô thị 3D.',
          'Thực hành bài toán tối ưu giao thông xanh & phân bổ không gian công cộng thông minh.',
          'Phát triển đề tài nghiên cứu đô thị thông minh cùng giảng viên Viện CTD.'
        ],
        roadmapEn: [
          'Master GIS spatial analytics and 3D urban digital twin modeling.',
          'Solve green mobility routing and smart public space optimization cases.',
          'Develop a smart city research project with UEH CTD faculty.'
        ]
      }
    ];

    const MINI_TASKS = [
      {
        id: 'rec-algo',
        track: 'tech',
        category: 'AI & ML Engineer',
        duration: '45 phút',
        durationEn: '45 mins',
        partner: 'MoMo R&D Hub',
        bannerBg: 'from-sky-500 via-ueh-600 to-indigo-700',
        title: 'Tối ưu hóa Thuật toán Gợi ý Sản phẩm',
        titleEn: 'Optimize Product Recommendation Algorithm',
        desc: 'Phân tích tập dữ liệu hành vi mua sắm giả lập và cải tiến mô hình Collaborative Filtering để nâng cao CTR cho đối tác thương mại điện tử.',
        descEn: 'Analyze simulated shopping behavior datasets and refine Collaborative Filtering models to boost e-commerce CTR.',
        xp: 200,
        badge: 'AI Pioneer'
      },
      {
        id: 'fintech-brand',
        track: 'design',
        category: 'Creative Brand Strategist',
        duration: '60 phút',
        durationEn: '60 mins',
        partner: 'UEH Innovation Hub',
        bannerBg: 'from-indigo-500 via-purple-600 to-ueh-700',
        title: 'Xây dựng Brand Identity cho Startup FinTech UEH',
        titleEn: 'Build Brand Identity for UEH FinTech Startup',
        desc: 'Xác lập Brand Persona, bộ quy chuẩn màu sắc và chiến lược truyền thông số cho ví điện tử sinh viên thông minh tạo ra tại Vườn ươm UEH UII.',
        descEn: 'Define Brand Persona, color system, and digital launch strategy for a smart student e-wallet incubated at UEH UII.',
        xp: 180,
        badge: 'Brand Crafter'
      },
      {
        id: 'campus-behavior',
        track: 'tech',
        category: 'Data Analyst',
        duration: '30 phút',
        durationEn: '30 mins',
        partner: 'UEH Smart Library',
        bannerBg: 'from-emerald-500 via-teal-600 to-cyan-700',
        title: 'Phân tích Dữ liệu Hành vi Sinh viên Campus UEH',
        titleEn: 'Analyze UEH Campus Student Behavior Data',
        desc: 'Trực quan hóa dữ liệu 15.000 lượt check-in tại thư viện và không gian tự học để đề xuất phương án phân bổ không gian tối ưu.',
        descEn: 'Visualize 15,000 library and co-working check-ins to propose optimal campus space allocation.',
        xp: 150,
        badge: 'Data Explorer'
      }
    ];

    const MENTOR_COHORT_DATABASE = [
      {
        id: 'mentor-bao',
        initials: 'PGS',
        name: 'PGS.TS Trần Quốc Bảo',
        roleVi: 'Phó Giáo sư • Cố vấn Đổi mới Sáng tạo & AI Product CTD UEH',
        roleEn: 'Associate Professor • Innovation & AI Product Advisor at UEH CTD',
        expVi: '14+ năm kinh nghiệm R&D & Product Strategy',
        expEn: '14+ years in R&D & Product Strategy',
        cohortCode: '#CTD-04',
        cohortSize: '16/20',
        cohortTitleVi: 'Cộng đồng Product Design, AI Product & Creative Tech',
        cohortTitleEn: 'Product Design, AI Product & Creative Tech Cohort',
        preferredMbti: ['ENTP', 'INTJ', 'ENFP', 'INTP', 'ENTJ'],
        preferredIndustries: ['ai-tech', 'design', 'creative-media'],
        preferredApproaches: ['A', 'C'],
        preferredMajors: ['tech-innov', 'ai-robotics', 'smart-city'],
        reasonTagsVi: ['Tư duy hệ thống & Đổi mới', 'Định hướng Product & AI', 'Thực chiến Agile Prototype'],
        reasonTagsEn: ['Systems & Innovation Mindset', 'Product & AI Orientation', 'Agile Prototyping Execution'],
        adviceVi: 'Với tổ hợp tính cách và tư duy giải quyết vấn đề thực chiến của em, em rất có tố chất dẫn dắt sản phẩm công nghệ mới. Hãy tham gia buổi review case cùng nhóm tuần này để thầy định hướng lộ trình Product/AI chi tiết nhé!',
        adviceEn: 'With your cognitive profile and practical problem-solving instincts, you are strongly wired to lead emerging tech products. Join this week’s cohort case review so we can map your Product/AI roadmap!',
        peers: [
          { name: 'Trần Hoàng Minh Khang', mbti: 'INTJ', role: 'AI Product Manager', initials: 'MK' },
          { name: 'Nguyễn Phương Uyên', mbti: 'ENFP', role: 'Product Designer', initials: 'PU' },
          { name: 'Đặng Quốc Anh', mbti: 'ISTP', role: 'Creative Technologist', initials: 'QA' },
          { name: 'Võ Thảo Vy', mbti: 'INFJ', role: 'UX Strategist', initials: 'TV' }
        ],
        sessions: [
          {
            id: 'sess-bao-1',
            dateVi: 'Thứ 7, 21/11 • 09:30 - 11:30',
            dateEn: 'Sat, Nov 21 • 09:30 - 11:30',
            type: 'Career Path Deep-Dive',
            titleVi: 'Từ Sinh viên CTD đến Product Designer & AI PM tại Big Tech',
            titleEn: 'From CTD Student to Product Designer & AI PM in Big Tech',
            spotsVi: '16/20 đã đăng ký',
            spotsEn: '16/20 registered'
          },
          {
            id: 'sess-bao-2',
            dateVi: 'Thứ 4, 25/11 • 19:30 - 21:00',
            dateEn: 'Wed, Nov 25 • 19:30 - 21:00',
            type: 'Case & Portfolio Review',
            titleVi: 'Phân tích trực tiếp Bài giải Simulation & Định vị Năng lực Lõi',
            titleEn: 'Live Review: Simulation Case Solutions & Core Competency Positioning',
            spotsVi: '14/20 đã đăng ký',
            spotsEn: '14/20 registered'
          }
        ]
      },
      {
        id: 'mentor-khue',
        initials: 'MK',
        name: 'ThS. Lê Hoàng Minh Khuê',
        roleVi: 'Head of Brand & Growth Strategy (Ex-Unilever & Shopee)',
        roleEn: 'Head of Brand & Growth Strategy (Ex-Unilever & Shopee)',
        expVi: '11+ năm dẫn dắt Chiến lược Thương hiệu & Tăng trưởng Số',
        expEn: '11+ years leading Digital Brand & Growth Strategy',
        cohortCode: '#CTD-MKT02',
        cohortSize: '15/20',
        cohortTitleVi: 'Cộng đồng Brand Strategy, Growth Marketing & Digital Storytelling',
        cohortTitleEn: 'Brand Strategy, Growth Marketing & Digital Storytelling Cohort',
        preferredMbti: ['ENFP', 'ENFJ', 'ESFP', 'ENTP', 'INFJ', 'ISFP'],
        preferredIndustries: ['marketing', 'creative-media'],
        preferredApproaches: ['B', 'C'],
        preferredMajors: ['digital-media', 'tech-innov'],
        reasonTagsVi: ['Trí tuệ cảm xúc & Thấu cảm KH', 'Tư duy Chiến dịch & Storytelling', 'Ứng biến Khủng hoảng Truyền thông'],
        reasonTagsEn: ['High EQ & Client Empathy', 'Campaign & Storytelling Craft', 'Agile Brand Crisis Pivot'],
        adviceVi: 'Cách em xử lý tình huống khách hàng cho thấy sự nhạy bén tuyệt vời về tâm lý người dùng và truyền thông thương hiệu. Nhóm #CTD-MKT02 đang cùng nhau giải các bài toán tăng trưởng thực tế từ doanh nghiệp — rất vui được đồng hành cùng em!',
        adviceEn: 'Your approach to the client scenario demonstrates sharp user empathy and brand storytelling instincts. Cohort #CTD-MKT02 is tackling live brand growth challenges — excited to mentor you!',
        peers: [
          { name: 'Lê Ngọc Bảo Trâm', mbti: 'ENFJ', role: 'Brand Strategist', initials: 'BT' },
          { name: 'Hoàng Gia Bảo', mbti: 'ENTP', role: 'Growth Marketer', initials: 'GB' },
          { name: 'Trịnh Minh Thư', mbti: 'ESFP', role: 'Social Creative Lead', initials: 'MT' },
          { name: 'Ngô Tấn Phát', mbti: 'INFP', role: 'Content Strategist', initials: 'TP' }
        ],
        sessions: [
          {
            id: 'sess-khue-1',
            dateVi: 'Thứ 6, 20/11 • 19:00 - 20:30',
            dateEn: 'Fri, Nov 20 • 19:00 - 20:30',
            type: 'Client Pitching Lab',
            titleVi: 'Nghệ thuật Đàm phán KPI & Bảo vệ Ý tưởng Sáng tạo trước Khách hàng Khó tính',
            titleEn: 'The Art of KPI Negotiation & Defending Creative Concepts to Tough Clients',
            spotsVi: '15/20 đã đăng ký',
            spotsEn: '15/20 registered'
          },
          {
            id: 'sess-khue-2',
            dateVi: 'Chủ Nhật, 29/11 • 09:30 - 11:00',
            dateEn: 'Sun, Nov 29 • 09:30 - 11:00',
            type: 'Growth Workshop',
            titleVi: 'Xây dựng Phễu Tăng trưởng Ngân sách Tinh gọn cho Startup Gen Z',
            titleEn: 'Building Lean-Budget Growth Funnels for Gen Z Startups',
            spotsVi: '13/20 đã đăng ký',
            spotsEn: '13/20 registered'
          }
        ]
      },
      {
        id: 'mentor-nguyen',
        initials: 'TN',
        name: 'ThS. Phạm Thảo Nguyên',
        roleVi: 'Lead Product Designer & UX Research Director (MoMo / VNG)',
        roleEn: 'Lead Product Designer & UX Research Director (MoMo / VNG)',
        expVi: '10+ năm Thiết kế Hệ thống Sản phẩm Số & Nghiên cứu Người dùng',
        expEn: '10+ years in Digital Product Systems & User Research',
        cohortCode: '#CTD-UX03',
        cohortSize: '14/20',
        cohortTitleVi: 'Cộng đồng UI/UX Design, Interaction & Design Systems',
        cohortTitleEn: 'UI/UX Design, Interaction & Design Systems Cohort',
        preferredMbti: ['INFJ', 'INFP', 'ISFP', 'ENFP', 'INTJ', 'ISTP'],
        preferredIndustries: ['design', 'creative-media'],
        preferredApproaches: ['B', 'C'],
        preferredMajors: ['digital-media', 'tech-innov', 'smart-city'],
        reasonTagsVi: ['Thiết kế Lấy con người làm trung tâm', 'Cân bằng UX & Mục tiêu Kinh doanh', 'Kiểm chứng Nguyên mẫu Nhanh'],
        reasonTagsEn: ['Human-Centered Design Thinking', 'Balancing UX & Business Goals', 'Rapid Usability Validation'],
        adviceVi: 'Em có khả năng kết nối rất tốt giữa trải nghiệm người dùng mượt mà và bài toán chuyển đổi thực tế. Trong nhóm #CTD-UX03, chị sẽ trực tiếp sửa từng màn hình Figma và hướng dẫn em cách bảo vệ quyết định thiết kế trước Product Manager.',
        adviceEn: 'You bridge seamless user experience with real conversion goals remarkably well. In Cohort #CTD-UX03, I will review your Figma flows directly and coach you on defending design decisions with PMs.',
        peers: [
          { name: 'Võ Thảo Vy', mbti: 'INFJ', role: 'UX Researcher', initials: 'TV' },
          { name: 'Đoàn Khánh Linh', mbti: 'ISFP', role: 'UI/Interaction Designer', initials: 'KL' },
          { name: 'Bùi Đức Duy', mbti: 'INTP', role: 'Design Systems Engineer', initials: 'DD' },
          { name: 'Phan Mỹ Duyên', mbti: 'ENFP', role: 'Product Designer', initials: 'MD' }
        ],
        sessions: [
          {
            id: 'sess-nguyen-1',
            dateVi: 'Thứ 5, 26/11 • 19:30 - 21:00',
            dateEn: 'Thu, Nov 26 • 19:30 - 21:00',
            type: 'Figma Critique Clinic',
            titleVi: 'Sửa trực tiếp Portfolio UX Case Study & Luồng Thanh toán 1 Chạm',
            titleEn: 'Live UX Case Study Portfolio Critique & 1-Tap Checkout Flows',
            spotsVi: '14/20 đã đăng ký',
            spotsEn: '14/20 registered'
          },
          {
            id: 'sess-nguyen-2',
            dateVi: 'Thứ 7, 05/12 • 14:00 - 16:00',
            dateEn: 'Sat, Dec 05 • 14:00 - 16:00',
            type: 'Usability Lab',
            titleVi: 'Kỹ thuật Phỏng vấn Người dùng Sâu & Đo lường Heatmap Thực chiến',
            titleEn: 'Deep User Interview Techniques & Live Heatmap Analytics',
            spotsVi: '12/20 đã đăng ký',
            spotsEn: '12/20 registered'
          }
        ]
      },
      {
        id: 'mentor-nam',
        initials: 'TS',
        name: 'TS. Nguyễn Thành Nam',
        roleVi: 'Tiến sĩ Khoa học Dữ liệu & Kiến trúc sư AI (UEH Smart Lab)',
        roleEn: 'PhD in Data Science & Principal AI Architect (UEH Smart Lab)',
        expVi: '12+ năm Nghiên cứu AI Ứng dụng, RAG Systems & Data Engineering',
        expEn: '12+ years in Applied AI, RAG Systems & Data Engineering',
        cohortCode: '#CTD-AI01',
        cohortSize: '13/20',
        cohortTitleVi: 'Cộng đồng AI Engineering, Data Analytics & Deep Tech R&D',
        cohortTitleEn: 'AI Engineering, Data Analytics & Deep Tech R&D Cohort',
        preferredMbti: ['INTJ', 'INTP', 'ISTJ', 'ENTJ', 'ISTP'],
        preferredIndustries: ['ai-tech', 'fintech'],
        preferredApproaches: ['A'],
        preferredMajors: ['ai-robotics', 'fintech'],
        reasonTagsVi: ['Tư duy Phân tích Định lượng Sâu', 'Kiến trúc Hệ thống & Tối ưu Hiệu năng', 'Giải quyết Bài toán Dữ liệu Lớn'],
        reasonTagsEn: ['Deep Quantitative & Analytical Rigor', 'Systems Architecture & Latency Optimization', 'Data-Driven Problem Solving'],
        adviceVi: 'Hồ sơ của em nổi bật ở tư duy logic sắc bén và khả năng ra quyết định dựa trên bằng chứng dữ liệu. Nhóm #CTD-AI01 sẽ giúp em biến các mô hình AI/Data thành sản phẩm có giá trị ứng dụng cao cho doanh nghiệp.',
        adviceEn: 'Your profile stands out for sharp logical reasoning and evidence-based decision-making. Cohort #CTD-AI01 will help you turn AI/Data models into high-impact enterprise solutions.',
        peers: [
          { name: 'Trần Hoàng Minh Khang', mbti: 'INTJ', role: 'ML Engineer', initials: 'MK' },
          { name: 'Lý Gia Hân', mbti: 'INTP', role: 'Data Scientist', initials: 'GH' },
          { name: 'Vũ Nhật Minh', mbti: 'ISTJ', role: 'AI Backend Developer', initials: 'NM' },
          { name: 'Nguyễn Tấn Tài', mbti: 'ENTJ', role: 'AI Solutions Architect', initials: 'TT' }
        ],
        sessions: [
          {
            id: 'sess-nam-1',
            dateVi: 'Thứ 4, 25/11 • 18:30 - 20:00',
            dateEn: 'Wed, Nov 25 • 18:30 - 20:00',
            type: 'AI Architecture Lab',
            titleVi: 'Tối ưu Độ trễ & Độ chính xác cho Hệ thống RAG Doanh nghiệp',
            titleEn: 'Optimizing Latency & Grounded Accuracy in Enterprise RAG Systems',
            spotsVi: '13/20 đã đăng ký',
            spotsEn: '13/20 registered'
          },
          {
            id: 'sess-nam-2',
            dateVi: 'Thứ 7, 05/12 • 09:00 - 11:00',
            dateEn: 'Sat, Dec 05 • 09:00 - 11:00',
            type: 'R&D Paper & Capstone',
            titleVi: 'Định hướng Nghiên cứu Khoa học Quốc tế & Thực tập R&D',
            titleEn: 'International Research Publishing & R&D Lab Internship Roadmap',
            spotsVi: '11/20 đã đăng ký',
            spotsEn: '11/20 registered'
          }
        ]
      },
      {
        id: 'mentor-hung',
        initials: 'QH',
        name: 'TS. Đặng Quốc Hưng',
        roleVi: 'Chuyên gia Fintech, Định lượng & Quản trị Rủi ro Số',
        roleEn: 'Fintech, Quantitative Analytics & Digital Risk Specialist',
        expVi: '13+ năm Tư vấn Sản phẩm Tài chính Số & Ngân hàng Mở',
        expEn: '13+ years Advising Digital Finance & Open Banking Products',
        cohortCode: '#CTD-FIN05',
        cohortSize: '14/20',
        cohortTitleVi: 'Cộng đồng Fintech Product, Business Analytics & Digital Banking',
        cohortTitleEn: 'Fintech Product, Business Analytics & Digital Banking Cohort',
        preferredMbti: ['ENTJ', 'ESTJ', 'INTJ', 'ISTJ', 'ENTP'],
        preferredIndustries: ['fintech', 'marketing'],
        preferredApproaches: ['A', 'C'],
        preferredMajors: ['fintech', 'tech-innov'],
        reasonTagsVi: ['Quản trị Rủi ro & Tối ưu ROI', 'Phân tích Phễu Chuyển đổi Tài chính', 'Tư duy Chiến lược Kinh doanh Số'],
        reasonTagsEn: ['Risk-Reward & ROI Optimization', 'Financial Funnel Analytics', 'Digital Business Strategy'],
        adviceVi: 'Khả năng cân bằng giữa tăng trưởng người dùng và kiểm soát rủi ro định lượng của em cực kỳ phù hợp với lĩnh vực Fintech & Business Analytics. Hãy cùng nhóm #CTD-FIN05 phân tích các bài toán sản phẩm tài chính thực tế nhé!',
        adviceEn: 'Your ability to balance user growth with quantitative risk governance fits Fintech & Business Analytics remarkably well. Join Cohort #CTD-FIN05 as we dissect real digital finance product cases!',
        peers: [
          { name: 'Phạm Gia Huy', mbti: 'ENTJ', role: 'Fintech Product Manager', initials: 'GH' },
          { name: 'Trần Quỳnh Như', mbti: 'ISTJ', role: 'Business Analyst', initials: 'QN' },
          { name: 'Lê Hoàng Phúc', mbti: 'INTJ', role: 'Quant & Risk Analyst', initials: 'HP' },
          { name: 'Đỗ Minh Anh', mbti: 'ENTP', role: 'Digital Banking PM', initials: 'MA' }
        ],
        sessions: [
          {
            id: 'sess-hung-1',
            dateVi: 'Thứ 6, 27/11 • 19:30 - 21:00',
            dateEn: 'Fri, Nov 27 • 19:30 - 21:00',
            type: 'Fintech Case Clinic',
            titleVi: 'Bài toán Cân bằng Bảo mật eKYC & Tỷ lệ Chuyển đổi Mở Ví Số',
            titleEn: 'Balancing eKYC Fraud Security & Digital Wallet Onboarding Conversion',
            spotsVi: '14/20 đã đăng ký',
            spotsEn: '14/20 registered'
          },
          {
            id: 'sess-hung-2',
            dateVi: 'Chủ Nhật, 06/12 • 14:00 - 16:00',
            dateEn: 'Sun, Dec 06 • 14:00 - 16:00',
            type: 'BA & PM Career Talk',
            titleVi: 'Lộ trình từ Sinh viên CTD đến Fintech Business Analyst & Product Owner',
            titleEn: 'Roadmap from CTD Student to Fintech Business Analyst & Product Owner',
            spotsVi: '12/20 đã đăng ký',
            spotsEn: '12/20 registered'
          }
        ]
      }
    ];

    // =========================================================================
    // 2. APPLICATION STATE WITH LOCALSTORAGE PERSISTENCE
    // =========================================================================
    const DEFAULT_STATE = {
      isLoggedIn: false,
      activeTab: 'profile',
      lang: 'vi',
      theme: 'light',
      student: {
        name: 'Lê Minh Ngọc',
        mssv: '31231024567',
        cohort: 'K49',
        programType: 'ĐHCQ',
        email: 'minhngoc.31231024567@st.ueh.edu.vn',
        verified: true,
        majorId: 'tech-innov',
        skills: ['Lập trình Python / Web', 'UI/UX Design', 'Data Analytics'],
        goalId: 'big-tech'
      },
      mbti: {
        currentIndex: 0,
        answers: Array(12).fill(null),
        completed: false,
        type: 'ENTP',
        archetype: 'Visionary Innovator',
        percentages: { E: 74, I: 26, N: 82, S: 18, T: 64, F: 36, P: 71, J: 29 }
      },
      simulation: {
        completed: false,
        selectedIndustry: 'marketing',
        selectedCaseIndex: 0,
        selectedApproach: 'A',
        lockedCases: {},
        solvedCaseKeys: [],
        xp: 850,
        activeTaskSteps: 2,
        completedTasks: []
      },
      community: {
        isMatched: false,
        matchedMentorId: null,
        matchScore: 95,
        rsvpedIds: [],
        connectedPeers: [],
        posts: [
          {
            author: 'Ban Điều phối Học thuật UEH CTD',
            role: 'BLUEPRINT Cohort Hub',
            time: '1 giờ trước',
            content: 'Chào mừng các thành viên mới đã hoàn thành 2 bài đánh giá MBTI & Simulation! Hãy giới thiệu chuyên ngành CTD và mục tiêu nghề nghiệp của bạn để kết nối cùng Mentor và nhóm nhé.'
          }
        ]
      }
    };

    let appState = loadState();

    function loadState() {
      try {
        const saved = localStorage.getItem('blueprint_ueh_figma_v2');
        if (saved) {
          const parsed = JSON.parse(saved);
          const merged = {
            ...DEFAULT_STATE,
            ...parsed,
            simulation: {
              ...DEFAULT_STATE.simulation,
              ...(parsed.simulation || {}),
              lockedCases: (parsed.simulation && parsed.simulation.lockedCases) || {}
            }
          };
          if (
            Array.isArray(merged.simulation.solvedCaseKeys) &&
            merged.simulation.solvedCaseKeys.length > 0 &&
            Object.keys(merged.simulation.lockedCases).length === 0
          ) {
            merged.simulation.solvedCaseKeys.forEach(k => {
              merged.simulation.lockedCases[k] = merged.simulation.selectedApproach || 'A';
            });
          }
          return merged;
        }
      } catch (e) {
        console.warn('Could not load saved state:', e);
      }
      return JSON.parse(JSON.stringify(DEFAULT_STATE));
    }

    function saveState() {
      try {
        localStorage.setItem('blueprint_ueh_figma_v2', JSON.stringify(appState));
      } catch (e) {
        console.warn('Could not persist state:', e);
      }
    }

    // =========================================================================
    // 3. THEME & BILINGUAL LOCALIZATION
    // =========================================================================
    function applyTheme() {
      const isDark = appState.theme === 'dark';
      const htmlEl = document.documentElement;
      const iconEl = document.getElementById('themeIcon');
      const labelEl = document.getElementById('themeLabel');

      if (isDark) {
        htmlEl.classList.add('dark');
        htmlEl.classList.remove('light');
        if (iconEl) iconEl.textContent = '🌙';
        if (labelEl) labelEl.textContent = appState.lang === 'en' ? 'Dark' : 'Tối';
      } else {
        htmlEl.classList.remove('dark');
        htmlEl.classList.add('light');
        if (iconEl) iconEl.textContent = '☀️';
        if (labelEl) labelEl.textContent = appState.lang === 'en' ? 'Light' : 'Sáng';
      }
    }

    function toggleTheme() {
      appState.theme = appState.theme === 'dark' ? 'light' : 'dark';
      saveState();
      applyTheme();
    }

    const I18N_STRINGS = {
      vi: {
        navOverview: 'AI Match',
        navProfile: 'Hồ sơ CTD',
        navMbti: 'MBTI Test',
        navSimulation: 'Simulation',
        navCommunity: 'Cohort & Mentor',
        mobOverview: 'Tổng quan',
        themeLight: 'Sáng',
        logoutTitle: 'Đăng xuất',
        shareProfileTitle: 'Chia sẻ hồ sơ',

        authSubtitle: 'Định hình tương lai nghề nghiệp với Trí tuệ Nhân tạo',
        authLoginTab: 'Đăng nhập',
        authRegisterTab: 'Đăng ký',
        authSsoBtn: 'Đăng nhập với Email UEH',
        authSsoSub: 'Cổng chứng thực sinh viên trực tuyến CTD',
        authDividerOtp: 'Hoặc xác thực MSSV & Email UEH',
        authFullNameLabel: 'Họ và tên sinh viên',
        authFullNamePlaceholder: 'VD: Lê Minh Ngọc',
        authMssvLabel: 'Mã sinh viên (MSSV)',
        authFillSample: 'Điền mẫu K49',
        authEmailLabel: 'Email sinh viên UEH',
        authRemember: 'Ghi nhớ đăng nhập',
        authLiveOtpGuide: 'Cấu hình Live OTP?',
        authContinueBtn: 'Tiếp tục khám phá (Gửi OTP)',
        otpStepTitle: '📩 Nhập mã OTP 6 số từ Email UEH',
        otpChangeMssv: 'Đổi MSSV',
        otpSentTo: 'Mã xác thực đã được gửi tới',
        otpSandboxTitle: '🧪 Mã OTP Sandbox Preview:',
        otpSandboxHint: 'Nhấn vào mã bên cạnh để điền tự động.',
        otpVerifyBtn: '✓ Xác nhận OTP & Vào BLUEPRINT',
        otpResendBtn: 'Gửi lại mã',
        authQuickLogin: 'Đăng nhập nhanh với',
        perksBadge: 'Đặc quyền Sinh viên CTD UEH',
        perksSub: 'Hành trang định hướng sự nghiệp cá nhân hóa',
        perk1Title: 'Trắc nghiệm MBTI & Holland chuẩn quốc tế',
        perk1Desc: 'Đo lường năng lực và tính cách nghề nghiệp chuẩn hóa theo định hướng Typologytesting.',
        perk2Title: 'Mô phỏng nhiệm vụ nghề thực tế & Xử lý tình huống',
        perk2Desc: 'Phân tích điểm mạnh/yếu khi đối mặt khách hàng khó tính và đo lường % Job Fit.',
        perk3Title: 'Cộng đồng Nhỏ (10–20 SV) & Cố vấn Mentor',
        perk3Desc: 'Ghép nhóm cùng các bạn đồng mục tiêu dưới sự dẫn dắt trực tiếp của Phó Giáo sư & Chuyên gia.',
        authReadyStatus: '● Sẵn sàng xác thực MSSV & Email @st.ueh.edu.vn',

        profStepTag: 'BƯỚC 1/2 • KHỞI TẠO NĂNG LỰC CTD',
        profTitle: 'Hồ sơ Sinh viên CTD',
        profSubtitle: 'Chọn chuyên ngành và kỹ năng hiện tại để AI BLUEPRINT cá nhân hóa lộ trình nghề nghiệp.',
        profMajorHeading: '• Chuyên ngành của bạn tại CTD',
        profPickOne: 'Chọn 1 ngành',
        profSkillsHeading: '• Kỹ năng & Điểm mạnh sở trường',
        profPickMany: 'Chọn nhiều kỹ năng',
        profSkillTip: 'Chọn ít nhất 3 kỹ năng để AI đánh giá chính xác độ tương thích công việc.',
        profGoalsHeading: '• Mục tiêu sau tốt nghiệp',
        profPriorityOne: 'Ưu tiên số 1',
        profSyncNote: 'Dữ liệu chuyên ngành sẽ được đồng bộ hóa trực tiếp với đề xuất nghề nghiệp từ Viện UEH CTD',
        profSaveBtn: 'Lưu & Bắt đầu làm bài test MBTI →',
        profSkipBtn: 'Bỏ qua bước này, thiết lập sau',

        mbtiBackBtn: 'Quay lại Hồ sơ',
        mbtiQuickDemo: 'Điền nhanh Demo →',
        mbtiSteadyPace: 'Tiến triển ổn định',
        mbtiAgreeSide: '👍 ĐỒNG Ý',
        mbtiDisagreeSide: 'PHẢN ĐỐI 👎',
        likertStronglyAgree: 'Rất đồng ý',
        likertAgree: 'Đồng ý',
        likertNeutral: 'Trung lập',
        likertDisagree: 'Không đồng ý',
        likertStronglyDisagree: 'Hoàn toàn phản đối',
        mbtiAutoAdvance: 'Tự động chuyển câu sau khi chọn mức độ',
        mbtiAiBoxTitle: 'Phân tích từ BLUEPRINT AI',
        mbtiDefaultInsight: 'Hãy chọn theo phản xạ tự nhiên nhất của bạn. Không có đáp án đúng hay sai — chỉ có góc nhìn phù hợp nhất với bản sắc năng lực của bạn tại UEH CTD!',
        mbtiPrevBtn: '← Câu trước',
        mbtiNextBtn: 'Tiếp tục →',
        mbtiFinishBtn: 'Hoàn thành & Xem AI Match ✓',
        mbtiDoneBadge: '✓ Hoàn thành Đánh giá MBTI',
        mbtiViewMatchBtn: 'Xem AI Match & Nghề nghiệp →',
        mbtiRetakeBtn: 'Làm lại bài test',

        dashReportBadge: 'Báo cáo Chân dung Cá nhân',
        dashArchetypeSub: 'Người kiến tạo tầm nhìn đa năng • Kết quả tổng hợp từ MBTI & Xử lý Tình huống CTD',
        dashAiCompatTitle: 'Chỉ số tương thích AI',
        dashAiCompatSub: 'Rất cao với nhóm nghề công nghệ sáng tạo',
        dashPill1: '✦ Tư duy liên ngành',
        dashPill2: '✦ Đột phá ý tưởng',
        dashPill3: '✦ Logic & Thẩm mỹ số',
        dashBehaviorHeading: '📊 Phân tích Hành vi Xử lý Tình huống',
        dashTryClientCase: 'Thử tình huống khách hàng →',
        dashStrengthLabel: '✓ Điểm mạnh (Strengths)',
        dashWeaknessLabel: '⚠ Điểm cần rèn luyện (Weaknesses)',
        dashBestRoleLabel: 'Vị trí phù hợp nhất theo hành vi:',
        dashCommCardTag: '🤝 Cộng đồng & Mentor',
        dashCohortCount: '16/20 Sinh viên',
        dashMentorRoleTag: 'Cohort #CTD-04 • Mentor Cố vấn',
        dashMentorBioShort: 'Phó Giáo sư • Cố vấn Chiến lược CTD',
        dashJoinCohortBtn: 'Vào nhóm & Đặt lịch Mentorship →',
        dashLockTitle: 'Mở khóa Ghép Mentor & Nhóm 10–20 SV',
        dashLockSub: 'Hoàn thành đủ 2 bài đánh giá bên dưới để AI tự động ghép Mentor phù hợp nhất với bạn:',
        dashUnlockMatchBtn: '✨ Kích hoạt Ghép Mentor ngay →',
        dashCareerHeading: 'Khuyến nghị Nghề nghiệp',
        dashUpdatedTag: 'Cá nhân hóa theo hồ sơ',
        filterAll4: 'Tất cả',
        filterTopMatch: 'Hợp nhất (≥85%)',
        filterTrending: 'Xu hướng tuyển',
        cardWhyMatchLabel: '🎯 Lý do sát với hồ sơ của bạn:',
        aiAdvisorReady: 'Sẵn sàng giải đáp thị trường việc làm',
        aiAdvisorWelcome: 'Đã phân tích! Các studio công nghệ & tập đoàn Fintech tại TP.HCM đang tuyển mạnh vị trí Product Designer. Bạn muốn hỏi gì về lộ trình ứng tuyển vào vị trí này trong quý này?',
        aiPrompt1: '"Năng lực cốt lõi để làm Product Designer tại Big Tech là gì?"',
        aiPrompt2: '"CTD có hỗ trợ portfolio review để ứng tuyển AI Product Manager?"',
        aiInputPlaceholder: 'Hỏi BLUEPRINT AI bất kỳ điều gì...',
        cardDemandLabel: 'Nhu cầu tuyển dụng',
        cardSalaryLabel: 'Mức lương dự kiến',
        cardSkillsLabel: 'Kỹ năng chuyên ngành bổ sung:',
        cardRoadmapBtn: '📖 Lộ trình học',
        cardTryNowBtn: '▶ Thử sức ngay',

        simBadge: 'Mô phỏng nghề thực tế',
        simTitle: 'Thử sức Nghề thực chiến',
        simSubtitle: 'Trải nghiệm các mini-task thực tế từ doanh nghiệp đối tác UEH CTD để khám phá tốc độ yêu thích và năng lực của bạn.',
        simMetricCases: 'Case studies',
        simMetricXp: 'Đã tích lũy',
        simMetricRank: 'Bảng xếp hạng',
        simActiveHeading: 'Đang thử sức',
        simDeadline: 'Hạn chót: Còn 2 ngày',
        simGreenGoTitle: 'Redesign Luồng Đặt xe Xanh cho Ứng dụng Di chuyển',
        simProgressLabel: 'Tiến độ hoàn thành',
        simCurrentMilestone: '✓ User Journey Map • Đang: High-Fidelity Prototype',
        simContinueBtn: '▶ Tiếp tục làm bài thử sức',
        caseBadge: '🔥 Case Thực chiến Đa ngành • Đánh giá Kỹ năng Giải quyết Vấn đề',
        caseSectionHeading: 'Chọn Ngành nghề & Giải quyết Tình huống Thực tế',
        caseIndustryStepLabel: '1. Nhóm ngành nghề định hướng',
        caseCompareBtn: '⚖️ So sánh Person A vs Person B',
        appSelectHint: 'Chọn & Khóa phương án này →',
        appSelectedHint: '🔒 Đã khóa lựa chọn của bạn',
        appLockedOtherHint: '🔒 Đã khóa',
        caseLockBannerTitle: 'Chưa chọn phương án • Lựa chọn sẽ được khóa ngay sau khi bấm',
        caseLockBannerDesc: 'Hãy đọc kỹ bối cảnh tình huống phía trên và chọn 1 trong 3 hướng tiếp cận (A, B hoặc C). Hệ thống sẽ khóa lựa chọn của bạn để đảm bảo đánh giá khách quan Điểm mạnh, Điểm yếu và % Job Fit.',
        personaCompTitle: '📊 So sánh Person A vs Person B cùng gặp 1 Khách hàng khó tính',
        personaATitle: '👤 Person A (Chọn Hướng A - Dữ liệu ROI)',
        personaADesc: 'Điểm mạnh: Tư duy định lượng, quản trị ngân sách → Hợp AI Product Manager (95%).',
        personaBTitle: '👤 Person B (Chọn Hướng B - Co-Creation & Storytelling)',
        personaBDesc: 'Điểm mạnh: Trí tuệ cảm xúc EQ, thấu cảm & sáng tạo → Hợp Brand Strategist (96%).',
        miniTasksHeading: 'Khám phá Mini-tasks',
        miniTasksSub: 'Chọn theo chuyên ngành',
        taskFilterAll: 'Tất cả',
        taskFilterDesign: 'Thiết kế & Đồ họa',
        taskFilterTech: 'Lập trình & AI',
        taskRewardLabel: 'Phần thưởng:',
        taskDetailBtn: 'Xem chi tiết Case',
        taskRegisterBtn: 'Đăng ký thử sức',
        taskDoneBtn: '✓ Hoàn thành',
        leaderboardHeading: '🏆 Bảng xếp hạng Thử sức',
        leaderboardWeek: 'Tuần 42 • Tháng 10',
        leaderboardYou: 'Bạn (Hồ sơ hiện tại)',
        leaderboardRank14: 'Hạng #14',
        badgesHeading: '🎖️ Huy hiệu tích lũy của cá nhân',
        badgesCount: '3/8 huy hiệu ›',
        simCtaTitle: 'Sẵn sàng bứt phá giới hạn?',
        simCtaDesc: 'Hệ thống AI sẽ tự động ghép bạn vào dự án thực tế phù hợp nhất với kết quả trắc nghiệm hướng nghiệp.',
        simCtaBtn: '▶ Bắt đầu Thử thách Mới ngay',

        commBadge: '● Nhóm Cộng đồng Quy mô Nhỏ (10–20 Sinh viên)',
        commTitle: 'Cộng đồng Product Design, AI Product & Creative Tech',
        commDesc: 'Sau khi hoàn thành đánh giá MBTI & Xử lý tình huống, bạn được ghép vào nhóm 10–20 sinh viên CTD có cùng mục tiêu nghề nghiệp dưới sự cố vấn trực tiếp của Phó Giáo sư & Chuyên gia ngành.',
        commGateBadge: '🔒 BƯỚC TIẾP THEO SAU ĐÁNH GIÁ',
        commGateTitle: 'Hoàn thành 2 bài đánh giá để AI ghép Mentor phù hợp nhất với bạn',
        commGateDesc: 'Theo quy trình BLUEPRINT, hệ thống chỉ tiến hành ghép nhóm 10–20 sinh viên và chỉ định 1 Mentor chuyên ngành sau khi phân tích đồng thời kết quả MBTI và hành vi xử lý tình huống Simulation của bạn.',
        commStep1Title: '1. Trắc nghiệm Tính cách MBTI (12 câu hỏi)',
        commStep1Done: '✓ Đã hoàn thành',
        commStep1Todo: 'Chưa hoàn thành • Bắt buộc',
        commStep1Btn: 'Làm bài test MBTI →',
        commStep2Title: '2. Mô phỏng Xử lý Tình huống (Simulation)',
        commStep2Done: '✓ Đã hoàn thành',
        commStep2Todo: 'Chưa hoàn thành • Bắt buộc',
        commStep2Btn: 'Giải tình huống ngay →',
        commReadyMatchBtn: '✨ Đã đủ 2/2 điều kiện — Bắt đầu Ghép Mentor ngay!',
        commRematchBtn: '🔄 Cập nhật ghép Mentor theo kết quả mới',
        commMatchBreakdownTitle: '🎯 Lý do AI ghép bạn với Mentor này:',
        commMentorHeading: 'Mentor Được Ghép Riêng Cho Nhóm Bạn',
        commMentorRole: 'Phó Giáo sư • Cố vấn Đổi mới Sáng tạo CTD UEH',
        commMentorExp: '14+ năm kinh nghiệm R&D & Product Strategy',
        commMentorAdviceLabel: '📌 Lời khuyên cá nhân hóa từ Mentor:',
        commMentorAdviceText: '"Với tổ hợp ENTP và tư duy phân tích ROI trong tình huống khách hàng, em rất hợp hướng Product Designer hoặc AI Product Manager. Hãy nộp Case GreenGo tuần này để thầy review trực tiếp nhé!"',
        commBookMentorBtn: '📅 Đặt lịch Mentorship Cá nhân hóa',
        commSessionsHeading: 'Lịch Sinh hoạt & Mentorship Sessions',
        commSessionsSub: 'Khám phá lộ trình nghề nghiệp, nhận góc nhìn thực tế từ Mentor và kết nối bạn đồng hành',
        commPeersHeading: 'Thành viên Nhóm Cùng Mục Tiêu',
        commPeersTag: 'Cùng mục tiêu nghề nghiệp',
        commFeedHeading: '💬 Thảo luận Nhóm & Mentor',
        commFeedPlaceholder: 'Chia sẻ câu hỏi cho nhóm & Mentor...',
        commPostBtn: 'Đăng',
        sessionJoinedBtn: '✓ Đã đăng ký',
        sessionJoinBtn: 'Tham gia',
        peerYouLabel: 'Bạn',
        peerConnectBtn: 'Kết nối',
        peerConnectedBtn: '✓ Đã kết nối',

        toastCopiedLink: 'Đã sao chép liên kết Hồ sơ Năng lực BLUEPRINT!',
        toastBookMentor: 'Đã gửi yêu cầu đặt lịch tư vấn 1-1 với Mentor của nhóm!',
        toastLangSwitched: 'Đã chuyển sang Tiếng Việt'
      },
      en: {
        navOverview: 'AI Match',
        navProfile: 'CTD Profile',
        navMbti: 'MBTI Test',
        navSimulation: 'Simulation',
        navCommunity: 'Cohort & Mentor',
        mobOverview: 'Overview',
        themeLight: 'Light',
        logoutTitle: 'Sign out',
        shareProfileTitle: 'Share profile',

        authSubtitle: 'Architect Your Career Future with Artificial Intelligence',
        authLoginTab: 'Sign In',
        authRegisterTab: 'Register',
        authSsoBtn: 'Sign in with UEH Email',
        authSsoSub: 'Official CTD Student Authentication Gateway',
        authDividerOtp: 'Or verify Student ID (MSSV) & UEH Email',
        authFullNameLabel: 'Student Full Name',
        authFullNamePlaceholder: 'e.g., Le Minh Ngoc',
        authMssvLabel: 'Student ID (MSSV)',
        authFillSample: 'Fill K49 Sample',
        authEmailLabel: 'UEH Student Email',
        authRemember: 'Keep me signed in',
        authLiveOtpGuide: 'Live OTP Setup?',
        authContinueBtn: 'Continue & Send OTP',
        otpStepTitle: '📩 Enter 6-Digit OTP from UEH Email',
        otpChangeMssv: 'Change ID',
        otpSentTo: 'Verification code sent to',
        otpSandboxTitle: '🧪 Sandbox Preview OTP:',
        otpSandboxHint: 'Click the code badge to auto-fill.',
        otpVerifyBtn: '✓ Verify OTP & Enter BLUEPRINT',
        otpResendBtn: 'Resend code',
        authQuickLogin: 'Quick sign in with',
        perksBadge: 'UEH CTD Student Privileges',
        perksSub: 'Personalized career architecture & mentorship',
        perk1Title: 'International Standard MBTI & Holland Assessment',
        perk1Desc: 'Measure cognitive strengths and career alignment modeled after Typologytesting.',
        perk2Title: 'Real-World Job Simulations & Problem-Solving Cases',
        perk2Desc: 'Analyze your strengths & weaknesses with difficult clients and calculate % Job Fit.',
        perk3Title: 'Small Cohort (10–20 Students) & Faculty Mentors',
        perk3Desc: 'Collaborate with like-minded peers guided directly by Associate Professors & Industry Leaders.',
        authReadyStatus: '● Ready to verify MSSV & @st.ueh.edu.vn email',

        profStepTag: 'STEP 1/2 • CTD COMPETENCY SETUP',
        profTitle: 'CTD Student Profile',
        profSubtitle: 'Select your major and current skills so BLUEPRINT AI can personalize your career roadmap.',
        profMajorHeading: '• Your Major at UEH CTD',
        profPickOne: 'Select 1 major',
        profSkillsHeading: '• Core Skills & Strengths',
        profPickMany: 'Select multiple',
        profSkillTip: 'Select at least 3 skills for accurate AI job-fit calibration.',
        profGoalsHeading: '• Post-Graduation Goal',
        profPriorityOne: 'Top priority',
        profSyncNote: 'Major data syncs directly with career recommendations from UEH College of Technology & Design',
        profSaveBtn: 'Save & Start MBTI Assessment →',
        profSkipBtn: 'Skip for now, configure later',

        mbtiBackBtn: 'Back to Profile',
        mbtiQuickDemo: 'Quick Demo Fill →',
        mbtiSteadyPace: 'Steady progress',
        mbtiAgreeSide: '👍 AGREE',
        mbtiDisagreeSide: 'DISAGREE 👎',
        likertStronglyAgree: 'Strongly Agree',
        likertAgree: 'Agree',
        likertNeutral: 'Neutral',
        likertDisagree: 'Disagree',
        likertStronglyDisagree: 'Strongly Disagree',
        mbtiAutoAdvance: 'Auto-advance to next question after selection',
        mbtiAiBoxTitle: 'BLUEPRINT AI Insight',
        mbtiDefaultInsight: 'Answer according to your natural instinct. There are no right or wrong answers — only what best reflects your authentic strengths at UEH CTD!',
        mbtiPrevBtn: '← Previous',
        mbtiNextBtn: 'Continue →',
        mbtiFinishBtn: 'Finish & View AI Match ✓',
        mbtiDoneBadge: '✓ MBTI Assessment Completed',
        mbtiViewMatchBtn: 'View AI Match & Careers →',
        mbtiRetakeBtn: 'Retake Test',

        dashReportBadge: 'Personal Archetype Report',
        dashArchetypeSub: 'Cross-disciplinary visionary • Synthesized from MBTI & CTD Case Simulations',
        dashAiCompatTitle: 'AI Compatibility Index',
        dashAiCompatSub: 'High synergy with creative technology roles',
        dashPill1: '✦ Cross-Disciplinary Thinking',
        dashPill2: '✦ Breakthrough Ideation',
        dashPill3: '✦ Logic & Digital Aesthetics',
        dashBehaviorHeading: '📊 Problem-Solving Behavioral Analysis',
        dashTryClientCase: 'Try difficult client case →',
        dashStrengthLabel: '✓ Identified Strengths',
        dashWeaknessLabel: '⚠ Growth Areas (Weaknesses)',
        dashBestRoleLabel: 'Best behavioral role fit:',
        dashCommCardTag: '🤝 Community & Mentor',
        dashCohortCount: '16/20 Students',
        dashMentorRoleTag: 'Cohort #CTD-04 • Faculty Mentor',
        dashMentorBioShort: 'Associate Professor • CTD Strategy Mentor',
        dashJoinCohortBtn: 'Enter Cohort & Book Mentorship →',
        dashLockTitle: 'Unlock Personalized Mentor & Cohort Match',
        dashLockSub: 'Complete both assessments below so our AI can match you with your ideal Mentor:',
        dashUnlockMatchBtn: '✨ Match My Mentor Now →',
        dashCareerHeading: 'Career Recommendations',
        dashUpdatedTag: 'Profile-Calibrated',
        filterAll4: 'All',
        filterTopMatch: 'Best Fit (≥85%)',
        filterTrending: 'In-Demand',
        cardWhyMatchLabel: '🎯 Why this matches your profile:',
        aiAdvisorReady: 'Ready to answer labor market questions',
        aiAdvisorWelcome: 'Analysis complete! Tech studios & Fintech firms in HCMC are actively hiring Product Designers. What would you like to ask about applying this quarter?',
        aiPrompt1: '"What core competencies are needed for Product Designer roles in Big Tech?"',
        aiPrompt2: '"Does CTD offer portfolio reviews for AI Product Manager applicants?"',
        aiInputPlaceholder: 'Ask BLUEPRINT AI anything...',
        cardDemandLabel: 'Hiring Demand',
        cardSalaryLabel: 'Estimated Salary',
        cardSkillsLabel: 'Recommended Specialized Skills:',
        cardRoadmapBtn: '📖 Learning Roadmap',
        cardTryNowBtn: '▶ Try Simulation',

        simBadge: 'Real-World Job Simulation',
        simTitle: 'Hands-On Career Challenges',
        simSubtitle: 'Experience real mini-tasks from UEH CTD industry partners to discover your strengths and career fit.',
        simMetricCases: 'Case studies',
        simMetricXp: 'XP Earned',
        simMetricRank: 'Leaderboard',
        simActiveHeading: 'In Progress',
        simDeadline: 'Deadline: 2 days left',
        simGreenGoTitle: 'Redesign Green Ride-Hailing Flow for Mobility App',
        simProgressLabel: 'Completion Progress',
        simCurrentMilestone: '✓ User Journey Map • Active: High-Fidelity Prototype',
        simContinueBtn: '▶ Continue Challenge',
        caseBadge: '🔥 Live Multi-Industry Case • Problem-Solving Skill Assessment',
        caseSectionHeading: 'Select Career Track & Solve Real-World Scenarios',
        caseIndustryStepLabel: '1. Target career track',
        caseCompareBtn: '⚖️ Compare Person A vs Person B',
        appSelectHint: 'Select & Lock this approach →',
        appSelectedHint: '🔒 Your Choice (Locked)',
        appLockedOtherHint: '🔒 Locked',
        caseLockBannerTitle: 'No approach selected yet • Choice locks upon selection',
        caseLockBannerDesc: 'Read the scenario carefully and choose 1 of the 3 strategic approaches (A, B, or C). Your choice will be locked immediately to objectively evaluate your Strengths, Weaknesses, and % Job Fit.',
        personaCompTitle: '📊 Comparing Person A vs Person B Facing the Same Difficult Client',
        personaATitle: '👤 Person A (Chose Approach A - Data & ROI)',
        personaADesc: 'Strengths: Quantitative rigor, budget discipline → Best fit for AI Product Manager (95%).',
        personaBTitle: '👤 Person B (Chose Approach B - Co-Creation & Storytelling)',
        personaBDesc: 'Strengths: Emotional intelligence (EQ), empathy & brand craft → Best fit for Brand Strategist (96%).',
        miniTasksHeading: 'Explore Mini-tasks',
        miniTasksSub: 'Filter by specialization',
        taskFilterAll: 'All',
        taskFilterDesign: 'Design & Media',
        taskFilterTech: 'Coding & AI',
        taskRewardLabel: 'Reward:',
        taskDetailBtn: 'View Case Brief',
        taskRegisterBtn: 'Start Mini-task',
        taskDoneBtn: '✓ Completed',
        leaderboardHeading: '🏆 Challenge Leaderboard',
        leaderboardWeek: 'Week 42 • October',
        leaderboardYou: 'You (Current Profile)',
        leaderboardRank14: 'Rank #14',
        badgesHeading: '🎖️ Earned Personal Badges',
        badgesCount: '3/8 badges ›',
        simCtaTitle: 'Ready to push your limits?',
        simCtaDesc: 'Our AI engine matches you with real company mini-projects aligned with your career assessment.',
        simCtaBtn: '▶ Start New Challenge Now',

        commBadge: '● Small Learning Community (10–20 Students)',
        commTitle: 'Product Design, AI Product & Creative Tech Cohort',
        commDesc: 'After completing both MBTI & Simulation assessments, you are matched into a 10–20 student CTD cohort sharing similar career goals under a dedicated Faculty or Industry Mentor.',
        commGateBadge: '🔒 ASSESSMENT PREREQUISITE',
        commGateTitle: 'Complete Both Assessments to Unlock Your Matched Mentor',
        commGateDesc: 'Per the BLUEPRINT framework, our AI pairs you with a 10–20 student cohort and 1 dedicated Mentor only after analyzing both your MBTI personality profile and your Simulation problem-solving behavior.',
        commStep1Title: '1. MBTI Personality Assessment (12 Questions)',
        commStep1Done: '✓ Completed',
        commStep1Todo: 'Pending • Required',
        commStep1Btn: 'Take MBTI Test →',
        commStep2Title: '2. Problem-Solving Case Simulation',
        commStep2Done: '✓ Completed',
        commStep2Todo: 'Pending • Required',
        commStep2Btn: 'Solve Simulation Case →',
        commReadyMatchBtn: '✨ Both Assessments Complete — Match My Mentor Now!',
        commRematchBtn: '🔄 Re-run Mentor Match with Latest Results',
        commMatchBreakdownTitle: '🎯 Why AI Matched You with This Mentor:',
        commMentorHeading: 'Your AI-Matched Cohort Mentor',
        commMentorRole: 'Associate Professor • Innovation Advisor at UEH CTD',
        commMentorExp: '14+ years in R&D & Product Strategy',
        commMentorAdviceLabel: '📌 Personalized Guidance from Your Mentor:',
        commMentorAdviceText: '"With your ENTP profile and ROI-driven problem-solving approach, you are strongly aligned with Product Design or AI Product Management. Submit your GreenGo case this week for my direct review!"',
        commBookMentorBtn: '📅 Book 1-on-1 Mentorship Session',
        commSessionsHeading: 'Cohort & Mentorship Sessions Schedule',
        commSessionsSub: 'Explore career paths, gain real industry insights from your Mentor, and connect with peers',
        commPeersHeading: 'Cohort Members (10–20 Peers)',
        commPeersTag: 'Shared career goals',
        commFeedHeading: '💬 Cohort & Mentor Group Discussion',
        commFeedPlaceholder: 'Share a question with your peers & Mentor...',
        commPostBtn: 'Post',
        sessionJoinedBtn: '✓ Registered',
        sessionJoinBtn: 'Join Session',
        peerYouLabel: 'You',
        peerConnectBtn: 'Connect',
        peerConnectedBtn: '✓ Connected',

        toastCopiedLink: 'Copied BLUEPRINT Career Profile link!',
        toastBookMentor: 'Sent 1-on-1 mentorship booking request to your Cohort Mentor!',
        toastLangSwitched: 'Switched language to English'
      }
    };

    function t(key) {
      const lang = appState.lang === 'en' ? 'en' : 'vi';
      return (I18N_STRINGS[lang] && I18N_STRINGS[lang][key]) || I18N_STRINGS.vi[key] || key;
    }

    function setLanguage(lang, silent = false) {
      appState.lang = lang === 'en' ? 'en' : 'vi';
      document.documentElement.lang = appState.lang;
      saveState();

      const viBtn = document.getElementById('langViBtn');
      const enBtn = document.getElementById('langEnBtn');
      if (viBtn && enBtn) {
        if (appState.lang === 'vi') {
          viBtn.className = 'px-2.5 py-1 rounded-full transition-all bg-ueh-600 text-white shadow-sm';
          enBtn.className = 'px-2.5 py-1 rounded-full transition-all text-slate-500 dark:text-slate-300';
        } else {
          enBtn.className = 'px-2.5 py-1 rounded-full transition-all bg-ueh-600 text-white shadow-sm';
          viBtn.className = 'px-2.5 py-1 rounded-full transition-all text-slate-500 dark:text-slate-300';
        }
      }

      document.querySelectorAll('[data-i18n]').forEach(el => {
        const key = el.getAttribute('data-i18n');
        const val = t(key);
        if (val) el.textContent = val;
      });

      document.querySelectorAll('[data-i18n-placeholder]').forEach(el => {
        const key = el.getAttribute('data-i18n-placeholder');
        const val = t(key);
        if (val) el.setAttribute('placeholder', val);
      });

      document.querySelectorAll('[data-i18n-title]').forEach(el => {
        const key = el.getAttribute('data-i18n-title');
        const val = t(key);
        if (val) el.setAttribute('title', val);
      });

      applyTheme();
      handleLiveUehInput();

      if (appState.isLoggedIn) {
        renderProfileSetup();
        renderMbtiQuestion();
        renderSimulationView();
        renderCommunityView();
        renderDashboardView();
      }

      if (!silent) showToast(t('toastLangSwitched'));
    }

    // =========================================================================
    // 4. REAL UEH STUDENT AUTHENTICATION ENGINE (MSSV + OTP & OAUTH SSO)
    // =========================================================================
    let currentAuthMode = 'login';
    let currentSandboxOtp = '482910';
    let pendingUehStudent = null;
    let otpCountdownTimer = null;

    function setAuthMode(mode) {
      currentAuthMode = mode === 'register' ? 'register' : 'login';
      const loginTab = document.getElementById('authTabLogin');
      const regTab = document.getElementById('authTabRegister');
      const nameWrap = document.getElementById('registerNameWrap');

      const activeCls =
        'py-2 rounded-lg text-xs sm:text-sm font-bold bg-white dark:bg-slate-900 text-ueh-600 dark:text-ueh-400 shadow-sm transition-all';
      const inactiveCls =
        'py-2 rounded-lg text-xs sm:text-sm font-semibold text-slate-500 dark:text-slate-400 transition-all';

      if (loginTab && regTab) {
        loginTab.className = currentAuthMode === 'login' ? activeCls : inactiveCls;
        regTab.className = currentAuthMode === 'register' ? activeCls : inactiveCls;
      }
      if (nameWrap) {
        nameWrap.classList.toggle('hidden', currentAuthMode !== 'register');
      }
    }

    function parseUEHStudent(mssvInput, emailInput, fullNameInput = '') {
      const isEn = appState.lang === 'en';
      const mssv = (mssvInput || '').trim();
      const email = (emailInput || '').trim().toLowerCase();

      const mssvRegex = /^(31|32|33)\d{9}$/;
      if (!mssvRegex.test(mssv)) {
        return {
          valid: false,
          error: isEn
            ? 'Invalid Student ID (MSSV). Please enter 11 digits starting with 31, 32, or 33 (e.g., 31231024567).'
            : 'MSSV không hợp lệ. Vui lòng nhập đủ 11 chữ số bắt đầu bằng 31, 32 hoặc 33 (VD: 31231024567).'
        };
      }

      if (!email.endsWith('@st.ueh.edu.vn') || email.length <= '@st.ueh.edu.vn'.length) {
        return {
          valid: false,
          error: isEn
            ? 'Please use your official UEH student email ending in @st.ueh.edu.vn.'
            : 'Vui lòng sử dụng email sinh viên UEH chính thức có đuôi @st.ueh.edu.vn.'
        };
      }

      const embeddedDigits = email.split('@')[0].match(/(\d{11})/);
      if (embeddedDigits && embeddedDigits[1] !== mssv) {
        return {
          valid: false,
          error: isEn
            ? `Student ID (${mssv}) does not match the ID embedded in your email (${embeddedDigits[1]}).`
            : `MSSV (${mssv}) không khớp với mã số trong email UEH (${embeddedDigits[1]})!`
        };
      }

      const enrollYear = parseInt(mssv.substring(2, 4), 10);
      const cohortNumber = enrollYear + 26;
      const prefixCode = mssv.substring(0, 2);
      const programType =
        prefixCode === '31' ? 'ĐHCQ' : prefixCode === '32' ? 'Liên thông' : 'VB2 / Quốc tế';

      const cleanName = (fullNameInput || '').trim();
      let displayName = cleanName;
      if (!displayName) {
        const localPart = email.split('@')[0].split('.')[0].replace(/\d+/g, '');
        displayName = localPart
          ? localPart.charAt(0).toUpperCase() + localPart.slice(1)
          : isEn
            ? `UEH Student (${mssv.slice(-4)})`
            : `Sinh viên UEH (${mssv.slice(-4)})`;
      }

      return {
        valid: true,
        student: {
          mssv,
          email,
          cohort: `K${cohortNumber}`,
          programType,
          name: displayName
        }
      };
    }

    function handleLiveUehInput() {
      const mssvEl = document.getElementById('authMssvInput');
      const emailEl = document.getElementById('authUehEmailInput');
      const nameEl = document.getElementById('authFullName');
      const box = document.getElementById('uehLiveValidationBox');
      const icon = document.getElementById('uehLiveStatusIcon');
      const content = document.getElementById('uehLiveStatusContent');
      if (!mssvEl || !emailEl || !box || !icon || !content) return;

      const isEn = appState.lang === 'en';
      const mssv = mssvEl.value.trim();
      const email = emailEl.value.trim();

      if (!mssv && !email) {
        box.className =
          'p-2.5 rounded-xl bg-ueh-50/90 dark:bg-ueh-950/40 border border-ueh-200/80 dark:border-ueh-800/60 text-xs flex items-start gap-2';
        icon.className = 'text-ueh-600 font-extrabold mt-0.5';
        icon.textContent = 'i';
        content.innerHTML = isEn
          ? `<div class="font-bold text-ueh-800 dark:text-ueh-300">Enter your UEH Student ID &amp; Email to verify</div>
             <div class="text-[11px] text-ueh-700 dark:text-ueh-400">Automatically checks 11-digit MSSV format and @st.ueh.edu.vn domain.</div>`
          : `<div class="font-bold text-ueh-800 dark:text-ueh-300">Nhập MSSV &amp; Email sinh viên UEH để xác thực</div>
             <div class="text-[11px] text-ueh-700 dark:text-ueh-400">Hệ thống tự động kiểm tra định dạng 11 chữ số và đối chiếu hộp thư @st.ueh.edu.vn.</div>`;
        return;
      }

      const check = parseUEHStudent(mssv, email, nameEl ? nameEl.value : '');
      if (!check.valid) {
        box.className =
          'p-2.5 rounded-xl bg-amber-50/90 dark:bg-amber-950/40 border border-amber-200/80 dark:border-amber-800/60 text-xs flex items-start gap-2';
        icon.className = 'text-amber-600 font-extrabold mt-0.5';
        icon.textContent = '!';
        content.innerHTML = `<div class="font-bold text-amber-800 dark:text-amber-300">${check.error}</div>`;
        return;
      }

      const st = check.student;
      box.className =
        'p-2.5 rounded-xl bg-emerald-50/90 dark:bg-emerald-950/40 border border-emerald-200/80 dark:border-emerald-800/60 text-xs flex items-start gap-2';
      icon.className = 'text-emerald-600 font-extrabold mt-0.5';
      icon.textContent = '✓';
      content.innerHTML = isEn
        ? `<div class="font-bold text-emerald-800 dark:text-emerald-300">Verified UEH Student Format • ${st.cohort} (${st.programType})</div>
           <div class="text-[11px] text-emerald-700 dark:text-emerald-400 font-mono">MSSV: ${st.mssv} • Ready for OTP</div>`
        : `<div class="font-bold text-emerald-800 dark:text-emerald-300">Hợp lệ Sinh viên UEH • Khóa ${st.cohort} (${st.programType})</div>
           <div class="text-[11px] text-emerald-700 dark:text-emerald-400 font-mono">MSSV: ${st.mssv} • Sẵn sàng nhận mã OTP</div>`;
    }

    async function handleSendUehOtpSubmit(event) {
      if (event) event.preventDefault();
      const mssv = document.getElementById('authMssvInput').value;
      const email = document.getElementById('authUehEmailInput').value;
      const fullName = document.getElementById('authFullName')?.value || '';
      const isEn = appState.lang === 'en';

      const check = parseUEHStudent(mssv, email, fullName);
      if (!check.valid) {
        showToast(check.error);
        return;
      }

      pendingUehStudent = check.student;
      const submitBtn = document.getElementById('sendOtpSubmitBtn');
      if (submitBtn) submitBtn.disabled = true;

      try {
        if (IS_LIVE_SUPABASE && supabaseClient) {
          const { error } = await supabaseClient.auth.signInWithOtp({
            email: check.student.email,
            options: {
              shouldCreateUser: true,
              data: {
                mssv: check.student.mssv,
                cohort: check.student.cohort,
                program_type: check.student.programType,
                full_name: check.student.name
              }
            }
          });
          if (error) {
            showToast((isEn ? 'OTP send error: ' : 'Lỗi gửi mã OTP: ') + error.message);
            return;
          }
          document.getElementById('sandboxOtpHelperBanner')?.classList.add('hidden');
        } else {
          currentSandboxOtp = String(Math.floor(100000 + Math.random() * 900000));
          const codeEl = document.getElementById('sandboxOtpCodeDisplay');
          if (codeEl) codeEl.textContent = currentSandboxOtp;
          document.getElementById('sandboxOtpHelperBanner')?.classList.remove('hidden');
        }

        const parts = check.student.email.split('@');
        const masked = `${parts[0].slice(0, 2)}***@${parts[1]}`;
        const maskedEl = document.getElementById('maskedUehEmailLabel');
        if (maskedEl) maskedEl.textContent = masked;

        for (let i = 0; i < 6; i++) {
          const d = document.getElementById(`otp-digit-${i}`);
          if (d) d.value = '';
        }

        document.getElementById('uehStep1Form')?.classList.add('hidden');
        document.getElementById('uehStep2OtpView')?.classList.remove('hidden');
        startOtpCountdown();
        setTimeout(() => document.getElementById('otp-digit-0')?.focus(), 80);

        showToast(
          isEn
            ? `6-digit OTP sent to ${check.student.email}`
            : `Đã gửi mã OTP 6 số tới ${check.student.email}`
        );
      } finally {
        if (submitBtn) submitBtn.disabled = false;
      }
    }

    function startOtpCountdown() {
      if (otpCountdownTimer) clearInterval(otpCountdownTimer);
      let secondsLeft = 60;
      const countdownEl = document.getElementById('otpCountdownText');
      const resendBtn = document.getElementById('resendOtpBtn');
      const isEn = appState.lang === 'en';

      if (resendBtn) resendBtn.disabled = true;
      if (countdownEl) {
        countdownEl.textContent = isEn ? `Resend in: ${secondsLeft}s` : `Gửi lại mã sau: ${secondsLeft}s`;
      }

      otpCountdownTimer = setInterval(() => {
        secondsLeft -= 1;
        if (secondsLeft <= 0) {
          clearInterval(otpCountdownTimer);
          otpCountdownTimer = null;
          if (countdownEl) countdownEl.textContent = isEn ? 'Ready to resend' : 'Có thể gửi lại mã';
          if (resendBtn) resendBtn.disabled = false;
        } else if (countdownEl) {
          countdownEl.textContent = isEn ? `Resend in: ${secondsLeft}s` : `Gửi lại mã sau: ${secondsLeft}s`;
        }
      }, 1000);
    }

    function backToUehEmailStep() {
      if (otpCountdownTimer) {
        clearInterval(otpCountdownTimer);
        otpCountdownTimer = null;
      }
      document.getElementById('uehStep2OtpView')?.classList.add('hidden');
      document.getElementById('uehStep1Form')?.classList.remove('hidden');
    }

    function resendUehOtp() {
      handleSendUehOtpSubmit(null);
    }

    function autoFillSandboxOtp() {
      const digits = currentSandboxOtp.split('');
      digits.forEach((digit, idx) => {
        const el = document.getElementById(`otp-digit-${idx}`);
        if (el) el.value = digit;
      });
      setTimeout(() => handleVerifyOtpClick(), 220);
    }

    function handleOtpDigitInput(idx, inputEl) {
      const clean = (inputEl.value || '').replace(/\D/g, '').slice(-1);
      inputEl.value = clean;
      if (clean && idx < 5) {
        document.getElementById(`otp-digit-${idx + 1}`)?.focus();
      }
      let combined = '';
      for (let i = 0; i < 6; i++) {
        combined += document.getElementById(`otp-digit-${i}`)?.value || '';
      }
      if (combined.length === 6) {
        handleVerifyOtpClick();
      }
    }

    function handleOtpKeyDown(idx, event) {
      if (event.key === 'Backspace' && !event.target.value && idx > 0) {
        document.getElementById(`otp-digit-${idx - 1}`)?.focus();
      }
    }

    function handleOtpPaste(event) {
      const pasted = (event.clipboardData || window.clipboardData)?.getData('text') || '';
      const digits = pasted.replace(/\D/g, '').slice(0, 6);
      if (!digits) return;
      event.preventDefault();
      digits.split('').forEach((ch, idx) => {
        const el = document.getElementById(`otp-digit-${idx}`);
        if (el) el.value = ch;
      });
      if (digits.length === 6) {
        handleVerifyOtpClick();
      } else {
        document.getElementById(`otp-digit-${digits.length}`)?.focus();
      }
    }

    async function handleVerifyOtpClick() {
      const isEn = appState.lang === 'en';
      let code = '';
      for (let i = 0; i < 6; i++) {
        code += (document.getElementById(`otp-digit-${i}`)?.value || '').trim();
      }

      if (code.length < 6) {
        showToast(isEn ? 'Please enter all 6 OTP digits.' : 'Vui lòng nhập đủ 6 chữ số mã OTP.');
        return;
      }

      if (!pendingUehStudent) {
        const fallbackCheck = parseUEHStudent(
          document.getElementById('authMssvInput')?.value,
          document.getElementById('authUehEmailInput')?.value,
          document.getElementById('authFullName')?.value
        );
        if (!fallbackCheck.valid) {
          showToast(fallbackCheck.error);
          return;
        }
        pendingUehStudent = fallbackCheck.student;
      }

      if (IS_LIVE_SUPABASE && supabaseClient) {
        const { error } = await supabaseClient.auth.verifyOtp({
          email: pendingUehStudent.email,
          token: code,
          type: 'email'
        });
        if (error) {
          showToast(isEn ? 'Invalid or expired OTP code.' : 'Mã OTP không chính xác hoặc đã hết hạn.');
          return;
        }
      } else if (code !== currentSandboxOtp && code !== '123456') {
        showToast(
          isEn
            ? `Incorrect OTP. Click the Sandbox OTP badge (${currentSandboxOtp}) to auto-fill.`
            : `Mã OTP chưa đúng. Nhấn vào mã Sandbox (${currentSandboxOtp}) phía trên để điền nhanh.`
        );
        return;
      }

      completeUehLogin(pendingUehStudent);
    }

    function completeUehLogin(studentInfo) {
      if (otpCountdownTimer) {
        clearInterval(otpCountdownTimer);
        otpCountdownTimer = null;
      }

      appState.isLoggedIn = true;
      appState.student = {
        ...appState.student,
        name: studentInfo.name || appState.student.name,
        mssv: studentInfo.mssv || appState.student.mssv,
        cohort: studentInfo.cohort || appState.student.cohort,
        programType: studentInfo.programType || 'ĐHCQ',
        email: studentInfo.email || appState.student.email,
        verified: true
      };
      saveState();

      backToUehEmailStep();
      syncAuthUiVisibility();
      switchTab('profile');

      showToast(
        appState.lang === 'en'
          ? `Welcome ${appState.student.name} (${appState.student.cohort} CTD)!`
          : `Chào mừng ${appState.student.name} (${appState.student.cohort} CTD) đã xác thực thành công!`
      );
    }

    async function loginWithUEHOAuth(provider = 'azure') {
      const isEn = appState.lang === 'en';
      if (IS_LIVE_SUPABASE && supabaseClient) {
        const { error } = await supabaseClient.auth.signInWithOAuth({
          provider,
          options: {
            scopes: 'email profile',
            queryParams: {
              hd: 'st.ueh.edu.vn',
              domain_hint: 'st.ueh.edu.vn'
            },
            redirectTo: window.location.origin
          }
        });
        if (error) {
          showToast((isEn ? 'SSO connection error: ' : 'Lỗi kết nối SSO UEH: ') + error.message);
        }
        return;
      }

      const mssvVal = document.getElementById('authMssvInput')?.value || '';
      const emailVal = document.getElementById('authUehEmailInput')?.value || '';
      const nameVal = document.getElementById('authFullName')?.value || '';
      const check = parseUEHStudent(mssvVal, emailVal, nameVal);
      if (check.valid) {
        completeUehLogin(check.student);
        return;
      }

      const providerLabel =
        provider === 'google'
          ? 'Google Workspace (@st.ueh.edu.vn)'
          : provider === 'apple'
            ? 'Apple ID Linked UEH'
            : 'Microsoft 365 UEH SSO';

      openModal(
        'UEH SSO GATEWAY',
        providerLabel,
        `
        <div class="space-y-3.5">
          <p class="text-xs text-slate-600 dark:text-slate-300">
            ${
              isEn
                ? 'Enter your UEH Student ID and @st.ueh.edu.vn email to simulate single sign-on, or continue with a verified CTD test account:'
                : 'Nhập MSSV và Email @st.ueh.edu.vn của bạn để đăng nhập một chạm qua cổng UEH SSO, hoặc dùng tài khoản trải nghiệm CTD:'
            }
          </p>
          <div class="space-y-2">
            <input id="ssoModalMssv" type="text" maxlength="11" placeholder="MSSV (VD: 31231024567)" value="${mssvVal}" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs font-mono" />
            <input id="ssoModalEmail" type="email" placeholder="ten.31231024567@st.ueh.edu.vn" value="${emailVal}" class="w-full px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs font-mono" />
          </div>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 pt-1">
            <button type="button" onclick="submitSsoModalLogin()" class="py-2.5 px-3 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white font-bold text-xs">
              ${isEn ? '✓ Sign in with My UEH ID' : '✓ Đăng nhập bằng MSSV của tôi'}
            </button>
            <button type="button" onclick="closeModal(); completeUehLogin({ name: 'Lê Minh Ngọc', mssv: '31231024567', cohort: 'K49', programType: 'ĐHCQ', email: 'minhngoc.31231024567@st.ueh.edu.vn' });" class="py-2.5 px-3 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 text-slate-800 dark:text-slate-200 font-bold text-xs">
              ${isEn ? '⚡ Demo CTD Account' : '⚡ Tài khoản Trải nghiệm CTD'}
            </button>
          </div>
        </div>
        `
      );
    }

    function submitSsoModalLogin() {
      const mssv = document.getElementById('ssoModalMssv')?.value || '';
      const email = document.getElementById('ssoModalEmail')?.value || '';
      const check = parseUEHStudent(mssv, email);
      if (!check.valid) {
        showToast(check.error);
        return;
      }
      closeModal();
      completeUehLogin(check.student);
    }

    function showSupabaseSqlGuide() {
      const isEn = appState.lang === 'en';
      openModal(
        'SUPABASE LIVE AUTH',
        isEn ? 'Connect Live @st.ueh.edu.vn OTP & SSO' : 'Cấu hình Xác thực Email @st.ueh.edu.vn Thật',
        `
        <div class="space-y-3 text-xs">
          <p>${
            isEn
              ? '1. Replace SUPABASE_URL and SUPABASE_ANON_KEY at the top of the script with your Supabase project credentials.'
              : '1. Thay thế SUPABASE_URL và SUPABASE_ANON_KEY ở đầu thẻ script bằng thông tin dự án Supabase của bạn.'
          }</p>
          <p>${
            isEn
              ? '2. Run this SQL trigger in Supabase SQL Editor to restrict signups strictly to @st.ueh.edu.vn:'
              : '2. Chạy đoạn SQL Trigger sau trong Supabase SQL Editor để chỉ cho phép email sinh viên @st.ueh.edu.vn:'
          }</p>
          <pre class="p-3 rounded-xl bg-slate-950 text-emerald-300 font-mono text-[11px] overflow-x-auto">create or replace function public.enforce_ueh_domain()
returns trigger as $$
begin
  if new.email not like '%@st.ueh.edu.vn' then
    raise exception 'Only @st.ueh.edu.vn student emails allowed';
  end if;
  return new;
end;
$$ language plpgsql security definer;</pre>
        </div>
        `
      );
    }

    function logoutUser() {
      appState.isLoggedIn = false;
      saveState();
      syncAuthUiVisibility();
      showToast(appState.lang === 'en' ? 'Signed out of BLUEPRINT.' : 'Đã đăng xuất khỏi BLUEPRINT.');
    }

    // =========================================================================
    // 5. NAVIGATION & VIEW ROUTER
    // =========================================================================
    function syncAuthUiVisibility() {
      const authView = document.getElementById('view-auth');
      const desktopNav = document.getElementById('desktopNav');
      const mobileNav = document.getElementById('mobileBottomNav');
      const userArea = document.getElementById('headerUserArea');

      if (!appState.isLoggedIn) {
        document.querySelectorAll('.view-section').forEach(sec => sec.classList.add('hidden'));
        authView?.classList.remove('hidden');
        desktopNav?.classList.add('hidden');
        desktopNav?.classList.remove('lg:flex');
        mobileNav?.classList.add('hidden');
        userArea?.classList.add('hidden');
        userArea?.classList.remove('flex');
        return;
      }

      authView?.classList.add('hidden');
      desktopNav?.classList.remove('hidden');
      desktopNav?.classList.add('lg:flex');
      mobileNav?.classList.remove('hidden');
      userArea?.classList.remove('hidden');
      userArea?.classList.add('flex');

      const initials = (appState.student.name || 'SV')
        .split(' ')
        .filter(Boolean)
        .slice(-2)
        .map(w => w[0].toUpperCase())
        .join('') || 'SV';

      const avatarEl = document.getElementById('headerAvatarCircle');
      const nameEl = document.getElementById('headerStudentName');
      if (avatarEl) avatarEl.textContent = initials;
      if (nameEl) nameEl.textContent = appState.student.name;
    }

    function handleBrandClick() {
      if (appState.isLoggedIn) {
        switchTab('dashboard');
      } else {
        window.scrollTo({ top: 0, behavior: 'smooth' });
      }
    }

    function switchTab(tabName) {
      if (!appState.isLoggedIn) {
        syncAuthUiVisibility();
        return;
      }

      const validTabs = ['dashboard', 'profile', 'mbti', 'simulation', 'community'];
      const targetTab = validTabs.includes(tabName) ? tabName : 'profile';
      appState.activeTab = targetTab;
      saveState();

      document.querySelectorAll('.view-section').forEach(sec => sec.classList.add('hidden'));
      document.getElementById(`view-${targetTab}`)?.classList.remove('hidden');

      document.querySelectorAll('.nav-tab-btn').forEach(btn => {
        const isActive = btn.getAttribute('data-tab') === targetTab;
        btn.className = isActive
          ? 'nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5 bg-white dark:bg-slate-900 text-ueh-600 dark:text-ueh-400 shadow-sm'
          : 'nav-tab-btn px-3 py-1.5 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5 text-slate-500 dark:text-slate-400 hover:text-slate-800';
      });

      document.querySelectorAll('.mobile-tab-btn').forEach(btn => {
        const isActive = btn.getAttribute('data-tab') === targetTab;
        btn.className = isActive
          ? 'mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-extrabold text-ueh-600'
          : 'mobile-tab-btn py-1 rounded-xl flex flex-col items-center gap-0.5 text-[10px] font-bold text-slate-400';
      });

      if (targetTab === 'profile') renderProfileSetup();
      if (targetTab === 'mbti') renderMbtiQuestion();
      if (targetTab === 'dashboard') renderDashboardView();
      if (targetTab === 'simulation') renderSimulationView();
      if (targetTab === 'community') renderCommunityView();

      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // =========================================================================
    // 6. SCREEN 2: CTD STUDENT PROFILE SETUP
    // =========================================================================
    function renderProfileSetup() {
      const isEn = appState.lang === 'en';
      const st = appState.student;

      const initials = (st.name || 'SV')
        .split(' ')
        .filter(Boolean)
        .slice(-2)
        .map(w => w[0].toUpperCase())
        .join('') || 'SV';

      const avatarEl = document.getElementById('profileCardAvatar');
      const nameEl = document.getElementById('profileCardName');
      const cohortEl = document.getElementById('profileCohortBadge');
      const metaEl = document.getElementById('profileCardMeta');
      const emailEl = document.getElementById('profileCardEmail');

      if (avatarEl) avatarEl.textContent = initials;
      if (nameEl) nameEl.textContent = st.name;
      if (cohortEl) cohortEl.textContent = `${st.cohort} CTD`;
      if (metaEl) metaEl.textContent = `MSSV: ${st.mssv}`;
      if (emailEl) {
        emailEl.textContent = isEn
          ? `UEH College of Technology and Design • ${st.email}`
          : `Trường Công nghệ và Thiết kế UEH • ${st.email}`;
      }

      const majorListEl = document.getElementById('majorCardsList');
      if (majorListEl) {
        majorListEl.innerHTML = CTD_MAJORS.map(m => {
          const selected = st.majorId === m.id;
          return `
            <button type="button" onclick="selectStudentMajor('${m.id}')" class="w-full text-left p-3.5 rounded-2xl border-2 transition-all flex items-center justify-between gap-3 ${
              selected
                ? 'border-ueh-600 bg-ueh-50/70 dark:bg-ueh-950/50 shadow-sm'
                : 'border-slate-200/80 dark:border-slate-800 bg-white dark:bg-slate-900 hover:border-ueh-300'
            }">
              <div class="flex items-center gap-3 min-w-0">
                <div class="w-10 h-10 rounded-xl ${m.iconBg} flex items-center justify-center text-lg shrink-0">${m.icon}</div>
                <div class="min-w-0">
                  <div class="font-extrabold text-xs sm:text-sm text-slate-900 dark:text-white truncate">${isEn ? m.en : m.title}</div>
                  <div class="text-[11px] text-slate-400 truncate">${isEn ? m.title : m.en}</div>
                  <div class="flex flex-wrap gap-1 mt-1">
                    ${m.tags
                      .map(
                        tag =>
                          `<span class="px-2 py-0.5 rounded bg-slate-100 dark:bg-slate-800 text-[10px] font-semibold text-slate-500 dark:text-slate-400">${tag}</span>`
                      )
                      .join('')}
                  </div>
                </div>
              </div>
              <div class="w-5 h-5 rounded-full border-2 flex items-center justify-center shrink-0 ${
                selected ? 'border-ueh-600 bg-ueh-600 text-white' : 'border-slate-300 dark:border-slate-600'
              }">
                ${selected ? '<span class="text-[10px] font-bold">✓</span>' : ''}
              </div>
            </button>
          `;
        }).join('');
      }

      const skillsEl = document.getElementById('skillPillsList');
      if (skillsEl) {
        skillsEl.innerHTML = CTD_SKILLS.map(sk => {
          const active = (st.skills || []).includes(sk.vi);
          return `
            <button type="button" onclick="toggleStudentSkill('${sk.vi}')" class="px-3.5 py-2 rounded-full text-xs font-bold border transition-all flex items-center gap-1.5 ${
              active
                ? 'bg-ueh-600 border-ueh-600 text-white shadow-sm'
                : 'bg-white dark:bg-slate-900 border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 hover:border-ueh-400'
            }">
              <span>${active ? '✓' : '+'}</span>
              <span>${isEn ? sk.en : sk.vi}</span>
            </button>
          `;
        }).join('');
      }

      const goalsEl = document.getElementById('goalCardsList');
      if (goalsEl) {
        goalsEl.innerHTML = POST_GRAD_GOALS.map(g => {
          const selected = st.goalId === g.id;
          return `
            <button type="button" onclick="selectStudentGoal('${g.id}')" class="w-full text-left p-3.5 rounded-2xl border-2 transition-all flex items-center justify-between gap-3 ${
              selected
                ? 'border-ueh-600 bg-ueh-50/70 dark:bg-ueh-950/50 shadow-sm'
                : 'border-slate-200/80 dark:border-slate-800 bg-white dark:bg-slate-900 hover:border-ueh-300'
            }">
              <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-slate-100 dark:bg-slate-800 flex items-center justify-center text-lg shrink-0">${g.icon}</div>
                <div>
                  <div class="font-extrabold text-xs sm:text-sm text-slate-900 dark:text-white">${isEn ? g.titleEn : g.title}</div>
                  <div class="text-[11px] text-slate-400">${isEn ? g.descEn : g.desc}</div>
                </div>
              </div>
              <div class="w-5 h-5 rounded-full border-2 flex items-center justify-center shrink-0 ${
                selected ? 'border-ueh-600 bg-ueh-600 text-white' : 'border-slate-300 dark:border-slate-600'
              }">
                ${selected ? '<span class="w-2 h-2 rounded-full bg-white"></span>' : ''}
              </div>
            </button>
          `;
        }).join('');
      }
    }

    function selectStudentMajor(majorId) {
      appState.student.majorId = majorId;
      saveState();
      renderProfileSetup();
    }

    function toggleStudentSkill(skillVi) {
      if (!Array.isArray(appState.student.skills)) appState.student.skills = [];
      const idx = appState.student.skills.indexOf(skillVi);
      if (idx > -1) {
        appState.student.skills.splice(idx, 1);
      } else {
        appState.student.skills.push(skillVi);
      }
      saveState();
      renderProfileSetup();
    }

    function selectStudentGoal(goalId) {
      appState.student.goalId = goalId;
      saveState();
      renderProfileSetup();
    }

    function saveStudentProfile() {
      saveState();
      showToast(
        appState.lang === 'en'
          ? 'CTD Profile saved! Starting MBTI Assessment...'
          : 'Đã lưu Hồ sơ CTD! Chuyển sang bài trắc nghiệm MBTI...'
      );
      switchTab('mbti');
    }

    // =========================================================================
    // 7. SCREEN 3: MBTI PERSONALITY ASSESSMENT ENGINE
    // =========================================================================
    const MBTI_ARCHETYPES = {
      ENTP: 'Visionary Innovator',
      ENTJ: 'Strategic Commander',
      ENFP: 'Creative Catalyst',
      ENFJ: 'Inspiring Mentor-Lead',
      INTP: 'Systems Architect',
      INTJ: 'Master Strategist',
      INFP: 'Empathetic Creator',
      INFJ: 'Insightful Visionary',
      ESTP: 'Agile Trailblazer',
      ESTJ: 'Execution Director',
      ESFP: 'Dynamic Experience Maker',
      ESFJ: 'Community Harmonizer',
      ISTP: 'Tactical Problem-Solver',
      ISTJ: 'Precision Analyst',
      ISFP: 'Aesthetic Craftsperson',
      ISFJ: 'Dedicated Guardian'
    };

    function renderMbtiQuestion() {
      const idx = Math.min(MBTI_QUESTIONS.length - 1, Math.max(0, appState.mbti.currentIndex || 0));
      const q = MBTI_QUESTIONS[idx];
      const isEn = appState.lang === 'en';
      const currentAns = appState.mbti.answers[idx];

      const counterEl = document.getElementById('mbtiCounter');
      const pctTextEl = document.getElementById('mbtiPercentText');
      const barEl = document.getElementById('mbtiProgressBar');
      const dimEl = document.getElementById('mbtiDimensionBadge');
      const qViEl = document.getElementById('mbtiQuestionVi');
      const qEnEl = document.getElementById('mbtiQuestionEn');
      const insightEl = document.getElementById('mbtiLiveInsight');
      const prevBtn = document.getElementById('mbtiPrevBtn');
      const nextBtn = document.getElementById('mbtiNextBtn');

      const answeredCount = appState.mbti.answers.filter(a => a !== null && a !== undefined).length;
      const pct = Math.max(8, Math.round(((idx + 1) / MBTI_QUESTIONS.length) * 100));

      if (counterEl) counterEl.textContent = isEn ? `Question ${idx + 1} / 12` : `Câu ${idx + 1} / 12`;
      if (pctTextEl) {
        pctTextEl.textContent = isEn
          ? `${pct}% Progress (${answeredCount}/12 answered)`
          : `Đã hoàn thành ${pct}% (${answeredCount}/12 câu)`;
      }
      if (barEl) barEl.style.width = `${pct}%`;
      if (dimEl) dimEl.textContent = isEn ? q.dimLabelEn : q.dimLabel;
      if (qViEl) qViEl.textContent = isEn ? q.en : q.vi;
      if (qEnEl) qEnEl.textContent = isEn ? q.vi : q.en;

      document.querySelectorAll('.likert-btn').forEach(btn => {
        const score = parseInt(btn.getAttribute('data-score'), 10);
        const circle = btn.querySelector('.likert-circle');
        if (!circle) return;
        if (currentAns === score) {
          circle.classList.add('ring-4', 'ring-ueh-300', 'scale-110');
        } else {
          circle.classList.remove('ring-4', 'ring-ueh-300', 'scale-110');
        }
      });

      if (insightEl) {
        if (currentAns === null || currentAns === undefined || currentAns === 0) {
          insightEl.textContent = t('mbtiDefaultInsight');
        } else if (currentAns > 0) {
          insightEl.textContent = isEn ? q.insightPosEn : q.insightPos;
        } else {
          insightEl.textContent = isEn ? q.insightNegEn : q.insightNeg;
        }
      }

      if (prevBtn) prevBtn.disabled = idx === 0;
      if (nextBtn) {
        nextBtn.textContent =
          idx === MBTI_QUESTIONS.length - 1 ? t('mbtiFinishBtn') : t('mbtiNextBtn');
      }

      const resCard = document.getElementById('mbtiResultCard');
      if (resCard) {
        if (appState.mbti.completed) {
          resCard.classList.remove('hidden');
          renderMbtiResultSummary();
        } else {
          resCard.classList.add('hidden');
        }
      }
    }

    function selectMbtiOption(score) {
      const idx = appState.mbti.currentIndex || 0;
      appState.mbti.answers[idx] = score;
      saveState();
      renderMbtiQuestion();

      const autoAdvance = document.getElementById('mbtiAutoAdvanceChk')?.checked;
      if (autoAdvance) {
        setTimeout(() => {
          if (idx < MBTI_QUESTIONS.length - 1) {
            appState.mbti.currentIndex = idx + 1;
            saveState();
            renderMbtiQuestion();
          } else {
            finishMbtiAssessment();
          }
        }, 260);
      }
    }

    function prevMbtiQuestion() {
      if ((appState.mbti.currentIndex || 0) > 0) {
        appState.mbti.currentIndex -= 1;
        saveState();
        renderMbtiQuestion();
      }
    }

    function nextMbtiQuestion() {
      const idx = appState.mbti.currentIndex || 0;
      if (appState.mbti.answers[idx] === null || appState.mbti.answers[idx] === undefined) {
        appState.mbti.answers[idx] = 0;
      }
      if (idx < MBTI_QUESTIONS.length - 1) {
        appState.mbti.currentIndex = idx + 1;
        saveState();
        renderMbtiQuestion();
      } else {
        finishMbtiAssessment();
      }
    }

    function autoCompleteMbtiDemo() {
      const samplePattern = [2, 1, 2, 2, 2, 1, 1, 2, -1, 2, 1, 2];
      appState.mbti.answers = appState.mbti.answers.map((ans, i) =>
        ans === null || ans === undefined ? samplePattern[i] : ans
      );
      appState.mbti.currentIndex = MBTI_QUESTIONS.length - 1;
      finishMbtiAssessment();
    }

    function finishMbtiAssessment() {
      const sums = { EI: 0, SN: 0, TF: 0, JP: 0 };
      MBTI_QUESTIONS.forEach((q, idx) => {
        const val = appState.mbti.answers[idx] ?? 0;
        sums[q.dim] += val;
      });

      const pctE = Math.min(92, Math.max(8, Math.round(50 + (sums.EI / 6) * 40)));
      const pctN = Math.min(92, Math.max(8, Math.round(50 + (sums.SN / 6) * 40)));
      const pctT = Math.min(92, Math.max(8, Math.round(50 + (sums.TF / 6) * 40)));
      const pctP = Math.min(92, Math.max(8, Math.round(50 + (sums.JP / 6) * 40)));

      const type =
        (pctE >= 50 ? 'E' : 'I') +
        (pctN >= 50 ? 'N' : 'S') +
        (pctT >= 50 ? 'T' : 'F') +
        (pctP >= 50 ? 'P' : 'J');

      const wasMbtiDone = Boolean(appState.mbti.completed);
      appState.mbti.completed = true;
      appState.mbti.type = type;
      appState.mbti.archetype = MBTI_ARCHETYPES[type] || 'Visionary Innovator';
      appState.mbti.percentages = {
        E: pctE,
        I: 100 - pctE,
        N: pctN,
        S: 100 - pctN,
        T: pctT,
        F: 100 - pctT,
        P: pctP,
        J: 100 - pctP
      };

      if (appState.community.isMatched) {
        const best = computeBestMentorMatch();
        appState.community.matchedMentorId = best.mentor.id;
        appState.community.matchScore = best.score;
      }

      saveState();
      renderMbtiQuestion();

      const isEn = appState.lang === 'en';
      if (!wasMbtiDone && appState.simulation.completed) {
        showToast(
          isEn
            ? `🎉 MBTI (${type}) & Simulation both complete! Visit Cohort & Mentor to match your Mentor!`
            : `🎉 Đã xong cả MBTI (${type}) & Simulation! Vào tab Cohort & Mentor để ghép Mentor ngay!`
        );
      } else {
        showToast(
          isEn
            ? `MBTI Assessment Complete: ${type} — ${appState.mbti.archetype}!`
            : `Hoàn thành Trắc nghiệm MBTI: ${type} — ${appState.mbti.archetype}!`
        );
      }
    }

    function renderMbtiResultSummary() {
      const isEn = appState.lang === 'en';
      const p = appState.mbti.percentages;
      const titleEl = document.getElementById('mbtiResultTitle');
      const descEl = document.getElementById('mbtiResultDesc');
      const barsEl = document.getElementById('mbtiResultBars');

      if (titleEl) titleEl.textContent = `${appState.mbti.type} — ${appState.mbti.archetype}`;
      if (descEl) {
        descEl.textContent = isEn
          ? 'Your 4 cognitive dimensions have been synchronized with Career Recommendations and Mentor Matching.'
          : '4 trục tính cách của bạn đã được đồng bộ hóa với hệ thống Khuyến nghị Nghề nghiệp và Ghép Mentor.';
      }

      if (barsEl) {
        const axes = [
          { left: 'Extraversion (E)', right: 'Introversion (I)', lPct: p.E, rPct: p.I },
          { left: 'Intuition (N)', right: 'Sensing (S)', lPct: p.N, rPct: p.S },
          { left: 'Thinking (T)', right: 'Feeling (F)', lPct: p.T, rPct: p.F },
          { left: 'Perceiving (P)', right: 'Judging (J)', lPct: p.P, rPct: p.J }
        ];
        barsEl.innerHTML = axes
          .map(
            ax => `
            <div class="p-3 rounded-2xl bg-slate-50 dark:bg-slate-800/70 space-y-1.5 text-xs">
              <div class="flex justify-between font-bold">
                <span class="text-ueh-600">${ax.left} ${ax.lPct}%</span>
                <span class="text-indigo-500">${ax.rPct}% ${ax.right}</span>
              </div>
              <div class="w-full h-2 bg-indigo-200 dark:bg-indigo-950 rounded-full overflow-hidden">
                <div class="h-full bg-ueh-600 rounded-full" style="width: ${ax.lPct}%"></div>
              </div>
            </div>
          `
          )
          .join('');
      }
    }

    function resetMbtiTest() {
      appState.mbti.currentIndex = 0;
      appState.mbti.answers = Array(12).fill(null);
      appState.mbti.completed = false;
      saveState();
      renderMbtiQuestion();
    }

    // =========================================================================
    // 8. SCREEN 4: AI MATCH DASHBOARD & PERSONALIZED CAREER ENGINE
    // =========================================================================
    let currentCareerFilter = 'all';

    function getActiveCaseOptionData() {
      const industry =
        INDUSTRY_CASE_BANK.find(ind => ind.id === appState.simulation.selectedIndustry) ||
        INDUSTRY_CASE_BANK[0];
      const caseObj = industry.cases[appState.simulation.selectedCaseIndex] || industry.cases[0];
      const caseKey = `${industry.id}:${caseObj.id}`;
      const lockedCases = appState.simulation.lockedCases || {};
      const lockedApproach = lockedCases[caseKey] || null;
      const optKey = lockedApproach || appState.simulation.selectedApproach || 'A';
      const opt = caseObj.options[optKey] || caseObj.options.A;
      return { industry, caseObj, caseKey, lockedApproach, optKey, opt };
    }

    function computePersonalizedCareers() {
      const isEn = appState.lang === 'en';
      const student = appState.student;
      const majorObj = CTD_MAJORS.find(m => m.id === student.majorId) || CTD_MAJORS[0];
      const pcts = appState.mbti.percentages || { E: 60, I: 40, N: 70, S: 30, T: 60, F: 40, P: 60, J: 40 };
      const activeIndustry = appState.simulation.selectedIndustry || 'marketing';
      const activeApproach = appState.simulation.selectedApproach || 'A';

      const scored = CAREER_DATABASE.map(career => {
        let score = 54;
        const reasonsVi = [];
        const reasonsEn = [];

        // 1. CTD Major Alignment (up to +20 pts)
        const majorIdx = career.primaryMajors.indexOf(student.majorId);
        if (majorIdx === 0) {
          score += 20;
          reasonsVi.push(`Khớp chuyên ngành ${majorObj.title}`);
          reasonsEn.push(`Direct fit with ${majorObj.en}`);
        } else if (majorIdx > 0) {
          score += 13;
          reasonsVi.push(`Liên ngành với ${majorObj.title}`);
          reasonsEn.push(`Cross-major synergy with ${majorObj.en}`);
        }

        // 2. Student Selected Skills Alignment (up to +12 pts)
        const matchedSkills = (student.skills || []).filter(sk => career.matchingSkills.includes(sk));
        if (matchedSkills.length > 0) {
          score += Math.min(12, matchedSkills.length * 4);
          const firstSkillObj = CTD_SKILLS.find(s => s.vi === matchedSkills[0]);
          const skillLabel = isEn && firstSkillObj ? firstSkillObj.en : matchedSkills[0];
          reasonsVi.push(`Sở hữu kỹ năng ${skillLabel}${matchedSkills.length > 1 ? ` (+${matchedSkills.length - 1})` : ''}`);
          reasonsEn.push(`Matches ${skillLabel}${matchedSkills.length > 1 ? ` (+${matchedSkills.length - 1})` : ''}`);
        }

        // 3. MBTI Continuous Axis Synergy (up to +10 pts)
        let mbtiWeighted = 0;
        Object.entries(career.mbtiBias || {}).forEach(([axisLetter, weight]) => {
          const axisPct = pcts[axisLetter] || 50;
          mbtiWeighted += (axisPct / 100) * weight;
        });
        const mbtiBonus = Math.round(mbtiWeighted * 11);
        score += mbtiBonus;
        if (mbtiBonus >= 6) {
          reasonsVi.push(`Tương thích trục tính cách ${appState.mbti.type}`);
          reasonsEn.push(`Aligned with ${appState.mbti.type} cognitive style`);
        }

        // 4. Simulation Behavioral Choice Alignment (up to +10 pts)
        const indMatch = career.preferredIndustries.includes(activeIndustry);
        const appMatch = career.preferredApproaches.includes(activeApproach);
        if (indMatch) score += career.preferredIndustries[0] === activeIndustry ? 6 : 4;
        if (appMatch) score += career.preferredApproaches[0] === activeApproach ? 4 : 2;
        if (indMatch || appMatch) {
          const { opt } = getActiveCaseOptionData();
          reasonsVi.push(`Hợp hành vi Hướng ${activeApproach} (${opt.tag})`);
          reasonsEn.push(`Fits Approach ${activeApproach} (${opt.tag})`);
        }

        // 5. Post-Grad Goal Alignment (+4 pts)
        if ((career.preferredGoals || []).includes(student.goalId)) {
          score += 4;
        }

        const finalMatch = Math.min(98, Math.max(66, score));
        const rationale = isEn
          ? reasonsEn.slice(0, 3).join(' • ') || 'Aligned with your CTD multidisciplinary profile'
          : reasonsVi.slice(0, 3).join(' • ') || 'Phù hợp với nền tảng liên ngành UEH CTD';

        return {
          ...career,
          match: finalMatch,
          matchedSkills,
          rationale
        };
      });

      return scored.sort((a, b) => b.match - a.match);
    }

    function renderDashboardView() {
      const isEn = appState.lang === 'en';
      const { opt } = getActiveCaseOptionData();
      const rankedCareers = computePersonalizedCareers();
      const topCareer = rankedCareers[0];
      const majorObj = CTD_MAJORS.find(m => m.id === appState.student.majorId) || CTD_MAJORS[0];

      document.getElementById('dashArchetypeTitle').textContent = `${appState.mbti.type} • ${appState.mbti.archetype}`;
      document.getElementById('dashArchetypeDesc').textContent = isEn
        ? `${majorObj.en} • Top Career Fit: ${topCareer.title} (${topCareer.match}%)`
        : `Chuyên ngành ${majorObj.title} • Nghề phù hợp nhất: ${topCareer.title} (${topCareer.match}%)`;

      const heroScore = topCareer.match;
      document.getElementById('heroFitPercent').textContent = `${heroScore}%`;
      const compatSub = document.getElementById('dashAiCompatSubText');
      if (compatSub) {
        compatSub.textContent = isEn
          ? `Highest alignment with ${topCareer.title}`
          : `Độ tương thích cao nhất với ${topCareer.title}`;
      }

      const circumference = 263.89;
      const offset = circumference - (heroScore / 100) * circumference;
      document.getElementById('heroFitRing').style.strokeDashoffset = offset.toFixed(1);

      const heroPills = document.getElementById('dashHeroPills');
      if (heroPills) {
        const pill1 = isEn ? majorObj.en : majorObj.title;
        const pill2 = `${appState.mbti.type} • ${opt.tag}`;
        const pill3 = topCareer.title;
        heroPills.innerHTML = [pill1, pill2, pill3]
          .map(label => `<span class="px-3 py-1 rounded-full bg-white/15 text-[11px] font-semibold">✦ ${label}</span>`)
          .join('');
      }

      document.getElementById('dashStrengthText').textContent = isEn ? opt.strengthsEn : opt.strengthsVi;
      document.getElementById('dashWeaknessText').textContent = isEn ? opt.weaknessesEn : opt.weaknessesVi;
      document.getElementById('dashBestRoleBadge').textContent = `${topCareer.title} (${topCareer.match}%)`;

      renderDashboardMentorSlot();
      filterCareers(currentCareerFilter);
    }

    function renderDashboardMentorSlot() {
      const slot = document.getElementById('dashMentorSlot');
      if (!slot) return;
      const isEn = appState.lang === 'en';
      const mbtiDone = Boolean(appState.mbti.completed);
      const simDone = Boolean(appState.simulation.completed);

      if (appState.community.isMatched && appState.community.matchedMentorId) {
        const mentor = getMatchedMentor();
        const score = appState.community.matchScore || 95;
        slot.innerHTML = `
          <div class="flex items-center justify-between">
            <span class="text-xs font-extrabold uppercase tracking-wider text-emerald-600">${t('dashCommCardTag')}</span>
            <span class="px-2 py-0.5 rounded-full bg-emerald-50 dark:bg-emerald-950 text-emerald-700 dark:text-emerald-300 text-[10px] font-bold">${mentor.cohortSize} ${isEn ? 'Students' : 'Sinh viên'} • ${score}% Match</span>
          </div>
          <div class="flex items-center gap-3 p-3 rounded-2xl bg-slate-50 dark:bg-slate-800/80">
            <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-ueh-600 to-indigo-700 text-white font-extrabold text-xs flex items-center justify-center shrink-0">${mentor.initials}</div>
            <div class="min-w-0">
              <div class="text-[10px] font-bold text-ueh-600">Cohort ${mentor.cohortCode} • ${isEn ? 'Matched Mentor' : 'Mentor Đã Ghép'}</div>
              <div class="font-extrabold text-sm text-slate-900 dark:text-white truncate">${mentor.name}</div>
              <div class="text-[11px] text-slate-500 truncate">${isEn ? mentor.roleEn : mentor.roleVi}</div>
            </div>
          </div>
          <button type="button" onclick="switchTab('community')" class="w-full py-2.5 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white text-xs font-bold transition-colors">
            ${t('dashJoinCohortBtn')}
          </button>
        `;
        return;
      }

      const bothDone = mbtiDone && simDone;
      const doneCount = (mbtiDone ? 1 : 0) + (simDone ? 1 : 0);

      slot.innerHTML = `
        <div class="flex items-center justify-between">
          <span class="text-xs font-extrabold uppercase tracking-wider text-ueh-600">${t('dashCommCardTag')}</span>
          <span class="px-2 py-0.5 rounded-full ${bothDone ? 'bg-emerald-100 text-emerald-700' : 'bg-amber-50 dark:bg-amber-950/60 text-amber-700 dark:text-amber-300'} font-mono text-[10px] font-bold">${doneCount}/2 ${isEn ? 'Completed' : 'Hoàn thành'}</span>
        </div>
        <div class="space-y-2">
          <div class="font-extrabold text-xs sm:text-sm text-slate-900 dark:text-white">${t('dashLockTitle')}</div>
          <p class="text-[11px] text-slate-500 dark:text-slate-400 leading-relaxed">${t('dashLockSub')}</p>
          <div class="space-y-1.5 text-xs">
            <button type="button" onclick="switchTab('mbti')" class="w-full flex items-center justify-between px-3 py-2 rounded-xl border ${mbtiDone ? 'bg-emerald-50/70 dark:bg-emerald-950/30 border-emerald-200 dark:border-emerald-800 text-emerald-700 dark:text-emerald-300' : 'bg-slate-50 dark:bg-slate-800 border-slate-200 dark:border-slate-700 text-slate-700 dark:text-slate-200 hover:border-ueh-400'}">
              <span class="font-bold">${mbtiDone ? '✅' : '⏳'} 1. MBTI Personality Test</span>
              <span class="text-[11px] font-bold text-ueh-600">${mbtiDone ? (isEn ? 'Done' : 'Xong') : (isEn ? 'Start →' : 'Làm ngay →')}</span>
            </button>
            <button type="button" onclick="switchTab('simulation')" class="w-full flex items-center justify-between px-3 py-2 rounded-xl border ${simDone ? 'bg-emerald-50/70 dark:bg-emerald-950/30 border-emerald-200 dark:border-emerald-800 text-emerald-700 dark:text-emerald-300' : 'bg-slate-50 dark:bg-slate-800 border-slate-200 dark:border-slate-700 text-slate-700 dark:text-slate-200 hover:border-ueh-400'}">
              <span class="font-bold">${simDone ? '✅' : '⏳'} 2. Case Simulation</span>
              <span class="text-[11px] font-bold text-ueh-600">${simDone ? (isEn ? 'Done' : 'Xong') : (isEn ? 'Start →' : 'Thử sức →')}</span>
            </button>
          </div>
        </div>
        ${
          bothDone
            ? `<button type="button" onclick="triggerMentorMatching(true)" class="w-full py-2.5 rounded-xl bg-gradient-to-r from-ueh-600 to-indigo-600 hover:from-ueh-700 hover:to-indigo-700 text-white text-xs font-extrabold shadow-blue-glow transition-all">${t('dashUnlockMatchBtn')}</button>`
            : `<button type="button" onclick="switchTab('${!mbtiDone ? 'mbti' : 'simulation'}')" class="w-full py-2.5 rounded-xl bg-slate-900 dark:bg-ueh-600 text-white text-xs font-bold transition-colors">${!mbtiDone ? t('commStep1Btn') : t('commStep2Btn')}</button>`
        }
      `;
    }

    function filterCareers(mode) {
      currentCareerFilter = mode;
      const isEn = appState.lang === 'en';
      const rankedCareers = computePersonalizedCareers();
      const top5Careers = rankedCareers.slice(0, 5);

      const pillActive = 'px-3.5 py-1.5 rounded-full bg-ueh-600 text-white text-xs font-bold shrink-0';
      const pillInactive = 'px-3.5 py-1.5 rounded-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-xs font-semibold shrink-0';

      const allBtn = document.getElementById('careerFilterAll');
      if (allBtn) {
        allBtn.className = mode === 'all' ? pillActive : pillInactive;
        allBtn.textContent = isEn ? `All (${top5Careers.length})` : `Tất cả (${top5Careers.length})`;
      }
      document.getElementById('careerFilterTop').className = mode === 'top' ? pillActive : pillInactive;
      document.getElementById('careerFilterTrend').className = mode === 'trending' ? pillActive : pillInactive;

      let list = top5Careers;
      if (mode === 'top') list = top5Careers.filter(c => c.match >= 85);
      if (mode === 'trending') list = top5Careers.filter(c => c.trending);
      if (list.length === 0) list = top5Careers.slice(0, 2);

      const grid = document.getElementById('careerCardsGrid');
      grid.innerHTML = list
        .map((c, idx) => {
          return `
          <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border ${idx === 0 ? 'border-ueh-300 dark:border-ueh-700' : 'border-slate-200/80 dark:border-slate-800'} shadow-card space-y-4">
            <div class="flex items-start justify-between gap-3">
              <div class="flex items-center gap-3">
                <div class="w-11 h-11 rounded-2xl bg-ueh-50 dark:bg-ueh-950 text-ueh-600 flex items-center justify-center font-extrabold text-base shrink-0">
                  ${idx === 0 ? '★' : '❖'}
                </div>
                <div>
                  <div class="flex flex-wrap items-center gap-1.5">
                    <h3 class="font-extrabold text-base text-slate-900 dark:text-white">${c.title}</h3>
                    ${idx === 0 ? `<span class="px-2 py-0.5 rounded bg-ueh-600 text-white text-[10px] font-extrabold">TOP 1 FIT</span>` : ''}
                  </div>
                  <div class="text-xs text-slate-400 font-medium">${c.sub}</div>
                </div>
              </div>
              <span class="px-2.5 py-1 rounded-full bg-emerald-50 dark:bg-emerald-950 text-emerald-700 dark:text-emerald-300 font-mono text-xs font-extrabold shrink-0">
                ✓ ${c.match}% Match
              </span>
            </div>

            <!-- Personalized Rationale Strip -->
            <div class="px-3 py-2 rounded-xl bg-ueh-50/80 dark:bg-ueh-950/50 border border-ueh-200/60 dark:border-ueh-800/60 text-[11px] text-ueh-800 dark:text-ueh-300 font-semibold">
              ${t('cardWhyMatchLabel')} <span class="font-normal">${c.rationale}</span>
            </div>

            <p class="text-xs text-slate-600 dark:text-slate-300 leading-relaxed">
              ${isEn ? c.descEn : c.desc}
            </p>

            <div class="grid grid-cols-2 gap-2.5 p-3 rounded-2xl bg-slate-50 dark:bg-slate-800/70 text-xs">
              <div>
                <div class="text-[10px] text-slate-400">${t('cardDemandLabel')}</div>
                <div class="font-bold text-ueh-600 mt-0.5">↗ ${isEn ? c.demandEn : c.demand}</div>
              </div>
              <div>
                <div class="text-[10px] text-slate-400">${t('cardSalaryLabel')}</div>
                <div class="font-mono font-bold text-slate-900 dark:text-white mt-0.5">${c.salary}</div>
              </div>
            </div>

            <div class="space-y-1.5">
              <div class="text-[11px] font-semibold text-slate-400">${t('cardSkillsLabel')}</div>
              <div class="flex flex-wrap gap-1.5">
                ${c.skills
                  .map(
                    sk =>
                      `<span class="px-2.5 py-1 rounded-lg bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 text-[11px] font-semibold">${sk}</span>`
                  )
                  .join('')}
              </div>
            </div>

            <div class="grid grid-cols-2 gap-2.5 pt-1">
              <button type="button" onclick="openCareerRoadmap('${c.id}')" class="py-2.5 rounded-xl bg-ueh-50 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 hover:bg-ueh-100 text-xs font-bold transition-colors">
                ${t('cardRoadmapBtn')}
              </button>
              <button type="button" onclick="switchTab('simulation')" class="py-2.5 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white text-xs font-bold shadow-sm transition-colors">
                ${t('cardTryNowBtn')}
              </button>
            </div>
          </div>
        `;
        })
        .join('');
    }

    function openCareerRoadmap(careerId) {
      const rankedCareers = computePersonalizedCareers();
      const career = rankedCareers.find(c => c.id === careerId) || CAREER_DATABASE.find(c => c.id === careerId);
      if (!career) return;
      const isEn = appState.lang === 'en';
      const steps = isEn ? career.roadmapEn : career.roadmap;

      openModal(
        `${career.match}% AI MATCH`,
        `${career.title} — ${isEn ? '6-Month CTD Roadmap' : 'Lộ trình 6 Tháng CTD'}`,
        `
        <div class="space-y-3">
          <div class="p-3 rounded-2xl bg-emerald-50 dark:bg-emerald-950/50 border border-emerald-200/70 dark:border-emerald-800 text-xs text-emerald-800 dark:text-emerald-300 font-semibold">
            ${t('cardWhyMatchLabel')} ${career.rationale || ''}
          </div>
          <p>${isEn ? career.descEn : career.desc}</p>
          <div class="space-y-2">
            ${steps
              .map(
                (step, idx) => `
              <div class="p-3 rounded-2xl bg-ueh-50/80 dark:bg-ueh-950/60 border border-ueh-200/70 dark:border-ueh-800 flex items-start gap-2.5">
                <span class="w-5 h-5 rounded-full bg-ueh-600 text-white text-[11px] font-bold flex items-center justify-center shrink-0 mt-0.5">${idx + 1}</span>
                <span>${step}</span>
              </div>
            `
              )
              .join('')}
          </div>
          <button type="button" onclick="closeModal(); switchTab('simulation');" class="w-full py-3 rounded-xl bg-ueh-600 text-white font-bold text-xs">
            ${isEn ? '▶ Practice with Real Mini-Tasks' : '▶ Thực hành ngay qua Mini-task thực chiến'}
          </button>
        </div>
        `
      );
    }

    function askAiAdvisor(questionText) {
      const box = document.getElementById('aiChatMessages');
      if (!box) return;
      const isEn = appState.lang === 'en';
      const topCareer = computePersonalizedCareers()[0];
      const majorObj = CTD_MAJORS.find(m => m.id === appState.student.majorId) || CTD_MAJORS[0];

      box.innerHTML += `
        <div class="p-2.5 rounded-2xl bg-ueh-500/40 border border-white/15 text-right ml-6">
          ${questionText}
        </div>
      `;

      let reply = isEn
        ? `Based on your ${appState.mbti.type} profile and ${majorObj.en} major, your #1 match is ${topCareer.title} (${topCareer.match}%). Focus on ${topCareer.skills.slice(0, 2).join(' & ')} and review your case with your Cohort Mentor!`
        : `Dựa trên hồ sơ ${appState.mbti.type} và chuyên ngành ${majorObj.title}, vị trí phù hợp nhất của bạn là ${topCareer.title} (${topCareer.match}%). Hãy ưu tiên trau dồi ${topCareer.skills.slice(0, 2).join(' & ')} và thảo luận trực tiếp cùng Mentor nhóm nhé!`;

      if (questionText.toLowerCase().includes('product designer') || questionText.toLowerCase().includes('big tech')) {
        reply = isEn
          ? 'Big Tech Product Designer roles value: (1) Systems thinking & Design Tokens, (2) Quantitative UX metrics, and (3) Rapid AI prototyping. Completing the GreenGo Mobility case boosts your portfolio score by +12%!'
          : 'Vị trí Product Designer tại Big Tech ưu tiên 3 yếu tố: (1) Tư duy Design System & Token, (2) Đo lường UX bằng dữ liệu, và (3) Rapid Prototyping tích hợp AI. Hoàn thành case GreenGo Mobility sẽ cộng thêm +12% điểm hồ sơ của bạn!';
      } else if (questionText.toLowerCase().includes('portfolio') || questionText.toLowerCase().includes('ai product manager')) {
        reply = isEn
          ? 'Yes! UEH CTD hosts bi-weekly AI Product Manager portfolio clinics with VNG & MoMo product leads inside your Cohort mentorship hub.'
          : 'Có! Viện UEH CTD tổ chức buổi Portfolio Clinic định kỳ 2 tuần/lần cùng các Product Lead từ VNG & MoMo ngay trong không gian Mentorship của Cohort CTD.';
      }

      box.innerHTML += `
        <div class="p-3 rounded-2xl bg-white/10 border border-white/10 leading-relaxed mr-4">
          🤖 ${reply}
        </div>
      `;
      box.scrollTop = box.scrollHeight;
    }

    function handleAiChatSubmit(event) {
      event.preventDefault();
      const input = document.getElementById('aiChatInput');
      const val = input.value.trim();
      if (!val) return;
      input.value = '';
      askAiAdvisor(val);
    }

    // =========================================================================
    // 9. SCREEN 5: SIMULATION, MULTI-INDUSTRY CASES & MINI-TASKS
    // =========================================================================
    let currentMiniTaskFilter = 'all';

    function renderSimulationView() {
      const xp = appState.simulation.xp;
      document.getElementById('simXpBadge').textContent = `${xp} XP`;
      document.getElementById('leaderboardUserXp').textContent =
        `${3 + appState.simulation.completedTasks.length} Mini-tasks • ${xp} XP`;

      const steps = appState.simulation.activeTaskSteps;
      const pct = Math.min(100, Math.round((steps / 4) * 100));
      document.getElementById('activeTaskProgressText').textContent =
        appState.lang === 'en'
          ? `${steps}/4 Tasks (${pct}%)`
          : `${steps}/4 Nhiệm vụ (${pct}%)`;
      document.getElementById('activeTaskProgressBar').style.width = `${pct}%`;

      const totalCases = INDUSTRY_CASE_BANK.reduce((sum, ind) => sum + ind.cases.length, 0);
      const solvedCount = Object.keys(appState.simulation.lockedCases || {}).length;
      const counterBadge = document.getElementById('solvedCasesCounterBadge');
      if (counterBadge) counterBadge.textContent = `${solvedCount}/${totalCases} Cases`;

      renderIndustryCaseSelector();
      renderCaseAnalysisOutput();
      filterMiniTasks(currentMiniTaskFilter);
    }

    function renderIndustryCaseSelector() {
      const isEn = appState.lang === 'en';
      const { industry, caseObj, lockedApproach } = getActiveCaseOptionData();
      const lockedCases = appState.simulation.lockedCases || {};

      const trackContainer = document.getElementById('industryCaseTrackPills');
      if (trackContainer) {
        trackContainer.innerHTML = INDUSTRY_CASE_BANK.map(ind => {
          const active = ind.id === industry.id;
          return `
            <button type="button" onclick="selectSimulationIndustry('${ind.id}')" class="px-3.5 py-2 rounded-full text-xs font-bold shrink-0 transition-all ${
              active
                ? 'bg-ueh-600 text-white shadow-sm'
                : 'bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:bg-ueh-50'
            }">
              ${isEn ? ind.nameEn : ind.nameVi}
            </button>
          `;
        }).join('');
      }

      const casePills = document.getElementById('industryCaseSelectorPills');
      if (casePills) {
        casePills.innerHTML = industry.cases
          .map((c, idx) => {
            const active = idx === appState.simulation.selectedCaseIndex;
            const key = `${industry.id}:${c.id}`;
            const lockedChoice = lockedCases[key];
            return `
              <button type="button" onclick="selectSimulationCase(${idx})" class="px-3 py-1.5 rounded-xl text-xs font-bold border transition-all flex items-center gap-1.5 ${
                active
                  ? 'border-ueh-600 bg-ueh-50 dark:bg-ueh-950/60 text-ueh-700 dark:text-ueh-300'
                  : 'border-slate-200 dark:border-slate-700 text-slate-500 dark:text-slate-400 hover:border-ueh-300'
              }">
                <span>${lockedChoice ? '🔒' : '●'}</span>
                <span>${isEn ? `Scenario ${idx + 1}` : `Tình huống ${idx + 1}`}</span>
                ${lockedChoice ? `<span class="px-1.5 py-0.2 rounded bg-emerald-100 dark:bg-emerald-950 text-emerald-700 dark:text-emerald-300 font-mono text-[10px]">${lockedChoice}</span>` : ''}
              </button>
            `;
          })
          .join('');
      }

      document.getElementById('activeCaseTag').textContent = isEn ? caseObj.tagEn : caseObj.tagVi;
      document.getElementById('activeCaseTitle').textContent = isEn ? caseObj.titleEn : caseObj.titleVi;
      document.getElementById('activeCasePromptDesc').textContent = isEn ? caseObj.promptEn : caseObj.promptVi;

      const cardsWrap = document.getElementById('approachCardsContainer');
      if (cardsWrap) {
        const badgeColors = { A: 'bg-ueh-600', B: 'bg-indigo-600', C: 'bg-emerald-600' };
        const tagColors = { A: 'text-ueh-600', B: 'text-indigo-600', C: 'text-emerald-600' };

        cardsWrap.innerHTML = ['A', 'B', 'C']
          .map(k => {
            const opt = caseObj.options[k];
            const isLocked = Boolean(lockedApproach);
            const isChosenLocked = lockedApproach === k;
            const label = isEn ? `Approach ${k}` : `Hướng ${k}`;

            let cardStyle = 'border-slate-200 dark:border-slate-700 bg-white dark:bg-slate-800/50 hover:border-ueh-300 cursor-pointer';
            let footerStyle = 'border-slate-100 dark:border-slate-700 text-[11px] font-semibold text-slate-400';
            let footerLabel = t('appSelectHint');

            if (isChosenLocked) {
              cardStyle = 'border-ueh-600 bg-ueh-50/80 dark:bg-ueh-950/60 shadow-sm ring-2 ring-ueh-500/25 cursor-default';
              footerStyle = 'border-ueh-200/70 dark:border-ueh-800 text-[11px] font-extrabold text-emerald-600 dark:text-emerald-400';
              footerLabel = t('appSelectedHint');
            } else if (isLocked) {
              cardStyle = 'border-slate-200/70 dark:border-slate-800 bg-slate-100/70 dark:bg-slate-900/40 opacity-50 cursor-not-allowed';
              footerStyle = 'border-slate-200/60 dark:border-slate-800 text-[11px] font-semibold text-slate-400';
              footerLabel = t('appLockedOtherHint');
            }

            return `
              <button type="button" ${isLocked ? 'disabled' : ''} onclick="selectClientApproach('${k}')" id="approachCard${k}" class="text-left p-4 rounded-2xl border-2 transition-all flex flex-col justify-between ${cardStyle}">
                <div>
                  <div class="flex items-center justify-between mb-1.5">
                    <span class="px-2 py-0.5 rounded ${badgeColors[k]} text-white text-[11px] font-bold">${label}</span>
                    <span class="text-[11px] font-mono font-bold ${tagColors[k]}">${opt.tag}</span>
                  </div>
                  <h4 class="font-extrabold text-xs sm:text-sm text-slate-900 dark:text-white mb-1">${isEn ? opt.titleEn : opt.titleVi}</h4>
                  <p class="text-[11px] text-slate-500 dark:text-slate-400">${isEn ? opt.descEn : opt.descVi}</p>
                </div>
                <div class="mt-3 pt-2 border-t ${footerStyle}">
                  ${footerLabel}
                </div>
              </button>
            `;
          })
          .join('');
      }
    }

    function selectSimulationIndustry(industryId) {
      appState.simulation.selectedIndustry = industryId;
      appState.simulation.selectedCaseIndex = 0;
      saveState();
      renderSimulationView();
    }

    function selectSimulationCase(caseIdx) {
      appState.simulation.selectedCaseIndex = caseIdx;
      saveState();
      renderSimulationView();
    }

    function renderCaseAnalysisOutput() {
      const out = document.getElementById('approachAnalysisOutput');
      if (!out) return;
      const isEn = appState.lang === 'en';
      const { lockedApproach, opt } = getActiveCaseOptionData();

      if (!lockedApproach) {
        out.innerHTML = `
          <div class="flex items-start gap-3">
            <div class="w-10 h-10 rounded-2xl bg-white/15 text-sky-300 flex items-center justify-center text-lg shrink-0">🔒</div>
            <div class="space-y-1">
              <div class="font-extrabold text-xs sm:text-sm text-white">${t('caseLockBannerTitle')}</div>
              <p class="text-xs text-slate-300 leading-relaxed">${t('caseLockBannerDesc')}</p>
            </div>
          </div>
        `;
        return;
      }

      out.innerHTML = `
        <div class="flex flex-wrap items-center justify-between gap-2">
          <span class="px-3 py-1 rounded-full bg-white/15 text-sky-300 font-mono text-xs font-bold">
            🔒 ${isEn ? `Locked: Approach ${lockedApproach}` : `Đã khóa: Hướng ${lockedApproach}`} • ${opt.tag}
          </span>
          <span class="text-xs font-bold text-emerald-300">Best Job Fit: ${opt.bestRole}</span>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-3 text-xs">
          <div class="p-3.5 rounded-2xl bg-white/10 border border-white/10 space-y-1">
            <div class="font-extrabold text-emerald-300">${isEn ? '✓ Identified Strengths' : '✓ Điểm mạnh Phân tích được'}</div>
            <p class="text-slate-200 leading-relaxed">${isEn ? opt.strengthsEn : opt.strengthsVi}</p>
          </div>
          <div class="p-3.5 rounded-2xl bg-white/10 border border-white/10 space-y-1">
            <div class="font-extrabold text-amber-300">${isEn ? '⚠ Weaknesses & Blind Spots' : '⚠ Điểm yếu & Góc khuất cần lưu ý'}</div>
            <p class="text-slate-200 leading-relaxed">${isEn ? opt.weaknessesEn : opt.weaknessesVi}</p>
          </div>
        </div>
        <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 pt-1">
          ${opt.fitScores
            .map(
              f => `
            <div class="p-2.5 rounded-xl bg-white/10 text-center">
              <div class="text-base font-mono font-extrabold text-sky-300">${f.score}%</div>
              <div class="text-[10px] text-slate-300 truncate">${f.role}</div>
            </div>
          `
            )
            .join('')}
        </div>
      `;
    }

    function selectClientApproach(approachKey, silent = false) {
      const isEn = appState.lang === 'en';
      const { industry, caseObj, caseKey, lockedApproach } = getActiveCaseOptionData();

      if (lockedApproach) {
        if (!silent) {
          showToast(
            isEn
              ? `Your choice (Approach ${lockedApproach}) is locked for this scenario and cannot be changed.`
              : `Lựa chọn (Hướng ${lockedApproach}) của bạn cho tình huống này đã được khóa và không thể thay đổi.`
          );
        }
        return;
      }

      if (!appState.simulation.lockedCases) appState.simulation.lockedCases = {};
      appState.simulation.lockedCases[caseKey] = approachKey;
      appState.simulation.selectedApproach = approachKey;

      const wasSimCompleted = Boolean(appState.simulation.completed);
      appState.simulation.completed = true;
      if (!appState.simulation.solvedCaseKeys) appState.simulation.solvedCaseKeys = [];
      if (!appState.simulation.solvedCaseKeys.includes(caseKey)) {
        appState.simulation.solvedCaseKeys.push(caseKey);
        appState.simulation.xp += 50;
      }

      if (appState.community.isMatched) {
        const best = computeBestMentorMatch();
        appState.community.matchedMentorId = best.mentor.id;
        appState.community.matchScore = best.score;
      } else if (!wasSimCompleted && appState.mbti.completed) {
        setTimeout(() => {
          showToast(
            isEn
              ? '🎉 Both MBTI & Simulation completed! Open Cohort & Mentor to unlock your matched Mentor!'
              : '🎉 Đã hoàn thành cả 2 bài đánh giá! Vào tab Cohort & Mentor để ghép Mentor ngay!'
          );
        }, 450);
      }

      saveState();
      renderIndustryCaseSelector();
      renderCaseAnalysisOutput();

      const totalCases = INDUSTRY_CASE_BANK.reduce((sum, ind) => sum + ind.cases.length, 0);
      const solvedCount = Object.keys(appState.simulation.lockedCases).length;
      const counterBadge = document.getElementById('solvedCasesCounterBadge');
      if (counterBadge) counterBadge.textContent = `${solvedCount}/${totalCases} Cases`;
      document.getElementById('simXpBadge').textContent = `${appState.simulation.xp} XP`;

      if (!silent) {
        showToast(
          isEn
            ? `🔒 Locked Approach ${approachKey} (+50 XP) & updated Job Fit!`
            : `🔒 Đã khóa lựa chọn Hướng ${approachKey} (+50 XP) & cập nhật % Job Fit!`
        );
      }
    }

    function togglePersonaComparison() {
      const panel = document.getElementById('personaComparisonPanel');
      if (panel) panel.classList.toggle('hidden');
    }

    function filterMiniTasks(track) {
      currentMiniTaskFilter = track;
      const isEn = appState.lang === 'en';

      const pillActive = 'px-3.5 py-1.5 rounded-full bg-ueh-600 text-white text-xs font-bold shrink-0';
      const pillInactive = 'px-3.5 py-1.5 rounded-full bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-slate-600 dark:text-slate-300 text-xs font-semibold shrink-0';

      document.getElementById('taskFilterAll').className = track === 'all' ? pillActive : pillInactive;
      document.getElementById('taskFilterDesign').className = track === 'design' ? pillActive : pillInactive;
      document.getElementById('taskFilterTech').className = track === 'tech' ? pillActive : pillInactive;

      const list = track === 'all' ? MINI_TASKS : MINI_TASKS.filter(tk => tk.track === track);
      const grid = document.getElementById('miniTasksGrid');
      grid.innerHTML = list
        .map(tk => {
          const isDone = appState.simulation.completedTasks.includes(tk.id);
          return `
          <div class="bg-white dark:bg-slate-900 rounded-3xl overflow-hidden border border-slate-200/80 dark:border-slate-800 shadow-card flex flex-col justify-between">
            <div>
              <div class="h-28 bg-gradient-to-br ${tk.bannerBg} p-4 text-white flex flex-col justify-between">
                <div class="flex items-center justify-between text-[10px] font-bold">
                  <span class="px-2.5 py-0.5 rounded-full bg-black/25">${tk.category}</span>
                  <span class="px-2 py-0.5 rounded-full bg-white/20">${isEn ? tk.durationEn : tk.duration}</span>
                </div>
                <div class="font-mono text-[11px] text-sky-200 font-bold">🏢 ${tk.partner}</div>
              </div>
              <div class="p-4 space-y-2">
                <h3 class="font-extrabold text-sm text-slate-900 dark:text-white leading-snug">${isEn ? tk.titleEn : tk.title}</h3>
                <p class="text-xs text-slate-500 dark:text-slate-400 leading-relaxed">${isEn ? tk.descEn : tk.desc}</p>
              </div>
            </div>
            <div class="px-4 pb-4 space-y-2.5">
              <div class="flex items-center justify-between text-[11px] pt-2 border-t border-slate-100 dark:border-slate-800">
                <span class="text-slate-400">${t('taskRewardLabel')}</span>
                <span class="font-mono font-extrabold text-ueh-600">+${tk.xp} XP &amp; ${tk.badge}</span>
              </div>
              <div class="grid grid-cols-2 gap-2">
                <button type="button" onclick="openTaskModal('${tk.id}')" class="py-2 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-slate-200 text-xs font-bold text-slate-700 dark:text-slate-200">
                  ${t('taskDetailBtn')}
                </button>
                <button type="button" onclick="completeMiniTask('${tk.id}')" class="py-2 rounded-xl ${
                  isDone ? 'bg-emerald-600 text-white' : 'bg-ueh-600 hover:bg-ueh-700 text-white'
                } text-xs font-bold">
                  ${isDone ? t('taskDoneBtn') : t('taskRegisterBtn')}
                </button>
              </div>
            </div>
          </div>
        `;
        })
        .join('');
    }

    function openTaskModal(taskId) {
      const isEn = appState.lang === 'en';
      if (taskId === 'greengo') {
        openModal(
          'ACTIVE SIMULATION',
          isEn ? 'GreenGo Mobility — High-Fidelity Prototype' : 'GreenGo Mobility — Thiết kế Luồng Đặt xe Xanh',
          `
          <div class="space-y-3">
            <p>${
              isEn
                ? 'Complete step 3/4: Design the EV route carbon-savings badge and 1-tap booking confirmation sheet.'
                : 'Hoàn thành nhiệm vụ 3/4: Thiết kế thẻ hiển thị lượng CO2 tiết kiệm và màn hình xác nhận đặt xe điện 1 chạm.'
            }</p>
            <button type="button" onclick="advanceActiveGreenGoStep()" class="w-full py-3 rounded-xl bg-ueh-600 text-white font-bold text-xs">
              ${isEn ? '✓ Submit Milestone (+120 XP)' : '✓ Nộp bài Milestone (+120 XP)'}
            </button>
          </div>
          `
        );
        return;
      }

      const task = MINI_TASKS.find(tk => tk.id === taskId) || MINI_TASKS[0];
      openModal(
        task.category,
        isEn ? task.titleEn : task.title,
        `
        <div class="space-y-3">
          <div class="p-3 rounded-2xl bg-ueh-50 dark:bg-ueh-950/60 text-xs font-semibold text-ueh-700 dark:text-ueh-300">
            🏢 Partner: ${task.partner} • ⏱ ${isEn ? task.durationEn : task.duration} • 🏆 +${task.xp} XP
          </div>
          <p>${isEn ? task.descEn : task.desc}</p>
          <button type="button" onclick="completeMiniTask('${task.id}'); closeModal();" class="w-full py-3 rounded-xl bg-ueh-600 text-white font-bold text-xs">
            ${isEn ? `✓ Complete & Claim +${task.xp} XP` : `✓ Hoàn thành & Nhận +${task.xp} XP`}
          </button>
        </div>
        `
      );
    }

    function advanceActiveGreenGoStep() {
      if (appState.simulation.activeTaskSteps < 4) {
        appState.simulation.activeTaskSteps += 1;
        appState.simulation.xp += 120;
        saveState();
        renderSimulationView();
      }
      closeModal();
      showToast(appState.lang === 'en' ? '+120 XP! GreenGo progress updated.' : '+120 XP! Đã cập nhật tiến độ GreenGo Mobility.');
    }

    function completeMiniTask(taskId) {
      const task = MINI_TASKS.find(tk => tk.id === taskId);
      if (!task) return;
      if (!appState.simulation.completedTasks.includes(taskId)) {
        appState.simulation.completedTasks.push(taskId);
        appState.simulation.xp += task.xp;
        saveState();
        renderSimulationView();
        showToast(
          appState.lang === 'en'
            ? `Completed! Earned +${task.xp} XP & ${task.badge} badge.`
            : `Hoàn thành! Nhận +${task.xp} XP & huy hiệu ${task.badge}.`
        );
      } else {
        showToast(appState.lang === 'en' ? 'You already completed this mini-task!' : 'Bạn đã hoàn thành mini-task này!');
      }
    }

    // =========================================================================
    // 10. SCREEN 6: DYNAMIC MENTOR MATCHING & SMALL COHORT (10-20 STUDENTS)
    // =========================================================================
    let isMatchingInProgress = false;

    function computeBestMentorMatch() {
      const mbtiType = appState.mbti.type || 'ENTP';
      const indId = appState.simulation.selectedIndustry || 'marketing';
      const approach = appState.simulation.selectedApproach || 'A';
      const majorId = appState.student.majorId || 'tech-innov';

      let bestMentor = MENTOR_COHORT_DATABASE[0];
      let bestScore = -1;

      MENTOR_COHORT_DATABASE.forEach(m => {
        let score = 74;
        if (m.preferredMbti.includes(mbtiType)) {
          score += m.preferredMbti[0] === mbtiType ? 9 : 6;
        } else if (m.preferredMbti.some(t => t[1] === mbtiType[1] && t[2] === mbtiType[2])) {
          score += 4;
        }
        if (m.preferredIndustries.includes(indId)) {
          score += m.preferredIndustries[0] === indId ? 9 : 6;
        }
        if (m.preferredApproaches.includes(approach)) {
          score += m.preferredApproaches[0] === approach ? 5 : 3;
        }
        if (m.preferredMajors.includes(majorId)) {
          score += 3;
        }
        score = Math.min(98, score);

        if (score > bestScore) {
          bestScore = score;
          bestMentor = m;
        }
      });

      return { mentor: bestMentor, score: bestScore };
    }

    function getMatchedMentor() {
      return (
        MENTOR_COHORT_DATABASE.find(m => m.id === appState.community.matchedMentorId) ||
        computeBestMentorMatch().mentor
      );
    }

    function triggerMentorMatching(navigateToCommunity = false) {
      if (!appState.mbti.completed || !appState.simulation.completed) {
        showToast(
          appState.lang === 'en'
            ? 'Please complete both MBTI Test and Case Simulation first!'
            : 'Vui lòng hoàn thành đủ cả 2 bài đánh giá (MBTI & Simulation) trước khi ghép Mentor!'
        );
        return;
      }

      isMatchingInProgress = true;
      if (navigateToCommunity) {
        switchTab('community');
      } else {
        renderCommunityView();
      }

      setTimeout(() => {
        const result = computeBestMentorMatch();
        appState.community.isMatched = true;
        appState.community.matchedMentorId = result.mentor.id;
        appState.community.matchScore = result.score;
        isMatchingInProgress = false;
        saveState();

        renderCommunityView();
        renderDashboardMentorSlot();
        showToast(
          appState.lang === 'en'
            ? `Matched with ${result.mentor.name} (${result.score}% Compatibility)!`
            : `Đã ghép thành công với ${result.mentor.name} (${result.score}% Phù hợp)!`
        );
      }, 950);
    }

    function renderCommunityView() {
      const root = document.getElementById('communityDynamicRoot');
      if (!root) return;
      const isEn = appState.lang === 'en';
      const mbtiDone = Boolean(appState.mbti.completed);
      const simDone = Boolean(appState.simulation.completed);
      const bothDone = mbtiDone && simDone;

      // STATE 1: AI Matching Animation in Progress
      if (isMatchingInProgress) {
        root.innerHTML = `
          <div class="max-w-xl mx-auto bg-white dark:bg-slate-900 rounded-3xl p-8 border border-ueh-200 dark:border-ueh-800 shadow-card text-center space-y-4">
            <div class="w-16 h-16 mx-auto rounded-2xl bg-gradient-to-br from-ueh-600 to-indigo-600 text-white flex items-center justify-center text-2xl shadow-blue-glow animate-pulse">
              🤖
            </div>
            <h2 class="text-lg sm:text-xl font-extrabold text-slate-900 dark:text-white">
              ${isEn ? 'AI is Matching Your Ideal Mentor & Cohort...' : 'Hệ thống AI đang phân tích & ghép Mentor phù hợp...'}
            </h2>
            <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 leading-relaxed">
              ${
                isEn
                  ? `Cross-referencing your ${appState.mbti.type} cognitive profile, Simulation behavioral strengths, and UEH CTD career goals...`
                  : `Đang đối chiếu trục tính cách ${appState.mbti.type}, điểm mạnh hành vi từ bài Simulation và mục tiêu nghề nghiệp CTD của bạn...`
              }
            </p>
            <div class="w-full h-2 bg-slate-100 dark:bg-slate-800 rounded-full overflow-hidden">
              <div class="h-full bg-ueh-600 rounded-full animate-pulse" style="width: 85%"></div>
            </div>
          </div>
        `;
        return;
      }

      // STATE 2: Prerequisite Gate OR Ready-to-Match Trigger (Before Mentor is Assigned)
      if (!appState.community.isMatched || !bothDone) {
        const { opt } = getActiveCaseOptionData();
        root.innerHTML = `
          <div class="max-w-3xl mx-auto space-y-5">
            <div class="bg-gradient-to-br from-ueh-600 via-ueh-700 to-indigo-800 rounded-3xl p-6 sm:p-8 text-white shadow-blue-glow space-y-3">
              <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white/15 text-[11px] font-bold">
                ${t('commGateBadge')}
              </span>
              <h1 class="text-xl sm:text-2xl font-extrabold tracking-tight">
                ${t('commGateTitle')}
              </h1>
              <p class="text-xs sm:text-sm text-ueh-100/90 leading-relaxed">
                ${t('commGateDesc')}
              </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <!-- Prerequisite 1: MBTI Test -->
              <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border-2 ${mbtiDone ? 'border-emerald-500/70' : 'border-slate-200 dark:border-slate-800'} shadow-card flex flex-col justify-between space-y-4">
                <div class="space-y-2">
                  <div class="flex items-center justify-between">
                    <span class="w-9 h-9 rounded-xl ${mbtiDone ? 'bg-emerald-100 text-emerald-700' : 'bg-ueh-50 dark:bg-ueh-950 text-ueh-600'} flex items-center justify-center font-extrabold text-sm">
                      ${mbtiDone ? '✓' : '1'}
                    </span>
                    <span class="px-2.5 py-0.5 rounded-full text-[11px] font-bold ${mbtiDone ? 'bg-emerald-50 text-emerald-700' : 'bg-amber-50 text-amber-700'}">
                      ${mbtiDone ? t('commStep1Done') : t('commStep1Todo')}
                    </span>
                  </div>
                  <h2 class="font-extrabold text-base text-slate-900 dark:text-white">${t('commStep1Title')}</h2>
                  <p class="text-xs text-slate-500 dark:text-slate-400">
                    ${
                      mbtiDone
                        ? isEn
                          ? `Result: ${appState.mbti.type} (${appState.mbti.archetype})`
                          : `Kết quả của bạn: ${appState.mbti.type} (${appState.mbti.archetype})`
                        : isEn
                          ? 'Discover your 4 cognitive axes (E/I, N/S, T/F, P/J) and ideal CTD work environment.'
                          : 'Khám phá 4 trục tính cách (E/I, N/S, T/F, P/J) và phong cách làm việc tự nhiên tại CTD.'
                    }
                  </p>
                </div>
                <button type="button" onclick="switchTab('mbti')" class="w-full py-2.5 rounded-xl ${mbtiDone ? 'bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-200' : 'bg-ueh-600 hover:bg-ueh-700 text-white shadow-sm'} text-xs font-bold transition-colors">
                  ${mbtiDone ? (isEn ? 'Review / Retake MBTI' : 'Xem lại / Làm lại MBTI') : t('commStep1Btn')}
                </button>
              </div>

              <!-- Prerequisite 2: Problem-Solving Simulation -->
              <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border-2 ${simDone ? 'border-emerald-500/70' : 'border-slate-200 dark:border-slate-800'} shadow-card flex flex-col justify-between space-y-4">
                <div class="space-y-2">
                  <div class="flex items-center justify-between">
                    <span class="w-9 h-9 rounded-xl ${simDone ? 'bg-emerald-100 text-emerald-700' : 'bg-ueh-50 dark:bg-ueh-950 text-ueh-600'} flex items-center justify-center font-extrabold text-sm">
                      ${simDone ? '✓' : '2'}
                    </span>
                    <span class="px-2.5 py-0.5 rounded-full text-[11px] font-bold ${simDone ? 'bg-emerald-50 text-emerald-700' : 'bg-amber-50 text-amber-700'}">
                      ${simDone ? t('commStep2Done') : t('commStep2Todo')}
                    </span>
                  </div>
                  <h2 class="font-extrabold text-base text-slate-900 dark:text-white">${t('commStep2Title')}</h2>
                  <p class="text-xs text-slate-500 dark:text-slate-400">
                    ${
                      simDone
                        ? isEn
                          ? `Evaluated Approach ${appState.simulation.selectedApproach} (${opt.tag}) • Best fit: ${opt.bestRole}`
                          : `Đã phân tích Hướng ${appState.simulation.selectedApproach} (${opt.tag}) • Hợp nhất: ${opt.bestRole}`
                        : isEn
                          ? 'Solve at least 1 real industry client scenario so AI can identify your behavioral strengths.'
                          : 'Giải ít nhất 1 tình huống khách hàng thực tế để AI đo lường điểm mạnh hành vi của bạn.'
                    }
                  </p>
                </div>
                <button type="button" onclick="switchTab('simulation')" class="w-full py-2.5 rounded-xl ${simDone ? 'bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-200' : 'bg-ueh-600 hover:bg-ueh-700 text-white shadow-sm'} text-xs font-bold transition-colors">
                  ${simDone ? (isEn ? 'Try Another Industry Case' : 'Thử thêm tình huống khác') : t('commStep2Btn')}
                </button>
              </div>
            </div>

            ${
              bothDone
                ? `
                <div class="bg-white dark:bg-slate-900 rounded-3xl p-6 border-2 border-ueh-600 shadow-blue-glow text-center space-y-3">
                  <div class="text-xs font-extrabold uppercase tracking-wider text-emerald-600">
                    ✓ 2/2 ASSESSMENTS VERIFIED • ${appState.mbti.type} × ${opt.tag.toUpperCase()}
                  </div>
                  <button type="button" onclick="triggerMentorMatching(false)" class="w-full sm:w-auto px-6 py-3.5 rounded-2xl bg-gradient-to-r from-ueh-600 to-indigo-600 hover:from-ueh-700 hover:to-indigo-700 text-white font-extrabold text-xs sm:text-sm shadow-blue-glow transition-all">
                    ${t('commReadyMatchBtn')}
                  </button>
                </div>
                `
                : ''
            }
          </div>
        `;
        return;
      }

      // STATE 3: Matched Mentor & Small Cohort (10-20 Students) Hub
      const mentor = getMatchedMentor();
      const matchScore = appState.community.matchScore || 95;
      const reasonTags = isEn ? mentor.reasonTagsEn : mentor.reasonTagsVi;

      const userInitials = appState.student.name
        .split(' ')
        .filter(Boolean)
        .slice(-2)
        .map(w => w[0].toUpperCase())
        .join('') || 'SV';

      const allPeers = [
        {
          name: `${appState.student.name} (${t('peerYouLabel')})`,
          mbti: appState.mbti.type,
          role: computePersonalizedCareers()[0].title,
          initials: userInitials,
          isMe: true
        },
        ...mentor.peers.map(p => ({ ...p, isMe: false }))
      ];
      const connectedList = Array.isArray(appState.community.connectedPeers)
        ? appState.community.connectedPeers
        : [];

      root.innerHTML = `
        <div class="bg-gradient-to-br from-ueh-600 via-ueh-700 to-indigo-800 rounded-3xl p-5 sm:p-7 text-white shadow-blue-glow space-y-4">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white/15 text-[11px] font-bold">
              ● ${isEn ? `Matched Cohort ${mentor.cohortCode} (${mentor.cohortSize} Students)` : `Đã Ghép Nhóm Cộng đồng ${mentor.cohortCode} (${mentor.cohortSize} Sinh viên)`}
            </span>
            <button type="button" onclick="triggerMentorMatching(false)" class="px-3 py-1 rounded-full bg-white/15 hover:bg-white/25 text-[11px] font-bold transition-colors">
              ${t('commRematchBtn')}
            </button>
          </div>
          <h1 class="text-xl sm:text-3xl font-extrabold tracking-tight">
            ${isEn ? mentor.cohortTitleEn : mentor.cohortTitleVi}
          </h1>
          <p class="text-xs sm:text-sm text-ueh-100/90 max-w-3xl leading-relaxed">
            ${t('commDesc')}
          </p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
          <!-- Left 5 Cols: AI-Matched Mentor Card & Peer Directory -->
          <div class="lg:col-span-5 space-y-5">
            <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-4">
              <div class="flex items-center justify-between gap-2">
                <span class="text-xs font-extrabold uppercase tracking-wider text-ueh-600">${t('commMentorHeading')}</span>
                <span class="px-2.5 py-0.5 rounded-full bg-emerald-50 dark:bg-emerald-950 text-emerald-700 dark:text-emerald-300 font-mono text-xs font-extrabold">
                  ✓ ${matchScore}% Match
                </span>
              </div>

              <div class="flex items-center gap-3.5">
                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-ueh-600 to-indigo-700 text-white font-extrabold text-base flex items-center justify-center shrink-0 shadow">
                  ${mentor.initials}
                </div>
                <div>
                  <h2 class="font-extrabold text-base text-slate-900 dark:text-white">${mentor.name}</h2>
                  <div class="text-xs text-ueh-600 font-semibold">${isEn ? mentor.roleEn : mentor.roleVi}</div>
                  <div class="text-[11px] text-slate-400 mt-0.5">${isEn ? mentor.expEn : mentor.expVi}</div>
                </div>
              </div>

              <!-- Why AI Matched You Breakdown -->
              <div class="space-y-1.5">
                <div class="text-[11px] font-bold text-slate-500 dark:text-slate-400">${t('commMatchBreakdownTitle')}</div>
                <div class="flex flex-wrap gap-1.5">
                  ${reasonTags
                    .map(
                      tag =>
                        `<span class="px-2.5 py-1 rounded-lg bg-ueh-50 dark:bg-ueh-950/70 text-ueh-700 dark:text-ueh-300 text-[11px] font-bold">✦ ${tag}</span>`
                    )
                    .join('')}
                </div>
              </div>

              <div class="p-3.5 rounded-2xl bg-ueh-50/90 dark:bg-ueh-950/60 border border-ueh-200/70 dark:border-ueh-800 text-xs space-y-1">
                <div class="font-bold text-ueh-700 dark:text-ueh-300">${t('commMentorAdviceLabel')}</div>
                <p class="text-slate-600 dark:text-slate-300 leading-relaxed italic">
                  "${isEn ? mentor.adviceEn : mentor.adviceVi}"
                </p>
              </div>

              <button type="button" onclick="showToast(t('toastBookMentor'))" class="w-full py-3 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white text-xs font-bold shadow-blue-glow transition-all">
                ${t('commBookMentorBtn')}
              </button>
            </div>

            <!-- Peer Directory (10-20 Students) -->
            <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-3">
              <div class="flex items-center justify-between">
                <h3 class="font-extrabold text-sm text-slate-900 dark:text-white">
                  ${t('commPeersHeading')} ${mentor.cohortCode} (${mentor.cohortSize})
                </h3>
                <span class="px-2 py-0.5 rounded-full bg-emerald-50 dark:bg-emerald-950 text-emerald-700 dark:text-emerald-300 text-[10px] font-bold">${t('commPeersTag')}</span>
              </div>
              <div class="space-y-2">
                ${allPeers
                  .map(p => {
                    const isConnected = connectedList.includes(p.name);
                    return `
                  <div class="p-3 rounded-2xl bg-slate-50 dark:bg-slate-800/70 border border-slate-200/70 dark:border-slate-700 flex items-center justify-between gap-2">
                    <div class="flex items-center gap-2.5 min-w-0">
                      <div class="w-9 h-9 rounded-full bg-gradient-to-br from-ueh-500 to-indigo-600 text-white text-xs font-extrabold flex items-center justify-center shrink-0">${p.initials}</div>
                      <div class="min-w-0">
                        <div class="font-bold text-xs text-slate-900 dark:text-white truncate">${p.name}</div>
                        <div class="text-[10px] text-slate-400 truncate">${p.mbti} • ${p.role}</div>
                      </div>
                    </div>
                    ${
                      p.isMe
                        ? `<span class="px-2 py-0.5 rounded-full bg-ueh-100 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 text-[10px] font-bold">${t('peerYouLabel')}</span>`
                        : isConnected
                          ? `<button type="button" disabled class="px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 border border-slate-300 dark:border-slate-600 text-[11px] font-bold text-slate-500 dark:text-slate-300 cursor-default shrink-0 transition-colors">${t('peerConnectedBtn')}</button>`
                          : `<button type="button" onclick="connectWithPeer('${p.name}')" class="px-2.5 py-1 rounded-lg bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-700 text-[11px] font-bold text-ueh-600 hover:bg-ueh-50 shrink-0 transition-colors">${t('peerConnectBtn')}</button>`
                    }
                  </div>
                `;
                  })
                  .join('')}
              </div>
            </div>
          </div>

          <!-- Right 7 Cols: Mentorship Sessions & Cohort Discussion Feed -->
          <div class="lg:col-span-7 space-y-5">
            <!-- Mentorship Sessions Schedule -->
            <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-3.5">
              <div>
                <h3 class="font-extrabold text-sm sm:text-base text-slate-900 dark:text-white">${t('commSessionsHeading')}</h3>
                <p class="text-[11px] text-slate-400 mt-0.5">${t('commSessionsSub')}</p>
              </div>
              <div class="space-y-3">
                ${mentor.sessions
                  .map(sess => {
                    const joined = (appState.community.rsvpedIds || []).includes(sess.id);
                    return `
                      <div class="p-4 rounded-2xl bg-slate-50 dark:bg-slate-800/70 border border-slate-200/70 dark:border-slate-700 flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                        <div class="space-y-1">
                          <div class="flex flex-wrap items-center gap-2 text-[11px]">
                            <span class="px-2 py-0.5 rounded bg-ueh-100 dark:bg-ueh-950 text-ueh-700 dark:text-ueh-300 font-bold">${sess.type}</span>
                            <span class="font-mono text-slate-500">${isEn ? sess.dateEn : sess.dateVi}</span>
                          </div>
                          <div class="font-extrabold text-xs sm:text-sm text-slate-900 dark:text-white">${isEn ? sess.titleEn : sess.titleVi}</div>
                          <div class="text-[11px] text-emerald-600 font-semibold">👥 ${isEn ? sess.spotsEn : sess.spotsVi}</div>
                        </div>
                        <button type="button" onclick="toggleSessionRsvp('${sess.id}')" class="px-4 py-2 rounded-xl text-xs font-bold shrink-0 transition-colors ${
                          joined
                            ? 'bg-emerald-600 text-white'
                            : 'bg-ueh-600 hover:bg-ueh-700 text-white shadow-sm'
                        }">
                          ${joined ? t('sessionJoinedBtn') : t('sessionJoinBtn')}
                        </button>
                      </div>
                    `;
                  })
                  .join('')}
              </div>
            </div>

            <!-- Group Discussion Feed -->
            <div class="bg-white dark:bg-slate-900 rounded-3xl p-5 border border-slate-200/80 dark:border-slate-800 shadow-card space-y-3.5">
              <h3 class="font-extrabold text-sm sm:text-base text-slate-900 dark:text-white">${t('commFeedHeading')} (${mentor.cohortCode})</h3>
              <form onsubmit="handleCohortPost(event)" class="flex items-center gap-2">
                <input id="cohortPostInput" type="text" placeholder="${t('commFeedPlaceholder')}" class="flex-1 px-3.5 py-2.5 rounded-xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs focus:outline-none focus:ring-2 focus:ring-ueh-500" />
                <button type="submit" class="px-4 py-2.5 rounded-xl bg-ueh-600 hover:bg-ueh-700 text-white text-xs font-bold shrink-0">${t('commPostBtn')}</button>
              </form>
              <div class="space-y-2.5">
                ${appState.community.posts
                  .map(
                    post => `
                    <div class="p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-800/70 space-y-1.5 text-xs">
                      <div class="flex items-center justify-between">
                        <span class="font-extrabold text-slate-900 dark:text-white">${post.author}</span>
                        <span class="text-[10px] text-slate-400">${post.time}</span>
                      </div>
                      <div class="text-[10px] font-semibold text-ueh-600">${post.role}</div>
                      <p class="text-slate-600 dark:text-slate-300 leading-relaxed">${post.content}</p>
                    </div>
                  `
                  )
                  .join('')}
              </div>
            </div>
          </div>
        </div>
      `;
    }

    function toggleSessionRsvp(sessionId) {
      if (!Array.isArray(appState.community.rsvpedIds)) {
        appState.community.rsvpedIds = [];
      }
      const idx = appState.community.rsvpedIds.indexOf(sessionId);
      const isEn = appState.lang === 'en';
      if (idx > -1) {
        appState.community.rsvpedIds.splice(idx, 1);
        showToast(isEn ? 'Cancelled session registration.' : 'Đã hủy đăng ký buổi Mentorship.');
      } else {
        appState.community.rsvpedIds.push(sessionId);
        showToast(
          isEn
            ? 'Registered! Calendar invite sent to your UEH email.'
            : 'Đăng ký thành công! Lịch hẹn đã được gửi tới email UEH của bạn.'
        );
      }
      saveState();
      renderCommunityView();
    }

    function connectWithPeer(peerName) {
      if (!Array.isArray(appState.community.connectedPeers)) {
        appState.community.connectedPeers = [];
      }
      if (!appState.community.connectedPeers.includes(peerName)) {
        appState.community.connectedPeers.push(peerName);
        saveState();
        renderCommunityView();
        showToast(
          appState.lang === 'en'
            ? `Connected with ${peerName}!`
            : `Đã kết nối học tập cùng ${peerName}!`
        );
      }
    }

    function handleCohortPost(event) {
      event.preventDefault();
      const input = document.getElementById('cohortPostInput');
      const text = input.value.trim();
      if (!text) return;

      appState.community.posts.unshift({
        author: appState.student.name,
        role: `${appState.mbti.type} • ${appState.student.cohort} CTD`,
        time: appState.lang === 'en' ? 'Just now' : 'Vừa xong',
        content: text
      });
      input.value = '';
      saveState();
      renderCommunityView();
    }

    // =========================================================================
    // 11. MODAL & TOAST UTILITIES + INITIAL BOOTSTRAP
    // =========================================================================
    function openModal(tag, title, bodyHtml) {
      document.getElementById('modalTag').textContent = tag;
      document.getElementById('modalTitle').textContent = title;
      document.getElementById('modalBody').innerHTML = bodyHtml;
      document.getElementById('universalModal').classList.remove('hidden');
    }

    function closeModal() {
      document.getElementById('universalModal').classList.add('hidden');
    }

    let toastTimeout = null;
    function showToast(msg) {
      const banner = document.getElementById('toastBanner');
      const msgEl = document.getElementById('toastMessage');
      if (!banner || !msgEl) return;

      msgEl.textContent = msg;
      banner.classList.remove('translate-y-24', 'opacity-0', 'pointer-events-none');
      if (toastTimeout) clearTimeout(toastTimeout);
      toastTimeout = setTimeout(() => {
        banner.classList.add('translate-y-24', 'opacity-0', 'pointer-events-none');
      }, 3200);
    }

    window.addEventListener('DOMContentLoaded', () => {
      applyTheme();
      setLanguage(appState.lang || 'vi', true);
      syncAuthUiVisibility();
      if (appState.isLoggedIn) {
        switchTab(appState.activeTab || 'profile');
      }
    });
  </script>
</body>
</html>
