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
        
        .balance-card {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            text-align: center;
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
    </style>
</head>
<body>
    <div class="container">
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
                <button class="action-btn income" onclick="sendData('add_income')">
                    <div class="icon">+</div>
                    <div>Добавить доход</div>
                </button>
                <button class="action-btn expense" onclick="sendData('add_expense')">
                    <div class="icon">-</div>
                    <div>Добавить расход</div>
                </button>
            </div>
            
            <div class="section">
                <div class="section-title">Последние операции</div>
                <div id="transactionsList">
                    <div class="empty-state">Нет операций</div>
                </div>
            </div>
        </div>
        
        <!-- Ошибка -->
        <div class="error hidden" id="errorMessage">
            Ошибка загрузки данных
        </div>
    </div>

    <script>
        // Инициализация Telegram WebApp
        if (window.Telegram && Telegram.WebApp) {
            Telegram.WebApp.ready();
            Telegram.WebApp.expand();
            
            // Загружаем данные пользователя
            loadUserData();
        } else {
            document.getElementById('loading').style.display = 'none';
            document.getElementById('errorMessage').textContent = 'Откройте это приложение в Telegram';
            document.getElementById('errorMessage').classList.remove('hidden');
        }
        
        // Загрузка данных пользователя
        function loadUserData() {
            // В реальном приложении здесь будет запрос к боту
            // Пока используем мок-данные
            setTimeout(() => {
                document.getElementById('loading').classList.add('hidden');
                document.getElementById('mainApp').classList.remove('hidden');
                
                // Устанавливаем начальные данные
                document.getElementById('balanceAmount').textContent = '0 ₽';
                document.getElementById('transactionCount').textContent = '0 операций';
            }, 1000);
        }
        
        // Отправка данных боту
        function sendData(action) {
            if (window.Telegram && Telegram.WebApp) {
                const data = {
                    action: action,
                    timestamp: new Date().toISOString()
                };
                
                Telegram.WebApp.sendData(JSON.stringify(data));
                
                // Показываем сообщение
                if (action === 'add_income') {
                    alert('Используйте команду в боте: /income или напишите +сумма категория');
                } else if (action === 'add_expense') {
                    alert('Используйте команду в боте: напишите -сумма категория');
                }
            } else {
                alert('Для работы с ботом откройте это приложение в Telegram');
            }
        }
        
        // Обновление данных
        function updateUI(data) {
            if (data.balance !== undefined) {
                document.getElementById('balanceAmount').textContent = data.balance + ' ₽';
                document.getElementById('balanceAmount').className = 
                    `balance-amount ${data.balance >= 0 ? 'income-text' : 'expense-text'}`;
            }
            
            if (data.total_transactions !== undefined) {
                document.getElementById('transactionCount').textContent = 
                    data.total_transactions + ' операций';
            }
            
            if (data.transactions && data.transactions.length > 0) {
                const transactionsList = document.getElementById('transactionsList');
                transactionsList.innerHTML = '';
                
                data.transactions.forEach(transaction => {
                    const item = document.createElement('div');
                    item.className = 'transaction-item';
                    item.innerHTML = `
                        <div class="transaction-info">
                            <h4>${transaction.category}</h4>
                            <div class="transaction-date">${transaction.timestamp}</div>
                        </div>
                        <div class="transaction-amount ${transaction.amount >= 0 ? 'income-text' : 'expense-text'}">
                            ${transaction.amount >= 0 ? '+' : ''}${transaction.amount} ₽
                        </div>
                    `;
                    transactionsList.appendChild(item);
                });
            }
        }
    </script>
</body>
</html>
