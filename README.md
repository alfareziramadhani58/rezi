<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LezatO - Layanan Pesan Antar Makanan</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#f97316', // Orange-500
                        secondary: '#fb923c', // Orange-400
                        dark: '#1f2937', // Gray-800
                        light: '#f3f4f6', // Gray-100
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom scrollbar for a cleaner look */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8; 
        }
        
        /* Smooth scrolling */
        html {
            scroll-behavior: smooth;
        }

        /* Modal animation */
        .modal-enter {
            opacity: 0;
            transform: scale(0.9);
        }
        .modal-enter-active {
            opacity: 1;
            transform: scale(1);
            transition: opacity 300ms, transform 300ms;
        }
        .modal-exit {
            opacity: 1;
            transform: scale(1);
        }
        .modal-exit-active {
            opacity: 0;
            transform: scale(0.9);
            transition: opacity 300ms, transform 300ms;
        }
    </style>
</head>
<body class="bg-light font-sans text-gray-800">

    <!-- Navigation Bar -->
    <nav class="bg-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <a href="#" class="flex items-center gap-2">
                        <!-- Simple SVG Logo -->
                        <svg class="w-8 h-8 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"></path>
                        </svg>
                        <span class="font-bold text-xl tracking-tight text-dark">Lezat<span class="text-primary">O</span></span>
                    </a>
                </div>
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#beranda" class="text-gray-600 hover:text-primary transition duration-300">Beranda</a>
                    <a href="#menu" class="text-gray-600 hover:text-primary transition duration-300">Menu</a>
                    <a href="#tentang" class="text-gray-600 hover:text-primary transition duration-300">Tentang Kami</a>
                    <!-- Cart Button -->
                    <button onclick="toggleCart()" class="relative p-2 text-gray-600 hover:text-primary transition duration-300">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"></path>
                        </svg>
                        <span id="cart-count" class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-white transform translate-x-1/2 -translate-y-1/2 bg-red-600 rounded-full">0</span>
                    </button>
                </div>
                <!-- Mobile menu button -->
                <div class="flex items-center md:hidden gap-4">
                     <button onclick="toggleCart()" class="relative p-2 text-gray-600 hover:text-primary transition duration-300">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"></path>
                        </svg>
                        <span id="mobile-cart-count" class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-white transform translate-x-1/2 -translate-y-1/2 bg-red-600 rounded-full">0</span>
                    </button>
                    <button onclick="toggleMobileMenu()" class="text-gray-600 hover:text-primary focus:outline-none">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <!-- Mobile Menu (Hidden by default) -->
        <div id="mobile-menu" class="hidden md:hidden bg-white border-t">
            <a href="#beranda" class="block px-4 py-3 text-sm text-gray-700 hover:bg-gray-100">Beranda</a>
            <a href="#menu" class="block px-4 py-3 text-sm text-gray-700 hover:bg-gray-100">Menu</a>
            <a href="#tentang" class="block px-4 py-3 text-sm text-gray-700 hover:bg-gray-100">Tentang Kami</a>
        </div>
    </nav>

    <!-- Hero Section -->
    <header id="beranda" class="relative bg-white overflow-hidden">
        <div class="max-w-7xl mx-auto">
            <div class="relative z-10 pb-8 bg-white sm:pb-16 md:pb-20 lg:max-w-2xl lg:w-full lg:pb-28 xl:pb-32 pt-10 sm:pt-16 lg:pt-20">
                <main class="mt-10 mx-auto max-w-7xl px-4 sm:mt-12 sm:px-6 md:mt-16 lg:mt-20 lg:px-8 xl:mt-28">
                    <div class="sm:text-center lg:text-left">
                        <h1 class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl">
                            <span class="block xl:inline">Makanan Lezat,</span>
                            <span class="block text-primary xl:inline">Langsung ke Pintumu</span>
                        </h1>
                        <p class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0">
                            Nikmati berbagai pilihan hidangan lezat dari koki terbaik kami. Pesan sekarang dan rasakan pengalaman kuliner tak terlupakan tanpa harus keluar rumah.
                        </p>
                        <div class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start">
                            <div class="rounded-md shadow">
                                <a href="#menu" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-primary hover:bg-secondary md:py-4 md:text-lg transition duration-300">
                                    Pesan Sekarang
                                </a>
                            </div>
                            <div class="mt-3 sm:mt-0 sm:ml-3">
                                <a href="#tentang" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-primary bg-orange-100 hover:bg-orange-200 md:py-4 md:text-lg transition duration-300">
                                    Pelajari Lebih Lanjut
                                </a>
                            </div>
                        </div>
                    </div>
                </main>
            </div>
        </div>
        <div class="lg:absolute lg:inset-y-0 lg:right-0 lg:w-1/2">
            <!-- Placeholder image for Hero Section -->
            <img class="h-56 w-full object-cover sm:h-72 md:h-96 lg:w-full lg:h-full" src="https://placehold.co/800x600/f97316/ffffff?text=Makanan+Lezat" alt="Makanan Lezat">
        </div>
    </header>

    <!-- Menu Section -->
    <section id="menu" class="py-16 bg-light">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-extrabold text-gray-900 sm:text-4xl">Menu Populer Kami</h2>
                <p class="mt-4 text-lg text-gray-500">Pilihan hidangan favorit pelanggan kami yang wajib Anda coba.</p>
            </div>
            
            <!-- Category Filter (Static for now) -->
            <div class="flex flex-wrap justify-center gap-4 mb-10">
                <button class="px-6 py-2 rounded-full bg-primary text-white font-medium hover:bg-secondary transition shadow-md">Semua</button>
                <button class="px-6 py-2 rounded-full bg-white text-gray-700 font-medium hover:bg-gray-50 transition shadow-sm border">Makanan Utama</button>
                <button class="px-6 py-2 rounded-full bg-white text-gray-700 font-medium hover:bg-gray-50 transition shadow-sm border">Minuman</button>
                <button class="px-6 py-2 rounded-full bg-white text-gray-700 font-medium hover:bg-gray-50 transition shadow-sm border">Penutup</button>
            </div>

            <!-- Menu Grid -->
            <div id="menu-container" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                <!-- Menu items will be injected here by JavaScript -->
            </div>
        </div>
    </section>

    <!-- Features Section -->
    <section id="tentang" class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="lg:text-center">
                <h2 class="text-base text-primary font-semibold tracking-wide uppercase">Tentang Kami</h2>
                <p class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-gray-900 sm:text-4xl">
                    Cara Lebih Baik untuk Menikmati Makanan
                </p>
                <p class="mt-4 max-w-2xl text-xl text-gray-500 lg:mx-auto">
                    Kami berkomitmen memberikan kualitas terbaik dari dapur hingga ke meja makan Anda.
                </p>
            </div>

            <div class="mt-10">
                <div class="space-y-10 md:space-y-0 md:grid md:grid-cols-3 md:gap-x-8 md:gap-y-10">
                    
                    <div class="relative">
                        <div class="absolute flex items-center justify-center h-12 w-12 rounded-md bg-primary text-white">
                            <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg>
                        </div>
                        <p class="ml-16 text-lg leading-6 font-medium text-gray-900">Pengiriman Cepat</p>
                        <dd class="mt-2 ml-16 text-base text-gray-500">
                            Armada kami siap mengantarkan pesanan Anda dalam kondisi masih hangat dan segar dalam waktu singkat.
                        </dd>
                    </div>

                    <div class="relative">
                        <div class="absolute flex items-center justify-center h-12 w-12 rounded-md bg-primary text-white">
                            <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9"></path></svg>
                        </div>
                        <p class="ml-16 text-lg leading-6 font-medium text-gray-900">Bahan Berkualitas</p>
                        <dd class="mt-2 ml-16 text-base text-gray-500">
                            Kami hanya menggunakan bahan-bahan segar pilihan yang dipasok harian dari petani lokal terpercaya.
                        </dd>
                    </div>

                    <div class="relative">
                        <div class="absolute flex items-center justify-center h-12 w-12 rounded-md bg-primary text-white">
                            <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 10h4.764a2 2 0 011.789 2.894l-3.5 7A2 2 0 0115.263 21h-4.017c-.163 0-.326-.02-.485-.06L7 20m7-10V5a2 2 0 00-2-2h-.095c-.5 0-.905.405-.905.905 0 .714-.211 1.412-.608 2.006L7 11v9m7-10h-2M7 20H5a2 2 0 01-2-2v-6a2 2 0 012-2h2.5"></path></svg>
                        </div>
                        <p class="ml-16 text-lg leading-6 font-medium text-gray-900">Kepuasan Pelanggan</p>
                        <dd class="mt-2 ml-16 text-base text-gray-500">
                            Ribuan pelanggan telah membuktikan kelezatan hidangan kami. Kepuasan Anda adalah prioritas utama kami.
                        </dd>
                    </div>

                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-dark text-white pt-12 pb-8">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div>
                    <span class="font-bold text-2xl tracking-tight flex items-center gap-2 mb-4">
                        <svg class="w-6 h-6 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"></path></svg>
                        Lezat<span class="text-primary">O</span>
                    </span>
                    <p class="text-gray-400 text-sm">Menyajikan kebahagiaan dalam setiap gigitan sejak 2026. Kami berdedikasi untuk memberikan pengalaman kuliner terbaik bagi Anda.</p>
                </div>
                <div>
                    <h3 class="text-lg font-semibold mb-4 border-b border-gray-700 pb-2 inline-block">Tautan Cepat</h3>
                    <ul class="space-y-2">
                        <li><a href="#beranda" class="text-gray-400 hover:text-white transition">Beranda</a></li>
                        <li><a href="#menu" class="text-gray-400 hover:text-white transition">Menu</a></li>
                        <li><a href="#tentang" class="text-gray-400 hover:text-white transition">Tentang Kami</a></li>
                    </ul>
                </div>
                <div>
                    <h3 class="text-lg font-semibold mb-4 border-b border-gray-700 pb-2 inline-block">Kontak</h3>
                    <ul class="space-y-2 text-gray-400">
                        <li class="flex items-center gap-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path></svg>
                            halo@lezato.com
                        </li>
                        <li class="flex items-center gap-2">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path></svg>
                            +62 812 3456 7890
                        </li>
                    </ul>
                </div>
            </div>
            <div class="mt-8 pt-8 border-t border-gray-800 text-center text-sm text-gray-500">
                &copy; 2026 LezatO. Hak Cipta Dilindungi.
            </div>
        </div>
    </footer>

    <!-- Shopping Cart Overlay/Modal -->
    <div id="cart-modal" class="fixed inset-0 z-50 hidden bg-black bg-opacity-50 flex justify-end transition-opacity duration-300 opacity-0">
        <div id="cart-drawer" class="w-full max-w-md bg-white h-full flex flex-col shadow-2xl transform translate-x-full transition-transform duration-300">
            <!-- Cart Header -->
            <div class="px-6 py-4 border-b border-gray-200 flex justify-between items-center bg-gray-50">
                <h2 class="text-xl font-bold text-gray-800 flex items-center gap-2">
                    <svg class="w-6 h-6 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"></path></svg>
                    Keranjang Belanja
                </h2>
                <button onclick="toggleCart()" class="text-gray-400 hover:text-gray-600 focus:outline-none transition">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            
            <!-- Cart Items -->
            <div id="cart-items" class="flex-1 overflow-y-auto p-6 space-y-4">
                <!-- Cart items will be rendered here via JS -->
                <div id="empty-cart-msg" class="text-center text-gray-500 mt-10">
                    <svg class="w-16 h-16 mx-auto text-gray-300 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"></path></svg>
                    <p>Keranjang Anda masih kosong.</p>
                    <p class="text-sm mt-2">Yuk, pilih menu lezat kami!</p>
                </div>
            </div>

            <!-- Cart Footer -->
            <div class="border-t border-gray-200 p-6 bg-gray-50">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-gray-600 font-medium">Total Harga</span>
                    <span id="cart-total" class="text-2xl font-bold text-gray-900">Rp 0</span>
                </div>
                <button onclick="checkout()" class="w-full py-3 px-4 bg-primary text-white rounded-lg font-medium text-lg hover:bg-secondary transition duration-300 shadow-md focus:outline-none focus:ring-2 focus:ring-primary focus:ring-opacity-50">
                    Lanjut Pembayaran
                </button>
            </div>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-4 right-4 z-50 transform translate-y-full opacity-0 transition-all duration-300 bg-white border-l-4 border-primary shadow-lg rounded-r-md px-4 py-3 flex items-center gap-3">
        <svg class="w-6 h-6 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>
        <div>
            <p id="toast-title" class="font-semibold text-gray-800">Berhasil</p>
            <p id="toast-message" class="text-sm text-gray-600">Ditambahkan ke keranjang.</p>
        </div>
    </div>

    <!-- Scripts -->
    <script>
        // Data Makanan (Mock Data)
        const menuItems = [
            {
                id: 1,
                name: "Nasi Goreng Spesial",
                description: "Nasi goreng dengan telur, ayam suwir, udang, dan kerupuk.",
                price: 35000,
                image: "https://placehold.co/400x300/1f2937/ffffff?text=Nasi+Goreng",
                category: "Makanan Utama"
            },
            {
                id: 2,
                name: "Ayam Bakar Madu",
                description: "Ayam bakar pilihan dengan olesan madu murni dan sambal terasi.",
                price: 45000,
                image: "https://placehold.co/400x300/1f2937/ffffff?text=Ayam+Bakar",
                category: "Makanan Utama"
            },
            {
                id: 3,
                name: "Sate Ayam Madura",
                description: "10 tusuk sate ayam dengan bumbu kacang kental dan lontong.",
                price: 30000,
                image: "https://placehold.co/400x300/1f2937/ffffff?text=Sate+Ayam",
                category: "Makanan Utama"
            },
            {
                id: 4,
                name: "Es Jeruk Peras",
                description: "Jeruk segar asli yang diperas dengan tambahan es batu.",
                price: 15000,
                image: "https://placehold.co/400x300/f97316/ffffff?text=Es+Jeruk",
                category: "Minuman"
            },
            {
                id: 5,
                name: "Kopi Susu Gula Aren",
                description: "Kopi espresso dengan susu segar dan gula aren asli.",
                price: 22000,
                image: "https://placehold.co/400x300/8b4513/ffffff?text=Kopi+Susu",
                category: "Minuman"
            },
            {
                id: 6,
                name: "Pancake Strawberry",
                description: "Pancake lembut dengan saus strawberry dan es krim vanilla.",
                price: 28000,
                image: "https://placehold.co/400x300/ff69b4/ffffff?text=Pancake",
                category: "Penutup"
            },
            {
                id: 7,
                name: "Mie Goreng Jawa",
                description: "Mie goreng dengan bumbu khas Jawa, telur, dan sayuran.",
                price: 32000,
                image: "https://placehold.co/400x300/1f2937/ffffff?text=Mie+Goreng",
                category: "Makanan Utama"
            },
            {
                id: 8,
                name: "Pudding Coklat",
                description: "Pudding coklat lembut dengan vla vanilla.",
                price: 18000,
                image: "https://placehold.co/400x300/8b4513/ffffff?text=Pudding",
                category: "Penutup"
            }
        ];

        // State
        let cart = [];

        // Format Currency
        const formatRupiah = (number) => {
            return new Intl.NumberFormat('id-ID', {
                style: 'currency',
                currency: 'IDR',
                minimumFractionDigits: 0
            }).format(number);
        };

        // Render Menu
        function renderMenu() {
            const container = document.getElementById('menu-container');
            container.innerHTML = '';

            menuItems.forEach(item => {
                const card = document.createElement('div');
                card.className = 'bg-white rounded-xl shadow-md overflow-hidden hover:shadow-xl transition-shadow duration-300 flex flex-col h-full';
                
                card.innerHTML = `
                    <div class="relative">
                        <img class="w-full h-48 object-cover" src="${item.image}" alt="${item.name}">
                        <div class="absolute top-2 right-2 bg-white px-2 py-1 rounded text-xs font-semibold text-gray-600 shadow">
                            ${item.category}
                        </div>
                    </div>
                    <div class="p-6 flex flex-col flex-1">
                        <div class="flex justify-between items-start mb-2">
                            <h3 class="text-xl font-bold text-gray-900 leading-tight">${item.name}</h3>
                        </div>
                        <p class="text-gray-500 text-sm mb-4 flex-1">${item.description}</p>
                        <div class="flex items-center justify-between mt-auto pt-4 border-t border-gray-100">
                            <span class="text-xl font-bold text-primary">${formatRupiah(item.price)}</span>
                            <button onclick="addToCart(${item.id})" class="p-2 rounded-full bg-orange-100 text-primary hover:bg-primary hover:text-white transition-colors duration-300 focus:outline-none focus:ring-2 focus:ring-primary focus:ring-opacity-50">
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"></path></svg>
                            </button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Cart Logic
        function addToCart(id) {
            const item = menuItems.find(i => i.id === id);
            if (!item) return;

            const existingItem = cart.find(i => i.id === id);
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({ ...item, quantity: 1 });
            }

            updateCartUI();
            showToast(`${item.name} ditambahkan ke keranjang.`);
        }

        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCartUI();
        }

        function updateQuantity(id, change) {
            const item = cart.find(i => i.id === id);
            if (item) {
                item.quantity += change;
                if (item.quantity <= 0) {
                    removeFromCart(id);
                } else {
                    updateCartUI();
                }
            }
        }

        function updateCartUI() {
            // Update counts
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cart-count').innerText = totalItems;
            document.getElementById('mobile-cart-count').innerText = totalItems;

            // Update Total Price
            const totalPrice = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            document.getElementById('cart-total').innerText = formatRupiah(totalPrice);

            // Render Cart Items
            const cartContainer = document.getElementById('cart-items');
            const emptyMsg = document.getElementById('empty-cart-msg');

            // clear existing items except empty message
            Array.from(cartContainer.children).forEach(child => {
                if(child.id !== 'empty-cart-msg') {
                    child.remove();
                }
            });

            if (cart.length === 0) {
                emptyMsg.style.display = 'block';
            } else {
                emptyMsg.style.display = 'none';
                cart.forEach(item => {
                    const el = document.createElement('div');
                    el.className = 'flex items-center gap-4 bg-white p-3 rounded-lg border border-gray-100 shadow-sm';
                    el.innerHTML = `
                        <img src="${item.image}" alt="${item.name}" class="w-16 h-16 object-cover rounded-md">
                        <div class="flex-1">
                            <h4 class="font-semibold text-gray-800 text-sm">${item.name}</h4>
                            <p class="text-primary font-medium text-sm">${formatRupiah(item.price)}</p>
                            <div class="flex items-center gap-2 mt-2">
                                <button onclick="updateQuantity(${item.id}, -1)" class="w-6 h-6 rounded-full bg-gray-200 flex items-center justify-center text-gray-600 hover:bg-gray-300">-</button>
                                <span class="text-sm font-medium w-4 text-center">${item.quantity}</span>
                                <button onclick="updateQuantity(${item.id}, 1)" class="w-6 h-6 rounded-full bg-gray-200 flex items-center justify-center text-gray-600 hover:bg-gray-300">+</button>
                            </div>
                        </div>
                        <button onclick="removeFromCart(${item.id})" class="text-red-500 p-2 hover:bg-red-50 rounded-full transition">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                        </button>
                    `;
                    cartContainer.appendChild(el);
                });
            }
        }

        // UI Toggles
        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        function toggleCart() {
            const modal = document.getElementById('cart-modal');
            const drawer = document.getElementById('cart-drawer');
            
            if (modal.classList.contains('hidden')) {
                // Open
                modal.classList.remove('hidden');
                // trigger reflow
                void modal.offsetWidth;
                modal.classList.remove('opacity-0');
                drawer.classList.remove('translate-x-full');
            } else {
                // Close
                modal.classList.add('opacity-0');
                drawer.classList.add('translate-x-full');
                setTimeout(() => {
                    modal.classList.add('hidden');
                }, 300); // match duration
            }
        }

        // Close cart when clicking outside drawer
        document.getElementById('cart-modal').addEventListener('click', function(e) {
            if (e.target === this) {
                toggleCart();
            }
        });

        // Toast Notification
        let toastTimeout;
        function showToast(message) {
            const toast = document.getElementById('toast');
            const toastMessage = document.getElementById('toast-message');
            
            toastMessage.innerText = message;
            
            toast.classList.remove('translate-y-full', 'opacity-0');
            
            clearTimeout(toastTimeout);
            toastTimeout = setTimeout(() => {
                toast.classList.add('translate-y-full', 'opacity-0');
            }, 3000);
        }

        // Custom Message Box (Replacing alert)
        function showMessage(title, text) {
            // Create modal elements
            const overlay = document.createElement('div');
            overlay.className = 'fixed inset-0 z-[60] bg-black bg-opacity-50 flex items-center justify-center transition-opacity opacity-0';
            
            const dialog = document.createElement('div');
            dialog.className = 'bg-white rounded-lg p-6 max-w-sm w-full mx-4 shadow-xl transform scale-90 transition-transform';
            
            dialog.innerHTML = `
                <h3 class="text-lg font-bold text-gray-900 mb-2">${title}</h3>
                <p class="text-gray-600 mb-6">${text}</p>
                <div class="flex justify-end">
                    <button class="px-4 py-2 bg-primary text-white rounded hover:bg-secondary transition focus:outline-none" id="msg-close">Tutup</button>
                </div>
            `;
            
            overlay.appendChild(dialog);
            document.body.appendChild(overlay);
            
            // Animate in
            requestAnimationFrame(() => {
                overlay.classList.remove('opacity-0');
                dialog.classList.remove('scale-90');
                dialog.classList.add('scale-100');
            });
            
            // Close logic
            const closeBtn = dialog.querySelector('#msg-close');
            const close = () => {
                overlay.classList.add('opacity-0');
                dialog.classList.remove('scale-100');
                dialog.classList.add('scale-90');
                setTimeout(() => {
                    document.body.removeChild(overlay);
                }, 300);
            };
            
            closeBtn.addEventListener('click', close);
            overlay.addEventListener('click', (e) => {
                if(e.target === overlay) close();
            });
        }

        // Checkout Action
        function checkout() {
            if (cart.length === 0) {
                showMessage("Peringatan", "Keranjang belanja Anda masih kosong. Silakan pilih menu terlebih dahulu.");
                return;
            }
            
            toggleCart(); // Close cart
            showMessage("Pesanan Berhasil!", "Terima kasih telah memesan di LezatO. Pesanan Anda sedang diproses dan akan segera dikirim.");
            
            // Clear cart
            cart = [];
            updateCartUI();
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            renderMenu();
        });

    </script>
</body>
</html>
