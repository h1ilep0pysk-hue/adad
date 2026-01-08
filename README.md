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
            padding: 20px;
            color: #333;
        }

        .app-container {
            max-width: 450px;
            margin: 0 auto;
            background: white;
            border-radius: 24px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
            min-height: 95vh;
            display: flex;
            flex-direction: column;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
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
            padding: 20px;
            text-align: center;
            background: #f8f9ff;
            margin: 15px;
            border-radius: 18px;
            box-shadow: 0 4px 20px rgba(102, 126, 234, 0.1);
        }

        .balance-label {
            font-size: 14px;
            color: #666;
            margin-bottom: 8px;
        }

        .balance-amount {
            font-size: 42px;
            font-weight: 700;
            color: #333;
            line-height: 1;
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
            gap: 12px;
            padding: 0 20px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: white;
            padding: 18px;
            border-radius: 16px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            text-align: center;
            border: 1px solid #f0f0f0;
        }

        .stat-value {
            font-size: 24px;
            font-weight: 600;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 12px;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 0.5px;
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
            border-radius: 12px;
            padding: 4px;
            margin-bottom: 20px;
        }

        .tab {
            flex: 1;
            text-align: center;
            padding: 12px;
            border-radius: 10px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            color: #666;
        }

        .tab.active {
            background: white;
            color: #667eea;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        .form-section {
            padding: 0 20px;
            margin-bottom: 25px;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            font-size: 14px;
            color: #666;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .input-group input,
        .input-group select {
            width: 100%;
            padding: 16px;
            border: 2px solid #e5e7eb;
            border-radius: 12px;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .type-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 15px;
        }

        .type-button {
            padding: 16px;
            border: 2px solid #e5e7eb;
            border-radius: 12px;
            text-align: center;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            background: white;
        }

        .type-button.active {
            border-color: #667eea;
            background: #f8f9ff;
            color: #667eea;
        }

        .income-button.active {
            border-color: #10b981;
            background: #f0fdf4;
            color: #10b981;
        }

        .expense-button.active {
            border-color: #ef4444;
            background: #fef2f2;
            color: #ef4444;
        }

        .submit-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 18px;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .submit-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
        }

        .transactions-section {
            flex: 1;
            padding: 0 20px 20px;
            overflow-y: auto;
        }

        .transactions-section h3 {
            font-size: 18px;
            margin-bottom: 15px;
            color: #333;
        }

        .transaction-list {
            list-style: none;
        }

        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px;
            background: white;
            border-radius: 12px;
            margin-bottom: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            border-left: 4px solid;
        }

        .transaction-item.income {
            border-left-color: #10b981;
        }

        .transaction-item.expense {
            border-left-color: #ef4444;
        }

        .transaction-info {
            flex: 1;
        }

        .transaction-category {
            font-weight: 500;
            margin-bottom: 5px;
        }

        .transaction-date {
            font-size: 12px;
            color: #999;
        }

        .transaction-amount {
            font-weight: 600;
            font-size: 18px;
        }

        .income-amount {
            color: #10b981;
        }

        .expense-amount {
            color: #ef4444;
        }

        .no-transactions {
            text-align: center;
            padding: 40px 20px;
            color: #999;
        }

        .categories-section {
            padding: 0 20px 20px;
        }

        .category-list {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
        }

        .category-item {
            padding: 12px;
            background: #f8f9ff;
            border-radius: 12px;
            text-align: center;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
        }

        .category-item:hover {
            background: #667eea;
            color: white;
        }

        .category-item.active {
            background: #667eea;
            color: white;
            border-color: #764ba2;
        }

        .loading {
            text-align: center;
            padding: 40px;
            color: #667eea;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #10b981;
            color: white;
            padding: 16px 24px;
            border-radius: 12px;
            box-shadow: 0 8px 25px rgba(16, 185, 129, 0.4);
            transform: translateX(150%);
            transition: transform 0.3s;
            z-index: 1000;
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.error {
            background: #ef4444;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .transaction-item {
            animation: fadeIn 0.3s ease-out;
        }

        .month-selector {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
            margin-bottom: 15px;
        }

        .month-button {
            background: none;
            border: none;
            font-size: 20px;
            color: #667eea;
            cursor: pointer;
            padding: 5px 10px;
            border-radius: 8px;
            transition: background 0.3s;
        }

        .month-button:hover {
            background: #f8f9ff;
        }

        .current-month {
            font-weight: 500;
            color: #333;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <div class="header">
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

        <!-- Month Selector (hidden by default) -->
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
            Загрузка данных...
        </div>
    </div>

    <!-- Notification -->
    <div class="notification" id="notification"></div>

    <script>
        // Telegram WebApp API
        const tg = window.Telegram.WebApp;
        
        // Инициализация
        tg.ready();
        tg.expand();
        
        // Глобальные переменные
        let currentUserData = {
            balance: 0,
            transactions: [],
            categories: {},
            totalTransactions: 0
        };
        
        let currentTab = 'transactions';
        let transactionType = 'expense';
        
        // Категории с иконками
        const categories = [
            { id: 'еда', name: '🍕 Еда' },
            { id: 'транспорт', name: '🚗 Транспорт' },
            { id: 'развлечения', name: '🎬 Развлечения' },
            { id: 'покупки', name: '🛍️ Покупки' },
            { id: 'здоровье', name: '🏥 Здоровье' },
            { id: 'образование', name: '📚 Образование' },
            { id: 'квартира', name: '🏠 Квартира' },
            { id: 'зарплата', name: '💰 Зарплата' },
            { id: 'другое', name: '📌 Другое' }
        ];
        
        // Инициализация приложения
        document.addEventListener('DOMContentLoaded', function() {
            loadUserData();
            setupCategoryButtons();
        });
        
        // Загрузка данных пользователя
        function loadUserData() {
            showLoading(true);
            
            // Отправляем запрос на получение данных пользователя
            const data = {
                action: 'get_user_data'
            };
            
            tg.sendData(JSON.stringify(data));
            
            // В реальном приложении данные придут через Telegram WebApp
            // Для демо используем симуляцию
            setTimeout(() => {
                // Симуляция получения данных
                updateUIWithData();
                showLoading(false);
            }, 500);
        }
        
        // Обновление UI с данными
        function updateUIWithData() {
            // Обновляем баланс
            const balanceElement = document.getElementById('balance');
            balanceElement.textContent = `${currentUserData.balance} ₽`;
            
            if (currentUserData.balance > 0) {
                balanceElement.className = 'balance-amount balance-positive';
            } else if (currentUserData.balance < 0) {
                balanceElement.className = 'balance-amount balance-negative';
            } else {
                balanceElement.className = 'balance-amount';
            }
            
            // Рассчитываем доходы и расходы
            let income = 0;
            let expense = 0;
            
            currentUserData.transactions.forEach(transaction => {
                if (transaction.amount > 0) {
                    income += transaction.amount;
                } else {
                    expense += Math.abs(transaction.amount);
                }
            });
            
            // Обновляем статистику
            document.getElementById('total-income').textContent = `${income} ₽`;
            document.getElementById('total-expense').textContent = `${expense} ₽`;
            
            // Обновляем список транзакций
            updateTransactionList();
        }
        
        // Обновление списка транзакций
        function updateTransactionList() {
            const transactionList = document.getElementById('transactionList');
            const noTransactions = document.getElementById('noTransactions');
            
            if (currentUserData.transactions.length === 0) {
                noTransactions.style.display = 'block';
                transactionList.innerHTML = '<li class="no-transactions">Нет операций. Добавьте первую!</li>';
                return;
            }
            
            noTransactions.style.display = 'none';
            
            // Показываем последние 10 транзакций в обратном порядке
            const recentTransactions = [...currentUserData.transactions].reverse().slice(0, 10);
            
            let html = '';
            recentTransactions.forEach(transaction => {
                const isIncome = transaction.amount > 0;
                const amount = Math.abs(transaction.amount);
                const date = transaction.timestamp || new Date().toLocaleDateString('ru-RU');
                
                // Находим иконку категории
                const category = categories.find(cat => cat.id === transaction.category.toLowerCase());
                const categoryName = category ? category.name.split(' ')[1] : transaction.category;
                
                html += `
                    <li class="transaction-item ${isIncome ? 'income' : 'expense'}">
                        <div class="transaction-info">
                            <div class="transaction-category">${categoryName}</div>
                            <div class="transaction-date">${date}</div>
                        </div>
                        <div class="transaction-amount ${isIncome ? 'income-amount' : 'expense-amount'}">
                            ${isIncome ? '+' : '-'}${amount} ₽
                        </div>
                    </li>
                `;
            });
            
            transactionList.innerHTML = html;
        }
        
        // Переключение вкладок
        function switchTab(tabName) {
            currentTab = tabName;
            
            // Обновляем активные табы
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            document.querySelectorAll('.tab')[getTabIndex(tabName)].classList.add('active');
            
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
        
        function getTabIndex(tabName) {
            switch(tabName) {
                case 'transactions': return 0;
                case 'add': return 1;
                case 'categories': return 2;
                default: return 0;
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
                return;
            }
            
            // Подготавливаем данные для отправки
            const transactionData = {
                action: 'add_transaction',
                amount: amount,
                category: category,
                type: transactionType,
                date: new Date().toISOString()
            };
            
            // Отправляем данные в Telegram бот
            tg.sendData(JSON.stringify(transactionData));
            
            // Обновляем локальные данные (в реальном приложении обновим после ответа от бота)
            const finalAmount = transactionType === 'expense' ? -amount : amount;
            
            currentUserData.balance += finalAmount;
            currentUserData.transactions.push({
                amount: finalAmount,
                category: category,
                timestamp: new Date().toLocaleDateString('ru-RU', { 
                    day: '2-digit', 
                    month: '2-digit',
                    hour: '2-digit',
                    minute: '2-digit'
                })
            });
            currentUserData.totalTransactions++;
            
            // Обновляем статистику категорий
            if (!currentUserData.categories[category]) {
                currentUserData.categories[category] = 0;
            }
            currentUserData.categories[category] += finalAmount;
            
            // Обновляем UI
            updateUIWithData();
            
            // Показываем уведомление
            showNotification(`Операция добавлена: ${transactionType === 'expense' ? '-' : '+'}${amount} ₽`);
            
            // Очищаем форму
            amountInput.value = '';
            
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
                        ${category.name}
                    </div>
                `;
            });
            
            categoryList.innerHTML = html;
        }
        
        // Выбор категории при добавлении транзакции
        function selectCategory(categoryId) {
            document.getElementById('category').value = categoryId;
            switchTab('add');
        }
        
        // Изменение месяца (заглушка)
        function changeMonth(delta) {
            // В будущем можно реализовать фильтрацию по месяцам
            showNotification('Фильтрация по месяцам в разработке');
        }
        
        // Показать/скрыть индикатор загрузки
        function showLoading(show) {
            document.getElementById('loading').style.display = show ? 'block' : 'none';
        }
        
        // Показать уведомление
        function showNotification(message, isError = false) {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${isError ? 'error' : ''} show`;
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }
        
        // Для демонстрации: генерация тестовых данных
        function generateDemoData() {
            const demoTransactions = [
                { amount: 50000, category: 'зарплата', timestamp: '01.01 09:00' },
                { amount: -1500, category: 'еда', timestamp: '02.01 12:30' },
                { amount: -500, category: 'транспорт', timestamp: '03.01 08:15' },
                { amount: -3000, category: 'покупки', timestamp: '04.01 16:45' },
                { amount: -1200, category: 'развлечения', timestamp: '05.01 20:00' }
            ];
            
            currentUserData.transactions = demoTransactions;
            currentUserData.balance = demoTransactions.reduce((sum, t) => sum + t.amount, 0);
            currentUserData.totalTransactions = demoTransactions.length;
            
            // Создаем категории из транзакций
            demoTransactions.forEach(t => {
                if (!currentUserData.categories[t.category]) {
                    currentUserData.categories[t.category] = 0;
                }
                currentUserData.categories[t.category] += t.amount;
            });
        }
        
        // Если приложение открыто не через Telegram, используем демо-данные
        if (!window.Telegram?.WebApp?.initData) {
            console.log('Приложение открыто не в Telegram, используем демо-режим');
            generateDemoData();
            updateUIWithData();
        }
    </script>
</body>
</html>
