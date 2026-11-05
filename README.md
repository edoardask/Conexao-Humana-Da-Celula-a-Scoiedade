# Conexao-Humana-Da-Celula-a-Scoiedade
Trabalho de Culminância Eletiva - Conexão Humana: Da célula à sociedade
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Detetive da Saúde — Descubra a Doença!</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Courier+Prime:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;500;600;700;800&family=Outfit:wght@400;600;700;800;900&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        heading: ['Outfit', 'sans-serif'],
                        mono: ['Courier Prime', 'monospace']
                    },
                    colors: {
                        mahogany: '#1c100b',
                        clipboard: '#8c532b',
                        paper: '#fcfbf7',
                        paperBorder: '#e2d9c8',
                        tealMed: '#0d9488',
                        crimsonMed: '#e11d48'
                    }
                }
            }
        }
    </script>

    <style>
        /* Realistic Dark Mahogany Wood Background */
        .desk-bg {
            background-color: #1a0e09;
            background-image: 
                radial-gradient(circle at 50% 20%, rgba(217, 119, 6, 0.12) 0%, transparent 60%),
                linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)),
                repeating-linear-gradient(0deg, transparent, transparent 4px, rgba(0,0,0,0.25) 4px, rgba(0,0,0,0.25) 8px);
        }

        /* Medical Paper Clip & Texture */
        .paper-shadow {
            box-shadow: 
                0 15px 35px -5px rgba(0, 0, 0, 0.65),
                0 0 0 1px rgba(0, 0, 0, 0.15),
                inset 0 0 50px rgba(190, 170, 130, 0.2);
        }

        .clipboard-clip {
            background: linear-gradient(180deg, #d1d5db 0%, #6b7280 40%, #374151 100%);
            box-shadow: 0 6px 14px rgba(0,0,0,0.6), inset 0 1px 2px rgba(255,255,255,0.8);
        }

        /* Custom Scrollbar for Clinical Sheet */
        .custom-scroll::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scroll::-webkit-scrollbar-track {
            background: #f1ede4;
            border-radius: 4px;
        }
        .custom-scroll::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        .custom-scroll::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }

        /* Stamp Effects */
        .stamp-approved {
            border: 3px double #16a34a;
            color: #16a34a;
            transform: rotate(-14deg);
            opacity: 0.85;
            font-family: 'Courier Prime', monospace;
            text-shadow: 0 0 2px rgba(22, 163, 74, 0.3);
        }
        .stamp-rejected {
            border: 3px double #e11d48;
            color: #e11d48;
            transform: rotate(10deg);
            opacity: 0.85;
            font-family: 'Courier Prime', monospace;
        }

        /* Animated Pulse Glow */
        @keyframes subtle-pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.96; transform: scale(1.008); }
        }
        .animate-subtle-pulse {
            animation: subtle-pulse 2s infinite ease-in-out;
        }
    </style>
