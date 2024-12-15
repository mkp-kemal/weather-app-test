## Author

**Muhammad Kemal Pasha**  
  [GitHub Profile](https://github.com/mkp-kemal)   
  [Email](mailto:mkp.kemal@gmail.com)


# BAGIAN A

# Membuat Tombol dengan Efek Hover Menggunakan CSS
## Deskripsi
Proyek ini mencakup pembuatan tombol dengan efek hover menggunakan HTML dan CSS. Efek hover yang diinginkan adalah perubahan warna latar belakang tombol saat pengguna mengarahkan kursor ke atasnya.

## Langkah-Langkah Implementasi
### 1. Buat CSS Class
```css
.hover-button {
    background-color: #3498db; 
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease; 
}

.hover-button:hover {
    background-color: #2ecc71; 
}
```

### 2. Buat struktur code html
```html
<body>
    <button class="hover-button">Hover Me</button>
</body>
```


# Menggabungkan File CSS dan JavaScript untuk Mengoptimalkan Performa Aplikasi Web
## Deskripsi
Menggabungkan beberapa file CSS dan JavaScript menjadi satu file untuk mengurangi jumlah permintaan HTTP, sehingga mempercepat waktu muat halaman aplikasi web.

## Contoh Implementasi
### 1. Menggabungkan File CSS dan Javascript pada html
```html
<!DOCTYPE html>
<html>
<head>
    <title>Implementsasi Gabung CSS dan JavaScript</title>
    <style>
        body {
            background-color: lightblue;
        }
        h1 {
            color: white;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>Halo Dunia!</h1>
    <button onclick="ubahWarna()">Ubah Warna</button>

    <script>
        function ubahWarna() {
            document.body.style.backgroundColor = "lightgreen";
        }
    </script>
</body>
</html>
```


# Praktik Terbaik untuk Membuat Tombol yang Dapat Diakses melalui Keyboard
## Deskripsi
membuat tombol yang dapat diakses dengan navigasi keyboard yang mudah dan dukungan untuk pembaca layar.

## Teknik dan Praktik Terbaik
### TEKNIK
#### 1. Analisis experience pengguna untuk menentukan tombol mana yang lebih mudah di klik, contohnya "enter"
#### 2. Membuat logic javascript untuk menambahkan navigasi ke keyboard pembaca layar/menggunakan element bawaan div yaitu oneKeydown

### Praktik
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aksesibilitas Tombol</title>
    <style>
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #2ecc71;
        }

        button:focus {
            outline: 2px solid #f1c40f;
            outline-offset: 2px;
        }
    </style>
</head>
<body>
    <h1>Aksesibilitas Tombol</h1>
    <button id="toggleButton" aria-pressed="false">Toggle Konten</button>
    <div id="konten" style="margin-top: 20px; display: none;">Konten berhasil ditampilkan!</div>

    <script>
        const toggleButton = document.getElementById('toggleButton');
        const konten = document.getElementById('konten');

        function toggleContent() {
            const isPressed = toggleButton.getAttribute('aria-pressed') === 'true';
            toggleButton.setAttribute('aria-pressed', !isPressed);
            konten.style.display = isPressed ? 'none' : 'block';
        }

        toggleButton.addEventListener('click', toggleContent);

        toggleButton.addEventListener('keydown', (event) => {
            if (event.key === 'Enter' || event.key === ' ') {
                event.preventDefault(); 
                toggleContent(); 
            }
        });
    </script>
</body>
</html>
```

# BAGIAN B
## Demo Aplikasi
[![Demo Weather App](https://github.com/mkp-kemal/weather-app-test/raw/main/assets/demo-weather-app.gif)](https://github.com/mkp-kemal/weather-app-test/raw/main/assets/demo-weather-app.gif)

# Nuxt Minimal Starter

Look at the [Nuxt documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm dev

# yarn
yarn dev

# bun
bun run dev
```

## Production

Build the application for production:

```bash
# npm
npm run build

# pnpm
pnpm build

# yarn
yarn build

# bun
bun run build
```

Locally preview production build:

```bash
# npm
npm run preview

# pnpm
pnpm preview

# yarn
yarn preview

# bun
bun run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
