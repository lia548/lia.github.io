<!-- Sistema de Login -->
<div id="loginSection" class="flex items-center justify-center min-h-screen">
    <div class="bg-white p-8 rounded-lg shadow-lg w-full max-w-md">
        <h2 class="text-2xl font-bold text-center mb-6">Acessar Sistema</h2>
        <div class="mb-4">
            <label class="block text-gray-700 mb-2">Tipo de Usuário</label>
            <select id="userType" class="w-full px-3 py-2 border rounded form-input">
                <option value="client">Cliente</option>
                <option value="admin">Vendedor</option>
            </select>
        </div>
        <div class="mb-6 relative">
            <label class="block text-gray-700 mb-2">Senha (para vendedor)</label>
            <div class="relative">
                <input id="password" type="password" class="w-full px-3 py-2 border rounded form-input" placeholder="Digite a senha">
                <button onclick="togglePasswordVisibility()" type="button" class="absolute inset-y-0 right-0 pr-3 flex items-center">
                    <svg id="eyeIcon" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                    </svg>
                </button>
            </div>
        </div>
        <button onclick="login()" class="w-full bg-blue-500 hover:bg-blue-600 text-white py-2 rounded">
            Entrar
        </button>
    </div>
</div>
// Mostrar/esconder senha
function togglePasswordVisibility() {
    const passwordInput = document.getElementById('password');
    const eyeIcon = document.getElementById('eyeIcon');
    
    if (passwordInput.type === 'password') {
        passwordInput.type = 'text';
        eyeIcon.innerHTML = `
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21" />
        `;
    } else {
        passwordInput.type = 'password';
        eyeIcon.innerHTML = `
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
        `;
    }
}
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bazar de Roupas Novas e Usadas</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-image: url('https://images.unsplash.com/photo-1607082348824-0a96f2a4b9da?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-attachment: fixed;
            background-position: center;
            position: relative;
        }
        
        body::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(255, 255, 255, 0.85);
            z-index: -1;
        }
        
        .price-tag {
            transition: all 0.3s ease;
        }
        
        .price-tag:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .header-banner {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-bottom: 3px solid #d4a373;
        }
        
        .item-card {
            transition: all 0.3s ease;
            background-color: rgba(255, 255, 255, 0.9);
        }
        
        .item-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
    </style>
