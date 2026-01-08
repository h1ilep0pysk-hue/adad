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
            -webkit-tap-highlight-color: transparent;
        }

        html, body {
            height: 100%;
            overflow: hidden;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        body {
            padding: 0;
            margin: 0;
            color: #333;
            position: relative;
            touch-action: pan-y;
        }

        .app-container {
            width: 100%;
            height: 100%;
            max-width: 450px;
            margin: 0 auto;
            background: white;
            box-shadow: 0 0 40px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
            position: relative;
            overflow-y: auto;
            overflow-x: hidden;
            scroll-behavior: smooth;
            -webkit-overflow-scrolling: touch;
        }

        /* Стили для скроллбара */
        .app-container::-webkit-scrollbar {
            width: 8px;
        }

        .app-container::-webkit-scrollbar-track {
            background: #f1f1f1;
        }

        .app-container::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 4px;
        }

        .app-container::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
        }

        /* Для Firefox */
        .app-container {
            scrollbar-width: thin;
            scrollbar-color: #667eea #f1f1f1;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
            flex-shrink: 0;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
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

        .content-wrapper {
            flex: 1;
            padding-bottom: 20px;
            min-height: calc(100vh - 80px);
        }

        .balance-section {
            padding: 30px 20px;
            text-align: center;
            background: #f8f9ff;
            margin: 20px;
            border-radius: 25px;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.15);
            position: relative;
            overflow: hidden;
        }

        .balance-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 5px;
            background: linear-gradient(90deg, #667eea, #764ba2);
        }

        .balance-label {
            font-size: 14px;
            color: #666;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
        }

        .balance-amount {
            font-size: 52px;
            font-weight: 700;
            color: #333;
            line-height: 1.2;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            margin: 10px 0;
        }

        .balance-positive {
            color: #10b981;
        }

        .balance-negative {
            color: #ef4444;
        }

        .balance-zero {
            color: #667eea;
        }

        .stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            padding: 0 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 25px 20px;
            border-radius: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.08);
            text-align: center;
            border: 2px solid transparent;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.12);
        }

        .stat-card.income {
            border-color: rgba(16, 185, 129, 0.2);
        }

        .stat-card.expense {
            border-color: rgba(239, 68, 68, 0.2);
        }

        .stat-value {
            font-size: 32px;
            font-weight: 700;
            margin-bottom: 8px;
            transition: transform 0.3s;
        }

        .stat-card:hover .stat-value {
            transform: scale(1.05);
        }

        .stat-label {
            font-size: 13px;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            font-weight: 600;
        }

        .tabs-container {
            background: #f8f9ff;
            margin: 0 20px 30px;
            border-radius: 20px;
            padding: 10px;
            position: sticky;
            top: 180px;
            z-index: 90;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        }

        .tabs {
            display: flex;
            background: rgba(255,255,255,0.5);
            border-radius: 15px;
            padding: 8px;
            gap: 8px;
        }

        .tab {
            flex: 1;
            text-align: center;
            padding: 18px 10px;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            color: #666;
            font-size: 15px;
            border: 2px solid transparent;
            background: transparent;
            white-space: nowrap;
        }

        .tab.active {
            background: white;
            color: #667eea;
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.25);
            border-color: #667eea;
            transform: scale(1.02);
        }

        .tab:hover:not(.active) {
            background: rgba(255,255,255,0.8);
            color: #667eea;
            transform: translateY(-2px);
        }

        .section-content {
            padding: 0 20px;
            animation: fadeIn 0.4s ease-out;
        }

        .form-section {
            padding: 30px 20px;
            background: white;
            border-radius: 25px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
        }

        .input-group {
            margin-bottom: 25px;
        }

        .input-group label {
            display: block;
            font-size: 15px;
            color: #555;
            margin-bottom: 12px;
            font-weight: 600;
        }

        .input-group input,
        .input-group select {
            width: 100%;
            padding: 20px;
            border: 2px solid #e5e7eb;
            border-radius: 15px;
            font-size: 17px;
            transition: all 0.3s;
            background: white;
            color: #333;
        }

        .input-group input:focus,
        .input-group select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 4px rgba(102, 126, 234, 0.15);
        }

        .type-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 25px;
        }

        .type-button {
            padding: 20px;
            border: 3px solid #e5e7eb;
            border-radius: 15px;
            text-align: center;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            background: white;
            font-size: 17px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .type-button.active {
            border-color: transparent;
            color: white;
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
            transform: scale(1.02);
        }

        .expense-button.active {
            background: linear-gradient(135deg, #ef4444 0%, #f87171 100%);
        }

        .income-button.active {
            background: linear-gradient(135deg, #10b981 0%, #34d399 100%);
        }

        .submit-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 22px;
            border-radius: 15px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .submit-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(102, 126, 234, 0.5);
        }

        .submit-button:active {
            transform: translateY(0);
        }

        .transactions-section {
            padding: 30px 0;
        }

        .section-title {
            font-size: 20px;
            margin-bottom: 25px;
            color: #333;
            font-weight: 700;
            padding-left: 5px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-title::before {
            content: '';
            width: 4px;
            height: 24px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 2px;
        }

        .transaction-list {
            list-style: none;
            max-height: 500px;
            overflow-y: auto;
            padding-right: 10px;
        }

        .transaction-list::-webkit-scrollbar {
            width: 6px;
        }

        .transaction-list::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 3px;
        }

        .transaction-list::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 3px;
        }

        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 22px;
            background: white;
            border-radius: 18px;
            margin-bottom: 15px;
            box-shadow: 0 6px 20px rgba(0,0,0,0.06);
            border-left: 6px solid;
            transition: all 0.3s;
            cursor: pointer;
            animation: slideIn 0.3s ease-out;
            position: relative;
            overflow: hidden;
        }

        .transaction-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transform: translateX(-100%);
            transition: transform 0.6s;
        }

        .transaction-item:hover::before {
            transform: translateX(100%);
        }

        .transaction-item:hover {
            transform: translateX(8px);
            box-shadow: 0 12px 30px rgba(0,0,0,0.1);
        }

        .transaction-item.income {
            border-left-color: #10b981;
            background: linear-gradient(to right, #f0fdf4 0%, white 100%);
        }

        .transaction-item.expense {
            border-left-color: #ef4444;
            background: linear-gradient(to right, #fef2f2 0%, white 100%);
        }

        .transaction-info {
            flex: 1;
            min-width: 0;
        }

        .transaction-category {
            font-weight: 700;
            margin-bottom: 8px;
            font-size: 17px;
            color: #333;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .transaction-date {
            font-size: 14px;
            color: #888;
            font-weight: 500;
        }

        .transaction-amount {
            font-weight: 800;
            font-size: 22px;
            min-width: fit-content;
            margin-left: 15px;
            padding: 8px 16px;
            border-radius: 12px;
            background: rgba(255,255,255,0.9);
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .income-amount {
            color: #10b981;
            background: rgba(16, 185, 129, 0.1);
        }

        .expense-amount {
            color: #ef4444;
            background: rgba(239, 68, 68, 0.1);
        }

        .no-transactions {
            text-align: center;
            padding: 80px 20px;
            color: #999;
            font-size: 17px;
            background: #f9fafb;
            border-radius: 20px;
            margin-top: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
        }

        .no-transactions::before {
            content: '📊';
            font-size: 60px;
            opacity: 0.5;
        }

        .categories-section {
            padding: 30px 0;
        }

        .category-list {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
        }

        .category-item {
            padding: 25px 15px;
            background: white;
            border-radius: 18px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 2px solid transparent;
            box-shadow: 0 6px 20px rgba(0,0,0,0.06);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 120px;
            position: relative;
            overflow: hidden;
        }

        .category-item::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, #667eea, #764ba2);
            transform: translateY(-100%);
            transition: transform 0.3s;
        }

        .category-item:hover::after {
            transform: translateY(0);
        }

        .category-item:hover {
            transform: translateY(-5px) scale(1.03);
            box-shadow: 0 15px 35px rgba(102, 126, 234, 0.2);
            border-color: #667eea;
        }

        .category-item.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-color: #764ba2;
            transform: translateY(-5px) scale(1.03);
            box-shadow: 0 20px 40px rgba(102, 126, 234, 0.4);
        }

        .category-icon {
            font-size: 32px;
            margin-bottom: 12px;
            transition: transform 0.3s;
        }

        .category-item:hover .category-icon {
            transform: scale(1.2);
        }

        .category-name {
            font-weight: 600;
            font-size: 15px;
            transition: transform 0.3s;
        }

        .loading {
            text-align: center;
            padding: 100px 20px;
            color: #667eea;
            font-size: 18px;
            font-weight: 600;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 25px;
        }

        .loading::after {
            content: '';
            width: 50px;
            height: 50px;
            border: 4px solid #f3f3f3;
            border-top: 4px solid #667eea;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        .notification {
            position: fixed;
            top: 30px;
            right: 30px;
            background: linear-gradient(135deg, #10b981 0%, #34d399 100%);
            color: white;
            padding: 22px 28px;
            border-radius: 18px;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.4);
            transform: translateX(150%) translateY(0);
            transition: transform 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            z-index: 1000;
            max-width: 350px;
            font-weight: 600;
            font-size: 16px;
            line-height: 1.5;
        }

        .notification.show {
            transform: translateX(0) translateY(0);
        }

        .notification.error {
            background: linear-gradient(135deg, #ef4444 0%, #f87171 100%);
            box-shadow: 0 15px 40px rgba(239, 68, 68, 0.4);
        }

        .sync-button {
            position: absolute;
            top: 25px;
            right: 25px;
            background: rgba(255,255,255,0.25);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            transition: all 0.3s;
            z-index: 101;
        }

        .sync-button:hover {
            background: rgba(255,255,255,0.35);
            transform: rotate(180deg) scale(1.1);
            box-shadow: 0 0 20px rgba(255,255,255,0.3);
        }

        .sync-button:active {
            transform: rotate(180deg) scale(0.95);
        }

        .scroll-hint {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            color: rgba(255,255,255,0.7);
            font-size: 14px;
            animation: bounce 2s infinite;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }

        .scroll-hint span {
            font-size: 20px;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(-30px); }
            to { opacity: 1; transform: translateX(0); }
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @keyframes bounce {
            0%, 100% { transform: translateX(-50%) translateY(0); }
            50% { transform: translateX(-50%) translateY(-10px); }
        }

        /* Анимации появления */
        .balance-section, .stats, .tabs-container {
            animation: fadeIn 0.6s ease-out;
        }

        /* Мобильная оптимизация */
        @media (max-width: 480px) {
            .app-container {
                max-width: 100%;
                border-radius: 0;
            }
            
            .balance-amount {
                font-size: 46px;
            }
            
            .stat-value {
                font-size: 28px;
            }
            
            .category-list {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .tab {
                padding: 16px 8px;
                font-size: 14px;
            }
            
            .type-button {
                padding: 18px;
                font-size: 16px;
            }
            
            .transaction-item {
                padding: 20px;
            }
            
            .transaction-amount {
                font-size: 20px;
            }
        }

        @media (max-width: 380px) {
            .category-list {
                grid-template-columns: 1fr;
            }
            
            .tabs {
                flex-direction: column;
            }
        }

        /* Эффект параллакса для глубины */
        .header {
            transform: translateZ(0);
        }

        .balance-section {
            transform: translateZ(10px);
        }

        .stats {
            transform: translateZ(5px);
        }

        /* Плавное появление контента при скролле */
        .section-content {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s ease, transform 0.6s ease;
        }

        .section-content.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* Индикатор скролла */
        .scroll-progress {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(90deg, #667eea, #764ba2);
            transform-origin: 0%;
            transform: scaleX(0);
            z-index: 1000;
            transition: transform 0.1s;
        }

        /* Улучшенный фокус для доступности */
        *:focus {
            outline: 3px solid #667eea;
            outline-offset: 2px;
        }

        /* Анимация пульсации для баланса */
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        .balance-updated {
            animation: pulse 0.5s ease;
        }
    </style>
</head>
<body>
    <!-- Индикатор скролла -->
    <div class="scroll-progress" id="scrollProgress"></div>

    <!-- Подсказка скролла (только на десктопе) -->
    <div class="scroll-hint" id="scrollHint">
        <span>↓</span>
        <span>Крутите колесико мыши</span>
    </div>

    <div class="app-container" id="appContainer">
        <!-- Header -->
        <div class="header">
            <button class="sync-button" onclick="syncWithBot()" title="Синхронизировать">
                🔄
            </button>
            <h1>CoinKeeper</h1>
            <div class="subtitle">Учет расходов и доходов</div>
        </div>

        <div class="content-wrapper">
            <!-- Balance Section -->
            <div class="balance-section">
                <div class="balance-label">ТЕКУЩИЙ БАЛАНС</div>
                <div class="balance-amount" id="balance">0 ₽</div>
            </div>

            <!-- Stats -->
            <div class="stats">
                <div class="stat-card income" onclick="switchTab('transactions')">
                    <div class="stat-value income" id="total-income">0 ₽</div>
                    <div class="stat-label">ДОХОДЫ</div>
                </div>
                <div class="stat-card expense" onclick="switchTab('transactions')">
                    <div class="stat-value expense" id="total-expense">0 ₽</div>
                    <div class="stat-label">РАСХОДЫ</div>
                </div>
            </div>

            <!-- Tabs -->
            <div class="tabs-container">
                <div class="tabs">
                    <button class="tab active" onclick="switchTab('transactions')">
                        📋 Транзакции
                    </button>
                    <button class="tab" onclick="switchTab('add')">
                        ➕ Добавить
                    </button>
                    <button class="tab" onclick="switchTab('categories')">
                        🏷️ Категории
                    </button>
                </div>
            </div>

            <!-- Transactions Section -->
            <div class="section-content visible" id="transactionsContent">
                <div class="transactions-section">
                    <div class="section-title">Последние операции</div>
                    <ul class="transaction-list" id="transactionList">
                        <li class="no-transactions" id="noTransactions">
                            Нет операций. Добавьте первую!
                        </li>
                    </ul>
                </div>
            </div>

            <!-- Add Transaction Form -->
            <div class="section-content" id="addContent" style="display: none;">
                <div class="form-section">
                    <div class="type-buttons">
                        <button class="type-button expense-button active" onclick="setTransactionType('expense')">
                            <span>➖</span> Расход
                        </button>
                        <button class="type-button income-button" onclick="setTransactionType('income')">
                            <span>➕</span> Доход
                        </button>
                    </div>
                    
                    <div class="input-group">
                        <label for="amount">Сумма (₽)</label>
                        <input type="number" id="amount" placeholder="Введите сумму" min="1" step="1" autocomplete="off">
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
                            <option value="кофе">☕ Кофе</option>
                            <option value="обед">🍽️ Обед</option>
                            <option value="продукты">🛒 Продукты</option>
                            <option value="другое">📌 Другое</option>
                        </select>
                    </div>
                    
                    <button class="submit-button" onclick="addTransaction()">
                        <span>💾</span> Добавить операцию
                    </button>
                </div>
            </div>

            <!-- Categories Section -->
            <div class="section-content" id="categoriesContent" style="display: none;">
                <div class="categories-section">
                    <div class="section-title">Выберите категорию</div>
                    <div class="category-list" id="categoryList">
                        <!-- Categories will be populated by JavaScript -->
                    </div>
                </div>
            </div>
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
        const tg = window.Telegram?.WebApp;
        const isDesktop = window.innerWidth > 768;
        
        // Глобальные переменные
        let userData = {
            balance: 15200,
            transactions: [],
            categories: {},
            totalTransactions: 0
        };
        
        let currentTab = 'transactions';
        let transactionType = 'expense';
        let isInitialized = false;
        
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
            setupScrollHandling();
            hideScrollHintAfterInteraction();
        });

        // Настройка скроллинга
        function setupScrollHandling() {
            const appContainer = document.getElementById('appContainer');
            const scrollProgress = document.getElementById('scrollProgress');
            
            // Обработчик колесика мыши
            appContainer.addEventListener('wheel', function(e) {
                // Плавный скролл
                this.scrollBy({
                    top: e.deltaY * 0.5,
                    behavior: 'smooth'
                });
                
                // Показать/скрыть подсказку
                if (isDesktop) {
                    const scrollHint = document.getElementById('scrollHint');
                    if (this.scrollTop > 100) {
                        scrollHint.style.opacity = '0';
                        scrollHint.style.pointerEvents = 'none';
                    }
                }
                
                // Обновить индикатор прогресса
                updateScrollProgress();
            }, { passive: true });
            
            // Обновление индикатора при скролле
            appContainer.addEventListener('scroll', function() {
                updateScrollProgress();
                checkVisibility();
            });
            
            // Начальное обновление прогресса
            updateScrollProgress();
        }

        // Обновление индикатора прогресса скролла
        function updateScrollProgress() {
            const appContainer = document.getElementById('appContainer');
            const scrollProgress = document.getElementById('scrollProgress');
            
            const scrolled = appContainer.scrollTop;
            const maxScroll = appContainer.scrollHeight - appContainer.clientHeight;
            const progress = scrolled / maxScroll;
            
            scrollProgress.style.transform = `scaleX(${progress})`;
        }

        // Проверка видимости элементов
        function checkVisibility() {
            const sections = document.querySelectorAll('.section-content');
            const appContainer = document.getElementById('appContainer');
            
            sections.forEach(section => {
                const rect = section.getBoundingClientRect();
                const containerRect = appContainer.getBoundingClientRect();
                
                if (rect.top <= containerRect.bottom - 100) {
                    section.classList.add('visible');
                }
            });
        }

        // Скрыть подсказку скролла после взаимодействия
        function hideScrollHintAfterInteraction() {
            if (!isDesktop) return;
            
            const scrollHint = document.getElementById('scrollHint');
            const hideEvents = ['wheel', 'touchstart', 'mousedown', 'keydown'];
            
            const hideHint = () => {
                scrollHint.style.opacity = '0';
                scrollHint.style.pointerEvents = 'none';
                scrollHint.style.transition = 'opacity 0.5s';
            };
            
            hideEvents.forEach(event => {
                document.addEventListener(event, hideHint, { once: true });
            });
            
            // Автоскрытие через 5 секунд
            setTimeout(hideHint, 5000);
        }

        // Инициализация приложения
        function initApp() {
            if (tg) {
                // Если в Telegram
                tg.ready();
                tg.expand();
                setupTelegramTheme();
                loadUserDataFromBot();
            } else {
                // Если не в Telegram, используем локальное хранилище
                loadFromLocalStorage();
            }
            
            setupCategoryButtons();
            setupDemoData();
            updateUI();
            isInitialized = true;
        }

        // Настройка темы Telegram
        function setupTelegramTheme() {
            if (tg) {
                document.documentElement.style.setProperty('--tg-color-scheme', tg.colorScheme);
                document.documentElement.style.setProperty('--tg-theme-bg-color', tg.themeParams.bg_color || '#ffffff');
                document.documentElement.style.setProperty('--tg-theme-text-color', tg.themeParams.text_color || '#000000');
                document.documentElement.style.setProperty('--tg-theme-hint-color', tg.themeParams.hint_color || '#999999');
                document.documentElement.style.setProperty('--tg-theme-link-color', tg.themeParams.link_color || '#2481cc');
                document.documentElement.style.setProperty('--tg-theme-button-color', tg.themeParams.button_color || '#667eea');
                document.documentElement.style.setProperty('--tg-theme-button-text-color', tg.themeParams.button_text_color || '#ffffff');
                
                // Применяем тему
                document.body.style.background = tg.themeParams.bg_color || 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)';
            }
        }

        // Настройка демо-данных
        function setupDemoData() {
            const demoTransactions = [
                { 
                    amount: 20000, 
                    category: 'зарплата', 
                    timestamp: '01.01 09:00',
                    note: 'Январская зарплата'
                },
                { 
                    amount: -500, 
                    category: 'кофе', 
                    timestamp: '02.01 12:30',
                    note: 'Кофе с коллегами'
                },
                { 
                    amount: -1500, 
                    category: 'обед', 
                    timestamp: '03.01 13:45',
                    note: 'Бизнес-ланч'
                },
                { 
                    amount: -800, 
                    category: 'транспорт', 
                    timestamp: '04.01 08:15',
                    note: 'Такси на работу'
                }
            ];
            
            // Обновляем данные только если они пустые
            if (userData.transactions.length === 0) {
                userData.transactions = demoTransactions;
                userData.balance = demoTransactions.reduce((sum, t) => sum + t.amount, 0);
                userData.totalTransactions = demoTransactions.length;
                
                // Создаем категории из транзакций
                demoTransactions.forEach(t => {
                    if (!userData.categories[t.category]) {
                        userData.categories[t.category] = 0;
                    }
                    userData.categories[t.category] += t.amount;
                });
                
                saveToLocalStorage();
            }
        }

        // Остальные функции остаются такими же, как в предыдущей версии
        // (loadFromLocalStorage, saveToLocalStorage, updateUI, switchTab, и т.д.)

        // Обновление UI
        function updateUI() {
            const balanceElement = document.getElementById('balance');
            balanceElement.textContent = `${formatNumber(userData.balance)} ₽`;
            
            // Анимация обновления баланса
            balanceElement.classList.remove('balance-updated');
            void balanceElement.offsetWidth; // Trigger reflow
            balanceElement.classList.add('balance-updated');
            
            if (userData.balance > 0) {
                balanceElement.className = 'balance-amount balance-positive balance-updated';
            } else if (userData.balance < 0) {
                balanceElement.className = 'balance-amount balance-negative balance-updated';
            } else {
                balanceElement.className = 'balance-amount balance-zero balance-updated';
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
            
            document.querySelectorAll('.tab')[tabName === 'transactions' ? 0 : tabName === 'add' ? 1 : 2].classList.add('active');
            
            // Показываем/скрываем соответствующие секции
            const contents = ['transactionsContent', 'addContent', 'categoriesContent'];
            contents.forEach(contentId => {
                const element = document.getElementById(contentId);
                if (contentId === `${tabName}Content`) {
                    element.style.display = 'block';
                    element.classList.add('visible');
                    
                    // Прокручиваем к началу секции
                    setTimeout(() => {
                        const appContainer = document.getElementById('appContainer');
                        const elementTop = element.offsetTop - 20;
                        appContainer.scrollTo({
                            top: elementTop,
                            behavior: 'smooth'
                        });
                    }, 100);
                } else {
                    element.style.display = 'none';
                    element.classList.remove('visible');
                }
            });
        }

        // Фокус на поле ввода при открытии вкладки добавления
        document.addEventListener('DOMContentLoaded', function() {
            document.addEventListener('tabChanged', function(e) {
                if (e.detail.tab === 'add') {
                    setTimeout(() => {
                        document.getElementById('amount').focus();
                    }, 300);
                }
            });
        });

        // Остальной код остается таким же, как в предыдущей версии
        // (setTransactionType, addTransaction, setupCategoryButtons, и т.д.)

        // Добавьте обработчики для улучшения UX
        function enhanceUX() {
            // Добавляем клавиатурные сокращения
            document.addEventListener('keydown', function(e) {
                if (e.ctrlKey || e.metaKey) {
                    switch(e.key) {
                        case '1':
                            e.preventDefault();
                            switchTab('transactions');
                            break;
                        case '2':
                            e.preventDefault();
                            switchTab('add');
                            break;
                        case '3':
                            e.preventDefault();
                            switchTab('categories');
                            break;
                        case 's':
                            e.preventDefault();
                            if (currentTab === 'add') addTransaction();
                            break;
                    }
                }
                
                // Escape закрывает уведомления
                if (e.key === 'Escape') {
                    const notification = document.getElementById('notification');
                    notification.classList.remove('show');
                }
            });
            
            // Сохраняем данные при закрытии
            window.addEventListener('beforeunload', function() {
                saveToLocalStorage();
            });
        }

        // Запускаем улучшения UX
        enhanceUX();
    </script>
</body>
</html>
