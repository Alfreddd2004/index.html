<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal Clínico MiSalud - Entrega Inclusiva de Resultados</title>

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Font Awesome 6 CDN para íconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Google Fonts: Atkinson Hyperlegible e Inter para alta legibilidad -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Atkinson+Hyperlegible:ital,wght@0,400;0,700;1,400;1,700&family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        clinical: {
                            50: '#f0f7ff',
                            100: '#e0effe',
                            500: '#0284c7',
                            700: '#0369a1',
                            900: '#0c4a6e',
                        },
                        accessible: {
                            yellow: '#facc15',
                            dark: '#0f172a',
                            highBlue: '#0047ab'
                        }
                    },
                    fontFamily: {
                        sans: ['Atkinson Hyperlegible', 'Inter', 'sans-serif'],
                        dyslexic: ['Comic Sans MS', 'Arial', 'sans-serif'] // Fallback legible
                    }
                }
            }
        }
    </script>

    <style>
        /* Estilos de Accesibilidad Personalizables */
        :root {
            --font-scale: 1rem;
            --letter-spacing: 0.02em;
            --line-height: 1.6;
        }

        html {
            font-size: var(--font-scale);
            letter-spacing: var(--letter-spacing);
            line-height: var(--line-height);
        }

        /* Focus accesible de alto contraste para teclado */
        :focus-visible {
            outline: 4px solid #facc15 !important;
            outline-offset: 3px !important;
            box-shadow: 0 0 0 6px #0369a1 !important;
        }

        /* Modos de Contraste */
        .theme-high-dark {
            background-color: #000000 !important;
            color: #ffffff !important;
        }
        .theme-high-dark nav, .theme-high-dark section, .theme-high-dark div, .theme-high-dark card {
            background-color: #121212 !important;
            color: #ffffff !important;
            border-color: #ffff00 !important;
        }
        .theme-high-dark button, .theme-high-dark a {
            border: 2px solid #ffff00 !important;
        }

        .theme-yellow-black {
            background-color: #000000 !important;
            color: #ffff00 !important;
        }
        .theme-yellow-black * {
            background-color: #000000 !important;
            color: #ffff00 !important;
            border-color: #ffff00 !important;
        }

        .theme-grayscale {
            filter: grayscale(100%);
        }

        /* Dislexia Friendly */
        .font-dyslexic-mode * {
            font-family: 'Comic Sans MS', 'Chalkboard SE', 'Arial', sans-serif !important;
            word-spacing: 0.15em !important;
        }

        /* Animaciones para el asistente por voz */
        @keyframes sound-wave {
            0%, 100% { transform: height: 6px; }
            50% { height: 24px; }
        }
        .wave-bar {
            animation: sound-wave 1.2s ease-in-out infinite;
        }
        .wave-bar:nth-child(2) { animation-delay: 0.2s; }
        .wave-bar:nth-child(3) { animation-delay: 0.4s; }
        .wave-bar:nth-child(4) { animation-delay: 0.1s; }
    </style>
