
# Dokumentasi WIBU

Dokumentasi ini bertujuan untuk mempermudah proses implementasi proyek yang sedang kita kerjakan maupun proyek baru yang akan kita buat. Dengan adanya dokumentasi ini, kita dapat lebih mudah memahami struktur proyek, fungsi dari setiap folder dan file, serta alur kerja yang perlu diikuti. Hal ini diharapkan dapat mempercepat pengembangan dan memastikan bahwa semua anggota tim memiliki pemahaman yang konsisten.



## Install Next js

Langkah pertama untuk menggunakan Next.js adalah menginstalnya. Kita dapat melakukan instalasi menggunakan npm atau yarn. Berikut adalah langkah-langkahnya:

Syarat-syarat:

- Versi Node.js 18.17 atau diatasnya.
- macOS, Windows (termasuk WSL), dan Linux.

Pada terminal yang digunakan, jalankan perintah dibawah untuk men-generate project,

```bash
  npx create-next-app@latest
```

Lalu setelah perintah diatas nantinya akan ada interaksi didalam terminal untuk memilih konfigurasi daripada project Next.js kita nantinya

```javascript
1. What is your project named? `nama project`
2. Would you like to use TypeScript? No / `Yes`
3. Would you like to use ESLint? `No` / Yes
4. Would you like to use Tailwind CSS? No / `Yes`
5. Would you like to use 'src/' directory? No / `Yes`
6. Would you like to use App Router? (recommended) No / `Yes`
7. Would you like to customize the default import alias? `No` / Yes
8. What import alias would you like configured? @/*
```

Setelah proses pemilihan konfigurasi selesai, nantinya `npx create-next-app@latest` akan membuat suatu folder bernama sesuai dari nama project yang telah kita pilih sebelumnya.


### Menjalankan Server Development

Jalankan perintah `npm run dev` atau `yarn dev` pada terminal IDE untuk menjalankan server development.

```bash
  npm run dev
```
atau
```bash
  yarn dev
```

Buka http://localhost:3000 pada peramban yang digunakan untuk melihat web app kita.

```bash
  http://localhost:3000
```
Lebih jelasnya bisa lihat di dokumentasi resmi next js, link ada di bawah ini:
```
https://nextjs.org/
```

## Install Mantine Component

Langkah pertama untuk menggunakan Mantine di Next js

Syarat-syarat:

- Sudah Memiliki Project Next Js
- macOS, Windows (termasuk WSL), dan Linux.

Pada terminal Project yang sudah di buat, jalankan perintah dibawah untuk melakukan install Mantine,

```bash
yarn add @mantine/core @mantine/hooks @mantine/form @mantine/dates dayjs @mantine/charts recharts@2 @mantine/notifications @mantine/code-highlight @mantine/tiptap @tabler/icons-react @tiptap/react @tiptap/extension-link @tiptap/starter-kit @mantine/dropzone @mantine/carousel embla-carousel-react @mantine/spotlight @mantine/modals @mantine/nprogress
```

Setelah proses install selesai, lalu buka codingan `app/layout.tsx` untuk merubah menjadi codingan yang di sediakan oleh mantine seperti di bawah ini:

```javascript
// Import styles of packages that you've installed.
// All packages except `@mantine/hooks` require styles imports
import '@mantine/core/styles.css';

import { ColorSchemeScript, MantineProvider } from '@mantine/core';

export const metadata = {
  title: 'My Mantine app',
  description: 'I have followed setup instructions carefully',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <head>
        <ColorSchemeScript />
      </head>
      <body>
        <MantineProvider>{children}</MantineProvider>
      </body>
    </html>
  );
}
```

Setelah itu coba rubah codingan di folder `src/app/page.tsx` untuk melihat apakah mantine bisa gunakan atau tidak, contoh codingan di bawah ini:

```javascript
import { Button, Box } from '@mantine/core';

function App() {
  return (
    <Box>
      <Button >
        Submit
      </Button>
    </Box>
  );
}

```
Lebih jelasnya bisa melihat dokumentasi resmi Mantine, Link ada di bawah ini:
```
https://mantine.dev/
```

## Install Prisma

Pembuatan Prisma untuk menyambungkan ke database

inisialisasi proyek TypeScript dan tambahkan Prisma CLI sebagai ketergantungan pengembangan padanya:

