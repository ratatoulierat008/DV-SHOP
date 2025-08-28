<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DVSHOP - Modern Online Shopping</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #3b82f6;
            --secondary: #6366f1;
            --accent: #f59e0b;
            --dark: #1f2937;
            --light: #f9fafb;
        }
        
        .product-card {
            transition: all 0.3s ease;
        }
        
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
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
        
        .loading-spinner {
            border: 3px solid #f3f3f3;
            border-top: 3px solid var(--primary);
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .checkout-step {
            opacity: 0.5;
        }
        
        .checkout-step.active {
            opacity: 1;
            border-color: var(--primary);
        }
        
        .mobile-menu {
            transform: translateX(-100%);
            transition: transform 0.3s ease-out;
        }
        
        .mobile-menu.open {
            transform: translateX(0);
        }
    </style>
</head>
<body class="bg-gray-50 font-sans">
    <!-- Header -->
    <header class="bg-white shadow-md sticky top-0 z-50">
        <!-- Top Bar -->
        <div class="bg-gray-900 text-white py-2 px-4">
            <div class="max-w-7xl mx-auto flex justify-between items-center">
                <p class="text-sm">🚚 Free shipping on orders over $50! Use code: WELCOME10</p>
                <div class="hidden md:flex space-x-4 text-sm">
                    <a href="#track-order" class="hover:text-gray-300">Track Order</a>
                    <a href="#help" class="hover:text-gray-300">Help Center</a>
                    <a href="#contact" class="hover:text-gray-300">Contact Us</a>
                </div>
            </div>
        </div>

        <!-- Main Navigation -->
        <nav class="max-w-7xl mx-auto px-4 py-4">
            <div class="flex justify-between items-center">
                <!-- Logo -->
                <div class="flex items-center">
                    <h1 class="text-2xl font-bold text-gray-800">STYLEHUB</h1>
                </div>

                <!-- Desktop Navigation -->
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#home" class="text-gray-600 hover:text-gray-900 font-medium">Home</a>
                    <a href="#shop" class="text-gray-600 hover:text-gray-900 font-medium">Shop</a>
                    <a href="#categories" class="text-gray-600 hover:text-gray-900 font-medium">Categories</a>
                    <a href="#deals" class="text-gray-600 hover:text-gray-900 font-medium">Deals</a>
                </div>

                <!-- Search Bar -->
                <div class="hidden md:flex flex-1 max-w-2xl mx-8">
                    <div class="relative w-full">
                        <input type="text" placeholder="Search for products, brands, and more..." 
                               class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <button class="absolute right-2 top-2 text-gray-400 hover:text-gray-600">
                            <i class="fas fa-search"></i>
                        </button>
                    </div>
                </div>

                <!-- Navigation Icons -->
                <div class="flex items-center space-x-6">
                    <div class="dropdown relative hidden md:block">
                        <button class="text-gray-600 hover:text-gray-900">
                            <i class="fas fa-user text-xl"></i>
                        </button>
                        <div class="dropdown-menu absolute right-0 mt-2 w-48 bg-white rounded-md shadow-lg py-2 z-50">
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" onclick="showAuthModal()">Sign In</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" onclick="showAuthModal()">Create Account</a>
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">Order History</a>
                        </div>
                    </div>
                    
                    <button class="text-gray-600 hover:text-gray-900 relative" onclick="toggleWishlist()">
                        <i class="fas fa-heart text-xl"></i>
                        <span class="absolute -top-2 -right-2 bg-red-500 text-white rounded-full text-xs w-5 h-5 flex items-center justify-center" id="wishlist-count">0</span>
                    </button>
                    
                    <button class="text-gray-600 hover:text-gray-900 relative" onclick="toggleCart()">
                        <i class="fas fa-shopping-cart text-xl"></i>
                        <span class="absolute -top-2 -right-2 bg-blue-500 text-white rounded-full text-xs w-5 h-5 flex items-center justify-center" id="cart-count">0</span>
                    </button>

                    <!-- Mobile Menu Button -->
                    <button class="md:hidden text-gray-600 hover:text-gray-900" onclick="toggleMobileMenu()">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </nav>

        <!-- Mobile Menu -->
        <div id="mobile-menu" class="mobile-menu fixed top-0 left-0 w-64 h-full bg-white shadow-lg z-50 md:hidden">
            <div class="p-6">
                <div class="flex justify-between items-center mb-8">
                    <h2 class="text-xl font-bold">STYLEHUB</h2>
                    <button onclick="toggleMobileMenu()" class="text-gray-400 hover:text-gray-600">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <div class="space-y-4">
                    <a href="#home" class="block py-2 text-gray-700 hover:text-blue-600">Home</a>
                    <a href="#shop" class="block py-2 text-gray-700 hover:text-blue-600">Shop</a>
                    <a href="#categories" class="block py-2 text-gray-700 hover:text-blue-600">Categories</a>
                    <a href="#deals" class="block py-2 text-gray-700 hover:text-blue-600">Deals</a>
                    <a href="#" class="block py-2 text-gray-700 hover:text-blue-600" onclick="showAuthModal()">Sign In</a>
                </div>
                <div class="mt-8">
                    <div class="relative">
                        <input type="text" placeholder="Search..." 
                               class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <button class="absolute right-2 top-2 text-gray-400 hover:text-gray-600">
                            <i class="fas fa-search"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="relative bg-gradient-to-r from-blue-600 to-purple-600 text-white py-20">
        <div class="max-w-7xl mx-auto px-4">
            <div class="flex flex-col md:flex-row items-center">
                <div class="md:w-1/2 mb-8 md:mb-0">
                    <h2 class="text-4xl md:text-5xl font-bold mb-4">Summer Collection 2024</h2>
                    <p class="text-xl mb-6">Discover the latest trends with up to 50% off on selected items. Limited time offer!</p>
                    <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
                        <button class="bg-white text-blue-600 px-8 py-3 rounded-lg font-semibold hover:bg-gray-100 transition duration-300">
                            Shop Now
                        </button>
                        <button class="border-2 border-white px-8 py-3 rounded-lg font-semibold hover:bg-white hover:text-blue-600 transition duration-300">
                            View Collection
                        </button>
                    </div>
                </div>
                <div class="md:w-1/2">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/d0951acd-9b89-4d5a-8134-3a78acf19b85.png" alt="Modern summer fashion collection featuring vibrant colors and trendy outfits for men and women" class="rounded-lg shadow-2xl w-full">
                </div>
            </div>
        </div>
    </section>

    <!-- Featured Categories -->
    <section class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12">Shop by Category</h2>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                <div class="category-card group cursor-pointer" onclick="filterProducts('clothing')">
                    <div class="relative overflow-hidden rounded-lg">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/121a1290-2a22-4bce-bb67-f4a7318f4e23.png" alt="Modern clothing collection with various outfits including dresses, shirts, and pants" class="w-full h-48 object-cover group-hover:scale-110 transition duration-300">
                        <div class="absolute inset-0 bg-black bg-opacity-40 group-hover:bg-opacity-20 transition duration-300"></div>
                    </div>
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Clothing</h3>
                </div>
                <div class="category-card group cursor-pointer" onclick="filterProducts('shoes')">
                    <div class="relative overflow-hidden rounded-lg">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0db98eb3-4569-4384-bbb6-03dc330dcd94.png" alt="Stylish footwear collection including sneakers, boots, and formal shoes" class="w-full h-48 object-cover group-hover:scale-110 transition duration-300">
                        <div class="absolute inset-0 bg-black bg-opacity-40 group-hover:bg-opacity-20 transition duration-300"></div>
                    </div>
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Shoes</h3>
                </div>
                <div class="category-card group cursor-pointer" onclick="filterProducts('accessories')">
                    <div class="relative overflow-hidden rounded-lg">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/dc42eecd-d9ab-41f8-a1b2-007fdfe12c04.png" alt="Collection of modern accessories including watches, bags, and jewelry" class="w-full h-48 object-cover group-hover:scale-110 transition duration-300">
                        <div class="absolute inset-0 bg-black bg-opacity-40 group-hover:bg-opacity-20 transition duration-300"></div>
                    </div>
                    <h3 class="text-center mt-4 font-semibold group-hover:text-blue-600">Accessories</h3>
                </div>
                <div class="category-card group cursor-pointer" onclick="filterProducts('electronics')">
                    <div class="relative overflow-hidden rounded-lg">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/fe116402-fde4-40df-8709-5d7db29e38f5.png" alt="Latest electronic gadgets including smartphones, laptops, and headphones" class="w-full h-48 object-cover group-hover:scale-110 transition duration-300">
                        <div class="absolute inset-0 bg-black bg-opacity-40 group-hover:bg-opacity-20 transition duration-300"></div>
                    </div>
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
                <div class="flex space-x-4">
                    <select id="sort-select" onchange="sortProducts()" class="px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="featured">Featured</option>
                        <option value="price-low">Price: Low to High</option>
                        <option value="price-high">Price: High to Low</option>
                        <option value="name">Name A-Z</option>
                    </select>
                    <button id="view-all-btn" class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700" onclick="showAllProducts()">
                        View All
                    </button>
                </div>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="products-grid">
                <!-- Products will be loaded dynamically -->
            </div>

            <div class="text-center mt-8">
                <button id="load-more-btn" class="bg-white text-blue-600 border border-blue-600 px-8 py-3 rounded-lg font-semibold hover:bg-blue-600 hover:text-white transition duration-300">
                    Load More Products
                </button>
            </div>
        </div>
    </section>

    <!-- Special Offers -->
    <section class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12">Special Offers & Deals</h2>
            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-gradient-to-r from-pink-500 to-red-500 rounded-lg p-8 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <h3 class="text-2xl font-bold mb-4">New Collection Launch</h3>
                        <p class="mb-6">Get 30% off on our newest arrivals. Limited time offer!</p>
                        <button class="bg-white text-pink-600 px-6 py-2 rounded-lg font-semibold hover:bg-gray-100">
                            Shop Now
                        </button>
                    </div>
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/00ca3246-296d-4770-8f48-cdbf7ee7acb3.png" alt="Fashion models wearing latest seasonal collection with vibrant colors and modern designs" class="absolute right-0 top-0 h-full object-cover opacity-30">
                </div>
                <div class="bg-gradient-to-r from-green-500 to-teal-500 rounded-lg p-8 text-white relative overflow-hidden">
                    <div class="relative z-10">
                        <h3 class="text-2xl font-bold mb-4">Clearance Sale</h3>
                        <p class="mb-6">Up to 60% off on selected items. Don't miss out!</p>
                        <button class="bg-white text-green-600 px-6 py-2 rounded-lg font-semibold hover:bg-gray-100">
                            Shop Now
                        </button>
                    </div>
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/40d19d97-5381-4619-b5d7-6f460d00dcd5.png" alt="Bargain section with discounted products including clothing and accessories" class="absolute right-0 top-0 h-full object-cover opacity-30">
                </div>
            </div>
        </div>
    </section>

    <!-- Testimonials -->
    <section class="py-16 bg-gray-50">
        <div class="max-w-7xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12">What Our Customers Say</h2>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <div class="flex items-center mb-4">
                        <div class="w-12 h-12 bg-gray-300 rounded-full mr-4"></div>
                        <div>
                            <h4 class="font-semibold">Sarah Johnson</h4>
                            <div class="flex text-yellow-400">
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                            </div>
                        </div>
                    </div>
                    <p class="text-gray-600">"The quality of products is amazing! Fast shipping and excellent customer service."</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <div class="flex items-center mb-4">
                        <div class="w-12 h-12 bg-gray-300 rounded-full mr-4"></div>
                        <div>
                            <h4 class="font-semibold">Mike Chen</h4>
                            <div class="flex text-yellow-400">
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star-half-alt"></i>
                            </div>
                        </div>
                    </div>
                    <p class="text-gray-600">"Great prices and frequent sales. I always find what I'm looking for at StyleHub."</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <div class="flex items-center mb-4">
                        <div class="w-12 h-12 bg-gray-300 rounded-full mr-4"></div>
                        <div>
                            <h4 class="font-semibold">Emily Davis</h4>
                            <div class="flex text-yellow-400">
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                                <i class="fas fa-star"></i>
                            </div>
                        </div>
                    </div>
                    <p class="text-gray-600">"The return process was seamless. I appreciate how customer-friendly this store is!"</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Newsletter -->
    <section class="py-16 bg-gray-900 text-white">
        <div class="max-w-4xl mx-auto px-4 text-center">
            <h2 class="text-3xl font-bold mb-4">Stay Updated</h2>
            <p class="mb-8 text-gray-300">Subscribe to our newsletter for exclusive deals, new arrivals, and special offers.</p>
            <div class="flex flex-col sm:flex-row gap-4 max-w-md mx-auto">
                <input type="email" placeholder="Enter your email" class="flex-1 px-4 py-3 rounded-lg text-gray-800 focus:outline-none focus:ring-2 focus:ring-blue-500">
                <button class="bg-blue-600 px-6 py-3 rounded-lg font-semibold hover:bg-blue-700 transition duration-300">
                    Subscribe
                </button>
            </div>
            <p class="text-sm text-gray-400 mt-4">By subscribing, you agree to our Privacy Policy</p>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-12">
        <div class="max-w-7xl mx-auto px-4">
            <div class="grid md:grid-cols-4 gap-8">
                <div>
                    <h3 class="text-xl font-bold mb-4">STYLEHUB</h3>
                    <p class="text-gray-400 mb-4">Your one-stop destination for quality products at affordable prices.</p>
                    <div class="flex space-x-4">
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-facebook text-xl"></i></a>
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-twitter text-xl"></i></a>
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-instagram text-xl"></i></a>
                        <a href="#" class="text-gray-400 hover:text-white"><i class="fab fa-pinterest text-xl"></i></a>
                    </div>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Shop</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><a href="#" class="hover:text-white">New Arrivals</a></li>
                        <li><a href="#" class="hover:text-white">Best Sellers</a></li>
                        <li><a href="#" class="hover:text-white">Sale Items</a></li>
                        <li><a href="#" class="hover:text-white">Gift Cards</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Support</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><a href="#" class="hover:text-white">Contact Us</a></li>
                        <li><a href="#" class="hover:text-white">FAQs</a></li>
                        <li><a href="#" class="hover:text-white">Shipping Info</a></li>
                        <li><a href="#" class="hover:text-white">Returns & Exchanges</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold mb-4">Company</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><a href="#" class="hover:text-white">About Us</a></li>
                        <li><a href="#" class="hover:text-white">Careers</a></li>
                        <li><a href="#" class="hover:text-white">Privacy Policy</a></li>
                        <li><a href="#" class="hover:text-white">Terms of Service</a></li>
                    </ul>
                </div>
            </div>
            <div class="border-t border-gray-700 mt-8 pt-8 flex flex-col md:flex-row justify-between items-center">
                <p class="text-gray-400">© 2024 StyleHub. All rights reserved.</p>
                <div class="flex space-x-4 mt-4 md:mt-0">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/467f4166-8145-4ad4-8751-7002300d6c86.png" alt="Visa payment method" class="h-6">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a9cbf2db-6493-4c83-89f6-457332bca795.png" alt="Mastercard payment method" class="h-6">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ca70c61a-8645-44a6-8c1c-8e507c16a523.png" alt="PayPal payment method" class="h-6">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ef6eed2e-95a5-4f10-96d2-a56f29b2059d.png" alt="Apple Pay payment method" class="h-6">
                </div>
            </div>
        </div>
    </footer>

    <!-- Cart Sidebar -->
    <div id="cart-sidebar" class="fixed top-0 right-0 h-full w-96 bg-white shadow-2xl transform translate-x-full transition-transform duration-300 z-50">
        <div class="p-6 h-full flex flex-col">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold">Shopping Cart</h3>
                <button onclick="toggleCart()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times text-xl"></i>
                </button>
            </div>
            <div class="flex-1 overflow-y-auto" id="cart-items">
                <!-- Cart items will be loaded here -->
            </div>
            <div class="border-t pt-4">
                <div class="space-y-2 mb-4">
                    <div class="flex justify-between">
                        <span>Subtotal:</span>
                        <span id="cart-subtotal">$0.00</span>
                    </div>
                    <div class="flex justify-between">
                        <span>Shipping:</span>
                        <span id="cart-shipping">$0.00</span>
                    </div>
                    <div class="flex justify-between">
                        <span>Tax:</span>
                        <span id="cart-tax">$0.00</span>
                    </div>
                    <div class="flex justify-between font-bold text-lg">
                        <span>Total:</span>
                        <span id="cart-total">$0.00</span>
                    </div>
                </div>
                <button onclick="proceedToCheckout()" class="w-full bg-blue-600 text-white py-3 rounded-lg font-semibold hover:bg-blue-700 mb-2">
                    Proceed to Checkout
                </button>
                <button onclick="continueShopping()" class="w-full border border-gray-300 text-gray-600 py-3 rounded-lg font-semibold hover:bg-gray-50">
                    Continue Shopping
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
            </div>
        </div>
    </div>

    <!-- Auth Modal -->
    <div id="auth-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-8 w-96">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold">Sign In to StyleHub</h3>
                <button onclick="hideAuthModal()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <form id="auth-form">
                <div class="mb-4">
                    <label class="block text-sm font-medium mb-2">Email Address</label>
                    <input type="email" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div class="mb-6">
                    <label class="block text-sm font-medium mb-2">Password</label>
                    <input type="password" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <button type="submit" class="w-full bg-blue-600 text-white py-2 rounded-lg font-semibold hover:bg-blue-700 mb-4">
                    Sign In
                </button>
            </form>
            <div class="text-center">
                <p class="text-sm text-gray-600">
                    Don't have an account? <a href="#" class="text-blue-600 hover:underline">Sign up</a>
                </p>
                <a href="#" class="text-sm text-blue-600 hover:underline mt-2 block">Forgot password?</a>
            </div>
        </div>
    </div>

    <!-- Checkout Modal -->
    <div id="checkout-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg p-8 w-full max-w-4xl mx-4 max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-2xl font-bold">Checkout</h3>
                <button onclick="hideCheckoutModal()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times text-xl"></i>
                </button>
            </div>
            
            <!-- Checkout Steps -->
            <div class="flex justify-between mb-8">
                <div class="checkout-step active border-b-2 border-blue-600 pb-2">
                    <span class="text-blue-600 font-semibold">1. Shipping</span>
                </div>
                <div class="checkout-step border-b-2 border-gray-300 pb-2">
                    <span class="text-gray-500">2. Payment</span>
                </div>
                <div class="checkout-step border-b-2 border-gray-300 pb-2">
                    <span class="text-gray-500">3. Review</span>
                </div>
            </div>

            <!-- Shipping Form -->
            <form id="shipping-form" class="space-y-4">
                <div class="grid md:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium mb-2">First Name</label>
                        <input type="text" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-2">Last Name</label>
                        <input type="text" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                <div>
                    <label class="block text-sm font-medium mb-2">Email Address</label>
                    <input type="email" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <label class="block text-sm font-medium mb-2">Shipping Address</label>
                    <input type="text" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div class="grid md:grid-cols-3 gap-4">
                    <div>
                        <label class="block text-sm font-medium mb-2">City</label>
                        <input type="text" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-2">State</label>
                        <select required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Select State</option>
                            <option value="CA">California</option>
                            <option value="NY">New York</option>
                            <option value="TX">Texas</option>
                            <!-- Add more states -->
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-2">ZIP Code</label>
                        <input type="text" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                <div class="flex items-center">
                    <input type="checkbox" id="save-address" class="mr-2">
                    <label for="save-address" class="text-sm text-gray-600">Save this address for future purchases</label>
                </div>
            </form>

            <div class="flex justify-between mt-8">
                <button onclick="hideCheckoutModal()" class="px-6 py-2 border border-gray-300 rounded-lg text-gray-600 hover:bg-gray-50">
                    Cancel
                </button>
                <button onclick="nextCheckoutStep()" class="px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
                    Continue to Payment
                </button>
            </div>
        </div>
    </div>

    <!-- Cart Notification -->
    <div id="cart-notification" class="fixed top-4 right-4 bg-green-500 text-white px-6 py-3 rounded-lg shadow-lg cart-notification hidden z-50">
        <div class="flex items-center">
            <i class="fas fa-check-circle mr-2"></i>
            <span>Item added to cart!</span>
        </div>
    </div>

    <!-- Loading Overlay -->
    <div id="loading-overlay" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white p-6 rounded-lg shadow-lg">
            <div class="loading-spinner mx-auto mb-4"></div>
            <p class="text-gray-600">Processing...</p>
        </div>
    </div>

    <script>
        // Application State
        const state = {
            products: [],
            cart: JSON.parse(localStorage.getItem('cart')) || [],
            wishlist: JSON.parse(localStorage.getItem('wishlist')) || [],
            currentUser: null,
            currentPage: 1,
            productsPerPage: 8,
            currentFilter: 'all',
            currentSort: 'featured'
        };

        // Sample product data (would typically come from a backend API)
        const sampleProducts = [
            {
                id: 1,
                name: "Premium Cotton T-Shirt",
                price: 29.99,
                oldPrice: 39.99,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/22c80849-2e9d-4979-afe7-ac474c08305b.png",
                alt: "Premium quality cotton t-shirt in various colors with modern fit and comfort",
                category: "clothing",
                rating: 4.5,
                reviews: 128,
                stock: 50,
                colors: ["black", "white", "gray", "navy"],
                sizes: ["S", "M", "L", "XL"]
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
                reviews: 256,
                stock: 25,
                colors: ["black", "white", "silver"]
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
                reviews: 89,
                stock: 30,
                sizes: ["8", "9", "10", "11", "12"]
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
                reviews: 342,
                stock: 15
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
                reviews: 167,
                stock: 20,
                colors: ["brown", "black", "tan"]
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
                reviews: 204,
                stock: 40,
                sizes: ["7", "8", "9", "10", "11"]
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
                reviews: 178,
                stock: 60,
                colors: ["blue", "black", "gray"],
                sizes: ["30", "32", "34", "36"]
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
                reviews: 145,
                stock: 35
            },
            // Additional products...
            {
                id: 9,
                name: "Winter Parka Jacket",
                price: 129.99,
                oldPrice: 179.99,
                image: "https://placehold.co/300x300",
                alt: "Warm winter parka jacket with waterproof exterior and insulated lining",
                category: "clothing",
                rating: 4.6,
                reviews: 92,
                stock: 18
            },
            {
                id: 10,
                name: "Gaming Laptop",
                price: 1299.99,
                oldPrice: 1499.99,
                image: "https://placehold.co/300x300",
                alt: "High-performance gaming laptop with RGB keyboard and powerful graphics",
                category: "electronics",
                rating: 4.7,
                reviews: 156,
                stock: 12
            }
        ];

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
        });

        function initializeApp() {
            // Load products (simulate API call)
            setTimeout(() => {
                state.products = sampleProducts;
                loadProducts();
                updateCartCount();
                updateWishlistCount();
            }, 500);
            
            // Set up event listeners
            document.getElementById('auth-form')?.addEventListener('submit', handleAuthSubmit);
            document.getElementById('load-more-btn')?.addEventListener('click', loadMoreProducts);
        }

        function loadProducts() {
            const productsGrid = document.getElementById('products-grid');
            const filteredProducts = filterAndSortProducts();
            const productsToShow = filteredProducts.slice(0, state.currentPage * state.productsPerPage);
            
            if (productsToShow.length === 0) {
                productsGrid.innerHTML = `
                    <div class="col-span-full text-center py-12">
                        <i class="fas fa-search text-4xl text-gray-400 mb-4"></i>
                        <p class="text-gray-600">No products found matching your criteria.</p>
                    </div>
                `;
                return;
            }
            
            productsGrid.innerHTML = '';
            
            productsToShow.forEach(product => {
                const productCard = createProductCard(product);
                productsGrid.appendChild(productCard);
            });
            
            // Show/hide load more button
            const loadMoreBtn = document.getElementById('load-more-btn');
            if (loadMoreBtn) {
                if (productsToShow.length < filteredProducts.length) {
                    loadMoreBtn.style.display = 'block';
                } else {
                    loadMoreBtn.style.display = 'none';
                }
            }
        }

        function createProductCard(product) {
            const card = document.createElement('div');
            card.className = 'product-card bg-white rounded-lg shadow-md p-4 transition duration-300';
            card.innerHTML = `
                <div class="relative mb-4">
                    <img src="${product.image}" alt="${product.alt}" class="w-full h-48 object-cover rounded-lg">
                    <button onclick="toggleWishlistItem(${product.id})" class="absolute top-2 right-2 bg-white p-2 rounded-full shadow-md hover:text-red-500 transition duration-200">
                        <i class="fas fa-heart ${state.wishlist.some(item => item.id === product.id) ? 'text-red-500' : 'text-gray-400'}"></i>
                    </button>
                    ${product.oldPrice ? `
                    <div class="absolute top-2 left-2 bg-red-500 text-white px-2 py-1 rounded text-xs">
                        SALE
                    </div>
                    ` : ''}
                </div>
                <h3 class="font-semibold mb-2 text-gray-800">${product.name}</h3>
                <div class="flex items-center mb-2">
                    <div class="flex text-yellow-400 mr-2">
                        ${getStarRating(product.rating)}
                    </div>
                    <span class="text-sm text-gray-600">(${product.reviews})</span>
                </div>
                <div class="flex items-center justify-between mb-2">
                    <div>
                        <span class="text-lg font-bold text-gray-800">$${product.price.toFixed(2)}</span>
                        ${product.oldPrice ? `
                        <span class="text-sm text-gray-500 line-through ml-2">$${product.oldPrice.toFixed(2)}</span>
                        ` : ''}
                    </div>
                    <span class="text-sm ${product.stock > 10 ? 'text-green-600' : product.stock > 0 ? 'text-yellow-600' : 'text-red-600'}">
                        ${product.stock > 10 ? 'In Stock' : product.stock > 0 ? 'Low Stock' : 'Out of Stock'}
                    </span>
                </div>
                <button onclick="addToCart(${product.id})" 
                        class="w-full bg-blue-600 text-white py-2 rounded-lg font-semibold hover:bg-blue-700 transition duration-200 disabled:bg-gray-400 disabled:cursor-not-allowed"
                        ${product.stock === 0 ? 'disabled' : ''}>
                    ${product.stock === 0 ? 'Out of Stock' : 'Add to Cart'}
                </button>
            `;
            return card;
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

        function filterAndSortProducts() {
            let filtered = state.products;
            
            // Apply filter
            if (state.currentFilter !== 'all') {
                filtered = filtered.filter(product => product.category === state.currentFilter);
            }
            
            // Apply sort
            switch (state.currentSort) {
                case 'price-low':
                    filtered.sort((a, b) => a.price - b.price);
                    break;
                case 'price-high':
                    filtered.sort((a, b) => b.price - a.price);
                    break;
                case 'name':
                    filtered.sort((a, b) => a.name.localeCompare(b.name));
                    break;
                case 'featured':
                default:
                    // Keep original order for featured
                    break;
            }
            
            return filtered;
        }

        function filterProducts(category) {
            state.currentFilter = category;
            state.currentPage = 1;
            loadProducts();
        }

        function sortProducts() {
            const sortSelect = document.getElementById('sort-select');
            state.currentSort = sortSelect.value;
            loadProducts();
        }

        function showAllProducts() {
            state.currentFilter = 'all';
            state.currentPage = 1;
            loadProducts();
        }

        function loadMoreProducts() {
            state.currentPage++;
            loadProducts();
        }

        function addToCart(productId) {
            showLoading();
            
            setTimeout(() => {
                const product = state.products.find(p => p.id === productId);
                if (!product) return;
                
                const existingItem = state.cart.find(item => item.id === productId);
                
                if (existingItem) {
                    if (existingItem.quantity < product.stock) {
                        existingItem.quantity += 1;
                    } else {
                        hideLoading();
                        showNotification('Maximum stock reached for this item', 'error');
                        return;
                    }
                } else {
                    state.cart.push({ ...product, quantity: 1 });
                }
                
                // Save to localStorage
                localStorage.setItem('cart', JSON.stringify(state.cart));
                
                updateCartCount();
                updateCartDisplay();
                showNotification('Item added to cart!', 'success');
                hideLoading();
            }, 500);
        }

        function toggleWishlistItem(productId) {
            const product = state.products.find(p => p.id === productId);
            if (!product) return;
            
            const index = state.wishlist.findIndex(item => item.id === productId);
            
            if (index === -1) {
                state.wishlist.push(product);
                showNotification('Added to wishlist!', 'success');
            } else {
                state.wishlist.splice(index, 1);
                showNotification('Removed from wishlist', 'info');
            }
            
            // Save to localStorage
            localStorage.setItem('wishlist', JSON.stringify(state.wishlist));
            
            updateWishlistCount();
            updateWishlistDisplay();
            loadProducts(); // Refresh to update heart icons
        }

        function updateCartCount() {
            const count = state.cart.reduce((total, item) => total + item.quantity, 0);
            document.getElementById('cart-count').textContent = count;
        }

        function updateWishlistCount() {
            document.getElementById('wishlist-count').textContent = state.wishlist.length;
        }

        function updateCartDisplay() {
            const cartItems = document.getElementById('cart-items');
            const cartSubtotal = document.getElementById('cart-subtotal');
            const cartShipping = document.getElementById('cart-shipping');
            const cartTax = document.getElementById('cart-tax');
            const cartTotal = document.getElementById('cart-total');
            
            if (state.cart.length === 0) {
                cartItems.innerHTML = `
                    <div class="text-center py-12 text-gray-500">
                        <i class="fas fa-shopping-cart text-4xl mb-4"></i>
                        <p>Your cart is empty</p>
                        <button onclick="continueShopping()" class="text-blue-600 hover:underline mt-2">
                            Start Shopping
                        </button>
                    </div>
                `;
                cartSubtotal.textContent = '$0.00';
                cartShipping.textContent = '$0.00';
                cartTax.textContent = '$0.00';
                cartTotal.textContent = '$0.00';
                return;
            }
            
            let subtotal = 0;
            cartItems.innerHTML = '';
            
            state.cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                subtotal += itemTotal;
                
                const cartItem = document.createElement('div');
                cartItem.className = 'flex items-center space-x-4 py-4 border-b';
                cartItem.innerHTML = `
                    <img src="${item.image}" alt="${item.alt}" class="w-16 h-16 object-cover rounded">
                    <div class="flex-1">
                        <h4 class="font-semibold text-sm">${item.name}</h4>
                        <p class="text-gray-600 text-sm">$${item.price.toFixed(2)}</p>
                    </div>
                    <div class="flex items-center space-x-2">
                        <button onclick="updateCartQuantity(${item.id}, ${item.quantity - 1})" class="text-gray-400 hover:text-gray-600 p-1">
                            <i class="fas fa-minus text-xs"></i>
                        </button>
                        <span class="text-sm w-6 text-center">${item.quantity}</span>
                        <button onclick="updateCartQuantity(${item.id}, ${item.quantity + 1})" class="text-gray-400 hover:text-gray-600 p-1"
                                ${item.quantity >= (state.products.find(p => p.id === item.id)?.stock || 0) ? 'disabled' : ''}>
                            <i class="fas fa-plus text-xs"></i>
                        </button>
                    </div>
                    <p class="font-semibold text-sm">$${itemTotal.toFixed(2)}</p>
                    <button onclick="removeFromCart(${item.id})" class="text-red-500 hover:text-red-700 p-1">
                        <i class="fas fa-trash text-sm"></i>
                    </button>
                `;
                cartItems.appendChild(cartItem);
            });
            
            const shipping = subtotal > 50 ? 0 : 5.99;
            const tax = subtotal * 0.08;
            const total = subtotal + shipping + tax;
            
            cartSubtotal.textContent = `$${subtotal.toFixed(2)}`;
            cartShipping.textContent = shipping === 0 ? 'FREE' : `$${shipping.toFixed(2)}`;
            cartTax.textContent = `$${tax.toFixed(2)}`;
            cartTotal.textContent = `$${total.toFixed(2)}`;
        }

        function updateWishlistDisplay() {
            const wishlistItems = document.getElementById('wishlist-items');
            
            if (state.wishlist.length === 0) {
                wishlistItems.innerHTML = `
                    <div class="text-center py-12 text-gray-500">
                        <i class="fas fa-heart text-4xl mb-4"></i>
                        <p>Your wishlist is empty</p>
                        <button onclick="continueShopping()" class="text-blue-600 hover:underline mt-2">
                            Browse Products
                        </button>
                    </div>
                `;
                return;
            }
            
            wishlistItems.innerHTML = '';
            
            state.wishlist.forEach(item => {
                const wishlistItem = document.createElement('div');
                wishlistItem.className = 'flex items-center space-x-4 py-4 border-b';
                wishlistItem.innerHTML = `
                    <img src="${item.image}" alt="${item.alt}" class="w-16 h-16 object-cover rounded">
                    <div class="flex-1">
                        <h4 class="font-semibold text-sm">${item.name}</h4>
                        <p class="text-gray-600 text-sm">$${item.price.toFixed(2)}</p>
                    </div>
                    <button onclick="addToCart(${item.id})" class="bg-blue-600 text-white p-2 rounded hover:bg-blue-700"
                            ${item.stock === 0 ? 'disabled' : ''}>
                        <i class="fas fa-shopping-cart text-sm"></i>
                    </button>
                    <button onclick="toggleWishlistItem(${item.id})" class="text-red-500 hover:text-red-700 p-2">
                        <i class="fas fa-trash text-sm"></i>
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
            
            const product = state.products.find(p => p.id === productId);
            const item = state.cart.find(item => item.id === productId);
            
            if (item && product && newQuantity <= product.stock) {
                item.quantity = newQuantity;
                localStorage.setItem('cart', JSON.stringify(state.cart));
                updateCartDisplay();
                updateCartCount();
            }
        }

        function removeFromCart(productId) {
            state.cart = state.cart.filter(item => item.id !== productId);
            localStorage.setItem('cart', JSON.stringify(state.cart));
            updateCartDisplay();
            updateCartCount();
            showNotification('Item removed from cart', 'info');
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

        function toggleMobileMenu() {
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenu.classList.toggle('open');
        }

        function showAuthModal() {
            document.getElementById('auth-modal').classList.remove('hidden');
        }

        function hideAuthModal() {
            document.getElementById('auth-modal').classList.add('hidden');
        }

        function showCheckoutModal() {
            document.getElementById('checkout-modal').classList.remove('hidden');
        }

        function hideCheckoutModal() {
            document.getElementById('checkout-modal').classList.add('hidden');
        }

        function showLoading() {
            document.getElementById('loading-overlay').classList.remove('hidden');
        }

        function hideLoading() {
            document.getElementById('loading-overlay').classList.add('hidden');
        }

        function showNotification(message, type = 'success') {
            const notification = document.getElementById('cart-notification');
            notification.innerHTML = `
                <div class="flex items-center">
                    <i class="fas fa-${type === 'success' ? 'check' : 'exclamation'}-circle mr-2"></i>
                    <span>${message}</span>
                </div>
            `;
            notification.className = `fixed top-4 right-4 px-6 py-3 rounded-lg shadow-lg cart-notification z-50 ${
                type === 'success' ? 'bg-green-500 text-white' : 
                type === 'error' ? 'bg-red-500 text-white' : 'bg-blue-500 text-white'
            }`;
            notification.classList.remove('hidden');
            
            setTimeout(() => {
                notification.classList.add('hidden');
            }, 3000);
        }

        function handleAuthSubmit(e) {
            e.preventDefault();
            showLoading();
            
            // Simulate authentication
            setTimeout(() => {
                hideLoading();
                hideAuthModal();
                showNotification('Welcome back!', 'success');
                // Here you would typically set user state and update UI
            }, 1500);
        }

        function proceedToCheckout() {
            if (state.cart.length === 0) {
                showNotification('Your cart is empty', 'error');
                return;
            }
            
            toggleCart();
            showCheckoutModal();
        }

        function continueShopping() {
            toggleCart();
            toggleWishlist();
        }

        function nextCheckoutStep() {
            // Validate shipping form
            const form = document.getElementById('shipping-form');
            if (!form.checkValidity()) {
                form.reportValidity();
                return;
            }
            
            // Move to next step (payment)
            const steps = document.querySelectorAll('.checkout-step');
            steps[0].classList.remove('active');
            steps[1].classList.add('active');
            
            // Here you would typically show the payment form
            // For this demo, we'll simulate order completion
            setTimeout(() => {
                hideCheckoutModal();
                // Clear cart
                state.cart = [];
                localStorage.setItem('cart', JSON.stringify(state.cart));
                updateCartCount();
                showNotification('Order placed successfully!', 'success');
            }, 2000);
        }

        // Close modals when clicking outside
        document.addEventListener('click', function(e) {
            const cartSidebar = document.getElementById('cart-sidebar');
            const wishlistSidebar = document.getElementById('wishlist-sidebar');
            const authModal = document.getElementById('auth-modal');
            const checkoutModal = document.getElementById('checkout-modal');
            const mobileMenu = document.getElementById('mobile-menu');
            
            if (!cartSidebar.contains(e.target) && !e.target.closest('[onclick*="toggleCart"]')) {
                cartSidebar.classList.add('translate-x-full');
            }
            
            if (!wishlistSidebar.contains(e.target) && !e.target.closest('[onclick*="toggleWishlist"]')) {
                wishlistSidebar.classList.add('translate-x-full');
            }
            
            if (authModal && !authModal.classList.contains('hidden') && !authModal.contains(e.target) && !e.target.closest('[onclick*="showAuthModal"]')) {
                hideAuthModal();
            }
            
            if (checkoutModal && !checkoutModal.classList.contains('hidden') && !checkoutModal.contains(e.target) && !e.target.closest('[onclick*="showCheckoutModal"]')) {
                hideCheckoutModal();
            }
            
            if (mobileMenu && !mobileMenu.contains(e.target) && !e.target.closest('[onclick*="toggleMobileMenu"]')) {
                mobileMenu.classList.remove('open');
            }
        });

        // API simulation functions (would connect to real backend)
        async function simulateApiCall(endpoint, data) {
            showLoading();
            try {
                // Simulate network delay
                await new Promise(resolve => setTimeout(resolve, 1000));
                
                // Simulate different responses based on endpoint
                switch (endpoint) {
                    case '/api/products':
                        return { success: true, data: sampleProducts };
                    case '/api/cart':
                        return { success: true, data: state.cart };
                    case '/api/checkout':
                        return { success: true, orderId: 'ORD-' + Date.now() };
                    default:
                        return { success: true, data };
                }
            } catch (error) {
                return { success: false, error: 'Network error' };
            } finally {
                hideLoading();
            }
        }

        // Export functions for global access
        window.addToCart = addToCart;
        window.toggleWishlistItem = toggleWishlistItem;
        window.toggleCart = toggleCart;
        window.toggleWishlist = toggleWishlist;
        window.toggleMobileMenu = toggleMobileMenu;
        window.showAuthModal = showAuthModal;
        window.hideAuthModal = hideAuthModal;
        window.updateCartQuantity = updateCartQuantity;
        window.removeFromCart = removeFromCart;
        window.filterProducts = filterProducts;
        window.sortProducts = sortProducts;
        window.showAllProducts = showAllProducts;
        window.proceedToCheckout = proceedToCheckout;
        window.continueShopping = continueShopping;
        window.nextCheckoutStep = nextCheckoutStep;
        window.hideCheckoutModal = hideCheckoutModal;
    </script>
</body>
</html>

