<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CoinKeeper - Учет финансов</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 0;
            margin: 0;
            color: #333;
            position: fixed;
            width: 100%;
            height: 100%;
        }

        .app-container {
            width: 100%;
            height: 100%;
            max-width: 450px;
            margin: 0 auto;
            background: white;
            border-radius: 0;
            box-shadow: 0 0 40px rgba(0,0,0,0.3);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            position: relative;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
            flex-shrink: 0;
        }

        .header h1 {
            font-size: 24px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .header .subtitle {
            font-size: 14px;
            opacity: 0.9;
        }

        .balance-section {
            padding: 25px 20px;
            text-align: center;
            background: #f8f9ff;
            margin: 15px;
            border-radius: 20px;
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.15);
            flex-shrink: 0;
        }

        .balance-label {
            font-size: 14px;
            color: #666;
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
        }

        .balance-amount {
            font-size: 48px;
            font-weight: 700;
            color: #333;
            line-height: 1.2;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .balance-positive {
            color: #10b981;
        }

        .balance-negative {
            color: #ef4444;
        }

        .stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            padding: 0 20px;
            margin-bottom: 20px;
            flex-shrink: 0;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 18px;
            box-shadow: 0 6px 15px rgba(0,0,0,0.08);
            text-align: center;
            border: 1px solid #f0f0f0;
            transition: transform 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-2px);
        }

        .stat-value {
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 12px;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 500;
        }

        .income {
            color: #10b981;
        }

        .expense {
            color: #ef4444;
        }

        .tabs {
            display: flex;
            background: #f8f9ff;
            margin: 0 20px;
            border-radius: 15px;
            padding: 6px;
            margin-bottom: 20px;
            flex-shrink: 0;
        }

        .tab {
            flex: 1;
            text-align: center;
            padding: 14px;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            color: #666;
            font-size: 15px;
        }

        .tab.active {
            background: white;
            color: #667eea;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.25);
        }

        .tab:hover:not(.active) {
            background: rgba(255,255,255,0.5);
        }

        .form-section {
            padding: 0 20px;
            margin-bottom: 25px;
            flex-shrink: 0;
        }

        .input-group {
            margin-bottom: 20px;
        }

        .input-group label {
            display: block;
            font-size: 14px;
            color: #666;
            margin-bottom: 8px;
            font-weight: 600;
        }

        .input-group input,
        .input-group select {
            width: 100%;
            padding: 18px;
            border: 2px solid #e5e7eb;
            border-radius: 15px;
            font-size: 16px;
            transition: all 0.3s;
            background: white;
        }

        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .type-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-bottom: 20px;
        }

        .type-button {
            padding: 18px;
            border: 2px solid #e5e7eb;
            border-radius: 15px;
            text-align: center;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            background: white;
            font-size: 16px;
        }

        .type-button.active {
            border-color: #667eea;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        .income-button.active {
            border-color: #10b981;
            background: linear-gradient(135deg, #10b981 0%, #34d399 100%);
        }

        .expense-button.active {
            border-color: #ef4444;
            background: linear-gradient(135deg, #ef4444 0%, #f87171 100%);
        }

        .submit-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 20px;
            border-radius: 15px;
            font-size: 17px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s;
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .submit-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.5);
        }

        .submit-button:active {
            transform: translateY(0);
        }

        .transactions-section {
            flex: 1;
            padding: 0 20px 20px;
            overflow-y: auto;
            min-height: 0;
        }

        .transactions-section h3 {
            font-size: 18px;
            margin-bottom: 20px;
            color: #333;
            font-weight: 600;
            padding-left: 5px;
        }

        .transaction-list {
            list-style: none;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 5px;
        }

        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 18px;
            background: white;
            border-radius: 15px;
            margin-bottom: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            border-left: 5px solid;
            transition: transform 0.2s;
            animation: slideIn 0.3s ease-out;
        }

        .transaction-item:hover {
            transform: translateX(5px);
        }

        .transaction-item.income {
            border-left-color: #10b981;
            background: linear-gradient(to right, #f0fdf4, white);
        }

        .transaction-item.expense {
            border-left-color: #ef4444;
            background: linear-gradient(to right, #fef2f2, white);
        }

        .transaction-info {
            flex: 1;
        }

        .transaction-category {
            font-weight: 600;
            margin-bottom: 6px;
            font-size: 16px;
            color: #333;
        }

        .transaction-date {
            font-size: 13px;
            color: #888;
        }

        .transaction-amount {
            font-weight: 700;
            font-size: 20px;
        }

        .income-amount {
            color: #10b981;
        }

        .expense-amount {
            color: #ef4444;
        }

        .no-transactions {
            text-align: center;
            padding: 60px 20px;
            color: #999;
            font-size: 16px;
            background: #f9fafb;
            border-radius: 15px;
            margin-top: 20px;
        }

        .categories-section {
            flex: 1;
            padding: 0 20px 20px;
            overflow-y: auto;
        }

        .category-list {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
        }

        .category-item {
            padding: 20px 10px;
            background: white;
            border-radius: 15px;
            text-align: center;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100px;
        }

        .category-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.2);
            border-color: #667eea;
        }

        .category-item.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-color: #764ba2;
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
        }

        .category-icon {
            font-size: 24px;
            margin-bottom: 8px;
        }

        .category-name {
            font-weight: 500;
        }

        .loading {
            text-align: center;
            padding: 60px;
            color: #667eea;
            font-size: 18px;
            font-weight: 500;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #10b981 0%, #34d399 100%);
            color: white;
            padding: 20px 25px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.4);
            transform: translateX(150%);
            transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            z-index: 1000;
            max-width: 300px;
            font-weight: 500;
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.error {
            background: linear-gradient(135deg, #ef4444 0%, #f87171 100%);
            box-shadow: 0 10px 30px rgba(239, 68, 68, 0.4);
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(-20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .transaction-item {
            animation: slideIn 0.3s ease-out;
        }

        .sync-button {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            transition: all 0.3s;
        }

        .sync-button:hover {
            background: rgba(255,255,255,0.3);
            transform: rotate(180deg);
        }

        .month-selector {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
            margin-bottom: 20px;
            flex-shrink: 0;
        }

        .month-button {
            background: #f8f9ff;
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            font-size: 20px;
            color: #667eea;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .month-button:hover {
            background: #667eea;
            color: white;
            transform: scale(1.1);
        }

        .current-month {
            font-weight: 600;
            color: #333;
            font-size: 16px;
        }

        /* Стили для скроллбара */
        .transaction-list::-webkit-scrollbar {
            width: 6px;
        }

        .transaction-list::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 3px;
        }

        .transaction-list::-webkit-scrollbar-thumb {
            background: #667eea;
            border-radius: 3px;
        }

        .transaction-list::-webkit-scrollbar-thumb:hover {
            background: #764ba2;
        }

        /* Мобильная оптимизация */
        @media (max-width: 480px) {
            .app-container {
                border-radius: 0;
            }
            
            .balance-amount {
                font-size: 42px;
            }
            
            .category-list {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .stat-value {
                font-size: 24px;
            }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <div class="header">
            <button class="sync-button" onclick="syncWithBot()">
                🔄
            </button>
            <h1>CoinKeeper</h1>
            <div class="subtitle">Учет расходов и доходов</div>
        </div>

        <!-- Balance Section -->
        <div class="balance-section">
            <div class="balance-label">Текущий баланс</div>
            <div class="balance-amount" id="balance">0 ₽</div>
        </div>

        <!-- Stats -->
        <div class="stats">
            <div class="stat-card">
                <div class="stat-value income" id="total-income">0 ₽</div>
                <div class="stat-label">Доходы</div>
            </div>
            <div class="stat-card">
                <div class="stat-value expense" id="total-expense">0 ₽</div>
                <div class="stat-label">Расходы</div>
            </div>
        </div>

        <!-- Tabs -->
        <div class="tabs">
            <div class="tab active" onclick="switchTab('transactions')">Транзакции</div>
            <div class="tab" onclick="switchTab('add')">Добавить</div>
            <div class="tab" onclick="switchTab('categories')">Категории</div>
        </div>

        <!-- Month Selector -->
        <div class="month-selector" id="monthSelector" style="display: none;">
            <button class="month-button" onclick="changeMonth(-1)">←</button>
            <span class="current-month" id="currentMonth">Январь 2024</span>
            <button class="month-button" onclick="changeMonth(1)">→</button>
        </div>

        <!-- Add Transaction Form (hidden by default) -->
        <div class="form-section" id="addForm" style="display: none;">
            <div class="type-buttons">
                <div class="type-button expense-button active" onclick="setTransactionType('expense')">
                    Расход
                </div>
                <div class="type-button income-button" onclick="setTransactionType('income')">
                    Доход
                </div>
            </div>
            
            <div class="input-group">
                <label for="amount">Сумма (₽)</label>
                <input type="number" id="amount" placeholder="Введите сумму" min="1" step="1">
            </div>
            
            <div class="input-group">
                <label for="category">Категория</label>
                <select id="category">
                    <option value="еда">🍕 Еда</option>
                    <option value="транспорт">🚗 Транспорт</option>
                    <option value="развлечения">🎬 Развлечения</option>
                    <option value="покупки">🛍️ Покупки</option>
                    <option value="здоровье">🏥 Здоровье</option>
                    <option value="образование">📚 Образование</option>
                    <option value="квартира">🏠 Квартира</option>
                    <option value="зарплата">💰 Зарплата</option>
                    <option value="другое">📌 Другое</option>
                </select>
            </div>
            
            <button class="submit-button" onclick="addTransaction()">
                Добавить операцию
            </button>
        </div>

        <!-- Categories Section (hidden by default) -->
        <div class="categories-section" id="categoriesSection" style="display: none;">
            <h3>Выберите категорию</h3>
            <div class="category-list" id="categoryList">
                <!-- Categories will be populated by JavaScript -->
            </div>
        </div>

        <!-- Transactions List -->
        <div class="transactions-section" id="transactionsSection">
            <h3>Последние операции</h3>
            <ul class="transaction-list" id="transactionList">
                <li class="no-transactions" id="noTransactions">
                    Нет операций. Добавьте первую!
                </li>
            </ul>
        </div>

        <!-- Loading Indicator -->
        <div class="loading" id="loading" style="display: none;">
            <div>Загрузка данных...</div>
            <div style="font-size: 40px; margin-top: 20px;">⌛</div>
        </div>
    </div>

    <!-- Notification -->
    <div class="notification" id="notification"></div>

    <script>
        // Telegram WebApp API
        const tg = window.Telegram?.WebApp;
        
        // Глобальные переменные
        let userData = {
            balance: 0,
            transactions: [],
            categories: {},
            totalTransactions: 0
        };
        
        let currentTab = 'transactions';
        let transactionType = 'expense';
        
        // Категории с иконками
        const categories = [
            { id: 'еда', name: 'Еда', icon: '🍕' },
            { id: 'транспорт', name: 'Транспорт', icon: '🚗' },
            { id: 'развлечения', name: 'Развлечения', icon: '🎬' },
            { id: 'покупки', name: 'Покупки', icon: '🛍️' },
            { id: 'здоровье', name: 'Здоровье', icon: '🏥' },
            { id: 'образование', name: 'Образование', icon: '📚' },
            { id: 'квартира', name: 'Квартира', icon: '🏠' },
            { id: 'зарплата', name: 'Зарплата', icon: '💰' },
            { id: 'кофе', name: 'Кофе', icon: '☕' },
            { id: 'обед', name: 'Обед', icon: '🍽️' },
            { id: 'продукты', name: 'Продукты', icon: '🛒' },
            { id: 'другое', name: 'Другое', icon: '📌' }
        ];

        // Инициализация приложения
        document.addEventListener('DOMContentLoaded', function() {
            initApp();
        });

        // Инициализация приложения
        function initApp() {
            if (tg) {
                // Если в Telegram
                tg.ready();
                tg.expand();
                loadUserDataFromBot();
            } else {
                // Если не в Telegram, используем локальное хранилище
                loadFromLocalStorage();
                showNotification('Используется локальное хранилище', false);
            }
            
            setupCategoryButtons();
            updateCurrentMonth();
        }

        // Загрузка данных из бота
        function loadUserDataFromBot() {
            showLoading(true);
            
            // Отправляем запрос боту
            const data = {
                action: 'get_user_data',
                timestamp: new Date().getTime()
            };
            
            if (tg) {
                tg.sendData(JSON.stringify(data));
                setTimeout(() => {
                    // Загрузка демо-данных, если ответ не пришел
                    loadDemoData();
                    showLoading(false);
                }, 2000);
            } else {
                loadFromLocalStorage();
                showLoading(false);
            }
        }

        // Загрузка из localStorage
        function loadFromLocalStorage() {
            const saved = localStorage.getItem('coinKeeperData');
            if (saved) {
                try {
                    userData = JSON.parse(saved);
                    updateUI();
                    showNotification('Данные загружены из памяти', false);
                } catch (e) {
                    console.error('Ошибка загрузки:', e);
                    loadDemoData();
                }
            } else {
                loadDemoData();
            }
        }

        // Сохранение в localStorage
        function saveToLocalStorage() {
            localStorage.setItem('coinKeeperData', JSON.stringify(userData));
        }

        // Загрузка демо-данных
        function loadDemoData() {
            const demoTransactions = [
                { 
                    amount: 20000, 
                    category: 'зарплата', 
                    timestamp: new Date().toLocaleDateString('ru-RU', { 
                        day: '2-digit', 
                        month: '2-digit',
                        hour: '2-digit',
                        minute: '2-digit'
                    }) 
                },
                { 
                    amount: -500, 
                    category: 'кофе', 
                    timestamp: new Date().toLocaleDateString('ru-RU', { 
                        day: '2-digit', 
                        month: '2-digit',
                        hour: '2-digit',
                        minute: '2-digit'
                    }) 
                },
                { 
                    amount: -1500, 
                    category: 'обед', 
                    timestamp: new Date().toLocaleDateString('ru-RU', { 
                        day: '2-digit', 
                        month: '2-digit',
                        hour: '2-digit',
                        minute: '2-digit'
                    }) 
                }
            ];
            
            userData.transactions = demoTransactions;
            userData.balance = demoTransactions.reduce((sum, t) => sum + t.amount, 0);
            userData.totalTransactions = demoTransactions.length;
            userData.categories = {};
            
            // Создаем категории из транзакций
            demoTransactions.forEach(t => {
                if (!userData.categories[t.category]) {
                    userData.categories[t.category] = 0;
                }
                userData.categories[t.category] += t.amount;
            });
            
            updateUI();
            saveToLocalStorage();
        }

        // Обновление UI
        function updateUI() {
            // Обновляем баланс
            const balanceElement = document.getElementById('balance');
            balanceElement.textContent = `${formatNumber(userData.balance)} ₽`;
            
            if (userData.balance > 0) {
                balanceElement.className = 'balance-amount balance-positive';
            } else if (userData.balance < 0) {
                balanceElement.className = 'balance-amount balance-negative';
            } else {
                balanceElement.className = 'balance-amount';
            }
            
            // Рассчитываем доходы и расходы
            let income = 0;
            let expense = 0;
            
            userData.transactions.forEach(transaction => {
                if (transaction.amount > 0) {
                    income += transaction.amount;
                } else {
                    expense += Math.abs(transaction.amount);
                }
            });
            
            // Обновляем статистику
            document.getElementById('total-income').textContent = `${formatNumber(income)} ₽`;
            document.getElementById('total-expense').textContent = `${formatNumber(expense)} ₽`;
            
            // Обновляем список транзакций
            updateTransactionList();
        }

        // Обновление списка транзакций
        function updateTransactionList() {
            const transactionList = document.getElementById('transactionList');
            const noTransactions = document.getElementById('noTransactions');
            
            if (userData.transactions.length === 0) {
                noTransactions.style.display = 'block';
                transactionList.innerHTML = '<li class="no-transactions">Нет операций. Добавьте первую!</li>';
                return;
            }
            
            noTransactions.style.display = 'none';
            
            // Показываем последние 10 транзакций в обратном порядке
            const recentTransactions = [...userData.transactions].reverse().slice(0, 10);
            
            let html = '';
            recentTransactions.forEach((transaction, index) => {
                const isIncome = transaction.amount > 0;
                const amount = Math.abs(transaction.amount);
                const date = transaction.timestamp || new Date().toLocaleDateString('ru-RU', { 
                    day: '2-digit', 
                    month: '2-digit',
                    hour: '2-digit',
                    minute: '2-digit'
                });
                
                // Находим иконку категории
                const category = categories.find(cat => cat.id === transaction.category.toLowerCase());
                const categoryName = category ? category.name : transaction.category;
                const categoryIcon = category ? category.icon : '📌';
                
                html += `
                    <li class="transaction-item ${isIncome ? 'income' : 'expense'}">
                        <div class="transaction-info">
                            <div class="transaction-category">
                                ${categoryIcon} ${categoryName}
                            </div>
                            <div class="transaction-date">${date}</div>
                        </div>
                        <div class="transaction-amount ${isIncome ? 'income-amount' : 'expense-amount'}">
                            ${isIncome ? '+' : '-'}${formatNumber(amount)} ₽
                        </div>
                    </li>
                `;
            });
            
            transactionList.innerHTML = html;
        }

        // Форматирование чисел
        function formatNumber(num) {
            return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
        }

        // Переключение вкладок
        function switchTab(tabName) {
            currentTab = tabName;
            
            // Обновляем активные табы
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            const tabElements = document.querySelectorAll('.tab');
            const tabIndex = tabName === 'transactions' ? 0 : tabName === 'add' ? 1 : 2;
            tabElements[tabIndex].classList.add('active');
            
            // Показываем/скрываем соответствующие секции
            document.getElementById('transactionsSection').style.display = 'none';
            document.getElementById('addForm').style.display = 'none';
            document.getElementById('categoriesSection').style.display = 'none';
            document.getElementById('monthSelector').style.display = 'none';
            
            switch(tabName) {
                case 'transactions':
                    document.getElementById('transactionsSection').style.display = 'block';
                    document.getElementById('monthSelector').style.display = 'flex';
                    break;
                case 'add':
                    document.getElementById('addForm').style.display = 'block';
                    break;
                case 'categories':
                    document.getElementById('categoriesSection').style.display = 'block';
                    break;
            }
        }

        // Установка типа транзакции
        function setTransactionType(type) {
            transactionType = type;
            
            // Обновляем кнопки
            document.querySelectorAll('.type-button').forEach(button => {
                button.classList.remove('active');
            });
            
            if (type === 'expense') {
                document.querySelector('.expense-button').classList.add('active');
            } else {
                document.querySelector('.income-button').classList.add('active');
            }
        }

        // Добавление транзакции
        function addTransaction() {
            const amountInput = document.getElementById('amount');
            const categorySelect = document.getElementById('category');
            
            const amount = parseInt(amountInput.value);
            const category = categorySelect.value;
            
            if (!amount || amount <= 0) {
                showNotification('Введите корректную сумму', true);
                amountInput.focus();
                return;
            }
            
            // Создаем транзакцию
            const finalAmount = transactionType === 'expense' ? -amount : amount;
            const newTransaction = {
                amount: finalAmount,
                category: category,
                timestamp: new Date().toLocaleDateString('ru-RU', { 
                    day: '2-digit', 
                    month: '2-digit',
                    hour: '2-digit',
                    minute: '2-digit'
                })
            };
            
            // Добавляем в данные
            userData.transactions.push(newTransaction);
            userData.balance += finalAmount;
            userData.totalTransactions++;
            
            // Обновляем категории
            if (!userData.categories[category]) {
                userData.categories[category] = 0;
            }
            userData.categories[category] += finalAmount;
            
            // Сохраняем
            saveToLocalStorage();
            
            // Обновляем UI
            updateUI();
            
            // Отправляем в бот, если в Telegram
            if (tg) {
                const transactionData = {
                    action: 'add_transaction',
                    amount: amount,
                    category: category,
                    type: transactionType,
                    timestamp: new Date().toISOString()
                };
                
                tg.sendData(JSON.stringify(transactionData));
            }
            
            // Показываем уведомление
            const typeText = transactionType === 'expense' ? 'Расход' : 'Доход';
            showNotification(`${typeText} добавлен: ${formatNumber(amount)} ₽`);
            
            // Очищаем форму
            amountInput.value = '';
            amountInput.focus();
            
            // Переключаемся на вкладку транзакций
            switchTab('transactions');
        }

        // Настройка кнопок категорий
        function setupCategoryButtons() {
            const categoryList = document.getElementById('categoryList');
            let html = '';
            
            categories.forEach(category => {
                html += `
                    <div class="category-item" onclick="selectCategory('${category.id}')">
                        <div class="category-icon">${category.icon}</div>
                        <div class="category-name">${category.name}</div>
                    </div>
                `;
            });
            
            categoryList.innerHTML = html;
        }

        // Выбор категории
        function selectCategory(categoryId) {
            document.getElementById('category').value = categoryId;
            switchTab('add');
            showNotification(`Выбрана категория: ${categoryId}`, false);
        }

        // Изменение месяца
        function changeMonth(delta) {
            // В будущем можно реализовать фильтрацию по месяцам
            showNotification('Фильтрация по месяцам скоро появится!', false);
        }

        // Обновление текущего месяца
        function updateCurrentMonth() {
            const now = new Date();
            const monthNames = [
                'Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь',
                'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь'
            ];
            const monthName = monthNames[now.getMonth()];
            const year = now.getFullYear();
            
            document.getElementById('currentMonth').textContent = `${monthName} ${year}`;
        }

        // Синхронизация с ботом
        function syncWithBot() {
            if (tg) {
                showNotification('Синхронизация с ботом...', false);
                loadUserDataFromBot();
            } else {
                showNotification('Не в Telegram', true);
            }
        }

        // Показать/скрыть загрузку
        function showLoading(show) {
            document.getElementById('loading').style.display = show ? 'block' : 'none';
        }

        // Показать уведомление
        function showNotification(message, isError = false) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${isError ? 'error' : ''}`;
            
            // Показываем
            setTimeout(() => {
                notification.classList.add('show');
            }, 10);
            
            // Скрываем через 3 секунды
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        // Обработчик сообщений от Telegram
        function handleTelegramMessage(data) {
            try {
                const message = JSON.parse(data);
                
                if (message.action === 'update_data') {
                    // Обновляем данные от бота
                    userData = message.data;
                    updateUI();
                    saveToLocalStorage();
                    showNotification('Данные синхронизированы с ботом', false);
                }
            } catch (e) {
                console.error('Ошибка обработки сообщения:', e);
            }
        }

        // Инициализация слушателя сообщений (для Telegram)
        if (tg) {
            // Telegram WebApp обрабатывает сообщения автоматически
            console.log('Telegram WebApp инициализирован');
        }

        // Добавляем обработчик нажатия Enter в поле суммы
        document.getElementById('amount')?.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addTransaction();
            }
        });
    </script>
</body>
</html>