</head>
<body class="min-h-screen py-8">
    <div class="container mx-auto px-4">
        <!-- Header Banner -->
        <div class="header-banner rounded-lg shadow-lg mb-8 p-6 text-center">
            <h1 class="text-4xl font-bold text-gray-800 mb-2">BAZAR DE ROUPAS</h1>
            <h2 class="text-2xl font-semibold text-gray-700">Novas e Usadas com Preços Variados</h2>
            <p class="text-lg text-gray-600 mt-2">De R$2,00 até R$60,00 - Tudo com ótima qualidade!</p>
        </div>
        
        <!-- Price Filter -->
        <div class="bg-white rounded-lg shadow-md p-4 mb-8">
            <h3 class="text-xl font-semibold mb-4 text-gray-800">Filtrar por Preço:</h3>
            <div class="flex flex-wrap gap-2">
                <button onclick="filterItems(2)" class="price-tag bg-green-100 text-green-800 px-4 py-2 rounded-full font-medium">R$2</button>
                <button onclick="filterItems(5)" class="price-tag bg-blue-100 text-blue-800 px-4 py-2 rounded-full font-medium">R$5</button>
                <button onclick="filterItems(10)" class="price-tag bg-purple-100 text-purple-800 px-4 py-2 rounded-full font-medium">R$10</button>
                <button onclick="filterItems(15)" class="price-tag bg-yellow-100 text-yellow-800 px-4 py-2 rounded-full font-medium">R$15</button>
                <button onclick="filterItems(20)" class="price-tag bg-red-100 text-red-800 px-4 py-2 rounded-full font-medium">R$20</button>
                <button onclick="filterItems(25)" class="price-tag bg-indigo-100 text-indigo-800 px-4 py-2 rounded-full font-medium">R$25</button>
                <button onclick="filterItems(30)" class="price-tag bg-pink-100 text-pink-800 px-4 py-2 rounded-full font-medium">R$30</button>
                <button onclick="filterItems(40)" class="price-tag bg-teal-100 text-teal-800 px-4 py-2 rounded-full font-medium">R$40</button>
                <button onclick="filterItems(50)" class="price-tag bg-orange-100 text-orange-800 px-4 py-2 rounded-full font-medium">R$50</button>
                <button onclick="filterItems(60)" class="price-tag bg-amber-100 text-amber-800 px-4 py-2 rounded-full font-medium">R$60</button>
                <button onclick="resetFilter()" class="price-tag bg-gray-100 text-gray-800 px-4 py-2 rounded-full font-medium">Todos</button>
            </div>
        </div>
        
        <!-- Clothing Items Grid -->
        <div id="itemsGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
            <!-- Items will be dynamically inserted here by JavaScript -->
        </div>
    </div>

    <script>
        // Clothing items data
        const clothingItems = [
            { name: "Camiseta Básica", type: "nova", price: 20, category: "camisetas" },
            { name: "Calça Jeans", type: "usada", price: 30, category: "calças" },
            { name: "Vestido Floral", type: "nova", price: 40, category: "vestidos" },
            { name: "Blusa de Moletom", type: "usada", price: 15, category: "blusas" },
            { name: "Short Jeans", type: "nova", price: 25, category: "shorts" },
            { name: "Camisa Social", type: "usada", price: 10, category: "camisas" },
            { name: "Saia Midi", type: "nova", price: 15, category: "saias" },
            { name: "Jaqueta de Couro", type: "usada", price: 50, category: "jaquetas" },
            { name: "Blazer", type: "nova", price: 60, category: "blazers" },
            { name: "Camiseta Estampada", type: "usada", price: 5, category: "camisetas" },
            { name: "Calça de Moletom", type: "nova", price: 30, category: "calças" },
            { name: "Vestido Longo", type: "usada", price: 20, category: "vestidos" },
            { name: "Blusa de Frio", type: "nova", price: 40, category: "blusas" },
            { name: "Short Esportivo", type: "usada", price: 10, category: "shorts" },
            { name: "Camisa Polo", type: "nova", price: 25, category: "camisas" },
            { name: "Saia Longa", type: "usada", price: 15, category: "saias" },
            { name: "Jaqueta Jeans", type: "nova", price: 50, category: "jaquetas" },
            { name: "Blazer Slim", type: "usada", price: 30, category: "blazers" },
            { name: "Camiseta Regata", type: "nova", price: 15, category: "camisetas" },
            { name: "Calça Social", type: "usada", price: 20, category: "calças" },
            { name: "Vestido Curto", type: "nova", price: 30, category: "vestidos" },
            { name: "Blusa Tricot", type: "usada", price: 10, category: "blusas" },
            { name: "Short Jeans Destroyed", type: "nova", price: 25, category: "shorts" },
            { name: "Camisa Xadrez", type: "usada", price: 15, category: "camisas" },
            { name: "Saia Plissada", type: "nova", price: 20, category: "saias" },
            { name: "Jaqueta Corta-Vento", type: "usada", price: 40, category: "jaquetas" },
            { name: "Blazer Clássico", type: "nova", price: 60, category: "blazers" },
            { name: "Camiseta Oversized", type: "usada", price: 20, category: "camisetas" },
            { name: "Calça Pantalona", type: "nova", price: 30, category: "calças" },
            { name: "Vestido Tubinho", type: "usada", price: 15, category: "vestidos" },
            { name: "Blusa Cropped", type: "nova", price: 25, category: "blusas" },
            { name: "Short Sarja", type: "usada", price: 10, category: "shorts" },
            { name: "Camisa Slim", type: "nova", price: 30, category: "camisas" },
            { name: "Saia Evasê", type: "usada", price: 15, category: "saias" },
            { name: "Jaqueta Bomber", type: "nova", price: 50, category: "jaquetas" },
            { name: "Blazer Moderno", type: "usada", price: 40, category: "blazers" },
            { name: "Camiseta Gola V", type: "nova", price: 20, category: "camisetas" },
            { name: "Calça Legging", type: "usada", price: 15, category: "calças" },
            { name: "Vestido Midi", type: "nova", price: 30, category: "vestidos" },
            { name: "Blusa Gola Alta", type: "usada", price: 10, category: "blusas" },
            { name: "Short Linho", type: "nova", price: 25, category: "shorts" },
            { name: "Camisa Básica", type: "usada", price: 15, category: "camisas" },
            { name: "Saia Lápis", type: "nova", price: 20, category: "saias" },
            { name: "Jaqueta de Pele", type: "usada", price: 50, category: "jaquetas" },
            { name: "Blazer Tradicional", type: "nova", price: 60, category: "blazers" }
        ];

        // Function to render items
        function renderItems(items = clothingItems) {
            const itemsGrid = document.getElementById('itemsGrid');
            itemsGrid.innerHTML = '';
            
            items.forEach(item => {
                const itemCard = document.createElement('div');
                itemCard.className = 'item-card rounded-lg shadow-md overflow-hidden';
                
                // Determine color based on price
                let priceColor;
                if (item.price <= 5) priceColor = 'bg-green-500';
                else if (item.price <= 15) priceColor = 'bg-blue-500';
                else if (item.price <= 25) priceColor = 'bg-purple-500';
                else if (item.price <= 40) priceColor = 'bg-yellow-500';
                else priceColor = 'bg-red-500';
                
                itemCard.innerHTML = `
                    <div class="relative h-48 bg-gray-200">
                        <div class="absolute top-2 right-2 ${priceColor} text-white px-2 py-1 rounded text-sm font-bold">
                            R$${item.price.toFixed(2)}
                        </div>
                        <div class="absolute bottom-2 left-2 bg-white bg-opacity-80 px-2 py-1 rounded text-xs">
                            ${item.type === 'nova' ? '🆕 Nova' : '🔄 Usada'}
                        </div>
                    </div>
                    <div class="p-4">
                        <h3 class="font-semibold text-lg text-gray-800">${item.name}</h3>
                        <p class="text-gray-600">${item.category.charAt(0).toUpperCase() + item.category.slice(1)}</p>
                        <div class="mt-3 flex justify-between items-center">
                            <span class="text-gray-700 font-medium">R$${item.price.toFixed(2)}</span>
                            <button class="bg-amber-500 hover:bg-amber-600 text-white px-3 py-1 rounded text-sm">
                                Comprar
                            </button>
                        </div>
                    </div>
                `;
                
                itemsGrid.appendChild(itemCard);
            });
        }

        // Filter items by price
        function filterItems(price) {
            const filteredItems = clothingItems.filter(item => item.price === price);
            renderItems(filteredItems);
        }

        // Reset filter
        function resetFilter() {
            renderItems();
        }

        // Initial render
        document.addEventListener('DOMContentLoaded', renderItems);
    </script>
</body>
</html>
