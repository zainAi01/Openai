<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Chat Pro - Your Advanced AI Assistant</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        * {
            font-family: 'Inter', sans-serif;
        }
        
        .gradient-bg {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        
        .glass {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .message-bubble {
            max-width: 80%;
            margin: 8px 0;
            padding: 16px 20px;
            border-radius: 20px;
            position: relative;
        }
        
        .user-message {
            margin-left: auto;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }
        
        .ai-message {
            background: rgba(255, 255, 255, 0.9);
            color: #1f2937;
            border: 1px solid rgba(0, 0, 0, 0.1);
        }
        
        .typing-indicator {
            display: inline-flex;
            align-items: center;
        }
        
        .typing-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            margin: 0 2px;
            background: #667eea;
            animation: typing 1.4s infinite;
        }
        
        .typing-dot:nth-child(2) { animation-delay: 0.2s; }
        .typing-dot:nth-child(3) { animation-delay: 0.4s; }
        
        @keyframes typing {
            0%, 60%, 100% { transform: scale(1); opacity: 0.4; }
            30% { transform: scale(1.2); opacity: 1; }
        }
        
        .glow {
            box-shadow: 0 0 20px rgba(102, 126, 234, 0.4);
        }
    </style>
</head>
<body class="min-h-screen gradient-bg overflow-hidden">
    <!-- Animated Background -->
    <div id="bg-animation" class="fixed inset-0 z-0 opacity-30"></div>
    
    <!-- Main Container -->
    <div class="relative z-10 flex flex-col h-screen max-w-6xl mx-auto">
        <!-- Header -->
        <header class="glass p-6 sticky top-0 z-20 backdrop-blur-md">
            <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                    <div class="w-12 h-12 bg-white/20 rounded-2xl flex items-center justify-center glow">
                        <i class="fas fa-brain text-white text-xl"></i>
                    </div>
                    <div>
                        <h1 class="text-2xl font-bold text-white">AI Chat Pro</h1>
                        <p class="text-white/70 text-sm">Advanced AI Assistant</p>
                    </div>
                </div>
                <div class="flex items-center space-x-4">
                    <button id="theme-toggle" class="p-2 text-white/70 hover:text-white transition-all">
                        <i class="fas fa-moon"></i>
                    </button>
                    <button class="px-6 py-2 bg-white/20 backdrop-blur-sm rounded-xl text-white font-medium hover:bg-white/30 transition-all">
                        Upgrade to Pro
                    </button>
                </div>
            </div>
        </header>

        <!-- Chat Container -->
        <div class="flex-1 flex overflow-hidden">
            <!-- Sidebar -->
            <div class="w-80 glass border-r border-white/20 p-6 hidden lg:block">
                <div class="space-y-4">
                    <div class="flex items-center space-x-3 p-3 bg-white/10 rounded-xl">
                        <i class="fas fa-history text-white/80"></i>
                        <span class="text-white font-medium">New Chat</span>
                    </div>
                    
                    <div class="space-y-2">
                        <h3 class="text-white/80 font-semibold text-sm uppercase tracking-wide">Recent Chats</h3>
                        <div id="chat-history" class="space-y-2 max-h-96 overflow-y-auto">
                            <!-- Chat history items will be populated here -->
                        </div>
                    </div>
                    
                    <div class="pt-4 border-t border-white/20">
                        <div class="flex items-center space-x-3 p-3 bg-white/10 rounded-xl cursor-pointer hover:bg-white/20">
                            <i class="fas fa-cog text-white/80"></i>
                            <span class="text-white font-medium">Settings</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Main Chat Area -->
            <div class="flex-1 flex flex-col">
                <!-- Messages Container -->
                <div id="messages-container" class="flex-1 overflow-y-auto p-8 space-y-6 scrollbar-thin scrollbar-thumb-white/20 scrollbar-track-transparent">
                    <!-- Welcome Message -->
                    <div class="text-center py-20">
                        <div class="w-24 h-24 mx-auto mb-6 bg-white/20 rounded-3xl flex items-center justify-center glow">
                            <i class="fas fa-robot text-3xl text-white"></i>
                        </div>
                        <h2 class="text-3xl font-bold text-white mb-4">Welcome to AI Chat Pro</h2>
                        <p class="text-xl text-white/80 mb-8 max-w-md mx-auto">
                            Ask me anything. I'm here to help with coding, writing, analysis, and more.
                        </p>
                        <div class="flex flex
