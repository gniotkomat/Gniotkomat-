<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gniotkomat - Sklep z Najsłodszymi Gniotkami!</title>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600&family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #ff9ebb;
            --primary-light: #ffd1dc;
            --secondary: #b19cd9;
            --accent: #a0e7e5;
            --bg: #fdf6f9;
            --card-bg: #ffffff;
            --text: #4a404d;
            --shadow: 0 10px 25px rgba(255, 158, 187, 0.2);
            --radius: 24px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Quicksand', sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            overflow-x: hidden;
            position: relative;
        }

        /* Tło z bąbelkami */
        .bubbles {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            z-index: -1;
            pointer-events: none;
        }
        .bubble {
            position: absolute;
            background: rgba(255, 192, 203, 0.25);
            border-radius: 50%;
            animation: floatUp 12s infinite linear;
        }
        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0); opacity: 0; }
            50% { opacity: 0.6; }
            100% { transform: translateY(-10vh) scale(1); opacity: 0; }
        }

        header {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 20px rgba(177, 156, 217, 0.1);
            padding: 15px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 12px;
            text-decoration: none;
        }

        .logo-img {
            width: 50px;
            height: 50px;
            object-fit: contain;
            border-radius: 50%;
            box-shadow: 0 4px 10px rgba(255,158,187,0.3);
        }

        .logo-text {
            font-family: 'Fredoka', cursive;
            font-size: 26px;
            color: var(--primary);
            text-shadow: 1px 1px 0px var(--primary-light);
        }

        .nav-icons {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .cart-btn, .machine-nav-btn {
            background: var(--primary-light);
            border: none;
            padding: 10px 18px;
            border-radius: 50px;
            font-weight: 700;
            color: var(--text);
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: 0.2s;
            box-shadow: 0 4px 15px rgba(255, 158, 187, 0.3);
        }

        .cart-btn:hover, .machine-nav-btn:hover {
            transform: scale(1.05);
            background: var(--primary);
            color: white;
        }

        /* Hero sekcja z logo */
        .hero {
            text-align: center;
            padding: 40px 20px;
            max-width: 800px;
            margin: 0 auto;
        }

        .hero-main-logo {
            width: 180px;
            height: 180px;
            object-fit: contain;
            margin-bottom: 20px;
            filter: drop-shadow(0 10px 15px rgba(177, 156, 217, 0.3));
            animation: bounce 3s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-8px); }
        }

        .hero h1 {
            font-family: 'Fredoka', cursive;
            font-size: 38px;
            color: var(--secondary);
            margin-bottom: 10px;
        }

        .hero p {
            font-size: 17px;
            color: #7a6e7d;
            margin-bottom: 25px;
        }

        /* Gniotkomat Sekcja */
        .gniotkomat-section {
            background: linear-gradient(135deg, #fff0f5 0%, #f3e8ff 100%);
            border: 4px dashed var(--primary);
            border-radius: var(--radius);
            max-width: 600px;
            margin: 0 auto 40px auto;
            padding: 30px;
            text-align: center;
            box-shadow: var(--shadow);
            position: relative;
        }

        .gniotkomat-section h2 {
            font-family: 'Fredoka', cursive;
            color: var(--primary);
            font-size: 28px;
            margin-bottom: 10px;
        }

        .machine-box {
            background: white;
            border-radius: 20px;
            padding: 20px;
            margin: 20px 0;
            box-shadow: inset 0 4px 10px rgba(0,0,0,0.05);
            min-height: 140px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .drum {
            font-size: 48px;
            transition: transform 0.1s ease;
            margin-bottom: 10px;
        }

        .spin-btn {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 14px 35px;
            font-size: 18px;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(177, 156, 217, 0.4);
            transition: 0.2s;
            font-family: 'Fredoka', cursive;
        }

        .spin-btn:active {
            transform: scale(0.95);
        }

        .spin-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
            box-shadow: none;
        }

        .prize-alert {
            margin-top: 15px;
            font-weight: 700;
            color: #6b4c7a;
            min-height: 24px;
        }

        .attempts-counter {
            font-size: 13px;
            color: #999;
            margin-top: 8px;
        }

        /* Sklep - Filtry i Produkty */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px 60px 20px;
        }

        .filters {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 30px;
        }

        .category-chips {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .chip {
            background: white;
            border: 2px solid var(--primary-light);
            padding: 8px 18px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 600;
            color: var(--text);
            transition: 0.2s;
        }

        .chip.active, .chip:hover {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        .search-box {
            padding: 10px 20px;
            border-radius: 50px;
            border: 2px solid var(--primary-light);
            outline: none;
            width: 250px;
            font-size: 14px;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 25px;
        }

        .product-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            overflow: hidden;
            box-shadow: var(--shadow);
            transition: 0.3s;
            display: flex;
            flex-direction: column;
            position: relative;
        }

        .product-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 30px rgba(255, 158, 187, 0.3);
        }

        .badge {
            position: absolute;
            top: 15px;
            left: 15px;
            background: var(--secondary);
            color: white;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 700;
            z-index: 2;
        }

        .product-img {
            width: 100%;
            height: 220px;
            object-fit: cover;
            background: #ffe4e9;
        }

        .product-info {
            padding: 20px;
            display: flex;
            flex-direction: column;
            flex-grow: 1;
            justify-content: space-between;
        }

        .product-title {
            font-family: 'Fredoka', cursive;
            font-size: 20px;
            margin-bottom: 8px;
            color: var(--text);
        }

        .product-desc {
            font-size: 13px;
            color: #8c7f91;
            margin-bottom: 15px;
        }

        .product-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .price {
            font-family: 'Fredoka', cursive;
            font-size: 22px;
            color: var(--primary);
        }

        .add-to-cart {
            background: var(--primary-light);
            border: none;
            width: 40px; height: 40px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            transition: 0.2s;
        }

        .add-to-cart:hover {
            background: var(--primary);
            color: white;
            transform: scale(1.1);
        }

        /* Koszyk wysuwany */
        .cart-drawer {
            position: fixed;
            top: 0; right: -400px;
            width: 380px; height: 100%;
            background: white;
            box-shadow: -10px 0 30px rgba(0,0,0,0.1);
            z-index: 1000;
            transition: 0.3s ease-in-out;
            display: flex;
            flex-direction: column;
            padding: 25px;
        }

        .cart-drawer.open {
            right: 0;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--bg);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }

        .cart-header h3 {
            font-family: 'Fredoka', cursive;
            font-size: 24px;
            color: var(--secondary);
        }

        .close-cart {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #999;
        }

        .cart-items {
            flex-grow: 1;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .cart-item {
            display: flex;
            align-items: center;
            gap: 15px;
            background: var(--bg);
            padding: 10px;
            border-radius: 15px;
        }

        .cart-item img {
            width: 60px; height: 60px;
            border-radius: 10px;
            object-fit: cover;
        }

        .cart-item-info h4 {
            font-size: 15px;
            font-family: 'Fredoka', cursive;
        }

        .cart-item-info p {
            font-size: 13px;
            color: var(--primary);
            font-weight: 700;
        }

        .promo-section {
            margin: 15px 0;
            display: flex;
            gap: 10px;
        }

        .promo-input {
            flex-grow: 1;
            padding: 8px 12px;
            border: 2px solid var(--primary-light);
            border-radius: 10px;
            outline: none;
        }

        .apply-promo {
            background: var(--secondary);
            color: white;
            border: none;
            padding: 0 15px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
        }

        .cart-total {
            border-top: 2px solid var(--bg);
            padding-top: 15px;
            margin-top: 15px;
        }

        .total-row {
            display: flex;
            justify-content: space-between;
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 15px;
        }

        .checkout-btn {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            width: 100%;
            padding: 15px;
            border-radius: 15px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            font-family: 'Fredoka', cursive;
            box-shadow: 0 4px 15px rgba(255, 158, 187, 0.4);
        }

        /* Stopka / Kontakt / Social Media */
        footer {
            background: white;
            border-top: 2px solid var(--primary-light);
            padding: 40px 20px;
            margin-top: 60px;
        }

        .footer-content {
            max-width: 1000px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            align-items: center;
        }

        .socials {
            display: flex;
            gap: 15px;
            margin-top: 15px;
        }

        .social-link {
            background: var(--primary-light);
            color: var(--text);
            text-decoration: none;
            padding: 10px 20px;
            border-radius: 50px;
            font-weight: 700;
            transition: 0.2s;
        }

        .social-link:hover {
            background: var(--primary);
            color: white;
        }

        .contact-form input, .contact-form textarea {
            width: 100%;
            padding: 10px 15px;
            margin-bottom: 10px;
            border: 2px solid var(--primary-light);
            border-radius: 10px;
            outline: none;
        }

        .contact-form button {
            background: var(--secondary);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 10px;
            font-weight: 700;
            cursor: pointer;
        }

        @media(max-width: 768px) {
            .filters { flex-direction: column; align-items: stretch; }
            .search-box { width: 100%; }
        }
    </style>
</head>
<body>

    <div class="bubbles" id="bubblesContainer"></div>

    <header>
        <a href="#" class="logo-container">
            <img src="https://i.ibb.co/6R2B4z3/logo.png" class="logo-img" alt="Gniotkomat Logo" onerror="this.src='https://images.unsplash.com/photo-1533738363-b7f9aef128ce?auto=format&fit=crop&w=100&q=80'">
            <span class="logo-text">Gniotkomat</span>
        </a>
        <div class="nav-icons">
            <button class="machine-nav-btn" onclick="scrollToMachine()">🎰 Gniotkomat</button>
            <button class="cart-btn" onclick="toggleCart()">🛒 Koszyk (<span id="cartCount">0</span>)</button>
        </div>
    </header>

    <section class="hero">
        <img src="https://i.ibb.co/6R2B4z3/logo.png" class="hero-main-logo" alt="Gniotkomat Główne Logo" onerror="this.style.display='none'">
        <h1>Wydźwiękaj swój stres! 🌸</h1>
        <p>Najsłodsze, super mięciutkie gniotki Mochi, zwierzaki i gniotki giganty czekają na Ciebie!</p>
    </section>

    <!-- Gniotkomat Maszyna z limitem 3 prób i szansą 1/30 -->
    <div class="container">
        <div class="gniotkomat-section" id="gniotkomatSection">
            <h2>✨ Gniotkomat Szczęścia ✨</h2>
            <p>Zakręć maszyną! Masz łącznie 3 próby na wylosowanie zniżki lub darmowej dostawy.</p>
            <div class="machine-box">
                <div class="drum" id="drumEmoji">🐱 🐰 🐼 🦄</div>
                <div class="prize-alert" id="prizeAlert">Kliknij przycisk poniżej, aby losować!</div>
                <div class="attempts-counter" id="attemptsCounter">Pozostałe próby: 3 / 3</div>
            </div>
            <button class="spin-btn" id="spinBtn" onclick="spinMachine()">KRĘĆ MASZYNĄ! 🎰</button>
        </div>

        <!-- Filtry i Produkty -->
        <div class="filters">
            <div class="category-chips">
                <div class="chip active" onclick="filterCategory('all', this)">Wszystkie</div>
                <div class="chip" onclick="filterCategory('zwierzaki', this)">Zwierzaki</div>
                <div class="chip" onclick="filterCategory('mochi', this)">Mochi</div>
                <div class="chip" onclick="filterCategory('owoce', this)">Owoce</div>
                <div class="chip" onclick="filterCategory('giganty', this)">Giganty</div>
            </div>
            <input type="text" class="search-box" id="searchBox" placeholder="Szukaj gniotka..." oninput="filterProducts()">
        </div>

        <div class="products-grid" id="productsGrid">
            <!-- Produkty wstrzykiwane przez JS -->
        </div>
    </div>

    <!-- Wysuwany Koszyk -->
    <div class="cart-drawer" id="cartDrawer">
        <div class="cart-header">
            <h3>Twój Koszyk 🛍️</h3>
            <button class="close-cart" onclick="toggleCart()">✕</button>
        </div>
        <div class="cart-items" id="cartItems">
            <!-- Elementy koszyka -->
        </div>
        <div class="promo-section">
            <input type="text" class="promo-input" id="promoInput" placeholder="Kod rabatowy">
            <button class="apply-promo" onclick="applyPromo()">Użyj</button>
        </div>
        <div class="cart-total">
            <div class="total-row">
                <span>Razem:</span>
                <span id="cartTotalPrice">0.00 zł</span>
            </div>
            <button class="checkout-btn" onclick="checkout()">Przejdź do kasy 💕</button>
        </div>
    </div>

    <!-- Stopka / Kontakt / Social Media -->
    <footer>
        <div class="footer-content">
            <div>
                <h3>Gniotkomat</h3>
                <p>Sklep stworzony z miłością do odstresowywania. Masz pytania? Pisz śmiało!</p>
                <div class="socials">
                    <a href="https://instagram.com" target="_blank" class="social-link">📸 Instagram</a>
                    <a href="https://tiktok.com" target="_blank" class="social-link">🎵 TikTok</a>
                </div>
            </div>
            <div class="contact-form">
                <h3>Napisz do nas 💌</h3>
                <form onsubmit="handleContact(event)">
                    <input type="email" placeholder="Twój adres e-mail" required id="contactEmail">
                    <textarea rows="3" placeholder="Twoja wiadomość..." required id="contactMsg"></textarea>
                    <button type="submit">Wyślij wiadomość</button>
                </form>
            </div>
        </div>
    </footer>

    <script>
        // BAZA PRODUKTÓW - TUTAJ MOŽESZ DODAWAĆ I EDYTOWAĆ GNIOTKI!
        const products = [
            {
                id: 1,
                name: "Kotemote Pastelowy",
                category: "zwierzaki",
                price: 19.99,
                rating: 4.9,
                badge: "Bestseller",
                image: "https://images.unsplash.com/photo-1533738363-b7f9aef128ce?auto=format&fit=crop&w=500&q=80",
                desc: "Super miękki kotek w pastelowym różu, idealny do odstresowania."
            },
            {
                id: 2,
                name: "Mochi Łapka Kociaka",
                category: "mochi",
                price: 14.99,
                rating: 5.0,
                badge: "Hit",
                image: "https://images.unsplash.com/photo-1561948955-570b270e7c36?auto=format&fit=crop&w=500&q=80",
                desc: "Malutka, silikonowa łapka, którą można ugniatać bez końca."
            },
            {
                id: 3,
                name: "Truskawkowy Książę",
                category: "owoce",
                price: 22.50,
                rating: 4.8,
                badge: "Nowość",
                image: "https://images.unsplash.com/photo-1464965911861-746a04b4bca6?auto=format&fit=crop&w=500&q=80",
                desc: "Pachnąca truskawka o niesamowicie elastycznej strukturze."
            },
            {
                id: 4,
                name: "Gigantyczny Jednorożec",
                category: "giganty",
                price: 49.99,
                rating: 4.9,
                badge: "Super Gigant",
                image: "https://images.unsplash.com/photo-1535223289827-42f1e9919769?auto=format&fit=crop&w=500&q=80",
                desc: "Ogromny, tęczowy jednorożec do przytulania i ugniatania obiema rękami."
            },
            {
                id: 5,
                name: "Panda w Bambusie",
                category: "zwierzaki",
                price: 18.00,
                rating: 4.7,
                badge: "Polecamy",
                image: "https://images.unsplash.com/photo-1564349683136-77e08dba1ef7?auto=format&fit=crop&w=500&q=80",
                desc: "Słodka panda, która po uszczypnięciu śmiesznie wystawia pyszczek."
            },
            {
                id: 6,
                name: "Mochi Brzoskwinka",
                category: "mochi",
                price: 12.99,
                rating: 4.9,
                badge: "Słodkość",
                image: "https://images.unsplash.com/photo-1582979512210-99b6a53386f9?auto=format&fit=crop&w=500&q=80",
                desc: "Mięciutka brzoskwinka, idealna do kieszeni lub piórnika."
            }
        ];

        let cart = [];
        let currentDiscount = 0; 
        let freeShipping = false;
        
        // System limitu 3 prób na użytkownika (zapisywany w przeglądarce)
        let userAttempts = parseInt(localStorage.getItem('gniotkomat_attempts') || '0');
        const maxAttempts = 3;

        // Inicjalizacja licznika prób przy starcie
        window.addEventListener('DOMContentLoaded', () => {
            updateAttemptsUI();
        });

        function updateAttemptsUI() {
            const counterEl = document.getElementById('attemptsCounter');
            const btn = document.getElementById('spinBtn');
            const remaining = maxAttempts - userAttempts;
            
            if(remaining > 0) {
                counterEl.innerHTML = `Pozostałe próby: ${remaining} / ${maxAttempts}`;
            } else {
                counterEl.innerHTML = `Wykorzystano wszystkie próby (3/3) 🥺`;
                btn.disabled = true;
                btn.textContent = "BRAK PRÓB 🚫";
            }
        }

        // Generowanie bąbelków tła
        const bubblesContainer = document.getElementById('bubblesContainer');
        for(let i=0; i<15; i++) {
            const b = document.createElement('div');
            b.className = 'bubble';
            const size = Math.random() * 60 + 20 + 'px';
            b.style.width = size;
            b.style.height = size;
            b.style.left = Math.random() * 100 + 'vw';
            b.style.animationDuration = (Math.random() * 10 + 8) + 's';
            b.style.animationDelay = (Math.random() * 5) + 's';
            bubblesContainer.appendChild(b);
        }

        // Wyświetlanie produktów
        function renderProducts(items) {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = '';
            if(items.length === 0) {
                grid.innerHTML = '<p style="grid-column: 1/-1; text-align:center; padding: 40px; color:#8c7f91;">Nie znaleziono takich gniotków 🥺</p>';
                return;
            }
            items.forEach(p => {
                grid.innerHTML += `
                    <div class="product-card">
                        <span class="badge">${p.badge}</span>
                        <img src="${p.image}" class="product-img" alt="${p.name}">
                        <div class="product-info">
                            <div>
                                <h3 class="product-title">${p.name}</h3>
                                <p class="product-desc">${p.desc}</p>
                            </div>
                            <div class="product-footer">
                                <span class="price">${p.price.toFixed(2)} zł</span>
                                <button class="add-to-cart" onclick="addToCart(${p.id})">＋</button>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        // Filtrowanie i wyszukiwanie
        let activeCategory = 'all';
        function filterCategory(cat, element) {
            activeCategory = cat;
            document.querySelectorAll('.chip').forEach(c => c.classList.remove('active'));
            element.classList.add('active');
            filterProducts();
        }

        function filterProducts() {
            const query = document.getElementById('searchBox').value.toLowerCase();
            const filtered = products.filter(p => {
                const matchCat = activeCategory === 'all' || p.category === activeCategory;
                const matchQuery = p.name.toLowerCase().includes(query) || p.desc.toLowerCase().includes(query);
                return matchCat && matchQuery;
            });
            renderProducts(filtered);
        }

        // Gniotkomat - Losowanie (Szansa ok. 1 na 30, limit 3 prób)
        const emojis = ["🐱", "🐰", "🐼", "🦄", "🍑", "🍓", "🐙", "🐸"];
        function spinMachine() {
            if (userAttempts >= maxAttempts) return;

            userAttempts++;
            localStorage.setItem('gniotkomat_attempts', userAttempts);
            updateAttemptsUI();

            const drum = document.getElementById('drumEmoji');
            const alertBox = document.getElementById('prizeAlert');
            let counter = 0;

            alertBox.innerHTML = "Maszyna losuje Twój gniotek... 🌀";

            const interval = setInterval(() => {
                drum.textContent = emojis[Math.floor(Math.random() * emojis.length)];
                counter++;
                if(counter > 15) {
                    clearInterval(interval);
                    
                    // Szansa ok. 1 na 30 (losowanie liczby od 1 do 30)
                    // (Dla testów możesz zmienić '30' na '2' żeby wygrać od razu!)
                    const winChance = Math.floor(Math.random() * 30) + 1;

                    if(winChance === 1) {
                        // Wygrana! Losujemy co wygrał (zniżka lub darmowa dostawa)
                        if(Math.random() > 0.5) {
                            alertBox.innerHTML = "🎉 NIESAMOWITE! Wylosowano **15% zniżki**! Kod: <b style='color:var(--primary);'>GNIOTEK15</b>";
                        } else {
                            alertBox.innerHTML = "🚚 BRAWO! Wylosowano **Darmową Dostawę**! Kod: <b style='color:var(--primary);'>FREESHIP</b>";
                        }
                    } else {
                        // Przegrana w tej próbie
                        if(userAttempts < maxAttempts) {
                            alertBox.innerHTML = "🥺 Tym razem nic nie wylosowano! Spróbuj ponownie. (Próba " + userAttempts + "/3)";
                        } else {
                            alertBox.innerHTML = "😢 Wykorzystano wszystkie 3 próby. Może następnym razem!";
                        }
                    }
                }
            }, 80);
        }

        // Koszyk
        function toggleCart() {
            document.getElementById('cartDrawer').classList.toggle('open');
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            const found = cart.find(item => item.id === id);
            if(found) {
                found.qty++;
            } else {
                cart.push({...product, qty: 1});
            }
            updateCartUI();
            toggleCart();
        }

        function updateCartUI() {
            const countEl = document.getElementById('cartCount');
            const itemsEl = document.getElementById('cartItems');
            const totalEl = document.getElementById('cartTotalPrice');

            let totalCount = 0;
            let totalPrice = 0;

            itemsEl.innerHTML = '';
            if(cart.length === 0) {
                itemsEl.innerHTML = '<p style="text-align:center; color:#999; margin-top:30px;">Twój koszyk jest pusty 🛒</p>';
            }

            cart.forEach(item => {
                totalCount += item.qty;
                totalPrice += item.price * item.qty;
                itemsEl.innerHTML += `
                    <div class="cart-item">
                        <img src="${item.image}">
                        <div class="cart-item-info" style="flex-grow:1">
                            <h4>${item.name}</h4>
                            <p>${item.price.toFixed(2)} zł (x${item.qty})</p>
                        </div>
                        <button onclick="removeFromCart(${item.id})" style="background:none; border:none; color:#ff9ebb; cursor:pointer; font-size:16px;">🗑️</button>
                    </div>
                `;
            });

            if(currentDiscount > 0) {
                totalPrice = totalPrice * (1 - currentDiscount / 100);
            }

            countEl.textContent = totalCount;
            totalEl.textContent = totalPrice.toFixed(2) + ' zł' + (freeShipping ? ' (Darmowa dostawa!)' : '');
        }

        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCartUI();
        }

        function applyPromo() {
            const code = document.getElementById('promoInput').value.trim().toUpperCase();
            if(code === 'GNIOTEK15') {
                currentDiscount = 15;
                alert('Aktywowano 15% zniżki! 💕');
                updateCartUI();
            } else if(code === 'FREESHIP') {
                freeShipping = true;
                alert('Aktywowano darmową dostawę! 🚚');
                updateCartUI();
            } else {
                alert('Niepoprawny kod rabatowy 🥺');
            }
        }

        function checkout() {
            if(cart.length === 0) {
                alert('Twój koszyk jest pusty!');
                return;
            }
            alert('Dziękujemy za zamówienie w Gniotkomacie! 💖 W prawdziwym sklepie nastąpiłoby teraz przejście do płatności BLIK.');
            cart = [];
            currentDiscount = 0;
            freeShipping = false;
            updateCartUI();
            toggleCart();
        }

        function scrollToMachine() {
            document.getElementById('gniotkomatSection').scrollIntoView({ behavior: 'smooth' });
        }

        function handleContact(e) {
            e.preventDefault();
            alert('Dziękujemy za wiadomość! Odpiszemy najszybciej jak to możliwe 💌');
            document.getElementById('contactEmail').value = '';
            document.getElementById('contactMsg').value = '';
        }

        renderProducts(products);
    </script>
</body>
</html>