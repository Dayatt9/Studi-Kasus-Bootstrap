## Pertanyaan

Berikut adalah penjelasan untuk beberapa keputusan desain dan teknis yang dibuat selama pengembangan.

### a. Mengapa memilih konfigurasi `col` tertentu untuk tiap breakpoint?

Keputusan konfigurasi kolom (`col-12`, `col-md-4`, dll.) didasarkan pada prinsip **desain responsif** dan **pengalaman pengguna (UX)** di berbagai ukuran layar.

* **Mobile (`col-12`)**: Di layar kecil (lebar ≤ 576px), saya menggunakan 1 kolom penuh. Ini memastikan setiap gambar postingan ditampilkan secara maksimal, jelas, dan mudah di-tap tanpa membuat pengguna harus melakukan zoom. Pengguna bisa fokus pada satu konten pada satu waktu saat melakukan scroll.

* **Tablet (`col-md-6` atau `col-md-4`)**: Di layar tablet (lebar ≥ 768px), ada lebih banyak ruang horizontal. Saya menggunakan 2 atau 3 kolom. Ini adalah keseimbangan yang baik antara menampilkan lebih banyak konten secara bersamaan dan menjaga agar ukuran gambar tetap nyaman dilihat.

* **Desktop (`col-lg-3`)**: Di layar desktop (lebar ≥ 992px), saya menggunakan 4 kolom. Ini memaksimalkan pemanfaatan ruang layar yang lebar, memungkinkan pengguna untuk memindai (scan) banyak postingan dengan cepat tanpa mengorbankan kualitas visual.

### b. Bagaimana kamu memastikan tombol Follow/Edit Profile tetap mudah dijangkau di mobile?

Saya memastikan tombol mudah dijangkau di mobile dengan pendekatan **Mobile-First** dan penempatan yang logis.

1.  **Struktur HTML**: Di dalam HTML, blok tombol (`<div>` yang berisi tombol) ditempatkan secara alami di bawah nama pengguna dan statistik. Pada tampilan mobile, ini membuatnya muncul di baris baru yang terpisah, memberikan area tap yang luas dan jelas.
2.  **Pemanfaatan Flexbox Utilities**: Saya menggunakan utility `d-flex` dan `flex-wrap` dari Bootstrap. Pada layar mobile, item-item (username, tombol) akan secara otomatis "turun" ke baris baru jika tidak cukup ruang. Kemudian, pada breakpoint yang lebih besar (misalnya `md`), mereka akan kembali sejajar karena ada lebih banyak ruang. Ini memastikan fungsionalitas utama tidak tersembunyi atau terlalu kecil di mobile.

### c. Jika postingan bertambah jadi 50, apa potensi masalah dan bagaimana solusi gridmu mengatasinya?

Jika postingan bertambah menjadi 50+, akan muncul dua masalah utama: **performa** dan **pengalaman pengguna (UX)**.

* **Potensi Masalah**:
    1.  **Waktu Muat Lambat**: Memuat 50+ gambar sekaligus akan membuat halaman sangat berat dan lambat dibuka, terutama bagi pengguna dengan koneksi internet yang lambat.
    2.  **UX yang Buruk**: Pengguna harus melakukan scroll yang sangat panjang untuk melihat semua konten, yang bisa jadi melelahkan.

* **Bagaimana Grid Mengatasinya (dan Keterbatasannya)**:
    * **Sistem grid Bootstrap sendiri akan menangani tata letaknya dengan sempurna**. Tidak peduli ada 50 atau 500 gambar, grid akan terus membungkusnya ke baris baru sesuai aturan kolom (`col-md-4`, `col-lg-3`, dst.). Jadi, secara visual, **tata letak tidak akan rusak**.
    * Namun, **grid tidak menyelesaikan masalah performa dan UX**. Solusi sebenarnya berada di level aplikasi, bukan hanya layout. Solusi yang umum digunakan adalah:
        1.  **Pagination**: Membagi 50 postingan ke dalam beberapa halaman (misal, 12 postingan per halaman).
        2.  **Infinite Scrolling**: Memuat 12 postingan pertama, dan saat pengguna scroll ke bawah, postingan berikutnya akan dimuat secara otomatis. Ini adalah pendekatan yang digunakan oleh Instagram asli dan memberikan pengalaman yang lebih mulus.
