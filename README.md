<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <meta name="theme-color" content="#1e3a8a" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="Shree Shyam Rent" />
  <title>Shree Shyam Rent — श्री श्याम रेंट (सांपला, रोहतक)</title>

  <!-- Tailwind CSS & FontAwesome -->
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" />
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Devanagari:wght@400;500;600;700;800&family=Plus+Jakarta+Sans:wght@500;600;700;800&display=swap" rel="stylesheet" />

  <style>
    body {
      font-family: 'Noto Sans Devanagari', 'Plus Jakarta Sans', sans-serif;
      background-color: #f8fafc;
      color: #0f172a;
      -webkit-tap-highlight-color: transparent;
    }
    .font-en { font-family: 'Plus Jakarta Sans', sans-serif; }
    .no-scrollbar::-webkit-scrollbar { display: none; }
    .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    @keyframes pulseRing {
      0% { transform: scale(0.95); opacity: 0.9; }
      70% { transform: scale(1.1); opacity: 0; }
      100% { transform: scale(0.95); opacity: 0; }
    }
    .badge-pulse::before {
      content: '';
      position: absolute;
      inset: -3px;
      border-radius: 9999px;
      background: #ef4444;
      animation: pulseRing 1.8s infinite;
      z-index: -1;
    }
  </style>
