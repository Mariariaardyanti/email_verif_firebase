# Pengujian Email Verification Firebase Authentication menggunakan Postman
**Nama :** Maria Euphrasia  
**NIM :** 1123150050  
**Kelas :** TI SE 23  

## 🔥 Penjelasan

Dokumentasi ini berisi panduan implementasi Email Verification menggunakan Firebase Authentication serta pengujian endpoint API menggunakan Postman.  
Tujuan dari pengujian ini adalah untuk memastikan bahwa proses autentikasi pengguna berjalan dengan benar sebelum diintegrasikan ke dalam aplikasi Flutter.

---

# 📑 Table of Contents

1. Setup Firebase Project
2. Enable Authentication
3. Mendapatkan Firebase API Key
4. Login ke Postman
5. Membuat Pengujian Baru di Postman
6. Registrasi User via Firebase REST API
7. Mengirim Email Verification
8. Cek Status Verifikasi Email

---

# 1️⃣ Setup Firebase Project

Pertama kita perlu membuat project baru di **Firebase Console**.

### Langkah-langkah

1. Buka halaman  
   https://console.firebase.google.com

2. Klik **Add Project**

3. Masukkan **Nama Project**

4. Klik **Continue** hingga project selesai dibuat.

### Tampilan pembuatan Project

![Create Firebase Project](/assets/images/1.png)

---

# 2️⃣ Enable Authentication

Selanjutnya kita perlu mengaktifkan fitur **Authentication**.

### Langkah-langkah

1. Pada sidebar Firebase klik **Build**
2. Pilih menu **Authentication**
3. Klik **Get Started**

![Firebase Authentication](/assets/images/2.png)

### Mengaktifkan Email / Password

1. Masuk ke tab **Sign-in Method**
2. Klik **Email/Password**
3. Aktifkan **Enable**
4. Klik **Save**

![Enable Email Password](/assets/images/3.png)

---

# 3️⃣ Mendapatkan Firebase API Key

Untuk menggunakan Firebase REST API melalui Postman, kita perlu mendapatkan **Firebase API Key**.  
API Key ini diperoleh ketika kita menambahkan **Web App** pada project Firebase.

### Langkah-langkah

1. Buka **Firebase Console**
2. Masuk ke **Project Settings**
3. Scroll ke bagian **Your Apps**
4. Klik ikon **Web (</>)** untuk menambahkan aplikasi web
5. Masukkan **nama aplikasi web**
6. Klik **Register App**

Setelah proses registrasi selesai, Firebase akan menampilkan konfigurasi aplikasi seperti berikut:

![Firebase Settings](/assets/images/4.png)

---

# 4️⃣ Login ke Postman

Setelah mendapatkan Firebase API Key, langkah berikutnya adalah membuka aplikasi **Postman** untuk melakukan pengujian Firebase REST API.

---

# 5️⃣ Membuat Pengujian Baru di Postman

### Langkah-langkah

1. Buat **Collection**
2. Buat **Environment**

Klik **Environments → Create New**

Ubah nama menjadi:

```
My Environment
```

Tambahkan variable:

| Variable | Value |
|---------|------|
| FIREBASE_API_KEY | API KEY Firebase |

![Setup Environment](/assets/images/5.png)

---

# 6️⃣ Registrasi User menggunakan Firebase REST API

Pada tahap ini kita akan melakukan registrasi user baru menggunakan Firebase Authentication API.

### Endpoint

```
POST https://identitytoolkit.googleapis.com/v1/accounts:signUp?key={{FIREBASE_API_KEY}}
```

### Setup Request di Postman

**Method**

```
POST
```

**Headers**

```
Content-Type : application/json
```

**Body**

```
{
  "email": "user@email.com",
  "password": "12345678",
  "returnSecureToken": true
}
```

![Register User](/assets/images/6.png)

---

### Response Berhasil

![Register Success](/assets/images/7.png)

---

# 7️⃣ Mengirim Email Verification

Setelah user berhasil registrasi, kita perlu mengirim email verifikasi.

### Endpoint

```
POST https://identitytoolkit.googleapis.com/v1/accounts:sendOobCode?key={{FIREBASE_API_KEY}}
```

### Body Request

```
{
  "requestType": "VERIFY_EMAIL",
  "idToken": "{{ID_TOKEN}}"
}
```

![Send Verification](/assets/images/8.png)

Setelah request berhasil, Firebase akan mengirim email verifikasi.

Biasanya email akan masuk ke:

- Inbox
- Spam

Klik **Verify Email** untuk memverifikasi akun.

---

### Email Verifikasi Diterima

Setelah request pengiriman verifikasi berhasil dilakukan melalui Postman, Firebase akan mengirimkan email verifikasi ke alamat email pengguna.

Berikut adalah contoh email verifikasi yang diterima oleh pengguna.

![Email Verification Inbox](/assets/images/9.png)

---

### Halaman Email Berhasil Diverifikasi

Setelah pengguna menekan tombol **Verify Email** pada email tersebut, Firebase akan menampilkan halaman konfirmasi bahwa email telah berhasil diverifikasi.

![Email Verified](/assets/images/10.png)

---

# 9️⃣ Cek Status Verifikasi Email

Untuk mengecek apakah email sudah diverifikasi, kita bisa menggunakan endpoint berikut.

### Endpoint

```
POST https://identitytoolkit.googleapis.com/v1/accounts:lookup?key={{FIREBASE_API_KEY}}
```

### Body Request

```
{
"idToken": "{{ID_TOKEN}}"
}
```

### Cek Status Verif

Kemudian kita dapat melakukan pengecekan status verifikasi melalui Postman menggunakan endpoint **accounts:lookup**.  
Jika email sudah diverifikasi maka response akan menampilkan nilai berikut:

```
"emailVerified": true
```

Berikut adalah hasil pengecekan status verifikasi email melalui Postman.

![Status Verifikasi Email](/assets/images/11.png)

---

# ✅ Kesimpulan

Dengan menggunakan Firebase Authentication dan Postman, kita dapat melakukan pengujian API autentikasi sebelum mengimplementasikannya pada aplikasi Flutter.

Proses yang dilakukan meliputi:

- Setup Firebase Project
- Mengaktifkan Authentication
- Mendapatkan API Key
- Registrasi User
- Mengirim Email Verification
- Verifikasi Email
- Mengecek Status Verifikasi

Metode ini membantu memastikan sistem autentikasi berjalan dengan baik sebelum digunakan pada aplikasi mobile.

---