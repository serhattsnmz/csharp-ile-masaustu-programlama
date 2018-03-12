## TEMEL I/O VE STRING İŞLEMLERİ
- IO : Input – Output anlamına gelir 
- Dosya ve klasör işlemleri genellikle bu kütüphane altında yapılır.

### 01 – Dosya ve Klasör Oluşturma
- System.IO.Directory : Klasör işlemleri yapmızı sağlar.
- System.IO.File : Dosya işlemleri yapmamızı sağlar. 

```cs
void klasor_olustur()
{
    string dosyaYolu = Application.StartupPath + "/yeni klasor";

    DirectoryInfo klasor = Directory.CreateDirectory(dosyaYolu);

    MessageBox.Show(klasor.FullName);
    MessageBox.Show(klasor.Name);
    MessageBox.Show(klasor.CreationTime.ToString());

    if(Directory.Exists(dosyaYolu))
        MessageBox.Show("Klasör oluşturuldu.");
}
```

```cs
void dosya_olustur()
{
    string dosyaYolu = Application.StartupPath + "/yeni klasor/deneme.txt";

    FileStream file = File.Create(dosyaYolu);
    file.Dispose();

    if(File.Exists(dosyaYolu))
        MessageBox.Show("Dosya oluşturuldu.");
}
```

- Dizin oluşturuken;
    - Dizin daha önce varsa, tekrar oluşturulmaz.
    - DirectoryInfo olarak dizin bilgileri alınıp üzerinde işlemler yapılabilir.
- Dosya oluştururken;
    - Dosyanın belirtilen konumu mevcut değilse, dosya oluşturulmaz.
    - Bu nedenle öncelikle dosya konumu oluşturulmalı veya var olan bir dosya konumu verilmelidir.
    - Dosya oluşturulduktan sonra dispose edilmeyene kadar program tarafından açık kalır. Bu nedenle dosya silinmesi başarısız olur. Bunu engellemek için dosya oluşturulduktan sonra dispose edilmelidir.
    - FileStream ile dosya bilgisi alınıp üzerinde işlemler yapılabilir.
        - Bu işlemler dispose edilmeden önce yapılmalıdır.

### 02 – Dosya Okuma ve Yazma 
```cs
void dosyaya_yaz ()
{
    string text = this.textBox1.Text;
    string dosyaYolu = Application.StartupPath + "/yeni klasor/deneme.txt";
    Encoding encoding = Encoding.GetEncoding("iso-8859-9");

    File.WriteAllText(dosyaYolu, text, encoding);
    // File.WriteAllLines  = string[]   ifadeleri yazar
    // File.WriteAllBytes  = byte[]     ifadeleri yazar

    File.AppendAllText(dosyaYolu, text, encoding);
    // File.AppendAllLines() = IEnumerable<string> ifadeleri yazar   
}
```

### 03 – Klasör İçindeki Dosyaları Gösterme
```cs
void klasor_icindeki_dosyalari_oku ()
{
    FolderBrowserDialog fbd = new FolderBrowserDialog();
    DialogResult result = fbd.ShowDialog();

    if (result == DialogResult.OK)
    {
        this.listBox1.Items.Clear();
        string[] dosyalar = Directory.GetFiles(fbd.SelectedPath, "*.*");

        foreach (var dosya in dosyalar)
        {
            FileInfo info = new FileInfo(dosya);
            this.listBox1.Items.Add(info.Name);
        }
    }
}
```

### 04 – File Nesnesi Metotları 
- **Copy** : Dosya kopyalar.
- **Create** : Yeni bir dosya oluşturur.
- **Enctypt** : Bir dosyayı şifrelemek için kullanılır.
- **Decrpyt** : Şifrelenmiş bir dosyayı çözümler.
- **Delete** : Dosya siler. Dosya mevcut değilse hata döndürmez.
- **Exists** : Dosyanın mevcut olup olmadığını kontrol eder.
- **GetCreationTime** : Dosya veya klasörün oluşturulma tarihini geriye döndürür.
- **GetLastAccessTime** : Son erişim tarihini geriye döndürür.
- **GetLastWriteTime** : Son yazım tarihini geriye döndürür.
- **Move** : Belirtilen dosyayı taşır.
- **Open** : Dosyayı FileStream nesnesi olarak açar.
- **OpenRead** : Belirtilen dosyayı okumak amacıyla açar.
- **OpenWrite** : Belirtilen dosyayı yazmak üzere açar.

### 05 – Directory Nesnesi Metotları 
- **Delete** : Bir klasörü içeriğiyle birlikte siler
- **Exists** : Klasörün mevcut olup olmadığını kontrol eder. 
- **GetCurrentDirectory** : Aktif çalışma dizinini geriye döndürür.
- **GetDirectories** : Belirtilen klasörün alt klasörlerini döndürür.
- **GetFiles** : Belirtilen klasörün alt dosyalarını döndürür.
- **GetFileSystemEntries** : Klasör altındaki tüm alt klasör ve dosyaları döndürür.
- **GetParent** : Belirtilen klasörün bağlı olduğu ana klasör ismini geriye döndürür.
- **Move** : İçeriğiyle birlikte taşıma işleminde kulanılır.