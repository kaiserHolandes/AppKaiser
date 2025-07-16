# AppKaiser
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WhatsApp Business Hub - Micro-SaaS</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        /* Custom styles */
        .nav-item.active {
            background-color: #dbeafe;
            color: #2563eb;
            border-right: 2px solid #2563eb;
        }

        .nav-item {
            color: #374151;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .settings-content {
            display: none;
        }

        .settings-content.active {
            display: block;
        }

        .settings-tab-btn.active {
            background-color: #dbeafe;
            color: #2563eb;
        }

        .settings-tab-btn {
            color: #374151;
        }

        .settings-tab-btn:hover {
            background-color: #f9fafb;
        }

        .conversation-item:hover {
            background-color: #f9fafb;
        }

        /* Responsive adjustments */
        @media (max-width: 1024px) {
            #sidebar {
                transform: translateX(-100%);
            }
            
            #sidebar.open {
                transform: translateX(0);
            }
            
            #main-content {
                margin-left: 0;
            }
        }

        /* Animation classes */
        .fade-in {
            animation: fadeIn 0.3s ease-in-out;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }

        ::-webkit-scrollbar-thumb {
            background: #c1c1c1;
            border-radius: 3px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #a8a8a8;
        }

        /* QR Code styles */
        .qr-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 2rem;
        }

        .qr-code {
            border: 2px solid #e5e7eb;
            border-radius: 0.5rem;
            padding: 1rem;
            background: white;
            margin: 1rem 0;
        }

        .connection-status {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.5rem 1rem;
            border-radius: 9999px;
            font-size: 0.875rem;
        }

        .status-connected {
            background-color: #dcfce7;
            color: #166534;
        }

        .status-disconnected {
            background-color: #fef2f2;
            color: #991b1b;
        }

        .status-connecting {
            background-color: #fef3c7;
            color: #92400e;
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.5;
            }
        }

        /* Login page styles */
        .login-container {
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .login-card {
            background: white;
            border-radius: 1rem;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            padding: 2rem;
            width: 100%;
            max-width: 400px;
        }

        .login-logo {
            width: 4rem;
            height: 4rem;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1.5rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            font-size: 0.875rem;
            font-weight: 500;
            color: #374151;
            margin-bottom: 0.5rem;
        }

        .form-input {
            width: 100%;
            padding: 0.75rem 1rem;
            border: 1px solid #d1d5db;
            border-radius: 0.5rem;
            font-size: 1rem;
            transition: all 0.2s;
        }

        .form-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .btn-primary {
            width: 100%;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 0.75rem 1rem;
            border: none;
            border-radius: 0.5rem;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary:hover {
            transform: translateY(-1px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .btn-primary:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .error-message {
            background-color: #fef2f2;
            border: 1px solid #fecaca;
            color: #dc2626;
            padding: 0.75rem;
            border-radius: 0.5rem;
            font-size: 0.875rem;
            margin-bottom: 1rem;
        }

        .demo-credentials {
            background-color: #eff6ff;
            border: 1px solid #bfdbfe;
            border-radius: 0.5rem;
            padding: 1rem;
            margin-top: 1.5rem;
        }

        .demo-credentials h4 {
            color: #1e40af;
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .demo-credentials p {
            color: #1d4ed8;
            font-size: 0.875rem;
            margin: 0.25rem 0;
        }

        /* Hide/show sections */
        .hidden {
            display: none !important;
        }

        .show {
            display: block !important;
        }

        /* Loading spinner */
        .spinner {
            border: 2px solid #f3f3f3;
            border-top: 2px solid #667eea;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
            display: inline-block;
            margin-right: 0.5rem;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Message bubbles */
        .message-bubble {
            max-width: 70%;
            padding: 0.75rem 1rem;
            border-radius: 1rem;
            margin-bottom: 0.5rem;
            position: relative;
        }

        .message-sent {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 0.25rem;
        }

        .message-received {
            background: #f3f4f6;
            color: #1f2937;
            margin-right: auto;
            border-bottom-left-radius: 0.25rem;
        }

        .message-time {
            font-size: 0.75rem;
            opacity: 0.7;
            margin-top: 0.25rem;
        }

        /* AI suggestions */
        .ai-suggestion {
            background: white;
            border: 1px solid #e5e7eb;
            border-radius: 0.5rem;
            padding: 0.75rem;
            margin-bottom: 0.5rem;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 0.875rem;
        }

        .ai-suggestion:hover {
            background: #f9fafb;
            border-color: #667eea;
        }

        /* Reminder cards */
        .reminder-card {
            background: white;
            border: 1px solid #e5e7eb;
            border-radius: 0.5rem;
            padding: 1.5rem;
            margin-bottom: 1rem;
            transition: all 0.2s;
        }

        .reminder-card:hover {
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        .reminder-status {
            display: inline-flex;
            align-items: center;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.75rem;
            font-weight: 500;
        }

        .status-active {
            background-color: #dcfce7;
            color: #166534;
        }

        .status-pending {
            background-color: #fef3c7;
            color: #92400e;
        }

        /* Stats cards */
        .stat-card {
            background: white;
            border-radius: 0.5rem;
            padding: 1.5rem;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
            transition: all 0.2s;
        }

        .stat-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        .stat-icon {
            width: 3rem;
            height: 3rem;
            border-radius: 0.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 1rem;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: #1f2937;
            margin-bottom: 0.25rem;
        }

        .stat-label {
            font-size: 0.875rem;
            color: #6b7280;
        }

        .stat-change {
            font-size: 0.875rem;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 0.25rem;
        }

        .stat-change.positive {
            color: #059669;
        }

        .stat-change.negative {
            color: #dc2626;
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Login Page -->
    <div id="login-page" class="login-container">
        <div class="login-card">
            <div class="text-center">
                <div class="login-logo">
                    <i class="fas fa-comments text-white text-2xl"></i>
                </div>
                <h1 class="text-2xl font-bold text-gray-900 mb-2">WhatsApp Business Hub</h1>
                <p class="text-gray-600 mb-8">Faça login para acessar sua conta</p>
            </div>

            <form id="login-form">
                <div id="error-container"></div>
                
                <div class="form-group">
                    <label for="email" class="form-label">Email</label>
                    <input type="email" id="email" class="form-input" placeholder="seu@email.com" required>
                </div>

                <div class="form-group">
                    <label for="password" class="form-label">Senha</label>
                    <div class="relative">
                        <input type="password" id="password" class="form-input" placeholder="Digite sua senha" required>
                        <button type="button" id="toggle-password" class="absolute right-3 top-3 text-gray-400 hover:text-gray-600">
                            <i class="fas fa-eye"></i>
                        </button>
                    </div>
                </div>

                <div class="flex items-center justify-between mb-6">
                    <label class="flex items-center">
                        <input type="checkbox" class="mr-2">
                        <span class="text-sm text-gray-600">Lembrar de mim</span>
                    </label>
                    <a href="#" class="text-sm text-blue-600 hover:text-blue-500">Esqueceu a senha?</a>
                </div>

                <button type="submit" id="login-btn" class="btn-primary">
                    <span id="login-text">Entrar</span>
                    <span id="login-loading" class="hidden">
                        <span class="spinner"></span>
                        Entrando...
                    </span>
                </button>
            </form>

            <div class="demo-credentials">
                <h4>Conta de Demonstração</h4>
                <p><strong>Email:</strong> admin@wahub.com</p>
                <p><strong>Senha:</strong> 123456</p>
            </div>

            <div class="text-center mt-6">
                <p class="text-sm text-gray-600">
                    Não tem uma conta? 
                    <a href="#" class="text-blue-600 hover:text-blue-500 font-medium">Cadastre-se gratuitamente</a>
                </p>
            </div>
        </div>
    </div>

    <!-- Main Application -->
    <div id="main-app" class="hidden">
        <!-- Header -->
        <header class="bg-white border-b border-gray-200 px-4 py-3 flex items-center justify-between fixed top-0 left-0 right-0 z-50">
            <div class="flex items-center space-x-4">
                <button id="sidebar-toggle" class="p-2 rounded-lg hover:bg-gray-100 transition-colors">
                    <i class="fas fa-bars text-xl"></i>
                </button>
                <h1 class="text-xl font-semibold text-gray-900">WhatsApp Business Hub</h1>
            </div>
            
            <div class="flex items-center space-x-3">
                <button class="relative p-2 rounded-lg hover:bg-gray-100 transition-colors">
                    <i class="fas fa-bell text-xl"></i>
                    <span class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center">3</span>
                </button>
                
                <div class="flex items-center space-x-2">
                    <div class="w-8 h-8 bg-blue-600 rounded-full flex items-center justify-center">
                        <i class="fas fa-user text-white text-sm"></i>
                    </div>
                    <span class="text-sm font-medium text-gray-700" id="user-name">João Silva</span>
                </div>
                
                <div class="relative group">
                    <button class="p-2 rounded-lg hover:bg-gray-100 transition-colors">
                        <i class="fas fa-cog text-xl"></i>
                    </button>
                    <div class="absolute right-0 top-full mt-2 w-48 bg-white rounded-lg shadow-lg border border-gray-200 opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200">
                        <div class="p-2">
                            <button id="logout-btn" class="w-full flex items-center space-x-2 px-3 py-2 text-sm text-gray-700 hover:bg-gray-100 rounded-lg">
                                <i class="fas fa-sign-out-alt"></i>
                                <span>Sair</span>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Sidebar -->
        <aside id="sidebar" class="bg-white border-r border-gray-200 fixed left-0 top-16 bottom-0 w-64 transition-transform duration-300 z-40">
            <div class="p-4 border-b border-gray-200 flex items-center justify-between">
                <div class="flex items-center space-x-2">
                    <div class="w-8 h-8 bg-green-600 rounded-lg flex items-center justify-center">
                        <i class="fas fa-bolt text-white text-sm"></i>
                    </div>
                    <span class="font-semibold text-gray-900">WA Hub</span>
                </div>
            </div>

            <nav class="mt-4">
                <button class="nav-item active w-full flex items-center space-x-3 px-4 py-3 text-left hover:bg-gray-50 transition-colors" data-tab="dashboard">
                    <i class="fas fa-chart-line text-xl"></i>
                    <span class="font-medium">Painel</span>
                </button>
                <button class="nav-item w-full flex items-center space-x-3 px-4 py-3 text-left hover:bg-gray-50 transition-colors" data-tab="conversations">
                    <i class="fas fa-comments text-xl"></i>
                    <span class="font-medium">Conversas</span>
                </button>
                <button class="nav-item w-full flex items-center space-x-3 px-4 py-3 text-left hover:bg-gray-50 transition-colors" data-tab="reminders">
                    <i class="fas fa-clock text-xl"></i>
                    <span class="font-medium">Lembretes</span>
                </button>
                <button class="nav-item w-full flex items-center space-x-3 px-4 py-3 text-left hover:bg-gray-50 transition-colors" data-tab="reports">
                    <i class="fas fa-chart-bar text-xl"></i>
                    <span class="font-medium">Relatórios</span>
                </button>
                <button class="nav-item w-full flex items-center space-x-3 px-4 py-3 text-left hover:bg-gray-50 transition-colors" data-tab="settings">
                    <i class="fas fa-cog text-xl"></i>
                    <span class="font-medium">Configurações</span>
                </button>
            </nav>
            
            <div class="absolute bottom-4 left-4 right-4">
                <div class="bg-gradient-to-r from-blue-600 to-purple-600 rounded-lg p-4 text-white">
                    <h4 class="font-semibold mb-1">Plano Pro</h4>
                    <p class="text-sm opacity-90">1.247 / 5.000 mensagens</p>
                    <button class="mt-2 text-sm underline hover:no-underline">Fazer upgrade</button>
                </div>
            </div>
        </aside>

        <!-- Main Content -->
        <main id="main-content" class="ml-64 mt-16 p-6 transition-all duration-300">
            <!-- Dashboard Tab -->
            <div id="dashboard-tab" class="tab-content active">
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <h2 class="text-2xl font-bold text-gray-900">Painel de Controle</h2>
                        <div id="whatsapp-status" class="connection-status status-disconnected">
                            <div class="w-3 h-3 bg-red-500 rounded-full"></div>
                            <span>WhatsApp Desconectado</span>
                        </div>
                    </div>

                    <!-- Stats Grid -->
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-4">
                                <div class="stat-icon bg-blue-100">
                                    <i class="fas fa-comments text-2xl text-blue-600"></i>
                                </div>
                                <div class="stat-change positive">
                                    <i class="fas fa-arrow-up text-sm"></i>
                                    <span>+12%</span>
                                </div>
                            </div>
                            <div class="stat-value">142</div>
                            <div class="stat-label">Mensagens Hoje</div>
                        </div>

                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-4">
                                <div class="stat-icon bg-green-100">
                                    <i class="fas fa-clock text-2xl text-green-600"></i>
                                </div>
                                <div class="stat-change positive">
                                    <i class="fas fa-arrow-down text-sm"></i>
                                    <span>-25%</span>
                                </div>
                            </div>
                            <div class="stat-value">3.2 min</div>
                            <div class="stat-label">Tempo Médio Resposta</div>
                        </div>

                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-4">
                                <div class="stat-icon bg-purple-100">
                                    <i class="fas fa-chart-line text-2xl text-purple-600"></i>
                                </div>
                                <div class="stat-change positive">
                                    <i class="fas fa-arrow-up text-sm"></i>
                                    <span>+8%</span>
                                </div>
                            </div>
                            <div class="stat-value">28%</div>
                            <div class="stat-label">Taxa de Conversão</div>
                        </div>

                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-4">
                                <div class="stat-icon bg-orange-100">
                                    <i class="fas fa-users text-2xl text-orange-600"></i>
                                </div>
                                <div class="stat-change positive">
                                    <i class="fas fa-arrow-up text-sm"></i>
                                    <span>+15%</span>
                                </div>
                            </div>
                            <div class="stat-value">89</div>
                            <div class="stat-label">Contatos Ativos</div>
                        </div>
                    </div>

                    <!-- Recent Activities -->
                    <div class="bg-white rounded-lg shadow-sm border border-gray-200">
                        <div class="p-6 border-b border-gray-200">
                            <h3 class="text-lg font-semibold text-gray-900">Atividades Recentes</h3>
                        </div>
                        
                        <div class="divide-y divide-gray-200">
                            <div class="p-6 hover:bg-gray-50 transition-colors">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center space-x-3 mb-2">
                                            <h4 class="font-medium text-gray-900">Nova mensagem de Maria Santos</h4>
                                            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-green-100 text-green-800">vendas</span>
                                        </div>
                                        <p class="text-sm text-gray-600 mb-2">Pergunta sobre preços dos produtos</p>
                                        <span class="text-xs text-gray-500">2 min atrás</span>
                                    </div>
                                    <div class="ml-4">
                                        <i class="fas fa-exclamation-circle text-orange-500 text-xl"></i>
                                    </div>
                                </div>
                            </div>

                            <div class="p-6 hover:bg-gray-50 transition-colors">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center space-x-3 mb-2">
                                            <h4 class="font-medium text-gray-900">Lembrete: Follow-up com João</h4>
                                            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-green-100 text-green-800">vendas</span>
                                        </div>
                                        <p class="text-sm text-gray-600 mb-2">Enviar proposta personalizada</p>
                                        <span class="text-xs text-gray-500">15 min atrás</span>
                                    </div>
                                    <div class="ml-4">
                                        <i class="fas fa-check-circle text-green-500 text-xl"></i>
                                    </div>
                                </div>
                            </div>

                            <div class="p-6 hover:bg-gray-50 transition-colors">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center space-x-3 mb-2">
                                            <h4 class="font-medium text-gray-900">Relatório semanal gerado</h4>
                                            <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800">sistema</span>
                                        </div>
                                        <p class="text-sm text-gray-600 mb-2">Relatório de performance da semana disponível</p>
                                        <span class="text-xs text-gray-500">1 hora atrás</span>
                                    </div>
                                    <div class="ml-4">
                                        <i class="fas fa-file-alt text-blue-500 text-xl"></i>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Conversations Tab -->
            <div id="conversations-tab" class="tab-content">
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <h2 class="text-2xl font-bold text-gray-900">Conversas</h2>
                        <button class="flex items-center space-x-2 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                            <i class="fas fa-plus"></i>
                            <span>Nova Conversa</span>
                        </button>
                    </div>

                    <div class="flex h-96 bg-white rounded-lg shadow-sm border border-gray-200">
                        <!-- Conversations List -->
                        <div class="w-1/3 border-r border-gray-200 flex flex-col">
                            <div class="p-4 border-b border-gray-200">
                                <div class="relative">
                                    <i class="fas fa-search absolute left-3 top-3 text-gray-400"></i>
                                    <input type="text" placeholder="Buscar conversas..." class="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                </div>
                            </div>

                            <div class="flex-1 overflow-y-auto">
                                <div class="conversation-item p-4 cursor-pointer hover:bg-gray-50 transition-colors bg-blue-50 border-r-2 border-blue-500">
                                    <div class="flex items-center space-x-3">
                                        <div class="relative">
                                            <div class="w-12 h-12 bg-pink-500 rounded-full flex items-center justify-center text-white font-medium">MS</div>
                                            <div class="absolute -bottom-1 -right-1 w-4 h-4 bg-green-500 rounded-full border-2 border-white"></div>
                                        </div>
                                        <div class="flex-1 min-w-0">
                                            <div class="flex items-center justify-between mb-1">
                                                <h4 class="font-medium text-gray-900 truncate">Maria Santos</h4>
                                                <div class="flex items-center space-x-2">
                                                    <span class="text-xs text-gray-500">2 min</span>
                                                    <span class="bg-blue-500 text-white text-xs rounded-full px-2 py-1 min-w-[20px] text-center">2</span>
                                                </div>
                                            </div>
                                            <div class="flex items-center justify-between">
                                                <p class="text-sm text-gray-600 truncate">Olá! Gostaria de saber sobre os preços...</p>
                                                <span class="px-2 py-1 text-xs rounded-full bg-green-100 text-green-800">vendas</span>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                                <div class="conversation-item p-4 cursor-pointer hover:bg-gray-50 transition-colors">
                                    <div class="flex items-center space-x-3">
                                        <div class="relative">
                                            <div class="w-12 h-12 bg-blue-500 rounded-full flex items-center justify-center text-white font-medium">JS</div>
                                        </div>
                                        <div class="flex-1 min-w-0">
                                            <div class="flex items-center justify-between mb-1">
                                                <h4 class="font-medium text-gray-900 truncate">João Silva</h4>
                                                <div class="flex items-center space-x-2">
                                                    <span class="text-xs text-gray-500">1h</span>
                                                </div>
                                            </div>
                                            <div class="flex items-center justify-between">
                                                <p class="text-sm text-gray-600 truncate">Obrigado pelo atendimento!</p>
                                                <span class="px-2 py-1 text-xs rounded-full bg-blue-100 text-blue-800">suporte</span>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                                <div class="conversation-item p-4 cursor-pointer hover:bg-gray-50 transition-colors">
                                    <div class="flex items-center space-x-3">
                                        <div class="relative">
                                            <div class="w-12 h-12 bg-green-500 rounded-full flex items-center justify-center text-white font-medium">AC</div>
                                            <div class="absolute -bottom-1 -right-1 w-4 h-4 bg-green-500 rounded-full border-2 border-white"></div>
                                        </div>
                                        <div class="flex-1 min-w-0">
                                            <div class="flex items-center justify-between mb-1">
                                                <h4 class="font-medium text-gray-900 truncate">Ana Costa</h4>
                                                <div class="flex items-center space-x-2">
                                                    <span class="text-xs text-gray-500">3h</span>
                                                    <span class="bg-blue-500 text-white text-xs rounded-full px-2 py-1 min-w-[20px] text-center">1</span>
                                                </div>
                                            </div>
                                            <div class="flex items-center justify-between">
                                                <p class="text-sm text-gray-600 truncate">Quando vocês fazem entrega?</p>
                                                <span class="px-2 py-1 text-xs rounded-full bg-yellow-100 text-yellow-800">logística</span>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Chat Area -->
                        <div class="flex-1 flex flex-col">
                            <div class="p-4 border-b border-gray-200 flex items-center justify-between">
                                <div class="flex items-center space-x-3">
                                    <div class="w-10 h-10 bg-pink-500 rounded-full flex items-center justify-center text-white font-medium">MS</div>
                                    <div>
                                        <h4 class="font-medium text-gray-900">Maria Santos</h4>
                                        <p class="text-sm text-gray-500">Online • Última vez: agora</p>
                                    </div>
                                </div>
                                <div class="flex items-center space-x-2">
                                    <button class="p-2 rounded-lg hover:bg-gray-100"><i class="fas fa-phone"></i></button>
                                    <button class="p-2 rounded-lg hover:bg-gray-100"><i class="fas fa-video"></i></button>
                                    <button class="p-2 rounded-lg hover:bg-gray-100"><i class="fas fa-star"></i></button>
                                </div>
                            </div>

                            <div class="flex-1 overflow-y-auto p-4 space-y-4">
                                <div class="flex justify-start">
                                    <div class="message-bubble message-received">
                                        <p class="text-sm">Olá! Gostaria de saber sobre os preços dos produtos</p>
                                        <div class="message-time">14:30</div>
                                    </div>
                                </div>
                                
                                <div class="flex justify-end">
                                    <div class="message-bubble message-sent">
                                        <p class="text-sm">Olá Maria! Claro, posso te ajudar com isso. Qual produto específico você tem interesse?</p>
                                        <div class="message-time">14:32</div>
                                    </div>
                                </div>

                                <div class="flex justify-start">
                                    <div class="message-bubble message-received">
                                        <p class="text-sm">Estou interessada nos produtos de beleza, principalmente cremes faciais</p>
                                        <div class="message-time">14:33</div>
                                    </div>
                                </div>

                                <div class="flex justify-end">
                                    <div class="message-bubble message-sent">
                                        <p class="text-sm">Perfeito! Temos uma linha completa de cremes faciais. Posso te enviar nosso catálogo?</p>
                                        <div class="message-time">14:35</div>
                                    </div>
                                </div>
                            </div>

                            <div class="p-4 bg-gray-50 border-t border-gray-200">
                                <div class="flex items-center space-x-2 mb-3">
                                    <i class="fas fa-robot text-purple-500"></i>
                                    <span class="text-sm font-medium text-gray-700">Sugestões da IA</span>
                                </div>
                                <div class="space-y-2 mb-4">
                                    <div class="ai-suggestion" onclick="insertSuggestion(this)">
                                        Temos uma promoção especial hoje com 15% de desconto em toda linha de beleza!
                                    </div>
                                    <div class="ai-suggestion" onclick="insertSuggestion(this)">
                                        Posso te enviar nosso catálogo completo de produtos de beleza
                                    </div>
                                    <div class="ai-suggestion" onclick="insertSuggestion(this)">
                                        Gostaria de agendar uma demonstração dos produtos?
                                    </div>
                                </div>
                            </div>

                            <div class="p-4 border-t border-gray-200">
                                <div class="flex items-center space-x-2">
                                    <button class="p-2 rounded-lg hover:bg-gray-100"><i class="fas fa-paperclip"></i></button>
                                    <div class="flex-1 relative">
                                        <input type="text" id="message-input" placeholder="Digite sua mensagem..." class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                        <button class="absolute right-2 top-2 p-1 rounded-lg hover:bg-gray-100"><i class="fas fa-smile"></i></button>
                                    </div>
                                    <button onclick="sendMessage()" class="p-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors"><i class="fas fa-paper-plane"></i></button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Reminders Tab -->
            <div id="reminders-tab" class="tab-content">
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <h2 class="text-2xl font-bold text-gray-900">Lembretes Inteligentes</h2>
                        <button class="flex items-center space-x-2 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                            <i class="fas fa-plus"></i>
                            <span>Novo Lembrete</span>
                        </button>
                    </div>

                    <div class="bg-white rounded-lg shadow-sm border border-gray-200">
                        <div class="p-6 border-b border-gray-200">
                            <h3 class="text-lg font-semibold text-gray-900">Lembretes Ativos</h3>
                        </div>

                        <div class="divide-y divide-gray-200">
                            <div class="reminder-card">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center space-x-3 mb-2">
                                            <h4 class="font-medium text-gray-900">Follow-up Maria Santos</h4>
                                            <span class="reminder-status status-active">Ativo</span>
                                            <span class="px-2 py-1 text-xs rounded-full bg-green-100 text-green-800">vendas</span>
                                        </div>
                                        <div class="flex items-center space-x-4 text-sm text-gray-600 mb-3">
                                            <div class="flex items-center space-x-1">
                                                <i class="fas fa-user text-sm"></i>
                                                <span>Maria Santos</span>
                                            </div>
                                            <div class="flex items-center space-x-1">
                                                <i class="fas fa-clock text-sm"></i>
                                                <span>15 min</span>
                                            </div>
                                        </div>
                                        <p class="text-sm text-gray-700 bg-gray-50 p-3 rounded-lg">
                                            Olá Maria! Vi que você tinha interesse em nossos produtos de beleza. Gostaria de conversar mais sobre nossa promoção especial?
                                        </p>
                                    </div>
                                    <div class="ml-4 flex items-center space-x-2">
                                        <button class="p-2 text-yellow-600 hover:bg-yellow-50 rounded-lg"><i class="fas fa-pause"></i></button>
                                        <button class="p-2 text-gray-600 hover:bg-gray-50 rounded-lg"><i class="fas fa-edit"></i></button>
                                        <button class="p-2 text-red-600 hover:bg-red-50 rounded-lg"><i class="fas fa-trash"></i></button>
                                    </div>
                                </div>
                            </div>

                            <div class="reminder-card">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center space-x-3 mb-2">
                                            <h4 class="font-medium text-gray-900">Lembrete de proposta - João Silva</h4>
                                            <span class="reminder-status status-pending">Pendente</span>
                                            <span class="px-2 py-1 text-xs rounded-full bg-blue-100 text-blue-800">vendas</span>
                                        </div>
                                        <div class="flex items-center space-x-4 text-sm text-gray-600 mb-3">
                                            <div class="flex items-center space-x-1">
                                                <i class="fas fa-user text-sm"></i>
                                                <span>João Silva</span>
                                            </div>
                                            <div class="flex items-center space-x-1">
                                                <i class="fas fa-clock text-sm"></i>
                                                <span>2 horas</span>
                                            </div>
                                        </div>
                                        <p class="text-sm text-gray-700 bg-gray-50 p-3 rounded-lg">
                                            Olá João! Preparei uma proposta personalizada para você. Quando podemos conversar sobre os detalhes?
                                        </p>
                                    </div>
                                    <div class="ml-4 flex items-center space-x-2">
                                        <button class="p-2 text-green-600 hover:bg-green-50 rounded-lg"><i class="fas fa-play"></i></button>
                                        <button class="p-2 text-gray-600 hover:bg-gray-50 rounded-lg"><i class="fas fa-edit"></i></button>
                                        <button class="p-2 text-red-600 hover:bg-red-50 rounded-lg"><i class="fas fa-trash"></i></button>
                                    </div>
                                </div>
                            </div>

                            <div class="reminder-card">
                                <div class="flex items-start justify-between">
                                    <div class="flex-1">
                                        <div class="flex items-center space-x-3 mb-2">
                                            <h4 class="font-medium text-gray-900">Follow-up Ana Costa - Entrega</h4>
                                            <span class="reminder-status status-active">Ativo</span>
                                            <span class="px-2 py-1 text-xs rounded-full bg-yellow-100 text-yellow-800">logística</span>
                                        </div>
                                        <div class="flex items-center space-x-4 text-sm text-gray-600 mb-3">
                                            <div class="flex items-center space-x-1">
                                                <i class="fas fa-user text-sm"></i>
                                                <span>Ana Costa</span>
                                            </div>
                                            <div class="flex items-center space-x-1">
                                                <i class="fas fa-clock text-sm"></i>
                                                <span>30 min</span>
                                            </div>
                                        </div>
                                        <p class="text-sm text-gray-700 bg-gray-50 p-3 rounded-lg">
                                            Olá Ana! Sobre sua pergunta de entrega, fazemos entregas de segunda a sexta das 8h às 18h. Gostaria de agendar?
                                        </p>
                                    </div>
                                    <div class="ml-4 flex items-center space-x-2">
                                        <button class="p-2 text-yellow-600 hover:bg-yellow-50 rounded-lg"><i class="fas fa-pause"></i></button>
                                        <button class="p-2 text-gray-600 hover:bg-gray-50 rounded-lg"><i class="fas fa-edit"></i></button>
                                        <button class="p-2 text-red-600 hover:bg-red-50 rounded-lg"><i class="fas fa-trash"></i></button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Reports Tab -->
            <div id="reports-tab" class="tab-content">
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <h2 class="text-2xl font-bold text-gray-900">Relatórios & Analytics</h2>
                        <div class="flex items-center space-x-3">
                            <select class="px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option>Últimos 7 dias</option>
                                <option>Últimos 30 dias</option>
                                <option>Últimos 90 dias</option>
                            </select>
                            <button class="flex items-center space-x-2 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                                <i class="fas fa-download"></i>
                                <span>Exportar</span>
                            </button>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="text-sm font-medium text-gray-600">Mensagens Processadas</h3>
                                <span class="text-sm font-medium text-green-600">+23%</span>
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-2xl font-bold text-gray-900">1,247</span>
                                <i class="fas fa-chart-line text-green-500"></i>
                            </div>
                            <p class="text-xs text-gray-500 mt-1">últimos 7 dias</p>
                        </div>

                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="text-sm font-medium text-gray-600">Taxa de Resposta</h3>
                                <span class="text-sm font-medium text-green-600">+5%</span>
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-2xl font-bold text-gray-900">94%</span>
                                <i class="fas fa-chart-line text-green-500"></i>
                            </div>
                            <p class="text-xs text-gray-500 mt-1">últimos 7 dias</p>
                        </div>

                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="text-sm font-medium text-gray-600">Tempo Médio</h3>
                                <span class="text-sm font-medium text-green-600">-15%</span>
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-2xl font-bold text-gray-900">2.3 min</span>
                                <i class="fas fa-chart-line text-green-500"></i>
                            </div>
                            <p class="text-xs text-gray-500 mt-1">últimos 7 dias</p>
                        </div>

                        <div class="stat-card">
                            <div class="flex items-center justify-between mb-2">
                                <h3 class="text-sm font-medium text-gray-600">Conversões</h3>
                                <span class="text-sm font-medium text-green-600">+12%</span>
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-2xl font-bold text-gray-900">34%</span>
                                <i class="fas fa-chart-line text-green-500"></i>
                            </div>
                            <p class="text-xs text-gray-500 mt-1">últimos 7 dias</p>
                        </div>
                    </div>

                    <!-- Charts Section -->
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                        <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-6">
                            <h3 class="text-lg font-semibold text-gray-900 mb-4">Mensagens por Dia</h3>
                            <div class="h-64 flex items-center justify-center border-2 border-dashed border-gray-300 rounded-lg">
                                <div class="text-center">
                                    <i class="fas fa-chart-line text-4xl text-gray-400 mb-2"></i>
                                    <p class="text-gray-500">Gráfico de mensagens por dia</p>
                                </div>
                            </div>
                        </div>

                        <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-6">
                            <h3 class="text-lg font-semibold text-gray-900 mb-4">Categorias de Conversa</h3>
                            <div class="h-64 flex items-center justify-center border-2 border-dashed border-gray-300 rounded-lg">
                                <div class="text-center">
                                    <i class="fas fa-chart-pie text-4xl text-gray-400 mb-2"></i>
                                    <p class="text-gray-500">Gráfico de categorias</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Detailed Reports -->
                    <div class="bg-white rounded-lg shadow-sm border border-gray-200">
                        <div class="p-6 border-b border-gray-200">
                            <h3 class="text-lg font-semibold text-gray-900">Relatório Detalhado</h3>
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Data</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Mensagens</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Respostas</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Taxa</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Conversões</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">Hoje</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">142</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">134</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-green-600">94.4%</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">12</td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">Ontem</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">156</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">148</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-green-600">94.9%</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">15</td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">2 dias atrás</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">128</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">119</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-green-600">93.0%</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">8</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Settings Tab -->
            <div id="settings-tab" class="tab-content">
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <h2 class="text-2xl font-bold text-gray-900">Configurações</h2>
                        <button class="flex items-center space-x-2 bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                            <i class="fas fa-save"></i>
                            <span>Salvar Alterações</span>
                        </button>
                    </div>

                    <div class="flex flex-col lg:flex-row gap-6">
                        <div class="w-full lg:w-64 bg-white rounded-lg shadow-sm border border-gray-200">
                            <nav class="p-4 space-y-2">
                                <button class="settings-tab-btn active w-full flex items-center space-x-3 px-3 py-2 text-left rounded-lg transition-colors" data-settings-tab="whatsapp">
                                    <i class="fas fa-mobile-alt"></i>
                                    <span class="text-sm font-medium">WhatsApp</span>
                                </button>
                                <button class="settings-tab-btn w-full flex items-center space-x-3 px-3 py-2 text-left rounded-lg transition-colors" data-settings-tab="ai">
                                    <i class="fas fa-robot"></i>
                                    <span class="text-sm font-medium">Inteligência Artificial</span>
                                </button>
                                <button class="settings-tab-btn w-full flex items-center space-x-3 px-3 py-2 text-left rounded-lg transition-colors" data-settings-tab="notifications">
                                    <i class="fas fa-bell"></i>
                                    <span class="text-sm font-medium">Notificações</span>
                                </button>
                                <button class="settings-tab-btn w-full flex items-center space-x-3 px-3 py-2 text-left rounded-lg transition-colors" data-settings-tab="account">
                                    <i class="fas fa-user-cog"></i>
                                    <span class="text-sm font-medium">Conta</span>
                                </button>
                            </nav>
                        </div>

                        <div class="flex-1 bg-white rounded-lg shadow-sm border border-gray-200 p-6">
                            <!-- WhatsApp Settings -->
                            <div id="whatsapp-settings" class="settings-content active">
                                <h3 class="text-lg font-semibold text-gray-900 mb-4">Conexão WhatsApp</h3>
                                
                                <!-- Connection Status -->
                                <div class="mb-6">
                                    <div id="connection-display" class="text-center">
                                        <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-4">
                                            <i class="fas fa-wifi-slash text-gray-400 text-2xl" id="connection-icon"></i>
                                        </div>
                                        <h4 class="text-lg font-semibold text-gray-900 mb-2" id="connection-title">WhatsApp Desconectado</h4>
                                        <p class="text-gray-600 mb-6" id="connection-description">
                                            Conecte sua conta WhatsApp para começar a receber mensagens
                                        </p>
                                        
                                        <!-- QR Code Container -->
                                        <div id="qr-container" class="qr-container" style="display: none;">
                                            <div class="qr-code">
                                                <canvas id="qr-canvas" width="256" height="256"></canvas>
                                            </div>
                                            <div class="bg-blue-50 p-4 rounded-lg mb-4 max-w-md">
                                                <h4 class="font-medium text-blue-900 mb-2">Como conectar:</h4>
                                                <ol class="text-sm text-blue-800 text-left space-y-1">
                                                    <li>1. Abra o WhatsApp no seu celular</li>
                                                    <li>2. Toque em "Mais opções" (⋮) → "Dispositivos conectados"</li>
                                                    <li>3. Toque em "Conectar um dispositivo"</li>
                                                    <li>4. Aponte a câmera para este QR code</li>
                                                </ol>
                                            </div>
                                        </div>
                                        
                                        <!-- Connected Info -->
                                        <div id="connected-info" style="display: none;">
                                            <div class="bg-green-50 p-4 rounded-lg mb-6">
                                                <div class="flex items-center justify-center space-x-2 mb-2">
                                                    <i class="fas fa-mobile-alt text-green-600"></i>
                                                    <span class="font-medium text-green-900" id="connected-name">WhatsApp Business</span>
                                                </div>
                                                <p class="text-sm text-green-700" id="connected-number">+55 11 99999-9999</p>
                                                <div class="flex items-center justify-center space-x-1 mt-2">
                                                    <i class="fas fa-wifi text-green-600 text-sm"></i>
                                                    <span class="text-xs text-green-600">Online</span>
                                                </div>
                                            </div>
                                        </div>
                                        
                                        <button id="connect-btn" class="bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition-colors flex items-center space-x-2 mx-auto">
                                            <i class="fas fa-qrcode"></i>
                                            <span>Conectar WhatsApp</span>
                                        </button>
                                        
                                        <button id="disconnect-btn" class="bg-red-600 text-white px-6 py-3 rounded-lg hover:bg-red-700 transition-colors" style="display: none;">
                                            Desconectar
                                        </button>
                                    </div>
                                </div>
                            </div>

                            <!-- AI Settings -->
                            <div id="ai-settings" class="settings-content">
                                <h3 class="text-lg font-semibold text-gray-900 mb-4">Configurações de IA</h3>
                                <div class="space-y-6">
                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-2">Provedor de IA</label>
                                        <select class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            <option>OpenAI GPT-4</option>
                                            <option>Anthropic Claude</option>
                                            <option>Google Gemini</option>
                                        </select>
                                    </div>
                                    
                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-2">Temperatura da IA (Criatividade)</label>
                                        <input type="range" min="0" max="1" step="0.1" value="0.7" class="w-full">
                                        <div class="flex justify-between text-xs text-gray-500 mt-1">
                                            <span>Conservadora</span>
                                            <span>Criativa</span>
                                        </div>
                                    </div>

                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-2">Resposta Automática</label>
                                        <div class="space-y-3">
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3" checked>
                                                <span class="text-sm text-gray-700">Ativar respostas automáticas</span>
                                            </label>
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3">
                                                <span class="text-sm text-gray-700">Apenas em horário comercial</span>
                                            </label>
                                        </div>
                                    </div>

                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-2">Mensagem de Ausência</label>
                                        <textarea class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" rows="3" placeholder="Digite a mensagem automática para quando estiver ausente...">Olá! Obrigado pela sua mensagem. Estou temporariamente ausente, mas retornarei em breve. Para urgências, ligue para (11) 99999-9999.</textarea>
                                    </div>
                                </div>
                            </div>

                            <!-- Notifications Settings -->
                            <div id="notifications-settings" class="settings-content">
                                <h3 class="text-lg font-semibold text-gray-900 mb-4">Configurações de Notificação</h3>
                                <div class="space-y-6">
                                    <div>
                                        <h4 class="font-medium text-gray-900 mb-3">Notificações por Email</h4>
                                        <div class="space-y-3">
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3" checked>
                                                <span class="text-sm text-gray-700">Novas mensagens</span>
                                            </label>
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3" checked>
                                                <span class="text-sm text-gray-700">Lembretes</span>
                                            </label>
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3">
                                                <span class="text-sm text-gray-700">Relatórios semanais</span>
                                            </label>
                                        </div>
                                    </div>

                                    <div>
                                        <h4 class="font-medium text-gray-900 mb-3">Notificações Push</h4>
                                        <div class="space-y-3">
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3" checked>
                                                <span class="text-sm text-gray-700">Mensagens urgentes</span>
                                            </label>
                                            <label class="flex items-center">
                                                <input type="checkbox" class="mr-3">
                                                <span class="text-sm text-gray-700">Todas as mensagens</span>
                                            </label>
                                        </div>
                                    </div>

                                    <div>
                                        <h4 class="font-medium text-gray-900 mb-3">Horário de Notificações</h4>
                                        <div class="grid grid-cols-2 gap-4">
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Das</label>
                                                <input type="time" value="08:00" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Até</label>
                                                <input type="time" value="18:00" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <!-- Account Settings -->
                            <div id="account-settings" class="settings-content">
                                <h3 class="text-lg font-semibold text-gray-900 mb-4">Configurações da Conta</h3>
                                <div class="space-y-6">
                                    <div>
                                        <h4 class="font-medium text-gray-900 mb-3">Informações Pessoais</h4>
                                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Nome</label>
                                                <input type="text" value="João Silva" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Email</label>
                                                <input type="email" value="admin@wahub.com" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                        </div>
                                    </div>

                                    <div>
                                        <h4 class="font-medium text-gray-900 mb-3">Alterar Senha</h4>
                                        <div class="space-y-4">
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Senha Atual</label>
                                                <input type="password" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Nova Senha</label>
                                                <input type="password" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                            <div>
                                                <label class="block text-sm font-medium text-gray-700 mb-1">Confirmar Nova Senha</label>
                                                <input type="password" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                            </div>
                                        </div>
                                    </div>

                                    <div>
                                        <h4 class="font-medium text-gray-900 mb-3">Plano Atual</h4>
                                        <div class="bg-gradient-to-r from-blue-600 to-purple-600 rounded-lg p-4 text-white">
                                            <div class="flex items-center justify-between">
                                                <div>
                                                    <h5 class="font-semibold">Plano Pro</h5>
                                                    <p class="text-sm opacity-90">5.000 mensagens/mês</p>
                                                </div>
                                                <div class="text-right">
                                                    <p class="text-2xl font-bold">R$ 49</p>
                                                    <p class="text-sm opacity-90">/mês</p>
                                                </div>
                                            </div>
                                            <div class="mt-3">
                                                <div class="bg-white bg-opacity-20 rounded-full h-2">
                                                    <div class="bg-white rounded-full h-2" style="width: 25%"></div>
                                                </div>
                                                <p class="text-sm mt-1">1.247 / 5.000 mensagens utilizadas</p>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>

        <!-- Mobile Overlay -->
        <div id="mobile-overlay" class="fixed inset-0 bg-black bg-opacity-50 z-30 hidden lg:hidden"></div>
    </div>

    <script>
        // WhatsApp Business Hub - JavaScript
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
        });

        let connectionStatus = 'disconnected'; // disconnected, connecting, connected
        let currentUser = null;
        let qrCodeInterval;

        function initializeApp() {
            checkAuthStatus();
            setupLoginForm();
            setupNavigation();
            setupSidebarToggle();
            setupSettingsTabs();
            setupResponsive();
            setupWhatsAppConnection();
            setupLogout();
            loadInitialData();
            setupRealTimeUpdates();
        }

        // Authentication
        function checkAuthStatus() {
            const savedAuth = localStorage.getItem('whatsapp-hub-auth');
            const savedUser = localStorage.getItem('whatsapp-hub-user');
            
            if (savedAuth === 'true' && savedUser) {
                currentUser = JSON.parse(savedUser);
                showMainApp();
            } else {
                showLoginPage();
            }
        }

        function setupLoginForm() {
            const loginForm = document.getElementById('login-form');
            const togglePassword = document.getElementById('toggle-password');
            const passwordInput = document.getElementById('password');

            // Toggle password visibility
            togglePassword.addEventListener('click', function() {
                const type = passwordInput.getAttribute('type') === 'password' ? 'text' : 'password';
                passwordInput.setAttribute('type', type);
                
                const icon = this.querySelector('i');
                icon.classList.toggle('fa-eye');
                icon.classList.toggle('fa-eye-slash');
            });

            // Handle form submission
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                handleLogin();
            });
        }

        function handleLogin() {
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            const loginBtn = document.getElementById('login-btn');
            const loginText = document.getElementById('login-text');
            const loginLoading = document.getElementById('login-loading');
            const errorContainer = document.getElementById('error-container');

            // Clear previous errors
            errorContainer.innerHTML = '';

            // Show loading state
            loginText.classList.add('hidden');
            loginLoading.classList.remove('hidden');
            loginBtn.disabled = true;

            // Simulate authentication delay
            setTimeout(() => {
                // Check credentials
                if (email === 'admin@wahub.com' && password === '123456') {
                    // Success
                    currentUser = {
                        id: 1,
                        name: 'João Silva',
                        email: email,
                        avatar: 'JS',
                        plan: 'Pro'
                    };

                    // Save to localStorage
                    localStorage.setItem('whatsapp-hub-auth', 'true');
                    localStorage.setItem('whatsapp-hub-user', JSON.stringify(currentUser));

                    // Show main app
                    showMainApp();
                } else {
                    // Error
                    showError('Email ou senha incorretos. Use admin@wahub.com e 123456');
                }

                // Reset button state
                loginText.classList.remove('hidden');
                loginLoading.classList.add('hidden');
                loginBtn.disabled = false;
            }, 1500);
        }

        function showError(message) {
            const errorContainer = document.getElementById('error-container');
            errorContainer.innerHTML = `<div class="error-message">${message}</div>`;
        }

        function showLoginPage() {
            document.getElementById('login-page').classList.remove('hidden');
            document.getElementById('main-app').classList.add('hidden');
        }

        function showMainApp() {
            document.getElementById('login-page').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');
            
            // Update user name in header
            if (currentUser) {
                document.getElementById('user-name').textContent = currentUser.name;
            }
        }

        function setupLogout() {
            const logoutBtn = document.getElementById('logout-btn');
            logoutBtn.addEventListener('click', function() {
                // Clear localStorage
                localStorage.removeItem('whatsapp-hub-auth');
                localStorage.removeItem('whatsapp-hub-user');
                
                // Reset state
                currentUser = null;
                connectionStatus = 'disconnected';
                
                // Show login page
                showLoginPage();
                
                // Reset form
                document.getElementById('login-form').reset();
            });
        }

        // Navigation System
        function setupNavigation() {
            const navItems = document.querySelectorAll('.nav-item');
            const tabContents = document.querySelectorAll('.tab-content');
            
            navItems.forEach(item => {
                item.addEventListener('click', function() {
                    const targetTab = this.getAttribute('data-tab');
                    
                    navItems.forEach(nav => nav.classList.remove('active'));
                    this.classList.add('active');
                    
                    tabContents.forEach(content => content.classList.remove('active'));
                    
                    const targetContent = document.getElementById(targetTab + '-tab');
                    if (targetContent) {
                        targetContent.classList.add('active');
                        targetContent.classList.add('fade-in');
                        
                        setTimeout(() => {
                            targetContent.classList.remove('fade-in');
                        }, 300);
                    }
                    
                    updatePageTitle(targetTab);
                    loadTabData(targetTab);
                });
            });
        }

        // Sidebar Toggle
        function setupSidebarToggle() {
            const sidebarToggle = document.getElementById('sidebar-toggle');
            const sidebar = document.getElementById('sidebar');
            const mainContent = document.getElementById('main-content');
            const mobileOverlay = document.getElementById('mobile-overlay');
            
            sidebarToggle.addEventListener('click', function() {
                if (window.innerWidth <= 1024) {
                    sidebar.classList.toggle('open');
                    mobileOverlay.classList.toggle('hidden');
                } else {
                    sidebar.classList.toggle('collapsed');
                    mainContent.classList.toggle('sidebar-collapsed');
                }
            });
            
            mobileOverlay.addEventListener('click', function() {
                sidebar.classList.remove('open');
                mobileOverlay.classList.add('hidden');
            });
        }

        // Settings Tabs
        function setupSettingsTabs() {
            const settingsTabBtns = document.querySelectorAll('.settings-tab-btn');
            const settingsContents = document.querySelectorAll('.settings-content');
            
            settingsTabBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    const targetTab = this.getAttribute('data-settings-tab');
                    
                    settingsTabBtns.forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    
                    settingsContents.forEach(content => content.classList.remove('active'));
                    
                    const targetContent = document.getElementById(targetTab + '-settings');
                    if (targetContent) {
                        targetContent.classList.add('active');
                    }
                });
            });
        }

        // WhatsApp Connection
        function setupWhatsAppConnection() {
            const connectBtn = document.getElementById('connect-btn');
            const disconnectBtn = document.getElementById('disconnect-btn');
            
            if (connectBtn) connectBtn.addEventListener('click', initiateConnection);
            if (disconnectBtn) disconnectBtn.addEventListener('click', disconnect);
        }

        function initiateConnection() {
            updateConnectionUI('connecting');
            generateQRCode();
            
            // Simulate connection process
            setTimeout(() => {
                updateConnectionUI('connected');
                updateWhatsAppStatus('connected');
                showNotification('WhatsApp conectado com sucesso!', 'success');
            }, 5000);
        }

        function disconnect() {
            connectionStatus = 'disconnected';
            updateConnectionUI('disconnected');
            updateWhatsAppStatus('disconnected');
            showNotification('WhatsApp desconectado', 'info');
        }

        function updateConnectionUI(status) {
            connectionStatus = status;
            const icon = document.getElementById('connection-icon');
            const title = document.getElementById('connection-title');
            const description = document.getElementById('connection-description');
            const connectBtn = document.getElementById('connect-btn');
            const disconnectBtn = document.getElementById('disconnect-btn');
            const qrContainer = document.getElementById('qr-container');
            const connectedInfo = document.getElementById('connected-info');
            
            if (!icon || !title || !description) return;
            
            switch(status) {
                case 'disconnected':
                    icon.className = 'fas fa-wifi-slash text-gray-400 text-2xl';
                    title.textContent = 'WhatsApp Desconectado';
                    description.textContent = 'Conecte sua conta WhatsApp para começar a receber mensagens';
                    if (connectBtn) connectBtn.style.display = 'flex';
                    if (disconnectBtn) disconnectBtn.style.display = 'none';
                    if (qrContainer) qrContainer.style.display = 'none';
                    if (connectedInfo) connectedInfo.style.display = 'none';
                    break;
                    
                case 'connecting':
                    icon.className = 'fas fa-qrcode text-blue-600 text-2xl';
                    title.textContent = 'Escaneie o QR Code';
                    description.textContent = 'Abra o WhatsApp no seu celular e escaneie o código abaixo';
                    if (connectBtn) connectBtn.style.display = 'none';
                    if (disconnectBtn) disconnectBtn.style.display = 'none';
                    if (qrContainer) qrContainer.style.display = 'block';
                    if (connectedInfo) connectedInfo.style.display = 'none';
                    break;
                    
                case 'connected':
                    icon.className = 'fas fa-check-circle text-green-600 text-2xl';
                    title.textContent = 'WhatsApp Conectado';
                    description.textContent = 'Sua conta está conectada e funcionando perfeitamente';
                    if (connectBtn) connectBtn.style.display = 'none';
                    if (disconnectBtn) disconnectBtn.style.display = 'block';
                    if (qrContainer) qrContainer.style.display = 'none';
                    if (connectedInfo) connectedInfo.style.display = 'block';
                    break;
            }
        }

        function generateQRCode() {
            const canvas = document.getElementById('qr-canvas');
            if (!canvas) return;
            
            const ctx = canvas.getContext('2d');
            
            // Clear canvas
            ctx.clearRect(0, 0, 256, 256);
            
            // Simulate QR Code pattern
            ctx.fillStyle = '#000000';
            const size = 8;
            
            for(let i = 0; i < 32; i++) {
                for(let j = 0; j < 32; j++) {
                    if(Math.random() > 0.5) {
                        ctx.fillRect(i * size, j * size, size, size);
                    }
                }
            }
            
            // Add QR Code corners
            ctx.fillRect(0, 0, 7*size, 7*size);
            ctx.fillRect(25*size, 0, 7*size, 7*size);
            ctx.fillRect(0, 25*size, 7*size, 7*size);
            
            ctx.fillStyle = '#ffffff';
            ctx.fillRect(size, size, 5*size, 5*size);
            ctx.fillRect(26*size, size, 5*size, 5*size);
            ctx.fillRect(size, 26*size, 5*size, 5*size);
            
            ctx.fillStyle = '#000000';
            ctx.fillRect(2*size, 2*size, 3*size, 3*size);
            ctx.fillRect(27*size, 2*size, 3*size, 3*size);
            ctx.fillRect(2*size, 27*size, 3*size, 3*size);
        }

        function updateWhatsAppStatus(status) {
            const statusElement = document.getElementById('whatsapp-status');
            if (!statusElement) return;
            
            const statusDot = statusElement.querySelector('div');
            const statusText = statusElement.querySelector('span');
            
            if (status === 'connected') {
                statusElement.className = 'connection-status status-connected';
                statusDot.className = 'w-3 h-3 bg-green-500 rounded-full';
                statusText.textContent = 'WhatsApp Conectado';
            } else {
                statusElement.className = 'connection-status status-disconnected';
                statusDot.className = 'w-3 h-3 bg-red-500 rounded-full';
                statusText.textContent = 'WhatsApp Desconectado';
            }
        }

        // Responsive Behavior
        function setupResponsive() {
            window.addEventListener('resize', function() {
                const sidebar = document.getElementById('sidebar');
                const mobileOverlay = document.getElementById('mobile-overlay');
                
                if (window.innerWidth > 1024) {
                    sidebar.classList.remove('open');
                    mobileOverlay.classList.add('hidden');
                }
            });
        }

        // Chat Functions
        function insertSuggestion(element) {
            const messageInput = document.getElementById('message-input');
            if (messageInput) {
                messageInput.value = element.textContent.trim();
                messageInput.focus();
            }
        }

        function sendMessage() {
            const messageInput = document.getElementById('message-input');
            if (!messageInput) return;
            
            const message = messageInput.value.trim();
            if (message) {
                // Add message to chat (simplified)
                console.log('Sending message:', message);
                messageInput.value = '';
                showNotification('Mensagem enviada!', 'success');
            }
        }

        // Data Loading Functions
        function loadInitialData() {
            loadDashboardStats();
            loadRecentActivities();
            loadConversations();
            loadReminders();
            loadReports();
        }

        function loadDashboardStats() {
            // Simulate loading dashboard statistics
            console.log('Loading dashboard stats...');
        }

        function loadRecentActivities() {
            // Simulate loading recent activities
            console.log('Loading recent activities...');
        }

        function loadConversations() {
            // Simulate loading conversations
            console.log('Loading conversations...');
        }

        function loadReminders() {
            // Simulate loading reminders
            console.log('Loading reminders...');
        }

        function loadReports() {
            // Simulate loading reports
            console.log('Loading reports...');
        }

        function loadTabData(tabName) {
            switch(tabName) {
                case 'dashboard':
                    loadDashboardStats();
                    break;
                case 'conversations':
                    loadConversations();
                    break;
                case 'reminders':
                    loadReminders();
                    break;
                case 'reports':
                    loadReports();
                    break;
                case 'settings':
                    loadSettings();
                    break;
            }
        }

        function loadSettings() {
            console.log('Loading settings...');
        }

        // Real-time Updates (Simulated)
        function setupRealTimeUpdates() {
            setInterval(() => {
                updateMessageCount();
                updateOnlineStatus();
            }, 30000);
            
            setInterval(() => {
                updateNotifications();
            }, 60000);
        }

        function updateMessageCount() {
            const badge = document.querySelector('.bg-red-500.text-white');
            if (badge && Math.random() > 0.8) {
                const currentCount = parseInt(badge.textContent || '0');
                const newCount = currentCount + 1;
                badge.textContent = newCount;
                badge.classList.add('pulse');
                setTimeout(() => {
                    badge.classList.remove('pulse');
                }, 2000);
            }
        }

        function updateOnlineStatus() {
            console.log('Updating online status...');
        }

        function updateNotifications() {
            if (Math.random() > 0.7) {
                showNotification('Nova mensagem recebida!', 'info');
            }
        }

        // Utility Functions
        function updatePageTitle(tabName) {
            const titles = {
                dashboard: 'Painel de Controle',
                conversations: 'Conversas',
                reminders: 'Lembretes',
                reports: 'Relatórios',
                settings: 'Configurações'
            };
            
            document.title = `${titles[tabName] || 'WhatsApp Business Hub'} - WhatsApp Business Hub`;
        }

        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = `fixed top-20 right-4 p-4 rounded-lg shadow-lg z-50 ${getNotificationClass(type)}`;
            notification.innerHTML = `
                <div class="flex items-center space-x-2">
                    <i class="fas ${getNotificationIcon(type)}"></i>
                    <span>${message}</span>
                    <button onclick="this.parentElement.parentElement.remove()" class="ml-2">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
            `;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                if (notification.parentElement) {
                    notification.remove();
                }
            }, 5000);
        }

        function getNotificationClass(type) {
            const classes = {
                info: 'bg-blue-500 text-white',
                success: 'bg-green-500 text-white',
                warning: 'bg-yellow-500 text-white',
                error: 'bg-red-500 text-white'
            };
            return classes[type] || classes.info;
        }

        function getNotificationIcon(type) {
            const icons = {
                info: 'fa-info-circle',
                success: 'fa-check-circle',
                warning: 'fa-exclamation-triangle',
                error: 'fa-times-circle'
            };
            return icons[type] || icons.info;
        }

        // Keyboard shortcuts
        document.addEventListener('keydown', function(e) {
            // Ctrl/Cmd + K for search
            if ((e.ctrlKey || e.metaKey) && e.key === 'k') {
                e.preventDefault();
                const searchInput = document.querySelector('input[placeholder*="Buscar"]');
                if (searchInput) {
                    searchInput.focus();
                }
            }
            
            // Escape to close mobile sidebar
            if (e.key === 'Escape') {
                const overlay = document.getElementById('mobile-overlay');
                const sidebar = document.getElementById('sidebar');
                if (overlay && !overlay.classList.contains('hidden')) {
                    sidebar.classList.remove('open');
                    overlay.classList.add('hidden');
                }
            }

            // Enter to send message in chat
            if (e.key === 'Enter' && e.target.id === 'message-input') {
                e.preventDefault();
                sendMessage();
            }
        });

        // Global WhatsApp Hub object
        window.WhatsAppHub = {
            showNotification,
            updateConnectionUI,
            connectionStatus: () => connectionStatus,
            currentUser: () => currentUser
        };
    </script>
</body>
</html>