</head>
<body class="desk-bg text-slate-100 min-h-screen font-sans antialiased flex flex-col justify-between selection:bg-teal-500 selection:text-white">

    <!-- HEADER / NAVIGATION BAR -->
    <header class="bg-slate-950/90 backdrop-blur border-b border-slate-800 sticky top-0 z-40 px-4 py-3 shadow-xl">
        <div class="max-w-6xl mx-auto flex flex-wrap items-center justify-between gap-3">
            <!-- Brand / Logo -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="goHome()">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-teal-600 via-emerald-600 to-sky-500 flex items-center justify-center text-white shadow-lg shadow-teal-500/20">
                    <i class="fa-solid fa-user-doctor text-xl"></i>
                </div>
                <div>
                    <h1 class="font-heading font-extrabold text-lg sm:text-xl tracking-tight text-white flex items-center gap-2">
                        Detetive da Saúde
                        <span class="text-[10px] font-bold uppercase tracking-wider bg-teal-500/20 text-teal-300 border border-teal-500/30 px-2 py-0.5 rounded-full hidden sm:inline-block">Investigação Médica</span>
                    </h1>
                    <p class="text-xs text-slate-400 hidden sm:block">Análise de Prontuários & Diagnóstico Diferencial</p>
                </div>
            </div>

            <!-- Game Live Stats (Visible when playing) -->
            <div id="header-stats" class="hidden flex items-center space-x-3 sm:space-x-4 bg-slate-900/90 px-4 py-1.5 rounded-full border border-slate-800 text-xs sm:text-sm shadow-inner">
                <div class="flex items-center space-x-1.5" title="Detetive Responsável">
                    <i class="fa-solid fa-user-ninja text-teal-400"></i>
                    <span id="stat-player-name" class="font-bold text-slate-200">Dr. Investigador</span>
                </div>
                <div class="h-4 w-px bg-slate-800"></div>
                <div class="flex items-center space-x-1.5" title="Pontuação">
                    <i class="fa-solid fa-trophy text-amber-400"></i>
                    <span id="stat-score" class="font-bold text-amber-400">0 pts</span>
                </div>
                <div class="h-4 w-px bg-slate-800"></div>
                <div class="flex items-center space-x-1.5" title="Multiplicador de Combo">
                    <i class="fa-solid fa-bolt text-emerald-400"></i>
                    <span id="stat-streak" class="font-bold text-emerald-400">1x</span>
                </div>
                <div id="stat-timer-container" class="hidden flex items-center space-x-1.5 text-rose-400 font-mono font-bold animate-pulse">
                    <i class="fa-solid fa-stopwatch"></i>
                    <span id="stat-timer">45s</span>
                </div>
            </div>

            <!-- Controls (Sound & Ranking) -->
            <div class="flex items-center space-x-2">
                <button id="btn-audio-toggle" onclick="toggleAudio()" class="w-9 h-9 rounded-lg bg-slate-900 hover:bg-slate-800 border border-slate-800 text-slate-300 flex items-center justify-center transition" title="Alternar Som">
                    <i id="audio-icon" class="fa-solid fa-volume-high"></i>
                </button>
                <button onclick="openLeaderboard()" class="px-3 py-1.5 rounded-lg bg-amber-500/10 hover:bg-amber-500/20 border border-amber-500/30 text-amber-300 text-xs sm:text-sm font-bold flex items-center gap-1.5 transition">
                    <i class="fa-solid fa-award text-amber-400"></i>
                    <span>Ranking</span>
                </button>
            </div>
        </div>
    </header>

    <!-- MAIN INTERACTIVE WORKSPACE -->
    <main class="flex-grow max-w-5xl w-full mx-auto p-3 sm:p-6 flex flex-col justify-center">

        <!-- SCREEN 1: START MENU & REGISTRATION -->
        <section id="screen-start" class="w-full max-w-2xl mx-auto bg-slate-950/90 border border-slate-800/90 rounded-3xl p-6 sm:p-10 shadow-2xl backdrop-blur-md">
            <div class="text-center mb-8">
                <div class="inline-flex items-center justify-center w-20 h-20 rounded-3xl bg-gradient-to-br from-teal-500 via-emerald-600 to-sky-600 text-white shadow-xl shadow-teal-500/25 mb-4 ring-8 ring-slate-900">
                    <i class="fa-solid fa-stethoscope text-4xl"></i>
                </div>
                <h2 class="font-heading text-3xl sm:text-4xl font-black text-white mb-2">Detetive da Saúde</h2>
                <p class="text-slate-400 text-sm sm:text-base max-w-md mx-auto">
                    Analise os sintomas, históricos epidemiológicos e exames de cada paciente para desvendar os mistérios diagnósticos!
                </p>
            </div>

            <form onsubmit="startGame(event)" class="space-y-6">
                <!-- Player Name Input -->
                <div>
                    <label for="input-player-name" class="block text-xs font-bold uppercase tracking-wider text-slate-300 mb-2">
                        <i class="fa-solid fa-id-card text-teal-400 mr-1.5"></i> Identificação do Investigador
                    </label>
                    <input type="text" id="input-player-name" required maxlength="24" placeholder="Ex: Dra. Beatriz, Dr. House..." class="w-full bg-slate-900 border border-slate-700 focus:border-teal-500 focus:ring-2 focus:ring-teal-500/30 rounded-xl px-4 py-3 text-white placeholder-slate-500 outline-none transition font-medium">
                </div>

                <!-- Game Mode Selection -->
                <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-300 mb-2">
                        <i class="fa-solid fa-sliders text-emerald-400 mr-1.5"></i> Modo de Investigação
                    </label>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                        <label class="relative flex flex-col p-4 bg-slate-900 border border-slate-800 hover:border-teal-500/50 rounded-2xl cursor-pointer transition has-[:checked]:border-teal-500 has-[:checked]:bg-teal-950/20">
                            <input type="radio" name="game-mode" value="standard" checked class="sr-only">
                            <div class="flex items-center justify-between mb-1">
                                <span class="font-bold text-sm text-white">Casos Clínicos</span>
                                <i class="fa-solid fa-briefcase-medical text-teal-400"></i>
                            </div>
                            <span class="text-xs text-slate-400">Progressão completa por todos os 10 prontuários.</span>
                        </label>

                        <label class="relative flex flex-col p-4 bg-slate-900 border border-slate-800 hover:border-amber-500/50 rounded-2xl cursor-pointer transition has-[:checked]:border-amber-500 has-[:checked]:bg-amber-950/20">
                            <input type="radio" name="game-mode" value="timed" class="sr-only">
                            <div class="flex items-center justify-between mb-1">
                                <span class="font-bold text-sm text-white">Emergência (Tempo)</span>
                                <i class="fa-solid fa-stopwatch text-amber-400"></i>
                            </div>
                            <span class="text-xs text-slate-400">45 segundos por diagnóstico. Bônus por rapidez!</span>
                        </label>

                        <label class="relative flex flex-col p-4 bg-slate-900 border border-slate-800 hover:border-purple-500/50 rounded-2xl cursor-pointer transition has-[:checked]:border-purple-500 has-[:checked]:bg-purple-950/20">
                            <input type="radio" name="game-mode" value="random" class="sr-only">
                            <div class="flex items-center justify-between mb-1">
                                <span class="font-bold text-sm text-white">Casos Surpresa</span>
                                <i class="fa-solid fa-dice text-purple-400"></i>
                            </div>
                            <span class="text-xs text-slate-400">Ordem aleatória sem padrão prévio.</span>
                        </label>
                    </div>
                </div>

                <!-- Start Button -->
                <button type="submit" class="w-full bg-gradient-to-r from-teal-600 via-emerald-600 to-sky-600 hover:from-teal-500 hover:to-sky-500 text-white font-heading font-black text-lg py-4 px-6 rounded-2xl shadow-xl shadow-teal-600/25 transition transform active:scale-[0.99] flex items-center justify-center gap-2">
                    <i class="fa-solid fa-microscope text-xl"></i>
                    <span>Iniciar Investigação Médica</span>
                </button>
            </form>
        </section>

        <!-- SCREEN 2: GAMEPLAY WORKSPACE (PHYSICAL CLIPBOARD & DIAGNOSTIC CARD) -->
        <section id="screen-game" class="hidden w-full flex flex-col gap-6 my-auto">
            
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

                <!-- LEFT COLUMN: REALISTIC MEDICAL CLIPBOARD (7 cols) -->
                <div class="lg:col-span-7 relative">
                    <!-- Metallic Clip Decor -->
                    <div class="absolute -top-4 left-1/2 -translate-x-1/2 z-20 w-40 h-10 rounded-t-xl clipboard-clip flex items-center justify-center">
                        <div class="w-14 h-2.5 rounded-full bg-slate-900/70 shadow-inner"></div>
                    </div>

                    <!-- Wood Backing Frame -->
                    <div class="bg-[#5c371d] p-3 sm:p-4 rounded-3xl shadow-2xl border border-amber-900/60">
                        <!-- Medical Paper Document -->
                        <div class="bg-[#fcfbf7] text-slate-900 rounded-2xl p-5 sm:p-8 paper-shadow relative overflow-hidden font-sans border border-[#e2d9c8]">
                            
                            <!-- Confidential Watermark Stamp -->
                            <div class="absolute top-4 right-4 opacity-20 pointer-events-none text-right">
                                <p class="font-mono text-xs uppercase font-extrabold text-slate-900 border-2 border-slate-900 px-2 py-0.5 rounded">CONFIDENCIAL</p>
                                <p class="text-[9px] font-mono mt-0.5">MINISTÉRIO DA SAÚDE</p>
                            </div>

                            <!-- Header: Case ID & Hospital -->
                            <div class="border-b-2 border-slate-300 pb-3 mb-4 flex items-center gap-3">
                                <div class="w-11 h-11 rounded-xl bg-teal-800 text-amber-100 flex items-center justify-center font-bold text-xl shadow-sm">
                                    <i class="fa-solid fa-hospital-user"></i>
                                </div>
                                <div>
                                    <h3 class="font-heading font-black text-slate-900 text-lg sm:text-xl leading-tight uppercase tracking-wide" id="case-id-display">PRONTUÁRIO #001</h3>
                                    <p class="text-xs text-slate-600 font-mono" id="case-category-display">Especialidade: Infectologia</p>
                                </div>
                            </div>

                            <!-- Patient Info Card -->
                            <div class="bg-[#f3ede0] border border-[#e2d7c0] rounded-xl p-3 mb-4 text-xs sm:text-sm grid grid-cols-2 sm:grid-cols-3 gap-2">
                                <div>
                                    <span class="text-slate-500 block text-[10px] uppercase font-bold tracking-wider">Idade</span>
                                    <span class="font-extrabold text-slate-900" id="patient-age">67 anos</span>
                                </div>
                                <div>
                                    <span class="text-slate-500 block text-[10px] uppercase font-bold tracking-wider">Sexo</span>
                                    <span class="font-extrabold text-slate-900" id="patient-sex">Masculino</span>
                                </div>
                                <div class="col-span-2 sm:col-span-1">
                                    <span class="text-slate-500 block text-[10px] uppercase font-bold tracking-wider">Admissão</span>
                                    <span class="font-semibold text-slate-800">Pronto Atendimento</span>
                                </div>
                            </div>

                            <!-- Patient Anamnesis / History -->
                            <div class="space-y-4 text-sm custom-scroll max-h-[390px] overflow-y-auto pr-1">
                                
                                <div>
                                    <h4 class="font-heading font-bold text-xs uppercase tracking-wider text-slate-700 flex items-center gap-1.5 mb-1.5">
                                        <i class="fa-solid fa-file-waveform text-teal-700"></i> Queixa Principal & História Clínica
                                    </h4>
                                    <p class="text-slate-800 bg-white/70 p-3 rounded-xl border border-slate-200/90 leading-relaxed font-sans text-sm sm:text-base" id="patient-history">
                                        <!-- Case description injected -->
                                    </p>
                                </div>

                                <!-- Vitals Display -->
                                <div>
                                    <h4 class="font-heading font-bold text-xs uppercase tracking-wider text-slate-700 flex items-center gap-1.5 mb-1.5">
                                        <i class="fa-solid fa-heart-pulse text-rose-600"></i> Sinais Vitais no Atendimento
                                    </h4>
                                    <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 text-center" id="vitals-grid">
                                        <!-- Vitals injected -->
                                    </div>
                                </div>

                                <!-- Physical Exam & Lab Findings -->
                                <div>
                                    <h4 class="font-heading font-bold text-xs uppercase tracking-wider text-slate-700 flex items-center gap-1.5 mb-1.5">
                                        <i class="fa-solid fa-vial-virus text-amber-700"></i> Achados do Exame Físico & Exames
                                    </h4>
                                    <div class="bg-amber-50/70 border border-amber-200/90 rounded-xl p-3 text-slate-900 text-xs sm:text-sm space-y-1.5 font-mono" id="patient-labs">
                                        <!-- Labs injected -->
                                    </div>
                                </div>

                                <!-- Extra Hint Box (Hidden until requested) -->
                                <div id="hint-box" class="hidden bg-sky-50 border-2 border-dashed border-sky-300 rounded-xl p-3.5 transition animate-fadeIn">
                                    <div class="flex items-center gap-2 text-sky-900 font-bold text-xs uppercase mb-1">
                                        <i class="fa-solid fa-lightbulb text-amber-500 text-sm"></i> Pista Especialista Desbloqueada
                                    </div>
                                    <p class="text-xs sm:text-sm text-sky-950 font-semibold italic" id="hint-text">
                                        Dica...
                                    </p>
                                </div>

                            </div>

                        </div>
                    </div>
                </div>

                <!-- RIGHT COLUMN: DIAGNOSTIC DECISION PANEL (5 cols) -->
                <div class="lg:col-span-5 space-y-4">

                    <!-- Diagnostic Choice Card -->
                    <div class="bg-slate-950/95 border border-slate-800 rounded-3xl p-5 sm:p-6 shadow-2xl">
                        
                        <div class="flex items-center justify-between mb-4 pb-3 border-b border-slate-800">
                            <div>
                                <span class="text-xs font-bold uppercase tracking-widest text-teal-400">Hipótese Médica</span>
                                <h3 class="font-heading font-black text-lg text-white">Qual é o diagnóstico mais provável?</h3>
                            </div>
                            <span class="w-8 h-8 rounded-full bg-teal-500/10 border border-teal-500/30 text-teal-400 flex items-center justify-center font-bold text-sm">
                                ?
                            </span>
                        </div>

                        <!-- 4 Diagnosis Options -->
                        <div class="space-y-2.5" id="options-container">
                            <!-- Options injected -->
                        </div>

                        <!-- Action Controls -->
                        <div class="mt-6 space-y-3">
                            <button id="btn-submit-diagnosis" disabled onclick="submitDiagnosis()" class="w-full bg-slate-800 text-slate-500 cursor-not-allowed font-heading font-black text-base py-4 px-4 rounded-xl shadow-lg transition flex items-center justify-center gap-2">
                                <i class="fa-solid fa-clipboard-check"></i>
                                <span>Confirmar Diagnóstico</span>
                            </button>

                            <button id="btn-request-hint" onclick="requestHint()" class="w-full bg-slate-900 hover:bg-slate-800 text-amber-300 hover:text-amber-200 border border-amber-500/30 font-bold text-xs py-2.5 px-4 rounded-xl transition flex items-center justify-center gap-2">
                                <i class="fa-solid fa-lightbulb text-amber-400"></i>
                                <span>Pedir Dica Extra (-15 Pontos)</span>
                            </button>
                        </div>

                    </div>

                    <!-- Clinical Tip Footer Card -->
                    <div class="bg-slate-950/70 border border-slate-800/80 rounded-2xl p-4 text-xs text-slate-400 flex items-start gap-3">
                        <i class="fa-solid fa-stethoscope text-teal-400 text-base mt-0.5"></i>
                        <div>
                            <p class="font-bold text-slate-300 mb-0.5">Raciocínio Clínico:</p>
                            <p>Correlacione o histórico epidemiológico do paciente com as alterações físicas marcantes para diferenciar síndromes febris graves.</p>
                        </div>
                    </div>

                </div>

            </div>

        </section>

        <!-- SCREEN 3: CLINICAL EXPLANATION & DIFFERENTIAL RATIONALE -->
        <section id="screen-explanation" class="hidden w-full max-w-3xl mx-auto bg-slate-950/95 border border-slate-800/90 rounded-3xl p-6 sm:p-8 shadow-2xl backdrop-blur-md my-auto">
            
            <!-- Result Banner (Success / Error) -->
            <div id="explanation-banner" class="rounded-2xl p-4 sm:p-5 mb-6 flex items-center justify-between">
                <div class="flex items-center gap-3.5">
                    <div id="explanation-icon-container" class="w-12 h-12 rounded-2xl flex items-center justify-center text-2xl font-bold shadow-md">
                        <!-- Icon injected -->
                    </div>
                    <div>
                        <h3 id="explanation-title" class="font-heading text-xl sm:text-2xl font-black">Diagnóstico Correto!</h3>
                        <p id="explanation-subtitle" class="text-xs sm:text-sm opacity-90">Sua análise clínica foi cirúrgica e precisa.</p>
                    </div>
                </div>
                <div id="explanation-points-badge" class="font-heading font-black text-lg sm:text-xl px-4 py-2 rounded-xl border bg-black/20 shadow-inner">
                    +100 pts
                </div>
            </div>

            <!-- Pathophysiology & Differential Breakdown -->
            <div class="space-y-4 text-sm">
                
                <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5">
                    <h4 class="font-heading font-bold text-teal-400 text-xs sm:text-sm uppercase tracking-wider mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-microscope text-teal-400"></i> Fisiopatologia & Quadro Clínico
                    </h4>
                    <p id="explanation-text" class="text-slate-300 leading-relaxed font-sans text-sm sm:text-base">
                        <!-- Explanation text injected -->
                    </p>
                </div>

                <!-- Differential Analysis List -->
                <div class="bg-slate-900 border border-slate-800 rounded-2xl p-4 sm:p-5">
                    <h4 class="font-heading font-bold text-amber-400 text-xs sm:text-sm uppercase tracking-wider mb-3 flex items-center gap-2">
                        <i class="fa-solid fa-scale-balanced text-amber-400"></i> Diagnóstico Diferencial
                    </h4>
                    <ul id="differential-list" class="space-y-2.5 text-xs sm:text-sm text-slate-300">
                        <!-- Differential injected -->
                    </ul>
                </div>

            </div>

            <!-- Next Case Button -->
            <div class="mt-6 flex justify-end">
                <button onclick="nextCase()" class="w-full sm:w-auto bg-gradient-to-r from-teal-600 to-emerald-600 hover:from-teal-500 hover:to-emerald-500 text-white font-heading font-black text-base px-8 py-3.5 rounded-xl shadow-lg transition flex items-center justify-center gap-2">
                    <span>Avançar para Próximo Caso</span>
                    <i class="fa-solid fa-arrow-right"></i>
                </button>
            </div>

        </section>

        <!-- SCREEN 4: GAME OVER & SUMMARY -->
        <section id="screen-gameover" class="hidden w-full max-w-2xl mx-auto bg-slate-950/95 border border-slate-800/90 rounded-3xl p-6 sm:p-10 shadow-2xl text-center my-auto">
            
            <div class="relative inline-block mb-4">
                <div class="w-24 h-24 rounded-3xl bg-gradient-to-br from-amber-400 via-amber-500 to-amber-700 text-slate-950 flex items-center justify-center text-5xl font-black shadow-xl shadow-amber-500/25 ring-8 ring-slate-900">
                    <i id="summary-rank-icon" class="fa-solid fa-award"></i>
                </div>
            </div>

            <h2 class="font-heading text-3xl sm:text-4xl font-black text-white mb-1">Investigação Concluída!</h2>
            <p id="summary-rank-title" class="text-amber-400 font-heading font-bold text-lg mb-6">Título: Médico Especialista Infectologista</p>

            <!-- Stats Overview -->
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 mb-8 text-left">
                <div class="bg-slate-900 border border-slate-800 p-4 rounded-2xl">
                    <span class="text-xs text-slate-400 block font-bold">Pontuação Final</span>
                    <span id="summary-score" class="font-heading font-black text-2xl text-amber-400">0 pts</span>
                </div>
                <div class="bg-slate-900 border border-slate-800 p-4 rounded-2xl">
                    <span class="text-xs text-slate-400 block font-bold">Diagnósticos Certos</span>
                    <span id="summary-accuracy" class="font-heading font-black text-2xl text-emerald-400">0 / 0</span>
                </div>
                <div class="bg-slate-900 border border-slate-800 p-4 rounded-2xl">
                    <span class="text-xs text-slate-400 block font-bold">Taxa de Precisão</span>
                    <span id="summary-percentage" class="font-heading font-black text-2xl text-teal-400">0%</span>
                </div>
                <div class="bg-slate-900 border border-slate-800 p-4 rounded-2xl">
                    <span class="text-xs text-slate-400 block font-bold">Dicas Utilizadas</span>
                    <span id="summary-hints" class="font-heading font-black text-2xl text-purple-400">0</span>
                </div>
            </div>

            <!-- Buttons -->
            <div class="flex flex-col sm:flex-row gap-3">
                <button onclick="goHome()" class="flex-1 bg-slate-800 hover:bg-slate-700 text-slate-200 font-heading font-bold py-3.5 px-5 rounded-xl transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-rotate-right"></i>
                    <span>Menu Principal</span>
                </button>
                <button onclick="openLeaderboard()" class="flex-1 bg-gradient-to-r from-amber-500 to-amber-600 hover:from-amber-400 hover:to-amber-500 text-slate-950 font-heading font-black py-3.5 px-5 rounded-xl shadow-lg transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-trophy"></i>
                    <span>Ver Ranking Global</span>
                </button>
            </div>

        </section>

    </main>

    <!-- LEADERBOARD MODAL -->
    <div id="modal-leaderboard" class="hidden fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-slate-950 border border-slate-800 w-full max-w-xl rounded-3xl p-6 shadow-2xl relative">
            <button onclick="closeLeaderboard()" class="absolute top-4 right-4 text-slate-400 hover:text-white text-xl w-8 h-8 rounded-xl bg-slate-900 flex items-center justify-center">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <div class="flex items-center gap-3 mb-6">
                <div class="w-10 h-10 rounded-xl bg-amber-500/10 border border-amber-500/30 text-amber-400 flex items-center justify-center font-bold text-xl">
                    <i class="fa-solid fa-trophy"></i>
                </div>
                <div>
                    <h3 class="font-heading font-black text-xl text-white">Ranking dos Detetives Médicos</h3>
                    <p class="text-xs text-slate-400">Melhores pontuações registradas neste navegador</p>
                </div>
            </div>

            <!-- Leaderboard Table -->
            <div class="max-h-80 overflow-y-auto custom-scroll border border-slate-800 rounded-2xl">
                <table class="w-full text-left text-xs sm:text-sm">
                    <thead class="bg-slate-900 text-slate-400 font-semibold uppercase text-[10px] tracking-wider sticky top-0">
                        <tr>
                            <th class="p-3">#</th>
                            <th class="p-3">Detetive</th>
                            <th class="p-3">Modo</th>
                            <th class="p-3 text-right">Pontuação</th>
                        </tr>
                    </thead>
                    <tbody id="leaderboard-body" class="divide-y divide-slate-800/60 text-slate-300">
                        <!-- Injected by JS -->
                    </tbody>
                </table>
            </div>

            <div class="mt-5 flex items-center justify-between">
                <button onclick="clearLeaderboard()" class="text-xs text-rose-400 hover:text-rose-300 flex items-center gap-1 font-semibold">
                    <i class="fa-solid fa-trash"></i> Resetar Histórico
                </button>
                <button onclick="closeLeaderboard()" class="bg-slate-800 hover:bg-slate-700 text-white font-bold text-xs px-5 py-2.5 rounded-xl">
                    Fechar
                </button>
            </div>
        </div>
    </div>

    <!-- AUDIO GENERATOR & GAME SYSTEM JAVASCRIPT -->
    <script>
        /* ==========================================================================
           1. WEB AUDIO API SYNTHESIZER (NO BROKEN EXTERNAL MP3s)
           ========================================================================== */
        class MedicalSoundEngine {
            constructor() {
                this.ctx = null;
                this.enabled = true;
            }

            init() {
                if (!this.ctx) {
                    const AudioCtx = window.AudioContext || window.webkitAudioContext;
                    if (AudioCtx) this.ctx = new AudioCtx();
                }
                if (this.ctx && this.ctx.state === 'suspended') {
                    this.ctx.resume();
                }
            }

            playTone(freq, type = 'sine', duration = 0.15, gainVal = 0.1) {
                if (!this.enabled) return;
                this.init();
                if (!this.ctx) return;

                try {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = type;
                    osc.frequency.setValueAtTime(freq, this.ctx.currentTime);
                    gain.gain.setValueAtTime(gainVal, this.ctx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.0001, this.ctx.currentTime + duration);

                    osc.connect(gain);
                    gain.connect(this.ctx.destination);

                    osc.start();
                    osc.stop(this.ctx.currentTime + duration);
                } catch(e) {
                    console.log('Audio error:', e);
                }
            }

            playClick() {
                this.playTone(650, 'sine', 0.05, 0.06);
            }

            playSuccess() {
                if (!this.enabled) return;
                this.init();
                if (!this.ctx) return;
                const notes = [523.25, 659.25, 783.99, 1046.50];
                notes.forEach((freq, i) => {
                    setTimeout(() => this.playTone(freq, 'triangle', 0.22, 0.12), i * 80);
                });
            }

            playError() {
                if (!this.enabled) return;
                this.init();
                if (!this.ctx) return;
                this.playTone(220, 'sawtooth', 0.25, 0.14);
                setTimeout(() => this.playTone(174.61, 'sawtooth', 0.35, 0.14), 120);
            }

            playHint() {
                this.playTone(880, 'sine', 0.12, 0.08);
                setTimeout(() => this.playTone(1174.66, 'sine', 0.2, 0.08), 90);
            }
        }

        const sound = new MedicalSoundEngine();

        function toggleAudio() {
            sound.enabled = !sound.enabled;
            const icon = document.getElementById('audio-icon');
            if (sound.enabled) {
                icon.className = 'fa-solid fa-volume-high';
                sound.playClick();
            } else {
                icon.className = 'fa-solid fa-volume-xmark text-rose-400';
            }
        }

        /* ==========================================================================
           2. COMPLETE CLINICAL CASES DATASET (Including prompt cases 1-5 + 5 extras)
           ========================================================================== */
        const CASES_DATA = [
            {
                id: "PRONTUÁRIO #001",
                difficulty: "easy",
                category: "Infectologia / Peste",
                patient: { age: "67 anos", sex: "Masculino" },
                history: "Um homem de 67 anos começou a apresentar febre muito alta, calafrios, dor de cabeça intensa e fraqueza. Depois de dois dias, percebeu o aparecimento de caroços muito doloridos na região da virilha e das axilas (bubões inflamatórios).",
                vitals: { pa: "100/65 mmHg", fc: "115 bpm", temp: "39.4 °C", sat: "96%" },
                labs: [
                    "Exame Físico: Linfadenopatia aguda dolorosa (bubões) em regiões inguinal e axilar.",
                    "Aspirado do Bubão: Presença de bacilos Gram-negativos em forma de alfinete de segurança (Yersinia pestis).",
                    "Hemograma: Leucocitose marcante (22.000/mm³) com desvio à esquerda."
                ],
                hint: "O aparecimento de adenopatias supurativas extremamente dolorosas (bubões) na virilha e axilas após febre súbita é a marca clássica da forma bubônica desta histórica zoonose.",
                options: ["Tuberculose Ganglionar", "Peste Bubônica", "Leishmaniose Visceral", "Linfoma de Hodgkin"],
                correctIndex: 1,
                explanation: "A Peste Bubônica é causada pela bactéria Yersinia pestis, transmitida pela picada da pulga do rato (Xenopsylla cheopis). A bactéria migra para os linfonodos regionais, gerando inflamação intensa, necrose e inchaços extremamente dolorosos denominados BUBÕES.",
                differential: [
                    { name: "Tuberculose Ganglionar", reason: "Doença indolente/crônica sem febre fulminante de início súbito ou bubões agudos hipermóveis e dolorosos." },
                    { name: "Leishmaniose Visceral", reason: "Cursa com esplenomegalia maciça e pancitopenia crônica, não com bubões agudos." },
                    { name: "Linfoma de Hodgkin", reason: "Neoplasia linfática com linfonodopatia indolor de crescimento lento." }
                ]
            },
            {
                id: "PRONTUÁRIO #002",
                difficulty: "medium",
                category: "Emergência Infectológica",
                patient: { age: "24 anos", sex: "Feminino" },
                history: "Uma mulher de 24 anos apresentou febre, vômitos, dores pelo corpo e manchas escuras na pele (púrpuras/equimoses). Também sentia muito cansaço e seu estado de saúde piorava rapidamente em poucas horas.",
                vitals: { pa: "85/50 mmHg", fc: "132 bpm", temp: "39.1 °C", sat: "93%" },
                labs: [
                    "Exame Físico: Lesões purpúricas e petequiais disseminadas que não desbotam à vitropressão. Sinais de instabilidade hemodinâmica (Choque Septico).",
                    "Coagulograma: TP e TPAE prolongados, D-Dímero elevado (CID - Coagulação Intravascular Disseminada).",
                    "Hemocultura: Diplococos Gram-negativos (Neisseria meningitidis) ou bacilos bacterêmicos graves."
                ],
                hint: "Manchas escuras purpúricas na pele com choque circulatório de evolução relâmpago em jovem indicam bacteremia fulminante com púrpura vascular.",
                options: ["Dengue Clássica", "Meningococcemia", "Púrpura Trombocitopênica Idiopática", "Febre Maculosa"],
                correctIndex: 1,
                explanation: "A Meningococcemia é a infecção bacteriana sistêmica grave causada por Neisseria meningitidis. O endotélio vascular é destruído pela endotoxina bacteriana, desencadeando a Coagulação Intravascular Disseminada (CID), petéquias, púrpuras fulminantes e choque séptico de rápida evolução.",
                differential: [
                    { name: "Dengue Clássica", reason: "Não causa choque bacterêmico fulminante com púrpura vascular em poucas horas sem sangramento manifesto prévio." },
                    { name: "PTI", reason: "A PTI causa trombocitopenia isolada sem febre alta, septicemia ou instabilidade hemodinâmica." },
                    { name: "Febre Maculosa", reason: "O exantema começa caracteristicamente nos pulsos e tornozelos após picada de carrapato com evolução de dias." }
                ]
            },
            {
                id: "PRONTUÁRIO #003",
                difficulty: "hard",
                category: "Pneumologia / Infectologia",
                patient: { age: "19 anos", sex: "Masculino" },
                history: "Um jovem de 19 anos começou a apresentar febre alta, tosse intensa, dor no peito e dificuldade para respirar. Sua tosse passou a apresentar secreção com sangue (hemoptise fulminante).",
                vitals: { pa: "90/60 mmHg", fc: "128 bpm", temp: "39.8 °C", sat: "84%" },
                labs: [
                    "Ausculta Pulmonar: Estertores crepitantes difusos em ambos os campos pulmonares.",
                    "Escarro (Gram/Bacterioscopia): Abundantes bacilos Gram-negativos com coloração bipolar.",
                    "Raio-X de Tórax: Opacidades e infiltrados broncopneumônicos bilaterais de progressão rápida."
                ],
                hint: "Insuficiência respiratória aguda febril com escarro hemoptoico (sangue) e bacilos Gram-negativos é a forma transmissível por gotículas da peste.",
                options: ["Pneumonia por Pneumococo", "Tuberculose Ativa", "Peste Pneumônica", "Edema Agudo de Pulmão"],
                correctIndex: 2,
                explanation: "A Peste Pneumônica é a forma mais letal e contagiosa da infecção por Yersinia pestis. Pode ser primária (por inalação de gotículas) ou secundária à disseminação hematogênica da forma bubônica. Provoca pneumonia necrotizante maciça com hemoptise, insuficiência respiratória severa e alta mortalidade sem antibioticoterapia precoce.",
                differential: [
                    { name: "Pneumonia por Pneumococo", reason: "Causa expectoração ferruginosa com consolidação lobar focal, sem o padrão necrotizante hemoptoico fulminante epidêmico." },
                    { name: "Tuberculose Ativa", reason: "Tem evolução subaguda a crônica ao longo de semanas/meses com emagrecimento." },
                    { name: "Edema Agudo de Pulmão", reason: "Origem cardiogênica sem quadro infeccioso febril com bacilos no escarro." }
                ]
            },
            {
                id: "PRONTUÁRIO #004",
                difficulty: "medium",
                category: "Infectologia / Epidemiologia",
                patient: { age: "42 anos", sex: "Masculino" },
                history: "Um homem de 42 anos chegou a uma cidade apresentando febre, calafrios, dores musculares e inchaços dolorosos no pescoço. Ele contou que havia passado por uma região onde muitos ratos estavam sendo encontrados mortos.",
                vitals: { pa: "110/70 mmHg", fc: "108 bpm", temp: "38.9 °C", sat: "97%" },
                labs: [
                    "Exame Físico: Linfadenite cervical dolorosa e pronunciada (bubão cervical).",
                    "Histórico Epidemiológico: Contato com pulgas de roedores silvestres e mortandade maciça de ratos (epizootia).",
                    "Sorologia / PCR: Positivo para antígeno F1 de Yersinia pestis."
                ],
                hint: "A mortandade prévia de roedores (ratos mortos) associada a febre e inchaço linfático no pescoço é a pista epidemiológica definitiva.",
                options: ["Leptospirose", "Peste Bubônica (Vetor Roedor)", "Febre Amarela", "Mononucleose Infecciosa"],
                correctIndex: 1,
                explanation: "Quando ocorre uma mortandade maciça de roedores (epizootia), as pulgas (Xenopsylla cheopis) abandonam os ratos mortos em busca de novos hospedeiros, infectando seres humanos. A bactéria inoculada pela picada gera a Peste Bubônica com infartamento ganglionar (pescoço/axila/virilha).",
                differential: [
                    { name: "Leptospirose", reason: "Transmitida pela urina do rato em água contaminada, causando sufusão conjuntival e dor nas panturrilhas, sem bubões linfáticos." },
                    { name: "Febre Amarela", reason: "Arbovirose transmitida por mosquitos silvestres que cursa com icterícia e sinal de Faget." },
                    { name: "Mononucleose", reason: "Causa adenomegalia cervical e dor de garganta em jovens, mas sem vínculo com mortandade de ratos." }
                ]
            },
            {
                id: "PRONTUÁRIO #005",
                difficulty: "hard",
                category: "Hematologia / Infectologia",
                patient: { age: "76 anos", sex: "Masculino" },
                history: "Um homem de 76 anos foi levado ao hospital com febre muito alta, fraqueza extrema, dores abdominais e vômitos. Seus dedos começaram a apresentar manchas escuras e enegrecidas, indicando necrose e gangrena por problemas graves de circulação.",
                vitals: { pa: "80/45 mmHg", fc: "124 bpm", temp: "39.6 °C", sat: "91%" },
                labs: [
                    "Exame Físico: Gangrena periférica acral (isquemia e necrose dos dígitos das mãos e pés - 'Morte Negra').",
                    "Laboratório: Trombose microvascular generalizada, Coagulação Intravascular Disseminada (CID).",
                    "Hemocultura: Crescimento de Yersinia pestis no sangue circulante."
                ],
                hint: "A necrose e gangrena periférica dos dedos desencadeada por microtrombose vascular disseminada originou historicamente o nome 'Peste Negra'.",
                options: ["Peste Septicêmica", "Gangrena de Fournier", "Doença de Raynaud", "Erisipela Bolosa"],
                correctIndex: 0,
                explanation: "A Peste Septicêmica ocorre quando a Yersinia pestis se multiplica diretamente na corrente sanguínea sem necessariamente formar bubões visíveis. O acúmulo de endotoxinas gera CID com microtrombos nos vasos periféricos, causando gangrena e necrose nos dedos das mãos e pés.",
                differential: [
                    { name: "Gangrena de Fournier", reason: "Fasciite necrotizante restrita à região perineal e genital." },
                    { name: "Doença de Raynaud", reason: "Fenômeno vasoespástico crônico episódico desencadeado pelo frio, sem febre fulminante ou choque." },
                    { name: "Erisipela Bolosa", reason: "Infecção cutânea estreptocócica dermoepidérmica sem gangrena acral sistêmica." }
                ]
            },
            {
                id: "PRONTUÁRIO #006",
                difficulty: "easy",
                category: "Infectologia / Arboviroses",
                patient: { age: "32 anos", sex: "Feminino" },
                history: "Paciente relata febre alta súbita, dor de cabeça intensa, dores musculares e dor acentuada atrás dos olhos (retro-orbitária) há 3 dias. Hoje notou sangramento na gengiva ao escovar os dentes.",
                vitals: { pa: "105/65 mmHg", fc: "96 bpm", temp: "38.7 °C", sat: "98%" },
                labs: [
                    "Hemograma: Plaquetopenia severa (48.000/mm³) e Leucopenia.",
                    "Prova do Laço: Positiva com mais de 20 petéquias no quadrado desenhado.",
                    "Sorologia: Antígeno NS1 positivo para arbovirose."
                ],
                hint: "Dor retro-orbitária característica associada a plaquetopenia e teste do laço positivo.",
                options: ["Gripe H1N1", "Dengue Grave", "Febre Tifóide", "Zika Vírus"],
                correctIndex: 1,
                explanation: "A Dengue com sinais de alarme é caracterizada por febre, trombocitopenia e dor retro-orbitária. A deposição de imunocomplexos leva a aumento da permeabilidade vascular e risco de sangramentos.",
                differential: [
                    { name: "Gripe H1N1", reason: "Cursa com tosse, coriza e dor de garganta marcantes, sem plaquetopenia severa isolada." },
                    { name: "Febre Tifóide", reason: "Infecção bacteriana entérica com roséolas tíficas e bradicardia relativa (Sinal de Faget)." },
                    { name: "Zika Vírus", reason: "Cursa com exantema pruriginoso precoce e hiperemia conjuntival sem dor retrorbitária intensa." }
                ]
            },
            {
                id: "PRONTUÁRIO #007",
                difficulty: "medium",
                category: "Zoonoses / Nefrologia",
                patient: { age: "38 anos", sex: "Masculino" },
                history: "Trabalhador da limpeza urbana que trabalhou em desentupimento de bueiros durante forte alagamento há 10 dias. Apresenta febre, olhos amarelados (icterícia rubínica) e dor insuportável nas panturrilhas.",
                vitals: { pa: "95/60 mmHg", fc: "110 bpm", temp: "39.0 °C", sat: "95%" },
                labs: [
                    "Exame Físico: Sufusão conjuntival (olhos vermelhos sem secreção) + Icterícia alaranjada/rubínica.",
                    "Laboratório: Creatinina 4.2 mg/dL (Insuficiência Renal), Bilirrubina Direta elevada, CPK elevada.",
                    "Sorologia: ELISA / Microaglutinação positiva para Leptospira interrogans."
                ],
                hint: "Histórico de alagamento + sufusão conjuntival + dor intensa nas panturrilhas e icterícia (Síndrome de Weil).",
                options: ["Hepatite Viral A", "Leptospirose (Síndrome de Weil)", "Febre Amarela", "Malária Falciparum"],
                correctIndex: 1,
                explanation: "A Leptospirose grave (Síndrome de Weil) é uma zoonose transmitida pela água contaminada com urina de roedores. Caracteriza-se pela tríade: icterícia rubínica, insuficiência renal aguda e hemorragia pulmonar/vascular com dor muscular (panturrilhas).",
                differential: [
                    { name: "Hepatite A", reason: "Transmissão fecal-oral que causa icterícia colestática sem dor nas panturrilhas ou insuficiência renal aguda inicial." },
                    { name: "Febre Amarela", reason: "Arbovirose silvestre sem história de contato com águas de enchente urbana." },
                    { name: "Malária", reason: "Caracterizada por paroxismos febris periódicos e anemia hemolítica." }
                ]
            },
            {
                id: "PRONTUÁRIO #008",
                difficulty: "easy",
                category: "Pneumologia",
                patient: { age: "55 anos", sex: "Masculino" },
                history: "Paciente apresenta tosse seca que se tornou produtiva há 4 semanas, accompanied por febre baixa ao final da tarde, sudorese noturna abundante que molha o lençol e perda de 7 kg no último mês.",
                vitals: { pa: "120/75 mmHg", fc: "84 bpm", temp: "37.6 °C", sat: "96%" },
                labs: [
                    "Ausculta Pulmonar: Murmúrio vesicular reduzido no ápice do pulmão direito.",
                    "Bacilosocopia do Escarro (BAAR): Positiva para Bacilos Álcool-Ácido Resistentes.",
                    "Raio-X de Tórax: Infiltrado cavitário no segmento apical do lobo superior direito."
                ],
                hint: "Tosse por mais de 3 semanas com sudorese noturna e lesão cavitária no ápice pulmonar.",
                options: ["Câncer de Pulmão", "Tuberculose Pulmonar", "Abscesso Pulmonar", "Pneumonia Micoplásmica"],
                correctIndex: 1,
                explanation: "A Tuberculose Pulmonar é causada pelo Mycobacterium tuberculosis. A resposta imune celular forma granulomas caseosos que cavitam nos ápices pulmonares (regiões mais oxigenadas), gerando febre vespertina, emagrecimento e tosse crônica.",
                differential: [
                    { name: "Câncer de Pulmão", reason: "Pode causar massa pulmonar e emagrecimento, mas não bacilos BAAR positivos no escarro." },
                    { name: "Abscesso Pulmonar", reason: "Causa nível hidroaéreo com escarro pútrido de evolução mais rápida." },
                    { name: "Pneumonia por Mycoplasma", reason: "Pneumonia atípica aguda autorregulada em jovens." }
                ]
            },
            {
                id: "PRONTUÁRIO #009",
                difficulty: "hard",
                category: "Infectologia Tropical",
                patient: { age: "29 anos", sex: "Masculino" },
                history: "Garimpeiro recém-chegado da Região Amazônica apresenta episódios de febre com calafrios intensos e tremores a cada 48 horas (febre terça), seguidos de sudorese profusa e prostração.",
                vitals: { pa: "110/70 mmHg", fc: "102 bpm", temp: "40.1 °C", sat: "97%" },
                labs: [
                    "Exame Físico: Hepatometalia e Esplenomegalia dolorosas à palpação.",
                    "Gota Espessa / Esfregaço Delgado: Presença de trofozoítos e esquizontes de Plasmodium falciparum nas hemácias.",
                    "Hemograma: Anemia normocítica e trombocitopenia."
                ],
                hint: "Picos febris periódicos com calafrios após estadia em área endêmica amazônica e parasitas intra-eritrocitários.",
                options: ["Malária", "Esquistossomose", "Doença de Chagas Aguda", "Leishmaniose Tegumentar"],
                correctIndex: 0,
                explanation: "A Malária é uma protozoose transmitida pela fêmea do mosquito Anopheles. Os merozoítos rompem as hemácias de forma síncrona (a cada 48h no P. falciparum/vivax), desencadeando os paroxismos febris clássicos com calafrios.",
                differential: [
                    { name: "Esquistossomose", reason: "Helmintíase intestinal/hepática sem paroxismos febris periódicos terçãos com parasita nas hemácias." },
                    { name: "Chagas Agudo", reason: "Transmitido pelo barbeiro; cursa com Sinal de Romaña ou chagoma de inoculação." },
                    { name: "Leishmaniose Tegumentar", reason: "Cursa com úlceras cutâneas indolores com bordas em moldura." }
                ]
            },
            {
                id: "PRONTUÁRIO #010",
                difficulty: "medium",
                category: "Pneumologia / Infectologia",
                patient: { age: "50 anos", sex: "Feminino" },
                history: "Paciente relata perda total do paladar (ageusia) e do olfato (anosmia) há 5 dias, associada a tosse seca, febre e progressiva falta de ar ao caminhar dentro de casa.",
                vitals: { pa: "130/85 mmHg", fc: "105 bpm", temp: "38.3 °C", sat: "89%" },
                labs: [
                    "Tomografia Computadorizada de Tórax: Infiltrados pulmonares parenquimatosos com padrão em 'vidro fosco' periférico e bilateral.",
                    "RT-PCR de Nasofaringe: Detectável para RNA do vírus SARS-CoV-2.",
                    "Gasometria Arterial: Hipoxemia (PaO2/FiO2 < 300)."
                ],
                hint: "Anosmia/ageusia súbita associada a infiltrado em vidro fosco bilateral na tomografia de tórax.",
                options: ["Infecção por Influenza A", "COVID-19 (SRAG)", "Aspergilose Pulmonar", "Pneumonite por Hipersensibilidade"],
                correctIndex: 1,
                explanation: "A COVID-19 causada pelo coronavírus SARS-CoV-2 acopla-se aos receptores ACE2, afetando o epitélio olfatório (anosmia) e pneumócitos tipo II, produzindo a Síndrome Respiratória Aguda Grave com padrão radiológico em vidro fosco.",
                differential: [
                    { name: "Influenza A", reason: "Raramente causa anosmia pura isolada sem sintomas catarrais intensos." },
                    { name: "Aspergilose Pulmonar", reason: "Infecção fúngica invasiva em imunodeprimidos com sinal do halo no TC." },
                    { name: "Pneumonite por Hipersensibilidade", reason: "Reação alérgica inalatória crônica a mofos ou aves." }
                ]
            }
        ];

        /* ==========================================================================
           3. GAME ENGINE & STATE MANAGEMENT
           ========================================================================== */
        const gameState = {
            playerName: "Dr. Investigador",
            mode: "standard",
            score: 0,
            casesCompleted: 0,
            correctCount: 0,
            hintsUsedCount: 0,
            streak: 0,
            availableCases: [],
            currentCase: null,
            selectedOption: null,
            hintRevealed: false,
            timerInterval: null,
            timerSeconds: 45
        };

        function showScreen(screenId) {
            ['screen-start', 'screen-game', 'screen-explanation', 'screen-gameover'].forEach(id => {
                document.getElementById(id).classList.add('hidden');
            });
            document.getElementById(screenId).classList.remove('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function goHome() {
            clearInterval(gameState.timerInterval);
            document.getElementById('header-stats').classList.add('hidden');
            showScreen('screen-start');
        }

        function startGame(e) {
            e.preventDefault();
            sound.init();
            sound.playClick();

            const nameInput = document.getElementById('input-player-name').value.trim();
            gameState.playerName = nameInput || "Dr. Investigador";
            gameState.mode = document.querySelector('input[name="game-mode"]:checked').value;

            // Reset Game Stats
            gameState.score = 0;
            gameState.casesCompleted = 0;
            gameState.correctCount = 0;
            gameState.hintsUsedCount = 0;
            gameState.streak = 0;

            prepareCases();

            // Setup Header Bar
            document.getElementById('stat-player-name').innerText = gameState.playerName;
            document.getElementById('stat-score').innerText = '0 pts';
            document.getElementById('stat-streak').innerText = '1x';
            document.getElementById('header-stats').classList.remove('hidden');

            const timerContainer = document.getElementById('stat-timer-container');
            if (gameState.mode === 'timed') {
                timerContainer.classList.remove('hidden');
            } else {
                timerContainer.classList.add('hidden');
            }

            loadNextCase();
        }

        function prepareCases() {
            if (gameState.mode === 'random') {
                gameState.availableCases = [...CASES_DATA].sort(() => Math.random() - 0.5);
            } else {
                // Keep preset order (Starting with requested historical plague/infection cases)
                gameState.availableCases = [...CASES_DATA];
            }
        }

        /* ==========================================================================
           4. CASE DISPLAY & SELECTION
           ========================================================================== */
        function loadNextCase() {
            if (gameState.availableCases.length === 0) {
                endGame();
                return;
            }

            gameState.currentCase = gameState.availableCases.shift();
            gameState.selectedOption = null;
            gameState.hintRevealed = false;

            // Render Clipboard Data
            document.getElementById('case-id-display').innerText = `${gameState.currentCase.id} — CASO ${gameState.casesCompleted + 1}`;
            document.getElementById('case-category-display').innerText = `Especialidade: ${gameState.currentCase.category}`;
            document.getElementById('patient-age').innerText = gameState.currentCase.patient.age;
            document.getElementById('patient-sex').innerText = gameState.currentCase.patient.sex;
            document.getElementById('patient-history').innerText = gameState.currentCase.history;

            // Render Vitals & Labs
            renderVitals(gameState.currentCase.vitals);
            document.getElementById('patient-labs').innerHTML = gameState.currentCase.labs.map(l => `<p>• ${l}</p>`).join('');

            // Reset Hint UI
            document.getElementById('hint-box').classList.add('hidden');
            document.getElementById('btn-request-hint').classList.remove('hidden');

            // Render Options
            renderOptions(gameState.currentCase.options);

            // Reset Submit Button
            const submitBtn = document.getElementById('btn-submit-diagnosis');
            submitBtn.disabled = true;
            submitBtn.className = "w-full bg-slate-800 text-slate-500 cursor-not-allowed font-heading font-black text-base py-4 px-4 rounded-xl shadow-lg transition flex items-center justify-center gap-2";

            showScreen('screen-game');

            if (gameState.mode === 'timed') {
                startTimer();
            }
        }

        function renderVitals(v) {
            document.getElementById('vitals-grid').innerHTML = `
                <div class="bg-white/80 p-2 rounded-lg border border-slate-200">
                    <span class="text-[9px] text-slate-500 block uppercase font-bold">PA</span>
                    <span class="font-extrabold text-slate-800 text-xs">${v.pa}</span>
                </div>
                <div class="bg-white/80 p-2 rounded-lg border border-slate-200">
                    <span class="text-[9px] text-slate-500 block uppercase font-bold">FC</span>
                    <span class="font-extrabold text-rose-600 text-xs">${v.fc}</span>
                </div>
                <div class="bg-white/80 p-2 rounded-lg border border-slate-200">
                    <span class="text-[9px] text-slate-500 block uppercase font-bold">Temp</span>
                    <span class="font-extrabold text-amber-600 text-xs">${v.temp}</span>
                </div>
                <div class="bg-white/80 p-2 rounded-lg border border-slate-200">
                    <span class="text-[9px] text-slate-500 block uppercase font-bold">SatO2</span>
                    <span class="font-extrabold text-teal-700 text-xs">${v.sat}</span>
                </div>
            `;
        }

        function renderOptions(options) {
            const container = document.getElementById('options-container');
            const letters = ['A', 'B', 'C', 'D'];
            
            container.innerHTML = options.map((opt, idx) => `
                <button onclick="selectOption(${idx})" id="opt-btn-${idx}" class="opt-btn w-full text-left p-3.5 rounded-2xl border border-slate-800 bg-slate-900 hover:bg-slate-800/80 transition flex items-center justify-between group">
                    <div class="flex items-center space-x-3">
                        <span class="w-7 h-7 rounded-lg bg-slate-800 text-slate-300 group-hover:bg-teal-500 group-hover:text-white flex items-center justify-center font-bold text-xs transition">
                            ${letters[idx]}
                        </span>
                        <span class="font-bold text-sm text-slate-200 group-hover:text-white transition">${opt}</span>
                    </div>
                    <div id="opt-check-${idx}" class="w-5 h-5 rounded-full border border-slate-700 flex items-center justify-center text-xs opacity-0 transition">
                        <i class="fa-solid fa-check text-teal-400"></i>
                    </div>
                </button>
            `).join('');
        }

        function selectOption(index) {
            sound.playClick();
            gameState.selectedOption = index;

            document.querySelectorAll('.opt-btn').forEach((btn, idx) => {
                const check = document.getElementById(`opt-check-${idx}`);
                if (idx === index) {
                    btn.className = "opt-btn w-full text-left p-3.5 rounded-2xl border-2 border-teal-500 bg-teal-950/30 transition flex items-center justify-between shadow-md shadow-teal-500/10";
                    check.classList.remove('opacity-0');
                } else {
                    btn.className = "opt-btn w-full text-left p-3.5 rounded-2xl border border-slate-800 bg-slate-900 hover:bg-slate-800/80 transition flex items-center justify-between";
                    check.classList.add('opacity-0');
                }
            });

            const submitBtn = document.getElementById('btn-submit-diagnosis');
            submitBtn.disabled = false;
            submitBtn.className = "w-full bg-gradient-to-r from-teal-500 via-emerald-600 to-sky-500 hover:from-teal-400 hover:to-sky-400 text-white font-heading font-black text-base py-4 px-4 rounded-xl shadow-lg shadow-teal-500/20 transition transform active:scale-[0.99] flex items-center justify-center gap-2 animate-subtle-pulse";
        }

        function requestHint() {
            if (gameState.hintRevealed) return;
            sound.playHint();

            gameState.hintRevealed = true;
            gameState.hintsUsedCount++;

            document.getElementById('hint-text').innerText = gameState.currentCase.hint;
            document.getElementById('hint-box').classList.remove('hidden');
            document.getElementById('btn-request-hint').classList.add('hidden');
        }

        /* ==========================================================================
           5. TIMED MODE CONTROLLER
           ========================================================================== */
        function startTimer() {
            clearInterval(gameState.timerInterval);
            gameState.timerSeconds = 45;
            updateTimerDisplay();

            gameState.timerInterval = setInterval(() => {
                gameState.timerSeconds--;
                updateTimerDisplay();

                if (gameState.timerSeconds <= 0) {
                    clearInterval(gameState.timerInterval);
                    sound.playError();
                    submitDiagnosis(true);
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            document.getElementById('stat-timer').innerText = `${gameState.timerSeconds}s`;
        }

        /* ==========================================================================
           6. SUBMISSION & EVALUATION
           ========================================================================== */
        function submitDiagnosis(isTimeout = false) {
            clearInterval(gameState.timerInterval);

            const isCorrect = !isTimeout && (gameState.selectedOption === gameState.currentCase.correctIndex);
            
            let pointsEarned = 0;
            if (isCorrect) {
                sound.playSuccess();
                gameState.streak++;
                const basePoints = { easy: 100, medium: 150, hard: 200 }[gameState.currentCase.difficulty] || 100;
                let penalty = gameState.hintRevealed ? 15 : 0;
                let timeBonus = gameState.mode === 'timed' ? gameState.timerSeconds * 2 : 0;
                let streakMultiplier = 1 + (gameState.streak - 1) * 0.15;

                pointsEarned = Math.round((basePoints - penalty + timeBonus) * streakMultiplier);
                gameState.score += pointsEarned;
                gameState.correctCount++;
            } else {
                sound.playError();
                gameState.streak = 0;
            }

            gameState.casesCompleted++;
            document.getElementById('stat-score').innerText = `${gameState.score} pts`;
            document.getElementById('stat-streak').innerText = `${gameState.streak}x`;

            renderExplanation(isCorrect, pointsEarned, isTimeout);
            showScreen('screen-explanation');
        }

        function renderExplanation(isCorrect, points, isTimeout) {
            const banner = document.getElementById('explanation-banner');
            const iconContainer = document.getElementById('explanation-icon-container');
            const title = document.getElementById('explanation-title');
            const subtitle = document.getElementById('explanation-subtitle');
            const pointsBadge = document.getElementById('explanation-points-badge');

            if (isCorrect) {
                banner.className = "rounded-2xl p-4 sm:p-5 mb-6 flex items-center justify-between bg-emerald-950/90 border border-emerald-500/40 text-emerald-200 shadow-xl";
                iconContainer.className = "w-12 h-12 rounded-2xl bg-emerald-500/20 text-emerald-400 flex items-center justify-center text-2xl font-bold";
                iconContainer.innerHTML = '<i class="fa-solid fa-check"></i>';
                title.innerText = "Diagnóstico Correto! 🎉";
                subtitle.innerText = "Sua conduta investigativa desvendou o caso com precisão.";
                pointsBadge.className = "font-heading font-black text-lg sm:text-xl px-4 py-2 rounded-xl border bg-emerald-900/60 border-emerald-500/50 text-emerald-300";
                pointsBadge.innerText = `+${points} pts`;
            } else {
                banner.className = "rounded-2xl p-4 sm:p-5 mb-6 flex items-center justify-between bg-rose-950/90 border border-rose-500/40 text-rose-200 shadow-xl";
                iconContainer.className = "w-12 h-12 rounded-2xl bg-rose-500/20 text-rose-400 flex items-center justify-center text-2xl font-bold";
                iconContainer.innerHTML = '<i class="fa-solid fa-xmark"></i>';
                title.innerText = isTimeout ? "Tempo Esgotado! ⏱️" : "Diagnóstico Incorreto ❌";
                subtitle.innerText = `O diagnóstico correto era: ${gameState.currentCase.options[gameState.currentCase.correctIndex]}`;
                pointsBadge.className = "font-heading font-black text-lg sm:text-xl px-4 py-2 rounded-xl border bg-rose-900/60 border-rose-500/50 text-rose-300";
                pointsBadge.innerText = `0 pts`;
            }

            document.getElementById('explanation-text').innerText = gameState.currentCase.explanation;
            
            // Render Differential
            const diffList = document.getElementById('differential-list');
            diffList.innerHTML = gameState.currentCase.differential.map(d => `
                <li class="bg-slate-950/60 border border-slate-800 p-3 rounded-xl">
                    <span class="font-bold text-amber-300 block mb-0.5">• ${d.name}</span>
                    <span class="text-slate-400 text-xs">${d.reason}</span>
                </li>
            `).join('');
        }

        function nextCase() {
            sound.playClick();
            if (gameState.availableCases.length > 0) {
                loadNextCase();
            } else {
                endGame();
            }
        }

        /* ==========================================================================
           7. SUMMARY & LEADERBOARD SYSTEM
           ========================================================================== */
        function endGame() {
            saveScore();

            const total = gameState.casesCompleted;
            const accuracyPct = total > 0 ? Math.round((gameState.correctCount / total) * 100) : 0;

            document.getElementById('summary-score').innerText = `${gameState.score} pts`;
            document.getElementById('summary-accuracy').innerText = `${gameState.correctCount} / ${total}`;
            document.getElementById('summary-percentage').innerText = `${accuracyPct}%`;
            document.getElementById('summary-hints').innerText = `${gameState.hintsUsedCount}`;

            // Rank Titles based on performance
            let title = "Estudante de Medicina";
            let icon = "fa-user-graduate";
            if (accuracyPct >= 90) {
                title = "Médico Especialista Infectologista 🏆";
                icon = "fa-award";
            } else if (accuracyPct >= 70) {
                title = "Médico Residente Sênior 🩺";
                icon = "fa-user-doctor";
            } else if (accuracyPct >= 50) {
                title = "Investigador Clínico Júnior 🔬";
                icon = "fa-microscope";
            }

            document.getElementById('summary-rank-title').innerText = title;
            document.getElementById('summary-rank-icon').className = `fa-solid ${icon}`;

            showScreen('screen-gameover');
        }

        function saveScore() {
            try {
                const leaderboard = JSON.parse(localStorage.getItem('detetive_saude_scores') || '[]');
                const newEntry = {
                    name: gameState.playerName,
                    score: gameState.score,
                    mode: gameState.mode === 'standard' ? 'Investigação' : gameState.mode === 'timed' ? 'Tempo' : 'Surpresa',
                    date: new Date().toLocaleDateString('pt-BR')
                };

                leaderboard.push(newEntry);
                leaderboard.sort((a, b) => b.score - a.score);
                const top10 = leaderboard.slice(0, 10);

                localStorage.setItem('detetive_saude_scores', JSON.stringify(top10));
            } catch(e) {
                console.log('Local storage disabled or restricted');
            }
        }

        function openLeaderboard() {
            sound.playClick();
            const body = document.getElementById('leaderboard-body');
            let leaderboard = [];
            try {
                leaderboard = JSON.parse(localStorage.getItem('detetive_saude_scores') || '[]');
            } catch(e) {}

            if (leaderboard.length === 0) {
                body.innerHTML = `
                    <tr>
                        <td colspan="4" class="p-4 text-center text-slate-500 italic">Nenhuma pontuação registrada ainda. Seja o primeiro!</td>
                    </tr>
                `;
            } else {
                body.innerHTML = leaderboard.map((item, idx) => `
                    <tr class="hover:bg-slate-900/60 transition">
                        <td class="p-3 font-bold ${idx === 0 ? 'text-amber-400' : 'text-slate-400'}">${idx + 1}</td>
                        <td class="p-3 font-bold text-white flex items-center gap-2">
                            ${idx === 0 ? '<i class="fa-solid fa-crown text-amber-400"></i>' : ''}
                            ${item.name}
                        </td>
                        <td class="p-3 text-slate-400"><span class="bg-slate-800 text-slate-300 text-[10px] px-2 py-0.5 rounded-full font-semibold">${item.mode}</span></td>
                        <td class="p-3 text-right font-black text-amber-400 font-heading">${item.score} pts</td>
                    </tr>
                `).join('');
            }

            document.getElementById('modal-leaderboard').classList.remove('hidden');
        }

        function closeLeaderboard() {
            sound.playClick();
            document.getElementById('modal-leaderboard').classList.add('hidden');
        }

        function clearLeaderboard() {
            try {
                localStorage.removeItem('detetive_saude_scores');
                openLeaderboard();
            } catch(e) {}
        }
    </script>
</body>
</html>