```bash
  npm init -y
```
```bash
  npm install prisma typescript ts-node @types/node --save-dev
```
Ini membuat package.json dengan pengaturan awal untuk aplikasi TypeScript Anda.

Selanjutnya, inisialisasi TypeScript:

```bash
  npx tsc --init
```

Selanjutnya, siapkan proyek Prisma ORM Anda dengan membuat file Skema Prisma dengan perintah berikut:

```bash
  npx prisma init
```

Untuk menghubungkan database, Anda perlu menyetel bidang url blok sumber data di skema Prisma ke URL koneksi database Anda:

```bash
  datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
```


Dalam hal ini, url diatur melalui variabel lingkungan yang didefinisikan dalam .env:

```bash
DATABASE_URL="postgresql://johndoe:randompassword@localhost:5432/mydb?schema=public"
```

### Buat Database schema
Dalam panduan ini, Anda akan menggunakan Prisma Migrate untuk membuat tabel di database Anda. Tambahkan model data berikut ke skema Prisma Anda di prisma/schema.prisma:

```javascript
model Post {
  id        Int      @id @default(autoincrement())
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  title     String   @db.VarChar(255)
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}

model Profile {
  id     Int     @id @default(autoincrement())
  bio    String?
  user   User    @relation(fields: [userId], references: [id])
  userId Int     @unique
}

model User {
  id      Int      @id @default(autoincrement())
  email   String   @unique
  name    String?
  posts   Post[]
  profile Profile?
}
```

Untuk memetakan model data Anda ke skema database, Anda perlu menggunakan perintah CLI prismamigrate:

```bash
npx prisma migrate dev --name init
```

Setelah ada perubahan schema database usahakan melakukan hal di bawah ini:
```bash
npx prisma db push
```
```bash
npx prisma generate
```
Lebih jelasnya bisa melihat documentasi resmi dari prisma, link di bawah ini
```
https://www.prisma.io/
```
## Clone Project Github

Clone project yang sudah di buatkan oleh tim atau leader, dengan membuka terminal dan jalankan code di bawah ini:

```bash
  git clone https://link-projectnya
```

Go to the project directory

```bash
  cd nama-projectnya
```

Install dependencies

```bash
  yarn
```

Start the server

```bash
  yarn dev
```
Go to the Vscode
```bash
  code .
```

## Struktur Folder Project Next.js

Berikut adalah struktur folder untuk project Next.js:

- `prisma/`
  - `schema.prisma`
- `public/`
- `src/`
  - `app/`
    - `page/`
      - `layout.tsx`
      - `page.tsx`
    - `layout.tsx`
    - `page.tsx`
    - `api/`
      - `folder/`
        - `route.ts`
  - `module/`
    - `_global/`
      - `bin/`
      - `components/`
      - `fun/`
      - `layout/`
      - `view/`
      - `index.ts`
    - `folder-contoh/`
      - `lib/`
        - `api_folder.ts`
        - `type_folder.ts`
      - `ui/`
        - `file-page.tsx`
      - `index.ts`
- `.env`
- `.gitignore`
- `package-lock.json`
- `package.json`
- `tailwind.config.ts`
- `tsconfig.json`
- `yarn.lock`

## Penjelasan Struktur Folder dan File

### `prisma/`
- **`schema.prisma`**: File ini berisi definisi skema database yang digunakan oleh Prisma ORM. Di sini, Anda dapat mendefinisikan model database dan hubungan antar model. Prisma akan menggunakan skema ini untuk menghasilkan query dan migrasi database.

### `public/`
- Folder ini berisi aset statis seperti gambar, favicon, dan file lainnya yang dapat diakses langsung oleh pengguna melalui URL aplikasi. File yang ditempatkan di sini akan tersedia di rute dasar aplikasi Next.js.

