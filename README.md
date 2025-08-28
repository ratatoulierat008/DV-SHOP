<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GameTech Store - Peralatan Gaming Terlengkap</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            scroll-behavior: smooth;
        }
        
        .hero-section {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        
        .cart-notification {
            transition: all 0.3s ease;
        }
        
        .category-btn.active {
            background-color: #667eea;
            color: white;
        }
        
        .quantity-btn {
            transition: all 0.2s ease;
        }
        
        .quantity-btn:hover {
            transform: scale(1.1);
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Header & Navigation -->
    <header class="bg-white shadow-lg sticky top-0 z-50">
        <nav class="container mx-auto px-6 py-4">
            <div class="flex justify-between items-center">
                <div class="flex items-center">
                    <div class="text-2xl font-bold text-indigo-600 flex items-center">
                        <i class="fas fa-gamepad mr-2"></i>
                        GameTech Store
                    </div>
                </div>
                
                <div class="hidden md:flex space-x-8">
                    <a href="#home" class="text-gray-700 hover:text-indigo-600 font-medium">Beranda</a>
                    <a href="#products" class="text-gray-700 hover:text-indigo-600 font-medium">Produk</a>
                    <a href="#categories" class="text-gray-700 hover:text-indigo-600 font-medium">Kategori</a>
                    <a href="#about" class="text-gray-700 hover:text-indigo-600 font-medium">Tentang</a>
                </div>
                
                <div class="flex items-center space-x-4">
                    <div class="relative">
                        <button id="cartBtn" class="p-2 text-gray-700 hover:text-indigo-600 relative">
                            <i class="fas fa-shopping-cart text-xl"></i>
                            <span id="cartCount" class="absolute -top-1 -right-1 bg-indigo-600 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center">0</span>
                        </button>
                    </div>
                    <button class="bg-indigo-600 text-white px-6 py-2 rounded-lg hover:bg-indigo-700 transition-colors">
                        Login
                    </button>
                    <button class="md:hidden">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>
    </header>

    <!-- Hero Section -->
    <section id="home" class="hero-section text-white py-20">
        <div class="container mx-auto px-6">
            <div class="max-w-4xl mx-auto text-center">
                <h1 class="text-5xl md:text-6xl font-bold mb-6">Tingkatkan Pengalaman Gaming Anda</h1>
                <p class="text-xl mb-8 opacity-90">Temukan peralatan gaming terbaik dengan kualitas premium dan harga terbaik</p>
                <div class="flex justify-center space-x-4">
                    <a href="#products" class="bg-white text-indigo-600 px-8 py-3 rounded-lg font-semibold hover:bg-gray-100 transition-colors">
                        Belanja Sekarang
                    </a>
                    <a href="#categories" class="border-2 border-white text-white px-8 py-3 rounded-lg font-semibold hover:bg-white hover:text-indigo-600 transition-colors">
                        Lihat Kategori
                    </a>
                </div>
            </div>
        </div>
    </section>

    <!-- Categories Section -->
    <section id="categories" class="py-16 bg-white">
        <div class="container mx-auto px-6">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Kategori Produk</h2>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                <button class="category-btn active bg-gray-100 p-6 rounded-lg text-center transition-colors" data-category="all">
                    <i class="fas fa-star text-3xl text-indigo-600 mb-3"></i>
                    <h3 class="font-semibold">Semua Produk</h3>
                </button>
                <button class="category-btn bg-gray-100 p-6 rounded-lg text-center transition-colors" data-category="keyboard">
                    <i class="fas fa-keyboard text-3xl text-indigo-600 mb-3"></i>
                    <h3 class="font-semibold">Keyboard</h3>
                </button>
                <button class="category-btn bg-gray-100 p-6 rounded-lg text-center transition-colors" data-category="mouse">
                    <i class="fas fa-mouse text-3xl text-indigo-600 mb-3"></i>
                    <h3 class="font-semibold">Mouse</h3>
                </button>
                <button class="category-btn bg-gray-100 p-6 rounded-lg text-center transition-colors" data-category="headset">
                    <i class="fas fa-headphones text-3xl text-indigo-600 mb-3"></i>
                    <h3 class="font-semibold">Headset</h3>
                </button>
            </div>
        </div>
    </section>

    <!-- Products Section -->
    <section id="products" class="py-16 bg-gray-50">
        <div class="container mx-auto px-6">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-3xl font-bold text-gray-800">Produk Terbaru</h2>
                <div class="flex space-x-4">
                    <select class="border border-gray-300 rounded-lg px-4 py-2">
                        <option>Urutkan: Terbaru</option>
                        <option>Harga: Rendah ke Tinggi</option>
                        <option>Harga: Tinggi ke Rendah</option>
                    </select>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                <!-- Product 1 -->
                <div class="product-card bg-white rounded-xl shadow-md overflow-hidden transition-all duration-300" data-category="keyboard">
                    <div class="product-image">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/5d91518f-7385-4f32-a896-bf7906d3a517.png" alt="Keyboard gaming mekanis RGB dengan backlight warna-warni dan desain ergonomis" class="w-full h-48 object-cover" onerror="this.style.backgroundColor='#f3f4f6'">
                    </div>
                    <div class="p-6">
                        <h3 class="font-semibold text-lg mb-2">Keyboard Gaming Pro RGB</h3>
                        <p class="text-gray-600 mb-4">Keyboard mekanis dengan switch merah dan RGB lighting</p>
                        <div class="flex items-center justify-between">
                            <span class="text-2xl font-bold text-indigo-600">Rp 899.000</span>
                            <button class="add-to-cart bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition-colors" data-id="1" data-name="Keyboard Gaming Pro RGB" data-price="899000">
                                <i class="fas fa-plus mr-2"></i>Keranjang
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Product 2 -->
                <div class="product-card bg-white rounded-xl shadow-md overflow-hidden transition-all duration-300" data-category="mouse">
                    <div class="product-image">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a5d0cc3d-6ef3-4edf-af63-a7dd5227ac1b.png" alt="Mouse gaming wireless dengan sensor presisi tinggi dan desain ergonomis untuk tangan kanan" class="w-full h-48 object-cover" onerror="this.style.backgroundColor='#f3f4f6'">
                    </div>
                    <div class="p-6">
                        <h3 class="font-semibold text-lg mb-2">Wireless Gaming Mouse</h3>
                        <p class="text-gray-600 mb-4">Mouse wireless dengan 16000 DPI dan 6 tombol programmable</p>
                        <div class="flex items-center justify-between">
                            <span class="text-2xl font-bold text-indigo-600">Rp 599.000</span>
                            <button class="add-to-cart bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition-colors" data-id="2" data-name="Wireless Gaming Mouse" data-price="599000">
                                <i class="fas fa-plus mr-2"></i>Keranjang
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Product 3 -->
                <div class="product-card bg-white rounded-xl shadow-md overflow-hidden transition-all duration-300" data-category="headset">
                    <div class="product-image">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/1cb4e40d-7de9-446e-9d62-f91c5d181e46.png" alt="Headset gaming dengan surround sound 7.1, microphone noise-cancelling, dan lighting RGB" class="w-full h-48 object-cover" onerror="this.style.backgroundColor='#f3f4f6'">
                    </div>
                    <div class="p-6">
                        <h3 class="font-semibold text-lg mb-2">Gaming Headset 7.1</h3>
                        <p class="text-gray-600 mb-4">Headset dengan audio surround dan microphone yang jernih</p>
                        <div class="flex items-center justify-between">
                            <span class="text-2xl font-bold text-indigo-600">Rp 799.000</span>
                            <button class="add-to-cart bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition-colors" data-id="3" data-name="Gaming Headset 7.1" data-price="799000">
                                <i class="fas fa-plus mr-2"></i>Keranjang
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Product 4 -->
                <div class="product-card bg-white rounded-xl shadow-md overflow-hidden transition-all duration-300" data-category="keyboard">
                    <div class="product-image">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/fd90e336-14f5-40fc-8c2e-27085c941781.png" alt="Keyboard gaming compact 60% dengan switch mekanis biru dan keycaps custom" class="w-full h-48 object-cover" onerror="this.style.backgroundColor='#f3f4f6'">
                    </div>
                    <div class="p-6">
                        <h3 class="font-semibold text-lg mb-2">Mini Mechanical Keyboard</h3>
                        <p class="text-gray-600 mb-4">Keyboard compact 60% dengan switch biru untuk respons cepat</p>
                        <div class="flex items-center justify-between">
                            <span class="text-2xl font-bold text-indigo-600">Rp 699.000</span>
                            <button class="add-to-cart bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition-colors" data-id="4" data-name="Mini Mechanical Keyboard" data-price="699000">
                                <i class="fas fa-plus mr-2"></i>Keranjang
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Features Section -->
    <section class="py-16 bg-white">
        <div class="container mx-auto px-6">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Kenapa Memilih Kami?</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="text-center">
                    <div class="bg-indigo-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                        <i class="fas fa-shipping-fast text-indigo-600 text-2xl"></i>
                    </div>
                    <h3 class="font-semibold text-lg mb-2">Gratis Pengiriman</h3>
                    <p class="text-gray-600">Gratis ongkir untuk pembelian di atas Rp 500.000</p>
                </div>
                <div class="text-center">
                    <div class="bg-indigo-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                        <i class="fas fa-shield-alt text-indigo-600 text-2xl"></i>
                    </div>
                    <h3 class="font-semibold text-lg mb-2">Garansi Resmi</h3>
                    <p class="text-gray-600">Semua produk dilengkapi garansi resmi 1-2 tahun</p>
                </div>
                <div class="text-center">
                    <div class="bg-indigo-100 w-16 h-16 rounded-full flex items-center justify-center mx-auto mb-4">
                        <i class="fas fa-headset text-indigo-600 text-2xl"></i>
                    </div>
                    <h3 class="font-semibold text-lg mb-2">Support 24/7</h3>
                    <p class="text-gray-600">Customer service siap membantu 24 jam sehari</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Cart Modal -->
    <div id="cartModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 hidden">
        <div class="fixed right-0 top-0 h-full w-96 bg-white shadow-xl overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold">Keranjang Belanja</h2>
                    <button id="closeCart" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times text-xl"></i>
                    </button>
                </div>
                
                <div id="cartItems" class="space-y-4 mb-6">
                    <!-- Cart items will be added here -->
                </div>
                
                <div class="border-t pt-4">
                    <div class="flex justify-between items-center mb-4">
                        <span class="font-semibold">Total:</span>
                        <span id="cartTotal" class="text-2xl font-bold text-indigo-600">Rp 0</span>
                    </div>
                    <button class="w-full bg-indigo-600 text-white py-3 rounded-lg font-semibold hover:bg-indigo-700 transition-colors">
                        Checkout Sekarang
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Notification -->
    <div id="notification" class="cart-notification fixed top-4 right-4 bg-green-500 text-white px-6 py-3 rounded-lg shadow-lg hidden">
        <div class="flex items-center">
            <i class="fas fa-check-circle mr-2"></i>
            <span>Produk ditambahkan ke keranjang!</span>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-12">
        <div class="container mx-auto px-6">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <h3 class="text-xl font-bold mb-4">GameTech Store</h3>
                    <p class="text-gray-400">Menyediakan peralatan gaming terbaik dengan kualitas premium dan harga terbaik.</p>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Tautan Cepat</h4>
                    <ul class="space-y-2">
                        <li><a href="#home" class="text-gray-400 hover:text-white">Beranda</a></li>
                        <li><a href="#products" class="text-gray-400 hover:text-white">Produk</a></li>
                        <li><a href="#categories" class="text-gray-400 hover:text-white">Kategori</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Layanan</h4>
                    <ul class="space-y-2">
                        <li><a href="#" class="text-gray-400 hover:text-white">Bantuan</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white">Pengiriman</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white">Garansi</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Kontak</h4>
                    <div class="space-y-2 text-gray-400">
                        <p><i class="fas fa-phone mr-2"></i> +62 812-3456-7890</p>
                        <p><i class="fas fa-envelope mr-2"></i> info@gametech.store</p>
                        <p><i class="fas fa-map-marker-alt mr-2"></i> Jakarta, Indonesia</p>
                    </div>
                </div>
            </div>
            <div class="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
                <p>© 2024 GameTech Store. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            let cart = [];
            const cartBtn = document.getElementById('cartBtn');
            const cartModal = document.getElementById('cartModal');
            const closeCart = document.getElementById('closeCart');
            const notification = document.getElementById('notification');
            const cartCount = document.getElementById('cartCount');
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');
            const categoryBtns = document.querySelectorAll('.category-btn');
            const productCards = document.querySelectorAll('.product-card');

            // Cart functionality
            cartBtn.addEventListener('click', () => {
                cartModal.classList.remove('hidden');
                updateCartDisplay();
            });

            closeCart.addEventListener('click', () => {
                cartModal.classList.add('hidden');
            });

            // Add to cart functionality
            document.querySelectorAll('.add-to-cart').forEach(button => {
                button.addEventListener('click', (e) => {
                    const id = e.target.dataset.id;
                    const name = e.target.dataset.name;
                    const price = parseInt(e.target.dataset.price);
                    
                    // Check if product already in cart
                    const existingItem = cart.find(item => item.id === id);
                    
                    if (existingItem) {
                        existingItem.quantity++;
                    } else {
                        cart.push({
                            id,
                            name,
                            price,
                            quantity: 1
                        });
                    }
                    
                    updateCartCount();
                    showNotification();
                    updateCartDisplay();
                });
            });

            // Category filtering
            categoryBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    // Remove active class from all buttons
                    categoryBtns.forEach(b => b.classList.remove('active'));
                    // Add active class to clicked button
                    btn.classList.add('active');
                    
                    const category = btn.dataset.category;
                    
                    productCards.forEach(card => {
                        if (category === 'all' || card.dataset.category === category) {
                            card.style.display = 'block';
                        } else {
                            card.style.display = 'none';
                        }
                    });
                });
            });

            function updateCartCount() {
                const totalItems = cart.reduce((total, item) => total + item.quantity, 0);
                cartCount.textContent = totalItems;
            }

            function showNotification() {
                notification.classList.remove('hidden');
                setTimeout(() => {
                    notification.classList.add('hidden');
                }, 2000);
            }

            function updateCartDisplay() {
                cartItems.innerHTML = '';
                let total = 0;
                
                if (cart.length === 0) {
                    cartItems.innerHTML = '<p class="text-gray-500 text-center py-8">Keranjang belanja masih kosong</p>';
                } else {
                    cart.forEach(item => {
                        const itemTotal = item.price * item.quantity;
                        total += itemTotal;
                        
                        const cartItem = document.createElement('div');
                        cartItem.className = 'flex justify-between items-center p-4 bg-gray-50 rounded-lg';
                        cartItem.innerHTML = `
                            <div>
                                <h4 class="font-semibold">${item.name}</h4>
                                <p class="text-gray-600">Rp ${item.price.toLocaleString()}</p>
                            </div>
                            <div class="flex items-center space-x-2">
                                <button class="quantity-btn text-indigo-600" onclick="decreaseQuantity(${item.id})">-</button>
                                <span class="font-semibold">${item.quantity}</span>
                                <button class="quantity-btn text-indigo-600" onclick="increaseQuantity(${item.id})">+</button>
                            </div>
                        `;
                        cartItems.appendChild(cartItem);
                    });
                }
                
                cartTotal.textContent = `Rp ${total.toLocaleString()}`;
            }

            // Global functions for quantity buttons
            window.increaseQuantity = function(id) {
                const item = cart.find(item => item.id === id.toString());
                if (item) {
                    item.quantity++;
                    updateCartCount();
                    updateCartDisplay();
                }
            };

            window.decreaseQuantity = function(id) {
                const item = cart.find(item => item.id === id.toString());
                if (item && item.quantity > 1) {
                    item.quantity--;
                } else if (item && item.quantity === 1) {
                    cart = cart.filter(cartItem => cartItem.id !== id.toString());
                }
                updateCartCount();
                updateCartDisplay();
            };

            // Close cart when clicking outside
            cartModal.addEventListener('click', (e) => {
                if (e.target === cartModal) {
                    cartModal.classList.add('hidden');
                }
            });
        });
    </script>
</body>
</html>

