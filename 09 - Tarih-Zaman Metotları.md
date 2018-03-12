## TARİH ZAMAN METODLARI

### 01 – DateTime Nesnesi Özellikleri
- DateTime nesnesi oluşturularak, verilen sayısal ifadeler tarih formatına dönüştürülebilir.
- ToLongDateString
- ToShortDateString
- ToLongTimeString
- ToShortTimeString
- Year – Month - Day
- Hour – Minute – Second – Milisecond

### 02 – Tarih İşlemleri
- Add* fonksiyonları kullanılarak tarih üzerine ekleme ve çıkarma işlemleri yapılabilir.
- Çıkarma işlemleri için negatif sayı girilmesi yeterlidir.

### 03 – TimeSpan Nesnesi
- Absulute Time 	-> DateTime
- Sliding Time 	-> TimeSpan
- Tarih aralığı belirtmek amacıyla kullanılır.
- Sonucu gün, saat, dakika, saniye, milisaniye olarak döndürür.
- Tarihlerin arasındaki fark bulunurken, sonuç TimeSpan olarak döner.
- Total* metodları kullanılarak, sonuç istenilen bir değerde döndürülebilir.

### 04 – Tarih ve Zamanları Karşılaştırmak
- CompareTo
    - `int sonuc = tarih1.CompareTo(tarih2);`
    - Sonuç ; 
        - -1 -> 1. Tarih küçük
        - 0	-> Tarihler eşit
        - 1	-> 1. Tarih büyük

### 05 – String Sınıfı Kullanarak Biçimlendirme Yapmak
- https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings
- http://www.csharp-examples.net/string-format-datetime/