### `src/`
- Folder utama yang berisi seluruh kode sumber aplikasi.

  #### `app/`
  - Folder ini mengikuti arsitektur baru Next.js (App Router) untuk mengatur halaman dan API.

    ##### `page/`
    - **`layout.tsx`**: File ini berfungsi untuk menentukan tata letak umum yang akan digunakan oleh seluruh halaman dalam folder `page`. Semua halaman di dalam folder ini akan mewarisi tata letak yang didefinisikan di sini.
    - **`page.tsx`**: File ini merupakan file utama yang mewakili halaman tertentu di aplikasi Next.js. Halaman ini akan dirender berdasarkan URL yang cocok dengan namanya.

    ##### `layout.tsx`
    - File ini menentukan tata letak umum yang akan digunakan oleh seluruh halaman dalam aplikasi di tingkat `app`. Semua halaman dan API di dalam folder `app` akan mewarisi tata letak ini.

    ##### `page.tsx`
    - File ini merupakan halaman utama aplikasi yang akan dirender ketika pengguna mengakses rute dasar (`/`) dari aplikasi.

    ##### `api/`
    - Folder ini berisi route API yang dapat diakses melalui rute tertentu di aplikasi.

      ###### `folder/`
      - **`route.ts`**: File ini berfungsi sebagai endpoint API untuk rute tertentu. Anda dapat mendefinisikan handler untuk request seperti GET, POST, dll., di sini.

  #### `module/`
  - Folder ini digunakan untuk modularisasi kode, memungkinkan komponen dan fungsi diorganisasi dengan lebih baik.

    ##### `_global/`
    - Folder ini berisi kode yang digunakan secara global di seluruh aplikasi, seperti komponen umum, fungsi, dan tata letak.

      ###### `bin/`
      - Folder ini mungkin digunakan untuk menyimpan file-file biner atau skrip yang diperlukan oleh aplikasi.

      ###### `components/`
      - Folder ini berisi komponen UI yang dapat digunakan kembali di berbagai tempat dalam aplikasi.

      ###### `fun/`
      - Folder ini mungkin digunakan untuk menyimpan fungsi atau utilitas yang bersifat menyenangkan atau tambahan.

      ###### `layout/`
      - Folder ini berisi tata letak umum yang dapat digunakan di berbagai bagian aplikasi.

      ###### `view/`
      - Folder ini mungkin berisi komponen atau fungsi yang berkaitan dengan tampilan atau rendering UI.

      ###### `index.ts`
      - File ini digunakan sebagai entry point untuk folder `_global`, di mana berbagai komponen dan fungsi diekspor untuk digunakan di tempat lain dalam aplikasi.

    ##### `folder-contoh/`
    - Contoh folder modul yang mengorganisasi kode berdasarkan fungsionalitas atau fitur.

      ###### `lib/`
      - **`api_folder.ts`**: File ini mungkin berisi fungsi yang terkait dengan API untuk `folder-contoh`.
      - **`type_folder.ts`**: File ini berisi definisi tipe TypeScript yang digunakan di `folder-contoh`.

      ###### `ui/`
      - **`file-page.tsx`**: File ini berisi komponen atau halaman UI yang terkait dengan `folder-contoh`.

      ###### `index.ts`
      - File ini digunakan sebagai entry point untuk `folder-contoh`, menggabungkan dan mengekspor komponen atau fungsi yang dibutuhkan.

### `.env`
- File ini berisi variabel lingkungan yang digunakan untuk menyimpan informasi sensitif seperti kunci API, konfigurasi database, dan lainnya. File ini tidak boleh dibagikan secara publik.

### `.gitignore`
- File ini berisi daftar file dan direktori yang harus diabaikan oleh Git saat melakukan commit. Biasanya digunakan untuk menghindari commit file sensitif atau file build yang tidak diperlukan di repositori.

### `package-lock.json`
- File ini berisi snapshot dari dependensi proyek yang digunakan oleh npm. Ini memastikan bahwa instalasi paket yang sama dilakukan di semua lingkungan.

### `package.json`
- File ini berisi informasi tentang proyek, seperti nama, versi, deskripsi, serta daftar dependensi dan skrip npm yang digunakan untuk mengelola proyek.

### `tailwind.config.ts`
- File ini berisi konfigurasi untuk Tailwind CSS, termasuk tema, varian, dan plugin yang digunakan dalam proyek.

### `tsconfig.json`
- File ini berisi konfigurasi untuk TypeScript, seperti opsi kompilator, direktori output, dan lintasan modul.

### `yarn.lock`
- File ini berfungsi sama seperti `package-lock.json` tetapi digunakan oleh Yarn sebagai package manager. Ini memastikan konsistensi versi paket di semua lingkungan.


## Dokumentasi GIT

