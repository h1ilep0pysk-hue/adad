<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CoinKeeper - Финансовый помощник</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 100%;
        }
        
        .header {
            text-align: center;
            margin-bottom: 25px;
            padding: 15px;
        }
        
        .header h1 {
            font-size: 28px;
            margin-bottom: 5px;
        }
        
        .header p {
            opacity: 0.8;
            font-size: 14px;
        }
        
        .balance-card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .balance-title {
            font-size: 14px;
            opacity: 0.8;
            margin-bottom: 5px;
        }
        
        .balance-amount {
            font-size: 36px;
            font-weight: bold;
            margin: 15px 0;
        }
        
        .balance-stats {
            font-size: 16px;
            opacity: 0.9;
        }
        
        .quick-actions {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .action-btn {
            background: white;
            color: #667eea;
            border: none;
            padding: 18px;
            border-radius: 15px;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transition: transform 0.2s;
        }
        
        .action-btn:active {
            transform: scale(0.95);
        }
        
        .action-btn.income {
            background: #4CAF50;
            color: white;
        }
        
        .action-btn.expense {
            background: #FF5252;
            color: white;
        }
        
        .action-btn .icon {
            font-size: 24px;
            margin-bottom: 5px;
        }
        
        .section {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 15px;
        }
        
        .section-title {
            font-size: 18px;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-info {
            flex: 1;
        }
        
        .transaction-info h4 {
            margin: 0 0 5px 0;
            font-size: 16px;
        }
        
        .transaction-date {
            font-size: 12px;
            opacity: 0.7;
        }
        
        .transaction-amount {
            font-size: 18px;
            font-weight: bold;
        }
        
        .income-text {
            color: #4CAF50;
        }
        
        .expense-text {
            color: #FF5252;
        }
        
        .empty-state {
            text-align: center;
            padding: 40px 0;
            opacity: 0.7;
            font-size: 14px;
        }
        
        .categories-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-top: 10px;
        }
        
        .category-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }
        
        .category-name {
            font-size: 14px;
            margin-bottom: 5px;
        }
        
        .category-amount {
            font-size: 16px;
            font-weight: bold;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 15px;
        }
        
        .stat-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 20px;
            font-weight: bold;
            margin: 5px 0;
        }
        
        .stat-label {
            font-size: 12px;
            opacity: 0.8;
        }
        
        .loading {
            text-align: center;
            padding: 50px;
            font-size: 16px;
        }
        
        .error {
            text-align: center;
            padding: 50px;
            color: #FF5252;
        }
        
        .hidden {
            display: none;
        }
        
        /* Категории для выбора */
        .categories-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        
        .categories-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 20px;
            padding: 25px;
            width: 90%;
            max-width: 400px;
            max-height: 80vh;
            overflow-y: auto;
        }
        
        .categories-title {
            font-size: 20px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .category-option {
            background: rgba(255, 255, 255, 0.15);
            padding: 15px;
            margin: 10px 0;
            border-radius: 10px;
            text-align: center;
            cursor: pointer;
            transition: background 0.2s;
        }
        
        .category-option:hover {
            background: rgba(255, 255, 255, 0.25);
        }
        
        .close-modal {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.2);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-size: 20px;
        }
        
        /* Форма ввода суммы */
        .input-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        
        .input-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 20px;
            padding: 30px;
            width: 90%;
            max-width: 350px;
        }
        
        .input-title {
            font-size: 20px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .input-field {
            width: 100%;
            padding: 15px;
            font-size: 24px;
            text-align: center;
            border: 2px solid rgba(255, 255, 255, 0.3);
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border-radius: 10px;
            margin-bottom: 20px;
        }
        
        .input-field:focus {
            outline: none;
            border-color: white;
        }
        
        .input-buttons {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .num-btn {
            padding: 15px;
            font-size: 18px;
            background: rgba(255, 255, 255, 0.15);
            border: none;
            color: white;
            border-radius: 10px;
            cursor: pointer;
        }
        
        .submit-btn {
            width: 100%;
            padding: 15px;
            background: white;
            color: #667eea;
            border: none;
            border-radius: 10px;
            font-weight: bold;
            font-size: 18px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container" id="app">
        <!-- Загрузка -->
        <div class="loading" id="loading">
            Загрузка данных...
        </div>
        
        <!-- Основное приложение -->
        <div class="hidden" id="mainApp">
            <div class="header">
                <h1>CoinKeeper</h1>
                <p>Ваш финансовый помощник</p>
            </div>
            
            <div class="balance-card">
                <div class="balance-title">Текущий баланс</div>
                <div class="balance-amount" id="balanceAmount">0 ₽</div>
                <div class="balance-stats">
                    <span id="transactionCount">0 операций</span>
                </div>
            </div>
            
            <div class="quick-actions">
                <button class="action-btn income" onclick="showIncomeCategories()">
                    <div class="icon">+</div>
                    <div>Доход</div>
                </button>
                <button class="action-btn expense" onclick="showExpenseCategories()">
                    <div class="icon">-</div>
                    <div>Расход</div>
                </button>
            </div>
            
            <div class="section">
                <div class="section-title">
                    <span>Последние операции</span>
                    <span style="font-size: 14px; opacity: 0.8;" id="lastUpdate"></span>
                </div>
                <div id="transactionsList">
                    <!-- Транзакции будут здесь -->
                </div>
            </div>
            
            <div class="section">
                <div class="section-title">Статистика</div>
                <div class="stats-grid">
                    <div class="stat-item">
                        <div class="stat-label">Доходы</div>
                        <div class="stat-value income-text" id="totalIncome">0 ₽</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">Расходы</div>
                        <div class="stat-value expense-text" id="totalExpense">0 ₽</div>
                    </div>
                </div>
            </div>
            
            <div class="section">
                <div class="section-title">Категории расходов</div>
                <div class="categories-grid" id="categoriesList">
                    <!-- Категории будут здесь -->
                </div>
            </div>
        </div>
        
        <!-- Ошибка -->
        <div class="error hidden" id="errorMessage">
            Ошибка загрузки данных
        </div>
        
        <!-- Модальное окно выбора категории -->
        <div class="categories-modal hidden" id="categoriesModal">
            <div class="categories-content">
                <div class="close-modal" onclick="closeModal()">×</div>
                <div class="categories-title" id="modalTitle">Выберите категорию</div>
                <div id="categoriesOptions">
                    <!-- Категории будут здесь -->
                </div>
            </div>
        </div>
        
        <!-- Модальное окно ввода суммы -->
        <div class="input-modal hidden" id="inputModal">
            <div class="input-content">
                <div class="close-modal" onclick="closeInputModal()">×</div>
                <div class="input-title" id="inputTitle">Введите сумму</div>
                <input type="text" class="input-field" id="amountInput" placeholder="0" inputmode="numeric">
                <div class="input-buttons">
                    <button class="num-btn" onclick="addNumber('1')">1</button>
                    <button class="num-btn" onclick="addNumber('2')">2</button>
                    <button class="num-btn" onclick="addNumber('3')">3</button>
                    <button class="num-btn" onclick="addNumber('4')">4</button>
                    <button class="num-btn" onclick="addNumber('5')">5</button>
                    <button class="num-btn" onclick="addNumber('6')">6</button>
                    <button class="num-btn" onclick="addNumber('7')">7</button>
                    <button class="num-btn" onclick="addNumber('8')">8</button>
                    <button class="num-btn" onclick="addNumber('9')">9</button>
                    <button class="num-btn" onclick="addNumber('00')">00</button>
                    <button class="num-btn" onclick="addNumber('0')">0</button>
                    <button class="num-btn" onclick="clearInput()">C</button>
                </div>
                <button class="submit-btn" onclick="submitTransaction()">Добавить</button>
            </div>
        </div>
    </div>

    <script>
        // Глобальные переменные
        let currentUser = null;
        let currentType = null; // 'income' или 'expense'
        let selectedCategory = null;
        let userData = null;
        
        // Категории
        const incomeCategories = [
            { icon: "💰", name: "Зарплата" },
            { icon: "💻", name: "Фриланс" },
            { icon: "📈", name: "Инвестиции" },
            { icon: "🎁", name: "Подарок" },
            { icon: "📊", name: "Другое" }
        ];
        
        const expenseCategories = [
            { icon: "🍔", name: "Еда" },
            { icon: "🚗", name: "Транспорт" },
            { icon: "🏠", name: "Жилье" },
            { icon: "🎮", name: "Развлечения" },
            { icon: "💊", name: "Здоровье" },
            { icon: "👕", name: "Одежда" },
            { icon: "📚", name: "Образование" },
            { icon: "🎁", name: "Другое" }
        ];
        
        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', function() {
            initTelegramWebApp();
            loadUserData();
        });
        
        // Инициализация Telegram WebApp
        function initTelegramWebApp() {
            if (window.Telegram && Telegram.WebApp) {
                Telegram.WebApp.ready();
                Telegram.WebApp.expand();
                Telegram.WebApp.setHeaderColor('#667eea');
                Telegram.WebApp.setBackgroundColor('#667eea');
                
                // Получаем данные пользователя из Telegram
                const user = Telegram.WebApp.initDataUnsafe.user;
                if (user) {
                    currentUser = user.id;
                    console.log('User ID:', currentUser);
                }
            } else {
                // Для отладки вне Telegram
                currentUser = 'test_user_' + Math.floor(Math.random() * 1000);
                console.log('Debug mode, user:', currentUser);
            }
        }
        
        // Загрузка данных пользователя
        async function loadUserData() {
            try {
                if (!currentUser) {
                    showError('Пользователь не определен');
                    return;
                }
                
                // Здесь будет запрос к вашему боту через API
                // Пока используем мок-данные для демонстрации
                await simulateDataLoading();
                
                // После получения данных скрываем загрузку
                document.getElementById('loading').classList.add('hidden');
                document.getElementById('mainApp').classList.remove('hidden');
                
                // Обновляем UI с данными
                updateUI();
                
            } catch (error) {
                console.error('Error loading data:', error);
                showError('Ошибка загрузки данных');
            }
        }
        
        // Симуляция загрузки данных (замените на реальный API запрос)
        async function simulateDataLoading() {
            return new Promise(resolve => {
                setTimeout(() => {
                    // Мок-данные для демонстрации
                    userData = {
                        balance: 15000,
                        transactions: [
                            { amount: 30000, category: "💰 Зарплата", date: "15.12 10:30", type: "income" },
                            { amount: -1500, category: "🍔 Еда", date: "15.12 13:45", type: "expense" },
                            { amount: -500, category: "🚗 Транспорт", date: "15.12 18:20", type: "expense" },
                            { amount: -3000, category: "🎮 Развлечения", date: "14.12 20:15", type: "expense" },
                            { amount: 5000, category: "💻 Фриланс", date: "13.12 16:00", type: "income" }
                        ],
                        categories: {
                            "💰 Зарплата": 30000,
                            "💻 Фриланс": 5000,
                            "🍔 Еда": 1500,
                            "🚗 Транспорт": 500,
                            "🎮 Развлечения": 3000
                        }
                    };
                    resolve();
                }, 1000);
            });
        }
        
        // Обновление интерфейса
        function updateUI() {
            if (!userData) return;
            
            // Баланс
            document.getElementById('balanceAmount').textContent = 
                formatCurrency(userData.balance);
            document.getElementById('balanceAmount').className = 
                `balance-amount ${userData.balance >= 0 ? 'income-text' : 'expense-text'}`;
            
            // Количество операций
            const transactionCount = userData.transactions.length;
            document.getElementById('transactionCount').textContent = 
                `${transactionCount} ${getWordForm(transactionCount, ['операция', 'операции', 'операций'])}`;
            
            // Доходы и расходы
            const totalIncome = userData.transactions
                .filter(t => t.type === 'income')
                .reduce((sum, t) => sum + t.amount, 0);
            const totalExpense = Math.abs(userData.transactions
                .filter(t => t.type === 'expense')
                .reduce((sum, t) => sum + t.amount, 0));
            
            document.getElementById('totalIncome').textContent = formatCurrency(totalIncome);
            document.getElementById('totalExpense').textContent = formatCurrency(totalExpense);
            
            // Список транзакций
            const transactionsList = document.getElementById('transactionsList');
            transactionsList.innerHTML = '';
            
            if (userData.transactions.length === 0) {
                transactionsList.innerHTML = '<div class="empty-state">Нет операций</div>';
            } else {
                userData.transactions.slice(0, 5).forEach(transaction => {
                    const item = document.createElement('div');
                    item.className = 'transaction-item';
                    item.innerHTML = `
                        <div class="transaction-info">
                            <h4>${transaction.category}</h4>
                            <div class="transaction-date">${transaction.date}</div>
                        </div>
                        <div class="transaction-amount ${transaction.type === 'income' ? 'income-text' : 'expense-text'}">
                            ${transaction.type === 'income' ? '+' : '-'}${formatCurrency(Math.abs(transaction.amount))}
                        </div>
                    `;
                    transactionsList.appendChild(item);
                });
            }
            
            // Категории расходов
            const categoriesList = document.getElementById('categoriesList');
            categoriesList.innerHTML = '';
            
            const expenseCats = Object.entries(userData.categories || {})
                .filter(([cat, amount]) => amount < 0)
                .sort((a, b) => Math.abs(b[1]) - Math.abs(a[1]))
                .slice(0, 4);
            
            if (expenseCats.length === 0) {
                categoriesList.innerHTML = '<div class="empty-state" style="grid-column: span 2;">Нет расходов</div>';
            } else {
                expenseCats.forEach(([category, amount]) => {
                    const item = document.createElement('div');
                    item.className = 'category-item';
                    item.innerHTML = `
                        <div class="category-name">${category}</div>
                        <div class="category-amount expense-text">${formatCurrency(Math.abs(amount))}</div>
                    `;
                    categoriesList.appendChild(item);
                });
            }
            
            // Время обновления
            document.getElementById('lastUpdate').textContent = 
                `Обновлено: ${new Date().toLocaleTimeString('ru-RU', { hour: '2-digit', minute: '2-digit' })}`;
        }
        
        // Показать категории доходов
        function showIncomeCategories() {
            currentType = 'income';
            document.getElementById('modalTitle').textContent = 'Выберите категорию дохода';
            showCategoriesModal(incomeCategories);
        }
        
        // Показать категории расходов
        function showExpenseCategories() {
            currentType = 'expense';
            document.getElementById('modalTitle').textContent = 'Выберите категорию расхода';
            showCategoriesModal(expenseCategories);
        }
        
        // Показать модальное окно с категориями
        function showCategoriesModal(categories) {
            const optionsContainer = document.getElementById('categoriesOptions');
            optionsContainer.innerHTML = '';
            
            categories.forEach(category => {
                const option = document.createElement('div');
                option.className = 'category-option';
                option.innerHTML = `
                    <div style="font-size: 24px; margin-bottom: 5px;">${category.icon}</div>
                    <div>${category.name}</div>
                `;
                option.onclick = () => selectCategory(category);
                optionsContainer.appendChild(option);
            });
            
            document.getElementById('categoriesModal').classList.remove('hidden');
        }
        
        // Выбор категории
        function selectCategory(category) {
            selectedCategory = category;
            closeModal();
            showInputModal();
        }
        
        // Закрыть модальное окно
        function closeModal() {
            document.getElementById('categoriesModal').classList.add('hidden');
        }
        
        // Показать модальное окно ввода суммы
        function showInputModal() {
            if (!selectedCategory) return;
            
            document.getElementById('inputTitle').textContent = 
                `Сумма для: ${selectedCategory.icon} ${selectedCategory.name}`;
            document.getElementById('amountInput').value = '';
            document.getElementById('inputModal').classList.remove('hidden');
        }
        
        // Закрыть модальное окно ввода
        function closeInputModal() {
            document.getElementById('inputModal').classList.add('hidden');
            selectedCategory = null;
        }
        
        // Добавить цифру в поле ввода
        function addNumber(num) {
            const input = document.getElementById('amountInput');
            if (input.value === '0') {
                input.value = num;
            } else {
                input.value += num;
            }
        }
        
        // Очистить поле ввода
        function clearInput() {
            document.getElementById('amountInput').value = '0';
        }
        
        // Отправить транзакцию
        async function submitTransaction() {
            const input = document.getElementById('amountInput');
            const amount = parseInt(input.value);
            
            if (!amount || amount <= 0) {
                alert('Введите корректную сумму');
                return;
            }
            
            if (!selectedCategory || !currentType) {
                alert('Ошибка выбора категории');
                return;
            }
            
            try {
                // Показываем загрузку
                document.getElementById('loading').classList.remove('hidden');
                document.getElementById('mainApp').classList.add('hidden');
                
                // Здесь будет отправка данных на сервер
                // Временная симуляция
                await simulateTransactionSubmit(amount);
                
                // Закрываем модальное окно
                closeInputModal();
                
                // Перезагружаем данные
                await loadUserData();
                
            } catch (error) {
                console.error('Error submitting transaction:', error);
                alert('Ошибка при добавлении операции');
            }
        }
        
        // Симуляция отправки транзакции (замените на реальный API)
        async function simulateTransactionSubmit(amount) {
            return new Promise(resolve => {
                setTimeout(() => {
                    // Добавляем транзакцию в мок-данные
                    const sign = currentType === 'income' ? 1 : -1;
                    const transaction = {
                        amount: sign * amount,
                        category: `${selectedCategory.icon} ${selectedCategory.name}`,
                        date: new Date().toLocaleString('ru-RU', { 
                            day: '2-digit', 
                            month: '2-digit',
                            hour: '2-digit',
                            minute: '2-digit'
                        }),
                        type: currentType
                    };
                    
                    userData.transactions.unshift(transaction);
                    userData.balance += transaction.amount;
                    
                    // Обновляем категории
                    const catKey = transaction.category;
                    if (!userData.categories[catKey]) {
                        userData.categories[catKey] = 0;
                    }
                    userData.categories[catKey] += transaction.amount;
                    
                    resolve();
                }, 500);
            });
        }
        
        // Вспомогательные функции
        function formatCurrency(amount) {
            return amount.toLocaleString('ru-RU') + ' ₽';
        }
        
        function getWordForm(number, forms) {
            const n = Math.abs(number) % 100;
            const n1 = n % 10;
            if (n > 10 && n < 20) return forms[2];
            if (n1 > 1 && n1 < 5) return forms[1];
            if (n1 === 1) return forms[0];
            return forms[2];
        }
        
        function showError(message) {
            document.getElementById('loading').classList.add('hidden');
            document.getElementById('mainApp').classList.add('hidden');
            document.getElementById('errorMessage').textContent = message;
            document.getElementById('errorMessage').classList.remove('hidden');
        }
        
        // Для отладки: обновление каждые 30 секунд
        setInterval(() => {
            if (userData) {
                updateUI();
            }
        }, 30000);
    </script>
</body>
</html>
