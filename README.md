<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Chat - AI Assistant Cerdas</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 900px;
            height: 90vh;
            max-height: 800px;
            background: #1a1a2e;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
            overflow: hidden;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .header p {
            font-size: 14px;
            opacity: 0.9;
        }

        .ai-icon {
            font-size: 30px;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        /* Chat Area */
        .chat-container {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background: #0f0f1e;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .chat-container::-webkit-scrollbar {
            width: 8px;
        }

        .chat-container::-webkit-scrollbar-track {
            background: #1a1a2e;
        }

        .chat-container::-webkit-scrollbar-thumb {
            background: #667eea;
            border-radius: 4px;
        }

        .message {
            display: flex;
            animation: fadeIn 0.3s ease-out;
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

        .message.user {
            justify-content: flex-end;
        }

        .message-content {
            max-width: 70%;
            padding: 12px 16px;
            border-radius: 12px;
            word-wrap: break-word;
            line-height: 1.5;
        }

        .user .message-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-radius: 18px 18px 4px 18px;
        }

        .ai .message-content {
            background: #1a1a2e;
            color: #e0e0e0;
            border: 1px solid #333;
            border-radius: 18px 18px 18px 4px;
            position: relative;
        }

        .message-time {
            font-size: 12px;
            opacity: 0.6;
            margin-top: 5px;
            padding: 0 5px;
        }

        .typing-indicator {
            display: flex;
            gap: 4px;
            padding: 12px 16px;
        }

        .typing-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #667eea;
            animation: typing 1.4s infinite;
        }

        .typing-dot:nth-child(2) {
            animation-delay: 0.2s;
        }

        .typing-dot:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes typing {
            0%, 60%, 100% { transform: translateY(0); }
            30% { transform: translateY(-10px); }
        }

        /* Input Area */
        .input-area {
            background: #1a1a2e;
            padding: 15px;
            border-top: 1px solid #333;
            display: flex;
            gap: 10px;
            align-items: flex-end;
        }

        .input-wrapper {
            flex: 1;
            display: flex;
            gap: 8px;
            align-items: center;
        }

        input {
            flex: 1;
            background: #0f0f1e;
            border: 1px solid #333;
            color: white;
            padding: 12px 15px;
            border-radius: 10px;
            font-size: 14px;
            outline: none;
            transition: all 0.3s;
        }

        input:focus {
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        input::placeholder {
            color: #666;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(102, 126, 234, 0.3);
        }

        .btn:active {
            transform: translateY(0);
        }

        .btn-small {
            padding: 8px 12px;
            font-size: 12px;
            background: #333;
            margin-left: 5px;
        }

        .btn-small:hover {
            background: #444;
        }

        .btn-clear {
            background: #e74c3c;
        }

        /* Welcome Message */
        .welcome {
            text-align: center;
            color: #888;
            padding: 40px 20px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100%;
        }

        .welcome h2 {
            font-size: 28px;
            margin-bottom: 10px;
            color: #667eea;
        }

        .welcome p {
            font-size: 14px;
            line-height: 1.6;
            max-width: 300px;
        }

        .features {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-top: 20px;
            max-width: 300px;
        }

        .feature {
            background: #1a1a2e;
            padding: 10px;
            border-radius: 8px;
            font-size: 12px;
        }

        .feature-icon {
            font-size: 18px;
            margin-bottom: 5px;
        }

        .copy-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #333;
            border: none;
            color: #888;
            padding: 6px 10px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            opacity: 0;
            transition: all 0.3s;
        }

        .ai .message-content:hover .copy-btn {
            opacity: 1;
        }

        .copy-btn:hover {
            background: #667eea;
            color: white;
        }

        @media (max-width: 600px) {
            .container {
                height: 100vh;
                max-height: none;
                border-radius: 0;
            }

            .header h1 {
                font-size: 24px;
            }

            .message-content {
                max-width: 85%;
                font-size: 14px;
            }

            .features {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>
                <span class="ai-icon">🤖</span>
                Smart Chat
            </h1>
            <p>AI Assistant Cerdas Siap Membantu Anda</p>
        </div>

        <div class="chat-container" id="chatContainer">
            <div class="welcome">
                <h2>👋 Halo! Selamat datang</h2>
                <p>Saya adalah Smart Chat AI yang siap membantu menjawab pertanyaan Anda dengan cerdas dan akurat.</p>
                <div class="features">
                    <div class="feature">
                        <div class="feature-icon">💡</div>
                        <div>Jawaban Cerdas</div>
                    </div>
                    <div class="feature">
                        <div class="feature-icon">⚡</div>
                        <div>Respons Cepat</div>
                    </div>
                    <div class="feature">
                        <div class="feature-icon">🎯</div>
                        <div>Akurat & Tepat</div>
                    </div>
                    <div class="feature">
                        <div class="feature-icon">💾</div>
                        <div>Riwayat Chat</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="input-area">
            <div class="input-wrapper">
                <input 
                    type="text" 
                    id="userInput" 
                    placeholder="Tanya apa saja... contoh: Apa itu AI? Bagaimana cara belajar coding?"
                    autocomplete="off"
                >
                <button class="btn btn-clear" onclick="clearChat()" title="Bersihkan Chat">🗑️</button>
            </div>
            <button class="btn" onclick="sendMessage()" id="sendBtn">Kirim</button>
        </div>
    </div>

    <script>
        // Simple AI Response Generator
        const aiResponses = {
            greeting: [
                "Halo! Senang bertemu dengan Anda. Ada yang bisa saya bantu?",
                "Hai! Apa kabar? Siap menjawab pertanyaan Anda!",
                "Selamat datang! Tanyakan apa saja kepada saya."
            ],
            ai: [
                "AI atau Artificial Intelligence adalah teknologi yang memungkinkan komputer untuk belajar dari data dan membuat keputusan. AI digunakan dalam berbagai aplikasi seperti chatbot, rekomendasi produk, dan pengenalan wajah.",
                "Artificial Intelligence adalah cabang ilmu komputer yang fokus pada pembuatan mesin atau program yang dapat melakukan tugas-tugas yang biasanya memerlukan kecerdasan manusia."
            ],
            coding: [
                "Untuk belajar coding, Anda bisa: 1) Mulai dari bahasa dasar seperti Python atau JavaScript, 2) Ikuti tutorial online di Codecademy, freeCodeCamp, atau Udemy, 3) Praktik membuat project kecil, 4) Bergabung dengan komunitas programmer. Konsistensi adalah kunci!",
                "Tips belajar coding: Pahami konsep dasar dulu, praktik coding setiap hari, buat project sendiri, dan jangan takut membuat kesalahan. Kesalahan adalah bagian dari proses belajar!"
            ],
            programming: [
                "Bahasa pemrograman populer: Python (mudah dipelajari), JavaScript (untuk web), Java (untuk aplikasi besar), C++ (untuk performa tinggi), Go (modern dan cepat). Pilih sesuai tujuan Anda!",
                "Bahasa yang cocok untuk pemula adalah Python karena sintaksnya mudah dipahami dan banyak resources pembelajaran tersedia."
            ],
            web: [
                "Web development melibatkan HTML (struktur), CSS (styling), dan JavaScript (interaktivitas). Framework populer: React, Vue, Angular untuk frontend; Node.js, Django untuk backend.",
                "Untuk membuat website, Anda perlu belajar: HTML untuk struktur, CSS untuk desain, dan JavaScript untuk interaktivitas. Mulai dari yang sederhana dulu!"
            ],
            python: [
                "Python adalah bahasa pemrograman yang powerful dan mudah dipelajari. Digunakan untuk web development, data science, AI, automation, dan banyak lagi. Sangat cocok untuk pemula!",
                "Python populer karena sintaksnya yang clean dan readable. Banyak library tersedia untuk berbagai keperluan seperti Django, Flask, TensorFlow, Pandas."
            ],
            data: [
                "Data science adalah bidang yang menggabungkan statistics, programming, dan domain knowledge untuk mengekstrak insight dari data. Tools populer: Python, R, SQL, Tableau.",
                "Data science melibatkan proses: pengumpulan data, cleaning, exploratory analysis, modeling, dan visualization. Skill yang diperlukan: math, statistics, programming, dan domain knowledge."
            ],
            cloud: [
                "Cloud computing adalah menyimpan dan memproses data di server yang tersebar di internet, bukan di komputer lokal. Keuntungan: skalabilitas, fleksibilitas, cost-effective. Provider: AWS, Google Cloud, Azure.",
                "Cloud services seperti AWS, Google Cloud, dan Microsoft Azure menyediakan infrastruktur yang dapat diakses dari mana saja dengan biaya yang fleksibel."
            ],
            security: [
                "Cybersecurity adalah praktik melindungi sistem, jaringan, dan data dari serangan digital. Tips: gunakan password yang kuat, update software, jangan klik link mencurigakan, gunakan VPN untuk koneksi publik.",
                "Untuk keamanan online: gunakan autentikasi dua faktor, jangan bagikan password, hati-hati phishing, gunakan firewall dan antivirus yang baik."
            ],
            career: [
                "Karir di tech sangat menjanjikan. Peran populer: software engineer, data scientist, cloud architect, cybersecurity specialist, UI/UX designer. Kembangkan skill terus dan bangun portfolio!",
                "Untuk sukses di industri tech: terus belajar, bangun project portfolio, networking dengan industry professionals, dan jangan takut untuk memulai dari junior level."
            ],
            productivity: [
                "Tips produktivitas: 1) Buat to-do list, 2) Fokus pada satu task, 3) Ambil break berkala, 4) Hindari distraksi (matikan notifikasi), 5) Prioritaskan tugas penting.",
                "Untuk meningkatkan produktivitas: gunakan Pomodoro Technique (25 menit kerja, 5 menit istirahat), pisahkan ruang kerja, gunakan tools seperti Trello atau Asana."
            ],
            health: [
                "Kesehatan fisik dan mental penting. Tips: olahraga teratur, tidur cukup (7-8 jam), makan sehat, kelola stress dengan meditasi atau hobi, dan konsultasi dokter jika perlu.",
                "Gaya hidup sehat: olahraga minimal 30 menit sehari, minum air putih cukup, makan makanan bergizi, istirahat yang cukup, dan hindari stress berlebihan."
            ],
            general: [
                "Pertanyaan menarik! Saya siap membantu. Bisa jelaskan lebih detail atau tanyakan tentang topik spesifik?",
                "Itu pertanyaan bagus! Berdasarkan informasi umum, saya bisa membantu memberikan insights dan perspektif berbeda.",
                "Saya akan mencoba membantu sebaik mungkin. Apa detail spesifik yang ingin Anda ketahui?"
            ]
        };

        function getAIResponse(userMessage) {
            const message = userMessage.toLowerCase();
            
            if (message.includes('halo') || message.includes('hi') || message.includes('pagi') || message.includes('salam')) {
                return getRandomResponse(aiResponses.greeting);
            }
            
            if (message.includes('ai ') || message.includes('artificial') || message.includes('intelligence') || message.includes('machine learning')) {
                return getRandomResponse(aiResponses.ai);
            }
            
            if (message.includes('belajar') && (message.includes('coding') || message.includes('program'))) {
                return getRandomResponse(aiResponses.coding);
            }
            
            if (message.includes('bahasa') && message.includes('program')) {
                return getRandomResponse(aiResponses.programming);
            }
            
            if (message.includes('web') || message.includes('website')) {
                return getRandomResponse(aiResponses.web);
            }
            
            if (message.includes('python')) {
                return getRandomResponse(aiResponses.python);
            }
            
            if (message.includes('data') || message.includes('analytics')) {
                return getRandomResponse(aiResponses.data);
            }
            
            if (message.includes('cloud') || message.includes('aws') || message.includes('azure')) {
                return getRandomResponse(aiResponses.cloud);
            }
            
            if (message.includes('security') || message.includes('keamanan') || message.includes('cyber')) {
                return getRandomResponse(aiResponses.security);
            }
            
            if (message.includes('karir') || message.includes('pekerjaan') || message.includes('kerja')) {
                return getRandomResponse(aiResponses.career);
            }
            
            if (message.includes('produktif') || message.includes('efisien') || message.includes('giat')) {
                return getRandomResponse(aiResponses.productivity);
            }
            
            if (message.includes('kesehatan') || message.includes('sehat') || message.includes('olahraga')) {
                return getRandomResponse(aiResponses.health);
            }
            
            return getRandomResponse(aiResponses.general);
        }

        function getRandomResponse(responseArray) {
            return responseArray[Math.floor(Math.random() * responseArray.length)];
        }

        function sendMessage() {
            const input = document.getElementById('userInput');
            const message = input.value.trim();
            
            if (!message) return;

            addMessage(message, 'user');
            input.value = '';
            input.focus();

            showTypingIndicator();

            setTimeout(() => {
                removeTypingIndicator();
                const response = getAIResponse(message);
                addMessage(response, 'ai');
                
                const chatContainer = document.getElementById('chatContainer');
                chatContainer.scrollTop = chatContainer.scrollHeight;
            }, 800 + Math.random() * 1200);
        }

        function addMessage(text, sender) {
            const chatContainer = document.getElementById('chatContainer');
            
            const welcome = chatContainer.querySelector('.welcome');
            if (welcome) welcome.remove();

            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${sender}`;

            const time = new Date().toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });

            if (sender === 'ai') {
                messageDiv.innerHTML = `
                    <div>
                        <div class="message-content">
                            <div style="position: relative;">
                                ${text}
                                <button class="copy-btn" onclick="copyToClipboard('${text.replace(/'/g, "\\'")}')">📋 Copy</button>
                            </div>
                        </div>
                        <div class="message-time">${time}</div>
                    </div>
                `;
            } else {
                messageDiv.innerHTML = `
                    <div>
                    