1. panter module bisa mengikuti contoh
2. untuk commit beri keterangan lengkap dan jelas
    
    **PANTERN**
    1. Tag Commit (Commit Tag)
    2. Deskripsi (Description)
    3. Body
    4. Referensi Isu (Issue References)
    
    **CONTOH**
    ```txt
    feat: Tambahkan fitur kalkulator

    Deskripsi:
    - Menambahkan fungsi penambahan, pengurangan, perkalian, dan pembagian
    - Memperbolehkan pengguna untuk memasukkan dua angka dan melakukan operasi matematika

    Fixes #12
    ```

    **REFRENSI**

   1. **`fix`**: Digunakan untuk menandakan perbaikan bug atau masalah yang ada dalam kode.

   Contoh:
   ```
   fix: Perbaiki bug tampilan pada halaman profil

   Deskripsi:
   - Mengatasi masalah tampilan yang menyebabkan foto profil tumpang tindih dengan teks

   Fixes #55
   ```

   1. **`docs`**: Digunakan ketika melakukan perubahan pada dokumentasi proyek, seperti menambahkan atau mengedit komentar, README, atau file dokumentasi lainnya.

   Contoh:
   ```
   docs: Update README dengan panduan instalasi

   Deskripsi:
   - Menyediakan petunjuk langkah demi langkah tentang cara menginstal dan menjalankan proyek

   No Issue
   ```

   1. **`chore`**: Digunakan untuk komit yang berhubungan dengan pekerjaan rutin, seperti pembaruan dependensi, pengaturan konfigurasi, atau tugas administratif lainnya.

   Contoh:
   ```
   chore: Pembaruan versi library requests

   Deskripsi:
   - Memperbarui library requests ke versi terbaru untuk meningkatkan keamanan dan kinerja

   No Issue
   ```

   1. **`refactor`**: Digunakan ketika melakukan refaktorisasi kode, yaitu mengubah struktur atau tata letak kode tanpa mengubah perilaku yang terlihat dari luar.

   Contoh:
   ```
   refactor: Ubah struktur kode halaman detail produk

   Deskripsi:
   - Memisahkan logika tampilan dari logika bisnis untuk meningkatkan keterbacaan dan pemeliharaan kode

   No Issue
   ```

   1. **`test`**: Digunakan ketika melakukan perubahan atau penambahan tes atau skrip pengujian.

   Contoh:
   ```
   test: Tambahkan tes unit untuk fungsi kalkulator

   Deskripsi:
   - Menulis tes unit untuk memastikan fungsi kalkulator berjalan dengan benar

   No Issue
   ```

   1. **`style`**: Digunakan ketika melakukan perubahan pada tampilan atau gaya kode, tanpa mengubah logika atau perilaku program.

   Contoh:
   ```
   style: Atur tata letak tombol 'Masuk'

   Deskripsi:
   - Memperbaiki tampilan tombol 'Masuk' pada halaman login agar lebih serasi

   No Issue
   ```

   1. **`perf`**: Digunakan ketika melakukan perubahan untuk meningkatkan kinerja aplikasi atau mengoptimalkan kode.

   Contoh:
   ```
   perf: Optimalkan penggunaan sumber daya gambar

   Deskripsi:
   - Mengurangi ukuran gambar dan mengimplementasikan caching untuk mempercepat waktu muat halaman

   Fixes #102
   ```
3. lakukan push dengan tahapan yang benar jangan menggunakan `git add -A ` tapi sesuai yang diedit atau yang di create saja

    **REFRENSI**

   1. **`git status`**: Pertama, periksa status repositori menggunakan perintah `git status`. Ini akan memberikan daftar perubahan yang belum ditambahkan ke area staging (unstaged changes) dan perubahan yang telah ditambahkan ke area staging (changes to be committed).

   2. **`git add`**: Tambahkan perubahan ke area staging menggunakan perintah `git add`. Misalnya, jika Anda ingin menambahkan semua perubahan, gunakan `git add .`, atau jika ingin menambahkan file tertentu, gunakan `git add <nama_file>`.

   3. **`git commit`**: Setelah perubahan ditambahkan ke area staging, lakukan commit perubahan menggunakan perintah `git commit -m "pesan_commit"`. Pastikan pesan commit yang Anda cantumkan informatif dan jelas mengenai perubahan yang Anda lakukan.

   4. **`git pull`**: Sebelum melakukan `push`, disarankan untuk melakukan `git pull` terlebih dahulu untuk mengambil perubahan terbaru dari repositori pusat (remote repository) dan memastikan bahwa Anda bekerja di atas versi terbaru dari branch yang Anda gunakan.

   5. **`git push`**: Jika tidak ada konflik dengan versi terbaru dari repositori pusat, Anda dapat melakukan `push` perubahan Anda ke repositori menggunakan perintah `git push`. Pastikan Anda memiliki izin yang cukup untuk melakukan `push` ke branch yang sedang Anda kerjakan.

   6. **`git log`**: Setelah `push`, gunakan perintah `git log` untuk memeriksa daftar commit yang telah Anda lakukan. Ini memastikan bahwa perubahan Anda berhasil tercatat di repositori.

    *note*

    - single file 
    
        git add index.html
    - multi file

        git add file1.txt file2.js file3.css
    - dir atau folder

        git add assets/

