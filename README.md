<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Daze App Ecosystem Tree</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            font-family: 'Space Grotesk', sans-serif;
        }
        
        .tree-container {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            min-height: 100vh;
            position: relative;
            overflow: hidden;
        }
        
        .tree-container::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(56, 189, 248, 0.1) 0%, transparent 70%);
            animation: pulse 4s ease-in-out infinite;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; }
        }
        
        .node {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .node:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
            border-color: rgba(56, 189, 248, 0.5);
        }
        
        .root-node {
            background: linear-gradient(135deg, rgba(56, 189, 248, 0.2), rgba(139, 92, 246, 0.2));
            border: 2px solid rgba(56, 189, 248, 0.5);
            animation: glow 3s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from { box-shadow: 0 0 20px rgba(56, 189, 248, 0.3); }
            to { box-shadow: 0 0 40px rgba(139, 92, 246, 0.4); }
        }
        
        .product-node {
            background: linear-gradient(135deg, rgba(30, 41, 59, 0.9), rgba(51, 65, 85, 0.9));
        }
        
        .sub-node {
            background: rgba(15, 23, 42, 0.8);
            border-left: 3px solid;
        }
        
        .connector {
            stroke: rgba(148, 163, 184, 0.3);
            stroke-width: 2;
            fill: none;
            stroke-dasharray: 5,5;
            animation: dash 20s linear infinite;
        }
        
        @keyframes dash {
            to { stroke-dashoffset: -100; }
        }
        
        .flow-particle {
            fill: #38bdf8;
            filter: drop-shadow(0 0 6px #38bdf8);
        }
        
        .integration-badge {
            background: linear-gradient(90deg, #f59e0b, #d97706);
            animation: shimmer 2s infinite;
        }
        
        @keyframes shimmer {
            0% { background-position: -200% center; }
            100% { background-position: 200% center; }
        }
        
        .expand-icon {
            transition: transform 0.3s ease;
        }
        
        .expanded .expand-icon {
            transform: rotate(180deg);
        }
        
        .children-container {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s cubic-bezier(0, 1, 0, 1);
        }
        
        .children-container.open {
            max-height: 1000px;
            transition: max-height 0.5s ease-in-out;
        }
        
        .tech-stack-tag {
            font-size: 0.7rem;
            letter-spacing: 0.05em;
            text-transform: uppercase;
        }
    </style>
</head>
<body class="tree-container text-white p-8">
    <div class="max-w-6xl mx-auto relative z-10">
        <h1 class="text-4xl font-bold text-center mb-12 bg-clip-text text-transparent bg-gradient-to-r from-cyan-400 to-purple-400">
            Daze App Ecosystem Architecture
        </h1>
        
        <div class="flex flex-col items-center space-y-8">
            <!-- Root Node -->
            <div class="root-node node rounded-2xl p-8 w-full max-w-2xl text-center cursor-pointer" onclick="toggleRoot()">
                <div class="flex items-center justify-center space-x-4 mb-4">
                    <svg class="w-10 h-10 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z"></path>
                    </svg>
                    <h2 class="text-3xl font-bold">Daze App</h2>
                </div>
                <p class="text-gray-300 mb-4">Web & Mobile Hospitality Platform</p>
                <div class="flex justify-center space-x-4 text-sm">
                    <span class="px-3 py-1 rounded-full bg-cyan-500/20 text-cyan-300 border border-cyan-500/30">POS Integration</span>
                    <span class="px-3 py-1 rounded-full bg-purple-500/20 text-purple-300 border border-purple-500/30">PMS Integration</span>
                    <span class="px-3 py-1 rounded-full bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">KDS Flow</span>
                </div>
                <div class="mt-4 flex justify-center">
                    <svg id="root-expand" class="expand-icon w-6 h-6 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </div>
            </div>

            <!-- SVG Connector -->
            <svg class="w-full h-16" style="max-width: 100px;">
                <line x1="50%" y1="0" x2="50%" y2="100%" class="connector"/>
                <circle cx="50%" cy="50%" r="3" class="flow-particle">
                    <animate attributeName="cy" values="0;100%;0" dur="3s" repeatCount="indefinite"/>
                </circle>
            </svg>

            <!-- Products Container -->
            <div id="products" class="children-container open w-full">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8 w-full">
                    
                    <!-- Product 1: In-Room Dining -->
                    <div class="flex flex-col items-center space-y-4">
                        <div class="product-node node rounded-xl p-6 w-full cursor-pointer group" onclick="toggleProduct('ird')">
                            <div class="flex items-center justify-between mb-3">
                                <div class="p-3 rounded-lg bg-orange-500/20 text-orange-400">
                                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
                                    </svg>
                                </div>
                                <svg id="icon-ird" class="expand-icon w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                                </svg>
                            </div>
                            <h3 class="text-xl font-semibold mb-2">In-Room Dining</h3>
                            <p class="text-sm text-gray-400 mb-3">Direct room service ordering</p>
                            <div class="tech-stack-tag text-orange-400">End-to-End Integration</div>
                        </div>
                        
                        <div id="children-ird" class="children-container open w-full space-y-3">
                            <div class="sub-node node rounded-lg p-4 border-l-orange-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-orange-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Guest App</span>
                                </div>
                                <p class="text-xs text-gray-500">Order from room TV or mobile</p>
                            </div>
                            
                            <div class="integration-badge rounded-lg p-3 text-center text-xs font-bold text-white">
                                ↓ Auto-Routes to Kitchen ↓
                            </div>
                            
                            <div class="sub-node node rounded-lg p-4 border-l-orange-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-orange-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path>
                                    </svg>
                                    <span class="font-medium text-sm">KDS Integration</span>
                                </div>
                                <p class="text-xs text-gray-500">Direct kitchen display routing</p>
                            </div>
                            
                            <div class="sub-node node rounded-lg p-4 border-l-orange-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-orange-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Accounting</span>
                                </div>
                                <p class="text-xs text-gray-500">Auto-post to room folio</p>
                            </div>
                        </div>
                    </div>

                    <!-- Product 2: Pool & Beach -->
                    <div class="flex flex-col items-center space-y-4">
                        <div class="product-node node rounded-xl p-6 w-full cursor-pointer group" onclick="toggleProduct('pool')">
                            <div class="flex items-center justify-between mb-3">
                                <div class="p-3 rounded-lg bg-cyan-500/20 text-cyan-400">
                                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"></path>
                                    </svg>
                                </div>
                                <svg id="icon-pool" class="expand-icon w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                                </svg>
                            </div>
                            <h3 class="text-xl font-semibold mb-2">Pool & Beach</h3>
                            <p class="text-sm text-gray-400 mb-3">Location-based delivery</p>
                            <div class="tech-stack-tag text-cyan-400">Courier Network Enabled</div>
                        </div>
                        
                        <div id="children-pool" class="children-container open w-full space-y-3">
                            <div class="sub-node node rounded-lg p-4 border-l-cyan-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Location Selection</span>
                                </div>
                                <p class="text-xs text-gray-500">Umbrella # / Lounger # / Cabana #</p>
                            </div>
                            
                            <div class="sub-node node rounded-lg p-4 border-l-cyan-400 bg-cyan-900/20">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Courier App</span>
                                </div>
                                <p class="text-xs text-gray-500">Dedicated delivery personnel interface</p>
                                <div class="mt-2 flex space-x-2">
                                    <span class="text-[10px] px-2 py-1 rounded bg-cyan-500/20 text-cyan-300">Pickup Alerts</span>
                                    <span class="text-[10px] px-2 py-1 rounded bg-cyan-500/20 text-cyan-300">GPS Navigation</span>
                                </div>
                            </div>
                            
                            <div class="integration-badge rounded-lg p-3 text-center text-xs font-bold text-white">
                                ↓ Order Flow + Delivery Tracking ↓
                            </div>
                            
                            <div class="sub-node node rounded-lg p-4 border-l-cyan-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Delivery Confirmation</span>
                                </div>
                                <p class="text-xs text-gray-500">Photo confirmation / QR scan</p>
                            </div>
                        </div>
                    </div>

                    <!-- Product 3: Table Pay & Order -->
                    <div class="flex flex-col items-center space-y-4">
                        <div class="product-node node rounded-xl p-6 w-full cursor-pointer group" onclick="toggleProduct('table')">
                            <div class="flex items-center justify-between mb-3">
                                <div class="p-3 rounded-lg bg-purple-500/20 text-purple-400">
                                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"></path>
                                    </svg>
                                </div>
                                <svg id="icon-table" class="expand-icon w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                                </svg>
                            </div>
                            <h3 class="text-xl font-semibold mb-2">Table Pay & Order</h3>
                            <p class="text-sm text-gray-400 mb-3">Restaurant/Bar table service</p>
                            <div class="tech-stack-tag text-purple-400">Server Communication Hub</div>
                        </div>
                        
                        <div id="children-table" class="children-container open w-full space-y-3">
                            <div class="sub-node node rounded-lg p-4 border-l-purple-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v1m6 11h2m-6 0h-2v4m0-11v3m0 0h.01M12 12h4.01M16 20h4M4 12h4m12 0h.01M5 8h2a1 1 0 001-1V5a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1zm12 0h2a1 1 0 001-1V5a1 1 0 00-1-1h-2a1 1 0 00-1 1v2a1 1 0 001 1zM5 20h2a1 1 0 001-1v-2a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Table QR/Ordering</span>
                                </div>
                                <p class="text-xs text-gray-500">Scan to order & pay</p>
                            </div>
                            
                            <div class="sub-node node rounded-lg p-4 border-l-purple-400 bg-purple-900/20">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Server App</span>
                                </div>
                                <p class="text-xs text-gray-500">Staff interface for guest communication</p>
                                <div class="mt-2 flex space-x-2">
                                    <span class="text-[10px] px-2 py-1 rounded bg-purple-500/20 text-purple-300">Chat</span>
                                    <span class="text-[10px] px-2 py-1 rounded bg-purple-500/20 text-purple-300">Requests</span>
                                    <span class="text-[10px] px-2 py-1 rounded bg-purple-500/20 text-purple-300">Status Updates</span>
                                </div>
                            </div>
                            
                            <div class="integration-badge rounded-lg p-3 text-center text-xs font-bold text-white">
                                ↓ Real-time Sync ↓
                            </div>
                            
                            <div class="sub-node node rounded-lg p-4 border-l-purple-400">
                                <div class="flex items-center space-x-2 mb-2">
                                    <svg class="w-4 h-4 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z"></path>
                                    </svg>
                                    <span class="font-medium text-sm">Payment Processing</span>
                                </div>
                                <p class="text-xs text-gray-500">Split bills, tips, room charge</p>
                            </div>
                        </div>
                    </div>

                </div>
            </div>

            <!-- Bottom Integration Layer -->
            <div class="w-full mt-8 p-6 rounded-2xl bg-gradient-to-r from-slate-800/50 to-slate-900/50 border border-slate-700 backdrop-blur-sm">
                <h3 class="text-center text-lg font-semibold mb-4 text-gray-300">Universal Integrations</h3>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                    <div class="flex items-center space-x-3 p-3 rounded-lg bg-slate-800/50 border border-slate-700">
                        <div class="w-2 h-2 rounded-full bg-green-400 animate-pulse"></div>
                        <span class="text-sm text-gray-300">POS Systems</span>
                    </div>
                    <div class="flex items-center space-x-3 p-3 rounded-lg bg-slate-800/50 border border-slate-700">
                        <div class="w-2 h-2 rounded-full bg-blue-400 animate-pulse"></div>
                        <span class="text-sm text-gray-300">PMS (Property Mgmt)</span>
                    </div>
                    <div class="flex items-center space-x-3 p-3 rounded-lg bg-slate-800/50 border border-slate-700">
                        <div class="w-2 h-2 rounded-full bg-yellow-400 animate-pulse"></div>
                        <span class="text-sm text-gray-300">Kitchen Display (KDS)</span>
                    </div>
                    <div class="flex items-center space-x-3 p-3 rounded-lg bg-slate-800/50 border border-slate-700">
                        <div class="w-2 h-2 rounded-full bg-pink-400 animate-pulse"></div>
                        <span class="text-sm text-gray-300">Accounting/ERP</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        function toggleRoot() {
            const products = document.getElementById('products');
            const icon = document.getElementById('root-expand');
            products.classList.toggle('open');
            icon.style.transform = products.classList.contains('open') ? 'rotate(180deg)' : 'rotate(0deg)';
        }

        function toggleProduct(product) {
            const children = document.getElementById(`children-${product}`);
            const icon = document.getElementById(`icon-${product}`);
            
            if (children.classList.contains('open')) {
                children.classList.remove('open');
                children.style.maxHeight = '0';
                icon.style.transform = 'rotate(0deg)';
            } else {
                children.classList.add('open');
                children.style.maxHeight = children.scrollHeight + 'px';
                icon.style.transform = 'rotate(180deg)';
            }
        }

        // Initialize all children containers to open state with proper height
        document.addEventListener('DOMContentLoaded', () => {
            ['ird', 'pool', 'table'].forEach(product => {
                const el = document.getElementById(`children-${product}`);
                if (el.classList.contains('open')) {
                    el.style.maxHeight = el.scrollHeight + 'px';
                }
            });
        });
    </script>
</body>
</html>