</head>
<body class="bg-slate-50 text-slate-900 min-h-screen flex flex-col transition-colors duration-200">

    <!-- Enlace directo para Lectores de Pantalla (Skip Link) -->
    <a href="#main-content" class="sr-only focus:not-sr-only focus:absolute focus:z-50 focus:p-4 focus:bg-amber-400 focus:text-slate-900 focus:font-bold focus:rounded-lg focus:shadow-xl">
        Saltar directamente al contenido principal
    </a>

    <!-- Alerta accesible para lectores de pantalla y eventos en vivo -->
    <div id="aria-announcer" class="sr-only" aria-live="polite" aria-atomic="true"></div>

    <!-- HEADER / NAVEGACIÓN FIJA -->
    <header class="sticky top-0 z-40 bg-slate-900 text-white shadow-xl border-b-4 border-blue-500">
        <!-- Barra Superior de Estado y Red -->
        <div class="bg-slate-950 px-4 py-1.5 text-xs flex justify-between items-center border-b border-slate-800">
            <div class="flex items-center space-x-3">
                <span class="font-bold tracking-wider text-blue-400"><i class="fa-solid fa-hospital-user mr-1.5" aria-hidden="true"></i>SISTEMA DE SALUD INCLUSIVO</span>
                <span class="hidden sm:inline text-slate-400">| WCAG 2.1 AAA Compliant</span>
            </div>
            
            <!-- Indicador de Red Dinámico -->
            <div id="network-status-bar" class="flex items-center space-x-2 bg-emerald-900/60 text-emerald-300 px-3 py-0.5 rounded-full text-xs font-semibold border border-emerald-500">
                <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse" aria-hidden="true"></span>
                <span id="network-status-text">Conexión Estable (Modo Online)</span>
            </div>
        </div>

        <!-- Menú Principal con 6 Apartados Solicitados -->
        <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex flex-wrap justify-between items-center" aria-label="Navegación Principal">
            <a href="#main-content" class="flex items-center space-x-3 group focus:rounded-lg p-1">
                <div class="bg-blue-600 text-white p-2.5 rounded-xl shadow-md group-hover:bg-blue-500 transition">
                    <i class="fa-solid fa-heart-pulse text-2xl" aria-hidden="true"></i>
                </div>
                <div>
                    <span class="text-xl font-extrabold tracking-tight block leading-tight">MiSalud</span>
                    <span class="text-xs text-blue-300 block font-medium">Portal Clínico Accesible</span>
                </div>
            </a>

            <!-- Botón Hamburguesa Móvil -->
            <button id="mobile-menu-btn" class="md:hidden p-2 rounded-lg bg-slate-800 text-slate-200 hover:text-white hover:bg-slate-700" aria-expanded="false" aria-controls="nav-links" aria-label="Abrir menú de navegación">
                <i class="fa-solid fa-bars text-xl" aria-hidden="true"></i>
            </button>

            <!-- Links de Navegación Exactos (6 Secciones) -->
            <ul id="nav-links" class="hidden md:flex flex-wrap items-center gap-1 sm:gap-2 mt-4 md:mt-0 w-full md:w-auto text-sm font-semibold">
                <li>
                    <a href="#registrarse" class="nav-item px-3 py-2 rounded-lg hover:bg-blue-800 focus:bg-blue-800 transition flex items-center gap-2 text-white">
                        <i class="fa-solid fa-user-plus text-blue-400" aria-hidden="true"></i> 1. Registrarse
                    </a>
                </li>
                <li>
                    <a href="#tutorial" class="nav-item px-3 py-2 rounded-lg hover:bg-blue-800 focus:bg-blue-800 transition flex items-center gap-2 text-white">
                        <i class="fa-solid fa-circle-question text-amber-400" aria-hidden="true"></i> 2. Tutorial
                    </a>
                </li>
                <li>
                    <a href="#resultados" class="nav-item px-3 py-2 rounded-lg hover:bg-blue-800 focus:bg-blue-800 transition flex items-center gap-2 text-white">
                        <i class="fa-solid fa-file-medical text-emerald-400" aria-hidden="true"></i> 3. Resultados
                    </a>
                </li>
                <li>
                    <a href="#accesibilidad" class="nav-item px-3 py-2 rounded-lg bg-blue-700/60 hover:bg-blue-700 focus:bg-blue-700 transition flex items-center gap-2 text-amber-300 border border-blue-500">
                        <i class="fa-solid fa-universal-access" aria-hidden="true"></i> 4. Accesibilidad
                    </a>
                </li>
                <li>
                    <a href="#condiciones" class="nav-item px-3 py-2 rounded-lg hover:bg-blue-800 focus:bg-blue-800 transition flex items-center gap-2 text-white">
                        <i class="fa-solid fa-shield-halved text-purple-400" aria-hidden="true"></i> 5. Condiciones
                    </a>
                </li>
                <li>
                    <a href="#offline-history" class="nav-item px-3 py-2 rounded-lg hover:bg-blue-800 focus:bg-blue-800 transition flex items-center gap-2 text-white">
                        <i class="fa-solid fa-wifi text-cyan-400" aria-hidden="true"></i> 6. Sin Internet
                    </a>
                </li>
            </ul>
        </nav>
    </header>

    <!-- CONTENIDO PRINCIPAL -->
    <main id="main-content" class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-16">

        <!-- Banner de Bienvenida Inclusivo -->
        <section class="bg-gradient-to-r from-blue-900 via-slate-900 to-blue-950 text-white rounded-3xl p-6 sm:p-10 shadow-2xl relative overflow-hidden border-2 border-blue-700">
            <div class="max-w-3xl space-y-4 relative z-10">
                <div class="inline-flex items-center gap-2 bg-blue-600/50 text-blue-200 px-3.5 py-1.5 rounded-full text-sm font-semibold border border-blue-400">
                    <i class="fa-solid fa-hands-asl-interpreting" aria-hidden="true"></i> Plataforma Rediseñada para Inclusión Equitativa
                </div>
                <h1 class="text-3xl sm:text-5xl font-extrabold tracking-tight leading-tight">
                    Tus resultados de salud, <span class="text-amber-400 underline decoration-blue-500">claros, seguros y a tu ritmo</span>.
                </h1>
                <p class="text-lg text-slate-200 leading-relaxed">
                    Hemos eliminado las limitaciones de tiempo. Consulta tus informes de laboratorio con asistentes por voz, lecturas adaptadas para adultos mayores y disponibilidad permanente sin conexión.
                </p>
                <div class="flex flex-wrap gap-4 pt-2">
                    <a href="#resultados" class="bg-amber-400 hover:bg-amber-300 text-slate-950 px-6 py-3.5 rounded-xl font-extrabold text-base flex items-center gap-3 transition shadow-lg focus:ring-4">
                        <i class="fa-solid fa-notes-medical text-xl" aria-hidden="true"></i> Ver Mis Resultados Ahora
                    </a>
                    <button onclick="speakText('Bienvenido al Portal Clínico MiSalud. Aquí puede consultar sus resultados clínicos sin tiempo límite, ajustar la letra y usar asistencia hablada.')" class="bg-slate-800 hover:bg-slate-700 text-white border border-slate-600 px-5 py-3.5 rounded-xl font-bold text-sm flex items-center gap-2 transition">
                        <i class="fa-solid fa-volume-high text-blue-400 text-lg" aria-hidden="true"></i> Escuchar Bienvenida
                    </button>
                </div>
            </div>
        </section>

         <!-- SECCIÓN 1: REGISTRARSE -->
        <section id="registrarse" class="bg-white rounded-3xl p-6 sm:p-10 shadow-xl border border-slate-200 space-y-8" aria-labelledby="heading-registro">
            <div class="border-b border-slate-200 pb-5 flex flex-wrap justify-between items-center gap-4">
                <div>
                    <h2 id="heading-registro" class="text-2xl sm:text-3xl font-extrabold text-slate-900 flex items-center gap-3">
                        <span class="w-10 h-10 bg-blue-100 text-blue-700 rounded-full flex items-center justify-center text-lg font-bold">1</span>
                        Registro de Pacientes Accesible
                    </h2>
                    <p class="text-slate-600 text-base mt-1">Formulario guiado compatible con lectores de pantalla y soporte biométrico.</p>
                </div>
                <span class="bg-blue-50 text-blue-800 text-xs font-bold px-3 py-1.5 rounded-lg border border-blue-200">
                    <i class="fa-solid fa-lock text-blue-600 mr-1" aria-hidden="true"></i> Datos Protegidos por Ley
                </span>
            </div>

            <div class="grid lg:grid-cols-12 gap-8">
                <!-- Formulario -->
                <form id="form-registro" class="lg:col-span-7 space-y-5" onsubmit="handleRegister(event)">
                    <div>
                        <label for="reg-nombre" class="block font-bold text-slate-900 text-base mb-1">
                            Nombre Completo <span class="text-red-600" aria-hidden="true">*</span>
                        </label>
                        <input type="text" id="reg-nombre" required aria-required="true" aria-describedby="reg-nombre-desc" class="w-full px-4 py-3 border-2 border-slate-300 rounded-xl focus:border-blue-600 text-slate-900 text-base" placeholder="Ej. Carmen Rodríguez">
                        <p id="reg-nombre-desc" class="text-xs text-slate-500 mt-1">Escriba su nombre y apellidos completos como figuran en su documento médico.</p>
                    </div>

                    <div class="grid sm:grid-cols-2 gap-4">
                        <div>
                            <label for="reg-doc" class="block font-bold text-slate-900 text-base mb-1">
                                Documento de Identidad <span class="text-red-600" aria-hidden="true">*</span>
                            </label>
                            <input type="text" id="reg-doc" required aria-required="true" class="w-full px-4 py-3 border-2 border-slate-300 rounded-xl focus:border-blue-600 text-slate-900 text-base" placeholder="N° de Cédula o DNI">
                        </div>
                        <div>
                            <label for="reg-codigo-medico" class="block font-bold text-slate-900 text-base mb-1">
                                Código de Validación Médica
                            </label>
                            <input type="text" id="reg-codigo-medico" aria-describedby="code-help" class="w-full px-4 py-3 border-2 border-slate-300 rounded-xl focus:border-blue-600 text-slate-900 text-base" placeholder="Ej. MED-8842-X">
                            <p id="code-help" class="text-xs text-slate-500 mt-1">Proporcionado por su médico en la consulta.</p>
                        </div>
                    </div>

                    <!-- Autenticación Simplificada y Biometría -->
                    <fieldset class="border-2 border-slate-200 rounded-2xl p-4 bg-slate-50 space-y-3">
                        <legend class="font-bold text-slate-900 text-sm px-2 bg-white rounded-md border border-slate-200">Métodos de Autenticación Rápida</legend>
                        <p class="text-xs text-slate-600">Active biometría para ingresar en el futuro sin recordar contraseñas complejas.</p>
                        
                        <div class="flex flex-wrap gap-4">
                            <button type="button" onclick="simulateBiometric('Huella Dactilar')" class="flex-1 min-w-[140px] bg-white border-2 border-slate-300 hover:border-blue-600 text-slate-800 p-3 rounded-xl flex items-center justify-center gap-2 font-bold text-sm transition">
                                <i class="fa-solid fa-fingerprint text-blue-600 text-xl" aria-hidden="true"></i> Registra Huella
                            </button>
                            <button type="button" onclick="simulateBiometric('Reconocimiento Facial')" class="flex-1 min-w-[140px] bg-white border-2 border-slate-300 hover:border-blue-600 text-slate-800 p-3 rounded-xl flex items-center justify-center gap-2 font-bold text-sm transition">
                                <i class="fa-solid fa-face-smile text-purple-600 text-xl" aria-hidden="true"></i> Reconocimiento Facial
                            </button>
                        </div>
                        <div id="biometric-status" class="hidden p-3 bg-emerald-100 text-emerald-900 rounded-lg text-xs font-bold flex items-center gap-2" role="status">
                            <i class="fa-solid fa-circle-check text-emerald-600 text-base" aria-hidden="true"></i>
                            <span id="biometric-msg">Biometría asociada exitosamente.</span>
                        </div>
                    </fieldset>

                    <button type="submit" class="w-full bg-blue-700 hover:bg-blue-800 text-white font-extrabold py-4 px-6 rounded-xl text-lg flex items-center justify-center gap-3 transition shadow-lg">
                        <i class="fa-solid fa-user-check text-xl" aria-hidden="true"></i> Completar Registro Seguro
                    </button>
                </form>

                <!-- Tarjeta del Médico Validador -->
                <div class="lg:col-span-5 bg-gradient-to-br from-slate-900 to-blue-950 text-white p-6 rounded-2xl flex flex-col justify-between border-2 border-blue-800">
                    <div class="space-y-4">
                        <div class="flex items-center gap-3">
                            <div class="w-12 h-12 rounded-full bg-blue-600 flex items-center justify-center text-xl font-bold text-white">
                                DR
                            </div>
                            <div>
                                <h3 class="font-bold text-base text-white">Validación Médica Directa</h3>
                                <p class="text-xs text-blue-300">Garantía de Entrega Oficial</p>
                            </div>
                        </div>
                        <p class="text-sm text-slate-300 leading-relaxed">
                            Si se le dificulta completar el formulario web, su médico tratante puede autorizar su cuenta de manera remota durante su consulta o vía llamada asistida.
                        </p>
                        <div class="bg-blue-900/50 p-4 rounded-xl border border-blue-700 text-xs space-y-2">
                            <div class="flex items-center justify-between text-blue-200 font-semibold">
                                <span><i class="fa-solid fa-phone-volume mr-1.5" aria-hidden="true"></i> Asistencia Telefónica:</span>
                                <span class="text-amber-400 font-mono text-sm">0800-MISALUD</span>
                            </div>
                            <p class="text-slate-400">Atención prioritaria para adultos mayores y personas con discapacidad.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 2: TUTORIAL PARA ADULTOS MAYORES Y FAQ -->
        <section id="tutorial" class="bg-white rounded-3xl p-6 sm:p-10 shadow-xl border border-slate-200 space-y-8" aria-labelledby="heading-tutorial">
            <div class="border-b border-slate-200 pb-5">
                <h2 id="heading-tutorial" class="text-2xl sm:text-3xl font-extrabold text-slate-900 flex items-center gap-3">
                    <span class="w-10 h-10 bg-amber-100 text-amber-700 rounded-full flex items-center justify-center text-lg font-bold">2</span>
                    Tutorial Fácil e Inducción Paso a Paso
                </h2>
                <p class="text-slate-600 text-base mt-1">Diseñado especialmente para personas con poca experiencia en computadoras o teléfonos inteligentes.</p>
            </div>

            <!-- Pasos Gigantes e Ilustrados -->
            <div class="grid md:grid-cols-3 gap-6">
                <!-- Paso 1 -->
                <div class="bg-amber-50/60 border-2 border-amber-200 rounded-2xl p-6 text-center space-y-3 relative flex flex-col justify-between">
                    <span class="absolute top-3 left-3 bg-amber-400 text-slate-950 font-black px-3 py-1 rounded-full text-sm">Paso 1</span>
                    <div class="pt-4">
                        <i class="fa-solid fa-arrow-pointer text-5xl text-amber-600 mb-3 block" aria-hidden="true"></i>
                        <h3 class="font-bold text-xl text-slate-900">Elija su Examen</h3>
                        <p class="text-sm text-slate-700 leading-relaxed mt-2">En la sección "Resultados", haga clic o toque el botón con el nombre de su prueba médica.</p>
                    </div>
                    <button onclick="speakText('Paso 1: Elija su examen. En la sección resultados haga clic sobre el botón de su prueba médica.')" class="w-full bg-white hover:bg-amber-100 border border-amber-300 text-amber-900 font-bold py-2 rounded-lg text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-volume-high" aria-hidden="true"></i> Escuchar Paso 1
                    </button>
                </div>

                <!-- Paso 2 -->
                <div class="bg-blue-50/60 border-2 border-blue-200 rounded-2xl p-6 text-center space-y-3 relative flex flex-col justify-between">
                    <span class="absolute top-3 left-3 bg-blue-600 text-white font-black px-3 py-1 rounded-full text-sm">Paso 2</span>
                    <div class="pt-4">
                        <i class="fa-solid fa-volume-xmark text-5xl text-blue-600 mb-3 block" aria-hidden="true"></i>
                        <h3 class="font-bold text-xl text-slate-900">Escuche la Lectura</h3>
                        <p class="text-sm text-slate-700 leading-relaxed mt-2">Presione el botón amarillo "Escuchar mis resultados". Nuestra voz de voz clara le leerá el informe completo.</p>
                    </div>
                    <button onclick="speakText('Paso 2: Escuche la lectura. Presione el botón amarillo Escuchar mis resultados para oír la explicación en voz alta.')" class="w-full bg-white hover:bg-blue-100 border border-blue-300 text-blue-900 font-bold py-2 rounded-lg text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-volume-high" aria-hidden="true"></i> Escuchar Paso 2
                    </button>
                </div>

                <!-- Paso 3 -->
                <div class="bg-emerald-50/60 border-2 border-emerald-200 rounded-2xl p-6 text-center space-y-3 relative flex flex-col justify-between">
                    <span class="absolute top-3 left-3 bg-emerald-600 text-white font-black px-3 py-1 rounded-full text-sm">Paso 3</span>
                    <div class="pt-4">
                        <i class="fa-solid fa-sliders text-5xl text-emerald-600 mb-3 block" aria-hidden="true"></i>
                        <h3 class="font-bold text-xl text-slate-900">Ajuste la Letra</h3>
                        <p class="text-sm text-slate-700 leading-relaxed mt-2">Si las letras son muy pequeñas, use el apartado "Accesibilidad" para agrandar los textos al tamaño que necesite.</p>
                    </div>
                    <button onclick="speakText('Paso 3: Ajuste la letra. Si las letras son muy pequeñas, ingrese a accesibilidad para agrandar el texto fácilmente.')" class="w-full bg-white hover:bg-emerald-100 border border-emerald-300 text-emerald-900 font-bold py-2 rounded-lg text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-volume-high" aria-hidden="true"></i> Escuchar Paso 3
                    </button>
                </div>
            </div>

            <!-- Acordeón de Preguntas Frecuentes (FAQ) -->
            <div class="space-y-4 pt-4">
                <h3 class="text-xl font-extrabold text-slate-900 flex items-center gap-2">
                    <i class="fa-solid fa-circle-question text-blue-600" aria-hidden="true"></i> Preguntas y Dudas Frecuentes
                </h3>
                
                <div class="space-y-3">
                    <!-- FAQ 1 -->
                    <div class="border-2 border-slate-200 rounded-xl overflow-hidden">
                        <button onclick="toggleFaq('faq-1')" class="w-full bg-slate-50 hover:bg-slate-100 p-4 text-left font-bold text-slate-900 flex justify-between items-center text-base" aria-expanded="false" aria-controls="faq-1">
                            <span>¿Se me cerrará la sesión si me tardo leyendo mis exámenes?</span>
                            <i id="faq-1-icon" class="fa-solid fa-chevron-down text-slate-500" aria-hidden="true"></i>
                        </button>
                        <div id="faq-1" class="hidden p-4 bg-white text-slate-700 text-base leading-relaxed border-t border-slate-200">
                            <strong>No, absolutamente no.</strong> Hemos eliminado el límite de tiempo anterior de 3 minutos. Puede tomarse todas las horas que necesite para revisar sus informes con calma o en compañía de sus familiares.
                        </div>
                    </div>

                    <!-- FAQ 2 -->
                    <div class="border-2 border-slate-200 rounded-xl overflow-hidden">
                        <button onclick="toggleFaq('faq-2')" class="w-full bg-slate-50 hover:bg-slate-100 p-4 text-left font-bold text-slate-900 flex justify-between items-center text-base" aria-expanded="false" aria-controls="faq-2">
                            <span>¿Qué hago si no tengo internet en mi casa?</span>
                            <i id="faq-2-icon" class="fa-solid fa-chevron-down text-slate-500" aria-hidden="true"></i>
                        </button>
                        <div id="faq-2" class="hidden p-4 bg-white text-slate-700 text-base leading-relaxed border-t border-slate-200">
                            La plataforma guarda automáticamente sus últimos estudios en la memoria de su dispositivo. Solamente debe dirigirse al botón <strong>"6. Sin Internet"</strong> en el menú superior para consultarlos en cualquier momento.
                        </div>
                    </div>

                    <!-- FAQ 3 -->
                    <div class="border-2 border-slate-200 rounded-xl overflow-hidden">
                        <button onclick="toggleFaq('faq-3')" class="w-full bg-slate-50 hover:bg-slate-100 p-4 text-left font-bold text-slate-900 flex justify-between items-center text-base" aria-expanded="false" aria-controls="faq-3">
                            <span>¿Cómo funciona el Asistente de IA por Voz?</span>
                            <i id="faq-3-icon" class="fa-solid fa-chevron-down text-slate-500" aria-hidden="true"></i>
                        </button>
                        <div id="faq-3" class="hidden p-4 bg-white text-slate-700 text-base leading-relaxed border-t border-slate-200">
                            En la esquina inferior derecha hay un botón circular con un micrófono. Al presionarlo, puede hablarle al sistema y hacerle preguntas como <i>"Léeme la glucosa"</i> o <i>"Agrandar letra"</i>.
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 3: ENTREGA DE RESULTADOS -->
        <section id="resultados" class="bg-white rounded-3xl p-6 sm:p-10 shadow-xl border border-slate-200 space-y-8" aria-labelledby="heading-resultados">
            <div class="border-b border-slate-200 pb-5 flex flex-wrap justify-between items-center gap-4">
                <div>
                    <h2 id="heading-resultados" class="text-2xl sm:text-3xl font-extrabold text-slate-900 flex items-center gap-3">
                        <span class="w-10 h-10 bg-emerald-100 text-emerald-700 rounded-full flex items-center justify-center text-lg font-bold">3</span>
                        Entrega de Resultados Médicos
                    </h2>
                    <p class="text-slate-600 text-base mt-1">Sin tiempo límite agresivo. Lectura por voz y vista adaptada disponibles.</p>
                </div>

                <!-- Botones de Acción Global de Resultados -->
                <div class="flex flex-wrap gap-2">
                    <button onclick="readCurrentResults()" class="bg-amber-400 hover:bg-amber-300 text-slate-950 font-extrabold px-4 py-2.5 rounded-xl text-sm flex items-center gap-2 shadow transition">
                        <i class="fa-solid fa-volume-high text-lg" aria-hidden="true"></i> Escuchar mis Resultados en Audio
                    </button>
                    <button onclick="downloadAdaptedVersion()" class="bg-slate-800 hover:bg-slate-700 text-white font-bold px-4 py-2.5 rounded-xl text-sm flex items-center gap-2 transition">
                        <i class="fa-solid fa-file-pdf text-red-400 text-lg" aria-hidden="true"></i> Descargar Versión Adaptada
                    </button>
                </div>
            </div>

            <!-- Banner informativo de tiempo ilimitado -->
            <div class="bg-emerald-50 border-2 border-emerald-300 rounded-2xl p-4 flex items-center gap-4">
                <div class="w-12 h-12 rounded-full bg-emerald-600 text-white flex items-center justify-center text-2xl shrink-0">
                    <i class="fa-solid fa-clock-rotate-left" aria-hidden="true"></i>
                </div>
                <div>
                    <h3 class="font-bold text-emerald-950 text-base">Consulta Sin Prisas de Tiempo</h3>
                    <p class="text-sm text-emerald-800">Esta sesión permanecerá activa de forma segura sin desconexiones repentinas.</p>
                </div>
            </div>

            <!-- Tarjeta de Resultados Clínicos -->
            <article class="border-2 border-slate-300 rounded-2xl p-6 bg-slate-50 space-y-6">
                <header class="flex flex-wrap justify-between items-start border-b border-slate-300 pb-4 gap-4">
                    <div>
                        <span class="text-xs font-bold text-blue-700 uppercase tracking-widest block mb-1">Informe Clínico N° LAB-2026-994</span>
                        <h3 class="text-2xl font-extrabold text-slate-900">Examen Completo de Sangre y Perfil Lipídico</h3>
                        <p class="text-xs text-slate-600 mt-1">Fecha de Toma: 05 de Noviembre de 2026 | Solicitado por: Dr. Alejandro Silva</p>
                    </div>
                    <span class="bg-emerald-100 text-emerald-800 font-bold px-3 py-1 rounded-full text-xs border border-emerald-300 flex items-center gap-1.5">
                        <i class="fa-solid fa-check-circle" aria-hidden="true"></i> Validado por Patología
                    </span>
                </header>

                <!-- Tabla de Resultados Accesible -->
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse" aria-label="Resultados del examen de sangre">
                        <thead>
                            <tr class="bg-slate-200 text-slate-900 text-sm font-bold border-b-2 border-slate-400">
                                <th class="p-3">Prueba / Parámetro</th>
                                <th class="p-3">Su Resultado</th>
                                <th class="p-3">Rango de Referencia Normal</th>
                                <th class="p-3">Estado</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-300 text-base">
                            <tr class="hover:bg-white transition">
                                <td class="p-3 font-bold text-slate-900">Glucosa en Ayunas</td>
                                <td class="p-3 font-mono font-bold text-slate-900">92 mg/dL</td>
                                <td class="p-3 text-slate-600">70 - 99 mg/dL</td>
                                <td class="p-3">
                                    <span class="inline-flex items-center gap-1 bg-emerald-100 text-emerald-900 font-bold text-xs px-2.5 py-1 rounded-md border border-emerald-300">
                                        <i class="fa-solid fa-circle text-[8px] text-emerald-600" aria-hidden="true"></i> Normal
                                    </span>
                                </td>
                            </tr>
                            <tr class="hover:bg-white transition">
                                <td class="p-3 font-bold text-slate-900">Colesterol Total</td>
                                <td class="p-3 font-mono font-bold text-amber-900 bg-amber-50 rounded-md">205 mg/dL</td>
                                <td class="p-3 text-slate-600">Deseable menor a 200 mg/dL</td>
                                <td class="p-3">
                                    <span class="inline-flex items-center gap-1 bg-amber-100 text-amber-900 font-bold text-xs px-2.5 py-1 rounded-md border border-amber-300">
                                        <i class="fa-solid fa-triangle-exclamation text-amber-600" aria-hidden="true"></i> Ligeramente Elevado
                                    </span>
                                </td>
                            </tr>
                            <tr class="hover:bg-white transition">
                                <td class="p-3 font-bold text-slate-900">Hemoglobina</td>
                                <td class="p-3 font-mono font-bold text-slate-900">14.2 g/dL</td>
                                <td class="p-3 text-slate-600">12.0 - 15.5 g/dL</td>
                                <td class="p-3">
                                    <span class="inline-flex items-center gap-1 bg-emerald-100 text-emerald-900 font-bold text-xs px-2.5 py-1 rounded-md border border-emerald-300">
                                        <i class="fa-solid fa-circle text-[8px] text-emerald-600" aria-hidden="true"></i> Normal
                                    </span>
                                </td>
                            </tr>
                            <tr class="hover:bg-white transition">
                                <td class="p-3 font-bold text-slate-900">Triglicéridos</td>
                                <td class="p-3 font-mono font-bold text-slate-900">135 mg/dL</td>
                                <td class="p-3 text-slate-600">Menor a 150 mg/dL</td>
                                <td class="p-3">
                                    <span class="inline-flex items-center gap-1 bg-emerald-100 text-emerald-900 font-bold text-xs px-2.5 py-1 rounded-md border border-emerald-300">
                                        <i class="fa-solid fa-circle text-[8px] text-emerald-600" aria-hidden="true"></i> Normal
                                    </span>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>

                <!-- Resumen Médico Simplificado -->
                <div class="bg-white p-5 rounded-xl border border-slate-300 space-y-2">
                    <h4 class="font-bold text-slate-900 text-base flex items-center gap-2">
                        <i class="fa-solid fa-user-doctor text-blue-600" aria-hidden="true"></i> Nota de Interpretación Simplificada del Médico:
                    </h4>
                    <p class="text-slate-700 text-base leading-relaxed">
                        "Estimado(a) paciente: Sus niveles generales de glucosa y sangre se encuentran óptimos. Presenta una elevación leve en el colesterol. Se recomienda mantener caminatas diarias de 20 minutos y reducir el consumo de grasas saturadas."
                    </p>
                </div>
            </article>
        </section>

        <!-- SECCIÓN 4: CAMBIO EN LA ACCESIBILIDAD (PANEL DE CONTROL EN TIEMPO REAL) -->
        <section id="accesibilidad" class="bg-slate-900 text-white rounded-3xl p-6 sm:p-10 shadow-2xl border-4 border-blue-500 space-y-8" aria-labelledby="heading-accesibilidad">
            <div class="border-b border-slate-800 pb-5">
                <div class="flex items-center gap-3">
                    <span class="w-10 h-10 bg-amber-400 text-slate-950 rounded-full flex items-center justify-center text-lg font-black">4</span>
                    <div>
                        <h2 id="heading-accesibilidad" class="text-2xl sm:text-3xl font-extrabold text-white">
                            Panel de Personalización y Accesibilidad
                        </h2>
                        <p class="text-blue-300 text-base mt-1">Ajuste la apariencia visual y la navegación a sus necesidades físicas o visuales.</p>
                    </div>
                </div>
            </div>

            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Control 1: Tamaño de Fuente -->
                <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 space-y-3">
                    <label class="font-bold text-base block text-amber-300 flex items-center gap-2">
                        <i class="fa-solid fa-text-height" aria-hidden="true"></i> Tamaño del Texto
                    </label>
                    <div class="grid grid-cols-3 gap-2">
                        <button onclick="setFontScale('normal')" class="bg-slate-700 hover:bg-slate-600 p-2.5 rounded-lg text-xs font-bold transition focus:ring-2">Normal (100%)</button>
                        <button onclick="setFontScale('large')" class="bg-slate-700 hover:bg-slate-600 p-2.5 rounded-lg text-sm font-bold transition focus:ring-2">Grande (120%)</button>
                        <button onclick="setFontScale('xlarge')" class="bg-slate-700 hover:bg-slate-600 p-2.5 rounded-lg text-base font-bold transition focus:ring-2">Muy Grande (140%)</button>
                    </div>
                </div>

                <!-- Control 2: Modos de Contraste -->
                <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 space-y-3">
                    <label class="font-bold text-base block text-amber-300 flex items-center gap-2">
                        <i class="fa-solid fa-circle-half-stroke" aria-hidden="true"></i> Modos de Contraste
                    </label>
                    <div class="grid grid-cols-2 gap-2 text-xs font-bold">
                        <button onclick="setThemeMode('default')" class="bg-slate-700 hover:bg-slate-600 p-2 rounded-lg transition">Estándar Limpio</button>
                        <button onclick="setThemeMode('high-dark')" class="bg-black text-white border border-yellow-400 p-2 rounded-lg transition">Alto Contraste Oscuro</button>
                        <button onclick="setThemeMode('yellow-black')" class="bg-black text-yellow-300 border border-yellow-300 p-2 rounded-lg transition">Amarillo / Negro</button>
                        <button onclick="setThemeMode('grayscale')" class="bg-slate-500 text-white p-2 rounded-lg transition">Escala de Grises</button>
                    </div>
                </div>

                <!-- Control 3: Tipografía Lectura Fácil / Dislexia -->
                <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 space-y-3">
                    <label class="font-bold text-base block text-amber-300 flex items-center gap-2">
                        <i class="fa-solid fa-font" aria-hidden="true"></i> Tipografía Especial
                    </label>
                    <button id="dyslexia-toggle" onclick="toggleDyslexicFont()" class="w-full bg-slate-700 hover:bg-slate-600 p-3 rounded-lg text-sm font-bold flex justify-between items-center transition">
                        <span>Fuente para Dislexia</span>
                        <span id="dyslexia-status" class="bg-slate-900 text-xs px-2 py-1 rounded">Inactiva</span>
                    </button>
                </div>

                <!-- Control 4: Espaciado de Texto -->
                <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 space-y-3">
                    <label class="font-bold text-base block text-amber-300 flex items-center gap-2">
                        <i class="fa-solid fa-arrows-left-right" aria-hidden="true"></i> Espaciado de Lectura
                    </label>
                    <div class="grid grid-cols-2 gap-2 text-xs font-bold">
                        <button onclick="setSpacing('normal')" class="bg-slate-700 hover:bg-slate-600 p-2.5 rounded-lg transition">Espaciado Normal</button>
                        <button onclick="setSpacing('wide')" class="bg-slate-700 hover:bg-slate-600 p-2.5 rounded-lg transition">Espaciado Amplio</button>
                    </div>
                </div>

                <!-- Control 5: Resaltador de Focus -->
                <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 space-y-3">
                    <label class="font-bold text-base block text-amber-300 flex items-center gap-2">
                        <i class="fa-solid fa-keyboard" aria-hidden="true"></i> Navegación por Teclado
                    </label>
                    <div class="p-3 bg-slate-950 rounded-lg text-xs text-slate-300">
                        Indicador de foco resaltado en amarillo encendido por defecto. Presione la tecla <kbd class="bg-slate-800 px-1.5 py-0.5 rounded text-amber-300 font-mono">TAB</kbd> para navegar.
                    </div>
                </div>

                <!-- Botón Reiniciar Accesibilidad -->
                <div class="bg-slate-800 p-5 rounded-2xl border border-slate-700 flex items-center justify-center">
                    <button onclick="resetAccessibility()" class="w-full bg-red-600 hover:bg-red-500 text-white font-bold p-3 rounded-xl text-sm flex items-center justify-center gap-2 transition">
                        <i class="fa-solid fa-rotate-left" aria-hidden="true"></i> Restaurar Valores por Defecto
                    </button>
                </div>
            </div>
        </section>

  <!-- SECCIÓN 5: CONDICIONES DE USO Y PRIVACIDAD EN LENGUAJE CLARO -->
        <section id="condiciones" class="bg-white rounded-3xl p-6 sm:p-10 shadow-xl border border-slate-200 space-y-8" aria-labelledby="heading-condiciones">
            <div class="border-b border-slate-200 pb-5">
                <h2 id="heading-condiciones" class="text-2xl sm:text-3xl font-extrabold text-slate-900 flex items-center gap-3">
                    <span class="w-10 h-10 bg-purple-100 text-purple-700 rounded-full flex items-center justify-center text-lg font-bold">5</span>
                    Condiciones de Uso y Privacidad Transparente
                </h2>
                <p class="text-slate-600 text-base mt-1">Explicación simple sin términos legales confusos sobre cómo cuidamos sus datos de salud.</p>
            </div>

            <div class="grid md:grid-cols-3 gap-6">
                <!-- Tarjeta 1 -->
                <div class="bg-purple-50/50 border-2 border-purple-200 rounded-2xl p-6 space-y-3">
                    <div class="w-10 h-10 rounded-xl bg-purple-600 text-white flex items-center justify-center text-lg font-bold">
                        <i class="fa-solid fa-user-shield" aria-hidden="true"></i>
                    </div>
                    <h3 class="font-bold text-xl text-slate-900">Sus Datos son Privados</h3>
                    <p class="text-sm text-slate-700 leading-relaxed">
                        Nadie más que usted y su médico tratante tienen autorización para consultar sus informes de laboratorio. No vendemos ni compartimos su información.
                    </p>
                </div>

                <!-- Tarjeta 2 -->
                <div class="bg-purple-50/50 border-2 border-purple-200 rounded-2xl p-6 space-y-3">
                    <div class="w-10 h-10 rounded-xl bg-purple-600 text-white flex items-center justify-center text-lg font-bold">
                        <i class="fa-solid fa-trash-can" aria-hidden="true"></i>
                    </div>
                    <h3 class="font-bold text-xl text-slate-900">Derecho de Supresión</h3>
                    <p class="text-sm text-slate-700 leading-relaxed">
                        Usted puede solicitar en cualquier momento que eliminemos sus respaldos digitales temporales de la plataforma sin costo alguno.
                    </p>
                </div>

                <!-- Tarjeta 3 -->
                <div class="bg-purple-50/50 border-2 border-purple-200 rounded-2xl p-6 space-y-3">
                    <div class="w-10 h-10 rounded-xl bg-purple-600 text-white flex items-center justify-center text-lg font-bold">
                        <i class="fa-solid fa-hospital" aria-hidden="true"></i>
                    </div>
                    <h3 class="font-bold text-xl text-slate-900">Cumplimiento Legal</h3>
                    <p class="text-sm text-slate-700 leading-relaxed">
                        Cumplimos estrictamente con los estándares internacionales HIPAA y GDPR de protección de historiales clínicos.
                    </p>
                </div>
            </div>
        </section>

        <!-- SECCIÓN 6: HISTORIAL SIN INTERNET (RESPALDO LOCAL CACHÉ) -->
        <section id="offline-history" class="bg-white rounded-3xl p-6 sm:p-10 shadow-xl border border-slate-200 space-y-8" aria-labelledby="heading-offline">
            <div class="border-b border-slate-200 pb-5 flex flex-wrap justify-between items-center gap-4">
                <div>
                    <h2 id="heading-offline" class="text-2xl sm:text-3xl font-extrabold text-slate-900 flex items-center gap-3">
                        <span class="w-10 h-10 bg-cyan-100 text-cyan-700 rounded-full flex items-center justify-center text-lg font-bold">6</span>
                        Historial Respaldado Sin Internet
                    </h2>
                    <p class="text-slate-600 text-base mt-1">Consulte sus exámenes guardados localmente aunque falle su señal de hogar.</p>
                </div>

                <!-- Simulador de Estado de Conexión -->
                <div class="flex items-center gap-2 bg-slate-100 p-2 rounded-xl border border-slate-300 text-xs font-bold">
                    <span>Simular Red:</span>
                    <button onclick="toggleNetworkSimulation(true)" id="btn-sim-online" class="bg-emerald-600 text-white px-3 py-1 rounded-lg">Online</button>
                    <button onclick="toggleNetworkSimulation(false)" id="btn-sim-offline" class="bg-slate-300 text-slate-700 px-3 py-1 rounded-lg">Sin Conexión</button>
                </div>
            </div>

            <!-- Banner de Estado de Red -->
            <div id="offline-alert-box" class="bg-cyan-50 border-2 border-cyan-300 rounded-2xl p-4 flex items-center gap-4">
                <div class="w-12 h-12 rounded-full bg-cyan-600 text-white flex items-center justify-center text-xl shrink-0">
                    <i class="fa-solid fa-database" aria-hidden="true"></i>
                </div>
                <div>
                    <h3 class="font-bold text-cyan-950 text-base">Almacenamiento Seguro En Dispositivo</h3>
                    <p id="offline-box-desc" class="text-sm text-cyan-900">Mostrando 3 consultas guardadas en memoria local (Caché sincronizada).</p>
                </div>
            </div>

            <!-- Tarjetas de Consultas Guardadas Off-line -->
            <div class="grid md:grid-cols-3 gap-6">
                <!-- Registro Offline 1 -->
                <div class="border-2 border-slate-200 rounded-2xl p-5 bg-slate-50 space-y-3">
                    <div class="flex justify-between items-start">
                        <span class="text-xs font-bold text-slate-500">12 Oct 2026</span>
                        <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-0.5 rounded">Sincronizado</span>
                    </div>
                    <h4 class="font-bold text-slate-900 text-base">Perfil Tiroideo (TSH, T4)</h4>
                    <p class="text-xs text-slate-600">Resultado: Valores dentro del rango normal. Sin novedades.</p>
                    <button onclick="speakText('Perfil Tiroideo del 12 de Octubre de 2026. Resultado: Valores dentro del rango normal.')" class="w-full bg-white hover:bg-slate-100 border border-slate-300 text-slate-800 font-bold py-2 rounded-lg text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-volume-high text-blue-600" aria-hidden="true"></i> Leer Resumen Local
                    </button>
                </div>

                <!-- Registro Offline 2 -->
                <div class="border-2 border-slate-200 rounded-2xl p-5 bg-slate-50 space-y-3">
                    <div class="flex justify-between items-start">
                        <span class="text-xs font-bold text-slate-500">01 Sep 2026</span>
                        <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-0.5 rounded">Sincronizado</span>
                    </div>
                    <h4 class="font-bold text-slate-900 text-base">Electrolitos en Suero</h4>
                    <p class="text-xs text-slate-600">Resultado: Sodio y Potasio equilibrados.</p>
                    <button onclick="speakText('Electrolitos en Suero del 1 de Septiembre. Resultado: Sodio y potasio equilibrados.')" class="w-full bg-white hover:bg-slate-100 border border-slate-300 text-slate-800 font-bold py-2 rounded-lg text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-volume-high text-blue-600" aria-hidden="true"></i> Leer Resumen Local
                    </button>
                </div>

                <!-- Registro Offline 3 -->
                <div class="border-2 border-slate-200 rounded-2xl p-5 bg-slate-50 space-y-3">
                    <div class="flex justify-between items-start">
                        <span class="text-xs font-bold text-slate-500">15 Jun 2026</span>
                        <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-0.5 rounded">Sincronizado</span>
                    </div>
                    <h4 class="font-bold text-slate-900 text-base">Electrocardiograma</h4>
                    <p class="text-xs text-slate-600">Resultado: Ritmo sinusal regular.</p>
                    <button onclick="speakText('Electrocardiograma del 15 de Junio. Resultado: Ritmo sinusal regular.')" class="w-full bg-white hover:bg-slate-100 border border-slate-300 text-slate-800 font-bold py-2 rounded-lg text-xs flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-volume-high text-blue-600" aria-hidden="true"></i> Leer Resumen Local
                    </button>
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER ACCESIBLE -->
    <footer class="bg-slate-950 text-slate-400 py-10 border-t-4 border-blue-600 mt-16">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center space-y-4">
            <div class="flex justify-center items-center gap-3 text-white font-extrabold text-xl">
                <i class="fa-solid fa-heart-pulse text-blue-500" aria-hidden="true"></i> MiSalud Accesible
            </div>
            <p class="text-sm text-slate-400 max-w-2xl mx-auto">
                Diseñado bajo criterios de Accesibilidad Universal (WCAG 2.1 AAA) para garantizar el derecho a la salud informada para todas las personas.
            </p>
            <p class="text-xs text-slate-600">© 2026 Portal Clínico MiSalud. Todos los derechos reservados.</p>
        </div>
    </footer>

    <!-- COMPONENTE FLOTANTE: ASISTENTE DE IA POR VOZ ACCESIBLE -->
    <div class="fixed bottom-6 right-6 z-50">
        <!-- Botón Flotante Principal -->
        <button id="voice-assistant-btn" onclick="toggleVoiceModal()" class="bg-amber-400 hover:bg-amber-300 text-slate-950 p-4 rounded-full shadow-2xl flex items-center gap-3 font-extrabold transition-all transform hover:scale-105 border-4 border-slate-900 focus:ring-4" aria-label="Abrir Asistente por Voz de Inteligencia Artificial">
            <!-- Indicador animado de micrófono -->
            <div class="relative flex items-center justify-center">
                <span class="absolute inline-flex h-full w-full rounded-full bg-amber-500 opacity-75 animate-ping"></span>
                <i class="fa-solid fa-microphone text-2xl relative z-10" aria-hidden="true"></i>
            </div>
            <span class="hidden sm:inline text-sm">Asistente por Voz</span>
        </button>
    </div>

    <!-- MODAL DEL ASISTENTE POR VOZ -->
    <div id="voice-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden" role="dialog" aria-labelledby="voice-modal-title" aria-modal="true">
        <div class="bg-slate-900 text-white rounded-3xl max-w-lg w-full p-6 sm:p-8 border-4 border-blue-500 shadow-2xl space-y-6">
            <div class="flex justify-between items-center border-b border-slate-800 pb-4">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-full bg-blue-600 flex items-center justify-center text-xl text-white">
                        <i class="fa-solid fa-robot" aria-hidden="true"></i>
                    </div>
                    <div>
                        <h3 id="voice-modal-title" class="font-extrabold text-xl">Asistente Virtual MiSalud</h3>
                        <p class="text-xs text-blue-300">Escuchando Comandos de Voz</p>
                    </div>
                </div>
                <button onclick="toggleVoiceModal()" class="text-slate-400 hover:text-white text-2xl font-bold p-1" aria-label="Cerrar asistente por voz">
                    &times;
                </button>
            </div>

            <!-- Animación de Ondas de Sonido de IA -->
            <div class="bg-slate-950 rounded-2xl p-6 text-center space-y-4 border border-slate-800">
                <div id="wave-container" class="flex justify-center items-end gap-1.5 h-12 my-2">
                    <span class="w-2 bg-amber-400 rounded-full wave-bar h-4"></span>
                    <span class="w-2 bg-amber-400 rounded-full wave-bar h-8"></span>
                    <span class="w-2 bg-amber-400 rounded-full wave-bar h-12"></span>
                    <span class="w-2 bg-amber-400 rounded-full wave-bar h-6"></span>
                    <span class="w-2 bg-amber-400 rounded-full wave-bar h-10"></span>
                </div>
                <p id="voice-assistant-status" class="text-base font-bold text-amber-300">
                    "Presione hablar y haga su consulta en voz alta"
                </p>
            </div>

            <!-- Comandos Rápidos de Ejemplo -->
            <div class="space-y-2">
                <span class="text-xs font-bold text-slate-400 uppercase tracking-wider block">Opciones Rápidas:</span>
                <div class="grid grid-cols-2 gap-2 text-xs">
                    <button onclick="handleVoiceCommand('Léeme los resultados')" class="bg-slate-800 hover:bg-slate-700 p-2.5 rounded-xl text-left border border-slate-700 font-semibold">
                        <i class="fa-solid fa-volume-high text-amber-400 mr-1" aria-hidden="true"></i> "Leer mis resultados"
                    </button>
                    <button onclick="handleVoiceCommand('Agrandar letra')" class="bg-slate-800 hover:bg-slate-700 p-2.5 rounded-xl text-left border border-slate-700 font-semibold">
                        <i class="fa-solid fa-text-height text-blue-400 mr-1" aria-hidden="true"></i> "Agrandar la letra"
                    </button>
                    <button onclick="handleVoiceCommand('Ir a tutorial')" class="bg-slate-800 hover:bg-slate-700 p-2.5 rounded-xl text-left border border-slate-700 font-semibold">
                        <i class="fa-solid fa-circle-question text-emerald-400 mr-1" aria-hidden="true"></i> "Ver tutorial"
                    </button>
                    <button onclick="handleVoiceCommand('Modo alto contraste')" class="bg-slate-800 hover:bg-slate-700 p-2.5 rounded-xl text-left border border-slate-700 font-semibold">
                        <i class="fa-solid fa-circle-half-stroke text-purple-400 mr-1" aria-hidden="true"></i> "Alto contraste"
                    </button>
                </div>
            </div>

            <!-- Control de Micrófono -->
            <button id="listen-toggle-btn" onclick="startSpeechRecognitionSim()" class="w-full bg-blue-600 hover:bg-blue-500 text-white font-extrabold py-3.5 px-4 rounded-xl text-base flex items-center justify-center gap-3 transition shadow-lg">
                <i class="fa-solid fa-microphone text-xl" aria-hidden="true"></i> Tocar para Hablar Ahora
            </button>
        </div>
    </div>

     <!-- JAVASCRIPT ACCESIBLE Y LÓGICA DE APLICACIÓN -->
    <script>
        // Mensajes para lectores de pantalla
        function announceToScreenReader(message) {
            const announcer = document.getElementById('aria-announcer');
            announcer.textContent = message;
        }

        // 1. SÍNTESIS DE VOZ (Web Speech API)
        function speakText(text) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel(); // Detener lecturas previas
                const utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = 'es-ES';
                utterance.rate = 0.9; // Velocidad ligeramente pausada para mayor claridad
                window.speechSynthesis.speak(utterance);
                announceToScreenReader("Leyendo texto en voz alta.");
            } else {
                alert("Su navegador no soporta síntesis de voz automática.");
            }
        }

        // Lectura de Resultados Médicos
        function readCurrentResults() {
            const textoExamen = "Resultados de Examen Completo de Sangre. Glucosa en Ayunas: 92 miligramos por decilitro, Estado Normal. Colesterol Total: 205 miligramos por decilitro, Estado Ligeramente Elevado. Hemoglobina: 14.2 gramos por decilitro, Estado Normal. Nota del Médico: Sus niveles generales están óptimos, se recomienda mantener caminatas diarias.";
            speakText(textoExamen);
        }

        // Descarga de Versión Adaptada
        function downloadAdaptedVersion() {
            announceToScreenReader("Generando informe adaptado para impresión de alta legibilidad.");
            alert("Descargando archivo 'Informe_Clinico_MiSalud_Macrotipo.pdf' optimizado con letra grande y contraste mejorado.");
        }

        // 2. CONTROLES DE ACCESIBILIDAD (JavaScript en tiempo real)
        function setFontScale(scale) {
            const root = document.documentElement;
            if (scale === 'normal') root.style.setProperty('--font-scale', '1rem');
            if (scale === 'large') root.style.setProperty('--font-scale', '1.2rem');
            if (scale === 'xlarge') root.style.setProperty('--font-scale', '1.4rem');
            announceToScreenReader(`Tamaño de letra cambiado a ${scale}`);
        }

        function setThemeMode(mode) {
            document.body.classList.remove('theme-high-dark', 'theme-yellow-black', 'theme-grayscale');
            if (mode === 'high-dark') document.body.classList.add('theme-high-dark');
            if (mode === 'yellow-black') document.body.classList.add('theme-yellow-black');
            if (mode === 'grayscale') document.body.classList.add('theme-grayscale');
            announceToScreenReader(`Modo de contraste ajustado a ${mode}`);
        }

        function toggleDyslexicFont() {
            document.body.classList.toggle('font-dyslexic-mode');
            const isActive = document.body.classList.contains('font-dyslexic-mode');
            document.getElementById('dyslexia-status').innerText = isActive ? 'Activa' : 'Inactiva';
            announceToScreenReader(`Fuente para dislexia ${isActive ? 'activada' : 'desactivada'}`);
        }

        function setSpacing(type) {
            const root = document.documentElement;
            if (type === 'normal') {
                root.style.setProperty('--letter-spacing', '0.02em');
                root.style.setProperty('--line-height', '1.6');
            } else {
                root.style.setProperty('--letter-spacing', '0.08em');
                root.style.setProperty('--line-height', '2.0');
            }
            announceToScreenReader(`Espaciado de texto ${type}`);
        }

        function resetAccessibility() {
            setFontScale('normal');
            setThemeMode('default');
            setSpacing('normal');
            if (document.body.classList.contains('font-dyslexic-mode')) {
                toggleDyslexicFont();
            }
            announceToScreenReader("Valores de accesibilidad restaurados por defecto.");
        }

        // 3. TUTORIAL Y FAQ
        function toggleFaq(id) {
            const content = document.getElementById(id);
            const icon = document.getElementById(`${id}-icon`);
            const isHidden = content.classList.contains('hidden');

            content.classList.toggle('hidden');
            icon.classList.toggle('rotate-180');
            announceToScreenReader(`Respuesta ${isHidden ? 'desplegada' : 'ocultada'}`);
        }

        // 4. BIOMETRÍA SIMULADA
        function simulateBiometric(type) {
            const statusBox = document.getElementById('biometric-status');
            const msg = document.getElementById('biometric-msg');
            statusBox.classList.remove('hidden');
            msg.innerText = `Autenticación de ${type} vinculada exitosamente a la cuenta.`;
            announceToScreenReader(`Biometría de ${type} registrada.`);
        }

        function handleRegister(e) {
            e.preventDefault();
            const nombre = document.getElementById('reg-nombre').value;
            alert(`¡Registro completado con éxito para ${nombre}! Ya puede consultar sus resultados.`);
            announceToScreenReader("Registro de cuenta exitoso.");
        }

        // 5. SIMULADOR DE RED Y HISTORIAL SIN INTERNET
        function toggleNetworkSimulation(isOnline) {
            const statusBar = document.getElementById('network-status-bar');
            const statusText = document.getElementById('network-status-text');
            const alertBox = document.getElementById('offline-alert-box');
            const alertDesc = document.getElementById('offline-box-desc');
            const btnOnline = document.getElementById('btn-sim-online');
            const btnOffline = document.getElementById('btn-sim-offline');

            if (isOnline) {
                statusBar.className = "flex items-center space-x-2 bg-emerald-900/60 text-emerald-300 px-3 py-0.5 rounded-full text-xs font-semibold border border-emerald-500";
                statusText.innerText = "Conexión Estable (Modo Online)";
                alertBox.className = "bg-cyan-50 border-2 border-cyan-300 rounded-2xl p-4 flex items-center gap-4";
                alertDesc.innerText = "Mostrando 3 consultas guardadas en memoria local (Caché sincronizada).";
                btnOnline.className = "bg-emerald-600 text-white px-3 py-1 rounded-lg";
                btnOffline.className = "bg-slate-300 text-slate-700 px-3 py-1 rounded-lg";
                announceToScreenReader("Modo en línea activado.");
            } else {
                statusBar.className = "flex items-center space-x-2 bg-amber-900/60 text-amber-300 px-3 py-0.5 rounded-full text-xs font-semibold border border-amber-500";
                statusText.innerText = "Modo Sin Conexión Activo (Datos Locales)";
                alertBox.className = "bg-amber-50 border-2 border-amber-300 rounded-2xl p-4 flex items-center gap-4";
                alertDesc.innerText = "¡Atención! No hay conexión a internet. Consultando respaldos guardados en este dispositivo.";
                btnOffline.className = "bg-amber-600 text-white px-3 py-1 rounded-lg";
                btnOnline.className = "bg-slate-300 text-slate-700 px-3 py-1 rounded-lg";
                announceToScreenReader("Atención: Modo sin conexión activado. Consultando datos almacenados en caché.");
            }
        }

        // Detectar estado real de red del navegador
        window.addEventListener('online', () => toggleNetworkSimulation(true));
        window.addEventListener('offline', () => toggleNetworkSimulation(false));

        // 6. ASISTENTE DE IA POR VOZ ACCESIBLE
        function toggleVoiceModal() {
            const modal = document.getElementById('voice-modal');
            modal.classList.toggle('hidden');
            const isVisible = !modal.classList.contains('hidden');
            if (isVisible) {
                speakText("Asistente por voz iniciado. ¿En qué le puedo ayudar?");
            } else {
                if ('speechSynthesis' in window) window.speechSynthesis.cancel();
            }
        }

        function handleVoiceCommand(cmd) {
            const status = document.getElementById('voice-assistant-status');
            status.innerText = `Comando recibido: "${cmd}"`;
            
            setTimeout(() => {
                if (cmd.includes('resultados')) {
                    readCurrentResults();
                } else if (cmd.includes('letra')) {
                    setFontScale('large');
                    speakText("He ampliado el tamaño de la letra.");
                } else if (cmd.includes('tutorial')) {
                    window.location.hash = '#tutorial';
                    speakText("Redirigiendo a la sección de tutorial.");
                } else if (cmd.includes('contraste')) {
                    setThemeMode('high-dark');
                    speakText("Modo de alto contraste activado.");
                }
            }, 800);
        }

        function startSpeechRecognitionSim() {
            const status = document.getElementById('voice-assistant-status');
            status.innerText = "Escuchando... Por favor hable claramente.";

             // Si el navegador soporta Web Speech Recognition
            if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
                const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                const recognition = new SpeechRecognition();
                recognition.lang = 'es-ES';
                recognition.start();

                recognition.onresult = function(event) {
                    const speechResult = event.results[0][0].transcript;
                    handleVoiceCommand(speechResult);
                };

                recognition.onerror = function() {
                    status.innerText = "No se detectó sonido. Intente con los botones rápidos.";
                };
            } else {
                // Simulación para entornos sin API de reconocimiento
                setTimeout(() => {
                    handleVoiceCommand('Léeme los resultados');
                }, 2000);
            }
        }

        // Navegación Móvil Hamburguesa
        document.getElementById('mobile-menu-btn').addEventListener('click', function() {
            const navLinks = document.getElementById('nav-links');
            navLinks.classList.toggle('hidden');
        });
    </script>
</body>
</html>
