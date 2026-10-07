<!DOCTYPE html>
<html lang="zh-TW" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>情感樹洞 - 溫暖傾訴與線上寵物陪伴</title>

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- FontAwesome Icons CDN -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Google Fonts: Inter & Noto Serif TC -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Noto+Serif+TC:wght@400;600;700&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            amberwarm: {
              50: '#fffbf5',
              100: '#fef5e7',
              200: '#fde5c8',
              300: '#fbcfa2',
              400: '#f7ad71',
              500: '#f38944',
              600: '#e36829',
              700: '#bc4d1e',
              800: '#963f1e',
              900: '#79361c',
              950: '#41190c',
            },
            cream: {
              100: '#fdfbf7',
              200: '#f8f3eb',
              300: '#f0e6d8',
              400: '#e4d2bc',
            },
            softbrown: {
              800: '#3d2b24',
              900: '#2a1d18',
            }
          },
          fontFamily: {
            serif: ['"Noto Serif TC"', 'serif'],
            sans: ['Inter', 'sans-serif'],
          },
          animation: {
            'float-slow': 'float 5s ease-in-out infinite',
            'bounce-soft': 'bounceSoft 2s infinite',
            'pulse-glow': 'pulseGlow 3s ease-in-out infinite alternate',
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0px)' },
              '50%': { transform: 'translateY(-8px)' },
            },
            bounceSoft: {
              '0%, 100%': { transform: 'translateY(0)' },
              '50%': { transform: 'translateY(-6px)' },
            },
            pulseGlow: {
              '0%': { boxShadow: '0 0 15px rgba(247, 173, 113, 0.2)' },
              '100%': { boxShadow: '0 0 30px rgba(243, 137, 68, 0.4)' },
            }
          }
        }
      }
    }
  </script>

  <style>
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #fef5e7;
    }
    ::-webkit-scrollbar-thumb {
      background: #f7ad71;
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #f38944;
    }

    /* Soft Warm Sunset Ambient Background */
    .bg-warm-ambient {
      background-color: #fffbf5;
      background-image: 
        radial-gradient(circle at 10% 20%, rgba(254, 229, 200, 0.6) 0%, transparent 40%),
        radial-gradient(circle at 90% 80%, rgba(251, 207, 162, 0.4) 0%, transparent 45%),
        radial-gradient(circle at 50% 50%, rgba(255, 251, 245, 1) 0%, transparent 100%);
      background-attachment: fixed;
    }

    .glass-warm-card {
      background: rgba(255, 251, 245, 0.85);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(247, 173, 113, 0.25);
    }

    .glass-warm-hover {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .glass-warm-hover:hover {
      transform: translateY(-4px);
      border-color: rgba(243, 137, 68, 0.5);
      box-shadow: 0 16px 32px -8px rgba(188, 77, 30, 0.12), 0 0 20px rgba(247, 173, 113, 0.2);
    }
  </style>
</head>

<body class="bg-warm-ambient text-softbrown-800 font-sans min-h-screen flex flex-col justify-between selection:bg-amberwarm-300 selection:text-amberwarm-950">

  <header class="sticky top-0 z-40 bg-amberwarm-50/90 backdrop-blur-md border-b border-amberwarm-200/80 shadow-sm">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
      <!-- Brand Logo -->
      <a href="#" class="flex items-center gap-3 group">
        <div class="w-10 h-10 rounded-2xl bg-gradient-to-br from-amberwarm-400 to-amberwarm-600 flex items-center justify-center shadow-lg shadow-amberwarm-500/20 group-hover:scale-105 transition-transform">
          <i class="fa-solid fa-tree text-white text-xl"></i>
        </div>
        <div>
          <span class="font-serif text-xl font-bold tracking-wide bg-gradient-to-r from-amberwarm-800 via-amberwarm-700 to-amberwarm-600 bg-clip-text text-transparent">情感樹洞</span>
          <span class="hidden sm:inline-block text-xs text-amberwarm-700/80 ml-2 font-normal">｜陪伴與聽見的暖心角落</span>
        </div>
      </a>

      <!-- Ambient Music, Pet Adoption & Post Controls -->
      <div class="flex items-center gap-2 sm:gap-3">
        <!-- Open Pet Adoption Dialog -->
        <button onclick="openPetAdoptionModal()" class="flex items-center gap-1.5 px-3 py-1.5 rounded-full bg-amberwarm-100 border border-amberwarm-300/80 text-xs text-amberwarm-900 hover:bg-amberwarm-200 transition-all font-medium">
          <i class="fa-solid fa-paw text-amberwarm-600 animate-bounce"></i>
          <span>領養線上寵物</span>
        </button>

        <!-- Sound Control Dropdown -->
        <div class="relative" id="soundControlMenu">
          <button onclick="toggleSoundMenu()" class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-amberwarm-100/80 border border-amberwarm-300/80 text-xs text-amberwarm-900 hover:bg-amberwarm-200 transition-all">
            <i class="fa-solid fa-volume-low text-amberwarm-600" id="soundIcon"></i>
            <span id="soundLabel" class="hidden md:inline">療癒音效</span>
            <i class="fa-solid fa-chevron-down text-[10px] opacity-60"></i>
          </button>

          <div id="soundDropdown" class="hidden absolute right-0 mt-2 w-48 bg-amberwarm-50 border border-amberwarm-200 rounded-2xl shadow-xl p-3 z-50 text-xs space-y-1.5 glass-warm-card">
            <div class="text-amberwarm-800 font-medium px-2 py-1 border-b border-amberwarm-200/60 flex justify-between items-center">
              <span>背景音效 (Web Audio)</span>
            </div>
            <button onclick="playAmbientSound('none')" class="w-full text-left px-2 py-1.5 rounded-lg hover:bg-amberwarm-100 flex items-center gap-2 text-amberwarm-900">
              <i class="fa-solid fa-volume-xmark w-4 text-center"></i> 靜音模式
            </button>
            <button onclick="playAmbientSound('rain')" class="w-full text-left px-2 py-1.5 rounded-lg hover:bg-amberwarm-100 flex items-center gap-2 text-amberwarm-900">
              <i class="fa-solid fa-cloud-rain w-4 text-center text-blue-500"></i> 窗外細雨聲
            </button>
            <button onclick="playAmbientSound('wind')" class="w-full text-left px-2 py-1.5 rounded-lg hover:bg-amberwarm-100 flex items-center gap-2 text-amberwarm-900">
              <i class="fa-solid fa-wind w-4 text-center text-teal-600"></i> 靜謐森林風聲
            </button>
            <button onclick="playAmbientSound('fire')" class="w-full text-left px-2 py-1.5 rounded-lg hover:bg-amberwarm-100 flex items-center gap-2 text-amberwarm-900">
              <i class="fa-solid fa-fire w-4 text-center text-amberwarm-600"></i> 溫暖篝火微響
            </button>
          </div>
        </div>

        <!-- Create Story Post Button -->
        <button onclick="openPostModal()" class="flex items-center gap-1.5 px-4 py-1.5 rounded-full bg-gradient-to-r from-amberwarm-400 to-amberwarm-600 text-white font-medium text-xs sm:text-sm hover:brightness-105 shadow-md shadow-amberwarm-500/20 transition-all transform active:scale-95">
          <i class="fa-solid fa-pen-nib"></i>
          <span>發表故事</span>
        </button>
      </div>
    </div>
  </header>

  <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-10 flex-grow w-full">

    <!-- 1. Daily Inspirational Quote Section -->
    <section class="glass-warm-card rounded-3xl p-6 sm:p-8 relative overflow-hidden border border-amberwarm-300/60 shadow-lg bg-gradient-to-r from-amberwarm-100/90 via-cream-100/80 to-amberwarm-100/90">
      <div class="absolute -top-12 -right-12 w-48 h-48 bg-amberwarm-300/20 rounded-full blur-3xl pointer-events-none"></div>
      <div class="flex flex-col md:flex-row items-center justify-between gap-6 relative z-10">
        <div class="space-y-3 text-center md:text-left flex-1">
          <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amberwarm-200/60 border border-amberwarm-300 text-amberwarm-800 text-xs font-medium">
            <i class="fa-solid fa-sun text-amberwarm-600"></i> 每日勵志金句
          </div>
          <blockquote id="dailyQuoteText" class="font-serif text-lg sm:text-xl md:text-2xl text-amberwarm-950 leading-relaxed font-semibold italic">
            "萬物皆有裂痕，那是光照進來的地方。"
          </blockquote>
          <p id="dailyQuoteAuthor" class="text-xs sm:text-sm text-amberwarm-700 font-medium tracking-wider">
            —— 萊昂納德·科恩 (Leonard Cohen)
          </p>
        </div>
        <button onclick="refreshQuote()" class="shrink-0 flex items-center gap-2 px-4 py-2.5 rounded-2xl bg-amberwarm-50 border border-amberwarm-300 text-amberwarm-800 text-xs sm:text-sm hover:bg-amberwarm-200 transition-all hover:rotate-180 duration-500 shadow-sm">
          <i class="fa-solid fa-arrows-rotate text-amberwarm-600"></i>
          <span class="hidden sm:inline">換一句名言</span>
        </button>
      </div>
    </section>

    <!-- 2. Daily Featured Hero Motivational Story -->
    <section class="space-y-4">
      <div class="flex items-center justify-between">
        <div class="flex items-center gap-3">
          <div class="w-2.5 h-7 bg-amberwarm-500 rounded-full"></div>
          <h2 class="font-serif text-xl sm:text-2xl font-bold text-amberwarm-950">今日主題勵志人物</h2>
        </div>
        <span class="text-xs text-amberwarm-700/80">每日更新 Daily Hero</span>
      </div>

      <div id="featuredStoryContainer" class="glass-warm-card rounded-3xl p-6 sm:p-8 border border-amberwarm-300/80 relative overflow-hidden bg-gradient-to-br from-cream-100 via-amberwarm-50 to-cream-200 shadow-xl">
        <!-- Rendered dynamically by JS -->
      </div>
    </section>

    <!-- 3. Tree Hole & Daily Stories Feed -->
    <section class="space-y-6">
      <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 border-b border-amberwarm-200/80 pb-4">
        <div class="flex items-center gap-3">
          <div class="w-2.5 h-7 bg-amberwarm-600 rounded-full"></div>
          <h2 class="font-serif text-xl sm:text-2xl font-bold text-amberwarm-950">小故事樹洞牆</h2>
        </div>

        <!-- Category & Search Filters -->
        <div class="flex flex-wrap items-center gap-2">
          <!-- Search Input -->
          <div class="relative flex-grow sm:w-48">
            <input type="text" id="searchInput" oninput="filterStories()" placeholder="搜尋故事與關鍵字..." class="w-full pl-8 pr-3 py-1.5 rounded-xl bg-amberwarm-50 border border-amberwarm-300 text-xs text-amberwarm-950 placeholder-amberwarm-400 focus:outline-none focus:border-amberwarm-500 transition-colors shadow-sm">
            <i class="fa-solid fa-magnifying-glass absolute left-2.5 top-2.5 text-xs text-amberwarm-400"></i>
          </div>

          <!-- Category Pills -->
          <div class="flex items-center gap-1 overflow-x-auto py-1 max-w-full" id="categoryFilterContainer">
            <button onclick="selectCategory('all')" data-cat="all" class="cat-btn active text-xs px-3 py-1.5 rounded-xl bg-amberwarm-500 text-white font-medium transition-all shrink-0 shadow-sm">全部</button>
            <button onclick="selectCategory('日常點滴')" data-cat="日常點滴" class="cat-btn text-xs px-3 py-1.5 rounded-xl bg-amberwarm-100/80 text-amberwarm-800 hover:bg-amberwarm-200 border border-amberwarm-200 transition-all shrink-0">日常點滴</button>
            <button onclick="selectCategory('勵志成長')" data-cat="勵志成長" class="cat-btn text-xs px-3 py-1.5 rounded-xl bg-amberwarm-100/80 text-amberwarm-800 hover:bg-amberwarm-200 border border-amberwarm-200 transition-all shrink-0">勵志成長</button>
            <button onclick="selectCategory('情感傾訴')" data-cat="情感傾訴" class="cat-btn text-xs px-3 py-1.5 rounded-xl bg-amberwarm-100/80 text-amberwarm-800 hover:bg-amberwarm-200 border border-amberwarm-200 transition-all shrink-0">情感傾訴</button>
            <button onclick="selectCategory('職場生活')" data-cat="職場生活" class="cat-btn text-xs px-3 py-1.5 rounded-xl bg-amberwarm-100/80 text-amberwarm-800 hover:bg-amberwarm-200 border border-amberwarm-200 transition-all shrink-0">職場生活</button>
            <button onclick="selectCategory('溫馨療癒')" data-cat="溫馨療癒" class="cat-btn text-xs px-3 py-1.5 rounded-xl bg-amberwarm-100/80 text-amberwarm-800 hover:bg-amberwarm-200 border border-amberwarm-200 transition-all shrink-0">溫馨療癒</button>
          </div>
        </div>
      </div>

      <!-- Stories Grid -->
      <div id="storiesGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Rendered dynamically by JS -->
      </div>
    </section>

  </main>

  <footer class="border-t border-amberwarm-200/80 bg-amberwarm-100/60 py-8 text-center text-xs text-amberwarm-700/80 mt-12">
    <div class="max-w-6xl mx-auto px-4 space-y-2">
      <div class="flex items-center justify-center gap-2 font-medium">
        <i class="fa-solid fa-heart text-amberwarm-500"></i>
        <span>情感樹洞 ‧ 溫暖陪伴每一個獨立的靈魂</span>
      </div>
      <p>© 2026 Warm Corner. 讓每一次表達都被溫柔以待。</p>
    </div>
  </footer>

  <div id="petFloatingWidget" class="fixed bottom-5 right-5 z-40 flex flex-col items-end gap-2 pointer-events-auto">
    <!-- Dialogue Bubble -->
    <div id="petSpeechBubble" class="glass-warm-card bg-amberwarm-50 border border-amberwarm-300/80 p-3 rounded-2xl shadow-xl max-w-xs text-xs text-amberwarm-950 transition-all duration-300 opacity-100 transform translate-y-0 relative">
      <div class="flex items-center justify-between gap-2 border-b border-amberwarm-200/60 pb-1 mb-1">
        <span id="petWidgetName" class="font-bold text-amberwarm-700">柴犬 ‧ 小橘</span>
        <span id="petWidgetType" class="text-[10px] px-2 py-0.5 rounded-full bg-amberwarm-200 text-amberwarm-800">陸地</span>
      </div>
      <p id="petWidgetDialogue" class="leading-relaxed font-medium">汪！今天過得好嗎？記得多喝水、照顧好自己喔！</p>
      <!-- Tiny triangle pointing down -->
      <div class="w-3 h-3 bg-amberwarm-50 border-r border-b border-amberwarm-300/80 transform rotate-45 absolute -bottom-1.5 right-6"></div>
    </div>

    <!-- Pet Avatar Character Frame & Action Panel -->
    <div class="flex items-center gap-2">
      <!-- Pet Interactive Action Panel -->
      <div class="glass-warm-card bg-amberwarm-50/90 rounded-full p-1.5 border border-amberwarm-300/80 shadow-md flex items-center gap-1.5 text-xs">
        <button onclick="interactWithPet('feed')" title="餵食" class="w-7 h-7 rounded-full bg-amberwarm-100 hover:bg-amberwarm-200 text-amberwarm-700 flex items-center justify-center transition-transform hover:scale-110">
          <i class="fa-solid fa-cookie-bite"></i>
        </button>
        <button onclick="interactWithPet('pat')" title="撫摸" class="w-7 h-7 rounded-full bg-amberwarm-100 hover:bg-amberwarm-200 text-amberwarm-700 flex items-center justify-center transition-transform hover:scale-110">
          <i class="fa-solid fa-hand-holding-heart"></i>
        </button>
        <button onclick="interactWithPet('talk')" title="說話" class="w-7 h-7 rounded-full bg-amberwarm-100 hover:bg-amberwarm-200 text-amberwarm-700 flex items-center justify-center transition-transform hover:scale-110">
          <i class="fa-solid fa-comment-dots"></i>
        </button>
      </div>

      <!-- Main Animated Pet Icon Trigger -->
      <button onclick="openPetAdoptionModal()" title="更換寵物/檢視狀態" class="w-16 h-16 rounded-full bg-gradient-to-tr from-amberwarm-300 via-amberwarm-200 to-white border-2 border-amberwarm-400 p-1 shadow-2xl hover:scale-105 transition-all relative group flex items-center justify-center animate-bounce-soft">
        <span id="petWidgetEmoji" class="text-3xl select-none">🐕</span>
        <span class="absolute -top-1 -right-1 w-4 h-4 bg-emerald-500 border-2 border-white rounded-full"></span>
      </button>
    </div>
  </div>

  <div id="petModal" class="fixed inset-0 bg-amberwarm-950/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
    <div class="glass-warm-card bg-amberwarm-50 border border-amberwarm-300 rounded-3xl max-w-2xl w-full p-6 space-y-5 shadow-2xl relative max-h-[90vh] overflow-y-auto">
      <button onclick="closePetAdoptionModal()" class="absolute top-5 right-5 text-amberwarm-600 hover:text-amberwarm-900 text-lg">
        <i class="fa-solid fa-xmark"></i>
      </button>

      <div class="space-y-1">
        <h3 class="font-serif text-xl font-bold text-amberwarm-950 flex items-center gap-2">
          <i class="fa-solid fa-paw text-amberwarm-500"></i> 水陸海空 ‧ 線上寵物夥伴選擇
        </h3>
        <p class="text-xs text-amberwarm-700">選擇一隻屬於你的療癒寵物，隨時在右下角陪伴你、聽你說話。</p>
      </div>

      <!-- Habitat Category Switcher Tabs -->
      <div class="flex items-center gap-2 border-b border-amberwarm-200 pb-2">
        <button onclick="switchPetTab('land')" id="tab-land" class="pet-tab-btn active px-3.5 py-1.5 rounded-xl bg-amberwarm-500 text-white text-xs font-semibold">🐾 陸地 (Land)</button>
        <button onclick="switchPetTab('ocean')" id="tab-ocean" class="pet-tab-btn px-3.5 py-1.5 rounded-xl bg-amberwarm-100 text-amberwarm-800 text-xs font-semibold">🌊 海洋 (Ocean)</button>
        <button onclick="switchPetTab('water')" id="tab-water" class="pet-tab-btn px-3.5 py-1.5 rounded-xl bg-amberwarm-100 text-amberwarm-800 text-xs font-semibold">🦦 水陸兩棲 (Water)</button>
        <button onclick="switchPetTab('sky')" id="tab-sky" class="pet-tab-btn px-3.5 py-1.5 rounded-xl bg-amberwarm-100 text-amberwarm-800 text-xs font-semibold">🕊️ 天空 (Sky)</button>
      </div>

      <!-- Pets Selection Grid -->
      <div id="petSelectionGrid" class="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <!-- Rendered dynamically by JS -->
      </div>
    </div>
  </div>

  <div id="postModal" class="fixed inset-0 bg-amberwarm-950/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
    <div class="glass-warm-card bg-amberwarm-50 border border-amberwarm-300 rounded-3xl max-w-lg w-full p-6 space-y-4 shadow-2xl relative">
      <button onclick="closePostModal()" class="absolute top-5 right-5 text-amberwarm-600 hover:text-amberwarm-900 text-lg">
        <i class="fa-solid fa-xmark"></i>
      </button>

      <div class="space-y-1">
        <h3 class="font-serif text-xl font-bold text-amberwarm-950 flex items-center gap-2">
          <i class="fa-solid fa-feather-pointed text-amberwarm-500"></i> 寫下你的心靈故事
        </h3>
        <p class="text-xs text-amberwarm-700">在這個溫暖樹洞裡，你的喜怒哀樂都將被溫柔擁抱。</p>
      </div>

      <form id="postForm" onsubmit="handlePostSubmit(event)" class="space-y-3">
        <div>
          <label class="block text-xs font-medium text-amberwarm-900 mb-1">主角暱稱 / 稱呼</label>
          <input type="text" id="postAuthor" required placeholder="例如: 尋光的旅人、小琥珀..." class="w-full px-3 py-2 rounded-xl bg-white border border-amberwarm-300 text-sm text-amberwarm-950 focus:outline-none focus:border-amberwarm-500">
        </div>

        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-medium text-amberwarm-900 mb-1">故事分類</label>
            <select id="postCategory" class="w-full px-3 py-2 rounded-xl bg-white border border-amberwarm-300 text-sm text-amberwarm-950 focus:outline-none focus:border-amberwarm-500">
              <option value="日常點滴">日常點滴</option>
              <option value="勵志成長">勵志成長</option>
              <option value="情感傾訴">情感傾訴</option>
              <option value="職場生活">職場生活</option>
              <option value="溫馨療癒">溫馨療癒</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-medium text-amberwarm-900 mb-1">個人的勵志短句</label>
            <input type="text" id="postMotto" placeholder="一句給自己的鼓勵" class="w-full px-3 py-2 rounded-xl bg-white border border-amberwarm-300 text-sm text-amberwarm-950 focus:outline-none focus:border-amberwarm-500">
          </div>
        </div>

        <div>
          <label class="block text-xs font-medium text-amberwarm-900 mb-1">故事標題</label>
          <input type="text" id="postTitle" required placeholder="給這個小故事起個名字" class="w-full px-3 py-2 rounded-xl bg-white border border-amberwarm-300 text-sm text-amberwarm-950 focus:outline-none focus:border-amberwarm-500">
        </div>

        <div>
          <label class="block text-xs font-medium text-amberwarm-900 mb-1">故事內容</label>
          <textarea id="postContent" rows="4" required placeholder="寫下今天發生的事、你的感悟或心中的悄悄話..." class="w-full px-3 py-2 rounded-xl bg-white border border-amberwarm-300 text-sm text-amberwarm-950 focus:outline-none focus:border-amberwarm-500 resize-none"></textarea>
        </div>

        <div class="flex items-center justify-between pt-1 border-t border-amberwarm-200">
          <label class="flex items-center gap-2 text-xs text-amberwarm-800 cursor-pointer">
            <input type="checkbox" id="allowChatCheckbox" checked class="rounded border-amberwarm-300 text-amberwarm-600 focus:ring-0">
            <span>開放他人透過小故事發起線上聊天</span>
          </label>
        </div>

        <div class="flex justify-end gap-3 pt-2">
          <button type="button" onclick="closePostModal()" class="px-4 py-2 rounded-xl bg-amberwarm-100 text-amberwarm-800 text-xs hover:bg-amberwarm-200">取消</button>
          <button type="submit" class="px-5 py-2 rounded-xl bg-gradient-to-r from-amberwarm-400 to-amberwarm-600 text-white font-semibold text-xs hover:brightness-105 shadow-md shadow-amberwarm-500/20">發布故事</button>
        </div>
      </form>
    </div>
  </div>

  <div id="chatModal" class="fixed inset-0 bg-amberwarm-950/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-2 sm:p-4">
    <div class="glass-warm-card bg-amberwarm-50 border border-amberwarm-300 rounded-3xl w-full max-w-2xl h-[85vh] max-h-[680px] flex flex-col overflow-hidden shadow-2xl relative">
      
      <!-- Chat Header -->
      <div class="p-4 bg-amberwarm-100/90 border-b border-amberwarm-200 flex items-center justify-between shrink-0">
        <div class="flex items-center gap-3">
          <div class="relative">
            <img id="chatPartnerAvatar" src="" alt="Avatar" class="w-11 h-11 rounded-full object-cover border-2 border-amberwarm-400">
            <span class="w-3 h-3 bg-emerald-500 rounded-full absolute bottom-0 right-0 border-2 border-white"></span>
          </div>
          <div>
            <div class="flex items-center gap-2">
              <h4 id="chatPartnerName" class="font-bold text-amberwarm-950 text-sm">--</h4>
              <span class="px-2 py-0.5 rounded-md bg-amberwarm-200 text-amberwarm-800 text-[10px]" id="chatCategoryTag">日常</span>
            </div>
            <p id="chatPartnerMotto" class="text-xs text-amberwarm-700 truncate max-w-[220px] sm:max-w-xs">--</p>
          </div>
        </div>

        <button onclick="closeChatModal()" class="w-9 h-9 rounded-full bg-amberwarm-200 hover:bg-amberwarm-300 text-amberwarm-800 flex items-center justify-center transition-colors">
          <i class="fa-solid fa-xmark text-base"></i>
        </button>
      </div>

      <!-- Story Title Context Banner -->
      <div class="px-4 py-2 bg-cream-200 border-b border-amberwarm-200 text-xs flex items-center justify-between gap-2 shrink-0">
        <div class="flex items-center gap-2 text-amberwarm-900 truncate">
          <i class="fa-solid fa-book-open text-amberwarm-600"></i>
          <span class="text-amberwarm-600 font-medium">衍生小故事：</span>
          <span id="chatStoryTitle" class="font-medium truncate">--</span>
        </div>
        <span class="text-[10px] text-emerald-700 bg-emerald-100 px-2 py-0.5 rounded border border-emerald-300 shrink-0">線上交流中</span>
      </div>

      <!-- Chat Messages Scroll Container -->
      <div id="chatMessagesContainer" class="flex-grow p-4 overflow-y-auto space-y-4 text-xs sm:text-sm bg-cream-100/50">
        <!-- Messages appended dynamically -->
      </div>

      <!-- Quick Greetings Bar -->
      <div class="px-4 py-2 bg-amberwarm-100/60 border-t border-amberwarm-200 flex items-center gap-2 overflow-x-auto shrink-0">
        <span class="text-[11px] text-amberwarm-700 shrink-0"><i class="fa-solid fa-wand-magic-sparkles"></i> 快選招呼:</span>
        <button onclick="sendQuickGreeting('看了你的故事深受感觸！想向你請教...')" class="shrink-0 px-2.5 py-1 rounded-full bg-white hover:bg-amberwarm-200 text-amberwarm-800 text-[11px] border border-amberwarm-300 transition-colors">✨ 看了你的故事深受感觸</button>
        <button onclick="sendQuickGreeting('嗨！我也曾經歷過類似的事，很高興認識你！')" class="shrink-0 px-2.5 py-1 rounded-full bg-white hover:bg-amberwarm-200 text-amberwarm-800 text-[11px] border border-amberwarm-300 transition-colors">🤝 我也有類似經歷</button>
        <button onclick="sendQuickGreeting('今天過得還好嗎？祝你有美好的一天！')" class="shrink-0 px-2.5 py-1 rounded-full bg-white hover:bg-amberwarm-200 text-amberwarm-800 text-[11px] border border-amberwarm-300 transition-colors">🌸 祝你有美好一天</button>
      </div>

      <!-- Input Field -->
      <div class="p-3 sm:p-4 bg-amberwarm-50 border-t border-amberwarm-200 shrink-0">
        <form onsubmit="handleSendMessage(event)" class="flex items-center gap-2">
          <input type="text" id="chatInput" required placeholder="輸入訊息... (按下 Enter 發送)" class="flex-grow px-4 py-2.5 rounded-2xl bg-white border border-amberwarm-300 text-xs sm:text-sm text-amberwarm-950 placeholder-amberwarm-400 focus:outline-none focus:border-amberwarm-500">
          <button type="submit" class="px-4 py-2.5 rounded-2xl bg-gradient-to-r from-amberwarm-400 to-amberwarm-600 text-white font-bold text-xs sm:text-sm hover:brightness-105 shadow-md shadow-amberwarm-500/20 transition-all flex items-center gap-1.5 shrink-0">
            <span>發送</span>
            <i class="fa-solid fa-paper-plane"></i>
          </button>
        </form>
      </div>

    </div>
  </div>

  <script>

    // Daily Quotes Dataset
    const INSPIRATIONAL_QUOTES = [
      { text: "萬物皆有裂痕，那是光照進來的地方。", author: "萊昂納德·科恩 (Leonard Cohen)" },
      { text: "生活不可能像你想像得那麼好，但也不會像你想像得那麼糟。", author: "莫泊桑 (Guy de Maupassant)" },
      { text: "黑夜無論怎樣悠長，白晝總會到來。", author: "莎士比亞 (William Shakespeare)" },
      { text: "星光不問趕路人，歲月不負有心人。", author: "樹洞暖心感悟" },
      { text: "在最深的黑暗裡，我們往往能看清內心最璀璨的光芒。", author: "卡爾·榮格 (Carl Jung)" },
      { text: "每一個不曾起舞的日子，都是對生命的辜負。", author: "尼采 (Friedrich Nietzsche)" }
    ];

    // Daily Featured Hero Story
    const FEATURED_STORY = {
      id: 'featured-1',
      author: '林晨 (Chen)',
      avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=150&auto=format&fit=crop&q=80',
      tagline: '「從聽障程式員到獨立遊戲開發者，我用程式碼寫下心中的旋律。」',
      category: '勵志成長',
      title: '在寂靜無聲的世界裡，點亮屬於自己的星光',
      summary: '12歲那年的一場高燒，奪走了我的聽力。世界變成了無聲的默劇，但我沒有放棄與世界的連接。我靠著自學程式語言，經歷無數次退稿與失敗，耗時四年獨立開發了一款音效視覺化遊戲，獲得了國際獨立遊戲大獎。我想告訴每個困頓中的人：上天關了一扇門，你自己就是打開窗戶的力量。',
      quote: '命運可以剝奪我的聲音，但無法阻止我奏響生命的樂章。',
      repliesCount: 42,
      likes: 328,
      hugs: 189,
      allowChat: true,
      chatGreeting: '你好！我是林晨。謝謝你來讀我的故事，如果你也在經歷困難，我很樂意陪你聊聊！'
    };

    // Tree Hole Feed Seed Data
    let storiesData = [
      {
        id: 'story-101',
        author: '雨後星空',
        avatar: 'https://images.unsplash.com/photo-1517841905240-472988babdf9?w=150&auto=format&fit=crop&q=80',
        motto: '溫柔地對待這個世界，世界也會回饋你溫暖。',
        category: '日常點滴',
        title: '深夜下班路上，路燈下那碗熱氣騰騰的麵',
        content: '今天加班到深夜11點，拖著疲憊的身體走在冷冽的街頭。走到轉角那家老夫妻開的麵攤，阿姨看到我，二話不說多加了一顆滷蛋，笑著說：「孩子，今天辛苦了，多吃點熱的。」那一瞬間，眼眶忍不住濕潤了。生活雖然不易，但這些微小的善意總能治癒一切。',
        time: '2小時前',
        likes: 45,
        hugs: 28,
        allowChat: true,
        comments: [
          { author: '小橘貓', text: '真的！人間煙火氣，最撫凡人心！加油～' },
          { author: '深夜旅人', text: '祝你明天又是美好順利的一天！' }
        ]
      },
      {
        id: 'story-102',
        author: '追風的陸克',
        avatar: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=150&auto=format&fit=crop&q=80',
        motto: '失敗只是通往成功的一條彎路。',
        category: '勵志成長',
        title: '第三次考研終於成功上岸！寫給曾經想放棄的自己',
        content: '收到錄取通知書的那一刻，我一個人坐在房間裡哭了很久。過去這兩年，身邊的朋友陸續工作、升職，只有我還在日復一日地啃著厚厚的考研資料。無數個懷疑自己的夜晚，都是靠著樹洞裡大家寫下的勵志名言熬過來的。如果你也在堅持某件事，請再給自己一次機會！',
        time: '5小時前',
        likes: 112,
        hugs: 86,
        allowChat: true,
        comments: [
          { author: '星光不滅', text: '太棒了！恭喜你！苦盡甘來！' }
        ]
      },
      {
        id: 'story-103',
        author: '微風拂過',
        avatar: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=150&auto=format&fit=crop&q=80',
        motto: '學會與不安相處，也是一種成長。',
        category: '情感傾訴',
        title: '關於30歲前的迷茫與自我和解',
        content: '即將跨入30歲的大門，突然發現自己並沒有成為小時候想像中那個無所不能的大人。沒有買房，感情也經歷了長跑後的離散。但今天坐在公園長椅上看著落葉，突然釋懷了。每個人都有自己的花期，我不必跟著別人的時鐘奔跑。',
        time: '昨天 21:30',
        likes: 89,
        hugs: 64,
        allowChat: true,
        comments: []
      },
      {
        id: 'story-104',
        author: '抹茶拿鐵無糖',
        avatar: 'https://images.unsplash.com/photo-1524504388940-b1c1722653e1?w=150&auto=format&fit=crop&q=80',
        motto: '做個有溫度的人。',
        category: '溫馨療癒',
        title: '流浪貓媽媽帶著小貓來我家陽台避雨了',
        content: '今天午後突降大雨，聽到陽台有弱弱的喵喵聲。打開門發現是平時經常餵食的流浪三花貓，帶著兩隻剛出生不久的小貓蜷縮在乾爽的角落。我立刻拿了毛巾和貓糧給牠們。看著牠們安心吃東西的樣子，感覺整天工作帶來的煩悶瞬間煙消雲散了！',
        time: '2天前',
        likes: 156,
        hugs: 95,
        allowChat: true,
        comments: [
          { author: '貓咪保護協會', text: '謝謝你的善良！希望小貓們健康長大！' }
        ]
      }
    ];

    const PETS_DATABASE = {
      land: [
        { id: 'shiba', name: '柴犬 ‧ 小橘', emoji: '🐕', desc: '熱情忠誠，最喜歡搖尾巴問候你。', type: '陸地 (Land)', quotes: ['汪！今天過得好嗎？記得多喝水喔！', '不管發生什麼，我都在這裡陪著你！', '伸個懶腰～今天也是充滿勇氣的一天！'] },
        { id: 'cat', name: '暖橘貓 ‧ 蜜糖', emoji: '🐱', desc: '慵懶療癒，會發出呼嚕呼嚕聲陪伴你。', type: '陸地 (Land)', quotes: ['喵～過來讓我蹭蹭你，把煩惱都蹭掉！', '累的話就睡個午覺吧，喵～', '你今天表現得超級棒！獎勵你摸摸我！'] },
        { id: 'alpaca', name: '羊駝 ‧ 棉花糖', emoji: '🦙', desc: '蓬鬆治癒，隨時準備給你一個大擁抱。', type: '陸地 (Land)', quotes: ['嚼嚼... 嚼嚼... 送你一顆軟綿綿的棉花糖！', '別焦慮，慢慢來比較快～', '你的笑容就像太陽一樣溫暖！'] }
      ],
      ocean: [
        { id: 'jellyfish', name: '夢幻水母 ‧ 泡泡', emoji: '🪼', desc: '悠遊自在，隨波逐流帶走心靈壓迫感。', type: '海洋 (Ocean)', quotes: ['咕嚕嚕... 讓心靈像大海一樣平靜吧～', '放鬆呼吸，感受當下的平穩。', '漂浮在柔軟的海洋裡，一切都很平安。'] },
        { id: 'dolphin', name: '微笑海豚 ‧ 嘟嘟', emoji: '🐬', desc: '聰明活潑，傳遞海洋中的快樂能量。', type: '海洋 (Ocean)', quotes: ['嗶嗶～跳個躍出海面的優雅舞蹈給你加油！', '相信自己，你擁有一整片大海的勇氣！', '今天也要保持甜甜的微笑喔！'] },
        { id: 'whale', name: '小鯨魚 ‧ 藍藍', emoji: '🐳', desc: '寬廣溫和，噴出彩虹水花為你祝福。', type: '海洋 (Ocean)', quotes: ['呼～噴出彩虹水花！願你今天心情美美！', '深海裡有無盡的包容，你的心事我都聽到了。', '慢慢游，總會抵達溫暖的港灣。'] }
      ],
      water: [
        { id: 'otter', name: '萌萌水獺 ‧ 珍珠', emoji: '🦦', desc: '手牽手漂浮，最喜歡收藏閃亮的小石頭。', type: '水陸兩棲 (Water)', quotes: ['手牽手就不會飄走喔！我們是最好的夥伴！', '送你這顆我最喜歡的圓圓小石頭！', '水裡好涼爽，快來跟我一起划水～'] },
        { id: 'turtle', name: '幸運小烏龜 ‧ 龜龜', emoji: '🐢', desc: '穩重堅定，一步一腳印地邁向美好未來。', type: '水陸兩棲 (Water)', quotes: ['不用急，一步一腳印，我們終會到達目標！', '遇到風雨就縮進暖暖的殼裡休息一下吧～', '長久的陪伴是最長情的告白。'] }
      ],
      sky: [
        { id: 'owl', name: '暖暖貓頭鷹 ‧ 咕咕', emoji: '🦉', desc: '睿智沉靜，夜裡默默守護你的星光。', type: '天空 (Sky)', quotes: ['咕咕～深夜裡如果睡不著，我就在這裡守護你。', '智慧屬於懂得傾聽內心的人。', '今夜星光璀璨，願你有個香甜的好夢。'] },
        { id: 'bird', name: '粉彩文鳥 ‧ 櫻花', emoji: '🐦', desc: '清脆歌唱，為你的日常生活唱響悅耳樂章。', type: '天空 (Sky)', quotes: ['啾啾！今天又是充滿新希望的一天！', '聽我為你唱一首歡快的小曲吧！', '飛上藍天，俯瞰世界其實很大很大～'] },
        { id: 'sugarglider', name: '小飛鼠 ‧ 飛飛', emoji: '🐿️', desc: '滑翔飛躍，靈動可愛地停在你肩膀上。', type: '天空 (Sky)', quotes: ['咻～滑翔落地！滑進你的心房裡！', '藏在口袋裡的堅果分你一半！', '勇敢跨出一小步，就能飛得更高！'] }
      ]
    };

    // Current Selected Pet State
    let currentAdoptedPet = PETS_DATABASE.land[0];
    let currentPetTab = 'land';

    window.onload = function() {
      renderFeaturedStory();
      renderStoriesGrid(storiesData);
      renderPetSelectionGrid('land');
      updatePetWidgetUI();

      // Auto periodic dialogue from Pet every 20s
      setInterval(() => {
        triggerPetAutoDialogue();
      }, 20000);
    };

    function refreshQuote() {
      const randomIndex = Math.floor(Math.random() * INSPIRATIONAL_QUOTES.length);
      const q = INSPIRATIONAL_QUOTES[randomIndex];
      const qText = document.getElementById('dailyQuoteText');
      const qAuthor = document.getElementById('dailyQuoteAuthor');

      qText.classList.add('opacity-0');
      qAuthor.classList.add('opacity-0');

      setTimeout(() => {
        qText.textContent = `"${q.text}"`;
        qAuthor.textContent = `—— ${q.author}`;
        qText.classList.remove('opacity-0');
        qAuthor.classList.remove('opacity-0');
      }, 200);
    }

    function renderFeaturedStory() {
      const container = document.getElementById('featuredStoryContainer');
      const story = FEATURED_STORY;

      container.innerHTML = `
        <div class="flex flex-col lg:flex-row items-start lg:items-center justify-between gap-8">
          <div class="space-y-4 flex-1">
            <div class="flex items-center gap-3">
              <img src="${story.avatar}" alt="${story.author}" class="w-14 h-14 rounded-full object-cover border-2 border-amberwarm-400 shadow-md">
              <div>
                <h3 class="font-bold text-amberwarm-950 text-lg sm:text-xl flex items-center gap-2">
                  ${story.author}
                  <span class="text-xs font-normal px-2.5 py-0.5 rounded-full bg-amberwarm-200 text-amberwarm-800 border border-amberwarm-300">今日精選主角</span>
                </h3>
                <p class="text-xs text-amberwarm-700 italic font-serif">${story.tagline}</p>
              </div>
            </div>

            <div class="space-y-2">
              <h4 class="font-serif text-lg sm:text-xl font-bold text-amberwarm-900">${story.title}</h4>
              <p class="text-xs sm:text-sm text-amberwarm-800/90 leading-relaxed">${story.summary}</p>
            </div>

            <div class="p-3 rounded-2xl bg-amberwarm-100/80 border border-amberwarm-200 text-xs text-amberwarm-800 flex items-center gap-2">
              <i class="fa-solid fa-quote-left text-amberwarm-500"></i>
              <span>${story.quote}</span>
            </div>
          </div>

          <div class="w-full lg:w-auto flex lg:flex-col justify-between items-center gap-4 pt-4 lg:pt-0 border-t lg:border-t-0 lg:border-l border-amberwarm-200/80 lg:pl-8">
            <div class="flex items-center gap-4 text-xs text-amberwarm-700">
              <span class="flex items-center gap-1.5"><i class="fa-solid fa-star text-amberwarm-500"></i> ${story.likes}</span>
              <span class="flex items-center gap-1.5"><i class="fa-solid fa-heart text-rose-400"></i> ${story.hugs}</span>
            </div>

            <button onclick="openChatWith('${story.id}', '${story.author}', '${story.avatar}', '${story.quote}', '${story.title}', '${story.category}', '${story.chatGreeting}')" class="w-full sm:w-auto px-6 py-3 rounded-2xl bg-gradient-to-r from-amberwarm-400 via-amberwarm-500 to-amberwarm-600 text-white font-bold text-xs sm:text-sm hover:brightness-105 shadow-lg shadow-amberwarm-500/25 transition-all flex items-center justify-center gap-2 transform active:scale-95">
              <i class="fa-solid fa-comments text-base"></i>
              <span>與他/她線上聊天</span>
            </button>
          </div>
        </div>
      `;
    }

    function renderStoriesGrid(stories) {
      const container = document.getElementById('storiesGrid');
      
      if (stories.length === 0) {
        container.innerHTML = `
          <div class="col-span-full py-12 text-center text-amberwarm-600 space-y-3">
            <i class="fa-solid fa-wind text-3xl"></i>
            <p>樹洞裡暫時沒有找到相關的小故事...</p>
          </div>
        `;
        return;
      }

      container.innerHTML = stories.map(story => `
        <div class="glass-warm-card glass-warm-hover rounded-3xl p-6 flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2.5">
                <img src="${story.avatar}" alt="${story.author}" class="w-9 h-9 rounded-full object-cover border border-amberwarm-300">
                <div>
                  <h4 class="font-bold text-amberwarm-950 text-xs sm:text-sm">${story.author}</h4>
                  <span class="text-[10px] text-amberwarm-600">${story.time}</span>
                </div>
              </div>
              <span class="px-2.5 py-1 rounded-full bg-amberwarm-100 text-amberwarm-800 text-[10px] border border-amberwarm-200/80">${story.category}</span>
            </div>

            <div class="space-y-1.5">
              <h3 class="font-serif font-bold text-amberwarm-950 text-base hover:text-amberwarm-600 transition-colors">${story.title}</h3>
              <p class="text-xs text-amberwarm-800/90 leading-relaxed line-clamp-4">${story.content}</p>
            </div>
          </div>

          <div class="pt-3 border-t border-amberwarm-200/80 space-y-3">
            <div class="flex items-center justify-between text-xs text-amberwarm-700">
              <div class="flex items-center gap-3">
                <button onclick="toggleLike('${story.id}')" class="flex items-center gap-1 hover:text-amberwarm-600 transition-colors">
                  <i class="fa-solid fa-star text-amberwarm-500"></i>
                  <span>${story.likes}</span>
                </button>
                <button onclick="toggleHug('${story.id}')" class="flex items-center gap-1 hover:text-rose-500 transition-colors">
                  <i class="fa-solid fa-heart text-rose-400"></i>
                  <span>${story.hugs}</span>
                </button>
              </div>

              ${story.allowChat ? `
                <button onclick="openChatWith('${story.id}', '${story.author}', '${story.avatar}', '${story.motto || ''}', '${story.title}', '${story.category}', '你好！很高興收到你的訊息，謝謝你閱讀我的故事！')" class="px-3 py-1 rounded-xl bg-amberwarm-100 hover:bg-amberwarm-200 text-amberwarm-800 border border-amberwarm-300 text-[11px] font-medium transition-all flex items-center gap-1">
                  <i class="fa-regular fa-comment-dots"></i>
                  <span>聊聊</span>
                </button>
              ` : ''}
            </div>

            <div class="space-y-2">
              <button onclick="toggleComments('${story.id}')" class="text-[11px] text-amberwarm-700 hover:text-amberwarm-900 flex items-center gap-1">
                <i class="fa-solid fa-message"></i> 留言回應 (${story.comments ? story.comments.length : 0})
              </button>

              <div id="commentsBox-${story.id}" class="hidden space-y-2 pt-2 border-t border-amberwarm-200">
                <div class="space-y-1.5 max-h-32 overflow-y-auto pr-1">
                  ${(story.comments || []).map(c => `
                    <div class="bg-amberwarm-100/70 p-2 rounded-xl text-[11px]">
                      <span class="font-semibold text-amberwarm-900">${c.author}:</span>
                      <span class="text-amberwarm-800 ml-1">${c.text}</span>
                    </div>
                  `).join('')}
                </div>
                <div class="flex items-center gap-1.5 pt-1">
                  <input type="text" id="commentInput-${story.id}" placeholder="發送溫馨留言..." class="flex-grow px-2.5 py-1 rounded-lg bg-white border border-amberwarm-300 text-[11px] text-amberwarm-950 focus:outline-none focus:border-amberwarm-500">
                  <button onclick="addComment('${story.id}')" class="px-2.5 py-1 rounded-lg bg-amberwarm-200 text-amberwarm-800 text-[11px] hover:bg-amberwarm-300">傳送</button>
                </div>
              </div>
            </div>

          </div>
        </div>
      `).join('');
    }

    let currentCategory = 'all';

    function selectCategory(cat) {
      currentCategory = cat;
      document.querySelectorAll('.cat-btn').forEach(btn => {
        if (btn.getAttribute('data-cat') === cat) {
          btn.className = 'cat-btn active text-xs px-3 py-1.5 rounded-xl bg-amberwarm-500 text-white font-medium transition-all shrink-0 shadow-sm';
        } else {
          btn.className = 'cat-btn text-xs px-3 py-1.5 rounded-xl bg-amberwarm-100/80 text-amberwarm-800 hover:bg-amberwarm-200 border border-amberwarm-200 transition-all shrink-0';
        }
      });
      filterStories();
    }

    function filterStories() {
      const keyword = document.getElementById('searchInput').value.toLowerCase().trim();
      const filtered = storiesData.filter(s => {
        const matchesCategory = (currentCategory === 'all') || (s.category === currentCategory);
        const matchesKeyword = s.title.toLowerCase().includes(keyword) || 
                               s.content.toLowerCase().includes(keyword) || 
                               s.author.toLowerCase().includes(keyword);
        return matchesCategory && matchesKeyword;
      });
      renderStoriesGrid(filtered);
    }

    function toggleLike(id) {
      const story = storiesData.find(s => s.id === id);
      if (story) { story.likes += 1; filterStories(); }
    }

    function toggleHug(id) {
      const story = storiesData.find(s => s.id === id);
      if (story) { story.hugs += 1; filterStories(); }
    }

    function toggleComments(id) {
      const box = document.getElementById(`commentsBox-${id}`);
      if (box) box.classList.toggle('hidden');
    }

    function addComment(id) {
      const input = document.getElementById(`commentInput-${id}`);
      if (!input || !input.value.trim()) return;
      const story = storiesData.find(s => s.id === id);
      if (story) {
        if (!story.comments) story.comments = [];
        story.comments.push({ author: '溫暖樹友', text: input.value.trim() });
        input.value = '';
        filterStories();
        setTimeout(() => {
          const box = document.getElementById(`commentsBox-${id}`);
          if (box) box.classList.remove('hidden');
        }, 50);
      }
    }

    function openPetAdoptionModal() {
      document.getElementById('petModal').classList.remove('hidden');
    }

    function closePetAdoptionModal() {
      document.getElementById('petModal').classList.add('hidden');
    }

    function switchPetTab(tab) {
      currentPetTab = tab;
      document.querySelectorAll('.pet-tab-btn').forEach(btn => {
        btn.className = 'pet-tab-btn px-3.5 py-1.5 rounded-xl bg-amberwarm-100 text-amberwarm-800 text-xs font-semibold';
      });
      const activeBtn = document.getElementById(`tab-${tab}`);
      if (activeBtn) {
        activeBtn.className = 'pet-tab-btn active px-3.5 py-1.5 rounded-xl bg-amberwarm-500 text-white text-xs font-semibold shadow-sm';
      }
      renderPetSelectionGrid(tab);
    }

    function renderPetSelectionGrid(tabKey) {
      const grid = document.getElementById('petSelectionGrid');
      const petList = PETS_DATABASE[tabKey] || [];

      grid.innerHTML = petList.map(p => `
        <div onclick="adoptPet('${p.id}')" class="p-4 rounded-2xl bg-white border border-amberwarm-200 hover:border-amberwarm-400 hover:shadow-lg transition-all cursor-pointer text-center space-y-2 group">
          <div class="text-4xl group-hover:scale-110 transition-transform duration-300 select-none">${p.emoji}</div>
          <h4 class="font-bold text-amberwarm-950 text-sm">${p.name}</h4>
          <p class="text-[11px] text-amberwarm-700 leading-tight">${p.desc}</p>
          <button class="w-full py-1.5 rounded-xl bg-amberwarm-100 group-hover:bg-amberwarm-500 group-hover:text-white text-amberwarm-800 text-xs font-medium transition-colors">
            ${currentAdoptedPet.id === p.id ? '陪伴中 ❤️' : '選擇領養'}
          </button>
        </div>
      `).join('');
    }

    function adoptPet(petId) {
      let found = null;
      Object.keys(PETS_DATABASE).forEach(k => {
        const item = PETS_DATABASE[k].find(p => p.id === petId);
        if (item) found = item;
      });

      if (found) {
        currentAdoptedPet = found;
        updatePetWidgetUI();
        closePetAdoptionModal();
        showPetDialogue(`${currentAdoptedPet.name} 來到你的身邊了！從現在開始陪伴你～`);
      }
    }

    function updatePetWidgetUI() {
      document.getElementById('petWidgetName').textContent = currentAdoptedPet.name;
      document.getElementById('petWidgetType').textContent = currentAdoptedPet.type;
      document.getElementById('petWidgetEmoji').textContent = currentAdoptedPet.emoji;
      
      const randomQuote = currentAdoptedPet.quotes[Math.floor(Math.random() * currentAdoptedPet.quotes.length)];
      document.getElementById('petWidgetDialogue').textContent = randomQuote;
    }

    function triggerPetAutoDialogue() {
      const quotes = currentAdoptedPet.quotes;
      const q = quotes[Math.floor(Math.random() * quotes.length)];
      showPetDialogue(q);
    }

    function showPetDialogue(msg) {
      const bubble = document.getElementById('petSpeechBubble');
      const text = document.getElementById('petWidgetDialogue');
      
      text.textContent = msg;
      bubble.classList.remove('opacity-0', 'translate-y-2');
      bubble.classList.add('opacity-100', 'translate-y-0');
    }

    function interactWithPet(action) {
      if (action === 'feed') {
        showPetDialogue(`好吃！感謝你的美味愛心大餐，${currentAdoptedPet.name} 感到滿滿的幸福！❤️`);
      } else if (action === 'pat') {
        showPetDialogue(`（開心蹭蹭）摸摸好舒服喔！你是世界上最溫柔的人～ ✨`);
      } else if (action === 'talk') {
        const randomQuote = currentAdoptedPet.quotes[Math.floor(Math.random() * currentAdoptedPet.quotes.length)];
        showPetDialogue(randomQuote);
      }
    }

    function openPostModal() { document.getElementById('postModal').classList.remove('hidden'); }
    function closePostModal() { document.getElementById('postModal').classList.add('hidden'); }

    function handlePostSubmit(e) {
      e.preventDefault();
      const author = document.getElementById('postAuthor').value.trim();
      const category = document.getElementById('postCategory').value;
      const motto = document.getElementById('postMotto').value.trim();
      const title = document.getElementById('postTitle').value.trim();
      const content = document.getElementById('postContent').value.trim();
      const allowChat = document.getElementById('allowChatCheckbox').checked;

      const newStory = {
        id: 'story-' + Date.now(),
        author: author || '匿名樹友',
        avatar: 'https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=150&auto=format&fit=crop&q=80',
        motto: motto || '生命的美好在於分享與傾聽。',
        category: category,
        title: title,
        content: content,
        time: '剛剛',
        likes: 1,
        hugs: 1,
        allowChat: allowChat,
        comments: []
      };

      storiesData.unshift(newStory);
      filterStories();
      closePostModal();
      document.getElementById('postForm').reset();
    }

    // 1-on-1 Chat Mechanics
    let currentChatPartner = null;
    let chatMessagesHistory = {};

    function openChatWith(id, name, avatar, motto, storyTitle, category, initialGreeting) {
      currentChatPartner = { id, name, avatar, motto, storyTitle, category };

      document.getElementById('chatPartnerName').textContent = name;
      document.getElementById('chatPartnerAvatar').src = avatar;
      document.getElementById('chatPartnerMotto').textContent = motto || '對生活保持溫柔與熱愛';
      document.getElementById('chatCategoryTag').textContent = category;
      document.getElementById('chatStoryTitle').textContent = storyTitle;

      if (!chatMessagesHistory[id]) {
        chatMessagesHistory[id] = [
          {
            sender: 'partner',
            time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
            text: initialGreeting || `你好！我是${name}。很高興透過故事與你相遇，你想和我聊些什麼呢？`
          }
        ];
      }

      renderChatMessages();
      document.getElementById('chatModal').classList.remove('hidden');
    }

    function closeChatModal() { document.getElementById('chatModal').classList.add('hidden'); }

    function renderChatMessages() {
      if (!currentChatPartner) return;
      const container = document.getElementById('chatMessagesContainer');
      const messages = chatMessagesHistory[currentChatPartner.id] || [];

      container.innerHTML = messages.map(msg => {
        const isMe = msg.sender === 'me';
        return `
          <div class="flex items-start gap-2.5 ${isMe ? 'flex-row-reverse' : ''}">
            ${!isMe ? `<img src="${currentChatPartner.avatar}" class="w-8 h-8 rounded-full object-cover border border-amberwarm-300 shrink-0">` : ''}
            <div class="space-y-1 max-w-[75%]">
              <div class="p-3 rounded-2xl ${isMe ? 'bg-gradient-to-r from-amberwarm-400 to-amberwarm-600 text-white font-medium rounded-tr-none shadow-md' : 'bg-white text-amberwarm-950 border border-amberwarm-200 rounded-tl-none shadow-sm'}">
                ${msg.text}
              </div>
              <p class="text-[10px] text-amberwarm-600 ${isMe ? 'text-right' : 'text-left'}">${msg.time}</p>
            </div>
          </div>
        `;
      }).join('');

      container.scrollTop = container.scrollHeight;
    }

    function handleSendMessage(e) {
      e.preventDefault();
      const input = document.getElementById('chatInput');
      const text = input.value.trim();
      if (!text || !currentChatPartner) return;

      sendMessage(text);
      input.value = '';
    }

    function sendQuickGreeting(text) {
      if (!currentChatPartner) return;
      sendMessage(text);
    }

    function sendMessage(text) {
      const partnerId = currentChatPartner.id;
      const nowTime = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

      chatMessagesHistory[partnerId].push({ sender: 'me', time: nowTime, text: text });
      renderChatMessages();

      setTimeout(() => {
        simulatePartnerReply(partnerId);
      }, 1200);
    }

    function simulatePartnerReply(partnerId) {
      if (!chatMessagesHistory[partnerId]) return;

      const replies = [
        "謝謝你的溫暖回應！有時候能把心事說出來，感覺真的會輕鬆很多。",
        "我也非常認同你的想法。生活雖然不完美，但每一個堅持下來的瞬間都值得驕傲！",
        "聽到你這麼說真的很有同感！希望我們都能在各自的人生軌道上勇敢閃耀。",
        "謝謝你的鼓勵！今天能收到你的訊息，是我今天最開心的事情之一。"
      ];

      const randomReply = replies[Math.floor(Math.random() * replies.length)];

      chatMessagesHistory[partnerId].push({
        sender: 'partner',
        time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
        text: randomReply
      });

      if (currentChatPartner && currentChatPartner.id === partnerId) {
        renderChatMessages();
      }
    }

    let audioCtx = null;
    let activeSoundSource = null;

    function toggleSoundMenu() {
      document.getElementById('soundDropdown').classList.toggle('hidden');
    }

    function playAmbientSound(type) {
      document.getElementById('soundDropdown').classList.add('hidden');
      const icon = document.getElementById('soundIcon');

      if (activeSoundSource) {
        try { activeSoundSource.stop(); } catch(e){}
        activeSoundSource = null;
      }

      if (type === 'none') {
        icon.className = 'fa-solid fa-volume-xmark text-amberwarm-600';
        return;
      }

      if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      }
      if (audioCtx.state === 'suspended') { audioCtx.resume(); }

      if (type === 'rain') {
        icon.className = 'fa-solid fa-cloud-rain text-blue-500 animate-pulse';
        activeSoundSource = createWhiteNoiseNode(0.06);
      } else if (type === 'wind') {
        icon.className = 'fa-solid fa-wind text-teal-600 animate-pulse';
        activeSoundSource = createPinkNoiseNode(0.05);
      } else if (type === 'fire') {
        icon.className = 'fa-solid fa-fire text-amberwarm-600 animate-pulse';
        activeSoundSource = createBrownNoiseNode(0.08);
      }
    }

    function createWhiteNoiseNode(gainVal) {
      const bufferSize = audioCtx.sampleRate * 2;
      const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
      const output = buffer.getChannelData(0);
      for (let i = 0; i < bufferSize; i++) { output[i] = Math.random() * 2 - 1; }
      const noise = audioCtx.createBufferSource();
      noise.buffer = buffer;
      noise.loop = true;
      const gain = audioCtx.createGain();
      gain.gain.value = gainVal;
      noise.connect(gain);
      gain.connect(audioCtx.destination);
      noise.start();
      return noise;
    }

    function createPinkNoiseNode(gainVal) {
      const bufferSize = audioCtx.sampleRate * 2;
      const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
      const output = buffer.getChannelData(0);
      let b0=0, b1=0, b2=0, b3=0, b4=0, b5=0, b6=0;
      for (let i = 0; i < bufferSize; i++) {
        let white = Math.random() * 2 - 1;
        b0 = 0.99886 * b0 + white * 0.0555179;
        b1 = 0.99332 * b1 + white * 0.0750759;
        b2 = 0.96900 * b2 + white * 0.1538520;
        b3 = 0.86650 * b3 + white * 0.3104856;
        b4 = 0.55000 * b4 + white * 0.5329522;
        b5 = -0.7616 * b5 - white * 0.0168980;
        output[i] = (b0 + b1 + b2 + b3 + b4 + b5 + b6 + white * 0.5362) * 0.11;
        b6 = white * 0.115926;
      }
      const noise = audioCtx.createBufferSource();
      noise.buffer = buffer;
      noise.loop = true;
      const gain = audioCtx.createGain();
      gain.gain.value = gainVal;
      noise.connect(gain);
      gain.connect(audioCtx.destination);
      noise.start();
      return noise;
    }

    function createBrownNoiseNode(gainVal) {
      const bufferSize = audioCtx.sampleRate * 2;
      const buffer = audioCtx.createBuffer(1, bufferSize, audioCtx.sampleRate);
      const output = buffer.getChannelData(0);
      let lastOut = 0.0;
      for (let i = 0; i < bufferSize; i++) {
        let white = Math.random() * 2 - 1;
        output[i] = (lastOut + (0.02 * white)) / 1.02;
        lastOut = output[i];
        output[i] *= 3.5;
      }
      const noise = audioCtx.createBufferSource();
      noise.buffer = buffer;
      noise.loop = true;
      const gain = audioCtx.createGain();
      gain.gain.value = gainVal;
      noise.connect(gain);
      gain.connect(audioCtx.destination);
      noise.start();
      return noise;
    }
  </script>
</body>
</html>
