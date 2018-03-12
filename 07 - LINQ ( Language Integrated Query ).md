##LINQ ( Language Integrated Query )

### 01 – Giriş
- Dil ile bütünleştirilmiş sorgu anlamı taşır.
- Dizileri, koleksiyon yapılarını, dosyaları, XML yapılarını ve veritabanlarını sorgulamak için kullanılan bir yapıdır. 
- İki türü vardır :
    - Klasik 
    - LINQ with Lambda Expressions

```cs
int[] sayilar = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

IEnumerable<int> sayi1= from veri in sayilar
                        where veri > 5
                        select veri;

List<int> sayi2 = sayilar.Where(veri => veri > 5).ToList();

foreach (var sayi in sayi2)
    MessageBox.Show(sayi.ToString());
```

### 02 – Sık Kullanılan Operatorler
- Where
    - Birden fazla sorgu varsa & ve | ifadeleri kullanılabilir.
- Select
    - Class yapısı içinde basit bir where ve select sorgusuyla örnek yapma.
- Distinct
    - Liste içindeki tekrarlayan değerlerin bir kere yazılmasını sağlar
- Max ve Min
    - Liste içindeki en yüksek ve en düşük değerleri bulmak amacıyla kullanılır.
- Count
    - Sorgu kriterlerine uyan kayıtları saymak amacıyla kullanılır.
- OrderBy 
    - Sıralama amacıyla kullanılır.
- Ayrıntılı bilgi : 
    - https://msdn.microsoft.com/en-us/library/bb308959.aspx
    - https://www.tutorialspoint.com/linq/index.htm
