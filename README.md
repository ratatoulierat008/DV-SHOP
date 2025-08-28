<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StyleShop - Modern Online Shopping</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
        }
        .cart-notification {
            animation: slideIn 0.3s ease-out;
        }
        @keyframes slideIn {
            from { transform: translateY(-100px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        .dropdown-menu {
            display: none;
            animation: fadeIn 0.2s ease-out;
        }
        .dropdown:hover .dropdown-menu {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Header -->
    <header class="bg-white shadow-md sticky top-0 z-50">
        <!-- Top Bar -->
        <div class="bg-gray-900 text-white py-2 px-4">
            <div class="max-w-7xl mx-auto flex justify-between items-center">
                <p class="text-sm">Free shipping on orders over $50!</p>
                <div class="flex space-x-4 text-sm">
                    <a href="#" class="hover:text-gray-300">Track Order</a>
                    <a href="#" class="hover:text-gray-300">Help Center</a>
                    <a href="#" class="hover:text-gray-300">Contact Us</a>
                </div>
            </div>
        </div>

        <!-- Main Navigation -->
        <nav class="max-w-7xl mx-auto px-4 py-4">
            <div class="flex justify-between items-center">
                <!-- Logo -->
                <div class="flex items-center">
                    <h1 class="text-2xl font-bold text-gray-800">STYLESHOP</h1>
                </div>

                <!-- Search Bar -->
                <div class="flex-1 max-w-2xl mx-8">
                    <div class="relative">
                        <input type="text" placeholder="Search for products..." 
                               class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <button class="absolute right-2 top-2 text-gray-400 hover:text-gray-600">
                            <i class="fas fa-search"></i>
                        </button>
                    </div>
                </div>

                <!-- Navigation Icons -->
                <div class="flex items-center space-x-6">
                    <div class="dropdown relative">
                        <button class="text-gray-600 hover:text-gray-900">
                            <i class="fas fa-user text-xl"></i>
                        </button>
                        <div class="dropdown-menu absolute right-0 mt-2 w-48 bg-white rounded-md shadow-lg py-2 z-50">
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" onclick="showAuthModal()">Sign In</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" onclick="showAuthModal()">Create Account</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Wishlist</a>
                        </div>
                    </div>
                    
                    <button class="text-gray-600 hover:text-gray-900 relative" onclick="toggleWishlist()">
                        <i class="fas fa-heart text-xl"></i>
                        <span class="absolute -top-2 -right-2 bg-red-500 text-white rounded-full text-xs w-5 h-5 flex items-center justify-center">3</span>
                    </button>
                    
                    <button class="text-gray-600 hover:text-gray-900 relative" onclick="toggleCart()">
                        <i class="fas fa-shopping-cart text-xl"></i>
                        <span class="absolute -top-2 -right-2 bg-blue-500 text-white rounded-full text-xs w-5 h-5 flex items-center justify-center cart-count">0</span>
                    </button>
                </div>
            </div>

            <!-- Categories -->
            <div class="mt-4 flex justify-center space-x-8">
                <a href="#" class="text-gray-600 hover:text-gray-900 font-medium">New Arrivals</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 font-medium">Clothing</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 font-medium">Shoes</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 font-medium">Accessories</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 font-medium">Electronics</a>
                <a href="#" class="text-gray-600 hover:text-gray-900 font-medium">Home & Living</a>
            </div>
        </nav>
    </header>

    <!-- Hero Section -->
    <section class="relative bg-gradient-to-r from-blue-600 to-purple-600 text-white py-20">
        <div class="max-w-7xl mx-auto px-4">
            <div class="flex flex-col md:flex-row items-center">
                <div class="md:w-1/2 mb-8 md:mb-0">
                    <h2 class="text-4xl md:text-5xl font-bold mb-4">Summer Sale Up to 50% Off</h2>
                    <p class="text-xl mb-6">Discover the latest trends and get amazing deals on fashion, electronics, and more.</p>
                    <div class="flex space-x-4">
                        <button class="bg-white text-blue-600 px-8 py-3 rounded-lg font-semibold hover:bg-gray-100 transition duration-300">
                            Shop Now
                        </button>
                        <button class="border-2 border-white px-8 py-3 rounded-lg font-semibold hover:bg-white hover:text-blue-600 transition duration-300">
                            Learn More
                        </button>
                    </div>
                </div>
                <div class="md:w-1/2">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a6bdc428-42ae-46ac-9ebd-814e3da61ba4.png" alt="Fashionable models showcasing summer collection with vibrant colors and modern clothing styles" class="rounded-lg shadow-2xl">
                </div>
            </div>
        </div>
    </section>

    <!-- Featured Categories -->
    <section class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12">Shop by Category</h2>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                <div class="category-card group">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/3358e132-8340-48b4-a853-c9222d0902e1.png" alt="Modern clothing collection with various outfits including dresses, shirts, and pants" class="w-full h-48 object-cover rounded-lg group-hover:scale-105 transition duration-300">
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Clothing</h3>
                </div>
                <div class="category-card group">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/2c6be9aa-d2d8-4006-a5a9-4eeef79a694a.png" alt="Stylish footwear collection including sneakers, boots, and formal shoes" class="w-full h-48 object-cover rounded-lg group-hover:scale-105 transition duration-300">
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Shoes</h3>
                </div>
                <div class="category-card group">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/5b85d496-8d5b-400a-b649-8db098670f1d.png" alt="Collection of modern accessories including watches, bags, and jewelry" class="w-full h-48 object-cover rounded-lg group-hover:scale-105 transition duration-300">
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Accessories</h3>
                </div>
                <div class="category-card group">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a2b5ddc0-2a22-434c-9def-f00ecbd3b4f8.png" alt="Latest electronic gadgets including smartphones, laptops, and headphones" class="w-full h-48 object-cover rounded-lg group-hover:scale-105 transition duration-300">
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Electronics</h3>
                </div>
            </div>
        </div>
    </section>

    <!-- Featured Products -->
    <section class="py-16 bg-gray-50">
        <div class="max-w-7xl mx-auto px-4">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-3xl font-bold">Featured Products</h2>
                <a href="#" class="text-blue-600 hover:text-blue-800 font-semibold">View All →</a>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="products-grid">
                <!-- Products will be loaded dynamically -->
            </div>
        </div>
    </section>

    <!-- Special Offers -->
    <section class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12">Special Offers</h2>
            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-gradient-to-r from-pink-500 to-red-500 rounded-lg p-8 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <h3 class="text-2xl font-bold mb-4">New Collection</h3>
                        <p class="mb-6">Get 30% off on our newest arrivals. Limited time offer!</p>
                        <button class="bg-white text-pink-600 px-6 py-2 rounded-lg font-semibold hover:bg-gray-100">
                            Shop Now
                        </button>
                    </div>
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/8c39c909-8003-49c8-8303-a50ad2b7ddbb.png" alt="Fashion models wearing latest seasonal collection with vibrant colors and modern designs" class="absolute right-0 top-0 h-full object-cover opacity-50">
                </div>
                <div class="bg-gradient-to-r from-green-500 to-teal-500 rounded-lg p-8 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <h3 class="text-2xl font-bold mb-4">Clearance Sale</h3>
                        <p class="mb-6">Up to 60% off on selected items. Don't miss out!</p>
                        <button class="bg-white text-green-600 px-6 py-2 rounded-lg font-semibold hover:bg-gray-100">
                            Shop Now
                        </button>
                    </div>
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/32541b98-6ffc-46e9-a7b8-9e86aa1f585f.png" alt="Bargain section with discounted products including clothing and accessories" class="absolute right-0 top-0 h-full object-cover opacity-50">
                </div>
            </div>
        </div>
    </section>

    <!-- Newsletter -->
    <section class="py-16 bg-gray-900 text-white">
        <div class="max-w-4xl mx-auto px-4 text-center">
            <h2 class="text-3xl font-bold mb-4">Subscribe to Our Newsletter</h2>
            <p class="mb-8 text-gray-300">Get the latest updates on new products, special offers, and exclusive discounts.</p>
            <div class="flex flex-col sm:flex-row gap-4 max-w-md mx-auto">
                <input type="email" placeholder="Enter your email" class="flex-1 px-4 py-3 rounded-lg text-gray-800 focus:outline-none focus:ring-2 focus:ring-blue-500">
                <button class="bg-blue-600 px-6 py-3 rounded-lg font-semibold hover:bg-blue-700 transition duration-300">
                    Subscribe
                </button>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-12">
        <div class="max-w-7xl mx-auto px-4">
            <div class="grid md:grid-cols-4 gap-8">
                <div>
                    <h3 class="text-xl font-bold mb-4">STYLESHOP</h3>
                    <p class="text-gray-400">Your one-stop destination for all your shopping needs. Quality products at affordable prices.</p>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Quick Links</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><a href="#" class="hover:text-white">About Us</a></li>
                        <li><a href="#" class="hover:text-white">Contact Us</a></li>
                        <li><a href="#" class="hover:text-white">FAQs</a></li>
                        <li><a href="#" class="hover:text-white">Terms & Conditions</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Customer Service</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><a href="#" class="hover:text-white">Track Order</a></li>
                        <li><a href="#" class="hover:text-white">Return Policy</a></li>
                        <li><a href="#" class="hover:text-white">Shipping Info</a></li>
                        <li><a href="#" class="hover:text-white">Privacy Policy</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Connect With Us</h4>
                    <div class="flex space-x-4">
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-facebook text-xl"></i></a>
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-twitter text-xl"></i></a>
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-instagram text-xl"></i></a>
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-pinterest text-xl"></i></a>
                    </div>
                    <div class="mt-4">
                        <p class="text-sm text-gray-400">Payment Methods:</p>
                        <div class="flex space-x-2 mt-2">
                            <i class="fab fa-cc-visa text-2xl"></i>
                            <i class="fab fa-cc-mastercard text-2xl"></i>
                            <i class="fab fa-cc-paypal text-2xl"></i>
                            <i class="fab fa-cc-apple-pay text-2xl"></i>
                        </div>
                    </div>
                </div>
            </div>
            <div class="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
                <p>© 2024 StyleShop. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <!-- Cart Sidebar -->
    <div id="cart-sidebar" class="fixed top-0 right-0 h-full w-96 bg-white shadow-2xl transform translate-x-full transition-transform duration-300 z-50">
        <div class="p-6 h-full flex flex-col">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold">Your Cart</h3>
                <button onclick="toggleCart()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times text-xl"></i>
                </button>
            </div>
            <div class="flex-1 overflow-y-auto" id="cart-items">
                <!-- Cart items will be loaded here -->
                <div class="text-center py-12 text-gray-500">
                    <i class="fas fa-shopping-cart text-4xl mb-4"></i>
                    <p>Your cart is empty</p>
                </div>
            </div>
            <div class="border-t pt-4">
                <div class="flex justify-between mb-4">
                    <span class="font-semibold">Total:</span>
                    <span class="font-bold" id="cart-total">$0.00</span>
                </div>
                <button class="w-full bg-blue-600 text-white py-3 rounded-lg font-semibold hover:bg-blue-700">
                    Proceed to Checkout
                </button>
            </div>
        </div>
    </div>

    <!-- Wishlist Sidebar -->
    <div id="wishlist-sidebar" class="fixed top-0 right-0 h-full w-96 bg-white shadow-2xl transform translate-x-full transition-transform duration-300 z-50">
        <div class="p-6 h-full flex flex-col">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold">Your Wishlist</h3>
                <button onclick="toggleWishlist()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times text-xl"></i>
                </button>
            </div>
            <div class="flex-1 overflow-y-auto" id="wishlist-items">
                <!-- Wishlist items will be loaded here -->
                <div class="text-center py-12 text-gray-500">
                    <i class="fas fa-heart text-4xl mb-4"></i>
                    <p>Your wishlist is empty</p>
                </div>
            </div>
    </div>

    <!-- Auth Modal -->
    <div id="auth-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-8 w-96">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold">Sign In</h3>
                <button onclick="hideAuthModal()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <form>
                <div class="mb-4">
                    <label class="block text-sm font-medium mb-2">Email</label>
                    <input type="email" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div class="mb-6">
                    <label class="block text-sm font-medium mb-2">Password</label>
                    <input type="password" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <button type="submit" class="w-full bg-blue-600 text-white py-2 rounded-lg font-semibold hover:bg-blue-700">
                    Sign In
                </button>
            </form>
            <p class="text-center mt-4 text-sm text-gray-600">
                Don't have an account? <a href="#" class="text-blue-600 hover:underline">Sign up</a>
            </p>
        </div>
    </div>

    <!-- Cart Notification -->
    <div id="cart-notification" class="fixed top-4 right-4 bg-green-500 text-white px-6 py-3 rounded-lg shadow-lg cart-notification hidden z-50">
        <div class="flex items-center">
            <i class="fas fa-check-circle mr-2"></i>
            <span>Item added to cart!</span>
        </div>
    </div>

    <script>
        // Sample product data
        const products = [
            {
                id: 1,
                name: "Premium Cotton T-Shirt",
                price: 29.99,
                oldPrice: 39.99,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/d41ac43b-e739-4215-bfbf-ab44f87e2104.png",
                alt: "Premium quality cotton t-shirt in various colors with modern fit and comfort",
                category: "clothing",
                rating: 4.5,
                reviews: 128
            },
            {
                id: 2,
                name: "Wireless Bluetooth Headphones",
                price: 89.99,
                oldPrice: 129.99,
                image: "https://placehold.co/300x300",
                alt: "Premium wireless Bluetooth headphones with noise cancellation and long battery life",
                category: "electronics",
                rating: 4.8,
                reviews: 256
            },
            {
                id: 3,
                name: "Leather Casual Shoes",
                price: 79.99,
                oldPrice: 99.99,
                image: "https://placehold.co/300x300",
                alt: "Comfortable leather casual shoes for men with modern design and durable construction",
                category: "shoes",
                rating: 4.3,
                reviews: 89
            },
            {
                id: 4,
                name: "Smart Watch Series 5",
                price: 199.99,
                oldPrice: 249.99,
                image: "https://placehold.co/300x300",
                alt: "Advanced smartwatch with health monitoring, GPS, and smartphone connectivity features",
                category: "electronics",
                rating: 4.7,
                reviews: 342
            },
            {
                id: 5,
                name: "Designer Handbag",
                price: 149.99,
                oldPrice: 199.99,
                image: "https://placehold.co/300x300",
                alt: "Elegant designer handbag made from genuine leather with multiple compartments",
                category: "accessories",
                rating: 4.6,
                reviews: 167
            },
            {
                id: 6,
                name: "Running Sport Shoes",
                price: 69.99,
                oldPrice: 89.99,
                image: "https://placehold.co/300x300",
                alt: "High-performance running shoes with cushioning technology and breathable mesh",
                category: "shoes",
                rating: 4.4,
                reviews: 204
            },
            {
                id: 7,
                name: "Slim Fit Jeans",
                price: 49.99,
                oldPrice: 69.99,
                image: "https://placehold.co/300x300",
                alt: "Comfortable slim fit jeans with stretch fabric and modern wash finishes",
                category: "clothing",
                rating: 4.2,
                reviews: 178
            },
            {
                id: 8,
                name: "Premium Sunglasses",
                price: 39.99,
                oldPrice: 59.99,
                image: "https://placehold.co/300x300",
                alt: "Stylish premium sunglasses with UV protection and polarized lenses",
                category: "accessories",
                rating: 4.5,
                reviews: 145
            }
        ];

        let cart = [];
        let wishlist = [];

        // Initialize the page
        document.addEventListener('DOMContentLoaded', function() {
            loadProducts();
            updateCartCount();
        });

        function loadProducts() {
            const productsGrid = document.getElementById('products-grid');
            productsGrid.innerHTML = '';
            
            products.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card bg-white rounded-lg shadow-md p-4 transition duration-300';
                productCard.innerHTML = `
                    <div class="relative mb-4">
                        <img src="${product.image}" alt="${product.alt}" class="w-full h-48 object-cover rounded-lg">
                        <button onclick="toggleWishlistItem(${product.id})" class="absolute top-2 right-2 bg-white p-2 rounded-full shadow-md hover:text-red-500">
                            <i class="fas fa-heart"></i>
                        </button>
                        <div class="absolute top-2 left-2 bg-red-500 text-white px-2 py-1 rounded text-xs">
                            SALE
                        </div>
                    </div>
                    <h3 class="font-semibold mb-2">${product.name}</h3>
                    <div class="flex items-center mb-2">
                        <div class="flex text-yellow-400 mr-2">
                            ${getStarRating(product.rating)}
                        </div>
                        <span class="text-sm text-gray-600">(${product.reviews})</span>
                    </div>
                    <div class="flex items-center justify-between">
                        <div>
                            <span class="text-lg font-bold text-gray-800">$${product.price.toFixed(2)}</span>
                            <span class="text-sm text-gray-500 line-through ml-2">$${product.oldPrice.toFixed(2)}</span>
                        </div>
                        <button onclick="addToCart(${product.id})" class="bg-blue-600 text-white p-2 rounded-lg hover:bg-blue-700">
                            <i class="fas fa-shopping-cart"></i>
                        </button>
                    </div>
                `;
                productsGrid.appendChild(productCard);
            });
        }

        function getStarRating(rating) {
            let stars = '';
            for (let i = 1; i <= 5; i++) {
                if (i <= Math.floor(rating)) {
                    stars += '<i class="fas fa-star"></i>';
                } else if (i === Math.ceil(rating) && rating % 1 > 0) {
                    stars += '<i class="fas fa-star-half-alt"></i>';
                } else {
                    stars += '<i class="far fa-star"></i>';
                }
            }
            return stars;
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }
            
            updateCartCount();
            showCartNotification();
            updateCartDisplay();
        }

        function toggleWishlistItem(productId) {
            const index = wishlist.findIndex(item => item.id === productId);
            if (index === -1) {
                const product = products.find(p => p.id === productId);
                wishlist.push(product);
            } else {
                wishlist.splice(index, 1);
            }
            updateWishlistDisplay();
        }

        function toggleCart() {
            const cartSidebar = document.getElementById('cart-sidebar');
            cartSidebar.classList.toggle('translate-x-full');
            updateCartDisplay();
        }

        function toggleWishlist() {
            const wishlistSidebar = document.getElementById('wishlist-sidebar');
            wishlistSidebar.classList.toggle('translate-x-full');
            updateWishlistDisplay();
        }

        function showAuthModal() {
            document.getElementById('auth-modal').classList.remove('hidden');
        }

        function hideAuthModal() {
            document.getElementById('auth-modal').classList.add('hidden');
        }

        function updateCartCount() {
            const count = cart.reduce((total, item) => total + item.quantity, 0);
            document.querySelectorAll('.cart-count').forEach(el => {
                el.textContent = count;
            });
        }

        function updateCartDisplay() {
            const cartItems = document.getElementById('cart-items');
            const cartTotal = document.getElementById('cart-total');
            
            if (cart.length === 0) {
                cartItems.innerHTML = `
                    <div class="text-center py-12 text-gray-500">
                        <i class="fas fa-shopping-cart text-4xl mb-4"></i>
                        <p>Your cart is empty</p>
                    </div>
                `;
                cartTotal.textContent = '$0.00';
                return;
            }
            
            let total = 0;
            cartItems.innerHTML = '';
            
            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                
                const cartItem = document.createElement('div');
                cartItem.className = 'flex items-center space-x-4 py-4 border-b';
                cartItem.innerHTML = `
                    <img src="${item.image}" alt="${item.alt}" class="w-16 h-16 object-cover rounded">
                    <div class="flex-1">
                        <h4 class="font-semibold">${item.name}</h4>
                        <p class="text-gray-600">$${item.price.toFixed(2)} x ${item.quantity}</p>
                    </div>
                    <div class="flex items-center space-x-2">
                        <button onclick="updateCartQuantity(${item.id}, ${item.quantity - 1})" class="text-gray-400 hover:text-gray-600">
                            <i class="fas fa-minus"></i>
                        </button>
                        <span>${item.quantity}</span>
                        <button onclick="updateCartQuantity(${item.id}, ${item.quantity + 1})" class="text-gray-400 hover:text-gray-600">
                            <i class="fas fa-plus"></i>
                        </button>
                    </div>
                    <button onclick="removeFromCart(${item.id})" class="text-red-500 hover:text-red-700">
                        <i class="fas fa-trash"></i>
                    </button>
                `;
                cartItems.appendChild(cartItem);
            });
            
            cartTotal.textContent = `$${total.toFixed(2)}`;
        }

        function updateWishlistDisplay() {
            const wishlistItems = document.getElementById('wishlist-items');
            
            if (wishlist.length === 0) {
                wishlistItems.innerHTML = `
                    <div class="text-center py-12 text-gray-500">
                        <i class="fas fa-heart text-4xl mb-4"></i>
                        <p>Your wishlist is empty</p>
                    </div>
                `;
                return;
            }
            
            wishlistItems.innerHTML = '';
            
            wishlist.forEach(item => {
                const wishlistItem = document.createElement('div');
                wishlistItem.className = 'flex items-center space-x-4 py-4 border-b';
                wishlistItem.innerHTML = `
                    <img src="${item.image}" alt="${item.alt}" class="w-16 h-16 object-cover rounded">
                    <div class="flex-1">
                        <h4 class="font-semibold">${item.name}</h4>
                        <p class="text-gray-600">$${item.price.toFixed(2)}</p>
                    </div>
                    <button onclick="addToCart(${item.id})" class="bg-blue-600 text-white p-2 rounded hover:bg-blue-700">
                        <i class="fas fa-shopping-cart"></i>
                    </button>
                    <button onclick="toggleWishlistItem(${item.id})" class="text-red-500 hover:text-red-700">
                        <i class="fas fa-trash"></i>
                    </button>
                `;
                wishlistItems.appendChild(wishlistItem);
            });
        }

        function updateCartQuantity(productId, newQuantity) {
            if (newQuantity <= 0) {
                removeFromCart(productId);
                return;
            }
            
            const item = cart.find(item => item.id === productId);
            if (item) {
                item.quantity = newQuantity;
                updateCartDisplay();
                updateCartCount();
            }
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartDisplay();
            updateCartCount();
        }

        function showCartNotification() {
            const notification = document.getElementById('cart-notification');
            notification.classList.remove('hidden');
            setTimeout(() => {
                notification.classList.add('hidden');
            }, 3000);
        }

        // Close modals when clicking outside
        document.addEventListener('click', function(e) {
            const cartSidebar = document.getElementById('cart-sidebar');
            const wishlistSidebar = document.getElementById('wishlist-sidebar');
            const authModal = document.getElementById('auth-modal');
            
            if (!cartSidebar.contains(e.target) && !e.target.closest('[onclick="toggleCart()"]')) {
                cartSidebar.classList.add('translate-x-full');
            }
            
            if (!wishlistSidebar.contains(e.target) && !e.target.closest('[onclick="toggleWishlist()"]')) {
                wishlistSidebar.classList.add('translate-x-full');
            }
            
            if (authModal && !authModal.classList.contains('hidden') && !authModal.contains(e.target) && !e.target.closest('[onclick="showAuthModal()"]')) {
                hideAuthModal();
            }
        });
    </script>
</body>
</html>

