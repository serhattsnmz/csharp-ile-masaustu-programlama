## HATALARI BULMAK VE KONTROL ETMEK

### 01 – Giriş
- Programın çalışması sırasında birçok nedenden ötürü hata meydana gelebilir.
- Bu hataların yakalanması, yönetilmesi ve gerekiyorsa loglanması gerekmektedir.
- Yakalanmayan hatalar programın çalışmasını durdurur ve son kullanıcının işlemini kesintiye uğratır. Bu da istenmeyen bir durumdur ve kaçınılması gerekmektedir.
- Kısa bir hata yakalama bloğu şu şekildedir; 

```cs
try
{
    // Hatanın oluşabileceği kod satırı
}
catch (Exception)
{
    // Hata oluştuğunda çalıştırılacak kod satırı
}
finally
{
    // Hata olsa da olmasa da çalıştırılacak kod satırı
}
```

### 02 – Exception Nesnesi
- Program içinde oluşan tüm hatalar Exception nesnesinden türetilir.
- Exception öz nesnesi kullanılarak tüm hatalar yakalanabilir. Bunun dışında özel hatalar yakanmak isteniyorsa, bunlar belirtilebilir.
- Birden çok catch bloğu açılabilir ve her hata için yapılacaklar ayrı ayrı belirtilebilir.
- Exception nesnesinin özellikleri :
    - **Message** : Oluşan hatanın açıklaması
    - **Source** : Hatanın oluştuğu nesne veya sınıf hakkında bilgi
    - **TargetSite** : Hatayı oluşturan metot hakkında bilgi 
    - **HelpLink** : Hataya atanmış yardım dosyasını görüntülemek için kullanılır.
    - **StackTrace** : Hataya neden olan çağrıları içeren stack (yığın) bilgilerini içerir.
    - **InnerException** : Oluşan iç hataları yakalamak için kullanılır. Eğer hiç iç hata oluşmazsa değer null döner. 
- Tüm exception tipleri:
    - https://msdn.microsoft.com/tr-tr/library/system.exception(v=vs.110).aspx

### 03 – Throw Deyimi 
- Yeni bir hata yaratmak için kullanılır. 
- Yaratılan hata, Exception sınıfından olabiliceği gibi, custom olarak biz de oluşturabiliriz.

### 04 – Exception.Data Özelliği
- Oluşan hata durumlarında, kullanıcı tarafından tanımlanan ek bilgilerin anahtar ve değer şeklinde bir koleksiyon içinde saklanması ve okunması amacıyla kullanılan özelliktir.
- Şu bilgiler saklanabilir : 
    - **stringInfo** : Oluşan hata durumuyla ilgili bilgi vermek amacıyla kullanılır.
    - **IntInfo** : Oluşan hata durumuyla ilgili sayısal değer bilgisi ( satır numarası, hata adedi vs. ) saklamak amacıyla kullanılır.
    - **DateTimeInfo** : Tarih ve zaman bilgisi içerir.
    - **ExtraInfo** : Oluşan hata durumuyla ilgili ayrıntılı bilgi vemek amacıyla kullanılır.
    - **MoreExtraInfo** : Daha fazla bilgi varsa burada saklanabilir.
- Örnekler : 

```cs
int deger, bolen, sonuc;
try
{
    deger = Convert.ToInt32(this.textBox1.Text);
    bolen = Convert.ToInt32(this.textBox2.Text);

    sonuc = deger / bolen;
}

// Sıfıra bölme hatası
catch (DivideByZeroException)
{
    MessageBox.Show("Sıfıra bölme hatası!");
}

// Aritmetik hata
catch(ArithmeticException)
{
    MessageBox.Show("Aritmetik hata!");
}

// Genel hata
catch
{
    MessageBox.Show("Tanımlanmamış hata!");
}
```

```cs
try
{
    int not = Convert.ToInt32(this.textBox1.Text);
    if (not < 45)
        MessageBox.Show("Kaldınız");
    else if (not >= 45 && not <= 100)
        MessageBox.Show("Geçtiniz");
    else
        throw new OverflowException();
}
catch (Exception ex)
{
    if (ex is OverflowException)
    {
        ex.Data["stringInfo"] = "100'den büyük bir değer giriniz!";
        ex.Data["Time"] = DateTime.Now;
    }
    foreach (DictionaryEntry bilgi in ex.Data)
        MessageBox.Show(bilgi.Key.ToString() + " " + bilgi.Value.ToString());
}
```