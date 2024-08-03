# Program-Manajemen-Perpustakaan

  Program Manajemen Perpustakaan ini dibuat menggunakan struktur data binary search tree. Program ini memiliki fitur berupa menambahkan buku, menampilkan semua buku yang tersedia, mencari buku berdasarkan ID dari buku, dan menghapus buku berdasarkan ID buku.

  ID dari buku sendiri dibuat berdasarkan urutan abjad dari masing-masing huruf pada judul buku. ID ini akan menentukan posisi buku dalam tree (jika ID buku tersebut bukan sebagai root atau data pertama yang masuk dalam tree). Collision handling dalam program ini aktif apabila terdapat ID buku yang sama. ID buku yang sama yang baru dimasukkan akan dikalikan 2 sehingga tidak ada ID buku yang sama. Jika dimasukkan buku dengan judul yang sama, maka buku yang akan dimasukkan akan ditolak.

  Contoh kasus misal terdapat buku berjudul "Hampa" yang ingin ditambahkan, maka user tinggal memilih menu 3 pada menu utama lalu mengisi data buku yang ingin ditambahkan. Buku berjudul "Hampa" akan mendapat ID 39 (H + A + M + P + A --> 8 + 1 + 13 + 6 + 1 = 39) dan tersimpan dalam tree pada posisi root. Lalu ditambahkan buku baru berjudul "Paham" yang sama-sama memiliki ID 39 dengan buku berjudul "Hampa". Karena sudah terdapat ID 39 pada tree, maka collision handling program ini aktif sehingga ID dari buku "Paham" dilipatgandakan 2 kali lipat sehingga buku "Paham" memiliki ID 78 dan tersimpan dalam posisi right child.

  Buku-buku tersebut juga bisa dicari dan dihapus menggunakan ID masing-masing buku. Jika menggunakan fitur cari, maka data-data buku yang sesuai dengan ID yang dimasukkan (misal 39) akan ditampilkan (judul, genre, ID, dll.). Hal ini juga berlaku pada fitur hapus buku, dimana user akan diminta konfirmasi apabila ingin menghapus buku.
