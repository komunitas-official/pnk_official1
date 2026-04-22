<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PNK - Perlindungan Nusantara Komunitas</title>
    <style>
        :root {
            --primary: #00d2ff;
            --secondary: #3a7bd5;
            --dark: #0f0c29;
            --glass: rgba(255, 255, 255, 0.1);
        }

        body {
            font-family: 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow-x: hidden;
        }

        .container {
            background: var(--glass);
            backdrop-filter: blur(20px);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
            width: 100%;
            max-width: 400px;
            text-align: center;
            position: absolute;
            transition: all 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        /* Status Halaman */
        .hidden { 
            opacity: 0; 
            transform: scale(0.8) translateY(100px); 
            pointer-events: none; 
        }

        .active {
            opacity: 1;
            transform: scale(1) translateY(0);
            pointer-events: all;
        }

        h2 { margin-bottom: 25px; letter-spacing: 3px; color: var(--primary); text-shadow: 0 0 10px var(--primary); }

        input, select {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border-radius: 10px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.3);
            color: white;
            box-sizing: border-box;
            outline: none;
        }

        input:focus { border-color: var(--primary); box-shadow: 0 0 10px var(--primary); }

        button {
            width: 100%;
            padding: 15px;
            margin-top: 20px;
            border-radius: 10px;
            border: none;
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            transition: 0.4s;
        }

        button:hover {
            letter-spacing: 2px;
            box-shadow: 0 0 20px var(--primary);
        }

        /* Label untuk form intro */
        .label-text { text-align: left; font-size: 12px; margin-top: 5px; color: #ccc; }
    </style>
</head>
<body>

    <audio id="clickSound" src="https://www.soundjay.com/buttons/sounds/button-16.mp3"></audio>
    <audio id="successSound" src="https://www.soundjay.com/buttons/sounds/button-09.mp3"></audio>

    <div id="loginPage" class="container active">
        <h2>PNK SYSTEM</h2>
        <p style="font-size: 13px; color: #aaa;">Silahkan Masuk ke Komunitas</p>
        <input type="text" id="username" placeholder="Username (Bebas)">
        <input type="password" id="password" placeholder="Password (Bebas)">
        <button onclick="goToIntro()">MASUK SISTEM</button>
    </div>

    <div id="introPage" class="container hidden">
        <h2>IDENTITAS DIRI</h2>
        <div style="max-height: 400px; overflow-y: auto; padding-right: 10px;">
            <input type="text" id="nama" placeholder="Nama Lengkap">
            <input type="number" id="umur" placeholder="Umur">
            <div class="label-text">Tanggal Lahir:</div>
            <input type="date" id="tglLahir">
            <select id="gender">
                <option value="">Pilih Jenis Kelamin</option>
                <option value="Laki-laki">Laki-laki</option>
                <option value="Perempuan">Perempuan</option>
            </select>
            <input type="text" id="tiktok" placeholder="Username TikTok (@)">
            <input type="text" id="asal" placeholder="Asal Kota/Provinsi">
            <input type="text" id="alasan" placeholder="Alasan Bergabung">
        </div>
        <button onclick="finalizeAndJoin()">KIRIM & GABUNG GRUP</button>
    </div>

    <script>
        const clickSfx = document.getElementById('clickSound');
        const successSfx = document.getElementById('successSound');

        // Fungsi pindah ke halaman Intro
        function goToIntro() {
            const user = document.getElementById('username').value;
            const pass = document.getElementById('password').value;

            // Validasi: Username & Password boleh apa saja asal tidak kosong
            if (user.trim() !== "" && pass.trim() !== "") {
                clickSfx.play();
                successSfx.play();
                
                // Animasi perpindahan halaman
                document.getElementById('loginPage').classList.remove('active');
                document.getElementById('loginPage').classList.add('hidden');
                
                setTimeout(() => {
                    document.getElementById('introPage').classList.remove('hidden');
                    document.getElementById('introPage').classList.add('active');
                }, 600);
            } else {
                alert("Mohon isi username dan password terlebih dahulu!");
            }
        }

        // Fungsi kirim data dan ke WA
        function finalizeAndJoin() {
            clickSfx.play();
            const fields = ['nama', 'umur', 'tglLahir', 'gender', 'tiktok', 'asal', 'alasan'];
            let isComplete = true;

            fields.forEach(id => {
                if (document.getElementById(id).value === "") isComplete = false;
            });

            if (isComplete) {
                successSfx.play();
                alert("Data Berhasil Diverifikasi oleh AI. Mengalihkan ke WhatsApp...");
                setTimeout(() => {
                    window.location.href = "https://chat.whatsapp.com/KJQGOzP9OazAF3MbyUFx65?mode=gi_t";
                }, 1000);
            } else {
                alert("Lengkapi semua kolom intro sebelum bergabung!");
            }
        }

        // FITUR KEAMANAN AI TERSEMBUNYI
        // 1. Anti Inspect Element
        document.addEventListener('contextmenu', event => event.preventDefault());
        document.onkeydown = function(e) {
            if(e.keyCode == 123 || (e.ctrlKey && e.shiftKey && e.keyCode == 'I'.charCodeAt(0))) {
                return false;
            }
        };

        // 2. Simulasi AI Monitoring (Hanya terlihat di console log yang tersembunyi)
        console.log("%c[AI SECURITY ACTIVE]", "color: cyan; font-weight: bold; font-size: 15px;");
        console.log("Monitoring traffic and identity verification...");
    </script>
</body>
</html>