</head>
<body class="min-h-screen flex flex-col">

  <!-- Top Owner Settings Bar -->
  <div class="bg-amber-400 text-slate-950 px-3 py-2 text-xs sm:text-sm font-semibold flex flex-wrap items-center justify-between gap-2 shadow-sm">
    <div class="flex items-center gap-2">
      <i class="fa-solid fa-building-shield text-slate-900"></i>
      <span><strong>Shree Shyam Rent</strong> — सांपला, रोहतक (हरियाणा)</span>
    </div>
    <div class="flex items-center gap-2">
      <button id="installAppBtn" onclick="installPWA()" class="hidden bg-emerald-700 hover:bg-emerald-800 text-white px-3 py-1 rounded-lg text-xs font-bold shadow transition flex items-center gap-1.5">
        <i class="fa-solid fa-download"></i> INSTALL APP
      </button>
      <button onclick="openSettingsModal()" class="bg-slate-900 hover:bg-slate-800 text-white px-3 py-1 rounded-lg text-xs font-bold transition flex items-center gap-1.5">
        <i class="fa-solid fa-gear"></i> नंबर / किराया बदलें
      </button>
    </div>
  </div>

  <!-- Main Sticky Header -->
  <header class="sticky top-0 z-40 bg-white/95 backdrop-blur border-b border-slate-200 shadow-sm">
    <div class="max-w-7xl mx-auto px-4 py-3 flex flex-wrap items-center justify-between gap-3">
      <!-- Brand -->
      <div class="flex items-center gap-3 cursor-pointer" onclick="switchMainView('public')">
        <div class="w-10 h-10 rounded-xl bg-blue-900 text-white flex items-center justify-center font-en font-extrabold text-lg shadow">
          SS
        </div>
        <div>
          <h1 class="font-en font-extrabold text-lg sm:text-xl text-blue-950 leading-tight">SHREE SHYAM RENT</h1>
          <p class="text-xs text-slate-500 font-medium">बेरी मोड़ के पास, सांपला (रोहतक)</p>
        </div>
      </div>

      <!-- View Switcher + Notification Bell -->
      <div class="flex items-center gap-2 sm:gap-3">
        <div class="bg-slate-100 p-1 rounded-xl flex items-center border border-slate-200">
          <button id="tabPublic" onclick="switchMainView('public')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-bold transition bg-blue-900 text-white shadow-sm">
            <i class="fa-solid fa-house-chimney mr-1"></i> प्रॉपर्टी व बुकिंग
          </button>
          <button id="tabOwner" onclick="switchMainView('owner')" class="relative px-3 py-1.5 rounded-lg text-xs sm:text-sm font-bold transition text-slate-700 hover:text-blue-900 flex items-center gap-1.5">
            <i class="fa-solid fa-wallet"></i> पेमेंट ट्रैकर
            <span id="navPendingBadge" class="bg-red-600 text-white text-[10px] font-en font-extrabold px-1.5 py-0.5 rounded-full">0</span>
          </button>
        </div>

        <!-- Bell Icon -->
        <button onclick="switchMainView('owner'); scrollToNotifications()" class="relative w-10 h-10 rounded-xl bg-amber-50 hover:bg-amber-100 border border-amber-200 text-amber-700 flex items-center justify-center transition" title="Messages Notification">
          <i class="fa-solid fa-bell text-base"></i>
          <span id="bellCountBadge" class="badge-pulse absolute -top-1 -right-1 bg-red-600 text-white text-[10px] font-en font-extrabold w-5 h-5 rounded-full flex items-center justify-center">0</span>
        </button>
      </div>
    </div>
  </header>

  <!-- =========================================================
       VIEW 1: PUBLIC PROPERTY & BOOKING SHOWCASE
  ========================================================= -->
  <main id="publicView" class="flex-1">
    <!-- Hero Section -->
    <section class="bg-gradient-to-br from-blue-950 via-blue-900 to-slate-900 text-white py-12 px-4">
      <div class="max-w-6xl mx-auto grid md:grid-cols-2 gap-8 items-center">
        <div>
          <span class="inline-block bg-amber-400/20 border border-amber-400/40 text-amber-300 text-xs font-bold px-3 py-1 rounded-full mb-3">
            <i class="fa-solid fa-location-dot mr-1"></i> प्राइम लोकेशन — सांपला, जिला रोहतक
          </span>
          <h2 class="text-3xl sm:text-4xl font-extrabold leading-snug mb-3">
            किराए के लिए बेहतरीन कमरे एवं कमर्शियल दुकानें
          </h2>
          <p class="text-blue-100 text-sm sm:text-base mb-6 leading-relaxed">
            <strong>Shree Shyam Rent</strong> में विद्यार्थियों, नौकरीपेशा व्यक्तियों और व्यापारियों के लिए स्वच्छ, सुरक्षित व हवादार <strong>10 रेंटल रूम्स (₹4,000/माह)</strong> और मुख्य मार्ग पर <strong>कमर्शियल शॉप्स</strong> उपलब्ध हैं।
          </p>
          <div class="flex flex-wrap gap-3">
            <a href="#listings" class="bg-amber-400 hover:bg-amber-300 text-slate-950 font-extrabold px-5 py-3 rounded-xl text-sm shadow-lg transition">
              <i class="fa-solid fa-magnifying-glass mr-1.5"></i> उपलब्ध रूम व शॉप्स देखें
            </a>
            <button onclick="openDirectWhatsApp('नमस्ते, मुझे Shree Shyam Rent (सांपला) में रूम/दुकान किराए पर लेने की जानकारी चाहिए।')" class="bg-emerald-600 hover:bg-emerald-500 text-white font-bold px-5 py-3 rounded-xl text-sm shadow-lg transition flex items-center gap-2">
              <i class="fa-brands fa-whatsapp text-lg"></i> सीधे WhatsApp करें
            </button>
          </div>
        </div>

        <!-- Live Availability Summary Card -->
        <div class="bg-white/10 backdrop-blur-md border border-white/20 rounded-2xl p-6 shadow-xl">
          <h3 class="font-bold text-amber-300 text-sm uppercase tracking-wider mb-4">लाइव उपलब्धता (Live Status)</h3>
          <div class="grid grid-cols-2 gap-4 mb-5">
            <div class="bg-white/10 rounded-xl p-4 border border-white/10">
              <p class="text-xs text-blue-200">रेंटल रूम्स (₹<span class="dispRoomRent">4,000</span>/माह)</p>
              <p id="publicVacantRooms" class="font-en text-2xl sm:text-3xl font-extrabold text-white mt-1">--</p>
              <p class="text-[11px] text-emerald-300 mt-1">बिजली, पानी व पार्किंग सुविधा</p>
            </div>
            <div class="bg-white/10 rounded-xl p-4 border border-white/10">
              <p class="text-xs text-blue-200">कमर्शियल शॉप्स (₹<span class="dispShopRent">8,000</span>/माह)</p>
              <p id="publicVacantShops" class="font-en text-2xl sm:text-3xl font-extrabold text-white mt-1">--</p>
              <p class="text-[11px] text-amber-300 mt-1">मेन रोड फ्रंट, शटर सहित</p>
            </div>
          </div>
          <div class="text-xs text-blue-100 flex items-center justify-between border-t border-white/15 pt-3">
            <span><i class="fa-solid fa-phone text-amber-400 mr-1"></i> संपर्क: <strong class="dispPhone font-en">+91 98120 00000</strong></span>
            <span class="dispAddress">बेरी मोड़ के पास, सांपला</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Filter & Listings -->
    <section id="listings" class="max-w-6xl mx-auto px-4 py-10">
      <div class="flex flex-wrap items-center justify-between gap-4 mb-6">
        <div>
          <h3 class="text-2xl font-extrabold text-slate-900">उपलब्ध यूनिट्स (Rooms & Shops)</h3>
          <p class="text-sm text-slate-500">अपनी आवश्यकता अनुसार रूम या दुकान चुनें और सीधे बुक करें</p>
        </div>
        <div class="flex bg-white p-1 rounded-xl border border-slate-200 shadow-sm">
          <button onclick="filterPublicCards('all', this)" class="pub-filter-btn px-4 py-2 rounded-lg text-xs font-bold bg-blue-900 text-white">सभी (All)</button>
          <button onclick="filterPublicCards('room', this)" class="pub-filter-btn px-4 py-2 rounded-lg text-xs font-bold text-slate-600 hover:text-blue-900">रेंटल रूम्स</button>
          <button onclick="filterPublicCards('shop', this)" class="pub-filter-btn px-4 py-2 rounded-lg text-xs font-bold text-slate-600 hover:text-blue-900">कमर्शियल शॉप्स</button>
        </div>
      </div>

      <div id="publicUnitsGrid" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-5">
        <!-- Rendered by JS -->
      </div>
    </section>

    <!-- WhatsApp Inquiry Form -->
    <section class="bg-slate-100 border-t border-slate-200 py-10 px-4">
      <div class="max-w-3xl mx-auto bg-white rounded-2xl shadow-md border border-slate-200 p-6 sm:p-8">
        <h3 class="text-xl sm:text-2xl font-extrabold text-blue-950 mb-1">रूम या शॉप बुकिंग के लिए संदेश भेजें</h3>
        <p class="text-sm text-slate-500 mb-6">नीचे विवरण भरें—आपका संदेश सीधे मालिक के WhatsApp पर खुल जाएगा।</p>
        <form onsubmit="submitPublicInquiry(event)" class="grid sm:grid-cols-2 gap-4">
          <div>
            <label class="block text-xs font-bold text-slate-700 mb-1">आपका पूरा नाम *</label>
            <input type="text" id="inqName" required placeholder="जैसे: राहुल शर्मा" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:outline-none focus:border-blue-800" />
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-700 mb-1">मोबाइल नंबर *</label>
            <input type="tel" id="inqPhone" required placeholder="10 अंकों का मोबाइल नंबर" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:outline-none focus:border-blue-800" />
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-700 mb-1">क्या किराए पर चाहिए? *</label>
            <select id="inqType" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:outline-none focus:border-blue-800">
              <option value="Rental Room (₹4,000/माह)">Rental Room (आवासीय कमरा)</option>
              <option value="Commercial Shop (दुकान)">Commercial Shop (दुकान)</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-700 mb-1">कब से शिफ्ट होना है?</label>
            <input type="date" id="inqDate" class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 text-sm focus:outline-none focus:border-blue-800" />
          </div>
          <div class="sm:col-span-2">
            <button type="submit" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold py-3 rounded-xl text-sm shadow transition flex items-center justify-center gap-2">
              <i class="fa-brands fa-whatsapp text-lg"></i> WHATSAPP पर बुकिंग संदेश भेजें
            </button>
          </div>
        </form>
      </div>
    </section>
  </main>

  <!-- =========================================================
       VIEW 2: OWNER PAYMENT, REMINDER & DUE TO ADD DASHBOARD
  ========================================================= -->
  <main id="ownerView" class="hidden flex-1 max-w-7xl w-full mx-auto px-4 py-6 space-y-6">

    <!-- Top Control Bar: Month Selector & Quick Actions -->
    <div class="bg-white rounded-2xl border border-slate-200 p-4 shadow-sm flex flex-wrap items-center justify-between gap-4">
      <div class="flex flex-wrap items-center gap-3">
        <div>
          <label class="block text-[11px] font-en font-extrabold uppercase tracking-wider text-slate-500">SELECT MONTH (महीना चुनें)</label>
          <select id="monthSelector" onchange="changeMonth()" class="mt-1 bg-blue-50 border border-blue-200 text-blue-950 font-bold text-sm rounded-xl px-3.5 py-2 focus:outline-none">
            <option value="2026-10">अक्टूबर 2026 (October 2026)</option>
            <option value="2026-11" selected>नवंबर 2026 (November 2026)</option>
            <option value="2026-12">दिसंबर 2026 (December 2026)</option>
            <option value="2027-01">जनवरी 2027 (January 2027)</option>
            <option value="2027-02">फ़रवरी 2027 (February 2027)</option>
          </select>
        </div>

        <div>
          <label class="block text-[11px] font-en font-extrabold uppercase tracking-wider text-slate-500">MONTHLY DUE DATE</label>
          <select id="dueDaySelector" onchange="saveDueDay()" class="mt-1 bg-slate-50 border border-slate-200 text-slate-800 font-bold text-sm rounded-xl px-3 py-2 focus:outline-none">
            <option value="5">हर महीने की 5 तारीख</option>
            <option value="7">हर महीने की 7 तारीख</option>
            <option value="10" selected>हर महीने की 10 तारीख</option>
            <option value="15">हर महीने की 15 तारीख</option>
          </select>
        </div>
      </div>

      <div class="flex flex-wrap items-center gap-2">
        <button onclick="copyPreviousMonthData()" class="bg-slate-100 hover:bg-slate-200 text-slate-800 font-bold text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 transition flex items-center gap-1.5">
          <i class="fa-solid fa-copy"></i> पिछले महीने के किरायेदार कॉपी करें
        </button>
        <button onclick="openAddUnitModal()" class="bg-blue-900 hover:bg-blue-800 text-white font-bold text-xs px-3.5 py-2.5 rounded-xl shadow transition flex items-center gap-1.5">
          <i class="fa-solid fa-plus"></i> नया रूम / शॉप जोड़ें
        </button>
      </div>
    </div>

    <!-- =========================================================
         5 ORDERED SUMMARY CARDS (EXACT SEQUENCE REQUESTED)
         1. PAYMENT DEPOSIT
         2. PENDING PAYMENT
         3. MESSAGES NOTIFICATION
         4. REMINDER
         5. DUE TO ADD
    ========================================================= -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4">
      
      <!-- 1. PAYMENT DEPOSIT -->
      <div class="bg-white rounded-2xl border-2 border-emerald-500 p-4 shadow-sm flex flex-col justify-between">
        <div class="flex items-center justify-between">
          <span class="font-en text-xs font-extrabold tracking-wider text-emerald-700 uppercase">1. PAYMENT DEPOSIT</span>
          <span class="w-8 h-8 rounded-lg bg-emerald-100 text-emerald-700 flex items-center justify-center">
            <i class="fa-solid fa-circle-check"></i>
          </span>
        </div>
        <div class="my-3">
          <p id="cardDepositAmount" class="font-en text-2xl font-extrabold text-emerald-700">₹0</p>
          <p id="cardDepositSub" class="text-xs text-slate-500 mt-0.5">0 यूनिट्स जमा (Paid)</p>
        </div>
        <div class="text-[11px] font-semibold text-emerald-800 bg-emerald-50 px-2.5 py-1 rounded-lg">
          कुल प्राप्त किराया व शुल्क
        </div>
      </div>

      <!-- 2. PENDING PAYMENT -->
      <div class="bg-white rounded-2xl border-2 border-red-500 p-4 shadow-sm flex flex-col justify-between">
        <div class="flex items-center justify-between">
          <span class="font-en text-xs font-extrabold tracking-wider text-red-700 uppercase">2. PENDING PAYMENT</span>
          <span class="w-8 h-8 rounded-lg bg-red-100 text-red-700 flex items-center justify-center">
            <i class="fa-solid fa-clock"></i>
          </span>
        </div>
        <div class="my-3">
          <p id="cardPendingAmount" class="font-en text-2xl font-extrabold text-red-600">₹0</p>
          <p id="cardPendingSub" class="text-xs text-slate-500 mt-0.5">0 यूनिट्स बकाया (Pending)</p>
        </div>
        <div class="text-[11px] font-semibold text-red-800 bg-red-50 px-2.5 py-1 rounded-lg">
          कुल बकाया वसूली शेष
        </div>
      </div>

      <!-- 3. MESSAGES NOTIFICATION -->
      <div onclick="scrollToNotifications()" class="cursor-pointer bg-white rounded-2xl border-2 border-amber-500 p-4 shadow-sm hover:shadow-md transition flex flex-col justify-between">
        <div class="flex items-center justify-between">
          <span class="font-en text-xs font-extrabold tracking-wider text-amber-700 uppercase">3. MESSAGES NOTIFICATION</span>
          <span class="w-8 h-8 rounded-lg bg-amber-100 text-amber-700 flex items-center justify-center">
            <i class="fa-solid fa-bell"></i>
          </span>
        </div>
        <div class="my-3">
          <p id="cardNotifCount" class="font-en text-2xl font-extrabold text-amber-700">0 ALERTS</p>
          <p class="text-xs text-slate-500 mt-0.5">व्हाट्सएप व SMS रिमाइंडर अलर्ट</p>
        </div>
        <div class="text-[11px] font-bold text-amber-900 bg-amber-100/80 px-2.5 py-1 rounded-lg flex items-center justify-between">
          <span>अलर्ट लिस्ट देखें</span>
          <i class="fa-solid fa-arrow-down"></i>
        </div>
      </div>

      <!-- 4. REMINDER -->
      <div onclick="scrollToReminders()" class="cursor-pointer bg-white rounded-2xl border-2 border-indigo-500 p-4 shadow-sm hover:shadow-md transition flex flex-col justify-between">
        <div class="flex items-center justify-between">
          <span class="font-en text-xs font-extrabold tracking-wider text-indigo-700 uppercase">4. REMINDER</span>
          <span class="w-8 h-8 rounded-lg bg-indigo-100 text-indigo-700 flex items-center justify-center">
            <i class="fa-solid fa-calendar-check"></i>
          </span>
        </div>
        <div class="my-3">
          <p id="cardReminderCount" class="font-en text-2xl font-extrabold text-indigo-700">0 ACTIVE</p>
          <p id="cardReminderSub" class="text-xs text-slate-500 mt-0.5">ड्यू डेट व कस्टम रिमाइंडर</p>
        </div>
        <button onclick="event.stopPropagation(); openAddReminderModal()" class="w-full text-[11px] font-en font-extrabold text-white bg-indigo-600 hover:bg-indigo-700 px-2.5 py-1 rounded-lg transition">
          + ADD REMINDER
        </button>
      </div>

      <!-- 5. DUE TO ADD -->
      <div class="bg-white rounded-2xl border-2 border-purple-600 p-4 shadow-sm flex flex-col justify-between">
        <div class="flex items-center justify-between">
          <span class="font-en text-xs font-extrabold tracking-wider text-purple-700 uppercase">5. DUE TO ADD</span>
          <span class="w-8 h-8 rounded-lg bg-purple-100 text-purple-700 flex items-center justify-center">
            <i class="fa-solid fa-file-invoice-dollar"></i>
          </span>
        </div>
        <div class="my-3">
          <p id="cardDueToAddAmount" class="font-en text-2xl font-extrabold text-purple-700">₹0</p>
          <p id="cardDueToAddSub" class="text-xs text-slate-500 mt-0.5">बिजली / पानी / लेट फ़ीस आदि</p>
        </div>
        <button onclick="openDueToAddModal()" class="w-full text-[11px] font-en font-extrabold text-white bg-purple-600 hover:bg-purple-700 px-2.5 py-1 rounded-lg transition">
          + DUE TO ADD
        </button>
      </div>

    </div>

    <!-- =========================================================
         RENT & PAYMENT L
