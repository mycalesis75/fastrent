<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FastRent - เช่าอุปกรณ์ IT ออนไลน์</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .btn-gradient {
            background: linear-gradient(135deg, #1f2937 0%, #374151 100%);
        }
        .btn-gradient:hover {
            background: linear-gradient(135deg, #111827 0%, #1f2937 100%);
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(31, 41, 55, 0.3);
        }
        .card-hover {
            transition: all 0.3s ease;
        }
        .card-hover:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }
        .hero-gradient {
            background: linear-gradient(135deg, #1f2937 0%, #374151 50%, #4b5563 100%);
        }
        
        /* Floating animation */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        .float-animation {
            animation: float 3s ease-in-out infinite;
        }
        
        /* Pulse animation */
        @keyframes pulse-glow {
            0%, 100% { box-shadow: 0 0 20px rgba(37, 99, 235, 0.3); }
            50% { box-shadow: 0 0 30px rgba(37, 99, 235, 0.6); }
        }
        .pulse-glow {
            animation: pulse-glow 2s ease-in-out infinite;
        }
        
        /* Gradient text animation */
        @keyframes gradient-shift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .gradient-text {
            background: linear-gradient(-45deg, #f8fafc, #e2e8f0, #cbd5e1, #94a3b8);
            background-size: 400% 400%;
            animation: gradient-shift 3s ease infinite;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        /* Shimmer effect */
        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }
        .shimmer {
            position: relative;
            overflow: hidden;
        }
        .shimmer::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
            transform: translateX(-100%);
            animation: shimmer 2s infinite;
        }

        /* Category card animations */
        @keyframes bounce-in {
            0% { transform: scale(0.3) rotate(-10deg); opacity: 0; }
            50% { transform: scale(1.05) rotate(5deg); }
            70% { transform: scale(0.9) rotate(-2deg); }
            100% { transform: scale(1) rotate(0deg); opacity: 1; }
        }
        
        .category-card {
            animation: bounce-in 0.6s ease-out;
        }
        
        .category-card:hover {
            transform: translateY(-10px) scale(1.05);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
        }

        /* Cart icon styling */
        .cart-icon-bg {
            background: linear-gradient(135deg, #1f2937 0%, #374151 100%);
            border-radius: 50%;
            padding: 8px;
        }
    </style>
</head>
<body class="bg-white font-sans text-gray-900">
    <!-- Navigation -->
    <nav class="bg-white shadow-lg sticky top-0 z-40 border-b border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center space-x-4">
                    <button onclick="goToHome()" class="flex items-center space-x-3 hover:scale-105 transition duration-300 cursor-pointer">
                        <img src="https://github.com/Phurisit/Phurisit/blob/main/Main%20logo.png?raw=true" alt="FastRent Logo" class="h-10 w-auto" onerror="this.style.display='none';">
                        <span class="text-2xl font-bold text-gray-900">FastRent</span>
                    </button>
                </div>
                
                <div class="hidden md:flex items-center space-x-8">
                    <button onclick="goToHome()" class="text-gray-700 hover:text-gray-900 transition duration-300 font-medium">หน้าหลัก</button>
                    <button onclick="scrollToSection('about')" class="text-gray-700 hover:text-gray-900 transition duration-300 font-medium">เกี่ยวกับเรา</button>
                    <button onclick="scrollToSection('contact')" class="text-gray-700 hover:text-gray-900 transition duration-300 font-medium">ติดต่อเรา</button>
                </div>

                <div class="flex items-center space-x-4">
                    <!-- Cart -->
                    <button onclick="showCartModal()" class="relative p-2 text-gray-700 hover:text-gray-900 transition duration-300">
                        <div class="cart-icon-bg">
                            <img src="https://github.com/Phurisit/Phurisit/blob/main/Cart.png?raw=true" alt="Cart" class="w-6 h-6" onerror="this.style.display='none'; this.nextElementSibling.style.display='inline';">
                            <span class="text-2xl hidden">🛒</span>
                        </div>
                        <span id="cartBadge" class="absolute -top-1 -right-1 bg-gray-900 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center hidden">0</span>
                    </button>

                    <!-- Auth Section -->
                    <div id="loginBtn">
                        <button onclick="showLoginModal()" class="bg-gray-900 text-white px-4 py-2 rounded-lg font-medium hover:bg-gray-800 hover:shadow-lg transition duration-300">
                            เข้าสู่ระบบ
                        </button>
                    </div>
                    
                    <div id="profileSection" class="hidden relative">
                        <button onclick="toggleProfileMenu()" class="text-gray-700 hover:text-gray-900 transition duration-300 flex items-center space-x-2">
                            <div class="cart-icon-bg">
                                <img src="https://github.com/Phurisit/Phurisit/blob/main/Profile.png?raw=true" alt="Profile" class="w-6 h-6" onerror="this.style.display='none'; this.nextElementSibling.style.display='inline';">
                                <span class="text-2xl hidden">👤</span>
                            </div>
                            <span class="text-sm">▼</span>
                        </button>
                        <div id="profileMenu" class="hidden absolute right-0 top-full mt-2 bg-white rounded-lg shadow-lg border border-gray-200 py-2 w-48 z-50">
                            <button onclick="showPage('profile')" class="block w-full text-left px-4 py-2 text-gray-700 hover:bg-gray-100 transition duration-300">
                                👤 โปรไฟล์
                            </button>
                            <hr class="my-1 border-gray-200">
                            <button onclick="handleLogout()" class="block w-full text-left px-4 py-2 text-red-600 hover:bg-red-50 transition duration-300">
                                🚪 ออกจากระบบ
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- Home Page -->
    <div id="homePage">
        <!-- Hero Section -->
        <section class="bg-gradient-to-br from-gray-900 via-gray-800 to-gray-900 py-20 relative overflow-hidden">
            <div class="absolute inset-0 bg-gradient-to-r from-gray-900/80 to-gray-900/80"></div>
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center relative">
                <h1 class="text-5xl md:text-6xl font-bold mb-6 gradient-text">
                    FastRent - เช่าอุปกรณ์ IT
                </h1>
                <p class="text-xl md:text-2xl mb-8 text-gray-300 max-w-3xl mx-auto">
                    บริการเช่าอุปกรณ์เทคโนโลยีคุณภาพสูง ราคาประหยัด ส่งถึงที่ ทั่วประเทศไทย
                </p>
                
                <button onclick="scrollToSection('categories')" class="bg-gradient-to-r from-gray-800 to-gray-900 text-white px-8 py-4 rounded-full text-lg font-semibold hover:shadow-xl transition duration-300 transform hover:scale-105">
                    🚀 เริ่มเช่าเลย
                </button>
            </div>
        </section>

        <!-- Search Section -->
        <section class="bg-white py-8">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="max-w-2xl mx-auto">
                    <div class="relative">
                        <input type="text" id="searchInput" placeholder="ค้นหาสินค้าที่ต้องการ..." 
                               class="w-full bg-white text-gray-900 placeholder-gray-500 px-6 py-4 rounded-full border-2 border-gray-300 focus:outline-none focus:ring-2 focus:ring-gray-900 focus:border-gray-900 shadow-lg text-lg">
                        <button onclick="searchProducts()" class="absolute right-3 top-3 bg-gray-900 text-white p-2 rounded-full hover:bg-gray-800 hover:shadow-lg transition duration-300">
                            🔍
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Categories -->
        <section id="categories" class="py-16 bg-white">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center mb-12">
                    <img src="https://github.com/Phurisit/Phurisit/blob/main/Black%20category.png?raw=true" alt="Categories" class="h-16 w-auto mx-auto mb-4" onerror="this.style.display='none';">
                    <h2 class="text-3xl font-bold text-gray-900">หมวดหมู่สินค้า</h2>
                </div>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                    <button onclick="showProducts('camera')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.1s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">📷</div>
                        <h3 class="font-semibold text-gray-900 mb-1">กล้อง</h3>
                        <p class="text-sm text-gray-600">DSLR, Mirrorless</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-blue-500 to-purple-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('laptop')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.2s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">💻</div>
                        <h3 class="font-semibold text-gray-900 mb-1">แล็ปท็อป</h3>
                        <p class="text-sm text-gray-600">MacBook, Dell, HP</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-green-500 to-blue-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('computer')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.3s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">🖥️</div>
                        <h3 class="font-semibold text-gray-900 mb-1">คอมพิวเตอร์</h3>
                        <p class="text-sm text-gray-600">iMac, Gaming PC</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-purple-500 to-pink-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('printer')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.4s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">🖨️</div>
                        <h3 class="font-semibold text-gray-900 mb-1">เครื่องพิมพ์</h3>
                        <p class="text-sm text-gray-600">Canon, HP, Epson</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-orange-500 to-red-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('tablet')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.5s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">📱</div>
                        <h3 class="font-semibold text-gray-900 mb-1">แท็บเล็ต</h3>
                        <p class="text-sm text-gray-600">iPad, Surface</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-teal-500 to-cyan-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('monitor')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.6s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">🖥️</div>
                        <h3 class="font-semibold text-gray-900 mb-1">จอมอนิเตอร์</h3>
                        <p class="text-sm text-gray-600">4K, Ultrawide</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-indigo-500 to-purple-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('projector')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.7s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">📽️</div>
                        <h3 class="font-semibold text-gray-900 mb-1">โปรเจคเตอร์</h3>
                        <p class="text-sm text-gray-600">4K, Portable</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-yellow-500 to-orange-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                    
                    <button onclick="showProducts('network')" class="category-card bg-gradient-to-br from-white to-gray-50 hover:from-gray-50 hover:to-gray-100 p-6 rounded-xl text-center transition-all duration-500 border-2 border-gray-200 hover:border-gray-900 shadow-lg hover:shadow-2xl transform" style="animation-delay: 0.8s">
                        <div class="text-4xl mb-3 transform hover:scale-110 transition-transform duration-300">🌐</div>
                        <h3 class="font-semibold text-gray-900 mb-1">เครือข่าย</h3>
                        <p class="text-sm text-gray-600">Router, Switch</p>
                        <div class="mt-3 w-full h-1 bg-gradient-to-r from-emerald-500 to-teal-500 rounded-full opacity-0 hover:opacity-100 transition-opacity duration-300"></div>
                    </button>
                </div>
                
                <div class="text-center mt-8">
                    <button onclick="showAllProducts()" class="bg-gradient-to-r from-gray-800 to-gray-900 text-white px-6 py-3 rounded-full font-medium hover:shadow-lg transition duration-300 transform hover:scale-105">
                        ดูสินค้าทั้งหมด
                    </button>
                </div>
            </div>
        </section>

        <!-- Products Section -->
        <section id="products" class="py-16 bg-white">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <h2 class="text-3xl font-bold text-center mb-12 text-gray-900">สินค้าแนะนำ</h2>
                <div id="productsGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
                    <!-- Products will be rendered here -->
                </div>
            </div>
        </section>

        <!-- About Section -->
        <section id="about" class="py-16 bg-gray-900">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-white mb-6">เกี่ยวกับ FastRent</h2>
                    <p class="text-xl text-gray-300 max-w-3xl mx-auto">
                        เราคือผู้นำด้านการให้เช่าอุปกรณ์เทคโนโลยีในประเทศไทย ด้วยประสบการณ์กว่า 10 ปี
                    </p>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div class="text-center p-6 bg-gray-900 rounded-xl border border-gray-700">
                        <div class="text-4xl mb-4">⚡</div>
                        <h3 class="text-xl font-semibold text-white mb-3">รวดเร็ว</h3>
                        <p class="text-gray-300">ส่งของภายใน 24 ชั่วโมง ทั่วกรุงเทพและปริมณฑล</p>
                    </div>
                    
                    <div class="text-center p-6 bg-gray-900 rounded-xl border border-gray-700">
                        <div class="text-4xl mb-4">🛡️</div>
                        <h3 class="text-xl font-semibold text-white mb-3">ปลอดภัย</h3>
                        <p class="text-gray-300">อุปกรณ์ทุกชิ้นผ่านการตรวจสอบและทำความสะอาดแล้ว</p>
                    </div>
                    
                    <div class="text-center p-6 bg-gray-900 rounded-xl border border-gray-700">
                        <div class="text-4xl mb-4">💰</div>
                        <h3 class="text-xl font-semibold text-white mb-3">ประหยัด</h3>
                        <p class="text-gray-300">ราคาเช่าเริ่มต้นเพียงวันละ 100 บาท</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contact Section -->
        <section id="contact" class="py-16 bg-gray-900">
            <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
                <h2 class="text-3xl font-bold text-center mb-12 text-white">ติดต่อเรา</h2>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                    <div>
                        <h3 class="text-xl font-semibold mb-6 text-white">ข้อมูลติดต่อ</h3>
                        <div class="space-y-4">
                            <div class="flex items-center space-x-3">
                                <span class="text-2xl">📍</span>
                                <div>
                                    <p class="font-medium text-white">ที่อยู่</p>
                                    <p class="text-gray-300">123 ถนนเทคโนโลยี แขวงนวัตกรรม เขตดิจิทัล กรุงเทพฯ 10110</p>
                                </div>
                            </div>
                            
                            <div class="flex items-center space-x-3">
                                <span class="text-2xl">📞</span>
                                <div>
                                    <p class="font-medium text-white">โทรศัพท์</p>
                                    <p class="text-gray-300">02-123-4567</p>
                                </div>
                            </div>
                            
                            <div class="flex items-center space-x-3">
                                <span class="text-2xl">📧</span>
                                <div>
                                    <p class="font-medium text-white">อีเมล</p>
                                    <p class="text-gray-300">info@fastrent.co.th</p>
                                </div>
                            </div>
                            
                            <div class="flex items-center space-x-3">
                                <span class="text-2xl">⏰</span>
                                <div>
                                    <p class="font-medium text-white">เวลาทำการ</p>
                                    <p class="text-gray-300">จันทร์-ศุกร์ 9:00-18:00<br>เสาร์-อาทิตย์ 10:00-16:00</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="mt-8">
                            <h4 class="font-semibold mb-4 text-white">ติดตามเรา</h4>
                            <div class="flex space-x-4">
                                <a href="https://facebook.com/fastrent" target="_blank" class="text-3xl hover:scale-110 transition duration-300">📘</a>
                                <a href="https://line.me/@fastrent" target="_blank" class="text-3xl hover:scale-110 transition duration-300">💬</a>
                                <a href="https://instagram.com/fastrent" target="_blank" class="text-3xl hover:scale-110 transition duration-300">📷</a>
                            </div>
                        </div>
                    </div>
                    
                    <div>
                        <h3 class="text-xl font-semibold mb-6 text-white">ส่งข้อความถึงเรา</h3>
                        <form onsubmit="handleContactForm(event)" class="space-y-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-300 mb-2">ชื่อ-นามสกุล</label>
                                <input type="text" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกชื่อ-นามสกุล">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-300 mb-2">อีเมล</label>
                                <input type="email" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกอีเมล">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-300 mb-2">เบอร์โทรศัพท์</label>
                                <input type="tel" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกเบอร์โทรศัพท์">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-300 mb-2">ข้อความ</label>
                                <textarea required rows="4" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกข้อความที่ต้องการสอบถาม"></textarea>
                            </div>
                            
                            <button type="submit" class="w-full btn-gradient text-white py-3 rounded-lg font-medium hover:shadow-lg transition duration-300">
                                ส่งข้อความ 📧
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- About Page -->
    <div id="aboutPage" style="display: none;" class="min-h-screen bg-gray-900 py-16">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h1 class="text-4xl font-bold text-center mb-12 text-white">เกี่ยวกับ FastRent</h1>
            
            <div class="bg-gray-800 rounded-2xl p-8 mb-8 border border-gray-700">
                <h2 class="text-2xl font-semibold mb-6 text-white">ประวัติความเป็นมา</h2>
                <p class="text-gray-300 leading-relaxed mb-4">
                    FastRent ก่อตั้งขึ้นในปี 2014 ด้วยวิสัยทัศน์ในการทำให้เทคโนโลยีเข้าถึงได้ง่ายสำหรับทุกคน 
                    เราเริ่มต้นจากการให้เช่าแล็ปท็อปสำหรับนักเรียน นักศึกษา และได้ขยายธุรกิจมาเป็นผู้ให้บริการ
                    เช่าอุปกรณ์ IT ครบวงจรในปัจจุบัน
                </p>
                <p class="text-gray-300 leading-relaxed">
                    ด้วยประสบการณ์กว่า 10 ปี เราได้ให้บริการลูกค้ามากกว่า 50,000 ราย ทั้งบุคคลทั่วไป 
                    สถาบันการศึกษา และองค์กรธุรกิจต่างๆ
                </p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-8">
                <div class="bg-gray-800 rounded-xl p-6 border border-gray-700">
                    <h3 class="text-xl font-semibold mb-4 text-white">วิสัยทัศน์</h3>
                    <p class="text-gray-300">
                        เป็นผู้นำในการให้บริการเช่าอุปกรณ์เทคโนโลยีที่ทันสมัย เข้าถึงได้ง่าย 
                        และสร้างคุณค่าให้กับลูกค้าทุกกลุ่ม
                    </p>
                </div>
                
                <div class="bg-gray-800 rounded-xl p-6 border border-gray-700">
                    <h3 class="text-xl font-semibold mb-4 text-white">พันธกิจ</h3>
                    <p class="text-gray-300">
                        มุ่งมั่นให้บริการเช่าอุปกรณ์ IT คุณภาพสูง ด้วยราคาที่เป็นธรรม 
                        และการบริการที่เป็นเลิศ
                    </p>
                </div>
            </div>
            
            <div class="bg-gray-800 rounded-2xl p-8 border border-gray-700">
                <h2 class="text-2xl font-semibold mb-6 text-white">ทีมงาน</h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="text-center">
                        <div class="text-6xl mb-4">👨‍💼</div>
                        <h4 class="font-semibold text-white">คุณสมชาย ใจดี</h4>
                        <p class="text-gray-400">ผู้ก่อตั้งและ CEO</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="text-6xl mb-4">👩‍💻</div>
                        <h4 class="font-semibold text-white">คุณสมหญิง เทคโน</h4>
                        <p class="text-gray-400">CTO</p>
                    </div>
                    
                    <div class="text-center">
                        <div class="text-6xl mb-4">👨‍🔧</div>
                        <h4 class="font-semibold text-white">คุณสมศักดิ์ ซ่อมเก่ง</h4>
                        <p class="text-gray-400">หัวหน้าแผนกเทคนิค</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Contact Page -->
    <div id="contactPage" style="display: none;" class="min-h-screen bg-gray-900 py-16">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h1 class="text-4xl font-bold text-center mb-12 text-white">ติดต่อเรา</h1>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                <div>
                    <h3 class="text-2xl font-semibold mb-8 text-white">ข้อมูลติดต่อ</h3>
                    <div class="space-y-6">
                        <div class="flex items-start space-x-4">
                            <span class="text-3xl">📍</span>
                            <div>
                                <p class="font-semibold text-white text-lg">ที่อยู่สำนักงาน</p>
                                <p class="text-gray-300 mt-1">
                                    123 ถนนเทคโนโลยี แขวงนวัตกรรม<br>
                                    เขตดิจิทัล กรุงเทพฯ 10110
                                </p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-4">
                            <span class="text-3xl">📞</span>
                            <div>
                                <p class="font-semibold text-white text-lg">โทรศัพท์</p>
                                <p class="text-gray-300 mt-1">02-123-4567</p>
                                <p class="text-gray-300">มือถือ: 08-1234-5678</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-4">
                            <span class="text-3xl">📧</span>
                            <div>
                                <p class="font-semibold text-white text-lg">อีเมล</p>
                                <p class="text-gray-300 mt-1">info@fastrent.co.th</p>
                                <p class="text-gray-300">support@fastrent.co.th</p>
                            </div>
                        </div>
                        
                        <div class="flex items-start space-x-4">
                            <span class="text-3xl">⏰</span>
                            <div>
                                <p class="font-semibold text-white text-lg">เวลาทำการ</p>
                                <p class="text-gray-300 mt-1">
                                    จันทร์-ศุกร์: 9:00-18:00<br>
                                    เสาร์-อาทิตย์: 10:00-16:00<br>
                                    วันหยุดนักขัตฤกษ์: ปิดทำการ
                                </p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-10">
                        <h4 class="font-semibold mb-6 text-white text-lg">ติดตามเราได้ที่</h4>
                        <div class="flex space-x-6">
                            <a href="https://facebook.com/fastrent" target="_blank" class="text-4xl hover:scale-110 transition duration-300" title="Facebook">📘</a>
                            <a href="https://line.me/@fastrent" target="_blank" class="text-4xl hover:scale-110 transition duration-300" title="LINE">💬</a>
                            <a href="https://instagram.com/fastrent" target="_blank" class="text-4xl hover:scale-110 transition duration-300" title="Instagram">📷</a>
                            <a href="https://twitter.com/fastrent" target="_blank" class="text-4xl hover:scale-110 transition duration-300" title="Twitter">🐦</a>
                        </div>
                    </div>
                </div>
                
                <div>
                    <h3 class="text-2xl font-semibold mb-8 text-white">ส่งข้อความถึงเรา</h3>
                    <form onsubmit="handleContactForm(event)" class="space-y-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">ชื่อ-นามสกุล *</label>
                            <input type="text" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกชื่อ-นามสกุล">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">อีเมล *</label>
                            <input type="email" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกอีเมล">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">เบอร์โทรศัพท์ *</label>
                            <input type="tel" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกเบอร์โทรศัพท์">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">หัวข้อ</label>
                            <select class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white">
                                <option value="">เลือกหัวข้อ</option>
                                <option value="rental">สอบถามการเช่า</option>
                                <option value="support">ขอความช่วยเหลือ</option>
                                <option value="complaint">ร้องเรียน</option>
                                <option value="suggestion">ข้อเสนอแนะ</option>
                                <option value="other">อื่นๆ</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">ข้อความ *</label>
                            <textarea required rows="5" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกข้อความที่ต้องการสอบถาม"></textarea>
                        </div>
                        
                        <button type="submit" class="w-full btn-gradient text-white py-3 rounded-lg font-medium hover:shadow-lg transition duration-300">
                            ส่งข้อความ 📧
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- Profile Page -->
    <div id="profilePage" style="display: none;" class="min-h-screen bg-gray-900 py-16">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h1 class="text-4xl font-bold text-center mb-12 text-white">โปรไฟล์ของฉัน</h1>
            
            <div class="bg-gray-800 rounded-2xl p-8 mb-8 border border-gray-700">
                <div class="flex items-center space-x-6 mb-8">
                    <div class="text-8xl">👤</div>
                    <div>
                        <h2 class="text-3xl font-semibold text-white">ใจดี มานะ</h2>
                        <p class="text-gray-400 text-lg">สมาชิกตั้งแต่: มกราคม 2024</p>
                        <p class="text-green-400 font-medium">สถานะ: สมาชิกทอง ⭐</p>
                    </div>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-xl font-semibold mb-4 text-white">ข้อมูลส่วนตัว</h3>
                        <div class="space-y-3">
                            <div class="flex justify-between">
                                <span class="text-gray-400">อีเมล:</span>
                                <span class="text-white">jaidee@email.com</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-400">เบอร์โทร:</span>
                                <span class="text-white">08-1234-5678</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-400">วันเกิด:</span>
                                <span class="text-white">15 มิถุนายน 2533</span>
                            </div>
                        </div>
                    </div>
                    
                    <div>
                        <h3 class="text-xl font-semibold mb-4 text-white">สถิติการเช่า</h3>
                        <div class="space-y-3">
                            <div class="flex justify-between">
                                <span class="text-gray-400">จำนวนครั้งที่เช่า:</span>
                                <span class="text-white">28 ครั้ง</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-400">ยอดเช่าสะสม:</span>
                                <span class="text-white">฿50,600</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-400">คะแนนความน่าเชื่อถือ:</span>
                                <span class="text-green-400">⭐⭐⭐⭐⭐ (5.0)</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="bg-gray-800 rounded-xl p-6 border border-gray-700">
                    <h3 class="text-xl font-semibold mb-4 text-white">การเช่าล่าสุด</h3>
                    <div class="space-y-4">
                        <div class="flex items-center space-x-3 p-3 bg-gray-700 rounded-lg">
                            <span class="text-2xl">📷</span>
                            <div class="flex-1">
                                <p class="font-medium text-white">Canon EOS R5</p>
                                <p class="text-sm text-gray-400">30-31 ส.ค. 2025</p>
                            </div>
                            <span class="text-green-400 font-medium">เสร็จสิ้น</span>
                        </div>
                        
                        <div class="flex items-center space-x-3 p-3 bg-gray-700 rounded-lg">
                            <span class="text-2xl">💻</span>
                            <div class="flex-1">
                                <p class="font-medium text-white">MacBook Pro 16"</p>
                                <p class="text-sm text-gray-400">15-20 ม.ค. 2024</p>
                            </div>
                            <span class="text-green-400 font-medium">เสร็จสิ้น</span>
                        </div>
                        
                        <div class="flex items-center space-x-3 p-3 bg-gray-700 rounded-lg">
                            <span class="text-2xl">🖨️</span>
                            <div class="flex-1">
                                <p class="font-medium text-white">Canon PIXMA Pro</p>
                                <p class="text-sm text-gray-400">10-12 ม.ค. 2024</p>
                            </div>
                            <span class="text-green-400 font-medium">เสร็จสิ้น</span>
                        </div>
                    </div>
                </div>
                
                <div class="bg-gray-800 rounded-xl p-6 border border-gray-700">
                    <h3 class="text-xl font-semibold mb-4 text-white">สิทธิพิเศษ</h3>
                    <div class="space-y-3">
                        <div class="flex items-center space-x-3">
                            <span class="text-2xl">🚚</span>
                            <span class="text-white">ส่งฟรีทุกครั้ง</span>
                        </div>
                        <div class="flex items-center space-x-3">
                            <span class="text-2xl">💰</span>
                            <span class="text-white">ส่วนลด 10% สำหรับการเช่าต่อเนื่อง</span>
                        </div>
                        <div class="flex items-center space-x-3">
                            <span class="text-2xl">⚡</span>
                            <span class="text-white">จองล่วงหน้าได้ 30 วัน</span>
                        </div>
                        <div class="flex items-center space-x-3">
                            <span class="text-2xl">🎯</span>
                            <span class="text-white">ได้รับข้อเสนอพิเศษก่อนใคร</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="mt-8 text-center">
                <button class="btn-gradient text-white px-8 py-3 rounded-lg font-medium hover:shadow-lg transition duration-300 mr-4">
                    แก้ไขข้อมูล
                </button>
                <button class="bg-gray-700 hover:bg-gray-600 text-white px-8 py-3 rounded-lg font-medium transition duration-300">
                    ประวัติการเช่า
                </button>
            </div>
        </div>
    </div>

    <!-- Rental Page -->
    <div id="rentalPage" style="display: none;" class="min-h-screen bg-gray-900 py-8">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
            <h1 class="text-3xl font-bold text-center mb-8 text-white">จองการเช่า</h1>
            
            <div class="bg-gray-800 rounded-2xl p-8 border border-gray-700">
                <!-- Selected Product Display -->
                <div id="selectedProduct" class="mb-8">
                    <!-- Product details will be populated here -->
                </div>
                
                <!-- Rental Form -->
                <form id="rentalForm" onsubmit="confirmRental(event)" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">วันที่เริ่มเช่า *</label>
                            <input type="date" id="startDate" required onchange="calculateTotal()" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">วันที่สิ้นสุด *</label>
                            <input type="date" id="endDate" required onchange="calculateTotal()" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white">
                        </div>
                    </div>
                    
                    <!-- Price Calculation -->
                    <div class="bg-gray-700 rounded-xl p-6 border border-gray-600">
                        <h3 class="text-lg font-semibold mb-4 text-white">สรุปราคา</h3>
                        <div class="space-y-2">
                            <div class="flex justify-between">
                                <span class="text-gray-300">ราคาต่อวัน:</span>
                                <span id="dailyPrice" class="text-white font-medium">฿0</span>
                            </div>
                            <div class="flex justify-between">
                                <span class="text-gray-300">จำนวนวัน:</span>
                                <span id="totalDays" class="text-white font-medium">0 วัน</span>
                            </div>
                            <hr class="border-gray-600">
                            <div class="flex justify-between text-lg">
                                <span class="text-white font-semibold">ราคารวม:</span>
                                <span id="totalPrice" class="text-green-400 font-bold">฿0</span>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Customer Information -->
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">ชื่อ *</label>
                            <input type="text" id="firstName" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกชื่อ">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">นามสกุล *</label>
                            <input type="text" id="lastName" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกนามสกุล">
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">เบอร์โทรศัพท์ *</label>
                            <input type="tel" id="phone" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกเบอร์โทรศัพท์">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-300 mb-2">อีเมล *</label>
                            <input type="email" id="email" required class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกอีเมล">
                        </div>
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-300 mb-2">ที่อยู่จัดส่ง *</label>
                        <textarea id="address" required rows="3" class="w-full px-4 py-3 bg-gray-700 border border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-white placeholder-gray-400" placeholder="กรอกที่อยู่สำหรับจัดส่ง"></textarea>
                    </div>
                    
                    <input type="hidden" id="rentalDays" value="0">
                    
                    <div class="flex space-x-4">
                        <button type="button" onclick="showPage('home')" class="flex-1 bg-gray-600 hover:bg-gray-500 text-white py-3 rounded-lg font-medium transition duration-300">
                            ยกเลิก
                        </button>
                        <button type="submit" class="flex-1 btn-gradient text-white py-3 rounded-lg font-medium hover:shadow-lg transition duration-300">
                            ยืนยันการจอง 🚀
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Login Modal -->
    <div id="loginModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 border-2 border-gray-200 shadow-2xl">
            <h2 class="text-2xl font-bold text-center mb-6 text-gray-900">เข้าสู่ระบบ</h2>
            
            <form id="loginForm" onsubmit="handleLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อผู้ใช้</label>
                    <input type="text" id="username" required class="w-full px-4 py-3 bg-white border-2 border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900 placeholder-gray-500" placeholder="กรอกชื่อผู้ใช้">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">รหัสผ่าน</label>
                    <input type="password" id="password" required class="w-full px-4 py-3 bg-white border-2 border-gray-200 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent text-gray-900 placeholder-gray-500" placeholder="กรอกรหัสผ่าน">
                </div>
                
                <div id="loginError" class="hidden bg-red-50 border-2 border-red-200 text-red-700 px-4 py-3 rounded-lg">
                    ชื่อผู้ใช้หรือรหัสผ่านไม่ถูกต้อง
                </div>
                

                
                <div class="flex space-x-4">
                    <button type="button" onclick="closeLoginModal()" class="flex-1 bg-gray-200 hover:bg-gray-300 text-gray-700 py-3 rounded-lg font-medium transition duration-300">
                        ยกเลิก
                    </button>
                    <button type="submit" class="flex-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white py-3 rounded-lg font-medium hover:shadow-lg transition duration-300">
                        เข้าสู่ระบบ
                    </button>
                </div>
            </form>
        </div>
    </div>



    <!-- Cart Modal -->
    <div id="cartModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-gray-800 rounded-2xl p-8 max-w-2xl w-full mx-4 max-h-[80vh] overflow-y-auto border border-gray-700">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-bold text-white">ตะกร้าสินค้า</h2>
                <button onclick="closeCartModal()" class="text-gray-400 hover:text-white text-2xl">×</button>
            </div>
            
            <div id="cartItems" class="space-y-4 mb-6">
                <!-- Cart items will be rendered here -->
            </div>
            
            <div class="border-t border-gray-600 pt-4">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-lg font-semibold text-white">ยอดรวม:</span>
                    <span id="cartTotal" class="text-2xl font-bold text-green-400">฿0</span>
                </div>
                
                <div class="flex space-x-4">
                    <button onclick="clearCart()" class="flex-1 bg-red-600 hover:bg-red-700 text-white py-3 rounded-lg font-medium transition duration-300">
                        ล้างตะกร้า
                    </button>
                    <button onclick="proceedToCheckout()" class="flex-1 btn-gradient text-white py-3 rounded-lg font-medium hover:shadow-lg transition duration-300">
                        ดำเนินการจอง
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-800 text-gray-300 py-12 border-t border-gray-700">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <div class="text-2xl font-bold bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent mb-4">
                        ⚡ FastRent
                    </div>
                    <p class="text-gray-400 mb-4">
                        เช่าอุปกรณ์ IT คุณภาพสูง ราคาประหยัด ส่งถึงที่ทั่วประเทศไทย
                    </p>
                    <div class="flex space-x-4">
                        <a href="https://facebook.com/fastrent" target="_blank" class="text-2xl hover:scale-110 transition duration-300">📘</a>
                        <a href="https://line.me/@fastrent" target="_blank" class="text-2xl hover:scale-110 transition duration-300">💬</a>
                        <a href="https://instagram.com/fastrent" target="_blank" class="text-2xl hover:scale-110 transition duration-300">📷</a>
                    </div>
                </div>
                
                <div>
                    <h4 class="font-semibold mb-4 text-white">หมวดหมู่สินค้า</h4>
                    <ul class="space-y-2">
                        <li><button onclick="showProducts('laptop')" class="hover:text-white transition duration-300">แล็ปท็อป</button></li>
                        <li><button onclick="showProducts('computer')" class="hover:text-white transition duration-300">คอมพิวเตอร์</button></li>
                        <li><button onclick="showProducts('printer')" class="hover:text-white transition duration-300">เครื่องพิมพ์</button></li>
                        <li><button onclick="showProducts('tablet')" class="hover:text-white transition duration-300">แท็บเล็ต</button></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="font-semibold mb-4 text-white">บริการ</h4>
                    <ul class="space-y-2">
                        <li><button onclick="goToHome()" class="hover:text-white transition duration-300">เช่ารายวัน</button></li>
                        <li><button onclick="goToHome()" class="hover:text-white transition duration-300">เช่ารายเดือน</button></li>
                        <li><button onclick="goToHome()" class="hover:text-white transition duration-300">เช่าระยะยาว</button></li>
                        <li><button onclick="goToHome()" class="hover:text-white transition duration-300">บริการติดตั้ง</button></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="font-semibold mb-4 text-white">ติดต่อเรา</h4>
                    <ul class="space-y-2">
                        <li class="flex items-center space-x-2">
                            <span>📞</span>
                            <span>02-123-4567</span>
                        </li>
                        <li class="flex items-center space-x-2">
                            <span>📧</span>
                            <span>info@fastrent.co.th</span>
                        </li>
                        <li class="flex items-center space-x-2">
                            <span>📍</span>
                            <span>กรุงเทพฯ</span>
                        </li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-gray-700 mt-8 pt-8 text-center">
                <p class="text-gray-400">
                    © 2024 FastRent. สงวนลิขสิทธิ์ทุกประการ | 
                    <a href="#" class="hover:text-white transition duration-300">นโยบายความเป็นส่วนตัว</a> | 
                    <a href="#" class="hover:text-white transition duration-300">เงื่อนไขการใช้งาน</a>
                </p>
            </div>
        </div>
    </footer>

    <script>
        // Product data
        const products = [
            // Cameras (New category - first priority)
            { id: 1, name: "Canon EOS R5", category: "กล้อง", price: "2,500", image: "📷", description: "Canon EOS R5 Mirrorless 45MP 8K Video เหมาะสำหรับงานโปรเฟสชั่นนัล" },
            { id: 2, name: "Sony A7 IV", category: "กล้อง", price: "2,200", image: "📷", description: "Sony A7 IV Full Frame 33MP 4K Video ระบบ Auto Focus ที่แม่นยำ" },
            { id: 3, name: "Nikon Z9", category: "กล้อง", price: "3,000", image: "📷", description: "Nikon Z9 Professional 45.7MP 8K Video กล้องระดับโปรสำหรับมืออาชีพ" },
            { id: 4, name: "Fujifilm X-T5", category: "กล้อง", price: "1,800", image: "📷", description: "Fujifilm X-T5 APS-C 40MP Film Simulation โทนสีสวยงาม" },
            { id: 5, name: "Canon EOS R6 Mark II", category: "กล้อง", price: "2,000", image: "📷", description: "Canon EOS R6 Mark II 24MP Dual Pixel CMOS AF II ถ่ายรูปและวิดีโอคุณภาพสูง" },
            { id: 6, name: "Sony FX3", category: "กล้อง", price: "2,800", image: "📷", description: "Sony FX3 Cinema Camera Full Frame 4K 120p สำหรับงานภาพยนตร์" },

            // Laptops
            { id: 7, name: "MacBook Pro 16\"", category: "แล็ปท็อป", price: "1,500", image: "💻", description: "MacBook Pro 16 นิ้ว M2 Pro RAM 16GB SSD 512GB เหมาะสำหรับงานกราฟิก" },
            { id: 8, name: "Dell XPS 13", category: "แล็ปท็อป", price: "800", image: "💻", description: "Dell XPS 13 Intel i7 RAM 16GB SSD 256GB น้ำหนักเบา พกพาสะดวก" },
            { id: 9, name: "HP Pavilion Gaming", category: "แล็ปท็อป", price: "900", image: "💻", description: "HP Pavilion Gaming RTX 3060 RAM 16GB เล่นเกมส์ลื่น ทำงานเร็ว" },
            { id: 10, name: "Lenovo ThinkPad X1", category: "แล็ปท็อป", price: "1,200", image: "💻", description: "Lenovo ThinkPad X1 Carbon Intel i7 RAM 16GB ทนทาน เหมาะสำหรับธุรกิจ" },
            { id: 11, name: "ASUS ROG Laptop", category: "แล็ปท็อป", price: "1,800", image: "💻", description: "ASUS ROG Gaming RTX 4070 RAM 32GB เล่นเกมส์ระดับโปร" },
            { id: 12, name: "MacBook Air M2", category: "แล็ปท็อป", price: "1,000", image: "💻", description: "MacBook Air M2 RAM 8GB SSD 256GB เบา บาง ประหยัดแบตเตอรี่" },

            // Computers
            { id: 13, name: "iMac 24\"", category: "คอมพิวเตอร์", price: "2,000", image: "🖥️", description: "iMac 24 นิ้ว M1 RAM 16GB จอ Retina 4.5K สีสันสดใส" },
            { id: 14, name: "HP All-in-One", category: "คอมพิวเตอร์", price: "1,200", image: "🖥️", description: "HP All-in-One 27 นิ้ว Intel i5 RAM 8GB ประหยัดพื้นที่" },
            { id: 15, name: "Gaming PC RTX 4070", category: "คอมพิวเตอร์", price: "2,500", image: "🖥️", description: "Gaming PC Intel i7 RTX 4070 RAM 32GB เล่นเกมส์ 4K ลื่น" },
            { id: 16, name: "Workstation Dell", category: "คอมพิวเตอร์", price: "3,000", image: "🖥️", description: "Dell Workstation Xeon RTX A4000 RAM 64GB สำหรับงาน 3D Rendering" },

            // Printers
            { id: 17, name: "Canon PIXMA Pro", category: "เครื่องพิมพ์", price: "300", image: "🖨️", description: "Canon PIXMA Pro-100 พิมพ์ภาพคุณภาพสูง A3+ 8 สี" },
            { id: 18, name: "HP LaserJet Pro", category: "เครื่องพิมพ์", price: "250", image: "🖨️", description: "HP LaserJet Pro M404n พิมพ์เร็ว ประหยัดหมึก เหมาะสำนักงาน" },
            { id: 19, name: "Epson EcoTank", category: "เครื่องพิมพ์", price: "200", image: "🖨️", description: "Epson EcoTank L3250 พิมพ์ สแกน ถ่าย หมึกประหยัด" },
            { id: 20, name: "Brother MFC-L3770", category: "เครื่องพิมพ์", price: "400", image: "🖨️", description: "Brother MFC-L3770CDW เลเซอร์สี All-in-One WiFi" },

            // Tablets
            { id: 21, name: "iPad Pro 12.9\"", category: "แท็บเล็ต", price: "1,200", image: "📱", description: "iPad Pro 12.9 นิ้ว M2 256GB รองรับ Apple Pencil 2" },
            { id: 22, name: "Surface Pro 9", category: "แท็บเล็ต", price: "1,500", image: "📱", description: "Microsoft Surface Pro 9 Intel i7 RAM 16GB ใช้เป็นแท็บเล็ตและโน้ตบุ๊ก" },

            // Monitors
            { id: 23, name: "Monitor 4K 32\"", category: "จอมอนิเตอร์", price: "800", image: "🖥️", description: "จอมอนิเตอร์ 4K 32 นิ้ว IPS HDR400 เหมาะสำหรับงานกราฟิก" },
            { id: 24, name: "Ultrawide Monitor", category: "จอมอนิเตอร์", price: "1,200", image: "🖥️", description: "จอ Ultrawide 34 นิ้ว 3440x1440 144Hz เล่นเกมส์และทำงาน" },

            // Projectors
            { id: 25, name: "Projector 4K", category: "โปรเจคเตอร์", price: "2,000", image: "📽️", description: "โปรเจคเตอร์ 4K 3000 lumens เหมาะสำหรับห้องประชุมใหญ่" },
            { id: 26, name: "Portable Projector", category: "โปรเจคเตอร์", price: "500", image: "📽️", description: "โปรเจคเตอร์พกพา Full HD 1000 lumens ขนาดเล็ก น้ำหนักเบา" },

            // Network
            { id: 27, name: "Network Switch 24-port", category: "เครือข่าย", price: "300", image: "🌐", description: "Network Switch 24 port Gigabit managed สำหรับสำนักงาน" },
            { id: 28, name: "Wi-Fi Router Pro", category: "เครือข่าย", price: "200", image: "🌐", description: "Wi-Fi 6 Router AX6000 ความเร็วสูง ครอบคลุมพื้นที่กว้าง" }
        ];

        // Global variables
        let filteredProducts = [...products];
        let currentPage = 'home';
        let isLoggedIn = false;
        let cart = [];
        let selectedProductForRental = null;

        // Notification system
        function showNotification(message, type = 'success') {
            const notification = document.createElement('div');
            const bgColor = type === 'success' ? 'bg-green-600' : type === 'error' ? 'bg-red-600' : 'bg-blue-600';
            
            notification.className = `fixed top-20 right-4 ${bgColor} text-white px-6 py-4 rounded-lg shadow-lg z-50 transform translate-x-full transition-transform duration-300 max-w-sm`;
            notification.innerHTML = `
                <div class="flex items-center space-x-3">
                    <span class="text-2xl">${type === 'success' ? '✅' : type === 'error' ? '❌' : 'ℹ️'}</span>
                    <span>${message}</span>
                </div>
            `;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.classList.remove('translate-x-full');
            }, 100);
            
            setTimeout(() => {
                notification.classList.add('translate-x-full');
                setTimeout(() => {
                    if (document.body.contains(notification)) {
                        document.body.removeChild(notification);
                    }
                }, 300);
            }, 4000);
        }

        // Profile menu toggle
        function toggleProfileMenu() {
            const menu = document.getElementById('profileMenu');
            menu.classList.toggle('hidden');
        }

        // Close profile menu when clicking outside
        document.addEventListener('click', function(event) {
            const profileSection = document.getElementById('profileSection');
            const profileMenu = document.getElementById('profileMenu');
            
            if (profileSection && !profileSection.contains(event.target)) {
                profileMenu.classList.add('hidden');
            }
        });

        // Go to home function
        function goToHome() {
            showPage('home');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Cart functions
        function addToCart(productId, quantity = 1) {
            if (!isLoggedIn) {
                showLoginModal();
                return;
            }

            const product = products.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);

            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({ ...product, quantity: quantity });
            }

            updateCartUI();
            showCartNotification(`เพิ่ม ${product.name} ลงตะกร้าแล้ว!`);
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartUI();
            renderCartItems();
        }

        function updateCartQuantity(productId, quantity) {
            const item = cart.find(item => item.id === productId);
            if (item) {
                item.quantity = Math.max(1, quantity);
                updateCartUI();
                renderCartItems();
            }
        }

        function updateCartUI() {
            const cartBadge = document.getElementById('cartBadge');
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            
            if (totalItems > 0) {
                cartBadge.textContent = totalItems;
                cartBadge.classList.remove('hidden');
            } else {
                cartBadge.classList.add('hidden');
            }
        }

        function showCartModal() {
            document.getElementById('cartModal').classList.remove('hidden');
            renderCartItems();
        }

        function closeCartModal() {
            document.getElementById('cartModal').classList.add('hidden');
        }

        function renderCartItems() {
            const cartItemsContainer = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');

            if (cart.length === 0) {
                cartItemsContainer.innerHTML = `
                    <div class="text-center py-8">
                        <div class="text-6xl mb-4">🛒</div>
                        <p class="text-gray-400 text-lg">ตะกร้าของคุณว่างเปล่า</p>
                        <button onclick="closeCartModal()" class="mt-4 btn-gradient text-white px-6 py-2 rounded-lg">
                            เลือกสินค้า
                        </button>
                    </div>
                `;
                cartTotal.textContent = '฿0';
                return;
            }

            let total = 0;
            cartItemsContainer.innerHTML = cart.map(item => {
                const itemTotal = parseInt(item.price.replace(',', '')) * item.quantity;
                total += itemTotal;
                
                return `
                    <div class="flex items-center space-x-4 p-4 bg-gray-700 rounded-lg border border-gray-600">
                        <div class="text-3xl">${item.image}</div>
                        <div class="flex-1">
                            <h4 class="font-semibold text-white">${item.name}</h4>
                            <p class="text-sm text-gray-400">${item.category}</p>
                            <p class="text-lg font-bold text-green-400">฿${item.price}/วัน</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <button onclick="updateCartQuantity(${item.id}, ${item.quantity - 1})" class="bg-gray-600 text-gray-200 w-8 h-8 rounded-full hover:bg-gray-500">-</button>
                            <span class="w-8 text-center font-semibold text-white">${item.quantity}</span>
                            <button onclick="updateCartQuantity(${item.id}, ${item.quantity + 1})" class="bg-gray-600 text-gray-200 w-8 h-8 rounded-full hover:bg-gray-500">+</button>
                        </div>
                        <div class="text-right">
                            <p class="font-bold text-white">฿${itemTotal.toLocaleString()}</p>
                            <button onclick="removeFromCart(${item.id})" class="text-red-400 hover:text-red-300 text-sm">ลบ</button>
                        </div>
                    </div>
                `;
            }).join('');

            cartTotal.textContent = `฿${total.toLocaleString()}`;
        }

        function clearCart() {
            if (confirm('คุณต้องการล้างตะกร้าสินค้าทั้งหมดหรือไม่?')) {
                cart = [];
                updateCartUI();
                renderCartItems();
            }
        }

        function proceedToCheckout() {
            if (cart.length === 0) {
                alert('กรุณาเลือกสินค้าก่อนดำเนินการจอง');
                return;
            }
            
            // Show advanced rental options modal
            showAdvancedRentalModal();
        }

        function showAdvancedRentalModal() {
            const modal = document.createElement('div');
            modal.id = 'advancedRentalModal';
            modal.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50';
            
            const cartItemsHtml = cart.map((item, index) => `
                <div class="bg-gray-50 rounded-lg p-4 mb-4 border border-gray-200">
                    <div class="flex items-center space-x-4 mb-3">
                        <span class="text-3xl">${item.image}</span>
                        <div class="flex-1">
                            <h4 class="font-semibold text-gray-900">${item.name}</h4>
                            <p class="text-sm text-gray-600">จำนวน: ${item.quantity} ชิ้น × ฿${item.price}/วัน</p>
                        </div>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">วันที่เริ่มเช่า</label>
                            <input type="date" id="startDate-${index}" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" onchange="calculateAdvancedTotal()">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">วันที่สิ้นสุด</label>
                            <input type="date" id="endDate-${index}" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" onchange="calculateAdvancedTotal()">
                        </div>
                    </div>
                    <div class="mt-2 text-right">
                        <span class="text-sm text-gray-600">ราคารวม: </span>
                        <span id="itemTotal-${index}" class="font-bold text-blue-600">฿0</span>
                    </div>
                </div>
            `).join('');

            modal.innerHTML = `
                <div class="bg-white rounded-2xl p-8 max-w-4xl w-full mx-4 max-h-[90vh] overflow-y-auto">
                    <h2 class="text-2xl font-bold text-center mb-6 text-gray-900">กำหนดระยะเวลาการเช่าแต่ละรายการ</h2>
                    
                    <div class="mb-6">
                        ${cartItemsHtml}
                    </div>
                    
                    <div class="bg-blue-50 rounded-lg p-4 mb-6 border border-blue-200">
                        <div class="flex justify-between items-center">
                            <span class="text-lg font-semibold text-gray-900">ยอดรวมทั้งหมด:</span>
                            <span id="grandTotal" class="text-2xl font-bold text-blue-600">฿0</span>
                        </div>
                    </div>
                    
                    <div class="flex space-x-4">
                        <button onclick="closeAdvancedRentalModal()" class="flex-1 bg-gray-200 hover:bg-gray-300 text-gray-700 py-3 rounded-lg font-medium transition duration-300">
                            ยกเลิก
                        </button>
                        <button onclick="proceedWithAdvancedRental()" class="flex-1 bg-gradient-to-r from-blue-600 to-purple-600 text-white py-3 rounded-lg font-medium hover:shadow-lg transition duration-300">
                            ดำเนินการจอง
                        </button>
                    </div>
                </div>
            `;
            
            document.body.appendChild(modal);
            
            // Set default dates (today and tomorrow for all items)
            const today = new Date();
            const tomorrow = new Date(today);
            tomorrow.setDate(tomorrow.getDate() + 1);
            
            cart.forEach((item, index) => {
                document.getElementById(`startDate-${index}`).value = today.toISOString().split('T')[0];
                document.getElementById(`endDate-${index}`).value = tomorrow.toISOString().split('T')[0];
            });
            
            calculateAdvancedTotal();
        }

        function calculateAdvancedTotal() {
            let grandTotal = 0;
            
            cart.forEach((item, index) => {
                const startDate = new Date(document.getElementById(`startDate-${index}`).value);
                const endDate = new Date(document.getElementById(`endDate-${index}`).value);
                
                if (startDate && endDate && endDate > startDate) {
                    const timeDiff = endDate.getTime() - startDate.getTime();
                    const daysDiff = Math.ceil(timeDiff / (1000 * 3600 * 24));
                    const dailyPrice = parseInt(item.price.replace(',', ''));
                    const itemTotal = dailyPrice * item.quantity * daysDiff;
                    
                    document.getElementById(`itemTotal-${index}`).textContent = `฿${itemTotal.toLocaleString()}`;
                    grandTotal += itemTotal;
                } else {
                    document.getElementById(`itemTotal-${index}`).textContent = '฿0';
                }
            });
            
            document.getElementById('grandTotal').textContent = `฿${grandTotal.toLocaleString()}`;
        }

        function closeAdvancedRentalModal() {
            const modal = document.getElementById('advancedRentalModal');
            if (modal) {
                document.body.removeChild(modal);
            }
        }

        function proceedWithAdvancedRental() {
            // Validate all dates
            let isValid = true;
            const rentalDetails = [];
            
            cart.forEach((item, index) => {
                const startDate = document.getElementById(`startDate-${index}`).value;
                const endDate = document.getElementById(`endDate-${index}`).value;
                
                if (!startDate || !endDate || new Date(endDate) <= new Date(startDate)) {
                    isValid = false;
                    return;
                }
                
                const timeDiff = new Date(endDate).getTime() - new Date(startDate).getTime();
                const daysDiff = Math.ceil(timeDiff / (1000 * 3600 * 24));
                const dailyPrice = parseInt(item.price.replace(',', ''));
                const itemTotal = dailyPrice * item.quantity * daysDiff;
                
                rentalDetails.push({
                    ...item,
                    startDate,
                    endDate,
                    days: daysDiff,
                    totalPrice: itemTotal
                });
            });
            
            if (!isValid) {
                alert('กรุณาเลือกวันที่ให้ถูกต้องสำหรับทุกรายการ');
                return;
            }
            
            const grandTotal = rentalDetails.reduce((sum, item) => sum + item.totalPrice, 0);
            
            const confirmationMessage = `
การจองสำเร็จ! 🎉

รายละเอียดการเช่า:
${rentalDetails.map(item => 
    `• ${item.name} (${item.quantity} ชิ้น)\n  วันที่: ${item.startDate} ถึง ${item.endDate} (${item.days} วัน)\n  ราคา: ฿${item.totalPrice.toLocaleString()}`
).join('\n\n')}

ยอดรวมทั้งหมด: ฿${grandTotal.toLocaleString()}

ทีมงานจะติดต่อกลับภายใน 1 ชั่วโมง เพื่อยืนยันการจัดส่ง
ขอบคุณที่ใช้บริการ FastRent! 🚚
            `;
            
            alert(confirmationMessage);
            showNotification('การจองเสร็จสิ้น! ทีมงานจะติดต่อกลับเร็วๆ นี้', 'success');
            
            // Clear cart and close modals
            cart = [];
            updateCartUI();
            closeAdvancedRentalModal();
            closeCartModal();
            goToHome();
        }

        function showCartNotification(message) {
            showNotification(message, 'success');
        }

        // Page navigation
        function showPage(page) {
            // Hide all pages
            document.getElementById('homePage').style.display = 'none';
            document.getElementById('aboutPage').style.display = 'none';
            document.getElementById('contactPage').style.display = 'none';
            document.getElementById('rentalPage').style.display = 'none';
            document.getElementById('profilePage').style.display = 'none';
            
            // Show selected page
            if (page === 'home') {
                document.getElementById('homePage').style.display = 'block';
            } else if (page === 'about') {
                document.getElementById('aboutPage').style.display = 'block';
            } else if (page === 'contact') {
                document.getElementById('contactPage').style.display = 'block';
            } else if (page === 'rental') {
                document.getElementById('rentalPage').style.display = 'block';
            } else if (page === 'profile') {
                if (!isLoggedIn) {
                    showLoginModal();
                    return;
                }
                document.getElementById('profilePage').style.display = 'block';
                // Hide profile menu when showing profile page
                document.getElementById('profileMenu').classList.add('hidden');
                // Scroll to top of profile page
                window.scrollTo({ top: 0, behavior: 'smooth' });
            }
            
            currentPage = page;
        }

        // Scroll to section function
        function scrollToSection(sectionId) {
            const element = document.getElementById(sectionId);
            if (element) {
                element.scrollIntoView({ behavior: 'smooth' });
            }
        }

        // Login functions
        function showLoginModal() {
            document.getElementById('loginModal').classList.remove('hidden');
        }

        function closeLoginModal() {
            document.getElementById('loginModal').classList.add('hidden');
            document.getElementById('loginError').classList.add('hidden');
            document.getElementById('loginForm').reset();
        }

        function handleLogin(event) {
            event.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === 'jaidee' && password === 'mana') {
                isLoggedIn = true;
                updateAuthUI();
                closeLoginModal();
                showNotification('เข้าสู่ระบบสำเร็จ! ยินดีต้อนรับคุณใจดี มานะ', 'success');
            } else {
                document.getElementById('loginError').classList.remove('hidden');
                showNotification('ชื่อผู้ใช้หรือรหัสผ่านไม่ถูกต้อง', 'error');
            }
        }

        function handleLogout() {
            if (confirm('คุณต้องการออกจากระบบหรือไม่?')) {
                isLoggedIn = false;
                cart = []; // Clear cart on logout
                updateAuthUI();
                updateCartUI();
                
                // Hide profile menu
                document.getElementById('profileMenu').classList.add('hidden');
                
                // Reset to initial state - show home page and scroll to top
                showPage('home');
                window.scrollTo({ top: 0, behavior: 'smooth' });
                
                // Reset products display to show all products
                filteredProducts = [...products];
                renderProducts(filteredProducts);
                
                showNotification('ออกจากระบบเรียบร้อยแล้ว กรุณาเข้าสู่ระบบใหม่', 'info');
            }
        }



        function updateAuthUI() {
            const loginBtn = document.getElementById('loginBtn');
            const profileSection = document.getElementById('profileSection');
            
            if (isLoggedIn) {
                loginBtn.classList.add('hidden');
                profileSection.classList.remove('hidden');
            } else {
                loginBtn.classList.remove('hidden');
                profileSection.classList.add('hidden');
            }
        }

        // Contact form handler
        function handleContactForm(event) {
            event.preventDefault();
            showNotification('ส่งข้อความเรียบร้อย! เราจะติดต่อกลับโดยเร็วที่สุด', 'success');
            event.target.reset();
        }

        function renderProducts(productsToRender) {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = '';

            productsToRender.forEach(product => {
                const productCard = `
                    <div class="bg-white rounded-2xl shadow-lg hover:shadow-xl transition-all duration-300 overflow-hidden border-2 border-gray-200 hover:border-gray-900 card-hover transform hover:scale-105">
                        <div class="p-6">
                            <div class="text-6xl mb-4 text-center">${product.image}</div>
                            <h4 class="text-xl font-semibold mb-2 text-gray-900">${product.name}</h4>
                            <p class="text-sm text-gray-900 mb-2 font-medium bg-gray-100 px-3 py-1 rounded-full inline-block border border-gray-300">${product.category}</p>
                            <p class="text-gray-600 mb-4 text-sm leading-relaxed">${product.description}</p>
                            <div class="flex items-center justify-between mb-4">
                                <div class="text-2xl font-bold bg-gradient-to-r from-gray-800 to-gray-900 bg-clip-text text-transparent">฿${product.price}<span class="text-sm text-gray-500">/วัน</span></div>
                            </div>
                            <div class="flex items-center space-x-2 mb-4">
                                <label class="text-sm font-medium text-gray-700">จำนวน:</label>
                                <select id="quantity-${product.id}" class="border-2 border-gray-200 bg-white text-gray-900 rounded-lg px-3 py-1 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                    <option value="1">1</option>
                                    <option value="2">2</option>
                                    <option value="3">3</option>
                                    <option value="4">4</option>
                                    <option value="5">5</option>
                                </select>
                            </div>
                            <div class="flex space-x-2">
                                <button onclick="addToCart(${product.id}, parseInt(document.getElementById('quantity-${product.id}').value))" class="flex-1 bg-gradient-to-r from-green-500 to-green-600 text-white px-4 py-2 rounded-lg font-medium hover:from-green-600 hover:to-green-700 transition duration-300 shadow-md hover:shadow-lg">
                                    🛒 ใส่ตะกร้า
                                </button>
                                <button onclick="rentProduct(${product.id})" class="flex-1 bg-gradient-to-r from-gray-800 to-gray-900 text-white px-4 py-2 rounded-lg font-medium hover:shadow-lg transition duration-300">
                                    🚀 เช่าเลย
                                </button>
                            </div>
                        </div>
                    </div>
                `;
                grid.innerHTML += productCard;
            });
        }

        function rentProduct(productId) {
            if (!isLoggedIn) {
                showLoginModal();
            } else {
                selectedProductForRental = products.find(p => p.id === productId);
                showRentalPage();
            }
        }

        function showRentalPage() {
            if (!selectedProductForRental) return;
            
            // Populate product details
            const productHtml = `
                <div class="flex items-center space-x-4 p-6 bg-gradient-to-r from-gray-700 to-gray-600 rounded-xl border border-gray-600">
                    <div class="text-5xl">${selectedProductForRental.image}</div>
                    <div class="flex-1">
                        <h4 class="text-2xl font-semibold text-white">${selectedProductForRental.name}</h4>
                        <p class="text-gray-300 font-medium bg-gray-600 px-3 py-1 rounded-full inline-block mt-1 border border-gray-500">${selectedProductForRental.category}</p>
                        <p class="text-gray-300 text-sm mt-2">${selectedProductForRental.description}</p>
                        <p class="text-3xl font-bold bg-gradient-to-r from-green-400 to-blue-400 bg-clip-text text-transparent mt-3">฿${selectedProductForRental.price}/วัน</p>
                    </div>
                </div>
            `;
            
            document.getElementById('selectedProduct').innerHTML = productHtml;
            
            // Set default dates (today and tomorrow)
            const today = new Date();
            const tomorrow = new Date(today);
            tomorrow.setDate(tomorrow.getDate() + 1);
            
            document.getElementById('startDate').value = today.toISOString().split('T')[0];
            document.getElementById('endDate').value = tomorrow.toISOString().split('T')[0];
            
            // Calculate initial total
            calculateTotal();
            
            // Show rental page
            showPage('rental');
        }

        function showMultipleRentalPage(cartSummary) {
            // For multiple items, we'll show a simplified booking process
            const totalAmount = cartSummary.reduce((sum, item) => sum + item.totalPrice, 0);
            
            const productListHtml = cartSummary.map(item => `
                <div class="flex items-center space-x-4 p-4 bg-gray-700 rounded-lg mb-2 border border-gray-600">
                    <div class="text-3xl">${item.image}</div>
                    <div class="flex-1">
                        <h5 class="font-semibold text-white">${item.name}</h5>
                        <p class="text-sm text-gray-300">จำนวน: ${item.quantity} ชิ้น × ฿${item.price}/วัน</p>
                    </div>
                    <div class="text-right">
                        <p class="font-bold text-green-400">฿${item.totalPrice.toLocaleString()}/วัน</p>
                    </div>
                </div>
            `).join('');

            document.getElementById('selectedProduct').innerHTML = `
                <div class="bg-gradient-to-r from-gray-700 to-gray-600 rounded-xl border border-gray-600 p-6">
                    <h4 class="text-xl font-semibold text-white mb-4">รายการสินค้าที่เลือก</h4>
                    ${productListHtml}
                    <div class="border-t border-gray-600 pt-4 mt-4">
                        <div class="flex justify-between items-center">
                            <span class="text-lg font-semibold text-white">ยอดรวมต่อวัน:</span>
                            <span class="text-2xl font-bold text-green-400">฿${totalAmount.toLocaleString()}</span>
                        </div>
                    </div>
                </div>
            `;

            // Set default dates
            const today = new Date();
            const tomorrow = new Date(today);
            tomorrow.setDate(tomorrow.getDate() + 1);
            
            document.getElementById('startDate').value = today.toISOString().split('T')[0];
            document.getElementById('endDate').value = tomorrow.toISOString().split('T')[0];
            
            // Store cart summary for calculation
            selectedProductForRental = {
                name: `${cartSummary.length} รายการ`,
                price: totalAmount.toString()
            };
            
            calculateTotal();
            showPage('rental');
        }

        function calculateTotal() {
            const startDate = new Date(document.getElementById('startDate').value);
            const endDate = new Date(document.getElementById('endDate').value);
            
            if (startDate && endDate && endDate > startDate) {
                const timeDiff = endDate.getTime() - startDate.getTime();
                const daysDiff = Math.ceil(timeDiff / (1000 * 3600 * 24));
                
                document.getElementById('rentalDays').value = daysDiff;
                document.getElementById('totalDays').textContent = daysDiff + ' วัน';
                
                if (selectedProductForRental) {
                    const dailyPrice = parseInt(selectedProductForRental.price.replace(',', ''));
                    const totalPrice = dailyPrice * daysDiff;
                    
                    document.getElementById('dailyPrice').textContent = '฿' + selectedProductForRental.price;
                    document.getElementById('totalPrice').textContent = '฿' + totalPrice.toLocaleString();
                }
            } else {
                document.getElementById('rentalDays').value = 0;
                document.getElementById('totalDays').textContent = '0 วัน';
                document.getElementById('totalPrice').textContent = '฿0';
            }
        }

        function confirmRental(event) {
            event.preventDefault();
            const form = document.getElementById('rentalForm');
            const startDate = document.getElementById('startDate').value;
            const endDate = document.getElementById('endDate').value;
            
            if (!form.checkValidity() || !startDate || !endDate) {
                showNotification('กรุณากรอกข้อมูลให้ครบถ้วน', 'error');
                return;
            }
            
            const firstName = document.getElementById('firstName').value;
            const lastName = document.getElementById('lastName').value;
            const phone = document.getElementById('phone').value;
            const email = document.getElementById('email').value;
            const address = document.getElementById('address').value;
            const days = document.getElementById('rentalDays').value;
            const totalPrice = document.getElementById('totalPrice').textContent;
            
            const confirmationMessage = `การจองสำเร็จ! 🎉\n\nรายละเอียดการเช่า:\n• สินค้า: ${selectedProductForRental.name}\n• ผู้เช่า: ${firstName} ${lastName}\n• ระยะเวลา: ${days} วัน (${startDate} ถึง ${endDate})\n• ราคารวม: ${totalPrice}\n• เบอร์ติดต่อ: ${phone}\n• อีเมล: ${email}\n\nทีมงานจะติดต่อกลับภายใน 1 ชั่วโมง เพื่อยืนยันการจัดส่ง\nขอบคุณที่ใช้บริการ FastRent! 🚚`;
            
            alert(confirmationMessage);
            showNotification('การจองเสร็จสิ้น! ทีมงานจะติดต่อกลับเร็วๆ นี้', 'success');
            
            // Clear cart if booking from cart
            if (cart.length > 0) {
                cart = [];
                updateCartUI();
            }
            
            goToHome();
        }

        function searchProducts() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            
            if (searchTerm === '') {
                filteredProducts = [...products];
            } else {
                filteredProducts = products.filter(product => 
                    product.name.toLowerCase().includes(searchTerm) ||
                    product.category.toLowerCase().includes(searchTerm) ||
                    product.description.toLowerCase().includes(searchTerm)
                );
            }
            
            renderProducts(filteredProducts);
        }

        function showProducts(categoryType) {
            let categoryName = '';
            
            switch(categoryType) {
                case 'camera':
                    categoryName = 'กล้อง';
                    break;
                case 'laptop':
                    categoryName = 'แล็ปท็อป';
                    break;
                case 'computer':
                    categoryName = 'คอมพิวเตอร์';
                    break;
                case 'printer':
                    categoryName = 'เครื่องพิมพ์';
                    break;
                case 'tablet':
                    categoryName = 'แท็บเล็ต';
                    break;
                case 'monitor':
                    categoryName = 'จอมอนิเตอร์';
                    break;
                case 'projector':
                    categoryName = 'โปรเจคเตอร์';
                    break;
                case 'network':
                    categoryName = 'เครือข่าย';
                    break;
                default:
                    filteredProducts = [...products];
                    renderProducts(filteredProducts);
                    return;
            }
            
            filteredProducts = products.filter(product => 
                product.category === categoryName
            );
            
            renderProducts(filteredProducts);
            
            // Scroll to products section with proper offset
            const productsSection = document.getElementById('products');
            const navHeight = 80; // Account for fixed navigation
            const elementPosition = productsSection.offsetTop - navHeight;
            
            window.scrollTo({
                top: elementPosition,
                behavior: 'smooth'
            });
        }

        function showAllProducts() {
            filteredProducts = [...products];
            renderProducts(filteredProducts);
            
            // Scroll to products section with proper offset
            const productsSection = document.getElementById('products');
            const navHeight = 80; // Account for fixed navigation
            const elementPosition = productsSection.offsetTop - navHeight;
            
            window.scrollTo({
                top: elementPosition,
                behavior: 'smooth'
            });
        }

        // Search on Enter key
        document.getElementById('searchInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                searchProducts();
            }
        });

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            renderProducts(products);
            updateAuthUI();
            updateCartUI();
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9758b71d738b4b89',t:'MTc1NjI2Nzc4Ni4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
