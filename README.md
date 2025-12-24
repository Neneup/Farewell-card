<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Farewell Card - To PC Team</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;700&display=swap" rel="stylesheet">
    
    <style>
        body { font-family: 'Sarabun', sans-serif; }
        
        /* Custom Animations */
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        .animate-float { animation: float 3s ease-in-out infinite; }
        
        @keyframes bounce-slow {
            0%, 100% { transform: translateY(-5%); }
            50% { transform: translateY(5%); }
        }
        .animate-bounce-slow { animation: bounce-slow 2s infinite ease-in-out; }
        
        @keyframes fade-in {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in { animation: fade-in 0.5s ease-out forwards; }

        @keyframes pop-in {
            0% { transform: scale(0); }
            80% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        .animate-pop-in { animation: pop-in 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards; }
    </style>
</head>
<body class="bg-orange-50 min-h-screen flex items-center justify-center p-4 text-slate-700 select-none">

    <!-- Main Card Container -->
    <div id="card-container" class="w-full max-w-md bg-white rounded-3xl shadow-xl overflow-hidden border-4 border-white relative min-h-[700px] flex flex-col transition-all duration-500">
        
        <!-- Decorative Background (Fixed) -->
        <div class="absolute top-0 left-0 w-full h-full overflow-hidden pointer-events-none z-0">
            <div class="absolute top-10 left-10 text-pink-200 animate-pulse"><i data-lucide="heart" width="40" height="40" fill="#fbcfe8"></i></div>
            <div class="absolute bottom-20 right-10 text-purple-200 animate-bounce"><i data-lucide="star" width="30" height="30" fill="#e9d5ff"></i></div>
            <div class="absolute top-1/2 left-[-20px] w-32 h-32 bg-yellow-100 rounded-full blur-2xl opacity-60"></div>
            <div class="absolute bottom-0 right-[-20px] w-40 h-40 bg-blue-100 rounded-full blur-2xl opacity-60"></div>
        </div>

        <!-- Content Area -->
        <div id="app-content" class="relative z-10 flex-1 flex flex-col items-center justify-center p-6 text-center w-full">
            <!-- Dynamic Content will be injected here by JavaScript -->
        </div>

    </div>

    <!-- JavaScript Logic -->
    <script>
        // State Variables
        let currentState = 'start'; // start, moving, game, finish
        let collectedCount = 0;
        const totalItems = 5;
        const collectedItems = new Set();
        let progress = 0;

        // Memory Items Configuration
        const memoryItems = [
            { id: 1, icon: 'heart', color: 'text-pink-500', x: '20%', y: '30%', delay: '0s' },
            { id: 2, icon: 'star', color: 'text-yellow-500', x: '70%', y: '20%', delay: '0.5s' },
            { id: 3, icon: 'coffee', color: 'text-orange-500', x: '40%', y: '60%', delay: '1s' },
            { id: 4, icon: 'music', color: 'text-purple-500', x: '80%', y: '50%', delay: '0.2s' },
            { id: 5, icon: 'camera', color: 'text-blue-500', x: '15%', y: '70%', delay: '0.8s' },
        ];

        // Main Render Function
        function render() {
            const container = document.getElementById('app-content');
            container.innerHTML = ''; // Clear previous content

            if (currentState === 'start') {
                container.innerHTML = `
                    <div class="animate-fade-in flex flex-col items-center gap-6 w-full">
                        <div class="bg-blue-100 p-4 rounded-full mb-2 shadow-sm border-2 border-blue-200">
                            <i data-lucide="briefcase" size="48" class="text-blue-500 w-12 h-12"></i>
                        </div>
                        
                        <h1 class="text-2xl font-bold text-slate-700">Planning Dept. (PC)</h1>
                        <div class="bg-green-100 px-4 py-2 rounded-lg text-green-700 font-bold border-2 border-green-200 flex items-center gap-2">
                            <i data-lucide="sparkles" size="18"></i> Mission Completed!
                        </div>

                        <div class="bg-slate-50 p-6 rounded-2xl border-2 border-slate-100 shadow-inner w-full">
                            <p class="text-slate-600 mb-2 font-bold">My Status:</p>
                            <div class="space-y-2 text-sm text-left px-4">
                                <div class="flex justify-between border-b border-slate-200 pb-1">
                                    <span>Exp. Gained</span>
                                    <span class="font-bold text-blue-500">MAXIMUM</span>
                                </div>
                                <div class="flex justify-between border-b border-slate-200 pb-1">
                                    <span>Friendship</span>
                                    <span class="font-bold text-pink-500">FOREVER</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Next Destination</span>
                                    <span class="font-bold text-purple-500">HR Dept.</span>
                                </div>
                            </div>
                        </div>

                        <p class="text-slate-500 text-sm mt-2">ขอบคุณสำหรับการเดินทางที่ผ่านมา...</p>

                        <button onclick="startJourney()" class="group relative bg-gradient-to-r from-blue-400 to-indigo-400 text-white font-bold py-3 px-8 rounded-full shadow-lg hover:shadow-xl active:scale-95 transition-all duration-300 flex items-center gap-2 mt-4">
                            Send Last Message <i data-lucide="arrow-right" size="20"></i>
                        </button>
                    </div>
                `;
            } else if (currentState === 'moving') {
                container.innerHTML = `
                    <div class="w-full flex flex-col items-center gap-8 animate-fade-in">
                        <h2 class="text-xl font-bold text-slate-600 animate-pulse">Packing Memories...</h2>
                        
                        <div class="relative w-full h-32 flex items-center justify-between px-2">
                            <!-- Line -->
                            <div class="absolute top-1/2 left-0 w-full h-2 bg-slate-100 rounded-full z-0"></div>
                            <div id="progress-bar" class="absolute top-1/2 left-0 h-2 bg-gradient-to-r from-blue-300 to-pink-300 rounded-full z-0 transition-all duration-100 ease-linear" style="width: ${progress}%"></div>

                            <!-- Nodes -->
                            <div class="z-10 bg-blue-100 p-2 rounded-full border-4 border-white shadow-md">
                                <i data-lucide="briefcase" size="24" class="text-blue-400"></i>
                            </div>
                            <div class="z-10 bg-pink-100 p-2 rounded-full border-4 border-white shadow-md">
                                <i data-lucide="heart" size="24" class="text-pink-400"></i>
                            </div>

                            <!-- Character Avatar -->
                            <div id="character" class="absolute top-1/2 -mt-8 z-20 transition-all duration-100 ease-linear flex flex-col items-center" style="left: calc(${progress}% - 24px)">
                                <div class="w-12 h-12 bg-white rounded-full border-2 border-pink-300 shadow-lg flex items-center justify-center animate-bounce">
                                    <span class="text-2xl">🎒</span>
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            } else if (currentState === 'game') {
                let itemsHtml = '';
                if (collectedCount < totalItems) {
                    itemsHtml = memoryItems.map(item => {
                        if (collectedItems.has(item.id)) return '';
                        return `
                            <button onclick="collectItem(${item.id})" 
                                class="absolute p-3 bg-white rounded-full shadow-md active:scale-95 transition-transform duration-200 cursor-pointer animate-float hover:scale-110"
                                style="left: ${item.x}; top: ${item.y}; animation-delay: ${item.delay};">
                                <i data-lucide="${item.icon}" size="24" class="${item.color}"></i>
                            </button>
                        `;
                    }).join('');
                } else {
                    itemsHtml = `
                        <div class="w-full h-full flex flex-col items-center justify-center animate-pop-in">
                            <i data-lucide="gift" size="64" class="text-pink-500 mb-2"></i>
                            <span class="text-lg font-bold text-slate-600">All Collected!</span>
                        </div>
                    `;
                }

                container.innerHTML = `
                    <div class="w-full h-full flex flex-col items-center justify-between py-4 animate-fade-in relative">
                        <div class="z-20 text-center">
                            <h2 class="text-xl font-bold text-slate-700 mb-1">Collect Happy Memories!</h2>
                            <p class="text-slate-500 text-sm">แตะที่ไอคอนเพื่อเก็บความทรงจำ (${collectedCount}/${totalItems})</p>
                        </div>

                        <!-- Game Area -->
                        <div class="relative w-full h-64 bg-slate-50 rounded-2xl border-2 border-dashed border-blue-200 mt-4 overflow-hidden shadow-inner">
                            ${itemsHtml}
                        </div>

                        <div class="h-16 flex items-end justify-center z-20 w-full">
                            ${collectedCount >= totalItems ? `
                                <button onclick="finishGame()" class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-8 rounded-full shadow-lg transition-all animate-bounce w-3/4">
                                    Open Greeting Card <i data-lucide="arrow-right" class="inline ml-1"></i>
                                </button>
                            ` : ''}
                        </div>
                    </div>
                `;
            } else if (currentState === 'finish') {
                container.innerHTML = `
                    <div class="animate-fade-in flex flex-col items-center w-full h-full pb-4 overflow-y-auto">
                        
                        <div class="flex items-center gap-2 mb-4 bg-purple-100 text-purple-600 px-4 py-1 rounded-full text-sm font-bold border border-purple-200 shrink-0">
                            <i data-lucide="trophy" size="16"></i> To: PC Team
                        </div>

                        <!-- Photo Frame -->
                        <div class="relative mb-6 group shrink-0">
                            <div class="absolute -inset-1 bg-gradient-to-r from-blue-200 via-purple-200 to-pink-200 rounded-[2rem] blur opacity-75"></div>
                            <div class="relative w-48 h-48 bg-white rounded-[1.7rem] p-3 shadow-xl transform rotate-[2deg] hover:rotate-0 transition-all duration-500">
                                <div class="w-full h-full rounded-2xl overflow-hidden bg-slate-100 relative">
                                    <img src="1000013930.jpg" alt="Memory" class="w-full h-full object-cover" onerror="this.style.display='none'; this.parentElement.innerHTML='<div class=\'w-full h-full flex flex-col items-center justify-center text-purple-300 bg-purple-50\'><i data-lucide=\'image\' size=\'40\'></i><span class=\'text-xs mt-2\'>No Image Found</span></div>'">
                                </div>
                            </div>
                        </div>

                        <!-- Message Card -->
                        <div class="bg-white/90 backdrop-blur-sm p-5 rounded-2xl border border-white shadow-lg w-full mb-4 relative overflow-hidden text-left">
                            <div class="absolute top-0 left-0 w-full h-1 bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400"></div>
                            
                            <h3 class="text-lg font-bold text-slate-800 mb-3 flex items-center justify-center gap-2">
                            💌 ถึง ทีม PC มืออาชีพ
                            </h3>
                            
                            <div class="text-slate-600 text-sm font-medium space-y-3 leading-relaxed">
                                <p class="text-center">
                                    "แม้จะย้ายไปที่ใหม่...
                                    แต่ยังเป็นกำลังใจให้ <span class="text-blue-600 font-bold">ทุกคน</span> เสมอ
                                    และเชื่อมั่นว่าทีม PC ทุกคน
                                    จะก้าวหน้าและพัฒนาต่อไปอย่างไม่หยุดยั้ง"
                                </p>
                                
                                <div class="w-full h-px bg-slate-100 my-2"></div>

                                <p class="indent-4">
                                    "ขอบคุณสำหรับช่วงเวลาดีๆ และมิตรภาพที่อบอุ่น การได้ร่วมงานกับทุกคนคือประสบการณ์ที่มีคุณค่า"
                                </p>

                                <p class="text-center font-bold text-pink-500 mt-2">
                                    "นี่ไม่ใช่การบอกลา (Goodbye)<br/> 
                                    แต่เป็นแล้วพบกันใหม่ (See you again)<br/> 
                                    ขอบคุณค่ะ"
                                </p>
                            </div>
                        </div>

                        <button onclick="resetCard()" class="text-slate-400 text-xs hover:text-blue-500 transition-colors flex items-center gap-1 shrink-0 pb-2 cursor-pointer">
                            <i data-lucide="rotate-ccw" size="14"></i> Replay Message
                        </button>

                    </div>
                `;
            }

            // Re-initialize icons after DOM update
            lucide.createIcons();
        }

        // Action Functions
        function startJourney() {
            currentState = 'moving';
            render();
            let p = 0;
            const interval = setInterval(() => {
                p += 1.5; // speed
                progress = p;
                
                // Update DOM directly for smooth animation without full re-render
                const bar = document.getElementById('progress-bar');
                const char = document.getElementById('character');
                if(bar && char) {
                    bar.style.width = p + '%';
                    char.style.left = `calc(${p}% - 24px)`;
                }

                if (p >= 100) {
                    clearInterval(interval);
                    setTimeout(() => {
                        currentState = 'game';
                        render();
                    }, 300);
                }
            }, 30);
        }

        function collectItem(id) {
            collectedItems.add(id);
            collectedCount = collectedItems.size;
            render();
        }

        function finishGame() {
            currentState = 'finish';
            render();
        }

        function resetCard() {
            currentState = 'start';
            progress = 0;
            collectedCount = 0;
            collectedItems.clear();
            render();
        }

        // Initial Render
        window.onload = render;

    </script>
</body>
</html>

