[index.html](https://github.com/user-attachments/files/25087107/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beauty Selection Bootcamp - Ice Breaking</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Noto Sans KR', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#eff6ff', 100: '#dbeafe', 500: '#3b82f6', 600: '#2563eb', 900: '#1e3a8a',
                        },
                        accent: {
                            50: '#fdf4ff', 100: '#fae8ff', 500: '#d946ef', 600: '#c026d3',
                        }
                    },
                    animation: {
                        'bounce-slight': 'bounce-slight 1s infinite',
                        'fade-in': 'fadeIn 0.5s ease-out',
                        'slide-up': 'slideUp 0.5s ease-out',
                    },
                    keyframes: {
                        'bounce-slight': {
                            '0%, 100%': { transform: 'translateY(-2px)' },
                            '50%': { transform: 'translateY(2px)' },
                        },
                        fadeIn: {
                            '0%': { opacity: '0' },
                            '100%': { opacity: '1' },
                        },
                        slideUp: {
                            '0%': { opacity: '0', transform: 'translateY(20px)' },
                            '100%': { opacity: '1', transform: 'translateY(0)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body { font-family: 'Noto Sans KR', sans-serif; background-color: #F8FAFC; overflow: hidden; }
        
        .glass-card {
            background: rgba(255, 255, 255, 0.95);
            border: 1px solid rgba(226, 232, 240, 0.8);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05), 0 2px 4px -1px rgba(0, 0, 0, 0.03);
        }

        /* 이름 가리기 효과 */
        .hidden-text {
            filter: blur(5px);
            user-select: none;
            background: #cbd5e1;
            color: transparent;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .hidden-text:hover {
            background: #94a3b8;
        }

        .revealed-text {
            filter: none;
            background: transparent;
            color: inherit;
            cursor: default;
        }

        /* 조 키워드 전용 스타일 */
        .team-keyword-hidden {
            filter: blur(6px);
            background: linear-gradient(90deg, #e2e8f0 0%, #cbd5e1 100%);
            color: transparent;
            border-radius: 6px;
            padding: 0 8px;
            cursor: pointer;
            display: inline-block;
            transform: translateY(2px);
        }
        
        .team-keyword-revealed {
            filter: none;
            background: transparent;
            color: #d946ef; /* accent-500 */
            cursor: default;
            animation: fadeIn 0.5s ease-out;
        }

        /* 하이라이트 애니메이션 */
        .highlight-card {
            background-color: #fdf4ff !important;
            border-color: #d946ef !important;
            box-shadow: 0 0 0 4px rgba(217, 70, 239, 0.2) !important;
            transform: scale(1.02);
            z-index: 10;
            transition: all 0.3s ease;
        }

        .custom-scrollbar::-webkit-scrollbar { width: 6px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #f1f5f9; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover { background: #94a3b8; }

        /* Slide Transitions */
        .slide-container {
            display: none;
            height: 100%;
            width: 100%;
            opacity: 0;
            transition: opacity 0.4s ease-in-out;
        }
        
        .slide-container.active {
            display: flex;
            opacity: 1;
        }
    </style>
</head>
<body class="h-screen flex flex-col">

    <!-- 1. Header (Fixed) -->
    <header class="bg-white border-b border-slate-200 h-16 shrink-0 shadow-sm z-50">
        <div class="max-w-7xl mx-auto px-4 h-full flex items-center justify-between">
            <div class="flex items-center gap-3 cursor-pointer" onclick="goToSlide(1)">
                <div class="bg-gradient-to-br from-blue-600 to-indigo-600 text-white p-2 rounded-lg shadow-md w-9 h-9 flex items-center justify-center">
                    <i class="fa-solid fa-users"></i>
                </div>
                <div>
                    <h1 class="text-lg font-bold text-slate-900 tracking-tight leading-none">Beauty Selection Bootcamp</h1>
                    <p class="text-xs text-slate-500 font-medium mt-0.5">부트캠프에 오신 여러분들과 함께 하는 아이스브레이킹!</p>
                </div>
            </div>
            
            <div class="flex items-center gap-3">
                <!-- Slide Indicators -->
                <div class="hidden md:flex gap-2 mr-4">
                    <div id="dot-1" class="w-2.5 h-2.5 rounded-full bg-slate-300 transition-all cursor-pointer" onclick="goToSlide(1)"></div>
                    <div id="dot-2" class="w-2.5 h-2.5 rounded-full bg-slate-300 transition-all cursor-pointer" onclick="goToSlide(2)"></div>
                    <div id="dot-3" class="w-2.5 h-2.5 rounded-full bg-slate-300 transition-all cursor-pointer" onclick="goToSlide(3)"></div>
                </div>

                <button onclick="handleRandomPick()" id="randomBtn" class="flex items-center gap-2 px-4 py-2 bg-fuchsia-600 hover:bg-fuchsia-700 text-white rounded-full transition-all shadow-md text-sm font-bold active:scale-95 hidden">
                    <i class="fa-solid fa-dice text-lg"></i>
                    <span class="hidden sm:inline">랜덤 지목</span>
                </button>
                <div class="h-6 w-px bg-slate-200 mx-1"></div>
                <button onclick="handleReset()" class="flex items-center gap-2 text-slate-500 hover:text-brand-600 text-sm font-medium transition-colors px-2">
                    <i class="fa-solid fa-rotate-left"></i> <span class="hidden sm:inline">초기화</span>
                </button>
            </div>
        </div>
    </header>

    <!-- 2. Main Content (Slides) -->
    <main class="flex-1 relative overflow-hidden bg-slate-50">
        
        <!-- SLIDE 1: Intro (Who is This?) -->
        <section id="slide-1" class="slide-container active flex-col justify-center items-center p-6 animate-fade-in">
            <div class="max-w-4xl w-full text-center space-y-8">
                <!-- Hero Banner -->
                <div class="py-16 px-8 bg-gradient-to-br from-blue-600 to-indigo-700 rounded-3xl text-white shadow-2xl relative overflow-hidden group mx-auto w-full transform hover:scale-[1.01] transition-transform duration-500">
                    <div class="absolute top-0 left-0 w-full h-full opacity-10 bg-[url('https://www.transparenttextures.com/patterns/cubes.png')]"></div>
                    <div class="relative z-10">
                        <span class="inline-block px-4 py-1.5 bg-white/20 backdrop-blur-sm rounded-full text-sm font-semibold mb-6 border border-white/30 shadow-lg animate-bounce-slight">
                            AI Team Analysis
                        </span>
                        <h2 class="text-6xl md:text-7xl font-black mb-6 tracking-tighter drop-shadow-2xl">WHO IS THIS?</h2>
                        <p class="text-blue-100 text-xl font-light leading-relaxed mb-8 max-w-2xl mx-auto">
                            AI가 분석한 키워드 데이터를 통해<br>
                            우리 조의 <strong>숨겨진 주인공</strong>을 찾아보세요!
                        </p>
                    </div>
                </div>

                <!-- Intro Card -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 w-full max-w-4xl mx-auto">
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 text-center hover:shadow-md transition-shadow">
                        <div class="w-12 h-12 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center mx-auto mb-4 text-xl">
                            <i class="fa-solid fa-magnifying-glass"></i>
                        </div>
                        <h3 class="font-bold text-slate-800 mb-2">1. 탐색 (Search)</h3>
                        <p class="text-sm text-slate-500 leading-snug">제시된 키워드를 보고<br>누구의 특징인지 추리해보세요.</p>
                    </div>
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 text-center hover:shadow-md transition-shadow">
                        <div class="w-12 h-12 bg-pink-100 text-pink-600 rounded-full flex items-center justify-center mx-auto mb-4 text-xl">
                            <i class="fa-regular fa-comments"></i>
                        </div>
                        <h3 class="font-bold text-slate-800 mb-2">2. 대화 (Talk)</h3>
                        <p class="text-sm text-slate-500 leading-snug">질문을 주고받으며<br>자연스럽게 서로를 알아가세요.</p>
                    </div>
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-200 text-center hover:shadow-md transition-shadow">
                        <div class="w-12 h-12 bg-indigo-100 text-indigo-600 rounded-full flex items-center justify-center mx-auto mb-4 text-xl">
                            <i class="fa-solid fa-wand-magic-sparkles"></i>
                        </div>
                        <h3 class="font-bold text-slate-800 mb-2">3. 발견 (Discover)</h3>
                        <p class="text-sm text-slate-500 leading-snug">가려진 정보를 클릭해<br>반전 매력을 확인하세요!</p>
                    </div>
                </div>

                <button onclick="nextSlide()" class="mt-8 px-8 py-4 bg-slate-900 text-white rounded-full font-bold text-lg hover:bg-slate-800 transition-all shadow-lg hover:shadow-xl flex items-center gap-3 mx-auto animate-bounce-slight">
                    시작하기 <i class="fa-solid fa-arrow-right"></i>
                </button>
            </div>
        </section>

        <!-- SLIDE 2: Keyword Talk (Questions) -->
        <section id="slide-2" class="slide-container flex-col p-6 items-center">
            <div class="max-w-5xl w-full h-full flex flex-col justify-center">
                <div class="text-center mb-8 animate-slide-up">
                    <span class="text-brand-600 font-bold text-sm tracking-widest uppercase mb-2 block">Ice Breaking Phase 1</span>
                    <h2 class="text-3xl font-bold text-slate-900">키워드 토크 질문</h2>
                    <p class="text-slate-500 mt-2">어색한 침묵은 NO! 이 질문들로 대화의 물꼬를 터보세요.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full animate-slide-up" style="animation-delay: 0.1s;">
                    <!-- Static Questions List -->
                    <div class="bg-white rounded-2xl shadow-lg border border-slate-100 overflow-hidden flex flex-col">
                        <div class="p-5 bg-slate-50 border-b border-slate-100">
                            <h3 class="font-bold text-lg text-slate-700 flex items-center gap-2">
                                <i class="fa-regular fa-star text-yellow-500"></i> 추천 질문 리스트
                            </h3>
                        </div>
                        <div class="p-6 space-y-4 overflow-y-auto custom-scrollbar max-h-[400px]">
                            <div class="bg-slate-50 border border-slate-200 rounded-xl p-4 hover:border-brand-300 transition-colors cursor-default">
                                <span class="text-xs font-bold text-brand-500 mb-1 block">Q1. 워라밸 / 취미</span>
                                <p class="text-base text-slate-700 font-medium">"퇴근 후나 주말에 '나를 위한 보상'으로 주로 무엇을 하시나요?"</p>
                            </div>
                            <div class="bg-slate-50 border border-slate-200 rounded-xl p-4 hover:border-brand-300 transition-colors cursor-default">
                                <span class="text-xs font-bold text-brand-500 mb-1 block">Q2. 덕질 / 몰입</span>
                                <p class="text-base text-slate-700 font-medium">"최근에 무언가에 '푹' 빠져서 시간 가는 줄 몰랐던 적이 있으신가요?"</p>
                            </div>
                            <div class="bg-slate-50 border border-slate-200 rounded-xl p-4 hover:border-brand-300 transition-colors cursor-default">
                                <span class="text-xs font-bold text-brand-500 mb-1 block">Q3. 성격 / 반전매력</span>
                                <p class="text-base text-slate-700 font-medium">"MBTI가 어떻게 되세요? 첫인상과 실제 성격이 다른 편인가요?"</p>
                            </div>
                            <div class="bg-slate-50 border border-slate-200 rounded-xl p-4 hover:border-brand-300 transition-colors cursor-default">
                                <span class="text-xs font-bold text-brand-500 mb-1 block">Q4. 성향 파악</span>
                                <p class="text-base text-slate-700 font-medium">"날씨 좋은 날, '핫플레이스 탐방' vs '집콕 힐링' 중 어느 쪽이세요?"</p>
                            </div>
                        </div>
                    </div>

                    <!-- AI Generator -->
                    <div class="flex flex-col gap-6">
                        <div class="flex-1 bg-gradient-to-br from-indigo-600 to-purple-700 rounded-2xl shadow-xl p-8 flex flex-col justify-center items-center text-center text-white relative overflow-hidden group">
                            <div class="absolute top-0 right-0 p-8 opacity-20 group-hover:scale-110 transition-transform duration-700">
                                <i class="fa-solid fa-robot text-9xl"></i>
                            </div>
                            
                            <div class="relative z-10 w-full max-w-md">
                                <h3 class="font-bold text-2xl mb-2 flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-wand-magic-sparkles text-yellow-300"></i> AI 랜덤 질문 생성
                                </h3>
                                <p class="text-indigo-100 mb-8 opacity-90">더 색다른 질문이 필요하신가요?<br>AI가 즉석에서 흥미로운 질문을 만들어 드립니다!</p>
                                
                                <div id="aiResponseBox" class="hidden min-h-[100px] flex items-center justify-center w-full bg-white/10 backdrop-blur-md rounded-xl p-6 text-lg font-medium border border-white/20 text-white shadow-inner animate-fade-in mb-6">
                                    <!-- AI Response -->
                                </div>

                                <button onclick="generateAiQuestion()" id="aiBtn" class="w-full py-4 bg-white text-indigo-700 font-bold rounded-xl shadow-lg hover:bg-indigo-50 transition-all transform active:scale-95 flex items-center justify-center gap-2 text-lg">
                                    <i class="fa-solid fa-shuffle"></i> 새로운 질문 뽑기
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SLIDE 3: Groups Grid -->
        <section id="slide-3" class="slide-container flex-col p-4 md:p-8">
            <div class="max-w-[1600px] w-full mx-auto h-full flex flex-col">
                <div class="flex justify-between items-end mb-6 animate-slide-up shrink-0">
                    <div>
                        <span class="text-brand-600 font-bold text-sm tracking-widest uppercase mb-1 block">Ice Breaking Phase 2</span>
                        <h2 class="text-3xl font-bold text-slate-900">우리 조를 소개합니다!</h2>
                    </div>
                    <div class="text-right hidden md:block">
                        <p class="text-sm text-slate-500">
                            <i class="fa-solid fa-mouse-pointer mr-1"></i> 카드를 클릭하여 <strong>키워드</strong>를 확인하세요.
                        </p>
                    </div>
                </div>

                <!-- Grid Container (Scrollable) -->
                <div class="flex-1 overflow-y-auto custom-scrollbar pr-2 pb-10 animate-slide-up" style="animation-delay: 0.1s;">
                    <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 2xl:grid-cols-4 gap-6" id="groupsContainer">
                        <!-- Cards injected via JS -->
                    </div>
                </div>
            </div>
        </section>

        <!-- Navigation Controls (Fixed Bottom) -->
        <div class="fixed bottom-6 left-1/2 transform -translate-x-1/2 flex items-center gap-4 bg-white/90 backdrop-blur shadow-lg border border-slate-200 px-6 py-3 rounded-full z-40">
            <button onclick="prevSlide()" id="prevBtn" class="text-slate-400 hover:text-slate-900 transition-colors disabled:opacity-30 disabled:cursor-not-allowed">
                <i class="fa-solid fa-chevron-left text-xl"></i>
            </button>
            <div class="text-xs font-bold text-slate-500 tracking-wider">
                <span id="slide-indicator">1</span> / 3
            </div>
            <button onclick="nextSlide()" id="nextBtn" class="text-slate-900 hover:text-brand-600 transition-colors disabled:opacity-30 disabled:cursor-not-allowed">
                <i class="fa-solid fa-chevron-right text-xl"></i>
            </button>
        </div>

    </main>

    <!-- Winner Modal -->
    <div id="winnerModal" class="fixed inset-0 z-[100] hidden items-center justify-center bg-black/60 backdrop-blur-sm opacity-0 transition-opacity duration-300">
        <div class="bg-white rounded-3xl p-8 max-w-sm w-full mx-4 text-center shadow-2xl relative overflow-hidden transform scale-95 transition-transform duration-300">
            <div class="absolute top-0 left-0 w-full h-2 bg-gradient-to-r from-fuchsia-500 to-indigo-500"></div>
            <button onclick="closeModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-xl"></i>
            </button>
            
            <div class="text-7xl mb-4 animate-bounce-slight" id="modalEmoji">🎉</div>
            <h3 class="text-2xl font-black text-slate-800 mb-2">당첨되셨습니다!</h3>
            <p class="text-brand-600 font-bold text-xl mb-1" id="modalName">이름</p>
            <p class="text-slate-500 text-sm mb-4" id="modalGroup">소속 조</p>
            
            <div class="flex flex-wrap justify-center gap-1.5 mb-6" id="modalKeywords"></div>
            
            <div class="bg-slate-50 rounded-xl p-4 mb-6 border border-slate-100">
                <p class="text-slate-600 font-medium text-sm">"지금 바로 질문에 답변해주세요!"</p>
            </div>
            
            <button onclick="closeModal()" class="w-full bg-slate-800 text-white font-bold py-3 rounded-xl hover:bg-slate-900 transition-colors">
                확인
            </button>
        </div>
    </div>

    <script>
        // --- Configuration ---
        const apiKey = ""; // API Key

        // --- State ---
        let currentSlide = 1;
        const totalSlides = 3;

        // --- Data ---
        const GROUPS_DATA = [
            {
                id: 1, icon: 'fa-bolt', 
                teamName: "1조", 
                desc: "운동, 사진, 언어 등 에너지가 넘치는 다재다능 팀",
                hiddenKeyword: "열정 만렙 & 반전 매력",
                color: "from-orange-400 to-red-500", 
                members: [
                    { id: "m1", name: "김민서", keywords: ["📸 야경 사냥꾼", "🍰 디저트 러버"], desc: "날씨 좋은 날 노을/야경 찍으러 가고, 예쁜 디저트 카페 투어가 취미.", emoji: "📸" },
                    { id: "m2", name: "장고은", keywords: ["🏋️ 헬창 꿈나무", "🗣️ 수다쟁이 ISFJ"], desc: "작년부터 헬스에 진심! 낯 가리지만 친해지면 말 많아지는 반전 매력.", emoji: "💪" },
                    { id: "m3", name: "배수언", keywords: ["🏃 러닝 & 웨이트", "🤐 반전 수다쟁이"], desc: "I 성향이지만 친해지면 입이 터지신다고 합니다. 요즘은 러닝과 웨이트 홀릭!", emoji: "🏃‍♀️" },
                    { id: "m4", name: "장포야", keywords: ["🏰 디즈니 시민", "🗣️ 3.25개국어"], desc: "한국 생활 7년 차 대만인! 3개 국어 능통 + 일본어 0.25! 디즈니 덕후.", emoji: "🏰" },
                    { id: "m5", name: "김선호", keywords: ["🛠️ 뚝딱뚝딱 금손", "🐈 냥님 모시는 집사"], desc: "만들고 꾸미는 게 취미인 금손 PD님. 집에서는 고양이님을 모시는 집사.", emoji: "🐈" }
                ]
            },
            {
                id: 2, icon: 'fa-mug-hot', 
                teamName: "2조", 
                desc: "요가, 미식, 뷰티로 일상을 치유하는 힐링 팀",
                hiddenKeyword: "힐링 & 테라피스트",
                color: "from-emerald-400 to-teal-500", 
                members: [
                    { id: "m6", name: "김지원", keywords: ["🧘 누워서 하는 요가", "💄 찐 코덕"], desc: "눕는 게 제일 좋아 요가도 누워서 함. 화장품 사랑해서 입사한 찐 코덕.", emoji: "🧘" },
                    { id: "m7", name: "박은빈", keywords: ["🍽️ 미식 테라피스트", "🐣 득근 꿈나무"], desc: "맛있는 음식으로 스트레스를 풀고, 이제 막 웨이트/러닝 입문한 헬린이!", emoji: "🍽️" },
                    { id: "m8", name: "김하은", keywords: ["💎 숨겨진 보석", "❓ 미스터리 멤버"], desc: "아직 데이터가 로딩 중인 신비주의 멤버! 직접 대화하며 찾아보세요.", emoji: "💎" },
                    { id: "m9", name: "김수연", keywords: ["🧘 요가 파이어", "📚 활자 중독 집사"], desc: "요가와 등산을 즐기지만 추운 건 질색! 책을 사랑하는 냥집사.", emoji: "📚" },
                    { id: "m10", name: "김지아(한지아)", keywords: ["💊 드럭스토어 탐험가", "🏠 집순이 여행러"], desc: "여행 가면 드럭스토어부터 터는 뷰티 덕후. 평소엔 극 I 성향 집순이!", emoji: "🏠" }
                ]
            },
            {
                id: 3, icon: 'fa-palette', 
                teamName: "3조", 
                desc: "패션, 커피, 게임 등 확고한 취향을 가진 팀",
                hiddenKeyword: "감각적인 취향 수집가들",
                color: "from-purple-400 to-violet-500", 
                members: [
                    { id: "m11", name: "조수아", keywords: ["✨ 분위기 메이커", "❓ 히든 카드"], desc: "팀의 분위기를 담당할 잠재적 에이스! 대화로 매력을 찾아주세요.", emoji: "✨" },
                    { id: "m12", name: "유혜지", keywords: ["👗 패션/뷰티 덕후", "😌 사회화된 I"], desc: "패션/뷰티에 진심! 차분하지만 일할 땐 확실한 '사회화된 I'.", emoji: "👗" },
                    { id: "m13", name: "윤은수", keywords: ["🔗 금손 뜨개러", "☕ 카페인 네비게이터"], desc: "물류 공급망의 핵심이자, 커피와 뜨개질 없이는 못 사는 분.", emoji: "🧶" },
                    { id: "m14", name: "이주미", keywords: ["☕ 카페인 GPS", "🤫 계획형 힐러"], desc: "쉬는 시간엔 커피와 사색이 필수인 INTJ. 맛집 제보 환영!", emoji: "☕" },
                    { id: "m15", name: "채송은", keywords: ["👾 마인크래프트 요리사", "🏗️ 랜선 건축가"], desc: "퇴근 후엔 마인크래프트 건축가이자 요리사가 되는 금손!", emoji: "👾" }
                ]
            },
            {
                id: 4, icon: 'fa-campground', 
                teamName: "4조", 
                desc: "음악, 수집, 캠핑 등 뚜렷한 덕질 포인트가 있는 팀",
                hiddenKeyword: "덕질과 취미의 만남",
                color: "from-blue-400 to-cyan-500", 
                members: [
                    { id: "m16", name: "제갈서현", keywords: ["🎧 플리 디깅", "🏃 러닝으로 힐링"], desc: "나만 아는 노래 찾기가 취미! 생각 비우러 러닝도 하십니다.", emoji: "🎧" },
                    { id: "m17", name: "한승현", keywords: ["🌏 #사회화된 내향인", "🎭 #취미_콜렉터"], desc: "조용한 줄 알았는데 흥이 넘치는 반전 매력. 일과 취미 모두 욕심쟁이.", emoji: "🎭" },
                    { id: "m18", name: "배문주", keywords: ["🎲 가챠계의 큰손", "💡 경험 수집가"], desc: "랜덤 뽑기(가챠) 사랑! 새로운 경험엔 아낌없이 투자하는 경험 사치러.", emoji: "🎲" },
                    { id: "m19", name: "이재호", keywords: ["⛺ 캠핑하는 내향인", "🎳 볼링 꿈나무"], desc: "조용한 I형이지만 캠핑과 볼링 같은 액티비티는 못 참는 반전 매력.", emoji: "⛺" },
                    { id: "m20", name: "이나윤", keywords: ["🍪 두바이 초코쿠키", "🧸 리락쿠마 500마리"], desc: "요즘 핫한 두바이 초코쿠키에 꽂히셨고, 집에 리락쿠마가 500마리!", emoji: "🧸" }
                ]
            },
            {
                id: 5, icon: 'fa-music', 
                teamName: "5조", 
                desc: "운동 신경과 예술적 감각이 공존하는 팀",
                hiddenKeyword: "액티브 & 아티스트",
                color: "from-rose-400 to-pink-500", 
                members: [
                    { id: "m21", name: "장희두", keywords: ["⛸️ 피겨 스케이팅", "🏔️ 오지 여행러"], desc: "피겨 스케이팅 경험! 남들 안 가는 오지 여행을 즐기는 모험가.", emoji: "⛸️" },
                    { id: "m22", name: "안희진", keywords: ["🥐 빵지순례자", "💄 코덕 만렙"], desc: "빵집 탐방이 취미인 빵순이이자, 화장품을 사랑하는 진성 코덕!", emoji: "🥐" },
                    { id: "m23", name: "안영현", keywords: ["🧶 프로 뜨개러", "🎤 도영 성덕"], desc: "뜨개질 장인! 최애(NCT 도영)가 모델인 브랜드에 입사한 진정한 성덕.", emoji: "🧶" },
                    { id: "m24", name: "홍수현", keywords: ["🛒 장바구니 컬렉터", "💜 10년차 아미"], desc: "BTS 10년 찐팬! 사고 싶은 건 일단 장바구니에 쌓아두는 맥시멀리스트.", emoji: "🛒" },
                    { id: "m25", name: "김이준", keywords: ["🦕 디지몬 테이머", "🏃 풀코스 철인"], desc: "마라톤 풀코스 4회 완주! 마음속엔 디지몬과 반지의 제왕을 품은 소년.", emoji: "🏃" }
                ]
            },
            {
                id: 6, icon: 'fa-plane', 
                teamName: "6조", 
                desc: "새로운 문화와 경험을 즐기는 글로벌 탐험대",
                hiddenKeyword: "호기심 천국 탐험가들",
                color: "from-sky-400 to-blue-500", 
                members: [
                    { id: "m26", name: "김수연", keywords: ["📚 활자 중독", "🧘 요가 파이어"], desc: "요가와 등산을 즐기고 책을 사랑하는 고양이 집사.", emoji: "📚" },
                    { id: "m27", name: "용서현", keywords: ["📸 뷰파인더", "🎳 스트라이크 장인"], desc: "사진 촬영이 취미이자 볼링에 진심인 분! 동남아 시장을 향한 열정!", emoji: "📸" },
                    { id: "m28", name: "이수연", keywords: ["🇺🇸 미국물 먹은 호기심", "🎢 프로 활동러"], desc: "오랜 해외 거주 경험과 호기심으로 똘똘 뭉친, 재미 수집가.", emoji: "🎢" },
                    { id: "m29", name: "김민희", keywords: ["✈️ 요코하마_도슨트", "🍪 트렌드_실험가"], desc: "요코하마 거주 경험 보유! 핫한 트렌드는 직접 해봐야 직성이 풀림.", emoji: "🗾" }
                ]
            },
            {
                id: 7, icon: 'fa-earth-americas', 
                teamName: "7조", 
                desc: "트렌디한 아이템과 글로벌 감각을 갖춘 팀",
                hiddenKeyword: "글로벌 힙스터",
                color: "from-indigo-400 to-violet-500", 
                members: [
                    { id: "m30", name: "이준혁", keywords: ["🍺 안주 찾아 러닝", "👟 생계형 러너"], desc: "작년 4월부터 러닝 시작! 사실 맛있는 안주 맛집 가려고 뛰는 러너.", emoji: "🍺" },
                    { id: "m31", name: "한지아", keywords: ["💊 드럭스토어 탐험가", "🏠 집순이 여행러"], desc: "여행 가면 관광지보다 드럭스토어부터 터는 뷰티 덕후.", emoji: "💊" },
                    { id: "m32", name: "이아현", keywords: ["🕯️ 향기 수집가", "🧘‍♀️ 루틴 지킴이"], desc: "향수와 코스메틱 덕후! 운동과 문화생활로 꽉 채운 건강한 루틴.", emoji: "🕯️" },
                    { id: "m33", name: "김나연", keywords: ["🍫 두바이 초코 사냥꾼", "🌏 글로벌 노마드"], desc: "3개국 거주 경험! 요즘은 두바이 초코와 인스타 트렌드에 푹 빠짐.", emoji: "🍫" }
                ]
            }
        ];

        // --- Init Render ---
        function init() {
            renderGroups();
            updateNavigation();
        }

        function renderGroups() {
            const container = document.getElementById('groupsContainer');
            container.innerHTML = GROUPS_DATA.map(group => `
                <div class="glass-card rounded-2xl overflow-hidden flex flex-col h-full hover:shadow-lg transition-shadow duration-300">
                    <!-- Header -->
                    <div class="px-5 py-4 border-b border-slate-100 bg-white relative">
                        <div class="flex items-start gap-3">
                            <div class="w-10 h-10 rounded-xl flex items-center justify-center shadow-md bg-gradient-to-br ${group.color} text-white shrink-0">
                                <i class="fa-solid ${group.icon} text-lg"></i>
                            </div>
                            <div>
                                <h3 class="font-bold text-slate-800 text-lg leading-tight mb-1">
                                    ${group.teamName} <span class="text-sm font-normal text-slate-500 ml-1">(${group.desc})</span>
                                </h3>
                                <!-- Hidden Keyword -->
                                <div onclick="toggleTeamKeyword(this)" class="team-keyword-hidden text-xs font-bold" title="클릭해서 확인하세요">
                                    <i class="fa-solid fa-key mr-1"></i> ${group.hiddenKeyword}
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- Members -->
                    <div class="p-4 space-y-3 flex-1 bg-slate-50/30">
                        ${group.members.map(member => `
                            <div id="member-${member.id}" onclick="toggleReveal(this)" 
                                 class="member-card relative p-3.5 rounded-xl border border-slate-100 bg-white hover:border-brand-200 hover:shadow-sm transition-all duration-300 cursor-pointer group select-none">
                                <div class="flex items-center gap-4">
                                    <div class="member-emoji text-3xl transition-transform duration-300 group-hover:scale-110">
                                        ${member.emoji}
                                    </div>
                                    <div class="flex-1 min-w-0">
                                        <div class="flex flex-wrap gap-1.5 mb-1.5">
                                            ${member.keywords.map(kw => `
                                                <span class="inline-flex items-center px-2 py-0.5 rounded text-[11px] font-bold bg-slate-100 text-slate-600 border border-slate-200 whitespace-nowrap">
                                                    ${kw}
                                                </span>
                                            `).join('')}
                                        </div>
                                        <div class="relative h-auto">
                                            <div class="flex items-center gap-2">
                                                <p class="member-name hidden-text font-bold text-base transition-all duration-300 text-slate-900">${member.name}</p>
                                                <span class="reveal-badge hidden text-[10px] px-1.5 py-0.5 bg-brand-100 text-brand-700 rounded font-bold animate-fade-in">OPEN</span>
                                            </div>
                                            <p class="member-desc h-0 opacity-0 overflow-hidden text-xs text-slate-500 mt-1 transition-all duration-300 leading-relaxed">${member.desc}</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `).join('');
        }

        // --- Slide Logic ---
        function updateNavigation() {
            // Update slides
            for (let i = 1; i <= totalSlides; i++) {
                const slide = document.getElementById(`slide-${i}`);
                const dot = document.getElementById(`dot-${i}`);
                
                if (i === currentSlide) {
                    slide.classList.add('active');
                    dot.classList.remove('bg-slate-300');
                    dot.classList.add('bg-slate-800', 'w-6');
                } else {
                    slide.classList.remove('active');
                    dot.classList.add('bg-slate-300');
                    dot.classList.remove('bg-slate-800', 'w-6');
                }
            }

            // Update buttons & indicators
            document.getElementById('slide-indicator').textContent = currentSlide;
            document.getElementById('prevBtn').disabled = currentSlide === 1;
            document.getElementById('nextBtn').disabled = currentSlide === totalSlides;

            // Show/Hide Random Button (Only visible on Slide 3)
            const randomBtn = document.getElementById('randomBtn');
            if (currentSlide === 3) {
                randomBtn.classList.remove('hidden');
                randomBtn.classList.add('flex');
            } else {
                randomBtn.classList.add('hidden');
                randomBtn.classList.remove('flex');
            }
        }

        function nextSlide() {
            if (currentSlide < totalSlides) {
                currentSlide++;
                updateNavigation();
            }
        }

        function prevSlide() {
            if (currentSlide > 1) {
                currentSlide--;
                updateNavigation();
            }
        }

        function goToSlide(n) {
            currentSlide = n;
            updateNavigation();
        }

        // --- Interaction Logic ---

        function toggleTeamKeyword(element) {
            if (element.classList.contains('team-keyword-hidden')) {
                element.classList.remove('team-keyword-hidden');
                element.classList.add('team-keyword-revealed');
            } else {
                element.classList.add('team-keyword-hidden');
                element.classList.remove('team-keyword-revealed');
            }
        }

        function toggleReveal(element) {
            const nameEl = element.querySelector('.member-name');
            const descEl = element.querySelector('.member-desc');
            const badgeEl = element.querySelector('.reveal-badge');

            if (nameEl.classList.contains('hidden-text')) {
                nameEl.classList.remove('hidden-text');
                nameEl.classList.add('revealed-text');
                descEl.classList.remove('h-0', 'opacity-0');
                badgeEl.classList.remove('hidden');
            } else {
                nameEl.classList.add('hidden-text');
                nameEl.classList.remove('revealed-text');
                descEl.classList.add('h-0', 'opacity-0');
                badgeEl.classList.add('hidden');
            }
        }

        function handleReset() {
            document.querySelectorAll('.member-card').forEach(el => {
                const nameEl = el.querySelector('.member-name');
                const descEl = el.querySelector('.member-desc');
                const badgeEl = el.querySelector('.reveal-badge');
                
                nameEl.classList.add('hidden-text');
                nameEl.classList.remove('revealed-text');
                descEl.classList.add('h-0', 'opacity-0');
                badgeEl.classList.add('hidden');
                el.classList.remove('highlight-card');
            });

            document.querySelectorAll('.team-keyword-revealed').forEach(el => {
                el.classList.add('team-keyword-hidden');
                el.classList.remove('team-keyword-revealed');
            });

            document.getElementById('aiResponseBox').classList.add('hidden');
            document.getElementById('aiPlaceholder').classList.remove('hidden');
        }

        // --- Random Picker Logic ---
        let isPicking = false;
        function handleRandomPick() {
            if (isPicking) return;
            isPicking = true;

            const btn = document.getElementById('randomBtn');
            const originalBtnHtml = btn.innerHTML;
            btn.innerHTML = '<i class="fa-solid fa-spinner fa-spin"></i> <span class="hidden sm:inline">추첨 중...</span>';

            const allMembers = [];
            GROUPS_DATA.forEach(g => {
                g.members.forEach(m => {
                    allMembers.push({ ...m, groupName: g.teamName + " (" + g.desc + ")" });
                });
            });

            document.querySelectorAll('.highlight-card').forEach(el => el.classList.remove('highlight-card'));

            let cycles = 0;
            const maxCycles = 15;
            let interval = 80;

            const spin = () => {
                const randomIndex = Math.floor(Math.random() * allMembers.length);
                const member = allMembers[randomIndex];
                const el = document.getElementById(`member-${member.id}`);

                document.querySelectorAll('.highlight-card').forEach(e => e.classList.remove('highlight-card'));
                if (el) {
                    el.classList.add('highlight-card');
                    el.scrollIntoView({ behavior: 'smooth', block: 'center' });
                }

                cycles++;

                if (cycles < maxCycles) {
                    interval += 10; 
                    setTimeout(spin, interval);
                } else {
                    setTimeout(() => {
                        isPicking = false;
                        btn.innerHTML = originalBtnHtml;
                        showWinnerModal(member);
                    }, 500);
                }
            };
            spin();
        }

        function showWinnerModal(member) {
            const modal = document.getElementById('winnerModal');
            document.getElementById('modalEmoji').textContent = member.emoji;
            document.getElementById('modalName').textContent = member.name;
            document.getElementById('modalGroup').textContent = member.groupName;
            document.getElementById('modalKeywords').innerHTML = member.keywords.map(k => 
                `<span class="text-xs bg-slate-100 text-slate-500 px-2 py-1 rounded-md border border-slate-200 font-bold">${k}</span>`
            ).join('');

            modal.classList.remove('hidden');
            modal.classList.add('flex');
            
            setTimeout(() => {
                modal.classList.remove('opacity-0');
                modal.querySelector('div').classList.remove('scale-95');
                modal.querySelector('div').classList.add('scale-100');
            }, 10);
        }

        function closeModal() {
            const modal = document.getElementById('winnerModal');
            modal.classList.add('opacity-0');
            modal.querySelector('div').classList.remove('scale-100');
            modal.querySelector('div').classList.add('scale-95');
            
            setTimeout(() => {
                modal.classList.remove('flex');
                modal.classList.add('hidden');
            }, 300);
        }

        // --- AI Generation Logic ---
        async function generateAiQuestion() {
            const aiBtn = document.getElementById('aiBtn');
            const aiBox = document.getElementById('aiResponseBox');
            const placeholder = document.getElementById('aiPlaceholder');

            aiBtn.disabled = true;
            aiBtn.innerHTML = '<i class="fa-solid fa-spinner fa-spin"></i> 생성 중...';

            const prompt = "신규 입사자 아이스브레이킹을 위한 참신하고 재미있는 질문 하나. 조건: 한국어, 흥미로운 주제(밸런스 게임, 엉뚱한 상상 등), 해요체, 질문 문장 하나만 출력.";

            try {
                if (!apiKey) {
                    throw new Error("API Key not configured");
                }

                const response = await fetch(
                    `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`,
                    {
                        method: "POST",
                        headers: { "Content-Type": "application/json" },
                        body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
                    }
                );

                if (!response.ok) throw new Error("API Error");
                const data = await response.json();
                const text = data.candidates?.[0]?.content?.parts?.[0]?.text;

                placeholder.classList.add('hidden');
                aiBox.classList.remove('hidden');
                aiBox.textContent = `"${text}"`;

            } catch (error) {
                console.error(error);
                const fallbacks = [
                    "10억이 생긴다면 가장 먼저 무엇을 사고 싶나요?",
                    "투명인간이 된다면 하루 동안 무엇을 하고 싶으신가요?",
                    "평생 한 가지 음식만 먹어야 한다면? (피자 vs 치킨)",
                    "자신을 동물로 표현한다면 어떤 동물인가요?",
                    "가장 기억에 남는 여행지는 어디인가요?"
                ];
                const randomFallback = fallbacks[Math.floor(Math.random() * fallbacks.length)];
                
                placeholder.classList.add('hidden');
                aiBox.classList.remove('hidden');
                aiBox.classList.remove('hidden'); // Ensure visible
                aiBox.textContent = `"${randomFallback}" (API 키 미설정으로 랜덤 질문 제공)`;
            } finally {
                aiBtn.disabled = false;
                aiBtn.innerHTML = '새로운 질문 뽑기';
            }
        }

        // Initialize App
        init();

    </script>
</body>
</html>
