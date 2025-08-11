<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Buku Tamu Digital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
       @import photo('https://drive.google.com/file/d/1r1EMb7mQgJFJwi1ho5fwXZ9OzeQOijmr/view?usp=sharing');
		body {
		  background-image: url('DPRD.jpg');
		  background-repeat: no-repeat;
		  background-attachment: fixed;  
		  background-size: cover;
		}
        .bg-overlay {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
        }
        .drag-over { 
            border-color: #3b82f6; 
            background: linear-gradient(135deg, #eff6ff 0%, #dbeafe 100%);
            transform: scale(1.02);
        }
        .gradient-bg {
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.95) 0%, rgba(118, 75, 162, 0.95) 100%);
            backdrop-filter: blur(15px);
        }
        .card-shadow {
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            backdrop-filter: blur(16px);
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .btn-primary {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            transition: all 0.3s ease;
        }
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.4);
        }
        .btn-success {
            background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
        }
        .btn-success:hover {
            transform: translateY(-1px);
            box-shadow: 0 8px 15px rgba(72, 187, 120, 0.4);
        }
        .btn-danger {
            background: linear-gradient(135deg, #f56565 0%, #e53e3e 100%);
        }
        .btn-danger:hover {
            transform: translateY(-1px);
            box-shadow: 0 8px 15px rgba(245, 101, 101, 0.4);
        }
        .upload-zone {
            background: linear-gradient(135deg, rgba(247, 250, 252, 0.9) 0%, rgba(237, 242, 247, 0.9) 100%);
            border: 2px dashed #cbd5e0;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }
        .upload-zone:hover {
            background: linear-gradient(135deg, rgba(235, 248, 255, 0.9) 0%, rgba(190, 227, 248, 0.9) 100%);
            border-color: #4299e1;
        }
        .stats-card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .table-glass {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(15px);
        }
    </style>
</head>
<body class="min-h-screen">
    <!-- Background Overlay -->
    <div class="fixed inset-0 bg-gradient-to-br from-blue-900/20 via-purple-900/20 to-indigo-900/20 pointer-events-none"></div>
    
    <!-- Header -->
    <header class="gradient-bg shadow-2xl relative z-10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
            <div class="flex justify-between items-center">
                <h1 class="text-3xl font-bold text-white flex items-center">
                    <span class="text-4xl mr-3">📖</span>
                    Buku Tamu Digital
                </h1>
                <div class="flex space-x-4">
                    <button onclick="showVisitorForm()" id="visitorBtn" class="bg-white bg-opacity-20 hover:bg-opacity-30 text-white px-6 py-3 rounded-xl font-medium transition-all duration-300 backdrop-blur-sm border border-white border-opacity-20">
                        <span class="mr-2">👤</span>Daftar Kunjungan
                    </button>
                    <button onclick="showAdminLogin()" id="adminBtn" class="bg-white bg-opacity-10 hover:bg-opacity-20 text-white px-6 py-3 rounded-xl font-medium transition-all duration-300 backdrop-blur-sm border border-white border-opacity-20">
                        <span class="mr-2">🔧</span>Admin
                    </button>
                    <button onclick="adminLogout()" id="logoutBtn" class="bg-red-500 bg-opacity-80 hover:bg-opacity-100 text-white px-6 py-3 rounded-xl font-medium transition-all duration-300 hidden">
                        <span class="mr-2">🚪</span>Logout
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Visitor Form -->
    <div id="visitorForm" class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-8 relative z-10">
        <div class="glass-card rounded-2xl card-shadow p-8 border-t-4 border-purple-500">
            <div class="text-center mb-8">
                <div class="text-6xl mb-4">✨</div>
                <h2 class="text-3xl font-bold bg-gradient-to-r from-purple-600 to-blue-600 bg-clip-text text-transparent mb-2">Form Registrasi Kunjungan</h2>
				<h2 class="text-3xl font-bold bg-gradient-to-r from-purple-600 to-blue-600 bg-clip-text text-transparent mb-2">DPRD Kabupaten Muara Enim</h2>
                <p class="text-gray-700">Jalan Mayor Tjik Agus Kiemas, S.H. Kecamatan Muara Enim</p>
				<p class="text-blue-400">Email: setwanmuaraenim@gmail.com</p>
            </div>

                        <form id="visitForm" class="space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Tanggal Kunjungan -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">📅</span>Tanggal Kunjungan
                        </label>
                        <input type="date" id="visitDate" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm">
                    </div>

                    <!-- Jam Kunjungan -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">🕐</span>Jam Kunjungan
                        </label>
                        <input type="time" id="visitTime" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm">
                    </div>

                    <!-- Jumlah Tamu -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">👥</span>Jumlah Tamu
                        </label>
                        <input type="number" id="guestCount" min="1" max="20" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Masukkan jumlah tamu">
                    </div>

                    <!-- Nama -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">👤</span>Nama Pemohon
                        </label>
                        <input type="text" id="fullName" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Masukkan nama lengkap">
                    </div>

                    <!-- Email -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">📧</span>Email
                        </label>
                        <input type="email" id="email" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="contoh@email.com">
                    </div>

                    <!-- Nomor HP -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">📱</span>Nomor HP/ WA
                        </label>
                        <input type="tel" id="phoneNumber" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="08xxxxxxxxxx">
                    </div>

                    <!-- Jabatan -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">💼</span>Jabatan
                        </label>
                        <input type="text" id="position" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Masukkan jabatan">
                    </div>

                    <!-- Instansi -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">🏢</span>Instansi
                        </label>
                        <input type="text" id="institution" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Nama instansi">
                    </div>
                </div>

                <!-- Tujuan Kunjungan -->
                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                        <span class="text-lg mr-2">🎯</span>Tujuan Kunjungan
                    </label>
                    <select id="visitPurpose" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm">
                        <option value="">Pilih tujuan kunjungan</option>
                        <option value="consultation">💬 Audiensi</option>
						<option value="business">💼 Kunjungan Kerja</option>
                        <option value="personal">👤 Study Banding</option>
                        <option value="other">📋 Lainnya</option>
                    </select>
                </div>

                <!-- Keperluan -->
                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                        <span class="text-lg mr-2">📝</span>Keperluan Detail
                    </label>
                    <textarea id="visitDetails" rows="4" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Jelaskan keperluan kunjungan Anda secara detail..."></textarea>
                </div>

                <!-- Upload Dokumen -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Upload Area 1 - Dokumen Resmi -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">📎</span>Surat Permohonan Kunjungan
                        </label>
                        <div id="dropZone1" class="upload-zone rounded-xl p-6 text-center cursor-pointer">
                            <div class="text-4xl mb-3">📄</div>
                            <p class="text-gray-700 font-medium mb-2 text-sm"> Surat atau dokumen resmi lainnya</p>
                            <p class="text-xs text-gray-600">PDF, DOC, DOCX (Max: 5MB per file)</p>
                            <input type="file" id="fileInput1" multiple accept=".pdf,.doc,.docx" class="hidden">
                        </div>
                        <div id="fileList1" class="mt-3 space-y-2"></div>
                        <div id="uploadError1" class="mt-2 text-red-600 text-sm font-medium hidden"></div>
                    </div>

                    <!-- Upload Area 2 - Dokumen Pendukung -->
                    <div>
                        <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                            <span class="text-lg mr-2">📎</span>Surat Tugas
                        </label>
                        <div id="dropZone2" class="upload-zone rounded-xl p-6 text-center cursor-pointer">
                            <div class="text-4xl mb-3">📄</div>
                            <p class="text-gray-700 font-medium mb-2 text-sm">Surat atau dokumen pendukung lainnya</p>
                            <p class="text-xs text-gray-600">PDF, DOC, DOCX, JPG, PNG (Max: 5MB per file)</p>
                            <input type="file" id="fileInput2" multiple accept=".pdf,.doc,.docx,.jpg,.jpeg,.png" class="hidden">
                        </div>
                        <div id="fileList2" class="mt-3 space-y-2"></div>
                        <div id="uploadError2" class="mt-2 text-red-600 text-sm font-medium hidden"></div>
                    </div>
                </div>

                <button type="submit" class="w-full btn-primary text-white font-semibold py-4 px-6 rounded-xl text-lg">
                    <span class="mr-2">✅</span>Daftar Kunjungan
                </button>
            </form>
        </div>
    </div>

    <!-- Admin Login Form -->
    <div id="adminLogin" class="max-w-md mx-auto px-4 sm:px-6 lg:px-8 py-8 hidden relative z-10">
        <div class="glass-card rounded-2xl card-shadow p-8 border-t-4 border-blue-500">
            <div class="text-center mb-8">
                <div class="text-6xl mb-4">🔐</div>
                <h2 class="text-2xl font-bold bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent mb-2">Login Admin</h2>
                <p class="text-gray-700">Masukkan kredensial admin untuk mengakses panel</p>
            </div>

            <form id="adminLoginForm" class="space-y-6">
                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                        <span class="text-lg mr-2">👤</span>Username
                    </label>
                    <input type="text" id="adminUsername" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Masukkan username">
                </div>

                <div>
                    <label class="block text-sm font-semibold text-gray-700 mb-2 flex items-center">
                        <span class="text-lg mr-2">🔑</span>Password
                    </label>
                    <input type="password" id="adminPassword" required class="w-full px-4 py-3 border-2 border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Masukkan password">
                </div>

                <div id="loginError" class="text-red-600 text-sm font-medium hidden bg-red-50/80 backdrop-blur-sm p-3 rounded-lg border border-red-200">
                    ❌ Username atau password salah!
                </div>

                <button type="submit" class="w-full btn-primary text-white font-semibold py-3 px-6 rounded-xl">
                    <span class="mr-2">🚀</span>Login
                </button>
            </form>

        </div>
    </div>

    <!-- Admin Panel -->
    <div id="adminPanel" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 hidden relative z-10">
        <div class="glass-card rounded-2xl card-shadow p-8 border-t-4 border-green-500">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-3xl font-bold bg-gradient-to-r from-green-600 to-blue-600 bg-clip-text text-transparent flex items-center">
                    <span class="text-4xl mr-3">🔧</span>Admin Panel - Data Kunjungan
                </h2>
                <div class="flex space-x-4">
                    <button onclick="exportData()" class="btn-success text-white px-6 py-3 rounded-xl font-medium transition-all duration-300">
                        <span class="mr-2">📊</span>Export Data
                    </button>
                    <button onclick="clearAllData()" class="btn-danger text-white px-6 py-3 rounded-xl font-medium transition-all duration-300">
                        <span class="mr-2">🗑️</span>Hapus Semua
                    </button>
                </div>
            </div>

            <!-- Statistics -->
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
                <div class="bg-gradient-to-br from-blue-400 to-blue-600 stats-card p-6 rounded-xl text-white card-shadow">
                    <div class="flex items-center justify-between">
                        <div>
                            <div class="text-3xl font-bold" id="totalVisits">0</div>
                            <div class="font-medium opacity-90">Total Kunjungan</div>
                        </div>
                        <div class="text-4xl opacity-80">📊</div>
                    </div>
                </div>
                <div class="bg-gradient-to-br from-green-400 to-green-600 stats-card p-6 rounded-xl text-white card-shadow">
                    <div class="flex items-center justify-between">
                        <div>
                            <div class="text-3xl font-bold" id="todayVisits">0</div>
                            <div class="font-medium opacity-90">Hari Ini</div>
                        </div>
                        <div class="text-4xl opacity-80">📅</div>
                    </div>
                </div>
                <div class="bg-gradient-to-br from-yellow-400 to-orange-500 stats-card p-6 rounded-xl text-white card-shadow">
                    <div class="flex items-center justify-between">
                        <div>
                            <div class="text-3xl font-bold" id="totalGuests">0</div>
                            <div class="font-medium opacity-90">Total Tamu</div>
                        </div>
                        <div class="text-4xl opacity-80">👥</div>
                    </div>
                </div>
                <div class="bg-gradient-to-br from-purple-400 to-purple-600 stats-card p-6 rounded-xl text-white card-shadow">
                    <div class="flex items-center justify-between">
                        <div>
                            <div class="text-3xl font-bold" id="pendingVisits">0</div>
                            <div class="font-medium opacity-90">Menunggu</div>
                        </div>
                        <div class="text-4xl opacity-80">⏳</div>
                    </div>
                </div>
            </div>

            <!-- Filter -->
            <div class="mb-6 flex flex-wrap gap-4 p-4 bg-gradient-to-r from-gray-50/80 to-blue-50/80 backdrop-blur-sm rounded-xl border border-gray-200">
                <input type="date" id="filterDate" class="px-4 py-2 border-2 border-gray-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all duration-300 bg-white/80 backdrop-blur-sm" placeholder="Filter tanggal">
                <select id="filterPurpose" class="px-4 py-2 border-2 border-gray-200 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all duration-300 bg-white/80 backdrop-blur-sm">
                    <option value="">Semua Tujuan</option>
                        <option value="consultation">💬 Audiensi</option>
						<option value="business">💼 Kunjungan Kerja</option>
                        <option value="personal">👤 Study Banding</option>
                        <option value="other">📋 Lainnya</option>
                </select>
                <button onclick="applyFilter()" class="bg-blue-500 hover:bg-blue-600 text-white px-6 py-2 rounded-lg font-medium transition-all duration-300">
                    <span class="mr-1">🔍</span>Filter
                </button>
                <button onclick="clearFilter()" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg font-medium transition-all duration-300">
                    <span class="mr-1">🔄</span>Reset
                </button>
            </div>

            <!-- Data Table -->
            <div class="overflow-x-auto rounded-xl border border-gray-200">
                <table class="w-full border-collapse table-glass">
                    <thead class="bg-gradient-to-r from-gray-50/90 to-blue-50/90 backdrop-blur-sm">
                        <tr>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">No</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Tanggal Kunjungan</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Jam Kunjungan</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Nama Pemohon</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Jabatan</th>
							<th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Instansi</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Tujuan</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Jumlah Tamu</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Dokumen</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Status</th>
                            <th class="border-b border-gray-200 px-4 py-4 text-left font-semibold text-gray-700">Aksi</th>
                        </tr>
                    </thead>
                    <tbody id="visitTable">
                        <tr>
                            <td colspan="10" class="px-4 py-12 text-center text-gray-500">
                                <div class="text-6xl mb-4">📝</div>
                                <p class="text-lg font-medium">Belum ada data kunjungan</p>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Success Modal -->
    <div id="successModal" class="fixed inset-0 bg-black bg-opacity-50 hidden items-center justify-center z-50">
        <div class="glass-card rounded-2xl p-8 max-w-md mx-4 card-shadow border-t-4 border-green-500">
            <div class="text-center">
                <div class="text-6xl mb-4">✅</div>
                <h3 class="text-2xl font-bold bg-gradient-to-r from-green-600 to-blue-600 bg-clip-text text-transparent mb-2">Registrasi Berhasil!</h3>
                <p class="text-gray-700 mb-6">Data kunjungan Anda telah tersimpan. Terima kasih!</p>
                <button onclick="closeModal()" class="btn-success text-white px-8 py-3 rounded-xl font-medium">
                    <span class="mr-2">👍</span>Tutup
                </button>
            </div>
        </div>
    </div>


    <script>
        // Data storage
        let visitData = JSON.parse(localStorage.getItem('visitData')) || [];
        let isAdminLoggedIn = localStorage.getItem('adminLoggedIn') === 'true';
        let uploadedFiles1 = []; // Documents
        let uploadedFiles2 = []; // Images

        // Admin credentials
        const adminCredentials = {
            username: 'admin',
            password: 'maspro'
        };

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            showVisitorForm();
            updateAdminStats();
            renderVisitTable();
            updateLoginStatus();
            setupFileUpload();
        });

        // File upload setup
        function setupFileUpload() {
            // Setup for first upload area (Documents)
            const dropZone1 = document.getElementById('dropZone1');
            const fileInput1 = document.getElementById('fileInput1');

            dropZone1.addEventListener('click', () => fileInput1.click());
            dropZone1.addEventListener('dragover', (e) => handleDragOver(e, 1));
            dropZone1.addEventListener('dragleave', (e) => handleDragLeave(e, 1));
            dropZone1.addEventListener('drop', (e) => handleDrop(e, 1));
            fileInput1.addEventListener('change', (e) => handleFileSelect(e, 1));

            // Setup for second upload area (Images)
            const dropZone2 = document.getElementById('dropZone2');
            const fileInput2 = document.getElementById('fileInput2');

            dropZone2.addEventListener('click', () => fileInput2.click());
            dropZone2.addEventListener('dragover', (e) => handleDragOver(e, 2));
            dropZone2.addEventListener('dragleave', (e) => handleDragLeave(e, 2));
            dropZone2.addEventListener('drop', (e) => handleDrop(e, 2));
            fileInput2.addEventListener('change', (e) => handleFileSelect(e, 2));
        }

        function handleDragOver(e, zone) {
            e.preventDefault();
            e.currentTarget.classList.add('drag-over');
        }

        function handleDragLeave(e, zone) {
            e.preventDefault();
            e.currentTarget.classList.remove('drag-over');
        }

        function handleDrop(e, zone) {
            e.preventDefault();
            e.currentTarget.classList.remove('drag-over');
            const files = Array.from(e.dataTransfer.files);
            processFiles(files, zone);
        }

        function handleFileSelect(e, zone) {
            const files = Array.from(e.target.files);
            processFiles(files, zone);
        }

        function processFiles(files, zone) {
            const allowedTypes1 = ['application/pdf', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document'];
            const allowedTypes2 = ['application/pdf', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document', 'image/jpeg', 'image/jpg', 'image/png'];
            const maxSize = 5 * 1024 * 1024; // 5MB
            const errorDiv = document.getElementById(`uploadError${zone}`);
            const allowedTypes = zone === 1 ? allowedTypes1 : allowedTypes2;
            const uploadedFiles = zone === 1 ? uploadedFiles1 : uploadedFiles2;
            const fileTypeText = zone === 1 ? 'PDF, DOC, atau DOCX' : 'PDF, DOC, DOCX, JPG, atau PNG';
            
            errorDiv.classList.add('hidden');

            files.forEach(file => {
                if (!allowedTypes.includes(file.type)) {
                    showUploadError(`❌ File ${file.name} tidak didukung. Gunakan ${fileTypeText}.`, zone);
                    return;
                }

                if (file.size > maxSize) {
                    showUploadError(`❌ File ${file.name} terlalu besar. Maksimal 5MB.`, zone);
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    const fileData = {
                        name: file.name,
                        type: file.type,
                        size: file.size,
                        data: e.target.result,
                        category: zone === 1 ? 'document' : 'image'
                    };
                    if (zone === 1) {
                        uploadedFiles1.push(fileData);
                    } else {
                        uploadedFiles2.push(fileData);
                    }
                    displayFileList(zone);
                };
                reader.readAsDataURL(file);
            });
        }

        function showUploadError(message, zone) {
            const errorDiv = document.getElementById(`uploadError${zone}`);
            errorDiv.innerHTML = `<div class="bg-red-50/80 backdrop-blur-sm border border-red-200 rounded-lg p-3">${message}</div>`;
            errorDiv.classList.remove('hidden');
        }

        function displayFileList(zone) {
            const fileList = document.getElementById(`fileList${zone}`);
            const uploadedFiles = zone === 1 ? uploadedFiles1 : uploadedFiles2;
            
            fileList.innerHTML = uploadedFiles.map((file, index) => `
                <div class="flex items-center justify-between bg-gradient-to-r from-green-50/80 to-blue-50/80 backdrop-blur-sm p-3 rounded-xl border border-green-200">
                    <div class="flex items-center space-x-3">
                        <span class="text-xl">${getFileIcon(file.type)}</span>
                        <div>
                            <div class="font-semibold text-sm text-gray-800">${file.name}</div>
                            <div class="text-xs text-gray-600">${formatFileSize(file.size)}</div>
                        </div>
                    </div>
                    <button onclick="removeFile(${index}, ${zone})" class="text-red-500 hover:text-red-700 bg-red-100/80 hover:bg-red-200/80 backdrop-blur-sm p-2 rounded-lg transition-all duration-300">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                        </svg>
                    </button>
                </div>
            `).join('');
        }

        function removeFile(index, zone) {
            if (zone === 1) {
                uploadedFiles1.splice(index, 1);
            } else {
                uploadedFiles2.splice(index, 1);
            }
            displayFileList(zone);
        }

        function getFileIcon(type) {
            if (type.includes('pdf')) return '📄';
            if (type.includes('word') || type.includes('document')) return '📝';
            if (type.includes('image')) return '🖼️';
            return '📎';
        }

        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }

        // Form switching
        function showVisitorForm() {
            document.getElementById('visitorForm').classList.remove('hidden');
            document.getElementById('adminPanel').classList.add('hidden');
            document.getElementById('adminLogin').classList.add('hidden');
            document.getElementById('visitorBtn').classList.add('bg-white', 'bg-opacity-30');
            document.getElementById('visitorBtn').classList.remove('bg-opacity-10');
            document.getElementById('adminBtn').classList.add('bg-opacity-10');
            document.getElementById('adminBtn').classList.remove('bg-opacity-30');
        }

        function showAdminLogin() {
            if (isAdminLoggedIn) {
                showAdminPanel();
                return;
            }
            document.getElementById('visitorForm').classList.add('hidden');
            document.getElementById('adminPanel').classList.add('hidden');
            document.getElementById('adminLogin').classList.remove('hidden');
            document.getElementById('adminBtn').classList.add('bg-white', 'bg-opacity-30');
            document.getElementById('adminBtn').classList.remove('bg-opacity-10');
            document.getElementById('visitorBtn').classList.add('bg-opacity-10');
            document.getElementById('visitorBtn').classList.remove('bg-opacity-30');
        }

        function showAdminPanel() {
            if (!isAdminLoggedIn) {
                showAdminLogin();
                return;
            }
            document.getElementById('visitorForm').classList.add('hidden');
            document.getElementById('adminLogin').classList.add('hidden');
            document.getElementById('adminPanel').classList.remove('hidden');
            document.getElementById('adminBtn').classList.add('bg-white', 'bg-opacity-30');
            document.getElementById('adminBtn').classList.remove('bg-opacity-10');
            document.getElementById('visitorBtn').classList.add('bg-opacity-10');
            document.getElementById('visitorBtn').classList.remove('bg-opacity-30');
            updateAdminStats();
            renderVisitTable();
        }

        function updateLoginStatus() {
            const logoutBtn = document.getElementById('logoutBtn');
            
            if (isAdminLoggedIn) {
                logoutBtn.classList.remove('hidden');
            } else {
                logoutBtn.classList.add('hidden');
            }
        }

        function adminLogout() {
            isAdminLoggedIn = false;
            localStorage.removeItem('adminLoggedIn');
            updateLoginStatus();
            showVisitorForm();
            alert('✅ Anda telah logout dari panel admin');
        }

        // Admin login form submission
        document.getElementById('adminLoginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const username = document.getElementById('adminUsername').value;
            const password = document.getElementById('adminPassword').value;
            const errorDiv = document.getElementById('loginError');
            
            if (username === adminCredentials.username && password === adminCredentials.password) {
                isAdminLoggedIn = true;
                localStorage.setItem('adminLoggedIn', 'true');
                updateLoginStatus();
                showAdminPanel();
                
                document.getElementById('adminLoginForm').reset();
                errorDiv.classList.add('hidden');
            } else {
                errorDiv.classList.remove('hidden');
                document.getElementById('adminPassword').value = '';
            }
        });

        // Visitor form submission
        document.getElementById('visitForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = {
                id: Date.now(),
                visitDate: document.getElementById('visitDate').value,
                visitTime: document.getElementById('visitTime').value,
                guestCount: parseInt(document.getElementById('guestCount').value),
                fullName: document.getElementById('fullName').value,
                email: document.getElementById('email').value,
                phoneNumber: document.getElementById('phoneNumber').value,
                position: document.getElementById('position').value,
                institution: document.getElementById('institution').value,
                visitPurpose: document.getElementById('visitPurpose').value,
                visitDetails: document.getElementById('visitDetails').value,
                documents: [...uploadedFiles1, ...uploadedFiles2],
                status: 'pending',
                registeredAt: new Date().toISOString()
            };

            visitData.push(formData);
            localStorage.setItem('visitData', JSON.stringify(visitData));
            
            // Reset form and files
            document.getElementById('visitForm').reset();
            uploadedFiles1 = [];
            uploadedFiles2 = [];
            displayFileList(1);
            displayFileList(2);
            
            // Show success modal
            document.getElementById('successModal').classList.remove('hidden');
            document.getElementById('successModal').classList.add('flex');
        });

        // Modal functions
        function closeModal() {
            document.getElementById('successModal').classList.add('hidden');
            document.getElementById('successModal').classList.remove('flex');
        }

        // Admin functions
        function updateAdminStats() {
            const today = new Date().toISOString().split('T')[0];
            const todayVisits = visitData.filter(visit => visit.visitDate === today).length;
            const totalGuests = visitData.reduce((sum, visit) => sum + visit.guestCount, 0);
            const pendingVisits = visitData.filter(visit => visit.status === 'pending').length;

            document.getElementById('totalVisits').textContent = visitData.length;
            document.getElementById('todayVisits').textContent = todayVisits;
            document.getElementById('totalGuests').textContent = totalGuests;
            document.getElementById('pendingVisits').textContent = pendingVisits;
        }

        function renderVisitTable(filteredData = null) {
            const data = filteredData || visitData;
            const tbody = document.getElementById('visitTable');
            
            if (data.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="10" class="px-4 py-12 text-center text-gray-500">
                            <div class="text-6xl mb-4">📝</div>
                            <p class="text-lg font-medium">Belum ada data kunjungan</p>
                        </td>
                    </tr>
                `;
                return;
            }

            tbody.innerHTML = data.map((visit, index) => `
                <tr class="hover:bg-gradient-to-r hover:from-blue-50/50 hover:to-purple-50/50 transition-all duration-300 ${index % 2 === 0 ? 'bg-gray-50/50' : 'bg-white/50'} backdrop-blur-sm">
                    <td class="border-b border-gray-100 px-4 py-4 font-medium">${index + 1}</td>
                    <td class="border-b border-gray-100 px-4 py-4">${visit.visitDate}</td>
                    <td class="border-b border-gray-100 px-4 py-4">${visit.visitTime}</td>
                    <td class="border-b border-gray-100 px-4 py-4">
                        <div class="font-semibold text-gray-800">${visit.fullName}</div>
                        <div class="text-sm text-blue-600">${visit.email}</div>
                        <div class="text-sm text-gray-500">${visit.phoneNumber}</div>
                    </td>
                    <td class="border-b border-gray-100 px-4 py-4">
                        <div class="font-semibold text-gray-800">${visit.institution}</div>
                        <div class="text-sm text-gray-500">${visit.position}</div>
                    </td>
                    <td class="border-b border-gray-100 px-4 py-4">
                        <div class="font-semibold text-gray-800">${getPurposeText(visit.visitPurpose)}</div>
                        <div class="text-sm text-gray-500">${visit.visitDetails.substring(0, 50)}...</div>
                    </td>
                    <td class="border-b border-gray-100 px-4 py-4 text-center">
                        <span class="bg-blue-100/80 backdrop-blur-sm text-blue-800 px-3 py-1 rounded-full text-sm font-medium">${visit.guestCount}</span>
                    </td>
                    <td class="border-b border-gray-100 px-4 py-4">
                        ${visit.documents && visit.documents.length > 0 ? 
                            `<div class="space-y-1">
                                ${visit.documents.map(doc => `
                                    <div class="flex items-center space-x-2">
                                        <span class="text-sm">${getFileIcon(doc.type)}</span>
                                        <button onclick="downloadFile('${doc.data}', '${doc.name}')" class="text-blue-600 hover:text-blue-800 text-xs underline font-medium">
                                            ${doc.name.length > 12 ? doc.name.substring(0, 12) + '...' : doc.name}
                                        </button>
                                        <span class="text-xs px-2 py-1 rounded-full ${doc.category === 'document' ? 'bg-blue-100 text-blue-700' : 'bg-green-100 text-green-700'}">${doc.category === 'document' ? '📄' : '🖼️'}</span>
                                    </div>
                                `).join('')}
                            </div>` : 
                            '<span class="text-gray-400 text-sm">Tidak ada</span>'
                        }
                    </td>
                    <td class="border-b border-gray-100 px-4 py-4">
                        <span class="px-3 py-1 rounded-full text-xs font-semibold ${getStatusClass(visit.status)}">
                            ${getStatusText(visit.status)}
                        </span>
                    </td>
                    <td class="border-b border-gray-100 px-4 py-4">
                        <div class="flex space-x-2">
                            <button onclick="updateStatus(${visit.id}, 'approved')" class="bg-green-500 hover:bg-green-600 text-white px-3 py-1 rounded-lg text-xs font-medium transition-all duration-300">
                                ✅ Setujui
                            </button>
                            <button onclick="updateStatus(${visit.id}, 'rejected')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded-lg text-xs font-medium transition-all duration-300">
                                ❌ Tolak
                            </button>
                            <button onclick="deleteVisit(${visit.id})" class="bg-gray-500 hover:bg-gray-600 text-white px-3 py-1 rounded-lg text-xs font-medium transition-all duration-300">
                                🗑️ Hapus
                            </button>
                        </div>
                    </td>
                </tr>
            `).join('');
        }

        function getPurposeText(purpose) {
            const purposes = {
                'consultation': '💬 Audiensi',
				'business': '💼 Kunjungan Kerja',
                'personal': '👤 Study Banding',
                'other': '📋 Lainnya'
            };
            return purposes[purpose] || purpose;
        }

        function getStatusText(status) {
            const statuses = {
                'pending': '⏳ Menunggu',
                'approved': '✅ Disetujui',
                'rejected': '❌ Ditolak'
            };
            return statuses[status] || status;
        }

        function getStatusClass(status) {
            const classes = {
                'pending': 'bg-yellow-100/80 backdrop-blur-sm text-yellow-800 border border-yellow-200',
                'approved': 'bg-green-100/80 backdrop-blur-sm text-green-800 border border-green-200',
                'rejected': 'bg-red-100/80 backdrop-blur-sm text-red-800 border border-red-200'
            };
            return classes[status] || 'bg-gray-100/80 backdrop-blur-sm text-gray-800 border border-gray-200';
        }

        function updateStatus(id, newStatus) {
            const visit = visitData.find(v => v.id === id);
            if (!visit) return;
            
            visitData = visitData.map(v => 
                v.id === id ? { ...v, status: newStatus, updatedAt: new Date().toISOString() } : v
            );
            localStorage.setItem('visitData', JSON.stringify(visitData));
            
            // Send email notification to visitor
            sendEmailNotification(visit, newStatus);
            
            updateAdminStats();
            renderVisitTable();
        }

        function sendEmailNotification(visit, status) {
            // Email notification system (Demo - shows what would be sent)
            const statusMessages = {
                'approved': {
                    subject: '✅ Kunjungan Anda Telah Disetujui',
                    message: `Selamat! Kunjungan Anda pada ${visit.visitDate} pukul ${visit.visitTime} telah disetujui. Silakan datang sesuai jadwal yang telah ditentukan.`,
                    color: 'green'
                },
                'rejected': {
                    subject: '❌ Kunjungan Anda Tidak Dapat Disetujui',
                    message: `Mohon maaf, kunjungan Anda pada ${visit.visitDate} pukul ${visit.visitTime} tidak dapat disetujui. Silakan hubungi admin untuk informasi lebih lanjut.`,
                    color: 'red'
                }
            };

            const emailData = statusMessages[status];
            if (!emailData) return;

            // Show notification modal (simulating email sent)
            showEmailNotification(visit, emailData);
            
            // In real implementation, this would call an email service API
            console.log('Email would be sent to:', visit.email);
            console.log('Subject:', emailData.subject);
            console.log('Message:', emailData.message);
        }

        function showEmailNotification(visit, emailData) {
            // Create and show email notification modal
            const modal = document.createElement('div');
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            modal.innerHTML = `
                <div class="glass-card rounded-2xl p-8 max-w-md mx-4 card-shadow border-t-4 border-${emailData.color}-500">
                    <div class="text-center">
                        <div class="text-6xl mb-4">${emailData.color === 'green' ? '📧' : '📨'}</div>
                        <h3 class="text-2xl font-bold bg-gradient-to-r from-${emailData.color}-600 to-blue-600 bg-clip-text text-transparent mb-2">Email Terkirim!</h3>
                        <div class="text-left bg-gradient-to-r from-gray-50/80 to-blue-50/80 backdrop-blur-sm p-4 rounded-xl border border-gray-200 mb-6">
                            <p class="text-sm text-gray-600 mb-2"><strong>Kepada:</strong> ${visit.email}</p>
                            <p class="text-sm text-gray-600 mb-2"><strong>Subjek:</strong> ${emailData.subject}</p>
                            <p class="text-sm text-gray-700"><strong>Pesan:</strong></p>
                            <p class="text-sm text-gray-600 mt-1 italic">"${emailData.message}"</p>
                        </div>
                        <button onclick="this.parentElement.parentElement.parentElement.remove()" class="btn-${emailData.color === 'green' ? 'success' : 'danger'} text-white px-8 py-3 rounded-xl font-medium">
                            <span class="mr-2">👍</span>Tutup
                        </button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
            
            // Auto remove after 5 seconds
            setTimeout(() => {
                if (modal.parentElement) {
                    modal.remove();
                }
            }, 5000);
        }

        function deleteVisit(id) {
            if (confirm('🗑️ Apakah Anda yakin ingin menghapus data kunjungan ini?')) {
                visitData = visitData.filter(visit => visit.id !== id);
                localStorage.setItem('visitData', JSON.stringify(visitData));
                updateAdminStats();
                renderVisitTable();
            }
        }

        function clearAllData() {
            if (confirm('🗑️ Apakah Anda yakin ingin menghapus semua data kunjungan?')) {
                visitData = [];
                localStorage.removeItem('visitData');
                updateAdminStats();
                renderVisitTable();
            }
        }

        function applyFilter() {
            const filterDate = document.getElementById('filterDate').value;
            const filterPurpose = document.getElementById('filterPurpose').value;
            
            let filteredData = visitData;
            
            if (filterDate) {
                filteredData = filteredData.filter(visit => visit.visitDate === filterDate);
            }
            
            if (filterPurpose) {
                filteredData = filteredData.filter(visit => visit.visitPurpose === filterPurpose);
            }
            
            renderVisitTable(filteredData);
        }

        function clearFilter() {
            document.getElementById('filterDate').value = '';
            document.getElementById('filterPurpose').value = '';
            renderVisitTable();
        }

        function downloadFile(dataUrl, filename) {
            const a = document.createElement('a');
            a.href = dataUrl;
            a.download = filename;
            a.click();
        }

        function exportData() {
            if (visitData.length === 0) {
                alert('❌ Tidak ada data untuk diekspor');
                return;
            }
            
            const csvContent = [
                ['No', 'Tanggal', 'Jam', 'Nama', 'Email', 'HP', 'Jabatan', 'Instansi', 'Tujuan', 'Keperluan', 'Jumlah Tamu', 'Dokumen', 'Status'],
                ...visitData.map((visit, index) => [
                    index + 1,
                    visit.visitDate,
                    visit.visitTime,
                    visit.fullName,
                    visit.email,
                    visit.phoneNumber,
                    visit.position,
                    visit.institution,
                    getPurposeText(visit.visitPurpose).replace(/[💬💼👤📋]/g, '').trim(),
                    visit.visitDetails,
                    visit.guestCount,
                    visit.documents ? visit.documents.map(doc => doc.name).join('; ') : 'Tidak ada',
                    getStatusText(visit.status).replace(/[⏳✅❌]/g, '').trim()
                ])
            ].map(row => row.join(',')).join('\n');
            
            const blob = new Blob([csvContent], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `buku-tamu-${new Date().toISOString().split('T')[0]}.csv`;
            a.click();
            window.URL.revokeObjectURL(url);
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'96d46c8e75a47a69',t:'MTc1NDg4MDYxMS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
