class Buku:
    def __init__(self, judul, pengarang, tahun_terbit, isbn):
        self.judul = judul
        self.pengarang = pengarang
        self.tahun_terbit = tahun_terbit
        self.isbn = isbn
        self.status = "tersedia"  # Status: tersedia atau dipinjam

    def tampilkan_info_buku(self):
        print(f"Judul: {self.judul}, Pengarang: {self.pengarang}, Tahun Terbit: {self.tahun_terbit}, ISBN: {self.isbn}, Status: {self.status}")


class Anggota:
    def __init__(self, nama, nomor_anggota, alamat):
        self.nama = nama
        self.nomor_anggota = nomor_anggota
        self.alamat = alamat
        self.daftar_pinjaman = []  # List buku yang dipinjam

    def tampilkan_info_anggota(self):
        print(f"Nama: {self.nama}, Nomor Anggota: {self.nomor_anggota}, Alamat: {self.alamat}")
        print("Daftar Buku yang Dipinjam:")
        for buku in self.daftar_pinjaman:
            buku.tampilkan_info_buku()


class Perpustakaan:
    def __init__(self):
        self.daftar_buku = []
        self.daftar_anggota = []

    def tambah_buku(self, buku):
        self.daftar_buku.append(buku)
        print(f"Buku '{buku.judul}' berhasil ditambahkan ke perpustakaan.")

    def daftar_buku_tersedia(self):
        print("Daftar Buku Tersedia:")
        for buku in self.daftar_buku:
            if buku.status == "tersedia":
                buku.tampilkan_info_buku()

    def tambah_anggota(self, anggota):
        self.daftar_anggota.append(anggota)
        print(f"Anggota '{anggota.nama}' berhasil didaftarkan ke perpustakaan.")

    def pinjam_buku(self, nomor_anggota, isbn):
        anggota = next((a for a in self.daftar_anggota if a.nomor_anggota == nomor_anggota), None)
        buku = next((b for b in self.daftar_buku if b.isbn == isbn and b.status == "tersedia"), None)

        if anggota and buku:
            buku.status = "dipinjam"
            anggota.daftar_pinjaman.append(buku)
            print(f"Buku '{buku.judul}' berhasil dipinjam oleh anggota '{anggota.nama}'.")
        else:
            print("Peminjaman gagal: Anggota atau buku tidak ditemukan, atau buku tidak tersedia.")

    def kembalikan_buku(self, nomor_anggota, isbn):
        anggota = next((a for a in self.daftar_anggota if a.nomor_anggota == nomor_anggota), None)

        if anggota:
            buku = next((b for b in anggota.daftar_pinjaman if b.isbn == isbn), None)
            if buku:
                buku.status = "tersedia"
                anggota.daftar_pinjaman.remove(buku)
                print(f"Buku '{buku.judul}' berhasil dikembalikan.")
            else:
                print("Pengembalian gagal: Buku tidak ditemukan dalam daftar pinjaman anggota.")
        else:
            print("Pengembalian gagal: Anggota tidak ditemukan.")
