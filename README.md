### Judul Proyek: **Sistem Transaksi Properti Desentralisasi 

Proyek ini melibatkan pembangunan sistem transaksi properti desentralisasi menggunakan blockchain Ethereum. Sistem ini memungkinkan pemilik properti untuk memasang iklan penjualan rumah dengan harga tetap (10 Ether). Sistem ini melibatkan tiga pihak utama:
- **Pemilik Properti**: Individu yang memiliki rumah dan memasang iklan penjualan.
- **Agen**: Pihak ketiga yang bertindak sebagai perantara dalam transaksi dan menerima komisi sebesar 1 Ether.
- **Pembeli**: Individu yang membeli rumah dari pemilik properti, difasilitasi oleh agen.

Transaksi ini memastikan bahwa agen secara otomatis menerima komisi mereka, sementara sisa saldo ditransfer ke pemilik properti. Kontrak pintar menjamin transparansi, keamanan, dan ketidakubahannya sepanjang proses transaksi. Rumah hanya akan ditransfer ke pembeli setelah pembayaran berhasil diselesaikan.

---

### Fitur:

1. **Desentralisasi**: Semua operasi, termasuk pembayaran dan transfer properti, dilakukan di blockchain Ethereum, memastikan transparansi dan menghilangkan kebutuhan akan perantara (kecuali agen).  

2. **Komisi Agen**: Agen secara otomatis menerima komisi sebesar 1 Ether selama transaksi.  

3. **Kontrol Akses Berbasis Peran**: Sistem menerapkan kontrol akses di mana agen tidak dapat membeli properti secara langsung dan hanya pemilik properti yang dapat menunjuk agen.

4. **Penanganan Pembayaran Aman**: Pembeli harus membayar tepat 10 Ether untuk melanjutkan pembelian, memastikan konsistensi dan penanganan transaksi yang benar.

5. **Peralihan Kepemilikan**: Setelah transaksi, kepemilikan rumah dialihkan kepada pembeli, dan pemilik properti melepaskan kendali.

---

### Struktur Proyek:

Kontrak ini dikembangkan menggunakan Solidity dan berjalan di blockchain Ethereum. Kontrak ini menangani tiga peran utama, dan fungsi-fungsinya disesuaikan dengan peserta spesifik dalam proses transaksi.

#### Peserta Utama:
1. **Pemilik Properti**: Pengembang kontrak adalah pemilik properti awal.
2. **Agen**: Agen ditunjuk oleh pemilik properti untuk memfasilitasi transaksi.
3. **Pembeli**: Individu yang mengirim Ether untuk membeli rumah.

---

### Desain Kontrak:

#### Variabel:

- **propertyOwner**: Menyimpan alamat individu yang memiliki properti. Alamat ini ditetapkan saat kontrak diimplementasikan.
- **agent**: Menyimpan alamat agen yang ditunjuk oleh pemilik properti.
- **buyer**: Menyimpan alamat pembeli setelah rumah dibeli.
- **housePrice**: Harga total rumah (10 Ether).
- **agentCommission**: Komisi tetap untuk agen (1 Ether).
- **houseSold**: Bendera boolean yang memastikan rumah hanya dapat dijual sekali.

#### Modifier:

- **onlyPropertyOwner**: Memastikan hanya pemilik properti yang dapat melakukan tindakan tertentu (seperti menunjuk agen).
- **notAgent**: Mencegah agen membeli properti secara langsung.

#### Fungsi:

1. **constructor()**: 
   - Menginisialisasi kontrak dan menetapkan pemilik properti sebagai pengembang kontrak.

2. **assignAgent(address payable _agent)**:
   - Memungkinkan pemilik properti menunjuk agen untuk memfasilitasi penjualan.
   - Hanya dapat dipanggil oleh pemilik properti (diterapkan oleh modifikator `onlyPropertyOwner`).

3. **buyHouse()**:
   - Memungkinkan pembeli untuk membeli rumah dengan mengirimkan tepat 10 Ether.
   - Agen secara otomatis menerima komisi sebesar 1 Ether, dan sisa 9 Ether ditransfer ke pemilik properti.
   - Kepemilikan rumah beralih ke pembeli setelah transaksi.
   - Fungsi ini memeriksa bahwa pembeli bukan agen dan memastikan rumah belum terjual sebelumnya.

4. **getOwner()**:  
   - Memungkinkan siapa pun untuk memeriksa pemilik properti saat ini. Sebelum penjualan, pemilik adalah pemilik properti; setelah penjualan, pemilik adalah pembeli.

---

### Panduan Langkah demi Langkah:

1. **Deploy Kontrak**: 
   - Kontrak diimplementasikan oleh `propertyOwner`. Akun ini akan ditunjuk sebagai pemilik awal properti.  

2. **Menunjuk Agen**:  
   - Pemilik properti menggunakan fungsi `assignAgent()` untuk menunjuk agen dengan menyediakan alamat agen.  

3. **Membeli Properti**:
   - Fungsi `buyHouse()` memungkinkan pembeli untuk membeli rumah dengan mengirimkan tepat 10 Ether. Fungsi ini memastikan pembeli bukan agen dan rumah masih tersedia.  

4. **Komisi dan Transfer Kepemilikan**:  
   - Setelah menerima pembayaran, 1 Ether secara otomatis ditransfer ke agen, dan sisa 9 Ether dikirim ke pemilik properti. Kepemilikan rumah kemudian ditransfer ke pembeli.
   
5. **Pengecekan Kepemilikan**:  
   - Fungsi `getOwner()` memungkinkan siapa pun untuk memverifikasi pemilik saat ini dari rumah.

---

### Deployment dan Pengujian:

Kontrak pintar ini dapat di-deploy dan diuji menggunakan **Remix IDE**, alat yang kuat untuk pengembangan kontrak pintar Ethereum.
