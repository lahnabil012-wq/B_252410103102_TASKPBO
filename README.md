# B_252410103102_TASKPBO

using System;
using System.Collections.Generic;

class Item
{
    public string Judul { get; set; }
    public int Tahun { get; set; }

    public Item(string judul, int tahun)
    {
        Judul = judul;
        Tahun = tahun;
    }

    public virtual void Deskripsi()
    {
        Console.WriteLine($"Item: {Judul}, Tahun: {Tahun}");
    }

    public void InfoItem()
    {
        Console.WriteLine($"Judul: {Judul}");
        Console.WriteLine($"Tahun: {Tahun}");
    }
}

class Buku : Item
{
    public string Penulis { get; set; }

    public Buku(string judul, int tahun, string penulis)
        : base(judul, tahun)
    {
        Penulis = penulis;
    }

    public override void Deskripsi()
    {
        Console.WriteLine(
            $"Buku: {Judul}, Tahun: {Tahun}, Penulis: {Penulis}");
    }

    public void CekPenulis()
    {
        Console.WriteLine($"Penulis buku: {Penulis}");
    }
}

class Majalah : Item
{
    public int Edisi { get; set; }

    public Majalah(string judul, int tahun, int edisi)
        : base(judul, tahun)
    {
        Edisi = edisi;
    }

    public override void Deskripsi()
    {
        Console.WriteLine(
            $"Majalah: {Judul}, Tahun: {Tahun}, Edisi: {Edisi}");
    }

    public void InfoEdisi()
    {
        Console.WriteLine($"Edisi majalah: {Edisi}");
    }
}

class Novel : Buku
{
    public Novel(string judul, int tahun, string penulis)
        : base(judul, tahun, penulis) { }

    public override void Deskripsi()
    {
        Console.WriteLine(
            $"Novel: {Judul}, Tahun: {Tahun}, Penulis: {Penulis}");
    }

    public void BacaSinopsis()
    {
        Console.WriteLine(
            $"Sinopsis {Judul}: Cerita tentang perjalanan dan kehidupan tokoh utama.");
    }
}

class Komik : Buku
{
    public Komik(string judul, int tahun, string penulis)
        : base(judul, tahun, penulis) { }

    public override void Deskripsi()
    {
        Console.WriteLine(
            $"Komik: {Judul}, Tahun: {Tahun}, Penulis: {Penulis}");
    }

    public void TampilkanIlustrasi()
    {
        Console.WriteLine($"Ilustrasi komik {Judul} ditampilkan.");
    }
}

class MajalahAnak : Majalah
{
    public MajalahAnak(string judul, int tahun, int edisi)
        : base(judul, tahun, edisi) { }

    public override void Deskripsi()
    {
        Console.WriteLine(
            $"Majalah Anak: {Judul}, Tahun: {Tahun}, Edisi: {Edisi}");
    }

    public void KategoriAnak()
    {
        Console.WriteLine("Kategori: Pendidikan dan hiburan anak.");
    }
}

class MajalahTeknologi : Majalah
{
    public MajalahTeknologi(string judul, int tahun, int edisi)
        : base(judul, tahun, edisi) { }

    public override void Deskripsi()
    {
        Console.WriteLine(
            $"Majalah Teknologi: {Judul}, Tahun: {Tahun}, Edisi: {Edisi}");
    }

    public void TopikTeknologi()
    {
        Console.WriteLine(
            "Topik: Komputer, pemrograman, dan perkembangan teknologi.");
    }
}

class Perpustakaan
{
    private List<Item> koleksi = new List<Item>();

    public void TambahItem(Item item)
    {
        koleksi.Add(item);
    }

    public void DaftarItem()
    {
        Console.WriteLine("\n=== DAFTAR ITEM PERPUSTAKAAN ===");

        foreach (Item item in koleksi)
        {
            item.Deskripsi();
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        Perpustakaan perpustakaan = new Perpustakaan();

        Novel novel = new Novel(
            "Laskar Pelangi", 2005, "Andrea Hirata");

        Komik komik = new Komik(
            "Si Juki", 2017, "Faza Meonk");

        Majalah majalah = new Majalah(
            "Majalah Nasional", 2024, 10);

        MajalahAnak anak = new MajalahAnak(
            "Bobo", 2025, 12);

        MajalahTeknologi teknologi = new MajalahTeknologi(
            "Teknologi Digital", 2026, 5);

        // Menambahkan item ke perpustakaan
        perpustakaan.TambahItem(novel);
        perpustakaan.TambahItem(komik);
        perpustakaan.TambahItem(majalah);
        perpustakaan.TambahItem(anak);
        perpustakaan.TambahItem(teknologi);

        // Menampilkan seluruh koleksi
        perpustakaan.DaftarItem();

        // Nomor 1: Override Deskripsi()
        Console.WriteLine("\n=== NOMOR 1 ===");
        novel.Deskripsi();
        majalah.Deskripsi();

        // Nomor 2: Method khusus Novel
        Console.WriteLine("\n=== NOMOR 2 ===");
        novel.BacaSinopsis();

        // Nomor 3: Informasi lengkap Novel
        Console.WriteLine("\n=== NOMOR 3 ===");
        novel.InfoItem();
        novel.CekPenulis();

        // Nomor 4: Method khusus MajalahTeknologi
        Console.WriteLine("\n=== NOMOR 4 ===");
        teknologi.TopikTeknologi();

        // Nomor 5: Polymorphism menggunakan Item
        Console.WriteLine("\n=== NOMOR 5 ===");
        Item item = komik;
        item.Deskripsi();

        // Method khusus Komik
        komik.TampilkanIlustrasi();

        // Method khusus Majalah dan turunannya
        Console.WriteLine("\n=== METHOD KHUSUS LAINNYA ===");
        majalah.InfoEdisi();
        anak.KategoriAnak();

        Console.WriteLine("\nProgram selesai.");
        Console.ReadKey();
    }
}