### Info Umum Git

### Inisialisasi dan Kloning Repository:
- `git init`: Menginisialisasi repositori Git baru di direktori lokal.
- `git clone <URL>`: Mengkloning repositori dari GitHub ke direktori lokal.

### Pengelolaan Perubahan:
- `git status`: Menampilkan status perubahan dalam repositori.
- `git add <file/folder>`: Menambahkan file atau folder ke area staging untuk dimasukkan ke dalam commit.
- `git commit -m "pesan_commit"`: Membuat commit untuk menyimpan perubahan yang sudah ditambahkan ke area staging dengan pesan commit tertentu.
- `git push`: Mengirim perubahan dari repositori lokal ke repositori pusat (remote repository) di GitHub.
- `git pull`: Mengambil perubahan terbaru dari repositori pusat ke repositori lokal.

### Pengelolaan Branch:
- `git branch`: Menampilkan daftar branch yang ada dalam repositori.
- `git branch <nama_branch>`: Membuat branch baru dengan nama tertentu.
- `git checkout <nama_branch>`: Beralih ke branch tertentu.
- `git merge <nama_branch>`: Menggabungkan branch tertentu ke branch aktif.
- `git branch -d <nama_branch>`: Menghapus branch tertentu.

### Pengelolaan Remote Repository (GitHub):
- `git remote`: Menampilkan daftar remote repository yang terhubung dengan repositori lokal.
- `git remote add <nama_remote> <URL>`: Menambahkan remote repository baru ke repositori lokal.
- `git remote remove <nama_remote>`: Menghapus remote repository tertentu dari repositori lokal.

### Sinkronisasi dengan Repositori Pusat (Pull Request):
- `git fetch`: Mengambil perubahan dari repositori pusat tanpa menggabungkannya dengan branch aktif.
- `git pull origin <nama_branch>`: Mengambil perubahan dari repositori pusat dan menggabungkannya dengan branch aktif.
- `git push origin <nama_branch>`: Mengirim perubahan dari branch lokal ke branch yang sesuai di repositori pusat.

### Log dan Pencarian Commit:
- `git log`: Menampilkan log commit dalam repositori.
- `git log --oneline`: Menampilkan log commit dalam satu baris.
- `git log --author="nama_pengguna"`: Menampilkan log commit berdasarkan nama pengguna.
- `git log --grep="kata_kunci"`: Mencari commit berdasarkan kata kunci tertentu.

### Pembatalan Perubahan:
- `git reset <file>`: Membatalkan perubahan yang belum ditambahkan ke area staging.
- `git reset --soft HEAD~1`: Membatalkan commit terakhir dan mengembalikan perubahan ke area staging.
- `git reset --hard HEAD~1`: Menghapus commit terakhir dan mengembalikan perubahan ke kondisi sebelum commit tersebut.

### Lainnya:
- `git config`: Mengatur konfigurasi Git, seperti nama pengguna dan alamat email.
- `git stash`: Menyimpan perubahan sementara untuk diterapkan nanti.
- `git tag <nama_tag>`: Menandai titik spesifik dalam sejarah commit untuk memudahkan referensi di masa mendatang.

---

# NOTE PEMBUATAN BRANCH DI BIP

Branch di buat setiap hari, jadi misalkan sekarang tanggal 1 september 2024, berarti harus buat branch dengan tanggal 1 september 2024, contoh ada di bawah ini:

- `git checkout -b namaUser/tanggal-bulan-tahun`: Membuat branch baru dengan nama tertentu.

# Link Github Dokumentasi ini

```bash
 https://github.com/Luxxn12/dokumentasi-bip
```