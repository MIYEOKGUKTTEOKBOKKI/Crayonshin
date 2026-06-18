<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>진예지 | Portfolio Web App</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=BM+JUA&family=Nanum+Pen+Script&family=Pretendard:wght@800;900&display=swap" rel="stylesheet">
    <style>
        /* ==========================================================================
           1. DESIGN SYSTEM & VARIABLES (디자인 시스템 & 변수 설정)
           ========================================================================== */
        :root {
            --primary-color: #FFDE4D;       /* 활기찬 짱구 노랑 */
            --primary-light: #FFF4B7;       /* 부드러운 연노랑 */
            --secondary-color: #40A578;     /* 싱그러운 민트 그린 */
            --secondary-light: #9DDE8B;     /* 밝은 민트 */
            --dark-color: #2C3E50;          /* 깊이감 있는 텍스트용 네이비/블랙 */
            --light-color: #F9FBF9;         /* 베이스 배경색 */
            --card-bg: #FFFFFF;             /* 카드 배경 */
            
            /* 타이포그래피: 절대 글자가 사라지지 않도록 BM JUA 폰트와 고딕 계열 백업을 최우선 지정 */
            --font-main: 'BM JUA', 'Nanum Pen Script', 'Pretendard', -apple-system, sans-serif;
            --font-heading: 'BM JUA', 'Pretendard', -apple-system, sans-serif;
            
            /* 애니메이션 & 그림자 */
            --transition-smooth: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
            --shadow-sm: 0 4px 6px rgba(44, 62, 80, 0.05);
            --shadow-md: 0 10px 30px rgba(44, 62, 80, 0.08);
            --shadow-lg: 0 20px 40px rgba(44, 62, 80, 0.12);
            --radius-lg: 24px;
            --radius-md: 16px;
        }

        /* ==========================================================================
           2. RESET & BASE STYLES (기본 초기화 및 공통 스타일)
           ========================================================================== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        html {
            scroll-behavior: smooth;
            font-family: var(--font-main);
            background-color: var(--light-color);
            color: var(--dark-color);
            overflow-x: hidden;
            font-size: 18px; /* 가독성을 획기적으로 높인 베이스 폰트 크기 */
        }

        body {
            line-height: 1.6;
            color: var(--dark-color) !important; /* 글자색 강제 적용 */
        }

        section {
            padding: 120px 20px;
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
        }

        /* 스크롤바 커스텀 */
        ::-webkit-scrollbar {
            width: 10px;
        }
        ::-webkit-scrollbar-track {
            background: var(--light-color);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--secondary-light);
            border-radius: 5px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: var(--secondary-color);
        }

        /* ==========================================================================
           3. LAYOUT COMPONENTS (공통 레이아웃 구성요소)
           ========================================================================== */
        .section-header {
            text-align: center;
            margin-bottom: 60px;
            position: relative;
        }

        .section-header h2 {
            font-family: var(--font-heading);
            font-size: 2.8rem;
            font-weight: 900;
            position: relative;
            display: inline-block;
            margin-bottom: 10px;
            letter-spacing: -1px;
            color: var(--dark-color);
        }

        /* 타이틀 하단 데코레이션 선 */
        .section-header h2::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 6px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            border-radius: 10px;
        }

        .section-header p {
            color: #555555;
            font-size: 1.3rem;
            font-weight: 500;
        }

        /* 스크롤 애니메이션 효과를 주면서 최소 투명도 보장 */
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: var(--transition-smooth);
        }

        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* ==========================================================================
           4. HERO SECTION (첫 화면 영역)
           ========================================================================== */
        #hero {
            height: 100vh;
            max-width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: radial-gradient(circle at 20% 30%, rgba(255, 222, 77, 0.4) 0%, transparent 40%),
                        radial-gradient(circle at 80% 70%, rgba(64, 165, 120, 0.25) 0%, transparent 55%),
                        linear-gradient(135deg, #FFFDEB 0%, #EDF7F4 100%);
            position: relative;
            overflow: hidden;
            padding: 0 20px;
        }

        .bg-deco {
            position: absolute;
            border-radius: 50%;
            filter: blur(40px);
            z-index: 1;
            animation: float-deco 12s infinite ease-in-out alternate;
        }

        .bg-deco-1 {
            width: 300px;
            height: 300px;
            background-color: var(--primary-light);
            top: 10%;
            left: 10%;
        }

        .bg-deco-2 {
            width: 400px;
            height: 400px;
            background-color: #D6EFD8;
            bottom: 10%;
            right: 5%;
            animation-delay: -4s;
        }

        @keyframes float-deco {
            0% { transform: translateY(0) scale(1); }
            100% { transform: translateY(-40px) scale(1.15); }
        }

        .hero-content {
            position: relative;
            z-index: 10;
        }

        .hero-badge {
            display: inline-block;
            padding: 6px 20px;
            background: var(--card-bg);
            border: 2px solid var(--primary-color);
            color: var(--dark-color);
            font-family: var(--font-heading);
            font-weight: 800;
            font-size: 1rem;
            border-radius: 50px;
            margin-bottom: 20px;
            box-shadow: var(--shadow-sm);
            transform: rotate(-1.5deg);
        }

        .hero-content h1 {
            font-family: var(--font-heading);
            font-size: 4.5rem;
            font-weight: 900;
            line-height: 1.3;
            margin-bottom: 15px;
            color: var(--dark-color);
            letter-spacing: -1px;
        }

        .hero-content h1 span.highlight {
            position: relative;
            z-index: 1;
        }

        .hero-content h1 span.highlight::after {
            content: '';
            position: absolute;
            left: 0;
            bottom: 8px;
            width: 100%;
            height: 25px;
            background: var(--primary-color);
            z-index: -1;
            opacity: 0.7;
            border-radius: 4px;
        }

        .typing-container {
            font-size: 2.2rem;
            font-weight: 600;
            color: #34495E;
            height: 50px;
            margin-bottom: 30px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .typing-text {
            border-right: 3px solid var(--secondary-color);
            white-space: nowrap;
            padding-right: 5px;
            animation: blink 0.75s step-end infinite;
        }

        @keyframes blink {
            from, to { border-color: transparent }
            50% { border-color: var(--secondary-color); }
        }

        .scroll-indicator {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--secondary-color);
            gap: 5px;
            z-index: 10;
        }

        .scroll-mouse {
            width: 24px;
            height: 38px;
            border: 2px solid var(--secondary-color);
            border-radius: 20px;
            position: relative;
        }

        .scroll-wheel {
            width: 4px;
            height: 8px;
            background-color: var(--secondary-color);
            border-radius: 2px;
            position: absolute;
            top: 6px;
            left: 50%;
            transform: translateX(-50%);
            animation: scroll-anim 1.6s infinite;
        }

        @keyframes scroll-anim {
            0% { opacity: 1; transform: translate(-50%, 0); }
            100% { opacity: 0; transform: translate(-50%, 12px); }
        }

        /* ==========================================================================
           5. ABOUT ME SECTION (프로필 카드 영역)
           ========================================================================== */
        .about-wrapper {
            display: grid;
            grid-template-columns: 1fr 1.5fr;
            gap: 40px;
            align-items: stretch;
        }

        .profile-visual-card {
            background: linear-gradient(135deg, var(--primary-light) 0%, #E8F5E9 100%);
            border-radius: var(--radius-lg);
            padding: 40px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            box-shadow: var(--shadow-md);
            border: 1px solid rgba(255,255,255,0.6);
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .avatar-graphic {
            width: 160px;
            height: 160px;
            background: var(--card-bg);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 5rem;
            box-shadow: var(--shadow-sm);
            border: 4px solid var(--primary-color);
            margin-bottom: 20px;
            position: relative;
            transition: var(--transition-smooth);
        }

        .profile-visual-card:hover .avatar-graphic {
            transform: scale(1.05) rotate(5deg);
        }

        .profile-visual-card h3 {
            color: var(--dark-color);
        }

        .profile-details-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }

        .info-card {
            background: var(--card-bg);
            padding: 25px;
            border-radius: var(--radius-md);
            box-shadow: var(--shadow-sm);
            border: 1px solid rgba(0,0,0,0.02);
            transition: var(--transition-smooth);
        }

        .info-card:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow-md);
            border-color: var(--primary-light);
        }

        .info-card .label {
            font-size: 1.1rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: var(--secondary-color);
            font-weight: 700;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .info-card .value {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--dark-color);
            word-break: keep-all;
        }

        /* ==========================================================================
           6. MY SKILLS SECTION (역량/성격 스킬 바 영역)
           ========================================================================== */
        .skills-container {
            background: var(--card-bg);
            border-radius: var(--radius-lg);
            padding: 50px;
            box-shadow: var(--shadow-md);
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 40px;
        }

        .skill-item {
            display: flex;
            flex-direction: column;
        }

        .skill-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }

        .skill-name {
            font-weight: 700;
            font-size: 1.4rem;
            display: flex;
            align-items: center;
            gap: 8px;
            color: var(--dark-color);
        }

        .skill-percentage {
            font-weight: 800;
            color: var(--secondary-color);
            font-size: 1.3rem;
        }

        .skill-bar-track {
            height: 14px;
            background-color: #EDF2F7;
            border-radius: 10px;
            overflow: hidden;
            position: relative;
        }

        .skill-bar-fill {
            height: 100%;
            width: 0%; 
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            border-radius: 10px;
            transition: width 1.5s cubic-bezier(0.1, 1, 0.1, 1);
        }

        /* ==========================================================================
           7. MY FAVORITES SECTION (취향 저격 카드 갤러리)
           ========================================================================== */
        .favorites-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 30px;
        }

        .fav-card {
            background: var(--card-bg);
            border-radius: var(--radius-md);
            padding: 40px 35px;
            text-align: center;
            box-shadow: var(--shadow-sm);
            border: 1px solid rgba(0,0,0,0.01);
            transition: var(--transition-smooth);
            position: relative;
            overflow: hidden;
            z-index: 1;
        }

        .fav-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(255,222,77,0.15) 0%, rgba(64,165,120,0.15) 100%);
            z-index: -1;
            opacity: 0;
            transition: var(--transition-smooth);
        }

        .fav-card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: var(--shadow-lg);
            border-color: var(--secondary-light);
        }

        .fav-card:hover::before {
            opacity: 1;
        }

        .fav-title {
            font-size: 1.8rem;
            font-weight: 800;
            margin-bottom: 15px;
            color: var(--dark-color);
            position: relative;
            display: inline-block;
        }

        .fav-title::after {
            content: '';
            position: absolute;
            bottom: 2px;
            left: 0;
            width: 100%;
            height: 8px;
            background-color: rgba(255, 222, 77, 0.5);
            z-index: -1;
        }

        .fav-desc {
            font-size: 1.35rem;
            color: #4A5568;
            font-weight: 500;
            text-align: justify;
            text-align-last: center;
        }

        /* ==========================================================================
           8. MY DREAM SECTION (미래 지향 타임라인 구조)
           ========================================================================== */
        .dream-container {
            max-width: 800px;
            margin: 0 auto;
            position: relative;
        }

        .dream-timeline {
            position: absolute;
            left: 50%;
            top: 0;
            bottom: 0;
            width: 4px;
            background: linear-gradient(to bottom, var(--primary-color), var(--secondary-color));
            transform: translateX(-50%);
            border-radius: 10px;
        }

        .dream-item {
            margin-bottom: 40px;
            position: relative;
            width: 50%;
            padding: 0 40px;
        }

        .dream-item.left {
            left: 0;
            text-align: right;
        }

        .dream-item.right {
            left: 50%;
            text-align: left;
        }

        .dream-dot {
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background-color: var(--card-bg);
            border: 4px solid var(--secondary-color);
            position: absolute;
            top: 25px;
            z-index: 5;
            transition: var(--transition-smooth);
        }

        .dream-item.left .dream-dot {
            right: -10px;
        }

        .dream-item.right .dream-dot {
            left: -10px;
        }

        .dream-item:hover .dream-dot {
            background-color: var(--primary-color);
            transform: scale(1.3);
        }

        .dream-box {
            background: var(--card-bg);
            padding: 25px;
            border-radius: var(--radius-md);
            box-shadow: var(--shadow-sm);
            border: 1px solid rgba(0,0,0,0.02);
            transition: var(--transition-smooth);
        }

        .dream-item:hover .dream-box {
            box-shadow: var(--shadow-md);
            transform: translateY(-5px);
        }

        .dream-box h3 {
            font-size: 1.6rem;
            font-weight: 800;
            color: var(--dark-color);
            margin-bottom: 5px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .dream-item.left h3 {
            justify-content: flex-end;
        }

        .dream-box p {
            color: #4A5568;
            font-size: 1.3rem;
        }

        /* ==========================================================================
           9. QUOTE SECTION (감성적인 인용구 카드)
           ========================================================================== */
        .quote-wrapper {
            max-width: 900px;
            margin: 0 auto;
        }

        .quote-card {
            background: linear-gradient(135deg, var(--dark-color) 0%, #1A252F 100%);
            color: white;
            padding: 60px 40px;
            border-radius: var(--radius-lg);
            text-align: center;
            position: relative;
            box-shadow: var(--shadow-lg);
            overflow: hidden;
        }

        .quote-card::after {
            content: '';
            position: absolute;
            top: -50%;
            right: -20%;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            background: rgba(64, 165, 120, 0.2);
            filter: blur(50px);
        }

        .quote-icon {
            font-size: 4rem;
            color: var(--primary-color);
            margin-bottom: 10px;
            opacity: 0.8;
            line-height: 1;
        }

        .quote-text {
            font-size: 2.4rem;
            font-weight: 800;
            line-height: 1.5;
            margin-bottom: 15px;
            letter-spacing: -0.5px;
            word-break: keep-all;
            color: #FFFFFF !important;
        }

        .quote-author {
            font-size: 1.4rem;
            color: var(--secondary-light);
            font-weight: 600;
            letter-spacing: 2px;
        }

        /* ==========================================================================
           10. FOOTER (하단 푸터 정보)
           ========================================================================== */
        footer {
            background-color: #F0F4F1;
            padding: 40px 20px;
            text-align: center;
            font-size: 1.2rem;
            color: #555555;
            border-top: 1px solid rgba(0,0,0,0.05);
            font-weight: 600;
        }

        footer p .heart {
            color: #E74C3C;
            animation: heart-beat 0.8s infinite alternate;
            display: inline-block;
        }

        @keyframes heart-beat {
            0% { transform: scale(1); }
            100% { transform: scale(1.15); }
        }

        /* ==========================================================================
           11. RESPONSIVE MEDIA QUERIES (반응형 최적화 모바일 레이아웃)
           ========================================================================== */
        @media (max-width: 992px) {
            .about-wrapper {
                grid-template-columns: 1fr;
            }
            .skills-container {
                grid-template-columns: 1fr;
                padding: 35px;
            }
            .favorites-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            .hero-content h1 {
                font-size: 3.5rem;
            }
        }

        @media (max-width: 768px) {
            section {
                padding: 80px 20px;
            }
            .hero-content h1 {
                font-size: 2.8rem;
            }
            .typing-container {
                font-size: 1.8rem;
            }
            .profile-details-grid {
                grid-template-columns: 1fr;
            }
            .favorites-grid {
                grid-template-columns: 1fr;
            }
            .dream-timeline {
                left: 20px;
            }
            .dream-item {
                width: 100%;
                padding-left: 45px;
                padding-right: 0;
            }
            .dream-item.left {
                text-align: left;
            }
            .dream-item.left h3 {
                justify-content: flex-start;
            }
            .dream-item.left .dream-dot,
            .dream-item.right .dream-dot {
                left: 10px;
            }
            .dream-item.right {
                left: 0;
            }
            .quote-text {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>

    <div class="bg-deco bg-deco-1"></div>
    <div class="bg-deco bg-deco-2"></div>

    <header id="hero">
        <div class="hero-content">
            <div class="hero-badge">PORTFOLIO APPLICATION</div>
            <h1>안녕하세요, <br><span class="highlight">진예지</span>입니다.</h1>
            <div class="typing-container">
                <span class="typing-text"></span>
            </div>
        </div>
        <div class="scroll-indicator">
            <span>SCROLL DOWN</span>
            <div class="scroll-mouse">
                <div class="scroll-wheel"></div>
            </div>
        </div>
    </header>

    <main>
        <section id="about" class="reveal">
            <div class="section-header">
                <h2>About Me</h2>
                <p>차분하면서도 내면에 확실한 열정을 지닌 저를 소개합니다</p>
            </div>
            
            <div class="about-wrapper">
                <div class="profile-visual-card">
                    <div class="avatar-graphic">🧑‍🎨</div>
                    <h3 style="font-size: 2.2rem; font-weight:800; margin-bottom:5px;">진예지</h3>
                    <p style="color: #2E7D32; font-size: 1.5rem; font-weight:700;">#짱구누나 #차분함 #조용함</p>
                </div>

                <div class="profile-details-grid">
                    <div class="info-card">
                        <div class="label">💡 나를 표현하는 문장</div>
                        <div class="value">짱구누나</div>
                    </div>
                    <div class="info-card">
                        <div class="label">🎯 관심 분야</div>
                        <div class="value">신짱구 및 세계관 연구</div>
                    </div>
                    <div class="info-card">
                        <div class="label">🎵 나의 취미</div>
                        <div class="value">잔잔한 노래 듣기, 새로운 짱구 에피소드 찾아보기</div>
                    </div>
                    <div class="info-card">
                        <div class="label">✨ 나의 성격 & 분위기</div>
                        <div class="value">차분함과 조용함 속에 깃든 따뜻함</div>
                    </div>
                </div>
            </div>
        </section>

        <section id="skills" class="reveal">
            <div class="section-header">
                <h2>My Skills</h2>
                <p>내가 가진 고유한 핵심 역량과 강점 자산</p>
            </div>

            <div class="skills-container">
                <div class="skill-item">
                    <div class="skill-info">
                        <span class="skill-name">🤝 다정함 (Empathy)</span>
                        <span class="skill-percentage">95%</span>
                    </div>
                    <div class="skill-bar-track">
                        <div class="skill-bar-fill" data-percent="95%"></div>
                    </div>
                </div>
                <div class="skill-item">
                    <div class="skill-info">
                        <span class="skill-name">🌱 성실함 (Consistency)</span>
                        <span class="skill-percentage">90%</span>
                    </div>
                    <div class="skill-bar-track">
                        <div class="skill-bar-fill" data-percent="90%"></div>
                    </div>
                </div>
                <div class="skill-item">
                    <div class="skill-info">
                        <span class="skill-name">😊 잘 웃기 (Positive Energy)</span>
                        <span class="skill-percentage">88%</span>
                    </div>
                    <div class="skill-bar-track">
                        <div class="skill-bar-fill" data-percent="88%"></div>
                    </div>
                </div>
                <div class="skill-item">
                    <div class="skill-info">
                        <span class="skill-name">🔍 아카이빙 및 정보 탐색</span>
                        <span class="skill-percentage">85%</span>
                    </div>
                    <div class="skill-bar-track">
                        <div class="skill-bar-fill" data-percent="85%"></div>
                    </div>
                </div>
            </div>
        </section>

        <section id="favorites" class="reveal">
            <div class="section-header">
                <h2>My Favorites</h2>
                <p>생각만 해도 기분이 좋아지는 컬렉션</p>
            </div>

            <div class="favorites-grid">
                <div class="fav-card">
                    <h3 class="fav-title">짱구는 못말려</h3>
                    <p class="fav-desc">유년 시절부터 지금까지 변함없이 마음을 치유해주는 최애 애니메이션 작품.</p>
                </div>
                <div class="fav-card">
                    <h3 class="fav-title">신짱구</h3>
                    <p class="fav-desc">예측 불가능하지만 결코 미워할 수 없는 긍정 가득 유쾌한 주인공 캐릭터.</p>
                </div>
                <div class="fav-card">
                    <h3 class="fav-title">흰둥이</h3>
                    <p class="fav-desc">솜사탕 같고 똑똑하며 언제나 짱구 가족 곁을 묵묵히 지켜주는 귀염둥이 마스코트.</p>
                </div>
            </div>
        </section>

        <section id="dream" class="reveal">
            <div class="section-header">
                <h2>My Dream</h2>
                <p>앞으로 넓은 세상 속으로 나아갈 원대한 로드맵</p>
            </div>

            <div class="dream-container">
                <div class="dream-timeline"></div>

                <div class="dream-item left">
                    <div class="dream-dot"></div>
                    <div class="dream-box">
                        <h3>🎒 카스카베 여행</h3>
                        <p>짱구의 숨결과 세계관이 살아 숨 쉬는 실제 배경 마을, 카스카베로 떠나는 특별 성지순례.</p>
                    </div>
                </div>

                <div class="dream-item right">
                    <div class="dream-dot"></div>
                    <div class="dream-box">
                        <h3>👑 진정한 짱덕 되기</h3>
                        <p>단순한 시청을 넘어 깊이 있는 이해와 굿즈 콜렉팅을 마스터한 명예 짱구 덕후로 진화하기.</p>
                    </div>
                </div>

                <div class="dream-item left">
                    <div class="dream-dot"></div>
                    <div class="dream-box">
                        <h3>💵 경제적 여유 구축</h3>
                        <p>원하는 것을 자유롭게 선택하고 실천할 수 있는 안정적인 자립 기반과 자유 마련하기.</p>
                    </div>
                </div>

                <div class="dream-item right">
                    <div class="dream-dot"></div>
                    <div class="dream-box">
                        <h3>🌍 세계 일주 완주</h3>
                        <p>새로운 대륙, 다양한 문화권을 온몸으로 경험하며 세상을 넓고 깊게 보는 안목 기르기.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="quote" class="reveal">
            <div class="quote-wrapper">
                <div class="quote-card">
                    <div class="quote-icon">“</div>
                    <p class="quote-text">차분하지만 확실한 발걸음으로,<br>내가 좋아하는 것들로 가득 찬 행복한 세상을 만들어갈 거예요.</p>
                    <div class="quote-author">- 진예지 -</div>
                </div>
            </div>
        </section>
    </main>

    <footer>
        <p>Made with AI & <span class="heart">♥</span> My Imagination | © 2026 Jin Ye Ji</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            
            /* 1. TYPING ANIMATION */
            const typingText = document.querySelector('.typing-text');
            const phrases = [
                "매일 성실하고 다정하게 살아갑니다.",
                "짱구를 정말 사랑하는 덕후입니다.",
                "꿈을 향해 한 걸음씩 나아가는 중입니다."
            ];
            
            let phraseIdx = 0;
            let charIdx = 0;
            let isDeleting = false;
            let typingSpeed = 100;

            function typeEffect() {
                const currentPhrase = phrases[phraseIdx];
                
                if (isDeleting) {
                    typingText.textContent = currentPhrase.substring(0, charIdx - 1);
                    charIdx--;
                    typingSpeed = 40; 
                } else {
                    typingText.textContent = currentPhrase.substring(0, charIdx + 1);
                    charIdx++;
                    typingSpeed = 120;
                }

                if (!isDeleting && charIdx === currentPhrase.length) {
                    typingSpeed = 2000; 
                    isDeleting = true;
                } else if (isDeleting && charIdx === 0) {
                    isDeleting = false;
                    phraseIdx = (phraseIdx + 1) % phrases.length; 
                    typingSpeed = 500; 
                }

                setTimeout(typeEffect, typingSpeed);
            }
            
            typeEffect();


            /* 2. SCROLL REVEAL ANIMATION */
            const revealElements = document.querySelectorAll('.reveal');
            
            const revealObserver = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('active');
                        
                        if (entry.target.id === 'skills') {
                            animateSkills();
                        }
                        observer.unobserve(entry.target);
                    }
                });
            }, {
                threshold: 0.15, 
                rootMargin: "0px 0px -50px 0px"
            });

            revealElements.forEach(element => {
                revealObserver.observe(element);
            });


            /* 3. SKILLS BAR ANIMATION */
            function animateSkills() {
                const skillBars = document.querySelectorAll('.skill-bar-fill');
                skillBars.forEach(bar => {
                    const targetPercent = bar.getAttribute('data-percent');
                    bar.style.width = targetPercent;
                });
            }
        });
    </script>
</body>
</html>
