<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tugas Dart - Extension Methods</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 900px;
            margin: 20px auto;
            padding: 20px;
            background: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }

        .header {
            background: white;
            padding: 25px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        .header h1 {
            margin: 0 0 5px 0;
            font-size: 24px;
            color: #0175c2;
        }

        .header p {
            margin: 0;
            color: #666;
        }

        .identitas {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        .identitas td {
            padding: 8px 10px;
        }

        .identitas td:first-child {
            font-weight: bold;
            width: 80px;
            color: #555;
        }

        .identitas input {
            border: none;
            border-bottom: 1px solid #ccc;
            padding: 8px;
            font-size: 14px;
            width: 250px;
            background: transparent;
        }

        .identitas input:focus {
            outline: none;
            border-bottom-color: #0175c2;
        }

        .soal-box {
            background: white;
            padding: 25px;
            border-radius: 8px;
            margin-bottom: 20px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        .soal-box h2 {
            color: #0175c2;
            margin-top: 0;
            border-bottom: 2px solid #0175c2;
            padding-bottom: 10px;
        }

        .soal-box h3 {
            color: #d32f2f;
            margin: 15px 0 5px 0;
        }

        .pseudocode {
            background: #fff3e0;
            border-left: 4px solid #ff9800;
            padding: 15px 20px;
            margin: 15px 0;
            border-radius: 0 5px 5px 0;
        }

        .pseudocode h4 {
            margin: 0 0 10px 0;
            color: #e65100;
        }

        .pseudocode pre {
            margin: 0;
            background: transparent;
            color: #333;
            font-size: 13px;
            line-height: 1.5;
        }

        .jawaban {
            background: #e8f5e9;
            border-left: 4px solid #4caf50;
            padding: 15px 20px;
            margin: 15px 0;
            border-radius: 0 5px 5px 0;
        }

        .jawaban h4 {
            margin: 0 0 10px 0;
            color: #2e7d32;
        }

        .code-block {
            background: #263238;
            color: #aed581;
            padding: 15px;
            border-radius: 5px;
            overflow-x: auto;
            font-size: 13px;
            line-height: 1.5;
            margin: 10px 0;
        }

        .code-block pre {
            margin: 0;
            background: transparent;
            color: inherit;
            padding: 0;
        }

        .dartpad-mini {
            margin: 20px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            overflow: hidden;
        }

        .dartpad-mini iframe {
            width: 100%;
            height: 400px;
            border: none;
            display: block;
        }

        .dartpad-mini .label {
            background: #263238;
            color: #fff;
            padding: 8px 15px;
            font-size: 13px;
            font-weight: bold;
        }

        .btn {
            display: inline-block;
            padding: 8px 16px;
            background: #0175c2;
            color: white;
            text-decoration: none;
            border-radius: 4px;
            font-size: 14px;
            margin: 5px 5px 5px 0;
            border: none;
            cursor: pointer;
        }

        .btn:hover {
            background: #01579b;
        }

        .btn-share {
            background: #25d366;
        }

        .btn-share:hover {
            background: #1da851;
        }

        footer {
            text-align: center;
            color: #999;
            font-size: 12px;
            margin-top: 30px;
            padding: 15px;
        }
    </style>
</head>
<body>

    <!-- Header -->
    <div class="header">
        <h1>Tugas Pemrograman Mobile</h1>
        <p>Topik: Dart Extension Methods - Konflik Nama & Private Member</p>
    </div>

    <!-- Identitas -->
    <div class="identitas">
        <table>
            <tr>
                <td>Nama</td>
                <td><input type="text" id="nama" placeholder="Rifqi Prayoga"></td>
            </tr>
            <tr>
                <td>NIM</td>
                <td><input type="text" id="nim" placeholder="251410005"></td>
            </tr>
            <tr>
                <td>Kelas</td>
                <td><input type="text" id="kelas" placeholder="SI2A"></td>
            </tr>
        </table>
    </div>

    <!-- ==================== SOAL 1 ==================== -->
    <div class="soal-box">
        <h2>Soal 1: Konflik Nama Antar Extension</h2>
        
        <p>Perhatikan kode berikut:</p>

        <div class="code-block">
            <pre>extension StringNumber on String {
  int toInt() {
    return int.parse(this);
  }
}

extension StringDouble on String {
  double toInt() {  // ← nama method sama, return type beda
    return double.parse(this);
  }
}

void main() {
  String angka = '123';
  print(angka.toInt());
}</pre>
        </div>

        <p><strong>Pertanyaan:</strong> Apa yang terjadi saat kode dijalankan? Jelaskan penyebabnya dan berikan solusi agar kedua extension dapat digunakan tanpa konflik.</p>

        <!-- Jawaban -->
        <h3>Jawaban:</h3>
        <div class="jawaban">
            <h4>Penjelasan</h4>
            <p>Kode akan <strong>gagal dikompilasi (error)</strong>. Dart tidak bisa menentukan extension mana yang harus digunakan karena kedua extension (<code>StringNumber</code> dan <code>StringDouble</code>) memiliki method dengan nama yang sama persis yaitu <code>toInt</code>. Walaupun return type-nya berbeda (<code>int</code> vs <code>double</code>), Dart tidak mendukung method overloading berdasarkan return type.</p>

            <h4>Solusi</h4>
            <p>Cara paling sederhana dan direkomendasikan: <strong>gunakan nama method yang berbeda</strong> untuk masing-masing extension.</p>
        </div>

        <!-- Pseudocode -->
        <div class="pseudocode">
            <h4>Pseudocode Solusi</h4>
            <pre>EXTENSION StringNumber UNTUK String
  METHOD toInt() KEMBALIKAN integer
    LAKUKAN parsing string menjadi integer
  AKHIR METHOD
AKHIR EXTENSION

EXTENSION StringDouble UNTUK String
  METHOD toDouble() KEMBALIKAN double  ← nama dibedakan
    LAKUKAN parsing string menjadi double
  AKHIR METHOD
AKHIR EXTENSION

FUNGSI main()
  BUAT variabel angka = "123"
  PANGGIL angka.toInt()    → hasil: 123 (integer)
  PANGGIL angka.toDouble() → hasil: 123.0 (double)
AKHIR FUNGSI</pre>
        </div>

        <!-- DartPad Soal 1 -->
        <div class="dartpad-mini">
            <div class="label"> Live Demo Soal 1 (Auto-Run)</div>
            <iframe 
                id="dartpad-soal1"
                src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=560516deba54c778bd57b3e16abc818f">
            </iframe>
        

    <!-- ==================== SOAL 2 ==================== -->
    <div class="soal-box">
        <h2>Soal 2: Extension Method Tidak Bisa Mengakses Member Private</h2>
        
        <p>Diberikan class berikut:</p>

        <div class="code-block">
            <pre>class Counter {
  int _value = 0;  // private

  void increment() {
    _value++;
  }
}

extension CounterStats on Counter {
  int getValue() {
    return _value;  // ← baris ini bermasalah
  }
}

void main() {
  var c = Counter();
  c.increment();
  print(c.getValue());
}</pre>
        </div>

        <p><strong>Pertanyaan:</strong> Jelaskan mengapa kode di atas gagal dikompilasi. Bagaimana cara memperbaikinya tanpa mengubah akses modifier <code>_value</code> menjadi publik?</p>

        <!-- Jawaban -->
        <h3>Jawaban:</h3>
        <div class="jawaban">
            <h4>Penjelasan</h4>
            <p>Kode gagal dikompilasi karena <strong>extension method tidak dapat mengakses anggota private (<code>_value</code>)</strong> dari class <code>Counter</code>. Di Dart, anggota dengan awalan underscore (<code>_</code>) bersifat library-private, artinya hanya bisa diakses dari dalam file/library yang sama. Jika extension <code>CounterStats</code> ditulis di file yang berbeda dengan class <code>Counter</code>, maka extension tidak memiliki akses ke <code>_value</code>.</p>

            <h4>Solusi</h4>
            <p>Tanpa mengubah <code>_value</code> menjadi public, kita bisa <strong>menambahkan getter publik</strong> di dalam class <code>Counter</code>, lalu extension menggunakan getter tersebut.</p>
        </div>

        <!-- Pseudocode -->
        <div class="pseudocode">
            <h4>Pseudocode Solusi</h4>
            <pre>CLASS Counter
  PRIVATE _value = 0
  
  METHOD increment()
    TAMBAHKAN _value sebanyak 1
  AKHIR METHOD
  
  GETTER value KEMBALIKAN integer  ← getter publik
    KEMBALIKAN _value
  AKHIR GETTER
AKHIR CLASS

EXTENSION CounterStats UNTUK Counter
  METHOD getValue() KEMBALIKAN integer
    KEMBALIKAN value  ← pakai getter publik, bukan _value
  AKHIR METHOD
  
  GETTER isEmpty KEMBALIKAN boolean
    KEMBALIKAN value == 0
  AKHIR GETTER
  
  GETTER isNotEmpty KEMBALIKAN boolean
    KEMBALIKAN value > 0
  AKHIR GETTER
AKHIR EXTENSION

FUNGSI main()
  BUAT objek counter DARI Counter
  PANGGIL counter.increment() sebanyak 3 kali
  PANGGIL counter.getValue()  → hasil: 3
  PANGGIL counter.isEmpty     → hasil: false
  PANGGIL counter.isNotEmpty  → hasil: true
AKHIR FUNGSI</pre>
        </div>

        <!-- DartPad Soal 2 -->
        <div class="dartpad-mini">
            <div class="label"> Live Demo Soal 2 (Auto-Run)</div>
            <iframe 
                id="dartpad-soal2"
                src="https://dartpad.dev/embed-dart.html?theme=dark&run=true&id=843ac16158475e095a1f81e8616fdb36">
            </iframe>
      

    <footer>
        Rifqi Prayoga | 251410005 | SI2A
    </footer>

    <script>
        // Simpan identitas
        const namaInput = document.getElementById('nama');
        const nimInput = document.getElementById('nim');
        const kelasInput = document.getElementById('kelas');

        namaInput.value = localStorage.getItem('nama') || '';
        nimInput.value = localStorage.getItem('nim') || '';
        kelasInput.value = localStorage.getItem('kelas') || '';

        namaInput.addEventListener('input', () => localStorage.setItem('nama', namaInput.value));
        nimInput.addEventListener('input', () => localStorage.setItem('nim', nimInput.value));
        kelasInput.addEventListener('input', () => localStorage.setItem('kelas', kelasInput.value));

        // Share screen function
        function shareScreen(soal) {
            let dartpadId;
            if (soal === 'soal1') {
                dartpadId = 'GANTI_ID_SOAL_1'; // Ganti dengan ID Gist soal 1
            } else {
                dartpadId = 'GANTI_ID_SOAL_2'; // Ganti dengan ID Gist soal 2
            }
            
            const dartpadLink = 'https://dartpad.dev/?run=true&id=' + dartpadId;
            
            navigator.clipboard.writeText(dartpadLink).then(() => {
                alert('Link DartPad sudah dicopy! Membuka fullscreen...');
            });

            window.open(dartpadLink, '_blank', 
                'width=' + screen.width + ',height=' + screen.height);
        }
    </script>

</body>
</html>
