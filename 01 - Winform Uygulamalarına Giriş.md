## WinForm TABANLI UYGULAMALARA GİRİŞ

### 01 – Windows Form Application Projesi Oluşturma
- Yeni bir WinForm oluşturup solution yapısına bakma
    - Program.cs içindeki main fonksiyonu, konsoldaki gibi, ilk çalışan uygulamadır.
    - Main fonksiyon içinde, başlangıçta form yapısını çalıştıran bir yönlendirme vardır.
- Form.cs dosyası içine bakma
    - Tıklandığında Design modda başlar.
    - Form içindeki class yapısı partial olarak yazılmıştır. 
        - Bunun bir kısmı, Initialize metodunun da bulunduğu design kısmıdır.
        - Diğer bir kısmı ise event’ların yazıldığı asıl kullanacağımız kısımdır.
        - Design ile alakalı düzenlemeler yapıldığında, Initialize metodunda değişiklikler yapılır.
- ToolBox ekranını tanıma
- Properties ekranını tanıma
- Event nedir? Properties ekranındaki eventlar
    - Olay tanımlamadan önce nesnenin isminin değiştirilmesi daha uygun olur. Çünkü gerekli metotlar bu isim baz alınarak oluşturulur ve daha sonra değiştirilmesi sıkıntılıdır.
    - Event silinecekse yine event listesi içinde silme yapılmalıdır. Sadece fonksiyonun silinmesiyle event silinmez. Ayrıca Designer class’ının içindeki olay kısmı da silinmelidir.
    - Manuel olarak event fonksiyonu yazma ve bu fonksiyonu eventlar üzerine atama
        - Event bölümündeki combobox açılarak, event fonksiyonları seçilebilir.
        - Parametre olarak kısmının (object sender, EventArgs e) yazılması zorunludur yoksa seçilemez. 

```cs
private void Kapat(object sender, EventArgs e)
{
    this.Close();
}
```

- Form_Load olayı
- Debug.Print() ve MessageBox.Show()

### 02 – Temel Kontroller ve Özellikleri
- Kontrol ekleme yöntemleri
    - Üzerine çift tıklama
    - Sürükleyip ekrana bırakma
    - Seçtikten sonra boyutlandırarak ekleme
- Kontrollerin yerleşimi ve düzeni
    - Kontroller sürüklendiği zaman, otomatik çıkan klavuz çizgilerine göre uygun yere yerleştirilebilir.
    - Ayrıca birden fazla kontrol seçilerek, format menüsünden ya da üst menü kısmındaki kısa yollardan, hizalama, boyutlandırma yapılabilir.
- Temel Kontroller :
    - Label
    - TextBox
        - Max 255 karakterlik bilgi girilebilir.
    - Button
    - ComboBox
    - ListBox
    - TreeView
    - CheckBox
    - CheckedListBox
    - RadioButton

### 03 – Formlar
- Formlar arası geçiş :
    - Öncelikle eklenen form için bir nesne türetilmelidir.
    - Sonrasıda show ile bu formun gösterimi yapılır.
    - Metodlar : 
        - **Show** : Formun gösterilmesi sağlanır. Önceki form hala erişilebilir.
        - **ShowDialog** : Formun gösterilmesi sağlanır. Önceki form erişilemez.
        - **Hide** : Form gizlenir, fakat hafızada saklanmaya devam eder.
        - **Visible** : True veya False yapılarak gizleme ve gösterme işlemleri yapılabilir.
        - **Close** : Formun kapatılıp hafızadan silinmesi sağlanır.
            - Ana form için close işlemi yapılırsa, program tamamen kapanır!
    - **Show** metodu kullanıldığında, form kapatıldığı zaman dispose işlemi yapılır. Fakat **ShowDialog** metodu kullanıldığında bu dispose işlemi yapılmaz. Form, dispose edilene kadar arka planda çalışmaya devam eder. Bu nedenle ShowDialog kullanıldığı zaman dispose işlemi de yapılmalıdır.

```cs
// Form 1 - Ana Form
private void btn_formAc_Click(object sender, EventArgs e)
{
    this.Visible = false;
    Form2 frm2 = new Form2();
    frm2.form1 = this;
    frm2.ShowDialog();
    frm2.Dispose();
}

// 2. Form
public Form1 form1;

private void button1_Click(object sender, EventArgs e)
{
    this.Close();
    form1.label1.Text = "Form kapatıldı.";
    form1.Visible = true;
}
```

- Formlar arasında kontrol kullanımı :
    - Kontrol elemanının Modifiers özelliğinin public yapılması gereklidir.
    - Sonrasında form elemanı tanıtıldıktan sonra, bu nesne üzerinden public elemanlara ulaşılıp üzerinde işlemler yapılabilir.
- Başlangıç formunu değiştirmek için Program.cs içinde değişiklik yapılabilir.

### 04 – Menüler
- MenuStrip Ekleme
    - Üst kısımda ana menü eklemek için kullanılır.
    - Tek çizgi ile ( - ) ayıraç eklenebilir.
- ContextMenuStrip
    - Sağ tık için açılır menü
    - Hangi alana sağ tıklayınca gelmesini istiyorsak, orayı seçip, properties kısmında ContextMenuStrip özelliğinden, ilgili CMS’i seçmemiz gerekiyor.
- StatusStrip
    - En alt kısma bilgilendirme için bir bar ekler.
- ToolStrip
    - Ana menü dışındaki alt araç çubuğu vb kısımların eklendiği yer.
- ToolStripContainer
    - Eklenen ToolStrip’lerin pencerenin 4 tarafında hareket etmesini sağlar.

### 05 – Timer Kontrolü
- Belli bir zaman aralığı tekrarında, belirtilen kodların çalışmasını sağlar.
- Properties kısmından
    - Enabled – True olmalıdır.
    - Internal – Ms türünden zaman belirtilir.
- Timer’ın bir tane event’ı vardır. ( Tick )
    - Bu event içine, belirtilen zaman içinde yapılacak kodlar yazılır.