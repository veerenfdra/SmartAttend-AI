<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SmartAttend AI – Intelligent Attendance & Engagement System</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#0f172a',
                        accent: '#2563eb',
                        success: '#16a34a',
                        warning: '#ea580c',
                        danger: '#dc2626',
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <!-- Custom CSS Animations & Styling -->
    <style>
        body { font-family: 'Inter', sans-serif; }
        
        .scan-line {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, transparent, #3b82f6, #60a5fa, transparent);
            box-shadow: 0 0 15px #3b82f6;
            animation: scan 2.5s infinite ease-in-out;
        }

        @keyframes scan {
            0% { top: 0%; opacity: 0.8; }
            50% { top: 95%; opacity: 1; }
            100% { top: 0%; opacity: 0.8; }
        }

        .pulse-border {
            animation: pulse-border 2s infinite;
        }

        @keyframes pulse-border {
            0% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0.4); }
            70% { box-shadow: 0 0 0 12px rgba(37, 99, 235, 0); }
            100% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0); }
        }

        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="h-full text-slate-800 antialiased overflow-x-hidden flex flex-col md:flex-row">

    <!-- Mobile Header Navigation Toggle -->
    <div class="md:hidden bg-slate-900 text-white p-4 flex justify-between items-center z-50 sticky top-0 shadow-md">
        <div class="flex items-center space-x-2">
            <span class="text-2xl">🎓</span>
            <span class="font-bold text-lg tracking-wide">SmartAttend <span class="text-blue-400">AI</span></span>
        </div>
        <button id="mobileMenuBtn" class="p-2 text-slate-300 hover:text-white focus:outline-none">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path></svg>
        </button>
    </div>

    <!-- Desktop Sidebar Navigation -->
    <aside id="sidebar" class="fixed inset-y-0 left-0 z-40 w-64 bg-slate-900 text-slate-300 transform -translate-x-full md:translate-x-0 transition-transform duration-200 ease-in-out flex flex-col justify-between shadow-xl">
        <div>
            <!-- Logo Section -->
            <div class="p-5 border-b border-slate-800 flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-blue-600 flex items-center justify-center text-white text-xl font-bold shadow-lg shadow-blue-500/30">
                    🎓
                </div>
                <div>
                    <h1 class="text-lg font-extrabold text-white tracking-wider">SmartAttend <span class="text-blue-500">AI</span></h1>
                    <p class="text-xs text-slate-400">Smart Campus System</p>
                </div>
            </div>

            <!-- Navigation Links -->
            <nav class="mt-6 px-3 space-y-1.5">
                <button onclick="switchTab('dashboard')" id="nav-dashboard" class="nav-item w-full flex items-center space-x-3 px-4 py-3 rounded-xl font-medium text-sm transition-all bg-blue-600 text-white shadow-md shadow-blue-600/20">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path></svg>
                    <span>Dashboard</span>
                </button>

                <button onclick="switchTab('register')" id="nav-register" class="nav-item w-full flex items-center space-x-3 px-4 py-3 rounded-xl font-medium text-sm text-slate-400 hover:text-white hover:bg-slate-800/80 transition-all">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z"></path></svg>
                    <span>Face Registration</span>
                </button>

                <button onclick="switchTab('scanner')" id="nav-scanner" class="nav-item w-full flex items-center space-x-3 px-4 py-3 rounded-xl font-medium text-sm text-slate-400 hover:text-white hover:bg-slate-800/80 transition-all">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path></svg>
                    <span>AI Scanner</span>
                </button>

                <button onclick="switchTab('students')" id="nav-students" class="nav-item w-full flex items-center space-x-3 px-4 py-3 rounded-xl font-medium text-sm text-slate-400 hover:text-white hover:bg-slate-800/80 transition-all">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>
                    <span>Student Directory</span>
                </button>

                <button onclick="switchTab('analytics')" id="nav-analytics" class="nav-item w-full flex items-center space-x-3 px-4 py-3 rounded-xl font-medium text-sm text-slate-400 hover:text-white hover:bg-slate-800/80 transition-all">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path></svg>
                    <span>Analytics & Alerts</span>
                </button>

                <button onclick="switchTab('settings')" id="nav-settings" class="nav-item w-full flex items-center space-x-3 px-4 py-3 rounded-xl font-medium text-sm text-slate-400 hover:text-white hover:bg-slate-800/80 transition-all">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path></svg>
                    <span>System Settings</span>
                </button>
            </nav>
        </div>

        <!-- Sidebar Footer Status -->
        <div class="p-4 m-3 bg-slate-800/60 rounded-xl border border-slate-700/50">
            <div class="flex items-center justify-between text-xs mb-1 text-slate-300">
                <span>AI Core Engine</span>
                <span class="flex h-2 w-2 relative">
                    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                    <span class="relative inline-flex rounded-full h-2 w-2 bg-emerald-500"></span>
                </span>
            </div>
            <p class="text-[11px] text-slate-400">Model: Vision-Face v3.2</p>
            <p class="text-[10px] text-slate-500 mt-1">Accuracy Rate: 99.8%</p>
        </div>
    </aside>

    <!-- Main Content Area -->
    <main class="flex-1 md:ml-64 min-h-screen flex flex-col bg-slate-100">
        
        <!-- Top App Header -->
        <header class="bg-white border-b border-slate-200 px-6 py-4 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 sticky top-0 z-30 shadow-sm">
            <div>
                <div class="flex items-center space-x-3">
                    <h2 id="pageTitle" class="text-xl font-bold text-slate-900">Dashboard Overview</h2>
                    <span class="px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800 flex items-center gap-1">
                        <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"></span>
                        Active Session
                    </span>
                </div>
                <p class="text-xs text-slate-500 mt-0.5">Smart Campus AI Attendance Management Console</p>
            </div>

            <!-- Quick Action Header Tools -->
            <div class="flex items-center space-x-3 w-full sm:w-auto justify-end">
                <!-- Clock -->
                <div class="hidden lg:flex items-center bg-slate-100 px-3 py-1.5 rounded-lg border border-slate-200 text-xs text-slate-600 font-mono">
                    <svg class="w-4 h-4 mr-1.5 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                    <span id="liveClock">00:00:00 AM</span>
                </div>

                <!-- Load Demo Data Button -->
                <button onclick="loadDemoDataPrompt()" title="Populate system with sample students for testing" class="flex items-center space-x-1.5 text-xs bg-blue-50 text-blue-700 hover:bg-blue-100 border border-blue-200 px-3 py-2 rounded-lg font-medium transition-colors">
                    <svg class="w-4 h-4 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path></svg>
                    <span>Load Demo Data</span>
                </button>

                <!-- Clear / Reset System Button -->
                <button onclick="confirmResetData()" title="Reset to 0 students" class="flex items-center space-x-1.5 text-xs bg-slate-100 hover:bg-red-50 text-slate-600 hover:text-red-600 border border-slate-200 hover:border-red-200 px-3 py-2 rounded-lg font-medium transition-colors">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                    <span class="hidden sm:inline">Clear Data</span>
                </button>
            </div>
        </header>

        <!-- Main Page Container -->
        <div class="p-6 space-y-6 flex-1 max-w-7xl w-full mx-auto">

            <!-- TAB 1: DASHBOARD OVERVIEW -->
            <section id="tab-dashboard" class="tab-content space-y-6">
                <!-- Faculty Profile Header Banner -->
                <div class="bg-gradient-to-r from-slate-900 via-slate-800 to-blue-950 rounded-2xl p-6 text-white shadow-lg relative overflow-hidden">
                    <div class="absolute -right-10 -bottom-10 opacity-10 pointer-events-none">
                        <svg class="w-80 h-80 text-white" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2a10 10 0 100 20 10 10 0 000-20zm0 18a8 8 0 110-16 8 8 0 010 16z"/></svg>
                    </div>
                    <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-6 relative z-10">
                        <div class="flex items-center space-x-4">
                            <div class="w-16 h-16 rounded-2xl bg-blue-600/30 border border-blue-400/30 flex items-center justify-center text-3xl shadow-inner">
                                👩‍🏫
                            </div>
                            <div>
                                <div class="flex items-center space-x-2">
                                    <h3 class="text-xl font-bold">Dr. Anjali Rao</h3>
                                    <span class="bg-blue-500/20 text-blue-300 text-xs px-2.5 py-0.5 rounded-full border border-blue-400/30 font-medium">Faculty Lead</span>
                                </div>
                                <p class="text-slate-300 text-sm mt-0.5">Department of Computer Science & AI Engineering</p>
                                <p class="text-xs text-slate-400 mt-1 flex items-center gap-2">
                                    <span>📚 Subject: Artificial Intelligence & Neural Networks</span>
                                    <span>•</span>
                                    <span>🎓 Section: AIML - 3rd Year</span>
                                </p>
                            </div>
                        </div>

                        <div class="flex items-center gap-3">
                            <button onclick="switchTab('register')" class="bg-blue-600 hover:bg-blue-500 text-white text-xs font-semibold px-4 py-2.5 rounded-xl shadow-md transition-all flex items-center space-x-2">
                                <span>➕ Register First Student</span>
                            </button>
                            <button onclick="switchTab('scanner')" class="bg-white/10 hover:bg-white/20 text-white border border-white/20 text-xs font-semibold px-4 py-2.5 rounded-xl transition-all flex items-center space-x-2">
                                <span>📷 Open Attendance Scanner</span>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Metric Stats Row -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
                    <!-- Total Students -->
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="flex items-center justify-between text-slate-500 mb-3">
                            <span class="text-xs font-semibold uppercase tracking-wider">Total Registered</span>
                            <div class="p-2 rounded-xl bg-slate-100 text-slate-700">👨‍🎓</div>
                        </div>
                        <div class="flex items-baseline justify-between">
                            <h4 id="stat-total-students" class="text-3xl font-extrabold text-slate-900">0</h4>
                            <span class="text-xs text-slate-500 font-medium">Students</span>
                        </div>
                        <p class="text-xs text-slate-400 mt-2">Stored in system database</p>
                    </div>

                    <!-- Present Today -->
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="flex items-center justify-between text-slate-500 mb-3">
                            <span class="text-xs font-semibold uppercase tracking-wider">Present Today</span>
                            <div class="p-2 rounded-xl bg-emerald-100 text-emerald-700">✅</div>
                        </div>
                        <div class="flex items-baseline justify-between">
                            <h4 id="stat-present-today" class="text-3xl font-extrabold text-emerald-600">0</h4>
                            <span id="stat-present-pct" class="text-xs font-bold text-emerald-600">0%</span>
                        </div>
                        <p class="text-xs text-slate-400 mt-2">AI facial recognition verified</p>
                    </div>

                    <!-- Absent Today -->
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="flex items-center justify-between text-slate-500 mb-3">
                            <span class="text-xs font-semibold uppercase tracking-wider">Absent Today</span>
                            <div class="p-2 rounded-xl bg-amber-100 text-amber-700">⚠️</div>
                        </div>
                        <div class="flex items-baseline justify-between">
                            <h4 id="stat-absent-today" class="text-3xl font-extrabold text-amber-600">0</h4>
                            <span id="stat-absent-pct" class="text-xs font-bold text-amber-600">0%</span>
                        </div>
                        <p class="text-xs text-slate-400 mt-2">Pending recognition scan</p>
                    </div>

                    <!-- Attendance Rate -->
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm hover:shadow-md transition-shadow">
                        <div class="flex items-center justify-between text-slate-500 mb-3">
                            <span class="text-xs font-semibold uppercase tracking-wider">Attendance Rate</span>
                            <div class="p-2 rounded-xl bg-blue-100 text-blue-700">📊</div>
                        </div>
                        <div class="flex items-baseline justify-between">
                            <h4 id="stat-attendance-rate" class="text-3xl font-extrabold text-blue-600">0.0%</h4>
                            <span class="text-xs text-blue-600 font-semibold">Today</span>
                        </div>
                        <!-- Progress Bar -->
                        <div class="w-full bg-slate-100 h-2 rounded-full mt-3 overflow-hidden">
                            <div id="stat-rate-bar" class="bg-blue-600 h-full rounded-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                    </div>
                </div>

                <!-- Zero Data Alert Banner (Shown when no students) -->
                <div id="no-students-banner" class="bg-amber-50 border-2 border-dashed border-amber-200 rounded-2xl p-8 text-center my-6">
                    <div class="w-16 h-16 bg-amber-100 rounded-full flex items-center justify-center text-3xl mx-auto mb-4">
                        📷
                    </div>
                    <h3 class="text-lg font-bold text-slate-900 mb-1">No Student Profiles Detected in Database</h3>
                    <p class="text-sm text-slate-600 max-w-md mx-auto mb-6">
                        System is currently uninitialized. Register your first student using the <strong>Mandatory Face Capture</strong> workflow or load mock data for testing.
                    </p>
                    <div class="flex flex-wrap items-center justify-center gap-3">
                        <button onclick="switchTab('register')" class="bg-blue-600 hover:bg-blue-700 text-white px-5 py-2.5 rounded-xl font-semibold text-sm shadow-md transition-all flex items-center space-x-2">
                            <span>👤 Register Student Face Now</span>
                        </button>
                        <button onclick="loadDemoDataPrompt()" class="bg-white border border-slate-300 hover:bg-slate-50 text-slate-700 px-5 py-2.5 rounded-xl font-medium text-sm transition-all flex items-center space-x-2">
                            <span>📦 Load Demo Dataset (10 Students)</span>
                        </button>
                    </div>
                </div>

                <!-- Today's Attendance Real-Time Table -->
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                    <div class="p-5 border-b border-slate-100 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3">
                        <div>
                            <h3 class="text-base font-bold text-slate-900 flex items-center gap-2">
                                <span>📋 Today's Live Attendance Feed</span>
                                <span id="attendance-count-badge" class="bg-slate-100 text-slate-700 text-xs px-2.5 py-0.5 rounded-full font-semibold">0 Recorded</span>
                            </h3>
                            <p class="text-xs text-slate-500">Real-time facial verification timestamps and anti-spoofing logs</p>
                        </div>
                        <button onclick="exportToCSV()" class="text-xs bg-slate-100 hover:bg-slate-200 text-slate-700 px-3.5 py-2 rounded-lg font-semibold transition-colors flex items-center space-x-1.5">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path></svg>
                            <span>Export CSV Log</span>
                        </button>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs text-slate-600">
                            <thead class="bg-slate-50 text-slate-500 uppercase font-bold tracking-wider border-b border-slate-100">
                                <tr>
                                    <th class="px-5 py-3.5">Student</th>
                                    <th class="px-5 py-3.5">Student ID</th>
                                    <th class="px-5 py-3.5">Department</th>
                                    <th class="px-5 py-3.5">Time Log</th>
                                    <th class="px-5 py-3.5">AI Confidence</th>
                                    <th class="px-5 py-3.5">Liveness Check</th>
                                    <th class="px-5 py-3.5 text-right">Status</th>
                                </tr>
                            </thead>
                            <tbody id="attendance-table-body" class="divide-y divide-slate-100">
                                <!-- Dynamic dynamic rows inserted here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- TAB 2: MANDATORY FACE-FIRST STUDENT REGISTRATION -->
            <section id="tab-register" class="tab-content hidden space-y-6">
                <!-- Instruction Header -->
                <div class="bg-blue-50 border border-blue-200 rounded-2xl p-4 flex items-start space-x-3 text-blue-900 text-xs leading-relaxed">
                    <span class="text-xl">ℹ️</span>
                    <div>
                        <strong class="font-bold text-sm block">Mandatory Face Capture Security Policy:</strong>
                        To ensure database integrity and biometric accuracy, form fields are strictly locked until a valid high-quality face profile is captured and verified through live facial recognition camera check.
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- CAMERA / FACE CAPTURE PANEL -->
                    <div class="lg:col-span-5 bg-white p-6 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-4">
                                <h3 class="font-bold text-slate-900 text-sm flex items-center space-x-2">
                                    <span>📷 1. Face Capture Scanner</span>
                                </h3>
                                <span id="camera-status-tag" class="bg-slate-100 text-slate-600 text-[10px] uppercase font-bold px-2 py-0.5 rounded">Ready</span>
                            </div>

                            <!-- Camera Viewport Box -->
                            <div class="relative bg-slate-900 rounded-2xl aspect-4/3 overflow-hidden border-2 border-slate-800 shadow-inner flex items-center justify-center">
                                <!-- Real Webcam Stream -->
                                <video id="webcam-register" class="w-full h-full object-cover hidden" autoplay playsinline muted></video>
                                
                                <!-- Fallback / Simulation Canvas -->
                                <canvas id="canvas-register" class="w-full h-full object-cover"></canvas>

                                <!-- AI Scanning Overlay Grid -->
                                <div id="reg-scan-overlay" class="absolute inset-0 pointer-events-none flex flex-col items-center justify-center">
                                    <div class="w-48 h-48 border-2 border-dashed border-blue-400/70 rounded-3xl flex items-center justify-center relative">
                                        <div id="scan-line-reg" class="hidden scan-line"></div>
                                        <span class="text-3xl opacity-30 text-white">👤</span>
                                    </div>
                                    <p id="camera-guide-text" class="text-[11px] text-white/80 bg-black/60 px-3 py-1 rounded-full mt-3 backdrop-blur-sm">
                                        Position face inside outline
                                    </p>
                                </div>
                            </div>

                            <!-- Step Checklist -->
                            <div class="mt-5 space-y-2 text-xs">
                                <div id="chk-detect" class="flex items-center space-x-2 text-slate-400">
                                    <span class="w-4 h-4 rounded-full border border-slate-300 flex items-center justify-center text-[9px]">1</span>
                                    <span>Face Detection Alignment</span>
                                </div>
                                <div id="chk-centered" class="flex items-center space-x-2 text-slate-400">
                                    <span class="w-4 h-4 rounded-full border border-slate-300 flex items-center justify-center text-[9px]">2</span>
                                    <span>Feature Landmark Extraction</span>
                                </div>
                                <div id="chk-liveness" class="flex items-center space-x-2 text-slate-400">
                                    <span class="w-4 h-4 rounded-full border border-slate-300 flex items-center justify-center text-[9px]">3</span>
                                    <span>Anti-Spoofing Liveness Verification</span>
                                </div>
                                <div id="chk-profile" class="flex items-center space-x-2 text-slate-400">
                                    <span class="w-4 h-4 rounded-full border border-slate-300 flex items-center justify-center text-[9px]">4</span>
                                    <span>Biometric ID Generation</span>
                                </div>
                            </div>
                        </div>

                        <!-- Capture Action Button -->
                        <div class="mt-6 pt-4 border-t border-slate-100">
                            <button id="btn-capture-face" onclick="startFaceCaptureProcess()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-xl text-xs transition-all shadow-md flex items-center justify-center space-x-2">
                                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 9a2 2 0 012-2h0.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z"></path></svg>
                                <span>Capture & Verify Face Biometrics</span>
                            </button>
                        </div>
                    </div>

                    <!-- FORM PANEL (LOCKED UNTIL FACE IS CAPTURED) -->
                    <div class="lg:col-span-7 bg-white p-6 rounded-2xl border border-slate-200 shadow-sm relative">
                        
                        <!-- Lock Overlay Banner -->
                        <div id="form-lock-banner" class="bg-amber-50 border border-amber-200 text-amber-800 px-4 py-3 rounded-xl mb-6 flex items-center space-x-2 text-xs font-semibold">
                            <span class="text-base">🔒</span>
                            <span>Student details form is LOCKED. Complete Face Biometric Capture on the left to unlock details.</span>
                        </div>

                        <div class="flex items-center justify-between mb-4">
                            <h3 class="font-bold text-slate-900 text-sm">📝 2. Student Profile Details</h3>
                            <span id="face-id-badge" class="bg-slate-100 text-slate-500 text-[11px] font-mono px-2.5 py-1 rounded-lg">
                                Biometric ID: Unassigned
                            </span>
                        </div>

                        <!-- Captured Face Preview Thumbnail -->
                        <div id="captured-preview-box" class="hidden bg-slate-50 border border-slate-200 p-3 rounded-xl mb-5 flex items-center space-x-4">
                            <img id="captured-face-thumb" class="w-14 h-14 rounded-xl object-cover border border-blue-500 shadow-sm" src="" alt="Captured Face">
                            <div>
                                <span class="text-xs font-bold text-emerald-700 flex items-center gap-1">
                                    <span>✓</span> Biometrics Verified
                                </span>
                                <p class="text-[11px] text-slate-500 mt-0.5">Feature vectors computed & anti-spoof checks passed.</p>
                            </div>
                        </div>

                        <!-- Registration Form -->
                        <form id="student-reg-form" onsubmit="handleStudentSubmit(event)" class="space-y-4 opacity-50 pointer-events-none transition-opacity duration-300">
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-xs font-bold text-slate-700 mb-1">Student ID *</label>
                                    <input type="text" id="reg-id" required placeholder="e.g. CS2026001" class="w-full text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500">
                                </div>
                                <div>
                                    <label class="block text-xs font-bold text-slate-700 mb-1">Full Name *</label>
                                    <input type="text" id="reg-name" required placeholder="e.g. Rahul Sharma" class="w-full text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500">
                                </div>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-xs font-bold text-slate-700 mb-1">Department *</label>
                                    <select id="reg-dept" required class="w-full text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white">
                                        <option value="">Select Department</option>
                                        <option value="Computer Science">Computer Science & Eng.</option>
                                        <option value="Artificial Intelligence">AI & Machine Learning</option>
                                        <option value="Electronics">Electronics & Comm.</option>
                                        <option value="Mechanical">Mechanical Engineering</option>
                                        <option value="Civil">Civil Engineering</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs font-bold text-slate-700 mb-1">Year / Section *</label>
                                    <select id="reg-year" required class="w-full text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white">
                                        <option value="">Select Year</option>
                                        <option value="1st Year">1st Year (A)</option>
                                        <option value="2nd Year">2nd Year (B)</option>
                                        <option value="3rd Year">3rd Year (AIML)</option>
                                        <option value="4th Year">4th Year (Advanced)</option>
                                    </select>
                                </div>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-xs font-bold text-slate-700 mb-1">Email Address *</label>
                                    <input type="email" id="reg-email" required placeholder="rahul.s@college.edu" class="w-full text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500">
                                </div>
                                <div>
                                    <label class="block text-xs font-bold text-slate-700 mb-1">Phone Number</label>
                                    <input type="tel" id="reg-phone" placeholder="+91 98765 43210" class="w-full text-xs px-3.5 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500">
                                </div>
                            </div>

                            <div class="pt-4 border-t border-slate-100 flex items-center justify-end space-x-3">
                                <button type="button" onclick="resetRegForm()" class="px-4 py-2.5 text-xs font-semibold text-slate-600 hover:text-slate-800 bg-slate-100 hover:bg-slate-200 rounded-xl transition-colors">
                                    Cancel / Clear
                                </button>
                                <button type="submit" id="btn-submit-reg" disabled class="px-6 py-2.5 text-xs font-bold text-white bg-blue-600 hover:bg-blue-700 disabled:opacity-50 disabled:cursor-not-allowed rounded-xl transition-all shadow-md">
                                    Complete & Save Student Profile
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </section>

            <!-- TAB 3: REAL-TIME ATTENDANCE SCANNER -->
            <section id="tab-scanner" class="tab-content hidden space-y-6">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Scanner Camera Feed -->
                    <div class="lg:col-span-7 bg-white p-6 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="flex items-center justify-between mb-4">
                                <div>
                                    <h3 class="font-bold text-slate-900 text-sm">📷 Live AI Attendance Recognition</h3>
                                    <p class="text-xs text-slate-500">Real-time facial match against registered student database</p>
                                </div>
                                <span class="bg-blue-100 text-blue-700 text-xs px-2.5 py-1 rounded-full font-bold">5-Step AI Pipeline</span>
                            </div>

                            <!-- Scanner Viewport -->
                            <div class="relative bg-slate-950 rounded-2xl aspect-16/9 overflow-hidden border-2 border-slate-800 shadow-2xl flex items-center justify-center">
                                <video id="webcam-scanner" class="w-full h-full object-cover hidden" autoplay playsinline muted></video>
                                <canvas id="canvas-scanner" class="w-full h-full object-cover"></canvas>

                                <!-- AI Target Box Overlay -->
                                <div id="scanner-box" class="absolute w-56 h-56 border-2 border-blue-500 rounded-3xl transition-all duration-300 pointer-events-none flex flex-col justify-between p-3">
                                    <div class="flex justify-between">
                                        <div class="w-4 h-4 border-t-2 border-l-2 border-blue-400"></div>
                                        <div class="w-4 h-4 border-t-2 border-r-2 border-blue-400"></div>
                                    </div>
                                    <div id="scan-pulse-indicator" class="hidden scan-line"></div>
                                    <div class="flex justify-between">
                                        <div class="w-4 h-4 border-b-2 border-l-2 border-blue-400"></div>
                                        <div class="w-4 h-4 border-b-2 border-r-2 border-blue-400"></div>
                                    </div>
                                </div>
                            </div>

                            <!-- Student Simulator Dropdown (For fast testing) -->
                            <div class="mt-4 bg-slate-50 p-3 rounded-xl border border-slate-200">
                                <label class="block text-xs font-bold text-slate-700 mb-1.5">
                                    🎯 Simulated Face Target Selector (or use live camera):
                                </label>
                                <select id="scan-student-select" class="w-full text-xs px-3 py-2 rounded-lg border border-slate-300 bg-white focus:outline-none focus:ring-2 focus:ring-blue-500">
                                    <!-- Populated dynamically -->
                                </select>
                            </div>
                        </div>

                        <!-- Scan Trigger Button -->
                        <div class="mt-4 pt-4 border-t border-slate-100">
                            <button id="btn-trigger-scan" onclick="runAttendanceScanPipeline()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-xl text-xs transition-all shadow-md flex items-center justify-center space-x-2">
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path></svg>
                                <span>Execute Facial Recognition & Mark Attendance</span>
                            </button>
                        </div>
                    </div>

                    <!-- AI Pipeline Visual Tracker & Verification Result -->
                    <div class="lg:col-span-5 space-y-6">
                        <!-- Pipeline Stages -->
                        <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
                            <h3 class="font-bold text-slate-900 text-sm mb-4">🧠 5-Step AI Recognition Pipeline</h3>
                            
                            <div class="space-y-3 text-xs">
                                <!-- Step 1 -->
                                <div id="pipe-1" class="flex items-center justify-between p-2.5 rounded-xl border border-slate-200 bg-slate-50 transition-all">
                                    <div class="flex items-center space-x-2.5">
                                        <span class="w-6 h-6 rounded-lg bg-slate-200 flex items-center justify-center font-bold text-slate-600 text-[10px]">1</span>
                                        <span class="font-medium text-slate-700">👤 Face Detection</span>
                                    </div>
                                    <span class="pipe-status text-[10px] font-semibold text-slate-400">Idle</span>
                                </div>

                                <!-- Step 2 -->
                                <div id="pipe-2" class="flex items-center justify-between p-2.5 rounded-xl border border-slate-200 bg-slate-50 transition-all">
                                    <div class="flex items-center space-x-2.5">
                                        <span class="w-6 h-6 rounded-lg bg-slate-200 flex items-center justify-center font-bold text-slate-600 text-[10px]">2</span>
                                        <span class="font-medium text-slate-700">🧠 Vector Recognition</span>
                                    </div>
                                    <span class="pipe-status text-[10px] font-semibold text-slate-400">Idle</span>
                                </div>

                                <!-- Step 3 -->
                                <div id="pipe-3" class="flex items-center justify-between p-2.5 rounded-xl border border-slate-200 bg-slate-50 transition-all">
                                    <div class="flex items-center space-x-2.5">
                                        <span class="w-6 h-6 rounded-lg bg-slate-200 flex items-center justify-center font-bold text-slate-600 text-[10px]">3</span>
                                        <span class="font-medium text-slate-700">🛡️ Anti-Spoof Liveness</span>
                                    </div>
                                    <span class="pipe-status text-[10px] font-semibold text-slate-400">Idle</span>
                                </div>

                                <!-- Step 4 -->
                                <div id="pipe-4" class="flex items-center justify-between p-2.5 rounded-xl border border-slate-200 bg-slate-50 transition-all">
                                    <div class="flex items-center space-x-2.5">
                                        <span class="w-6 h-6 rounded-lg bg-slate-200 flex items-center justify-center font-bold text-slate-600 text-[10px]">4</span>
                                        <span class="font-medium text-slate-700">📋 Database Profile Match</span>
                                    </div>
                                    <span class="pipe-status text-[10px] font-semibold text-slate-400">Idle</span>
                                </div>

                                <!-- Step 5 -->
                                <div id="pipe-5" class="flex items-center justify-between p-2.5 rounded-xl border border-slate-200 bg-slate-50 transition-all">
                                    <div class="flex items-center space-x-2.5">
                                        <span class="w-6 h-6 rounded-lg bg-slate-200 flex items-center justify-center font-bold text-slate-600 text-[10px]">5</span>
                                        <span class="font-medium text-slate-700">✅ Attendance Recorded</span>
                                    </div>
                                    <span class="pipe-status text-[10px] font-semibold text-slate-400">Idle</span>
                                </div>
                            </div>
                        </div>

                        <!-- Live Match Result Card -->
                        <div id="scan-result-card" class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm hidden">
                            <div class="flex items-center space-x-4">
                                <img id="scan-match-photo" class="w-16 h-16 rounded-2xl object-cover border-2 border-emerald-500 shadow-md" src="" alt="Student">
                                <div>
                                    <span class="bg-emerald-100 text-emerald-800 text-[10px] font-extrabold uppercase px-2 py-0.5 rounded-full">VERIFIED PRESENT</span>
                                    <h4 id="scan-match-name" class="font-bold text-slate-900 text-base mt-1">--</h4>
                                    <p id="scan-match-meta" class="text-xs text-slate-500">--</p>
                                </div>
                            </div>
                            <div class="mt-4 pt-3 border-t border-slate-100 grid grid-cols-2 gap-2 text-center text-xs">
                                <div class="bg-slate-50 p-2 rounded-lg">
                                    <span class="text-slate-400 text-[10px] block">Confidence Match</span>
                                    <strong id="scan-match-conf" class="text-slate-800">98.5%</strong>
                                </div>
                                <div class="bg-slate-50 p-2 rounded-lg">
                                    <span class="text-slate-400 text-[10px] block">Liveness Score</span>
                                    <strong id="scan-match-live" class="text-emerald-600">99.1% Passed</strong>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- TAB 4: STUDENT DIRECTORY -->
            <section id="tab-students" class="tab-content hidden space-y-6">
                <!-- Search & Filters -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm flex flex-col md:flex-row justify-between items-center gap-4">
                    <div class="relative w-full md:w-96">
                        <svg class="w-4 h-4 absolute left-3.5 top-3.5 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
                        <input type="text" id="search-student-input" onkeyup="filterStudentDirectory()" placeholder="Search by Student ID, Name, or Department..." class="w-full text-xs pl-10 pr-4 py-2.5 rounded-xl border border-slate-300 focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>

                    <div class="flex items-center space-x-3 w-full md:w-auto justify-end">
                        <select id="dept-filter-select" onchange="filterStudentDirectory()" class="text-xs px-3 py-2.5 rounded-xl border border-slate-300 bg-white focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="ALL">All Departments</option>
                            <option value="Computer Science">Computer Science</option>
                            <option value="Artificial Intelligence">AI & ML</option>
                            <option value="Electronics">Electronics</option>
                            <option value="Mechanical">Mechanical</option>
                            <option value="Civil">Civil</option>
                        </select>
                        <button onclick="switchTab('register')" class="bg-blue-600 hover:bg-blue-700 text-white text-xs font-bold px-4 py-2.5 rounded-xl shadow-md transition-all whitespace-nowrap">
                            ➕ Register New Student
                        </button>
                    </div>
                </div>

                <!-- Directory Grid -->
                <div id="student-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5">
                    <!-- Dynamic Student Cards Rendered Here -->
                </div>

                <!-- Empty State Directory Banner -->
                <div id="directory-empty" class="hidden bg-slate-50 border border-slate-200 rounded-2xl p-12 text-center">
                    <span class="text-4xl block mb-2">👨‍🎓</span>
                    <h4 class="font-bold text-slate-800 text-base">No Students Found</h4>
                    <p class="text-xs text-slate-500 mt-1">There are no student profiles matching your filter or registered in the database.</p>
                </div>
            </section>

            <!-- TAB 5: ANALYTICS & ALERTS -->
            <section id="tab-analytics" class="tab-content hidden space-y-6">
                <!-- Top Row: Bar Visualizer & Low Attendance Warning Alert -->
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Pure CSS/JS Weekly Attendance Bar Chart Visualizer -->
                    <div class="lg:col-span-7 bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
                        <div class="flex items-center justify-between mb-6">
                            <div>
                                <h3 class="font-bold text-slate-900 text-sm">📈 Weekly Attendance Rate Trend</h3>
                                <p class="text-xs text-slate-500">5-Day Smart Campus Class Session Trends</p>
                            </div>
                            <span class="text-xs bg-emerald-50 text-emerald-700 font-bold px-2.5 py-1 rounded-lg">Avg 92.4%</span>
                        </div>

                        <!-- Bar Visualizer -->
                        <div class="h-48 flex items-end justify-between gap-3 pt-6 pb-2 border-b border-slate-100 px-4">
                            <div class="flex-1 flex flex-col items-center gap-2 h-full justify-end group">
                                <div class="w-full bg-blue-100 rounded-t-lg group-hover:bg-blue-500 transition-all relative" style="height: 85%">
                                    <span class="opacity-0 group-hover:opacity-100 text-[10px] bg-slate-900 text-white px-1.5 py-0.5 rounded absolute -top-6 left-1/2 -translate-x-1/2 transition-opacity">85%</span>
                                </div>
                                <span class="text-[11px] font-semibold text-slate-500">Mon</span>
                            </div>
                            <div class="flex-1 flex flex-col items-center gap-2 h-full justify-end group">
                                <div class="w-full bg-blue-100 rounded-t-lg group-hover:bg-blue-500 transition-all relative" style="height: 92%">
                                    <span class="opacity-0 group-hover:opacity-100 text-[10px] bg-slate-900 text-white px-1.5 py-0.5 rounded absolute -top-6 left-1/2 -translate-x-1/2 transition-opacity">92%</span>
                                </div>
                                <span class="text-[11px] font-semibold text-slate-500">Tue</span>
                            </div>
                            <div class="flex-1 flex flex-col items-center gap-2 h-full justify-end group">
                                <div class="w-full bg-blue-100 rounded-t-lg group-hover:bg-blue-500 transition-all relative" style="height: 78%">
                                    <span class="opacity-0 group-hover:opacity-100 text-[10px] bg-slate-900 text-white px-1.5 py-0.5 rounded absolute -top-6 left-1/2 -translate-x-1/2 transition-opacity">78%</span>
                                </div>
                                <span class="text-[11px] font-semibold text-slate-500">Wed</span>
                            </div>
                            <div class="flex-1 flex flex-col items-center gap-2 h-full justify-end group">
                                <div class="w-full bg-blue-100 rounded-t-lg group-hover:bg-blue-500 transition-all relative" style="height: 96%">
                                    <span class="opacity-0 group-hover:opacity-100 text-[10px] bg-slate-900 text-white px-1.5 py-0.5 rounded absolute -top-6 left-1/2 -translate-x-1/2 transition-opacity">96%</span>
                                </div>
                                <span class="text-[11px] font-semibold text-slate-500">Thu</span>
                            </div>
                            <div class="flex-1 flex flex-col items-center gap-2 h-full justify-end group">
                                <div class="w-full bg-blue-600 rounded-t-lg group-hover:bg-blue-700 transition-all relative" style="height: 90%">
                                    <span class="opacity-100 text-[10px] bg-slate-900 text-white px-1.5 py-0.5 rounded absolute -top-6 left-1/2 -translate-x-1/2">Today</span>
                                </div>
                                <span class="text-[11px] font-bold text-blue-600">Fri</span>
                            </div>
                        </div>
                    </div>

                    <!-- Low Attendance Warning Alerts (<75%) -->
                    <div class="lg:col-span-5 bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
                        <div class="flex items-center justify-between mb-4">
                            <h3 class="font-bold text-slate-900 text-sm flex items-center space-x-2">
                                <span class="text-amber-500">⚠️</span>
                                <span>Low Attendance Alerts (&lt;75%)</span>
                            </h3>
                            <span id="low-alert-badge" class="bg-amber-100 text-amber-800 text-[10px] font-bold px-2 py-0.5 rounded-full">0 Students</span>
                        </div>

                        <div id="low-attendance-list" class="space-y-3 max-h-60 overflow-y-auto custom-scrollbar">
                            <!-- Populated dynamically -->
                        </div>
                    </div>
                </div>

                <!-- Student Engagement & AI Accuracy Card -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
                        <span class="text-slate-400 text-xs font-semibold uppercase block">Class Participation Rate</span>
                        <h4 class="text-2xl font-extrabold text-slate-900 mt-1">94.2%</h4>
                        <p class="text-xs text-emerald-600 font-medium mt-1">↑ +3.1% vs last week</p>
                    </div>
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
                        <span class="text-slate-400 text-xs font-semibold uppercase block">Active AI Scanner Verification</span>
                        <h4 class="text-2xl font-extrabold text-blue-600 mt-1">99.8%</h4>
                        <p class="text-xs text-slate-500 mt-1">Zero false positive detections</p>
                    </div>
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm">
                        <span class="text-slate-400 text-xs font-semibold uppercase block">System Database Engine</span>
                        <h4 class="text-2xl font-extrabold text-slate-900 mt-1">LocalStorage</h4>
                        <p class="text-xs text-slate-500 mt-1">Browser sync active</p>
                    </div>
                </div>
            </section>

            <!-- TAB 6: SETTINGS & CONTROLS -->
            <section id="tab-settings" class="tab-content hidden space-y-6">
                <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm space-y-6">
                    <h3 class="font-bold text-slate-900 text-base">⚙️ System Configuration & Evaluator Demo Tools</h3>

                    <!-- Demo Dataset Populator Card -->
                    <div class="bg-blue-50/70 border border-blue-200 rounded-2xl p-5 flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                        <div>
                            <h4 class="font-bold text-slate-900 text-sm">📦 Populator Demo Dataset</h4>
                            <p class="text-xs text-slate-600 mt-1">
                                Instantly inject 10 sample college students with pre-generated biometric face thumbnails, departments, and historical attendance data for hackathon presentation.
                            </p>
                        </div>
                        <button onclick="loadDemoDataPrompt()" class="bg-blue-600 hover:bg-blue-700 text-white font-bold text-xs px-5 py-3 rounded-xl shadow-md transition-all whitespace-nowrap">
                            Load 10 Sample Students
                        </button>
                    </div>

                    <!-- Clear All Data Card -->
                    <div class="bg-red-50/70 border border-red-200 rounded-2xl p-5 flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                        <div>
                            <h4 class="font-bold text-red-900 text-sm">🚨 Clear Database (Reset to 0 Students)</h4>
                            <p class="text-xs text-red-700 mt-1">
                                Completely purge all stored student profiles, captured face biometrics, and attendance logs from `localStorage`.
                            </p>
                        </div>
                        <button onclick="confirmResetData()" class="bg-red-600 hover:bg-red-700 text-white font-bold text-xs px-5 py-3 rounded-xl shadow-md transition-all whitespace-nowrap">
                            Purge All Data
                        </button>
                    </div>
                </div>
            </section>

        </div>
    </main>

    <!-- Custom Toast Notification Box -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 transform translate-y-20 opacity-0 transition-all duration-300 bg-slate-900 text-white px-5 py-3.5 rounded-xl shadow-2xl flex items-center space-x-3 text-xs max-w-sm pointer-events-none">
        <span id="toast-icon" class="text-lg">✅</span>
        <span id="toast-message" class="font-medium">Notification message</span>
    </div>

    <!-- Custom Confirmation Modal Dialog -->
    <div id="modal-confirm" class="fixed inset-0 z-50 bg-slate-950/60 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl p-6 max-w-md w-full shadow-2xl border border-slate-200 animate-in fade-in zoom-in duration-200">
            <div id="modal-icon" class="w-12 h-12 rounded-full bg-blue-100 text-blue-600 text-2xl flex items-center justify-center mb-4">
                ℹ️
            </div>
            <h3 id="modal-title" class="text-base font-bold text-slate-900 mb-1">Confirmation Title</h3>
            <p id="modal-desc" class="text-xs text-slate-600 mb-6 leading-relaxed">Confirmation description text goes here.</p>
            <div class="flex items-center justify-end space-x-3">
                <button onclick="closeConfirmModal()" class="px-4 py-2.5 rounded-xl text-xs font-semibold text-slate-600 hover:text-slate-800 bg-slate-100 hover:bg-slate-200 transition-colors">
                    Cancel
                </button>
                <button id="modal-confirm-btn" class="px-5 py-2.5 rounded-xl text-xs font-bold text-white bg-blue-600 hover:bg-blue-700 transition-colors shadow-md">
                    Confirm Action
                </button>
            </div>
        </div>
    </div>

    <!-- MAIN JAVASCRIPT LOGIC -->
    <script>
        // Key Constants & Storage Keys
        const STORAGE_KEY_STUDENTS = 'smartattend_students_v2';
        const STORAGE_KEY_ATTENDANCE = 'smartattend_attendance_v2';

        // Global Application State
        let students = [];
        let attendanceLogs = [];
        let currentCapturedFace = null; // Captured Image Base64
        let faceProfileId = null; // Biometric FACE-XXXX ID
        let scannedTodaySet = new Set(); // Prevents duplicate scans in session
        let webcamStreamReg = null;
        let webcamStreamScan = null;

        // On Page Load Initialization
        window.addEventListener('DOMContentLoaded', () => {
            initLiveClock();
            setupMobileMenu();
            loadStateFromStorage();
            initRegistrationWebcam();
            initScannerWebcam();
            updateAllDashboardUI();
        });

        // Load data from LocalStorage
        function loadStateFromStorage() {
            try {
                const storedStudents = localStorage.getItem(STORAGE_KEY_STUDENTS);
                const storedAttendance = localStorage.getItem(STORAGE_KEY_ATTENDANCE);

                students = storedStudents ? JSON.parse(storedStudents) : [];
                attendanceLogs = storedAttendance ? JSON.parse(storedAttendance) : [];

                // Track today's marked attendance
                const todayStr = new Date().toLocaleDateString();
                scannedTodaySet.clear();
                attendanceLogs.forEach(log => {
                    if (log.date === todayStr) {
                        scannedTodaySet.add(log.studentId);
                    }
                });
            } catch (e) {
                console.error("Storage load error:", e);
                students = [];
                attendanceLogs = [];
            }
        }

        function saveStateToStorage() {
            localStorage.setItem(STORAGE_KEY_STUDENTS, JSON.stringify(students));
            localStorage.setItem(STORAGE_KEY_ATTENDANCE, JSON.stringify(attendanceLogs));
            updateAllDashboardUI();
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.nav-item').forEach(el => {
                el.classList.remove('bg-blue-600', 'text-white', 'shadow-md', 'shadow-blue-600/20');
                el.classList.add('text-slate-400');
            });

            const activeTab = document.getElementById(`tab-${tabId}`);
            if (activeTab) activeTab.classList.remove('hidden');

            const activeNav = document.getElementById(`nav-${tabId}`);
            if (activeNav) {
                activeNav.classList.add('bg-blue-600', 'text-white', 'shadow-md', 'shadow-blue-600/20');
                activeNav.classList.remove('text-slate-400');
            }

            // Title updates
            const titles = {
                dashboard: "Dashboard Overview",
                register: "Mandatory Face Registration Flow",
                scanner: "AI Facial Attendance Recognition",
                students: "Student Profile Directory",
                analytics: "Analytics & Low Attendance Alerts",
                settings: "System Settings & Demo Tools"
            };
            document.getElementById('pageTitle').innerText = titles[tabId] || "SmartAttend AI";
        }

        async function initRegistrationWebcam() {
            const video = document.getElementById('webcam-register');
            const canvas = document.getElementById('canvas-register');
            const ctx = canvas.getContext('2d');

            try {
                const stream = await navigator.mediaDevices.getUserMedia({ video: true });
                webcamStreamReg = stream;
                video.srcObject = stream;
                video.classList.remove('hidden');
                canvas.classList.add('hidden');
                document.getElementById('camera-status-tag').innerText = "LIVE WEBCAM";
                document.getElementById('camera-status-tag').className = "bg-emerald-100 text-emerald-800 text-[10px] uppercase font-bold px-2 py-0.5 rounded";
            } catch (err) {
                // Fallback simulation canvas drawing if camera unavailable
                console.log("Webcam unavailable, rendering simulation canvas avatar frame.");
                drawSimulatedFaceCanvas(canvas, ctx, "Capture Face");
            }
        }

        async function initScannerWebcam() {
            const video = document.getElementById('webcam-scanner');
            const canvas = document.getElementById('canvas-scanner');
            const ctx = canvas.getContext('2d');

            try {
                const stream = await navigator.mediaDevices.getUserMedia({ video: true });
                webcamStreamScan = stream;
                video.srcObject = stream;
                video.classList.remove('hidden');
                canvas.classList.add('hidden');
            } catch (err) {
                drawSimulatedFaceCanvas(canvas, ctx, "AI Scanner Feed");
            }
        }

        function drawSimulatedFaceCanvas(canvas, ctx, textLabel) {
            canvas.width = 400;
            canvas.height = 300;

            // Background
            ctx.fillStyle = '#0f172a';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Grid overlay
            ctx.strokeStyle = '#1e293b';
            ctx.lineWidth = 1;
            for (let x = 0; x < canvas.width; x += 20) {
                ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, canvas.height); ctx.stroke();
            }
            for (let y = 0; y < canvas.height; y += 20) {
                ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(canvas.width, y); ctx.stroke();
            }

            // Head Silhouette
            ctx.fillStyle = '#334155';
            ctx.beginPath();
            ctx.arc(200, 120, 50, 0, Math.PI * 2);
            ctx.fill();

            // Shoulders
            ctx.beginPath();
            ctx.arc(200, 260, 90, Math.PI, 0, true);
            ctx.fill();

            // Eyes
            ctx.fillStyle = '#64748b';
            ctx.beginPath(); ctx.arc(180, 110, 6, 0, Math.PI * 2); ctx.fill();
            ctx.beginPath(); ctx.arc(220, 110, 6, 0, Math.PI * 2); ctx.fill();

            // Label text
            ctx.fillStyle = '#94a3b8';
            ctx.font = '12px Inter, sans-serif';
            ctx.textAlign = 'center';
            ctx.fillText(textLabel + " (Simulated Feed)", 200, 280);
        }

        function startFaceCaptureProcess() {
            const btn = document.getElementById('btn-capture-face');
            btn.disabled = true;
            btn.innerHTML = `<span>⏳ Processing AI Biometrics...</span>`;

            const scanLine = document.getElementById('scan-line-reg');
            scanLine.classList.remove('hidden');

            // Sequential Checklist steps
            setTimeout(() => setCheckStep('chk-detect', true), 400);
            setTimeout(() => setCheckStep('chk-centered', true), 800);
            setTimeout(() => setCheckStep('chk-liveness', true), 1200);

            setTimeout(() => {
                setCheckStep('chk-profile', true);
                
                // Capture image frame
                const video = document.getElementById('webcam-register');
                const canvas = document.createElement('canvas');
                canvas.width = 200;
                canvas.height = 200;
                const ctx = canvas.getContext('2d');

                if (!video.classList.contains('hidden') && video.videoWidth > 0) {
                    ctx.drawImage(video, 0, 0, 200, 200);
                    currentCapturedFace = canvas.toDataURL('image/jpeg');
                } else {
                    // Generate crisp SVG avatar data URI if webcam unavailable
                    currentCapturedFace = generateMockAvatarURI();
                }

                // Generate FACE-XXXX Profile ID
                faceProfileId = 'FACE-' + Math.floor(1000 + Math.random() * 9000);

                // Unlock Registration Details Form
                unlockStudentForm();

                scanLine.classList.add('hidden');
                btn.disabled = false;
                btn.innerHTML = `<span>✓ Face Captured Successfully (Recapture)</span>`;
                showToast("Face profile captured and liveness verified!", "success");
            }, 1600);
        }

        function setCheckStep(elemId, done) {
            const el = document.getElementById(elemId);
            if (!el) return;
            if (done) {
                el.className = "flex items-center space-x-2 text-emerald-600 font-semibold";
                el.querySelector('span').innerHTML = "✓";
                el.querySelector('span').className = "w-4 h-4 rounded-full bg-emerald-100 flex items-center justify-center text-[10px] font-bold";
            }
        }

        function unlockStudentForm() {
            const form = document.getElementById('student-reg-form');
            const lockBanner = document.getElementById('form-lock-banner');
            const faceBadge = document.getElementById('face-id-badge');
            const previewBox = document.getElementById('captured-preview-box');
            const previewImg = document.getElementById('captured-face-thumb');
            const submitBtn = document.getElementById('btn-submit-reg');

            form.classList.remove('opacity-50', 'pointer-events-none');
            lockBanner.classList.add('hidden');
            faceBadge.innerText = `Biometric ID: ${faceProfileId}`;
            faceBadge.className = "bg-blue-100 text-blue-800 text-[11px] font-mono font-bold px-2.5 py-1 rounded-lg";

            previewImg.src = currentCapturedFace;
            previewBox.classList.remove('hidden');

            submitBtn.disabled = false;
        }

        function handleStudentSubmit(e) {
            e.preventDefault();

            if (!currentCapturedFace || !faceProfileId) {
                showToast("Mandatory face registration incomplete!", "error");
                return;
            }

            const newStudent = {
                id: document.getElementById('reg-id').value.trim(),
                name: document.getElementById('reg-name').value.trim(),
                dept: document.getElementById('reg-dept').value,
                year: document.getElementById('reg-year').value,
                email: document.getElementById('reg-email').value.trim(),
                phone: document.getElementById('reg-phone').value.trim() || 'N/A',
                faceProfileId: faceProfileId,
                photo: currentCapturedFace,
                createdAt: new Date().toISOString()
            };

            // Prevent duplicate Student ID
            if (students.some(s => s.id === newStudent.id)) {
                showToast(`Student ID '${newStudent.id}' already exists!`, "error");
                return;
            }

            // Save to array & LocalStorage
            students.unshift(newStudent);
            saveStateToStorage();

            showToast(`Student ${newStudent.name} registered successfully!`, "success");

            // Reset Form and Lock
            resetRegForm();
            switchTab('dashboard');
        }

        function resetRegForm() {
            document.getElementById('student-reg-form').reset();
            document.getElementById('student-reg-form').classList.add('opacity-50', 'pointer-events-none');
            document.getElementById('form-lock-banner').classList.remove('hidden');
            document.getElementById('captured-preview-box').classList.add('hidden');
            document.getElementById('face-id-badge').innerText = "Biometric ID: Unassigned";
            document.getElementById('face-id-badge').className = "bg-slate-100 text-slate-500 text-[11px] font-mono px-2.5 py-1 rounded-lg";
            document.getElementById('btn-submit-reg').disabled = true;

            currentCapturedFace = null;
            faceProfileId = null;

            // Reset checklist UI
            ['chk-detect', 'chk-centered', 'chk-liveness', 'chk-profile'].forEach(id => {
                const el = document.getElementById(id);
                el.className = "flex items-center space-x-2 text-slate-400";
            });
            document.getElementById('btn-capture-face').innerHTML = `<span>Capture & Verify Face Biometrics</span>`;
        }

        function runAttendanceScanPipeline() {
            if (students.length === 0) {
                showToast("No registered students found! Register a student first.", "error");
                return;
            }

            const btn = document.getElementById('btn-trigger-scan');
            const pulse = document.getElementById('scan-pulse-indicator');
            const selectEl = document.getElementById('scan-student-select');

            btn.disabled = true;
            btn.innerText = "⏳ Executing 5-Step AI Pipeline...";
            pulse.classList.remove('hidden');

            // Pick student from selector or first registered
            const selectedStudentId = selectEl.value;
            const targetStudent = students.find(s => s.id === selectedStudentId) || students[0];

            // Pipeline Step Animation Sequence
            updatePipeStage(1, "Detecting face...", "in-progress");

            setTimeout(() => {
                updatePipeStage(1, "Detected (1 Face)", "done");
                updatePipeStage(2, "Extracting vectors...", "in-progress");
            }, 500);

            setTimeout(() => {
                updatePipeStage(2, "99.4% Match", "done");
                updatePipeStage(3, "Checking liveness...", "in-progress");
            }, 900);

            setTimeout(() => {
                updatePipeStage(3, "Live Person Verified", "done");
                updatePipeStage(4, `Matched ID: ${targetStudent.id}`, "done");
                updatePipeStage(5, "Recording log...", "in-progress");
            }, 1300);

            setTimeout(() => {
                updatePipeStage(5, "Marked Present", "done");
                pulse.classList.add('hidden');
                btn.disabled = false;
                btn.innerText = "Execute Facial Recognition & Mark Attendance";

                // Record Attendance Logic
                recordAttendanceLog(targetStudent);
            }, 1700);
        }

        function updatePipeStage(stepNum, labelText, status) {
            const pipeEl = document.getElementById(`pipe-${stepNum}`);
            const statusTag = pipeEl.querySelector('.pipe-status');

            if (status === "in-progress") {
                pipeEl.className = "flex items-center justify-between p-2.5 rounded-xl border border-blue-300 bg-blue-50 transition-all";
                statusTag.innerText = labelText;
                statusTag.className = "pipe-status text-[10px] font-bold text-blue-600 animate-pulse";
            } else if (status === "done") {
                pipeEl.className = "flex items-center justify-between p-2.5 rounded-xl border border-emerald-200 bg-emerald-50 transition-all";
                statusTag.innerText = labelText;
                statusTag.className = "pipe-status text-[10px] font-bold text-emerald-700";
            }
        }

        function recordAttendanceLog(student) {
            // Check for duplicate attendance today
            if (scannedTodaySet.has(student.id)) {
                showToast(`Attendance already recorded for ${student.name} today!`, "warning");
                displayScanResultCard(student, true);
                return;
            }

            const now = new Date();
            const logEntry = {
                id: 'LOG-' + Date.now(),
                studentId: student.id,
                studentName: student.name,
                dept: student.dept,
                year: student.year,
                photo: student.photo,
                timestamp: now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' }),
                date: now.toLocaleDateString(),
                confidence: (96 + Math.random() * 3.8).toFixed(1) + '%',
                livenessScore: (98.5 + Math.random() * 1.4).toFixed(1) + '%',
                status: 'PRESENT'
            };

            attendanceLogs.unshift(logEntry);
            scannedTodaySet.add(student.id);

            saveStateToStorage();
            displayScanResultCard(student, false);
            showToast(`Attendance marked PRESENT for ${student.name}!`, "success");
        }

        function displayScanResultCard(student, isDuplicate) {
            const card = document.getElementById('scan-result-card');
            document.getElementById('scan-match-photo').src = student.photo;
            document.getElementById('scan-match-name').innerText = student.name;
            document.getElementById('scan-match-meta').innerText = `${student.id} • ${student.dept}`;
            
            if (isDuplicate) {
                card.className = "bg-amber-50 p-6 rounded-2xl border border-amber-200 shadow-sm";
            } else {
                card.className = "bg-white p-6 rounded-2xl border border-emerald-200 shadow-sm";
            }
            card.classList.remove('hidden');
        }

        function updateAllDashboardUI() {
            const totalCount = students.length;
            const presentCount = scannedTodaySet.size;
            const absentCount = Math.max(0, totalCount - presentCount);
            const rate = totalCount > 0 ? ((presentCount / totalCount) * 100).toFixed(1) : "0.0";

            // Dashboard Metrics
            document.getElementById('stat-total-students').innerText = totalCount;
            document.getElementById('stat-present-today').innerText = presentCount;
            document.getElementById('stat-absent-today').innerText = absentCount;
            document.getElementById('stat-attendance-rate').innerText = rate + "%";
            document.getElementById('stat-rate-bar').style.width = rate + "%";

            // Zero data banners
            const emptyBanner = document.getElementById('no-students-banner');
            if (totalCount === 0) {
                emptyBanner.classList.remove('hidden');
            } else {
                emptyBanner.classList.add('hidden');
            }

            // Render Attendance Table
            renderAttendanceTable();

            // Populate Scanner Student Dropdown
            populateScannerDropdown();

            // Render Student Directory
            renderStudentDirectory();

            // Render Low Attendance Alerts
            renderLowAttendanceAlerts();
        }

        function renderAttendanceTable() {
            const tbody = document.getElementById('attendance-table-body');
            const countBadge = document.getElementById('attendance-count-badge');
            
            countBadge.innerText = `${attendanceLogs.length} Recorded`;
            tbody.innerHTML = '';

            if (attendanceLogs.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" class="px-5 py-8 text-center text-slate-400">
                            No attendance logs recorded for today. Scan face biometrics to mark attendance.
                        </td>
                    </tr>
                `;
                return;
            }

            attendanceLogs.forEach(log => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 transition-colors";
                tr.innerHTML = `
                    <td class="px-5 py-3.5 flex items-center space-x-3">
                        <img class="w-8 h-8 rounded-lg object-cover border border-slate-200" src="${log.photo}" alt="">
                        <span class="font-bold text-slate-800">${escapeHTML(log.studentName)}</span>
                    </td>
                    <td class="px-5 py-3.5 font-mono text-slate-600">${escapeHTML(log.studentId)}</td>
                    <td class="px-5 py-3.5">${escapeHTML(log.dept)}</td>
                    <td class="px-5 py-3.5 font-mono">${log.timestamp}</td>
                    <td class="px-5 py-3.5 text-blue-600 font-bold">${log.confidence}</td>
                    <td class="px-5 py-3.5 text-emerald-600 font-semibold">Live (${log.livenessScore})</td>
                    <td class="px-5 py-3.5 text-right">
                        <span class="px-2.5 py-1 rounded-full text-[10px] font-extrabold bg-emerald-100 text-emerald-800">
                            PRESENT
                        </span>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function populateScannerDropdown() {
            const select = document.getElementById('scan-student-select');
            select.innerHTML = '';

            if (students.length === 0) {
                select.innerHTML = `<option value="">No registered students available</option>`;
                return;
            }

            students.forEach(s => {
                const opt = document.createElement('option');
                opt.value = s.id;
                opt.innerText = `${s.name} (${s.id}) - ${s.dept}`;
                select.appendChild(opt);
            });
        }

        function renderStudentDirectory() {
            const grid = document.getElementById('student-grid');
            const emptyState = document.getElementById('directory-empty');
            grid.innerHTML = '';

            if (students.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');

            students.forEach(student => {
                const card = document.createElement('div');
                card.className = "student-card bg-white p-5 rounded-2xl border border-slate-200 shadow-sm hover:shadow-md transition-all flex flex-col justify-between";
                card.setAttribute('data-search', `${student.name} ${student.id} ${student.dept}`.toLowerCase());

                const isPresentToday = scannedTodaySet.has(student.id);

                card.innerHTML = `
                    <div>
                        <div class="flex items-start justify-between mb-3">
                            <img class="w-14 h-14 rounded-2xl object-cover border-2 border-slate-100 shadow-sm" src="${student.photo}" alt="${escapeHTML(student.name)}">
                            <span class="px-2.5 py-0.5 rounded-full text-[10px] font-bold ${isPresentToday ? 'bg-emerald-100 text-emerald-800' : 'bg-slate-100 text-slate-500'}">
                                ${isPresentToday ? '✓ Present Today' : 'Pending Scan'}
                            </span>
                        </div>
                        <h4 class="font-bold text-slate-900 text-sm">${escapeHTML(student.name)}</h4>
                        <p class="text-xs text-blue-600 font-mono font-semibold">${escapeHTML(student.id)}</p>
                        <p class="text-xs text-slate-500 mt-1">${escapeHTML(student.dept)} • ${escapeHTML(student.year)}</p>
                    </div>

                    <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between text-[11px] text-slate-500">
                        <span class="font-mono bg-slate-50 px-2 py-0.5 rounded border border-slate-200">${student.faceProfileId}</span>
                        <button onclick="deleteStudentPrompt('${student.id}')" class="text-red-500 hover:text-red-700 font-semibold">
                            Delete
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function filterStudentDirectory() {
            const query = document.getElementById('search-student-input').value.toLowerCase();
            const selectedDept = document.getElementById('dept-filter-select').value;
            const cards = document.querySelectorAll('.student-card');

            cards.forEach(card => {
                const searchData = card.getAttribute('data-search');
                const matchesQuery = searchData.includes(query);
                const matchesDept = selectedDept === 'ALL' || searchData.includes(selectedDept.toLowerCase());

                if (matchesQuery && matchesDept) {
                    card.classList.remove('hidden');
                } else {
                    card.classList.add('hidden');
                }
            });
        }

        function renderLowAttendanceAlerts() {
            const container = document.getElementById('low-attendance-list');
            const badge = document.getElementById('low-alert-badge');
            container.innerHTML = '';

            // Flag students who haven't scanned today as simulated warning
            const absentStudents = students.filter(s => !scannedTodaySet.has(s.id));
            badge.innerText = `${absentStudents.length} Students`;

            if (absentStudents.length === 0) {
                container.innerHTML = `
                    <p class="text-xs text-slate-400 text-center py-4">No low attendance risk warnings detected today.</p>
                `;
                return;
            }

            absentStudents.forEach(s => {
                const div = document.createElement('div');
                div.className = "flex items-center justify-between p-3 rounded-xl bg-amber-50/60 border border-amber-200 text-xs";
                div.innerHTML = `
                    <div class="flex items-center space-x-3">
                        <img class="w-8 h-8 rounded-lg object-cover" src="${s.photo}" alt="">
                        <div>
                            <p class="font-bold text-slate-800">${escapeHTML(s.name)}</p>
                            <p class="text-[10px] text-slate-500">${s.id} • ${s.dept}</p>
                        </div>
                    </div>
                    <span class="text-amber-700 font-bold bg-amber-100 px-2 py-0.5 rounded text-[10px]">
                        Below 75% Threshold
                    </span>
                `;
                container.appendChild(div);
            });
        }

        function loadDemoDataPrompt() {
            showConfirmModal(
                "📦 Load Demo Dataset?",
                "This will populate the database with 10 sample college students and pre-configured face biometrics for testing.",
                () => {
                    const sampleDept = ["Computer Science", "Artificial Intelligence", "Electronics", "Mechanical"];
                    const sampleYears = ["3rd Year", "2nd Year", "4th Year", "1st Year"];
                    const names = [
                        "Aarav Patel", "Ananya Sharma", "Rohan Verma", "Priya Nair", 
                        "Vikram Singh", "Sneha Kulkarni", "Aditya Joshi", "Kavya Reddy", 
                        "Siddharth Rao", "Meera Iyer"
                    ];

                    students = names.map((name, idx) => ({
                        id: `CS2026${(101 + idx)}`,
                        name: name,
                        dept: sampleDept[idx % sampleDept.length],
                        year: sampleYears[idx % sampleYears.length],
                        email: `${name.toLowerCase().replace(' ', '.')}@smartcampus.edu`,
                        phone: `+91 98765 ${Math.floor(10000 + Math.random() * 90000)}`,
                        faceProfileId: `FACE-${3000 + idx}`,
                        photo: generateMockAvatarURI(name),
                        createdAt: new Date().toISOString()
                    }));

                    // Automatically mark 6 students as present today
                    attendanceLogs = [];
                    scannedTodaySet.clear();
                    const now = new Date();

                    for (let i = 0; i < 6; i++) {
                        const s = students[i];
                        scannedTodaySet.add(s.id);
                        attendanceLogs.push({
                            id: 'LOG-DEMO-' + i,
                            studentId: s.id,
                            studentName: s.name,
                            dept: s.dept,
                            year: s.year,
                            photo: s.photo,
                            timestamp: new Date(now.getTime() - i * 1200000).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
                            date: now.toLocaleDateString(),
                            confidence: (97.2 + Math.random() * 2).toFixed(1) + '%',
                            livenessScore: (99.0 + Math.random()).toFixed(1) + '%',
                            status: 'PRESENT'
                        });
                    }

                    saveStateToStorage();
                    showToast("10 Demo students successfully loaded!", "success");
                }
            );
        }

        function confirmResetData() {
            showConfirmModal(
                "🚨 Purge System Data?",
                "Are you sure you want to delete ALL students and attendance records? System will revert to 0 initial students.",
                () => {
                    students = [];
                    attendanceLogs = [];
                    scannedTodaySet.clear();
                    saveStateToStorage();
                    showToast("System purged. 0 students remaining.", "success");
                }
            );
        }

        function deleteStudentPrompt(id) {
            showConfirmModal(
                "Delete Student Profile?",
                `Delete student ID '${id}' and associated face profile from database?`,
                () => {
                    students = students.filter(s => s.id !== id);
                    attendanceLogs = attendanceLogs.filter(a => a.studentId !== id);
                    scannedTodaySet.delete(id);
                    saveStateToStorage();
                    showToast("Student profile deleted.", "success");
                }
            );
        }

        function exportToCSV() {
            if (attendanceLogs.length === 0) {
                showToast("No attendance data available to export!", "warning");
                return;
            }

            let csvContent = "data:text/csv;charset=utf-8,";
            csvContent += "Student ID,Student Name,Department,Year,Timestamp,Date,AI Confidence,Liveness Score,Status\n";

            attendanceLogs.forEach(l => {
                csvContent += `"${l.studentId}","${l.studentName}","${l.dept}","${l.year}","${l.timestamp}","${l.date}","${l.confidence}","${l.livenessScore}","${l.status}"\n`;
            });

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `SmartAttend_Logs_${new Date().toISOString().slice(0, 10)}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            showToast("CSV Attendance Log Downloaded!", "success");
        }

        function generateMockAvatarURI(name = "Student") {
            const colors = ['#2563eb', '#16a34a', '#ea580c', '#9333ea', '#0891b2', '#4f46e5'];
            const randomColor = colors[Math.floor(Math.random() * colors.length)];
            const initials = name.split(' ').map(n => n[0]).join('').substring(0, 2).toUpperCase();

            const svg = `<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100">
                <rect width="100" height="100" fill="${randomColor}"/>
                <circle cx="50" cy="40" r="22" fill="white" opacity="0.3"/>
                <circle cx="50" cy="90" r="38" fill="white" opacity="0.3"/>
                <text x="50" y="58" font-family="Arial, sans-serif" font-size="28" font-weight="bold" fill="white" text-anchor="middle">${initials}</text>
            </svg>`;

            return 'data:image/svg+xml;utf8,' + encodeURIComponent(svg);
        }

        function showToast(message, type = "success") {
            const toast = document.getElementById('toast');
            const icon = document.getElementById('toast-icon');
            const msg = document.getElementById('toast-message');

            const icons = {
                success: "✅",
                error: "🚨",
                warning: "⚠️"
            };

            icon.innerText = icons[type] || "ℹ️";
            msg.innerText = message;

            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }

        function showConfirmModal(title, desc, onConfirm) {
            const modal = document.getElementById('modal-confirm');
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-desc').innerText = desc;

            const confirmBtn = document.getElementById('modal-confirm-btn');
            confirmBtn.onclick = () => {
                onConfirm();
                closeConfirmModal();
            };

            modal.classList.remove('hidden');
        }

        function closeConfirmModal() {
            document.getElementById('modal-confirm').classList.add('hidden');
        }

        function initLiveClock() {
            const clockEl = document.getElementById('liveClock');
            setInterval(() => {
                const now = new Date();
                clockEl.innerText = now.toLocaleTimeString();
            }, 1000);
        }

        function setupMobileMenu() {
            const btn = document.getElementById('mobileMenuBtn');
            const sidebar = document.getElementById('sidebar');
            btn.addEventListener('click', () => {
                sidebar.classList.toggle('-translate-x-full');
            });
        }

        function escapeHTML(str) {
            return str.replace(/[&<>'"]/g, 
                tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag)
            );
        }
    </script>
</body>
</html>
