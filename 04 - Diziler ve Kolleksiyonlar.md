## COLLECTIONS / KOLLEKSİYONLAR

### 00 – Diziler ve Koleksiyonlar Arasındaki Fark
- Diziler;
    - Aynı tür veriler saklanır.
    - Boyutu bellidir. Array.Resize ile yeniden boyutlandırılabilir. Dizilerin boyutları aşıldığında hata verir.
    - System.Array namespace’i içinde yer alır.
    - Elaman türleri belli olduğu için hızlıdır.
- Koleksiyonlar;
    - Farklı tür veriler saklanabilir.
    - Eleman sınırı yoktur. Bellekte kapladığı alan eleman sayısına göre otomatik olarak belirlenir.
    - System.Collections namespace’i içinde yer alır.
    - Eleman türleri belli olmadığı için boxing ve unboxing yapılır. Daha yavaştır.

### 01 – Diziler ( Tek Boyutlu ve Çok Boyutlu )
- Birden çok verinin bir değişken içinde saklanması durumudur.
- Dizi örnekleri
    - String, int gibi bilinen türlerde dizi oluşturma.
    - Class yapısından türüyen nesnelerden oluşan dizi örnekleri
- Tek boyutlu ve çok boyutlu (matris) diziler ve örnekler
- Dizi klonlama
    - Clone ve CopyTo metotlarıyla yapılır.
        - CopyTo kullanıldığında, hedef dizinin boyutunun, ana dizi boyutuna büyük veya eşit olmasına dikkat edilmelidir. Yoksa program çalıştığında hata verir.
    - Dizinin başka bir dizi değişkeni üzerine kopyalanmasını sağlar. 

```cs
int[] liste1 = { 1, 2, 3 };

int[] liste2 = liste1.Clone() as int[];

int[] liste3 = new int[4];
liste1.CopyTo(liste3, 0); 		// 0 başladığı index
```

- Dizi Sıralama

```cs
string[] liste = { "serhat", "ahmet", "mehmet" };

// A-Z sıralama
Array.Sort(liste);

// Ters Çevirme
Array.Reverse(liste);
```

- Dizi İçeriğini Sorgulama
    - Textbox üzerinde yazılana göre solda belirtilen ana dizinin elemanlarını, sağda filtreleyerek yeniden veren basit bir uygulama yapma.

```cs
string[] liste = { "serhat", "ahmet", "mehmet" };

foreach (var item in liste)
{
    if (item.Contains("et"))
    {
        this.listBox1.Items.Add(item);
    }
}
```

### 02 – ArrayList
- Tipi farklı olan değişkenleri tutabilir. Dizilerden ayrılan en önemli özelliği budur.
- Boyut belirtilmez
- Dezavantaj olarak, boxing ve unboxing yaptığı için perfonmaslı değildir. 
- Object içindeki nesnenin tipi “is” operatorü ile kontrol edilebilir. 

```cs
ArrayList liste = new ArrayList();
liste.Add("serhat");
liste.Add(25);
liste.Add(DateTime.Now);

foreach (var item in liste)
{
    if (item is string)
        this.listBox1.Items.Add(item);
    else if (item is int)
        this.listBox1.Items.Add("Sayı  : " + item.ToString());
    else
        this.listBox1.Items.Add("Diğer : " + item.ToString());
}
```

### 03 – Dictionary ve Hashtable
- Key ve Value yapısındaki değişkenleri tutar.
- İkisi arasıdaki fark, 
    - Dictionary türü bellidir.
    - Hashtable object tutar. 

```cs
Dictionary<int, string> liste = new Dictionary<int, string>();
liste.Add(1, "Serhat");
liste.Add(2, "Sönmez");

Hashtable liste2 = new Hashtable();
liste2.Add(1, "Ahmet");
liste2.Add("Yas", 25);

foreach (DictionaryEntry item in liste2)
{
    this.listBox1.Items.Add(item.Value);
}
```

### 04 – SortedList
- Key ve Value ikilisinden oluşur.
- Key değerine göre otomatik sıralama yaparak liste oluşturulur.
- Verilecek key değerlerinin türlerinin aynı olması lazım, aksi taktirde sıralama yapamayacağı için hata oluşacaktır.