<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Data 000</title>
    <link href="https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css" rel="stylesheet">
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(120deg, #4e54c8, #8f94fb);
            color: white;
            animation: fadeIn 1s ease-in-out;
        }

        @keyframes fadeIn {
            from {opacity: 0; transform: translateY(-20px);}
            to {opacity: 1; transform: translateY(0);}
        }

        header {
            background: rgba(0,0,0,0.2);
            padding: 15px;
            text-align: center;
            font-size: 22px;
            font-weight: bold;
        }

        nav {
            display: flex;
            justify-content: center;
            background: rgba(255,255,255,0.1);
            padding: 10px;
            gap: 15px;
        }

        nav a {
            color: white;
            text-decoration: none;
            padding: 8px 15px;
            border-radius: 8px;
            transition: 0.3s;
        }

        nav a:hover {
            background: rgba(255,255,255,0.3);
        }

        .container {
            padding: 20px;
            display: none;
        }

        .active {
            display: block;
        }

        input, button {
            padding: 10px;
            margin: 8px 0;
            width: 100%;
            border-radius: 6px;
            border: none;
        }

        button {
            background: #00c6ff;
            color: white;
            cursor: pointer;
        }

        button:hover {
            background: #0072ff;
        }

        .owner-info {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 10px;
            margin-top: 15px;
        }
    </style>
</head>
<body>

    <header>
        <i class='bx bx-data'></i>Data
    </header>

    <nav>
        <a href="#" onclick="showPage('formPage')"><i class='bx bx-edit'></i> Input Data</a>
        <a href="#" onclick="showPage('hasilPage')"><i class='bx bx-list-ul'></i> Hasil Data</a>
        <a href="#" onclick="showPage('ownerPage')"><i class='bx bx-user'></i> Tentang Pemilik</a>
    </nav>

    <div id="formPage" class="container active">
        <h2>Login</h2>
        <input type="text" id="nama" placeholder="Masukkan Nama">
        <input type="password" id="password" placeholder="Masukkan Password">
        <button onclick="simpanData()"><i class='bx bx-save'></i> Simpan</button>
    </div>

    <div id="hasilPage" class="container">
        <h2>Hasil Data</h2>
        <div id="listData"></div>
    </div>

    <div id="ownerPage" class="container">
        <h2>Owner</h2>
        <div class="owner-info">
            <p><strong>Nama:</strong>ALVIN FIENZA</p>
            <p><strong>Pekerjaan:</strong> Developer & Desainer Web</p>
            <p><strong>Deskripsi:</strong> Membuat aplikasi web interaktif, game HTML, dan bot WA berbasis web.</p>
            <p><strong>Kontak:</strong> +62 851-6552-9572</p>
        </div>
    </div>

    <script>
        function showPage(pageId) {
            document.querySelectorAll('.container').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
        }

        function simpanData() {
            let nama = document.getElementById('nama').value;
            let password = document.getElementById('password').value;

            if (nama && password) {
                let data = JSON.parse(localStorage.getItem('dataPengguna')) || [];
                data.push({ nama, password });
                localStorage.setItem('dataPengguna', JSON.stringify(data));
                alert('Data berhasil disimpan!');
                document.getElementById('nama').value = '';
                document.getElementById('password').value = '';
                tampilkanData();
            } else {
                alert('Harap isi semua data!');
            }
        }

        function tampilkanData() {
            let data = JSON.parse(localStorage.getItem('dataPengguna')) || [];
            let listData = document.getElementById('listData');
            listData.innerHTML = data.map((item, index) => 
                `<p>${index+1}. Nama: ${item.nama} | Password: ${item.password}</p>`
            ).join('');
        }

        window.onload = tampilkanData;
    </script>

</body>
</html>
