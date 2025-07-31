<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Absensi Digital - MA Bahrul Ulum</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
        .gradient-bg { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .card-shadow { box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        .btn-primary { background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%); }
        .btn-primary:hover { background: linear-gradient(135deg, #4338ca 0%, #6d28d9 100%); }
        .attendance-card { transition: all 0.3s ease; }
        .attendance-card:hover { transform: translateY(-2px); }
        @media print {
            .no-print { display: none !important; }
            body { background: white !important; }
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Login Page -->
    <div id="loginPage" class="min-h-screen gradient-bg flex items-center justify-center p-4 relative overflow-hidden">
        <!-- Background Pattern -->
        <div class="absolute inset-0 opacity-10">
            <div class="absolute top-10 left-10 w-20 h-20 bg-white rounded-full"></div>
            <div class="absolute top-32 right-20 w-16 h-16 bg-white rounded-full"></div>
            <div class="absolute bottom-20 left-32 w-12 h-12 bg-white rounded-full"></div>
            <div class="absolute bottom-40 right-10 w-24 h-24 bg-white rounded-full"></div>
        </div>
        
        <div class="bg-white rounded-3xl card-shadow p-8 w-full max-w-md relative z-10 backdrop-blur-sm bg-white/95">
            <div class="text-center mb-8">
                <div class="relative mb-6">
                    <div class="w-24 h-24 mx-auto bg-gradient-to-br from-indigo-500 to-purple-600 rounded-full flex items-center justify-center shadow-lg">
                        <img src="https://iili.io/F8cTdiP.png" alt="Logo MA Bahrul Ulum" class="w-16 h-16 rounded-full object-cover border-2 border-white">
                    </div>
                    <div class="absolute -top-2 -right-2 w-6 h-6 bg-green-500 rounded-full flex items-center justify-center">
                        <svg class="w-3 h-3 text-white" fill="currentColor" viewBox="0 0 20 20">
                            <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"/>
                        </svg>
                    </div>
                </div>
                <h1 class="text-3xl font-bold bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">MA Bahrul Ulum</h1>
                <p class="text-sm text-gray-600 mb-1">Tajinan - Malang</p>
                <div class="inline-flex items-center px-3 py-1 rounded-full bg-gradient-to-r from-indigo-100 to-purple-100 text-indigo-700 text-sm font-medium">
                    <svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                    </svg>
                    Sistem Absensi Digital
                </div>
            </div>
            
            <form id="loginForm" class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Username</label>
                    <div class="relative">
                        <input type="text" id="username" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Ketik nama guru atau username..." autocomplete="off" oninput="showTeacherSuggestions(this.value)" onfocus="showTeacherSuggestions(this.value)">
                        <div id="teacherSuggestions" class="absolute z-10 w-full bg-white border border-gray-300 rounded-lg shadow-lg mt-1 max-h-60 overflow-y-auto hidden">
                            <!-- Suggestions will be populated here -->
                        </div>
                    </div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                    <input type="password" id="password" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Masukkan password">
                    <div id="passwordHint" class="mt-2 text-sm text-blue-600 hidden">
                        <svg class="w-4 h-4 inline mr-1" fill="currentColor" viewBox="0 0 20 20">
                            <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"/>
                        </svg>
                        <span id="passwordHintText">Password untuk semua guru: <strong>123</strong></span>
                    </div>
                </div>
                
                <button type="submit" class="w-full btn-primary text-white py-3 rounded-lg font-semibold hover:shadow-lg transition-all duration-300">
                    Masuk
                </button>
            </form>
            
            <div id="loginError" class="mt-4 text-red-600 text-sm text-center hidden"></div>
            


            <!-- Islamic Motivation -->
            <div class="mt-4 p-4 bg-gradient-to-r from-green-50 to-blue-50 rounded-lg border border-green-200">
                <div class="text-center">
                    <svg class="w-6 h-6 mx-auto mb-2 text-green-600" fill="currentColor" viewBox="0 0 24 24">
                        <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>
                    </svg>
                    <div id="islamicQuote" class="text-xs text-gray-700 italic mb-1 leading-relaxed"></div>
                    <div id="quoteSource" class="text-xs text-green-600 font-medium"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Main Dashboard -->
    <div id="mainPage" class="hidden min-h-screen bg-gray-50">
        <!-- Header -->
        <header class="bg-white shadow-sm border-b">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center py-4">
                    <div class="flex items-center space-x-4">
                        <img src="https://iili.io/F8cTdiP.png" alt="Logo" class="w-12 h-12 rounded-full object-cover border border-gray-200">
                        <div>
                            <h1 class="text-xl font-bold text-gray-900">MA Bahrul Ulum</h1>
                            <p class="text-sm text-gray-600">Tajinan - Malang</p>
                        </div>
                    </div>
                    <div class="flex items-center space-x-4">
                        <div class="text-right">
                            <p class="text-sm font-medium text-gray-900" id="currentDate"></p>
                            <p class="text-sm text-gray-600" id="currentTime"></p>
                        </div>
                        <button onclick="logout()" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                            Keluar
                        </button>
                    </div>
                </div>
            </div>
        </header>

        <!-- Navigation -->
        <nav class="bg-white shadow-sm">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex space-x-8">
                    <button onclick="showTab('dashboard')" class="nav-tab active py-4 px-2 border-b-2 border-indigo-500 text-indigo-600 font-medium">Dashboard</button>
                    <button onclick="showTab('attendance')" class="nav-tab py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium">Absensi</button>
                    <button onclick="showTab('teachers')" class="nav-tab py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium">Data Guru</button>
                    <button onclick="showTab('reports')" class="nav-tab py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium">Laporan</button>
                    <button onclick="showTab('settings')" class="nav-tab py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium">Pengaturan</button>
                </div>
            </div>
        </nav>

        <!-- Dashboard Tab -->
        <div id="dashboardTab" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                <div class="bg-white rounded-xl card-shadow p-6">
                    <div class="flex items-center">
                        <div class="p-3 rounded-full bg-green-100">
                            <svg class="w-6 h-6 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-600">Hadir Hari Ini</p>
                            <p class="text-2xl font-semibold text-gray-900" id="todayPresent">0</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-xl card-shadow p-6">
                    <div class="flex items-center">
                        <div class="p-3 rounded-full bg-red-100">
                            <svg class="w-6 h-6 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                            </svg>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-600">Tidak Hadir</p>
                            <p class="text-2xl font-semibold text-gray-900" id="todayAbsent">0</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-xl card-shadow p-6">
                    <div class="flex items-center">
                        <div class="p-3 rounded-full bg-blue-100">
                            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                            </svg>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-600">Total Guru</p>
                            <p class="text-2xl font-semibold text-gray-900" id="totalTeachers">0</p>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-xl card-shadow p-6">
                    <div class="flex items-center">
                        <div class="p-3 rounded-full bg-yellow-100">
                            <svg class="w-6 h-6 text-yellow-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                        </div>
                        <div class="ml-4">
                            <p class="text-sm font-medium text-gray-600">Sesi Aktif</p>
                            <p class="text-2xl font-semibold text-gray-900" id="activeSession">-</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Recent Attendance -->
            <div class="bg-white rounded-xl card-shadow">
                <div class="px-6 py-4 border-b border-gray-200">
                    <h3 class="text-lg font-semibold text-gray-900">Absensi Terbaru</h3>
                </div>
                <div class="p-6">
                    <div id="recentAttendance" class="space-y-4">
                        <p class="text-gray-500 text-center py-8">Belum ada data absensi hari ini</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Teachers Tab -->
        <div id="teachersTab" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="bg-white rounded-xl card-shadow p-6">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-lg font-semibold text-gray-900">Manajemen Data Guru</h3>
                    <div class="flex space-x-4">
                        <button onclick="showBroadcastForm()" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg font-medium transition-colors">
                            <svg class="w-4 h-4 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"></path>
                            </svg>
                            Siaran WhatsApp
                        </button>
                        <button onclick="importFromGoogleSheets()" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg font-medium transition-colors">
                            Import dari Google Sheets
                        </button>
                        <button onclick="showAddTeacherForm()" class="btn-primary text-white px-4 py-2 rounded-lg font-medium hover:shadow-lg">
                            Tambah Guru
                        </button>
                    </div>
                </div>

                <!-- Add/Edit Teacher Form -->
                <div id="teacherForm" class="hidden mb-6 p-6 bg-gray-50 rounded-lg">
                    <h4 class="text-lg font-semibold text-gray-900 mb-4" id="formTitle">Tambah Guru Baru</h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Nama Lengkap</label>
                            <input type="text" id="teacherName" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Masukkan nama lengkap">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">NIY</label>
                            <input type="text" id="teacherNiy" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Masukkan NIY">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Mata Pelajaran</label>
                            <input type="text" id="teacherSubject" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Masukkan mata pelajaran">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Username</label>
                            <input type="text" id="teacherUsername" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Username untuk login">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                            <input type="password" id="teacherPassword" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="Password untuk login">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Nomor WhatsApp</label>
                            <input type="text" id="teacherWhatsapp" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent" placeholder="08xxxxxxxxxx">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Status</label>
                            <select id="teacherStatus" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                                <option value="aktif">Aktif</option>
                                <option value="non-aktif">Non-Aktif</option>
                            </select>
                        </div>
                    </div>
                    <div class="mt-6 p-4 bg-blue-50 rounded-lg">
                        <h5 class="text-sm font-semibold text-blue-800 mb-2">Tips Pengisian:</h5>
                        <ul class="text-xs text-blue-700 space-y-1">
                            <li>• Username akan digunakan guru untuk login ke sistem</li>
                            <li>• Password sebaiknya mudah diingat oleh guru</li>
                            <li>• Jika kosong, username akan dibuat otomatis dari nama</li>
                            <li>• Jika kosong, password akan menggunakan NIY</li>
                        </ul>
                    </div>
                    <div class="mt-4 flex justify-end space-x-4">
                        <button onclick="cancelTeacherForm()" class="px-4 py-2 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">
                            Batal
                        </button>
                        <button onclick="saveTeacher()" class="btn-primary text-white px-4 py-2 rounded-lg hover:shadow-lg">
                            Simpan
                        </button>
                    </div>
                </div>

                <!-- Broadcast WhatsApp Form -->
                <div id="broadcastForm" class="hidden mb-6 p-6 bg-gradient-to-r from-green-50 to-blue-50 rounded-lg border border-green-200">
                    <h4 class="text-lg font-semibold text-gray-900 mb-4">📢 Siaran Pesan WhatsApp</h4>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Pilih Penerima</label>
                            <div class="space-y-2">
                                <label class="flex items-center">
                                    <input type="checkbox" id="selectAllTeachers" onchange="toggleAllTeachers()" class="rounded border-gray-300 text-green-600 focus:ring-green-500">
                                    <span class="ml-2 text-sm font-medium text-gray-700">Pilih Semua Guru</span>
                                </label>
                                <div id="teacherCheckboxes" class="max-h-40 overflow-y-auto space-y-1 border border-gray-200 rounded-lg p-3 bg-white">
                                    <!-- Teacher checkboxes will be populated here -->
                                </div>
                            </div>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Pesan</label>
                            <textarea id="broadcastMessage" rows="4" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="Ketik pesan yang akan dikirim..."></textarea>
                            <p class="text-xs text-gray-500 mt-1">Pesan akan dikirim melalui WhatsApp Web ke nomor pribadi masing-masing guru</p>
                        </div>
                        
                        <div class="bg-yellow-50 p-4 rounded-lg">
                            <h5 class="text-sm font-semibold text-yellow-800 mb-2">⚠️ Catatan Penting:</h5>
                            <ul class="text-xs text-yellow-700 space-y-1">
                                <li>• Pastikan WhatsApp Web sudah login di browser</li>
                                <li>• Pesan akan dibuka di tab baru untuk setiap guru</li>
                                <li>• Anda perlu mengirim manual setiap pesan</li>
                                <li>• Gunakan fitur ini dengan bijak</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="mt-6 flex justify-end space-x-4">
                        <button onclick="cancelBroadcast()" class="px-4 py-2 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">
                            Batal
                        </button>
                        <button onclick="sendBroadcast()" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg font-medium">
                            <svg class="w-4 h-4 inline mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"></path>
                            </svg>
                            Kirim Siaran
                        </button>
                    </div>
                </div>

                <!-- Teachers List -->
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">No</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Nama</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">NIY</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Mata Pelajaran</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">WhatsApp</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Username</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Password</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="teachersTableBody" class="bg-white divide-y divide-gray-200">
                            <!-- Teachers will be populated here -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Attendance Tab -->
        <div id="attendanceTab" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="bg-white rounded-xl card-shadow p-6">
                <h3 class="text-lg font-semibold text-gray-900 mb-6">Pilih Sesi Absensi</h3>
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
                    <button onclick="startAttendance('kedatangan')" class="attendance-card bg-gradient-to-r from-blue-500 to-blue-600 text-white p-6 rounded-xl hover:shadow-lg">
                        <div class="text-center">
                            <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"></path>
                            </svg>
                            <h4 class="font-semibold">Kedatangan</h4>
                            <p class="text-sm opacity-90" id="kedatanganTime">07:00 - 07:30</p>
                        </div>
                    </button>
                    
                    <button onclick="startAttendance('pagi')" class="attendance-card bg-gradient-to-r from-green-500 to-green-600 text-white p-6 rounded-xl hover:shadow-lg">
                        <div class="text-center">
                            <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"></path>
                            </svg>
                            <h4 class="font-semibold">Pendampingan Pagi</h4>
                            <p class="text-sm opacity-90" id="pagiTime">07:30 - 08:00</p>
                        </div>
                    </button>
                    
                    <button onclick="startAttendance('kepesantrenan')" class="attendance-card bg-gradient-to-r from-indigo-500 to-indigo-600 text-white p-6 rounded-xl hover:shadow-lg">
                        <div class="text-center">
                            <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 14v3m4-3v3m4-3v3M3 21h18M3 10h18M3 7l9-4 9 4M4 10h16v11H4V10z"></path>
                            </svg>
                            <h4 class="font-semibold">Kepesantrenan</h4>
                            <p class="text-sm opacity-90" id="kepesantrenanTime">08:00 - 08:30</p>
                        </div>
                    </button>
                    
                    <button onclick="startAttendance('wali')" class="attendance-card bg-gradient-to-r from-purple-500 to-purple-600 text-white p-6 rounded-xl hover:shadow-lg">
                        <div class="text-center">
                            <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                            </svg>
                            <h4 class="font-semibold">Pendampingan Wali Kelas</h4>
                            <p class="text-sm opacity-90" id="waliTime">08:30 - 09:00</p>
                        </div>
                    </button>
                    
                    <button onclick="startAttendance('pembelajaran')" class="attendance-card bg-gradient-to-r from-orange-500 to-orange-600 text-white p-6 rounded-xl hover:shadow-lg">
                        <div class="text-center">
                            <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.746 0 3.332.477 4.5 1.253v13C19.832 18.477 18.246 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"></path>
                            </svg>
                            <h4 class="font-semibold">Pembelajaran Kelas</h4>
                            <p class="text-sm opacity-90" id="pembelajaranTime">09:00 - 11:30</p>
                        </div>
                    </button>
                    
                    <button onclick="startAttendance('duhur')" class="attendance-card bg-gradient-to-r from-teal-500 to-teal-600 text-white p-6 rounded-xl hover:shadow-lg">
                        <div class="text-center">
                            <svg class="w-8 h-8 mx-auto mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.111 16.404a5.5 5.5 0 017.778 0M12 20h.01m-7.08-7.071c3.904-3.905 10.236-3.905 14.141 0M1.394 9.393c5.857-5.857 15.355-5.857 21.213 0"></path>
                            </svg>
                            <h4 class="font-semibold">Pendampingan Shalat Duhur</h4>
                            <p class="text-sm opacity-90" id="duhurTime">11:30 - 12:30</p>
                        </div>
                    </button>
                </div>

                <!-- Attendance Form -->
                <div id="attendanceForm" class="hidden">
                    <div class="border-t pt-6">
                        <h4 class="text-lg font-semibold text-gray-900 mb-4">Absensi <span id="sessionTitle"></span></h4>
                        
                        <div class="mb-4 p-4 bg-blue-50 rounded-lg">
                            <p class="text-sm text-blue-800">
                                <span class="font-semibold">Status Lokasi:</span> 
                                <span id="locationStatus" class="font-medium">Memeriksa lokasi...</span>
                            </p>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4" id="teacherList">
                            <!-- Teacher cards will be populated here -->
                        </div>

                        <div class="mt-6 flex justify-end space-x-4">
                            <button onclick="cancelAttendance()" class="px-6 py-2 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">
                                Batal
                            </button>
                            <button onclick="saveAttendance()" class="px-6 py-2 btn-primary text-white rounded-lg hover:shadow-lg">
                                Simpan Absensi
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Reports Tab -->
        <div id="reportsTab" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="bg-white rounded-xl card-shadow p-6">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-lg font-semibold text-gray-900">Laporan Kehadiran</h3>
                    <div class="flex space-x-4">
                        <select id="reportMonth" class="border border-gray-300 rounded-lg px-3 py-2">
                            <option value="0">Januari</option>
                            <option value="1">Februari</option>
                            <option value="2">Maret</option>
                            <option value="3">April</option>
                            <option value="4">Mei</option>
                            <option value="5">Juni</option>
                            <option value="6">Juli</option>
                            <option value="7">Agustus</option>
                            <option value="8">September</option>
                            <option value="9">Oktober</option>
                            <option value="10">November</option>
                            <option value="11">Desember</option>
                        </select>
                        <select id="reportYear" class="border border-gray-300 rounded-lg px-3 py-2">
                            <option value="2024">2024</option>
                            <option value="2025">2025</option>
                        </select>
                        <button onclick="generateReport()" class="btn-primary text-white px-4 py-2 rounded-lg hover:shadow-lg">
                            Tampilkan
                        </button>
                        <button onclick="printReport()" class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg">
                            Cetak
                        </button>
                        <button onclick="exportToGoogleSheets()" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg">
                            Export ke Google Sheets
                        </button>
                    </div>
                </div>

                <div class="mb-6">
                    <div class="flex space-x-4">
                        <button onclick="showReportType('daily')" class="report-tab active px-4 py-2 bg-indigo-500 text-white rounded-lg">Harian</button>
                        <button onclick="showReportType('monthly')" class="report-tab px-4 py-2 bg-gray-200 text-gray-700 rounded-lg hover:bg-gray-300">Bulanan</button>
                    </div>
                </div>

                <div id="reportContent">
                    <p class="text-gray-500 text-center py-8">Pilih bulan dan tahun untuk melihat laporan</p>
                </div>
            </div>
        </div>

        <!-- Settings Tab -->
        <div id="settingsTab" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <!-- Schedule Settings -->
                <div class="bg-white rounded-xl card-shadow p-6">
                    <h3 class="text-lg font-semibold text-gray-900 mb-6">Pengaturan Jadwal Absensi</h3>
                    
                    <div class="space-y-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Hari Aktif</label>
                            <select id="daySelect" class="w-full border border-gray-300 rounded-lg px-3 py-2" onchange="loadDaySchedule()">
                                <option value="senin">Senin</option>
                                <option value="selasa">Selasa</option>
                                <option value="rabu">Rabu</option>
                                <option value="kamis">Kamis</option>
                                <option value="jumat">Jumat</option>
                                <option value="sabtu">Sabtu</option>
                            </select>
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Kedatangan</label>
                                <div class="flex space-x-2">
                                    <input type="time" id="kedatanganStart" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                    <input type="time" id="kedatanganEnd" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Pendampingan Pagi</label>
                                <div class="flex space-x-2">
                                    <input type="time" id="pagiStart" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                    <input type="time" id="pagiEnd" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Kepesantrenan</label>
                                <div class="flex space-x-2">
                                    <input type="time" id="kepesantrenanStart" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                    <input type="time" id="kepesantrenanEnd" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Pendampingan Wali Kelas</label>
                                <div class="flex space-x-2">
                                    <input type="time" id="waliStart" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                    <input type="time" id="waliEnd" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Pembelajaran Kelas</label>
                                <div class="flex space-x-2">
                                    <input type="time" id="pembelajaranStart" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                    <input type="time" id="pembelajaranEnd" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Pendampingan Shalat Duhur</label>
                                <div class="flex space-x-2">
                                    <input type="time" id="duhurStart" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                    <input type="time" id="duhurEnd" class="flex-1 border border-gray-300 rounded-lg px-3 py-2">
                                </div>
                            </div>
                        </div>

                        <button onclick="saveSchedule()" class="w-full btn-primary text-white py-3 rounded-lg font-semibold hover:shadow-lg">
                            Simpan Jadwal
                        </button>
                    </div>
                </div>

                <!-- Location Settings -->
                <div class="bg-white rounded-xl card-shadow p-6">
                    <h3 class="text-lg font-semibold text-gray-900 mb-6">Pengaturan Lokasi</h3>
                    
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Latitude</label>
                            <input type="text" id="schoolLat" value="-8.042800" class="w-full border border-gray-300 rounded-lg px-3 py-2">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Longitude</label>
                            <input type="text" id="schoolLng" value="112.668200" class="w-full border border-gray-300 rounded-lg px-3 py-2">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Radius Toleransi (meter)</label>
                            <input type="number" id="locationRadius" value="100" class="w-full border border-gray-300 rounded-lg px-3 py-2">
                        </div>

                        <button onclick="saveLocationSettings()" class="w-full btn-primary text-white py-3 rounded-lg font-semibold hover:shadow-lg">
                            Simpan Pengaturan Lokasi
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Teacher data - will be loaded from localStorage or default data
        let teachers = JSON.parse(localStorage.getItem('teachersData')) || [
            { id: 1, name: "Drs. H. Abdul Wahab", niy: "196501011990031001", subject: "Bahasa Arab", whatsapp: "081234567801", username: "abdulwahab", password: "123", status: "aktif" },
            { id: 2, name: "Hj. Siti Aminah, S.Pd.I", niy: "197203152005012001", subject: "Al-Qur'an Hadits", whatsapp: "081234567802", username: "sitiaminah", password: "123", status: "aktif" },
            { id: 3, name: "Ahmad Fauzi, S.Pd", niy: "198505102009021001", subject: "Matematika", whatsapp: "081234567803", username: "ahmadfauzi", password: "123", status: "aktif" },
            { id: 4, name: "Fatimah Zahra, S.Pd", niy: "199001152014022001", subject: "Bahasa Indonesia", whatsapp: "081234567804", username: "fatimahzahra", password: "123", status: "aktif" },
            { id: 5, name: "Muhammad Ridwan, S.Pd.I", niy: "198712202011011001", subject: "Fiqih", whatsapp: "081234567805", username: "muhammadridwan", password: "123", status: "aktif" },
            { id: 6, name: "Khadijah, S.Pd", niy: "199205102015022001", subject: "Bahasa Inggris", whatsapp: "081234567806", username: "khadijah", password: "123", status: "aktif" },
            { id: 7, name: "Ali Hassan, S.Pd", niy: "198903152012011001", subject: "Sejarah Kebudayaan Islam", whatsapp: "081234567807", username: "alihassan", password: "123", status: "aktif" },
            { id: 8, name: "Maryam, S.Pd", niy: "199408202016022001", subject: "Akidah Akhlak", whatsapp: "081234567808", username: "maryam", password: "123", status: "aktif" },
            { id: 9, name: "Usman, S.Pd", niy: "198601102010011001", subject: "Fisika", whatsapp: "081234567809", username: "usman", password: "123", status: "aktif" },
            { id: 10, name: "Aisyah, S.Pd", niy: "199512152017022001", subject: "Kimia", whatsapp: "081234567810", username: "aisyah", password: "123", status: "aktif" }
        ];

        // Teacher management variables
        let editingTeacherId = null;

        // Default schedule for each day
        const defaultSchedule = {
            senin: {
                kedatangan: { start: "07:00", end: "07:30" },
                pagi: { start: "07:30", end: "08:00" },
                kepesantrenan: { start: "08:00", end: "08:30" },
                wali: { start: "08:30", end: "09:00" },
                pembelajaran: { start: "09:00", end: "11:30" },
                duhur: { start: "11:30", end: "12:30" }
            },
            selasa: {
                kedatangan: { start: "07:00", end: "07:30" },
                pagi: { start: "07:30", end: "08:00" },
                kepesantrenan: { start: "08:00", end: "08:30" },
                wali: { start: "08:30", end: "09:00" },
                pembelajaran: { start: "09:00", end: "11:30" },
                duhur: { start: "11:30", end: "12:30" }
            },
            rabu: {
                kedatangan: { start: "07:00", end: "07:30" },
                pagi: { start: "07:30", end: "08:00" },
                kepesantrenan: { start: "08:00", end: "08:30" },
                wali: { start: "08:30", end: "09:00" },
                pembelajaran: { start: "09:00", end: "11:30" },
                duhur: { start: "11:30", end: "12:30" }
            },
            kamis: {
                kedatangan: { start: "07:00", end: "07:30" },
                pagi: { start: "07:30", end: "08:00" },
                kepesantrenan: { start: "08:00", end: "08:30" },
                wali: { start: "08:30", end: "09:00" },
                pembelajaran: { start: "09:00", end: "11:30" },
                duhur: { start: "11:30", end: "12:30" }
            },
            jumat: {
                kedatangan: { start: "07:00", end: "07:30" },
                pagi: { start: "07:30", end: "08:00" },
                kepesantrenan: { start: "08:00", end: "08:30" },
                wali: { start: "08:30", end: "09:00" },
                pembelajaran: { start: "09:00", end: "10:30" },
                duhur: { start: "10:30", end: "11:30" }
            },
            sabtu: {
                kedatangan: { start: "07:00", end: "07:30" },
                pagi: { start: "07:30", end: "08:00" },
                kepesantrenan: { start: "08:00", end: "08:30" },
                wali: { start: "08:30", end: "09:00" },
                pembelajaran: { start: "09:00", end: "11:00" },
                duhur: { start: "11:00", end: "12:00" }
            }
        };

        // Global variables
        let currentSession = '';
        let attendanceData = JSON.parse(localStorage.getItem('attendanceData')) || {};
        let scheduleData = JSON.parse(localStorage.getItem('scheduleData')) || defaultSchedule;
        let currentLocation = null;
        let reportType = 'daily';

        // Islamic motivational quotes for teachers
        const islamicQuotes = [
            {
                quote: "وَمَن يَتَّقِ اللَّهَ يَجْعَل لَّهُ مَخْرَجًا وَيَرْزُقْهُ مِنْ حَيْثُ لَا يَحْتَسِبُ",
                translation: "Barangsiapa bertakwa kepada Allah, niscaya Dia akan mengadakan baginya jalan keluar dan memberinya rezeki dari arah yang tiada disangka-sangkanya.",
                source: "QS. At-Talaq: 2-3"
            },
            {
                quote: "إِنَّمَا الْأَعْمَالُ بِالنِّيَّاتِ",
                translation: "Sesungguhnya amal perbuatan itu tergantung pada niatnya.",
                source: "HR. Bukhari"
            },
            {
                quote: "خَيْرُ النَّاسِ أَنْفَعُهُمْ لِلنَّاسِ",
                translation: "Sebaik-baik manusia adalah yang paling bermanfaat bagi manusia lainnya.",
                source: "HR. Ahmad"
            },
            {
                quote: "مَنْ عَلَّمَ عِلْمًا فَلَهُ أَجْرُ مَنْ عَمِلَ بِهِ لَا يَنْقُصُ مِنْ أَجْرِ الْعَامِلِ شَيْئًا",
                translation: "Barangsiapa mengajarkan suatu ilmu, maka baginya pahala orang yang mengamalkannya tanpa mengurangi pahala orang yang mengamalkan sedikitpun.",
                source: "HR. Ibnu Majah"
            },
            {
                quote: "وَقُل رَّبِّ زِدْنِي عِلْمًا",
                translation: "Dan katakanlah: 'Ya Tuhanku, tambahkanlah kepadaku ilmu pengetahuan.'",
                source: "QS. Taha: 114"
            },
            {
                quote: "إِنَّ اللَّهَ لَا يُغَيِّرُ مَا بِقَوْمٍ حَتَّىٰ يُغَيِّرُوا مَا بِأَنفُسِهِمْ",
                translation: "Sesungguhnya Allah tidak mengubah keadaan suatu kaum sehingga mereka mengubah keadaan yang ada pada diri mereka sendiri.",
                source: "QS. Ar-Ra'd: 11"
            },
            {
                quote: "وَمَا تَوْفِيقِي إِلَّا بِاللَّهِ ۚ عَلَيْهِ تَوَكَّلْتُ وَإِلَيْهِ أُنِيبُ",
                translation: "Dan tidak ada taufik bagiku melainkan dengan pertolongan Allah. Hanya kepada-Nya aku bertawakkal dan hanya kepada-Nya aku kembali.",
                source: "QS. Hud: 88"
            }
        ];

        // Display daily Islamic quote
        function displayDailyQuote() {
            const today = new Date();
            const dayOfYear = Math.floor((today - new Date(today.getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24);
            const quoteIndex = dayOfYear % islamicQuotes.length;
            const todayQuote = islamicQuotes[quoteIndex];
            
            document.getElementById('islamicQuote').textContent = todayQuote.translation;
            document.getElementById('quoteSource').textContent = todayQuote.source;
        }

        // Initialize the application
        function init() {
            updateDateTime();
            setInterval(updateDateTime, 1000);
            updateDashboard();
            loadDaySchedule();
            loadTeachersTable();
            
            // Set current month and year in report
            const now = new Date();
            document.getElementById('reportMonth').value = now.getMonth();
            document.getElementById('reportYear').value = now.getFullYear();
        }

        // Initialize login page
        function initLoginPage() {
            displayDailyQuote();
            
            // Hide suggestions when clicking outside
            document.addEventListener('click', function(e) {
                if (!e.target.closest('#username') && !e.target.closest('#teacherSuggestions')) {
                    document.getElementById('teacherSuggestions').classList.add('hidden');
                }
            });
        }

        // Show teacher suggestions for login
        function showTeacherSuggestions(query) {
            const suggestionsDiv = document.getElementById('teacherSuggestions');
            
            if (!query.trim()) {
                // Show all teachers when no query
                const allUsers = [...userAccounts.filter(u => u.role === 'Guru'), 
                                 { username: 'admin', name: 'Admin Sistem', role: 'Administrator' },
                                 { username: 'kepala', name: 'Kepala Sekolah', role: 'Kepala Sekolah' },
                                 { username: 'waka', name: 'Wakil Kepala', role: 'Wakil Kepala' },
                                 { username: 'tata_usaha', name: 'Tata Usaha', role: 'Tata Usaha' }];
                
                let html = '';
                allUsers.forEach(user => {
                    html += `
                        <div class="px-4 py-3 hover:bg-gray-50 cursor-pointer border-b border-gray-100 last:border-b-0" onclick="selectUser('${user.username}', '${user.name}')">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm font-medium text-gray-900">${user.name}</p>
                                    <p class="text-xs text-gray-500">${user.role}</p>
                                </div>
                                <div class="text-right">
                                    <p class="text-xs font-mono text-blue-600">${user.username}</p>
                                    <p class="text-xs text-green-600">${user.role === 'Guru' ? '123' : 'hubungi admin'}</p>
                                </div>
                            </div>
                        </div>
                    `;
                });
                
                suggestionsDiv.innerHTML = html;
                suggestionsDiv.classList.remove('hidden');
                return;
            }
            
            // Filter users based on query
            const filteredUsers = userAccounts.filter(user => 
                user.name.toLowerCase().includes(query.toLowerCase()) || 
                user.username.toLowerCase().includes(query.toLowerCase())
            );
            
            if (filteredUsers.length === 0) {
                suggestionsDiv.innerHTML = '<div class="px-4 py-3 text-sm text-gray-500">Tidak ada hasil ditemukan</div>';
                suggestionsDiv.classList.remove('hidden');
                return;
            }
            
            let html = '';
            filteredUsers.forEach(user => {
                html += `
                    <div class="px-4 py-3 hover:bg-gray-50 cursor-pointer border-b border-gray-100 last:border-b-0" onclick="selectUser('${user.username}', '${user.name}')">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-900">${user.name}</p>
                                <p class="text-xs text-gray-500">${user.role}</p>
                            </div>
                            <div class="text-right">
                                <p class="text-xs font-mono text-blue-600">${user.username}</p>
                                <p class="text-xs text-green-600">${user.role === 'Guru' ? '123' : 'hubungi admin'}</p>
                            </div>
                        </div>
                    </div>
                `;
            });
            
            suggestionsDiv.innerHTML = html;
            suggestionsDiv.classList.remove('hidden');
        }

        // Select user from suggestions
        function selectUser(username, name) {
            document.getElementById('username').value = username;
            document.getElementById('teacherSuggestions').classList.add('hidden');
            
            // Show password hint
            const passwordHint = document.getElementById('passwordHint');
            const passwordHintText = document.getElementById('passwordHintText');
            
            const user = userAccounts.find(u => u.username === username);
            if (user && user.role === 'Guru') {
                passwordHintText.innerHTML = `Password untuk <strong>${name}</strong>: <strong>123</strong>`;
                passwordHint.classList.remove('hidden');
            } else if (user) {
                passwordHintText.innerHTML = `Password untuk <strong>${user.role}</strong>: hubungi admin`;
                passwordHint.classList.remove('hidden');
            } else {
                passwordHint.classList.add('hidden');
            }
            
            // Focus on password field
            document.getElementById('password').focus();
        }

        // Teacher Management Functions
        function loadTeachersTable() {
            const tbody = document.getElementById('teachersTableBody');
            let html = '';
            
            teachers.forEach((teacher, index) => {
                html += `
                    <tr>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${index + 1}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${teacher.name}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${teacher.niy}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${teacher.subject}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                            ${teacher.whatsapp ? `
                                <a href="https://wa.me/62${teacher.whatsapp.replace(/^0/, '')}" target="_blank" class="text-green-600 hover:text-green-800 flex items-center">
                                    <svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 24 24">
                                        <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893A11.821 11.821 0 0020.885 3.382"/>
                                    </svg>
                                    ${teacher.whatsapp}
                                </a>
                            ` : '<span class="text-gray-400">-</span>'}
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-mono text-blue-600">${teacher.username || '-'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-mono text-green-600">
                            <span class="cursor-pointer" onclick="togglePassword(this, '${teacher.password || teacher.niy}')" title="Klik untuk lihat/sembunyikan">
                                ••••••••
                            </span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm">
                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacher.status === 'aktif' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                ${teacher.status === 'aktif' ? 'Aktif' : 'Non-Aktif'}
                            </span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                            <div class="flex space-x-2">
                                <button onclick="editTeacher(${teacher.id})" class="inline-flex items-center px-3 py-1 border border-transparent text-xs font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-colors">
                                    <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
                                    </svg>
                                    Edit
                                </button>
                                <button onclick="deleteTeacher(${teacher.id})" class="inline-flex items-center px-3 py-1 border border-transparent text-xs font-medium rounded-md text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500 transition-colors">
                                    <svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                                    </svg>
                                    Hapus
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            });
            
            tbody.innerHTML = html;
        }

        // Toggle password visibility
        function togglePassword(element, password) {
            if (element.textContent === '••••••••') {
                element.textContent = password;
                element.title = 'Klik untuk sembunyikan';
            } else {
                element.textContent = '••••••••';
                element.title = 'Klik untuk lihat/sembunyikan';
            }
        }

        function showAddTeacherForm() {
            document.getElementById('formTitle').textContent = 'Tambah Guru Baru';
            document.getElementById('teacherForm').classList.remove('hidden');
            clearTeacherForm();
            editingTeacherId = null;
        }

        function editTeacher(teacherId) {
            const teacher = teachers.find(t => t.id === teacherId);
            if (teacher) {
                document.getElementById('formTitle').textContent = 'Edit Data Guru';
                document.getElementById('teacherName').value = teacher.name;
                document.getElementById('teacherNiy').value = teacher.niy;
                document.getElementById('teacherSubject').value = teacher.subject;
                document.getElementById('teacherWhatsapp').value = teacher.whatsapp || '';
                document.getElementById('teacherUsername').value = teacher.username || '';
                document.getElementById('teacherPassword').value = teacher.password || '';
                document.getElementById('teacherStatus').value = teacher.status;
                document.getElementById('teacherForm').classList.remove('hidden');
                editingTeacherId = teacherId;
            }
        }

        function deleteTeacher(teacherId) {
            if (confirm('Apakah Anda yakin ingin menghapus data guru ini?')) {
                teachers = teachers.filter(t => t.id !== teacherId);
                saveTeachersData();
                loadTeachersTable();
                updateDashboard();
                alert('Data guru berhasil dihapus!');
            }
        }

        function saveTeacher() {
            const name = document.getElementById('teacherName').value.trim();
            const niy = document.getElementById('teacherNiy').value.trim();
            const subject = document.getElementById('teacherSubject').value.trim();
            const whatsapp = document.getElementById('teacherWhatsapp').value.trim();
            let username = document.getElementById('teacherUsername').value.trim();
            let password = document.getElementById('teacherPassword').value.trim();
            const status = document.getElementById('teacherStatus').value;

            if (!name || !niy || !subject) {
                alert('Mohon lengkapi semua field yang diperlukan!');
                return;
            }

            // Auto-generate username if empty
            if (!username) {
                username = name
                    .replace(/^(Drs?\.|Dr\.|Hj\.|H\.|Prof\.|Ir\.)\s*/gi, '') // Remove titles
                    .replace(/,\s*(S\.Pd\.?I?|M\.Pd\.?I?|M\.A|S\.Ag|S\.Si|S\.Sos|M\.Si|Lc\.?)$/gi, '') // Remove degrees
                    .toLowerCase()
                    .replace(/[^a-z\s]/g, '') // Remove non-alphabetic characters except spaces
                    .replace(/\s+/g, '') // Remove all spaces
                    .substring(0, 20); // Limit length
            }

            // Use simple password if empty
            if (!password) {
                password = '123';
            }

            // Check if username already exists (for other teachers)
            const existingTeacher = teachers.find(t => t.username === username && t.id !== editingTeacherId);
            if (existingTeacher) {
                alert('Username sudah digunakan! Silakan gunakan username lain.');
                return;
            }

            if (editingTeacherId) {
                // Edit existing teacher
                const teacherIndex = teachers.findIndex(t => t.id === editingTeacherId);
                if (teacherIndex !== -1) {
                    const oldUsername = teachers[teacherIndex].username;
                    teachers[teacherIndex] = {
                        ...teachers[teacherIndex],
                        name: name,
                        niy: niy,
                        subject: subject,
                        whatsapp: whatsapp,
                        username: username,
                        password: password,
                        status: status
                    };

                    // Update user account if username changed
                    const userIndex = userAccounts.findIndex(u => u.username === oldUsername);
                    if (userIndex !== -1) {
                        userAccounts[userIndex] = {
                            ...userAccounts[userIndex],
                            username: username,
                            password: password,
                            name: name
                        };
                    }
                }
            } else {
                // Add new teacher
                const newId = Math.max(...teachers.map(t => t.id), 0) + 1;
                teachers.push({
                    id: newId,
                    name: name,
                    niy: niy,
                    subject: subject,
                    whatsapp: whatsapp,
                    username: username,
                    password: password,
                    status: status
                });

                // Add to user accounts for login
                userAccounts.push({
                    username: username,
                    password: password,
                    role: 'Guru',
                    name: name
                });
            }

            saveTeachersData();
            saveUserAccounts();
            loadTeachersTable();
            cancelTeacherForm();
            updateDashboard();
            alert('Data guru berhasil disimpan!');
        }

        function cancelTeacherForm() {
            document.getElementById('teacherForm').classList.add('hidden');
            clearTeacherForm();
            editingTeacherId = null;
        }

        function clearTeacherForm() {
            document.getElementById('teacherName').value = '';
            document.getElementById('teacherNiy').value = '';
            document.getElementById('teacherSubject').value = '';
            document.getElementById('teacherWhatsapp').value = '';
            document.getElementById('teacherUsername').value = '';
            document.getElementById('teacherPassword').value = '';
            document.getElementById('teacherStatus').value = 'aktif';
        }

        function saveTeachersData() {
            localStorage.setItem('teachersData', JSON.stringify(teachers));
        }

        async function importFromGoogleSheets() {
            if (!confirm('Import data akan mengambil data guru dari Google Sheets dan membuat akun login untuk setiap guru. Lanjutkan?')) {
                return;
            }

            try {
                // Show loading message
                const loadingMsg = document.createElement('div');
                loadingMsg.innerHTML = `
                    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
                        <div class="bg-white rounded-lg p-6 max-w-sm w-full mx-4">
                            <div class="text-center">
                                <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-indigo-600 mx-auto mb-4"></div>
                                <p class="text-gray-700">Mengambil data dari Google Sheets...</p>
                            </div>
                        </div>
                    </div>
                `;
                document.body.appendChild(loadingMsg);

                // Convert Google Sheets sharing link to CSV export link
                const sheetId = '1M1G43srbp5UG9Zk0598vXLRHpuiPIFqS';
                const csvUrl = `https://docs.google.com/spreadsheets/d/${sheetId}/export?format=csv&gid=0`;
                
                // Fetch data from Google Sheets
                const response = await fetch(csvUrl);
                const csvText = await response.text();
                
                // Parse CSV data
                const lines = csvText.split('\n');
                const headers = lines[0].split(',').map(h => h.replace(/"/g, '').trim());
                
                const importedData = [];
                for (let i = 1; i < lines.length; i++) {
                    if (lines[i].trim()) {
                        const values = lines[i].split(',').map(v => v.replace(/"/g, '').trim());
                        if (values.length >= 3 && values[0] && values[1] && values[2]) {
                            // Generate username from name (lowercase, no spaces, no titles)
                            const cleanName = values[0]
                                .replace(/^(Drs?\.|Dr\.|Hj\.|H\.|Prof\.|Ir\.)\s*/gi, '') // Remove titles
                                .replace(/,\s*(S\.Pd\.?I?|M\.Pd\.?I?|M\.A|S\.Ag|S\.Si|S\.Sos|M\.Si|Lc\.?)$/gi, '') // Remove degrees
                                .toLowerCase()
                                .replace(/[^a-z\s]/g, '') // Remove non-alphabetic characters except spaces
                                .replace(/\s+/g, '') // Remove all spaces
                                .substring(0, 20); // Limit length
                            
                            importedData.push({
                                name: values[0],
                                niy: values[1],
                                subject: values[2] || 'Umum',
                                status: 'aktif',
                                username: cleanName,
                                password: values[1] // NIY as password
                            });
                        }
                    }
                }

                // Remove loading message
                document.body.removeChild(loadingMsg);

                if (importedData.length === 0) {
                    alert('Tidak ada data valid yang ditemukan di Google Sheets!');
                    return;
                }

                // Show preview of imported data
                showImportPreview(importedData);

            } catch (error) {
                // Remove loading message if it exists
                const loadingMsg = document.querySelector('.fixed.inset-0');
                if (loadingMsg) {
                    document.body.removeChild(loadingMsg);
                }
                
                console.error('Error importing from Google Sheets:', error);
                alert('Gagal mengambil data dari Google Sheets. Pastikan link dapat diakses publik atau coba lagi nanti.');
                
                // Fallback to sample data
                importSampleData();
            }
        }

        function showImportPreview(importedData) {
            const previewHTML = `
                <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
                    <div class="bg-white rounded-lg p-6 max-w-4xl w-full mx-4 max-h-96 overflow-y-auto">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Preview Data Import (${importedData.length} guru)</h3>
                        <div class="overflow-x-auto mb-4">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase">Nama</th>
                                        <th class="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase">NIY</th>
                                        <th class="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase">Mapel</th>
                                        <th class="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase">Username</th>
                                        <th class="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase">Password</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    ${importedData.slice(0, 10).map(teacher => `
                                        <tr>
                                            <td class="px-3 py-2 text-sm text-gray-900">${teacher.name}</td>
                                            <td class="px-3 py-2 text-sm text-gray-900">${teacher.niy}</td>
                                            <td class="px-3 py-2 text-sm text-gray-900">${teacher.subject}</td>
                                            <td class="px-3 py-2 text-sm font-mono text-blue-600">${teacher.username}</td>
                                            <td class="px-3 py-2 text-sm font-mono text-green-600">${teacher.password}</td>
                                        </tr>
                                    `).join('')}
                                    ${importedData.length > 10 ? `<tr><td colspan="5" class="px-3 py-2 text-sm text-gray-500 text-center">... dan ${importedData.length - 10} guru lainnya</td></tr>` : ''}
                                </tbody>
                            </table>
                        </div>
                        <div class="flex justify-end space-x-4">
                            <button onclick="closeImportPreview()" class="px-4 py-2 border border-gray-300 rounded-lg text-gray-700 hover:bg-gray-50">
                                Batal
                            </button>
                            <button onclick="confirmImport()" class="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700">
                                Import Data
                            </button>
                        </div>
                    </div>
                </div>
            `;
            
            const previewDiv = document.createElement('div');
            previewDiv.innerHTML = previewHTML;
            previewDiv.id = 'importPreview';
            document.body.appendChild(previewDiv);
            
            // Store imported data temporarily
            window.tempImportData = importedData;
        }

        function closeImportPreview() {
            const preview = document.getElementById('importPreview');
            if (preview) {
                document.body.removeChild(preview);
            }
            window.tempImportData = null;
        }

        function confirmImport() {
            const importedData = window.tempImportData;
            if (!importedData) return;

            let addedCount = 0;
            let updatedAccounts = 0;

            importedData.forEach(importTeacher => {
                // Check if teacher with same NIY already exists
                const existingTeacher = teachers.find(t => t.niy === importTeacher.niy);
                if (!existingTeacher) {
                    const newId = Math.max(...teachers.map(t => t.id), 0) + 1;
                    teachers.push({
                        id: newId,
                        name: importTeacher.name,
                        niy: importTeacher.niy,
                        subject: importTeacher.subject,
                        status: importTeacher.status
                    });
                    addedCount++;
                }

                // Add to user accounts for login
                const existingAccount = userAccounts.find(u => u.username === importTeacher.username);
                if (!existingAccount) {
                    userAccounts.push({
                        username: importTeacher.username,
                        password: importTeacher.password,
                        role: 'Guru',
                        name: importTeacher.name
                    });
                    updatedAccounts++;
                }
            });

            if (addedCount > 0 || updatedAccounts > 0) {
                saveTeachersData();
                saveUserAccounts();
                loadTeachersTable();
                updateDashboard();
                closeImportPreview();
                
                alert(`Import berhasil!\n- ${addedCount} guru baru ditambahkan\n- ${updatedAccounts} akun login dibuat\n\nSetiap guru dapat login dengan:\nUsername: nama tanpa spasi (huruf kecil)\nPassword: NIY masing-masing`);
            } else {
                closeImportPreview();
                alert('Tidak ada data baru yang diimport. Semua guru sudah ada dalam sistem.');
            }
        }

        function importSampleData() {
            // Fallback sample data if Google Sheets fails
            const sampleData = [
                { name: "Drs. H. SAICHUL", niy: "099.07.001", subject: "ASWAJA", username: "saichul", password: "123" },
                { name: "NOER AZIZI", niy: "099.07.002", subject: "FIKIH, username: "noerazizi", password: "123" },
                { name: "H. CHOLIS AWALUDIN, SE", niy: "099.07.003", subject: "EKONOMI", username: "cholishawaludin", password: "123" },
                { name: "DWI NURCAHYANI, S.Si", niy: "099.07.004", subject: "FISIKA", username: "dwinurcahyani", password: "123" },
                { name: "LUXITASARI, S.Pd", niy: "099.07.006", subject: "BHS INGGRIS", username: "luxitasari", password: "123" }
            ];

            showImportPreview(sampleData);
        }

        function saveUserAccounts() {
            localStorage.setItem('userAccounts', JSON.stringify(userAccounts));
        }

        // User accounts - load from localStorage or use defaults
        let userAccounts = JSON.parse(localStorage.getItem('userAccounts')) || [
            { username: 'admin', password: 'admin123', role: 'Administrator', name: 'Admin Sistem' },
            
            // Teacher accounts will be auto-generated from teachers data
            { username: 'saichul', password: '123', role: 'Guru', name: 'Drs. H. SAICHUL' },
            { username: 'noerazizi', password: '123', role: 'Guru', name: 'NOER AZIZI' },
            { username: 'cholishawaludin', password: '123', role: 'Guru', name: 'H. CHOLIS AWALUDIN, SE' },
            { username: 'dwinurcahyani', password: '123', role: 'Guru', name: 'DWI NURCAHYANI, S.Si' },
            { username: 'luxitasari', password: '123', role: 'Guru', name: 'LUXITASARI, S.Pd' },
            { username: 'endangsrirahayu', password: '123', role: 'Guru', name: 'Dra. ENDANG SRI RAHAYU' },
            { username: 'vikakhullamahbubah', password: '123', role: 'Guru', name: 'Vika Khulla Mahbubah, M.Pd' },
            { username: 'zekkiyah', password: '123', role: 'Guru', name: 'ZEKKIYAH AL ALUF, S.Pd' },
            { username: 'anshori', password: '123', role: 'Guru', name: 'ANSHORI, S.Pd' },
            { username: 'afkhoriatul', password: '123', role: 'Guru', name: 'AFKHORIATUL HILMI, M.Pd' }
        ];

        let currentUser = null;

        // Login functionality
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            const user = userAccounts.find(u => u.username === username && u.password === password);
            
            if (user) {
                currentUser = user;
                document.getElementById('loginPage').classList.add('hidden');
                document.getElementById('mainPage').classList.remove('hidden');
                updateUserInfo();
                init();
            } else {
                document.getElementById('loginError').textContent = 'Username atau password salah!';
                document.getElementById('loginError').classList.remove('hidden');
            }
        });

        // Update user info in header
        function updateUserInfo() {
            if (currentUser) {
                const userInfoHTML = `
                    <div class="text-right">
                        <p class="text-sm font-medium text-gray-900">${currentUser.name}</p>
                        <p class="text-xs text-gray-600">${currentUser.role}</p>
                    </div>
                `;
                document.querySelector('.flex.items-center.space-x-4 .text-right').outerHTML = userInfoHTML;
            }
        }

        function logout() {
            document.getElementById('mainPage').classList.add('hidden');
            document.getElementById('loginPage').classList.remove('hidden');
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            document.getElementById('loginError').classList.add('hidden');
        }

        // Update date and time
        function updateDateTime() {
            const now = new Date();
            const options = { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            };
            document.getElementById('currentDate').textContent = now.toLocaleDateString('id-ID', options);
            document.getElementById('currentTime').textContent = now.toLocaleTimeString('id-ID');
            
            updateActiveSession();
        }

        // Update active session based on current time
        function updateActiveSession() {
            const now = new Date();
            const currentTime = now.toTimeString().slice(0, 5);
            const currentDay = ['minggu', 'senin', 'selasa', 'rabu', 'kamis', 'jumat', 'sabtu'][now.getDay()];
            
            if (currentDay === 'minggu' || !scheduleData[currentDay]) {
                document.getElementById('activeSession').textContent = 'Libur';
                return;
            }

            const schedule = scheduleData[currentDay];
            let activeSession = '-';

            for (const [session, time] of Object.entries(schedule)) {
                if (currentTime >= time.start && currentTime <= time.end) {
                    const sessionNames = {
                        kedatangan: 'Kedatangan',
                        pagi: 'Pendampingan Pagi',
                        kepesantrenan: 'Kepesantrenan',
                        wali: 'Pendampingan Wali Kelas',
                        pembelajaran: 'Pembelajaran Kelas',
                        duhur: 'Pendampingan Shalat Duhur'
                    };
                    activeSession = sessionNames[session];
                    break;
                }
            }

            document.getElementById('activeSession').textContent = activeSession;
        }

        // Tab navigation
        function showTab(tabName) {
            // Hide all tabs
            document.querySelectorAll('[id$="Tab"]').forEach(tab => {
                tab.classList.add('hidden');
            });
            
            // Show selected tab
            document.getElementById(tabName + 'Tab').classList.remove('hidden');
            
            // Update navigation
            document.querySelectorAll('.nav-tab').forEach(tab => {
                tab.classList.remove('active', 'border-indigo-500', 'text-indigo-600');
                tab.classList.add('border-transparent', 'text-gray-500');
            });
            
            event.target.classList.add('active', 'border-indigo-500', 'text-indigo-600');
            event.target.classList.remove('border-transparent', 'text-gray-500');
        }

        // Update dashboard statistics
        function updateDashboard() {
            const today = new Date().toDateString();
            const todayData = attendanceData[today] || {};
            
            // Filter only active teachers
            const activeTeachers = teachers.filter(teacher => teacher.status === 'aktif');
            
            let presentCount = 0;
            let totalSessions = 0;
            
            activeTeachers.forEach(teacher => {
                const teacherData = todayData[teacher.id] || {};
                let teacherPresent = 0;
                let teacherTotal = 0;
                
                ['kedatangan', 'pagi', 'kepesantrenan', 'wali', 'pembelajaran', 'duhur'].forEach(session => {
                    teacherTotal++;
                    if (teacherData[session] === 'hadir') {
                        teacherPresent++;
                    }
                });
                
                if (teacherPresent > 0) presentCount++;
                totalSessions += teacherTotal;
            });
            
            document.getElementById('todayPresent').textContent = presentCount;
            document.getElementById('todayAbsent').textContent = activeTeachers.length - presentCount;
            document.getElementById('totalTeachers').textContent = activeTeachers.length;
            
            updateRecentAttendance();
        }

        // Update recent attendance display
        function updateRecentAttendance() {
            const today = new Date().toDateString();
            const todayData = attendanceData[today] || {};
            const recentContainer = document.getElementById('recentAttendance');
            
            if (Object.keys(todayData).length === 0) {
                recentContainer.innerHTML = '<p class="text-gray-500 text-center py-8">Belum ada data absensi hari ini</p>';
                return;
            }
            
            let recentHTML = '';
            teachers.forEach(teacher => {
                const teacherData = todayData[teacher.id] || {};
                const sessions = ['kedatangan', 'pagi', 'kepesantrenan', 'wali', 'pembelajaran', 'duhur'];
                const presentSessions = sessions.filter(session => teacherData[session] === 'hadir');
                
                if (presentSessions.length > 0) {
                    recentHTML += `
                        <div class="flex items-center justify-between p-4 bg-gray-50 rounded-lg">
                            <div>
                                <p class="font-medium text-gray-900">${teacher.name}</p>
                                <p class="text-sm text-gray-600">${presentSessions.length} dari ${sessions.length} sesi hadir</p>
                            </div>
                            <div class="text-right">
                                <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-green-100 text-green-800">
                                    ${Math.round((presentSessions.length / sessions.length) * 100)}% Hadir
                                </span>
                            </div>
                        </div>
                    `;
                }
            });
            
            recentContainer.innerHTML = recentHTML || '<p class="text-gray-500 text-center py-8">Belum ada data absensi hari ini</p>';
        }

        // Start attendance session
        function startAttendance(session) {
            currentSession = session;
            const sessionNames = {
                kedatangan: 'Kedatangan',
                pagi: 'Pendampingan Pagi',
                kepesantrenan: 'Kepesantrenan',
                wali: 'Pendampingan Wali Kelas',
                pembelajaran: 'Pembelajaran Kelas',
                duhur: 'Pendampingan Shalat Duhur'
            };
            
            document.getElementById('sessionTitle').textContent = sessionNames[session];
            document.getElementById('attendanceForm').classList.remove('hidden');
            
            // Check location
            checkLocation();
            
            // Populate teacher list
            populateTeacherList();
        }

        // Check user location
        function checkLocation() {
            const locationStatus = document.getElementById('locationStatus');
            
            if (!navigator.geolocation) {
                locationStatus.textContent = 'Geolokasi tidak didukung browser';
                locationStatus.className = 'font-medium text-red-600';
                return;
            }
            
            navigator.geolocation.getCurrentPosition(
                function(position) {
                    const userLat = position.coords.latitude;
                    const userLng = position.coords.longitude;
                    const schoolLat = parseFloat(document.getElementById('schoolLat').value);
                    const schoolLng = parseFloat(document.getElementById('schoolLng').value);
                    const radius = parseInt(document.getElementById('locationRadius').value);
                    
                    const distance = calculateDistance(userLat, userLng, schoolLat, schoolLng);
                    
                    if (distance <= radius) {
                        locationStatus.textContent = `Lokasi valid (${Math.round(distance)}m dari sekolah)`;
                        locationStatus.className = 'font-medium text-green-600';
                        currentLocation = { valid: true, distance: distance };
                    } else {
                        locationStatus.textContent = `Lokasi terlalu jauh (${Math.round(distance)}m dari sekolah)`;
                        locationStatus.className = 'font-medium text-red-600';
                        currentLocation = { valid: false, distance: distance };
                    }
                },
                function(error) {
                    locationStatus.textContent = 'Gagal mendapatkan lokasi';
                    locationStatus.className = 'font-medium text-red-600';
                    currentLocation = { valid: false, error: error.message };
                }
            );
        }

        // Calculate distance between two coordinates
        function calculateDistance(lat1, lng1, lat2, lng2) {
            const R = 6371000; // Earth's radius in meters
            const dLat = (lat2 - lat1) * Math.PI / 180;
            const dLng = (lng2 - lng1) * Math.PI / 180;
            const a = Math.sin(dLat/2) * Math.sin(dLat/2) +
                      Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
                      Math.sin(dLng/2) * Math.sin(dLng/2);
            const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
            return R * c;
        }

        // Populate teacher list for attendance
        function populateTeacherList() {
            const teacherList = document.getElementById('teacherList');
            const today = new Date().toDateString();
            const todayData = attendanceData[today] || {};
            
            // Filter only active teachers
            const activeTeachers = teachers.filter(teacher => teacher.status === 'aktif');
            
            let html = '';
            activeTeachers.forEach(teacher => {
                const teacherData = todayData[teacher.id] || {};
                const currentStatus = teacherData[currentSession] || 'belum';
                
                html += `
                    <div class="bg-gray-50 rounded-lg p-4">
                        <div class="mb-3">
                            <h5 class="font-medium text-gray-900">${teacher.name}</h5>
                            <p class="text-sm text-gray-600">${teacher.subject}</p>
                        </div>
                        <div class="flex space-x-2">
                            <button onclick="setAttendance(${teacher.id}, 'hadir')" 
                                    class="flex-1 py-2 px-3 text-sm rounded-lg border ${currentStatus === 'hadir' ? 'bg-green-500 text-white border-green-500' : 'bg-white text-gray-700 border-gray-300 hover:bg-green-50'}">
                                Hadir
                            </button>
                            <button onclick="setAttendance(${teacher.id}, 'tidak_hadir')" 
                                    class="flex-1 py-2 px-3 text-sm rounded-lg border ${currentStatus === 'tidak_hadir' ? 'bg-red-500 text-white border-red-500' : 'bg-white text-gray-700 border-gray-300 hover:bg-red-50'}">
                                Tidak Hadir
                            </button>
                        </div>
                    </div>
                `;
            });
            
            teacherList.innerHTML = html;
        }

        // Set attendance status for a teacher
        function setAttendance(teacherId, status) {
            const today = new Date().toDateString();
            
            if (!attendanceData[today]) {
                attendanceData[today] = {};
            }
            
            if (!attendanceData[today][teacherId]) {
                attendanceData[today][teacherId] = {};
            }
            
            attendanceData[today][teacherId][currentSession] = status;
            
            // Update UI
            populateTeacherList();
        }

        // Save attendance data
        function saveAttendance() {
            if (!currentLocation || !currentLocation.valid) {
                alert('Lokasi tidak valid! Pastikan Anda berada di area sekolah.');
                return;
            }
            
            localStorage.setItem('attendanceData', JSON.stringify(attendanceData));
            alert('Data absensi berhasil disimpan!');
            cancelAttendance();
            updateDashboard();
        }

        // Cancel attendance
        function cancelAttendance() {
            document.getElementById('attendanceForm').classList.add('hidden');
            currentSession = '';
            currentLocation = null;
        }

        // Load schedule for selected day
        function loadDaySchedule() {
            const selectedDay = document.getElementById('daySelect').value;
            const schedule = scheduleData[selectedDay];
            
            if (schedule) {
                document.getElementById('kedatanganStart').value = schedule.kedatangan.start;
                document.getElementById('kedatanganEnd').value = schedule.kedatangan.end;
                document.getElementById('pagiStart').value = schedule.pagi.start;
                document.getElementById('pagiEnd').value = schedule.pagi.end;
                document.getElementById('kepesantrenanStart').value = schedule.kepesantrenan.start;
                document.getElementById('kepesantrenanEnd').value = schedule.kepesantrenan.end;
                document.getElementById('waliStart').value = schedule.wali.start;
                document.getElementById('waliEnd').value = schedule.wali.end;
                document.getElementById('pembelajaranStart').value = schedule.pembelajaran.start;
                document.getElementById('pembelajaranEnd').value = schedule.pembelajaran.end;
                document.getElementById('duhurStart').value = schedule.duhur.start;
                document.getElementById('duhurEnd').value = schedule.duhur.end;
            }
            
            updateScheduleDisplay();
        }

        // Update schedule display on attendance cards
        function updateScheduleDisplay() {
            const now = new Date();
            const currentDay = ['minggu', 'senin', 'selasa', 'rabu', 'kamis', 'jumat', 'sabtu'][now.getDay()];
            const schedule = scheduleData[currentDay] || scheduleData.senin;
            
            document.getElementById('kedatanganTime').textContent = `${schedule.kedatangan.start} - ${schedule.kedatangan.end}`;
            document.getElementById('pagiTime').textContent = `${schedule.pagi.start} - ${schedule.pagi.end}`;
            document.getElementById('kepesantrenanTime').textContent = `${schedule.kepesantrenan.start} - ${schedule.kepesantrenan.end}`;
            document.getElementById('waliTime').textContent = `${schedule.wali.start} - ${schedule.wali.end}`;
            document.getElementById('pembelajaranTime').textContent = `${schedule.pembelajaran.start} - ${schedule.pembelajaran.end}`;
            document.getElementById('duhurTime').textContent = `${schedule.duhur.start} - ${schedule.duhur.end}`;
        }

        // Save schedule settings
        function saveSchedule() {
            const selectedDay = document.getElementById('daySelect').value;
            
            scheduleData[selectedDay] = {
                kedatangan: {
                    start: document.getElementById('kedatanganStart').value,
                    end: document.getElementById('kedatanganEnd').value
                },
                pagi: {
                    start: document.getElementById('pagiStart').value,
                    end: document.getElementById('pagiEnd').value
                },
                kepesantrenan: {
                    start: document.getElementById('kepesantrenanStart').value,
                    end: document.getElementById('kepesantrenanEnd').value
                },
                wali: {
                    start: document.getElementById('waliStart').value,
                    end: document.getElementById('waliEnd').value
                },
                pembelajaran: {
                    start: document.getElementById('pembelajaranStart').value,
                    end: document.getElementById('pembelajaranEnd').value
                },
                duhur: {
                    start: document.getElementById('duhurStart').value,
                    end: document.getElementById('duhurEnd').value
                }
            };
            
            localStorage.setItem('scheduleData', JSON.stringify(scheduleData));
            updateScheduleDisplay();
            alert('Jadwal berhasil disimpan!');
        }

        // Save location settings
        function saveLocationSettings() {
            alert('Pengaturan lokasi berhasil disimpan!');
        }

        // Generate report
        function generateReport() {
            const month = parseInt(document.getElementById('reportMonth').value);
            const year = parseInt(document.getElementById('reportYear').value);
            const reportContent = document.getElementById('reportContent');
            
            if (reportType === 'daily') {
                generateDailyReport(month, year, reportContent);
            } else {
                generateMonthlyReport(month, year, reportContent);
            }
        }

        // Generate daily report
        function generateDailyReport(month, year, container) {
            const daysInMonth = new Date(year, month + 1, 0).getDate();
            let html = `
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tanggal</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Guru</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kedatangan</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Pagi</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Kepesantrenan</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Wali Kelas</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Pembelajaran</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Shalat Duhur</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-gray-200">
            `;
            
            for (let day = 1; day <= daysInMonth; day++) {
                const date = new Date(year, month, day);
                const dateString = date.toDateString();
                const dayData = attendanceData[dateString] || {};
                
                if (Object.keys(dayData).length > 0) {
                    teachers.forEach(teacher => {
                        const teacherData = dayData[teacher.id] || {};
                        const sessions = ['kedatangan', 'pagi', 'kepesantrenan', 'wali', 'pembelajaran', 'duhur'];
                        const presentCount = sessions.filter(session => teacherData[session] === 'hadir').length;
                        
                        html += `
                            <tr>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${day}/${month + 1}/${year}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${teacher.name}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacherData.kedatangan === 'hadir' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                        ${teacherData.kedatangan === 'hadir' ? 'Hadir' : 'Tidak Hadir'}
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacherData.pagi === 'hadir' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                        ${teacherData.pagi === 'hadir' ? 'Hadir' : 'Tidak Hadir'}
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacherData.kepesantrenan === 'hadir' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                        ${teacherData.kepesantrenan === 'hadir' ? 'Hadir' : 'Tidak Hadir'}
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacherData.wali === 'hadir' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                        ${teacherData.wali === 'hadir' ? 'Hadir' : 'Tidak Hadir'}
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacherData.pembelajaran === 'hadir' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                        ${teacherData.pembelajaran === 'hadir' ? 'Hadir' : 'Tidak Hadir'}
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm">
                                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${teacherData.duhur === 'hadir' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800'}">
                                        ${teacherData.duhur === 'hadir' ? 'Hadir' : 'Tidak Hadir'}
                                    </span>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${presentCount}/6</td>
                            </tr>
                        `;
                    });
                }
            }
            
            html += `
                        </tbody>
                    </table>
                </div>
            `;
            
            container.innerHTML = html;
        }

        // Generate monthly report
        function generateMonthlyReport(month, year, container) {
            let html = `
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Guru</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total Hadir</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total Sesi</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Persentase</th>
                            </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-gray-200">
            `;
            
            teachers.forEach(teacher => {
                let totalPresent = 0;
                let totalSessions = 0;
                
                const daysInMonth = new Date(year, month + 1, 0).getDate();
                for (let day = 1; day <= daysInMonth; day++) {
                    const date = new Date(year, month, day);
                    const dateString = date.toDateString();
                    const dayData = attendanceData[dateString] || {};
                    const teacherData = dayData[teacher.id] || {};
                    
                    ['kedatangan', 'pagi', 'kepesantrenan', 'wali', 'pembelajaran', 'duhur'].forEach(session => {
                        totalSessions++;
                        if (teacherData[session] === 'hadir') {
                            totalPresent++;
                        }
                    });
                }
                
                const percentage = totalSessions > 0 ? Math.round((totalPresent / totalSessions) * 100) : 0;
                
                html += `
                    <tr>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${teacher.name}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${totalPresent}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">${totalSessions}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                            <div class="flex items-center">
                                <div class="flex-1 bg-gray-200 rounded-full h-2 mr-2">
                                    <div class="bg-green-500 h-2 rounded-full" style="width: ${percentage}%"></div>
                                </div>
                                <span class="text-sm font-medium">${percentage}%</span>
                            </div>
                        </td>
                    </tr>
                `;
            });
            
            html += `
                        </tbody>
                    </table>
                </div>
            `;
            
            container.innerHTML = html;
        }

        // Show report type
        function showReportType(type) {
            reportType = type;
            
            document.querySelectorAll('.report-tab').forEach(tab => {
                tab.classList.remove('bg-indigo-500', 'text-white');
                tab.classList.add('bg-gray-200', 'text-gray-700');
            });
            
            event.target.classList.remove('bg-gray-200', 'text-gray-700');
            event.target.classList.add('bg-indigo-500', 'text-white');
            
            generateReport();
        }

        // Print report
        function printReport() {
            window.print();
        }

        // Export to Google Sheets
        function exportToGoogleSheets() {
            const month = parseInt(document.getElementById('reportMonth').value);
            const year = parseInt(document.getElementById('reportYear').value);
            const monthNames = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
            
            // Prepare data for export
            let csvData = [];
            
            if (reportType === 'daily') {
                // Daily report CSV
                csvData.push(['Tanggal', 'Nama Guru', 'NIY', 'Mata Pelajaran', 'Kedatangan', 'Pagi', 'Kepesantrenan', 'Wali Kelas', 'Pembelajaran', 'Shalat Duhur', 'Total Hadir']);
                
                const daysInMonth = new Date(year, month + 1, 0).getDate();
                for (let day = 1; day <= daysInMonth; day++) {
                    const date = new Date(year, month, day);
                    const dateString = date.toDateString();
                    const dayData = attendanceData[dateString] || {};
                    
                    if (Object.keys(dayData).length > 0) {
                        teachers.forEach(teacher => {
                            const teacherData = dayData[teacher.id] || {};
                            const sessions = ['kedatangan', 'pagi', 'kepesantrenan', 'wali', 'pembelajaran', 'duhur'];
                            const presentCount = sessions.filter(session => teacherData[session] === 'hadir').length;
                            
                            csvData.push([
                                `${day}/${month + 1}/${year}`,
                                teacher.name,
                                teacher.niy,
                                teacher.subject,
                                teacherData.kedatangan === 'hadir' ? 'Hadir' : 'Tidak Hadir',
                                teacherData.pagi === 'hadir' ? 'Hadir' : 'Tidak Hadir',
                                teacherData.kepesantrenan === 'hadir' ? 'Hadir' : 'Tidak Hadir',
                                teacherData.wali === 'hadir' ? 'Hadir' : 'Tidak Hadir',
                                teacherData.pembelajaran === 'hadir' ? 'Hadir' : 'Tidak Hadir',
                                teacherData.duhur === 'hadir' ? 'Hadir' : 'Tidak Hadir',
                                `${presentCount}/6`
                            ]);
                        });
                    }
                }
            } else {
                // Monthly report CSV
                csvData.push(['Nama Guru', 'NIY', 'Mata Pelajaran', 'Total Hadir', 'Total Sesi', 'Persentase']);
                
                teachers.forEach(teacher => {
                    let totalPresent = 0;
                    let totalSessions = 0;
                    
                    const daysInMonth = new Date(year, month + 1, 0).getDate();
                    for (let day = 1; day <= daysInMonth; day++) {
                        const date = new Date(year, month, day);
                        const dateString = date.toDateString();
                        const dayData = attendanceData[dateString] || {};
                        const teacherData = dayData[teacher.id] || {};
                        
                        ['kedatangan', 'pagi', 'kepesantrenan', 'wali', 'pembelajaran', 'duhur'].forEach(session => {
                            totalSessions++;
                            if (teacherData[session] === 'hadir') {
                                totalPresent++;
                            }
                        });
                    }
                    
                    const percentage = totalSessions > 0 ? Math.round((totalPresent / totalSessions) * 100) : 0;
                    
                    csvData.push([
                        teacher.name,
                        teacher.niy,
                        teacher.subject,
                        totalPresent,
                        totalSessions,
                        `${percentage}%`
                    ]);
                });
            }
            
            // Convert to CSV string
            const csvString = csvData.map(row => 
                row.map(cell => `"${cell}"`).join(',')
            ).join('\n');
            
            // Create and download CSV file
            const blob = new Blob([csvString], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', `Laporan_Absensi_${monthNames[month]}_${year}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            // Show Google Sheets import instructions
            showGoogleSheetsInstructions();
        }

        // Show Google Sheets import instructions
        function showGoogleSheetsInstructions() {
            const instructionsHTML = `
                <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
                    <div class="bg-white rounded-lg p-6 max-w-2xl w-full mx-4 max-h-96 overflow-y-auto">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">📊 Cara Import ke Google Sheets</h3>
                        <div class="space-y-4 text-sm text-gray-700">
                            <div class="bg-blue-50 p-4 rounded-lg">
                                <h4 class="font-semibold text-blue-800 mb-2">Langkah 1: Buka Google Sheets</h4>
                                <p>• Buka <a href="https://sheets.google.com" target="_blank" class="text-blue-600 underline">sheets.google.com</a></p>
                                <p>• Klik "Blank" untuk membuat spreadsheet baru</p>
                            </div>
                            
                            <div class="bg-green-50 p-4 rounded-lg">
                                <h4 class="font-semibold text-green-800 mb-2">Langkah 2: Import File CSV</h4>
                                <p>• Klik menu "File" → "Import"</p>
                                <p>• Pilih tab "Upload"</p>
                                <p>• Drag & drop file CSV yang baru didownload atau klik "Select a file from your device"</p>
                                <p>• Pilih "Replace spreadsheet" dan klik "Import data"</p>
                            </div>
                            
                            <div class="bg-yellow-50 p-4 rounded-lg">
                                <h4 class="font-semibold text-yellow-800 mb-2">Langkah 3: Format dan Simpan</h4>
                                <p>• Data akan otomatis terformat dalam tabel</p>
                                <p>• Rename spreadsheet sesuai kebutuhan</p>
                                <p>• Klik "Share" untuk berbagi dengan tim</p>
                            </div>
                            
                            <div class="bg-purple-50 p-4 rounded-lg">
                                <h4 class="font-semibold text-purple-800 mb-2">💡 Tips Tambahan</h4>
                                <p>• Gunakan filter dan sort untuk analisis data</p>
                                <p>• Buat chart/grafik untuk visualisasi</p>
                                <p>• Set up automatic backup dengan Google Drive</p>
                            </div>
                        </div>
                        
                        <div class="mt-6 flex justify-end">
                            <button onclick="closeInstructions()" class="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700">
                                Mengerti
                            </button>
                        </div>
                    </div>
                </div>
            `;
            
            const instructionsDiv = document.createElement('div');
            instructionsDiv.innerHTML = instructionsHTML;
            instructionsDiv.id = 'sheetsInstructions';
            document.body.appendChild(instructionsDiv);
        }

        // Close instructions modal
        function closeInstructions() {
            const instructions = document.getElementById('sheetsInstructions');
            if (instructions) {
                document.body.removeChild(instructions);
            }
        }

        // WhatsApp Broadcast Functions
        function showBroadcastForm() {
            document.getElementById('broadcastForm').classList.remove('hidden');
            populateTeacherCheckboxes();
        }

        function cancelBroadcast() {
            document.getElementById('broadcastForm').classList.add('hidden');
            document.getElementById('broadcastMessage').value = '';
            document.getElementById('selectAllTeachers').checked = false;
            // Uncheck all teacher checkboxes
            document.querySelectorAll('input[name="teacherSelect"]').forEach(checkbox => {
                checkbox.checked = false;
            });
        }

        function populateTeacherCheckboxes() {
            const container = document.getElementById('teacherCheckboxes');
            const activeTeachers = teachers.filter(teacher => teacher.status === 'aktif' && teacher.whatsapp);
            
            let html = '';
            activeTeachers.forEach(teacher => {
                html += `
                    <label class="flex items-center p-2 hover:bg-gray-50 rounded">
                        <input type="checkbox" name="teacherSelect" value="${teacher.id}" class="rounded border-gray-300 text-green-600 focus:ring-green-500">
                        <div class="ml-3 flex-1">
                            <div class="text-sm font-medium text-gray-900">${teacher.name}</div>
                            <div class="text-xs text-gray-500">${teacher.subject} • ${teacher.whatsapp}</div>
                        </div>
                    </label>
                `;
            });
            
            if (activeTeachers.length === 0) {
                html = '<p class="text-sm text-gray-500 text-center py-4">Tidak ada guru dengan nomor WhatsApp yang tersedia</p>';
            }
            
            container.innerHTML = html;
        }

        function toggleAllTeachers() {
            const selectAll = document.getElementById('selectAllTeachers');
            const teacherCheckboxes = document.querySelectorAll('input[name="teacherSelect"]');
            
            teacherCheckboxes.forEach(checkbox => {
                checkbox.checked = selectAll.checked;
            });
        }

        function sendBroadcast() {
            const message = document.getElementById('broadcastMessage').value.trim();
            const selectedTeachers = Array.from(document.querySelectorAll('input[name="teacherSelect"]:checked'))
                .map(checkbox => parseInt(checkbox.value));
            
            if (!message) {
                alert('Mohon masukkan pesan yang akan dikirim!');
                return;
            }
            
            if (selectedTeachers.length === 0) {
                alert('Mohon pilih minimal satu guru untuk mengirim pesan!');
                return;
            }
            
            // Show confirmation
            const teacherNames = selectedTeachers.map(id => {
                const teacher = teachers.find(t => t.id === id);
                return teacher ? teacher.name : '';
            }).filter(name => name);
            
            const confirmMessage = `Kirim pesan ke ${selectedTeachers.length} guru?\n\nPenerima:\n${teacherNames.slice(0, 5).join('\n')}${teacherNames.length > 5 ? `\n... dan ${teacherNames.length - 5} guru lainnya` : ''}\n\nPesan:\n"${message.substring(0, 100)}${message.length > 100 ? '...' : ''}"`;
            
            if (!confirm(confirmMessage)) {
                return;
            }
            
            // Open WhatsApp Web for each selected teacher
            let successCount = 0;
            selectedTeachers.forEach((teacherId, index) => {
                const teacher = teachers.find(t => t.id === teacherId);
                if (teacher && teacher.whatsapp) {
                    setTimeout(() => {
                        const phoneNumber = teacher.whatsapp.replace(/^0/, '62'); // Convert to international format
                        const encodedMessage = encodeURIComponent(message);
                        const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodedMessage}`;
                        
                        window.open(whatsappUrl, '_blank');
                        successCount++;
                        
                        // Show completion message after last message
                        if (index === selectedTeachers.length - 1) {
                            setTimeout(() => {
                                alert(`Berhasil membuka ${successCount} tab WhatsApp!\n\nSilakan kirim pesan secara manual di setiap tab yang terbuka.`);
                                cancelBroadcast();
                            }, 1000);
                        }
                    }, index * 1000); // Delay 1 second between each tab
                }
            });
        }

        // Initialize when page loads
        document.addEventListener('DOMContentLoaded', function() {
            initLoginPage();
            updateScheduleDisplay();
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9679343cb5b59a2b',t:'MTc1MzkyNDEwMC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
