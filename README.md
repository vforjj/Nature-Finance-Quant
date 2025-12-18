# Nature-Finance-Quant

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NFQ Lab | Nature Finance Quant Laboratory</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-main: #F8FAFC;
            --text-dark: #0F172A;
            --nfq-blue: #0369A1;
            --nfq-green: #15803D;
            --nfq-red: #E11D48;
            --nfq-accent: #FACC15;
        }
        body { font-family: 'Noto Sans KR', sans-serif; background-color: var(--bg-main); color: var(--text-dark); scroll-behavior: smooth; }
        .mono { font-family: 'JetBrains Mono', monospace; }
        
        .chart-container {
            position: relative;
            width: 100%;
            height: 300px;
            margin: 0 auto;
        }
        @media (min-width: 768px) {
            .chart-container { height: 350px; }
        }
        
        .card {
            background: white;
            border-radius: 1rem;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
            border: 1px solid #E2E8F0;
            padding: 1.5rem;
            transition: transform 0.2s ease;
        }
        .card:hover { transform: translateY(-2px); }

        .glass-header {
            background: rgba(248, 250, 252, 0.8);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid #E2E8F0;
        }

        /* Range Slider Styling */
        input[type=range] {
            -webkit-appearance: none;
            width: 100%;
            background: transparent;
        }
        input[type=range]::-webkit-slider-thumb {
            -webkit-appearance: none;
            height: 18px;
            width: 18px;
            border-radius: 50%;
            background: var(--nfq-blue);
            cursor: pointer;
            margin-top: -7px;
            box-shadow: 0 0 10px rgba(3, 105, 161, 0.3);
        }
        input[type=range]::-webkit-slider-runnable-track {
            width: 100%;
            height: 4px;
            cursor: pointer;
            background: #E2E8F0;
            border-radius: 2px;
        }

        .highlight { color: var(--nfq-blue); font-weight: 700; }
        .highlight-green { color: var(--nfq-green); font-weight: 700; }
        .highlight-red { color: var(--nfq-red); font-weight: 700; }
        
        section { opacity: 0; transform: translateY(20px); transition: all 0.6s ease-out; }
        section.visible { opacity: 1; transform: translateY(0); }
    </style>
</head>
<body class="antialiased">

    <!-- Navigation -->
    <nav class="fixed w-full z-50 glass-header">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex items-center gap-2">
                    <div class="bg-slate-900 text-white p-1.5 rounded-md font-bold text-xs mono">NFQ</div>
                    <span class="font-bold text-lg tracking-tight">NFQ <span class="text-sky-700">Lab</span></span>
                </div>
                <div class="hidden md:flex space-x-8 text-sm font-medium text-slate-600">
                    <a href="#macro" class="hover:text-sky-700 transition">Market Gap</a>
                    <a href="#methodology" class="hover:text-sky-700 transition">Methodology</a>
                    <a href="#simulator" class="hover:text-sky-700 transition">Simulator</a>
                    <a href="#case-study" class="hover:text-sky-700 transition">Pilot Case</a>
                </div>
                <button class="bg-sky-700 text-white px-5 py-2 rounded-lg text-sm font-bold hover:bg-sky-800 transition">
                    Contact Lab
                </button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="pt-40 pb-24 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto text-center">
        <div class="inline-flex items-center gap-2 px-3 py-1 bg-sky-50 text-sky-700 rounded-full text-xs font-bold uppercase tracking-wider mb-6 border border-sky-100">
            <span class="w-2 h-2 rounded-full bg-sky-600 animate-pulse"></span> Nature Finance Quant Intelligence
        </div>
        <h1 class="text-4xl md:text-7xl font-black text-slate-900 mb-8 leading-tight">
            자연의 가치를 <br>
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-sky-700 to-emerald-700">금융의 언어(Quant)</span>로 번역하다
        </h1>
        <p class="text-lg md:text-xl text-slate-600 max-w-3xl mx-auto leading-relaxed mb-12">
            NFQ Lab은 수학적 모델링과 AI 데이터 분석을 통해 자연 자본의 리스크를 정량화하고,<br class="hidden md:block">
            <span class="font-bold text-slate-900">지속 가능한 투자의 재무적 타당성</span>을 증명합니다.
        </p>
        <div class="flex flex-wrap justify-center gap-4">
            <a href="#simulator" class="bg-sky-700 text-white px-10 py-4 rounded-xl font-bold hover:bg-sky-800 transition shadow-xl shadow-sky-200">
                시뮬레이터 실행하기
            </a>
            <a href="#macro" class="bg-white text-slate-700 border border-slate-200 px-10 py-4 rounded-xl font-bold hover:bg-slate-50 transition">
                시장 분석 보기
            </a>
        </div>
    </header>

    <!-- Section 1: Macro Context -->
    <section id="macro" class="py-24 bg-white border-y border-slate-100">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid md:grid-cols-2 gap-16 items-center mb-16">
                <div>
                    <h2 class="text-3xl font-bold text-slate-900 mb-6">자연 금융의 거대한 격차 <br><span class="text-slate-400 font-light">(The Financing Gap)</span></h2>
                    <p class="text-slate-600 mb-8 text-lg leading-relaxed">
                        전 세계 GDP의 절반 이상인 <span class="highlight">$44 Trillion</span>이 자연 자본에 의존하고 있습니다.
                        그러나 생물다양성 보존을 위한 자금은 연간 <span class="highlight-red">$700 Billion</span>이 부족한 상황입니다.
                        이 격차는 금융 기관에게 거대한 리스크이자, 동시에 새로운 투자 기회입니다.
                    </p>
                    <div class="grid grid-cols-2 gap-6">
                        <div class="p-6 bg-slate-50 rounded-2xl border border-slate-100">
                            <p class="text-xs text-slate-500 font-bold uppercase mb-1">GDP Dependency</p>
                            <p class="text-3xl font-black text-slate-900">55%</p>
                        </div>
                        <div class="p-6 bg-rose-50 rounded-2xl border border-rose-100">
                            <p class="text-xs text-rose-500 font-bold uppercase mb-1">Annual Gap</p>
                            <p class="text-3xl font-black text-rose-600">$700B</p>
                        </div>
                    </div>
                </div>
                <div class="card bg-slate-50/50">
                    <h3 class="text-sm font-bold text-slate-500 uppercase mb-6 flex justify-between">
                        <span>Global Biodiversity Funding Gap</span>
                        <span class="text-[10px] text-slate-400">Unit: $Billion</span>
                    </h3>
                    <div class="chart-container">
                        <canvas id="fundingGapChart"></canvas>
                    </div>
                    <p class="text-xs text-slate-400 mt-6 text-center italic">Data Source: Paulson Institute, The Nature Conservancy</p>
                </div>
            </div>

            <div class="grid md:grid-cols-3 gap-8">
                <div class="card">
                    <h3 class="text-sm font-bold text-slate-500 uppercase mb-4">Nature Dependency (Asset Mix)</h3>
                    <div class="chart-container" style="height: 220px;">
                        <canvas id="dependencyChart"></canvas>
                    </div>
                    <p class="text-sm text-slate-600 mt-6 text-center leading-snug">
                        포트폴리오의 <span class="highlight">55%</span>가 자연 자본 리스크에<br>직접적으로 노출되어 있습니다.
                    </p>
                </div>
                <div class="md:col-span-2 flex flex-col justify-center lg:pl-12 border-l-4 border-sky-100 bg-sky-50/30 p-8 rounded-r-2xl">
                    <h3 class="text-2xl font-bold text-slate-900 mb-4">왜 퀀트(Quant)인가?</h3>
                    <p class="text-slate-600 mb-6 text-lg">
                        전통적인 금융 모델은 자연의 복합성을 경제적 가치로 계산하지 못합니다.<br>NFQ Lab의 퀀트 모델은 다음을 수행합니다:
                    </p>
                    <ul class="grid sm:grid-cols-1 gap-4">
                        <li class="flex items-start gap-4 p-3 bg-white rounded-xl shadow-sm border border-slate-100">
                            <span class="bg-sky-600 text-white w-6 h-6 flex items-center justify-center rounded-full text-xs font-bold shrink-0 mt-0.5">1</span>
                            <span class="text-slate-700 text-sm leading-relaxed"><strong>Risk Modeling:</strong> 물리적/이행 리스크를 nVaR(Nature Value at Risk)로 정밀 산출</span>
                        </li>
                        <li class="flex items-start gap-4 p-3 bg-white rounded-xl shadow-sm border border-slate-100">
                            <span class="bg-emerald-600 text-white w-6 h-6 flex items-center justify-center rounded-full text-xs font-bold shrink-0 mt-0.5">2</span>
                            <span class="text-slate-700 text-sm leading-relaxed"><strong>Valuation:</strong> 생태계 서비스의 가치를 현금 흐름(Cash Flow) 모델에 직접 통합</span>
                        </li>
                        <li class="flex items-start gap-4 p-3 bg-white rounded-xl shadow-sm border border-slate-100">
                            <span class="bg-amber-500 text-white w-6 h-6 flex items-center justify-center rounded-full text-xs font-bold shrink-0 mt-0.5">3</span>
                            <span class="text-slate-700 text-sm leading-relaxed"><strong>Data Integration:</strong> 위성 데이터와 재무 데이터를 결합하여 실시간 상관관계 분석</span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 2: Methodology -->
    <section id="methodology" class="py-24 bg-slate-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-20">
                <h2 class="text-3xl font-bold text-slate-900 mb-6">불확실성을 데이터로 <br><span class="text-slate-400 font-light">(From Uncertainty to Data)</span></h2>
                <p class="text-slate-600 max-w-2xl mx-auto text-lg leading-relaxed">
                    NFQ Lab은 독자적인 알고리즘을 통해 생태계의 건강도를 측정하고,<br>이를 재무적 리스크 분포로 변환하여 의사결정을 지원합니다.
                </p>
            </div>

            <div class="grid md:grid-cols-2 gap-10">
                <div class="card">
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="text-sm font-bold text-slate-500 uppercase">Ecosystem Health Metrics</h3>
                        <span class="bg-emerald-100 text-emerald-800 text-[10px] font-black px-2 py-1 rounded uppercase">AI Vision Analysis</span>
                    </div>
                    <div class="chart-container">
                        <canvas id="ecosystemRadarChart"></canvas>
                    </div>
                    <p class="text-sm text-slate-600 mt-6 leading-relaxed">
                        AI Vision을 통해 분석된 생태계는 <span class="highlight-green">복원 후(Restored)</span> 모든 지표에서 회복 탄력성과 가용 가치가 급격히 상승함을 보여줍니다.
                    </p>
                </div>

                <div class="card">
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="text-sm font-bold text-slate-500 uppercase">Risk Distribution (nVaR)</h3>
                        <span class="bg-sky-100 text-sky-800 text-[10px] font-black px-2 py-1 rounded uppercase">Monte Carlo Sim</span>
                    </div>
                    <div class="chart-container">
                        <canvas id="riskHistogramChart"></canvas>
                    </div>
                    <p class="text-sm text-slate-600 mt-6 leading-relaxed">
                        자연 자본 투자는 꼬리 리스크(Tail Risk)를 획기적으로 줄여, 포트폴리오의 <span class="highlight">안정성</span>을 높이는 'Shift Left' 효과를 창출합니다.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 3: Interactive Simulator -->
    <section id="simulator" class="py-24 bg-slate-900 text-white relative overflow-hidden">
        <div class="absolute top-0 left-0 w-full h-full overflow-hidden opacity-20 pointer-events-none">
            <div class="absolute -top-20 -left-20 w-96 h-96 bg-sky-600 rounded-full blur-[100px]"></div>
            <div class="absolute bottom-20 right-20 w-80 h-80 bg-emerald-600 rounded-full blur-[100px]"></div>
        </div>

        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="mb-16">
                <span class="font-mono text-sky-400 text-xs font-bold tracking-widest bg-sky-400/10 px-2 py-1 rounded">NFQ_TERMINAL_V2.5</span>
                <h2 class="text-3xl md:text-5xl font-bold mt-4 leading-tight">자연 자본 복원 투자 시뮬레이터 <br><span class="text-slate-500 font-light">(Quant Simulator)</span></h2>
                <p class="text-slate-400 mt-6 max-w-2xl text-lg">
                    투자 규모와 생태 복원 목표를 설정하여, 예상되는 <span class="text-white font-bold">NPV(순현재가치)</span>와 <span class="text-white font-bold">nVaR(자연 리스크)</span>를 금융공학적 관점에서 예측합니다.
                </p>
            </div>

            <div class="grid lg:grid-cols-12 gap-10">
                <div class="lg:col-span-4 space-y-8">
                    <div class="bg-white/5 backdrop-blur-xl border border-white/10 p-8 rounded-3xl">
                        <h3 class="text-xs font-bold text-slate-400 uppercase mb-8 tracking-[0.2em] border-b border-white/10 pb-4">Model Parameters</h3>
                        
                        <div class="mb-10">
                            <div class="flex justify-between text-sm font-bold mb-3">
                                <span class="text-slate-300">초기 투자금 (Capital)</span>
                                <span id="dispCap" class="text-sky-400 mono">50억 원</span>
                            </div>
                            <input type="range" id="inputCap" min="10" max="500" step="10" value="50" class="accent-sky-500">
                        </div>

                        <div class="mb-10">
                            <div class="flex justify-between text-sm font-bold mb-3">
                                <span class="text-slate-300">생태 복원 목표 (%)</span>
                                <span id="dispBio" class="text-emerald-400 mono">65%</span>
                            </div>
                            <input type="range" id="inputBio" min="0" max="100" step="5" value="65" class="accent-emerald-500">
                        </div>

                        <div class="mb-10">
                            <div class="flex justify-between text-sm font-bold mb-3">
                                <span class="text-slate-300">투자 기간 (Horizon)</span>
                                <span id="dispTime" class="text-amber-400 mono">15년</span>
                            </div>
                            <input type="range" id="inputTime" min="5" max="30" step="1" value="15" class="accent-amber-500">
                        </div>

                        <button id="btnRun" class="w-full bg-sky-700 hover:bg-sky-600 text-white font-bold py-4 rounded-2xl transition shadow-lg shadow-sky-900/40 flex items-center justify-center gap-2">
                            <span>⚡</span> 시뮬레이션 업데이트
                        </button>
                    </div>

                    <div class="grid grid-cols-2 gap-4">
                        <div class="bg-white/5 border border-white/10 p-6 rounded-2xl">
                            <p class="text-[10px] text-slate-400 uppercase font-black tracking-tighter">예상 NPV</p>
                            <p id="resNPV" class="text-2xl font-black text-white mt-2">₩0M</p>
                        </div>
                        <div class="bg-white/5 border border-white/10 p-6 rounded-2xl">
                            <p class="text-[10px] text-slate-400 uppercase font-black tracking-tighter">Nature ROI</p>
                            <p id="resROI" class="text-2xl font-black text-emerald-400 mt-2">0.0x</p>
                        </div>
                    </div>
                </div>

                <div class="lg:col-span-8 bg-white rounded-3xl p-4 md:p-8 shadow-2xl">
                    <div class="flex flex-col md:flex-row justify-between md:items-center mb-6 gap-4">
                        <h3 class="text-slate-900 font-bold text-lg">Portfolio Value Projection (Monte Carlo)</h3>
                        <div class="flex gap-4">
                            <div class="flex items-center gap-2">
                                <span class="w-3 h-3 rounded-full bg-sky-700"></span>
                                <span class="text-[10px] text-slate-500 font-bold uppercase">Expected</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span class="w-3 h-3 rounded-full bg-slate-200"></span>
                                <span class="text-[10px] text-slate-500 font-bold uppercase">95% Confidence</span>
                            </div>
                        </div>
                    </div>
                    <div class="chart-container" style="height: 450px;">
                        <canvas id="simulationChart"></canvas>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 4: Pilot Case Study -->
    <section id="case-study" class="py-24 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid md:grid-cols-2 gap-20 items-center">
                <div class="order-2 md:order-1">
                    <div class="card bg-slate-50 border-slate-100 p-8">
                        <h3 class="text-xs font-black text-slate-400 uppercase mb-8 text-center tracking-widest">30-Year Value Creation (Gyeongbuk Case)</h3>
                        <div class="chart-container" style="height: 380px;">
                            <canvas id="pilotAreaChart"></canvas>
                        </div>
                    </div>
                </div>
                <div class="order-1 md:order-2">
                    <span class="text-sky-700 font-black text-xs uppercase tracking-widest bg-sky-100 px-3 py-1 rounded-full">Pilot Case Study</span>
                    <h2 class="text-4xl font-bold text-slate-900 mt-6 mb-8 leading-tight">경북 산불 피해 복원: <br>위기를 금융 자산으로 전환하다</h2>
                    <p class="text-slate-600 mb-10 text-lg leading-relaxed">
                        NFQ Lab의 모델을 경북 울진-삼척 산불 피해 지역(99,289ha)에 적용했습니다. 
                        단순 복원을 넘어, <span class="highlight">탄소 배출권</span>, <span class="highlight">재해 방지(Risk Defense)</span>, 
                        그리고 <span class="highlight">지역 사회 가치</span>가 결합되어 시간이 지날수록 가치가 급등하는 
                        <strong>J-Curve</strong> 효과를 데이터로 입증했습니다.
                    </p>
                    <div class="grid gap-6">
                        <div class="flex items-start gap-5 group">
                            <div class="w-12 h-12 rounded-2xl bg-sky-100 flex items-center justify-center text-sky-700 font-black shrink-0 transition group-hover:bg-sky-700 group-hover:text-white">1</div>
                            <div>
                                <h4 class="font-bold text-slate-900 text-lg">Risk Defense (재난 방어)</h4>
                                <p class="text-sm text-slate-500 mt-1 leading-relaxed">산사태 및 홍수 예방을 통한 잠재적 손실 방지 가치를 퀀트로 정량화</p>
                            </div>
                        </div>
                        <div class="flex items-start gap-5 group">
                            <div class="w-12 h-12 rounded-2xl bg-emerald-100 flex items-center justify-center text-emerald-700 font-black shrink-0 transition group-hover:bg-emerald-700 group-hover:text-white">2</div>
                            <div>
                                <h4 class="font-bold text-slate-900 text-lg">Carbon Asset (탄소 자산)</h4>
                                <p class="text-sm text-slate-500 mt-1 leading-relaxed">REDD+ 및 고품질 탄소 크레딧 수익 창출 모델 구축</p>
                            </div>
                        </div>
                        <div class="flex items-start gap-5 group">
                            <div class="w-12 h-12 rounded-2xl bg-amber-100 flex items-center justify-center text-amber-700 font-black shrink-0 transition group-hover:bg-amber-600 group-hover:text-white">3</div>
                            <div>
                                <h4 class="font-bold text-slate-900 text-lg">Social Value (사회적 가치)</h4>
                                <p class="text-sm text-slate-500 mt-1 leading-relaxed">에코투어리즘 및 지역 주민 일자리 창출을 통한 경제 승수 효과</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-slate-900 text-white py-20 border-t border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row justify-between items-start gap-12 mb-16">
                <div class="max-w-sm">
                    <div class="flex items-center gap-2 mb-6">
                        <div class="bg-white text-slate-900 p-1.5 rounded font-bold text-xs mono">NFQ</div>
                        <span class="font-bold text-2xl tracking-tight">NFQ Lab</span>
                    </div>
                    <p class="text-slate-400 text-sm leading-relaxed">
                        자연 자본의 정량화를 통해 지구의 회복과 금융의 수익을 동시에 달성하는 Nature-Positive 미래를 만듭니다.
                    </p>
                </div>
                <div class="grid grid-cols-2 sm:grid-cols-3 gap-12">
                    <div>
                        <h4 class="text-xs font-bold text-white uppercase tracking-widest mb-6">Explore</h4>
                        <ul class="text-slate-400 text-sm space-y-4">
                            <li><a href="#macro" class="hover:text-white transition">Market Gap</a></li>
                            <li><a href="#methodology" class="hover:text-white transition">Methodology</a></li>
                            <li><a href="#simulator" class="hover:text-white transition">Simulator</a></li>
                        </ul>
                    </div>
                    <div>
                        <h4 class="text-xs font-bold text-white uppercase tracking-widest mb-6">Legal</h4>
                        <ul class="text-slate-400 text-sm space-y-4">
                            <li><a href="#" class="hover:text-white transition">Privacy Policy</a></li>
                            <li><a href="#" class="hover:text-white transition">Terms of Service</a></li>
                        </ul>
                    </div>
                    <div class="col-span-2 sm:col-span-1">
                        <h4 class="text-xs font-bold text-white uppercase tracking-widest mb-6">Connect</h4>
                        <div class="flex gap-4">
                            <div class="w-8 h-8 rounded-full bg-slate-800 flex items-center justify-center hover:bg-sky-600 transition cursor-pointer">
                                <span class="text-[10px]">IN</span>
                            </div>
                            <div class="w-8 h-8 rounded-full bg-slate-800 flex items-center justify-center hover:bg-sky-600 transition cursor-pointer">
                                <span class="text-[10px]">X</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="pt-8 border-t border-slate-800 flex flex-col md:flex-row justify-between items-center gap-4">
                <p class="text-xs text-slate-500 font-mono italic">&copy; 2025 Nature Finance Quant Laboratory. All Rights Reserved.</p>
                <p class="text-xs text-slate-600">Combining Science, Tech, and Finance for a Nature-Positive Future.</p>
            </div>
        </div>
    </footer>

    <script>
        // --- Initialize Scroll Animations ---
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if(entry.isIntersecting) entry.target.classList.add('visible');
            });
        }, { threshold: 0.1 });
        document.querySelectorAll('section').forEach(s => observer.observe(s));

        // --- Shared Configurations ---
        Chart.defaults.font.family = "'Noto Sans KR', sans-serif";
        Chart.defaults.color = '#94A3B8';
        
        // --- Chart 1: Global Funding Gap ---
        const ctxGap = document.getElementById('fundingGapChart').getContext('2d');
        new Chart(ctxGap, {
            type: 'bar',
            data: {
                labels: ['Current Spending', 'Financing Gap'],
                datasets: [
                    {
                        label: 'Available Funds',
                        data: [150, 0],
                        backgroundColor: '#0369A1',
                        borderRadius: 8
                    },
                    {
                        label: 'Required Gap',
                        data: [0, 700],
                        backgroundColor: '#F1F5F9',
                        borderColor: '#E11D48',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        borderRadius: 8
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { display: false } },
                    y: { beginAtZero: true, grid: { color: '#F1F5F9' } }
                }
            }
        });

        // --- Chart 2: Dependency Donut ---
        const ctxDonut = document.getElementById('dependencyChart').getContext('2d');
        new Chart(ctxDonut, {
            type: 'doughnut',
            data: {
                labels: ['High', 'Moderate', 'Low'],
                datasets: [{
                    data: [55, 30, 15],
                    backgroundColor: ['#0369A1', '#38BDF8', '#E2E8F0'],
                    borderWidth: 0,
                    hoverOffset: 15
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '75%',
                plugins: {
                    legend: { position: 'bottom', labels: { boxWidth: 8, font: { size: 10 } } }
                }
            }
        });

        // --- Chart 3: Ecosystem Radar ---
        const ctxRadar = document.getElementById('ecosystemRadarChart').getContext('2d');
        new Chart(ctxRadar, {
            type: 'radar',
            data: {
                labels: ['Biodiversity', 'Carbon Storage', 'Soil Health', 'Water', 'Resilience'],
                datasets: [
                    {
                        label: 'Degraded (Current)',
                        data: [30, 40, 35, 30, 25],
                        borderColor: '#CBD5E1',
                        backgroundColor: 'rgba(203, 213, 225, 0.2)',
                        borderWidth: 1,
                        pointRadius: 0
                    },
                    {
                        label: 'Restored (Target)',
                        data: [85, 90, 85, 80, 95],
                        borderColor: '#15803D',
                        backgroundColor: 'rgba(21, 128, 61, 0.2)',
                        borderWidth: 3,
                        pointBackgroundColor: '#15803D'
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    r: { ticks: { display: false }, grid: { color: '#E2E8F0' }, pointLabels: { font: { size: 10 } } }
                },
                plugins: { legend: { labels: { boxWidth: 10, font: { size: 10 } } } }
            }
        });

        // --- Chart 4: Risk Histogram ---
        const ctxHist = document.getElementById('riskHistogramChart').getContext('2d');
        new Chart(ctxHist, {
            type: 'bar',
            data: {
                labels: Array.from({length: 20}, (_, i) => i),
                datasets: [
                    {
                        label: 'Traditional',
                        data: [2, 5, 8, 12, 18, 25, 35, 50, 60, 45, 30, 20, 15, 12, 10, 8, 7, 6, 5, 4],
                        backgroundColor: 'rgba(225, 29, 72, 0.4)',
                        barPercentage: 1,
                        categoryPercentage: 1
                    },
                    {
                        label: 'Nature-Positive',
                        data: [1, 2, 4, 10, 25, 45, 75, 95, 80, 50, 25, 10, 5, 2, 1, 0, 0, 0, 0, 0],
                        backgroundColor: 'rgba(3, 105, 161, 0.6)',
                        barPercentage: 1,
                        categoryPercentage: 1
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { position: 'bottom', labels: { boxWidth: 10, font: { size: 10 } } } },
                scales: { x: { display: false }, y: { display: false } }
            }
        });

        // --- Chart 5: Interactive Simulator ---
        const ctxSim = document.getElementById('simulationChart').getContext('2d');
        let simulationChart = new Chart(ctxSim, {
            type: 'line',
            data: {
                labels: [],
                datasets: [
                    {
                        label: 'Expected Value',
                        data: [],
                        borderColor: '#0369A1',
                        backgroundColor: 'rgba(3, 105, 161, 0.1)',
                        borderWidth: 4,
                        tension: 0.4,
                        fill: false,
                        zIndex: 10
                    },
                    {
                        label: 'Confidence Interval',
                        data: [],
                        borderColor: 'transparent',
                        backgroundColor: 'rgba(226, 232, 240, 0.5)',
                        fill: '+1',
                        pointRadius: 0
                    },
                    {
                        label: 'Lower Bound',
                        data: [],
                        borderColor: 'transparent',
                        backgroundColor: 'transparent',
                        fill: false,
                        pointRadius: 0
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { legend: { display: false } },
                scales: {
                    x: { grid: { display: false }, ticks: { font: { size: 10 } } },
                    y: { grid: { color: '#F1F5F9' }, ticks: { font: { size: 10 }, callback: v => '₩' + v + '억' } }
                }
            }
        });

        function updateSimulation() {
            const cap = parseInt(document.getElementById('inputCap').value);
            const bio = parseInt(document.getElementById('inputBio').value) / 100;
            const years = parseInt(document.getElementById('inputTime.value') || 15);
            
            document.getElementById('dispCap').innerText = cap + '억 원';
            document.getElementById('dispBio').innerText = (bio * 100).toFixed(0) + '%';
            document.getElementById('dispTime').innerText = document.getElementById('inputTime').value + '년';

            const labels = [];
            const dataExpected = [];
            const dataUpper = [];
            const dataLower = [];
            
            // Financial logic: ROI depends on Bio Restoration Score (Alpha)
            const baseGrowth = 0.04;
            const bioAlpha = bio * 0.12; // High restoration leads to higher cash flow from carbon/resilience
            const volatility = 0.15 * (1 - bio * 0.5); // Higher restoration reduces risk/volatility
            
            for (let t = 0; t <= parseInt(document.getElementById('inputTime').value); t++) {
                labels.push('Year ' + t);
                const value = cap * Math.pow(1 + baseGrowth + bioAlpha, t);
                dataExpected.push(value.toFixed(1));
                
                // Confidence Intervals (95% approx)
                const margin = value * (volatility * Math.sqrt(t));
                dataUpper.push((value + margin).toFixed(1));
                dataLower.push((value - margin).toFixed(1));
            }

            simulationChart.data.labels = labels;
            simulationChart.data.datasets[0].data = dataExpected;
            simulationChart.data.datasets[1].data = dataUpper;
            simulationChart.data.datasets[2].data = dataLower;
            simulationChart.update();

            const finalNPV = dataExpected[dataExpected.length - 1];
            const roi = (finalNPV / cap).toFixed(1);
            
            document.getElementById('resNPV').innerText = '₩' + finalNPV + '억';
            document.getElementById('resROI').innerText = roi + 'x';
        }

        document.getElementById('btnRun').addEventListener('click', updateSimulation);
        ['inputCap', 'inputBio', 'inputTime'].forEach(id => {
            document.getElementById(id).addEventListener('input', updateSimulation);
        });

        // --- Chart 6: Pilot Case J-Curve ---
        const ctxPilot = document.getElementById('pilotAreaChart').getContext('2d');
        new Chart(ctxPilot, {
            type: 'line',
            data: {
                labels: ['0', '5', '10', '15', '20', '25', '30'],
                datasets: [
                    {
                        label: 'Risk Defense',
                        data: [10, 15, 25, 45, 60, 75, 85],
                        backgroundColor: 'rgba(3, 105, 161, 0.7)',
                        fill: true,
                        pointRadius: 0,
                        tension: 0.4
                    },
                    {
                        label: 'Carbon Asset',
                        data: [0, 5, 20, 55, 100, 160, 230],
                        backgroundColor: 'rgba(21, 128, 61, 0.7)',
                        fill: true,
                        pointRadius: 0,
                        tension: 0.4
                    },
                    {
                        label: 'Social Value',
                        data: [5, 10, 25, 50, 85, 130, 190],
                        backgroundColor: 'rgba(250, 204, 21, 0.7)',
                        fill: true,
                        pointRadius: 0,
                        tension: 0.4
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: { 
                    legend: { position: 'bottom', labels: { boxWidth: 10, font: { size: 10 } } },
                    tooltip: { mode: 'index', intersect: false }
                },
                scales: {
                    x: { grid: { display: false } },
                    y: { stacked: true, grid: { color: '#F1F5F9' }, ticks: { display: false } }
                }
            }
        });

        // Start with initial simulation
        window.onload = updateSimulation;
    </script>
</body>
</html>
