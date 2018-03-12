## DIALOG PENCERELERİ

### 01 – FolderDialogResult
- Klasör seçimi için kullanılır.
- Tool penceresinden seçilebileceği gibi, kod kısmında da oluşturulabilir. Kod kısmında oluşturulması daha mantıklıdır.
- Dosya seçim penceresi gösterildikten sonra, sonucun alınıp kontrol edilmesi gereklidir.

```cs
FolderBrowserDialog fbd = new FolderBrowserDialog();

fbd.RootFolder = Environment.SpecialFolder.MyComputer;
fbd.SelectedPath = Environment.GetFolderPath(Environment.SpecialFolder.Desktop);
fbd.ShowNewFolderButton = true;

var result = fbd.ShowDialog();
if (result == DialogResult.OK)
{
    MessageBox.Show(fbd.SelectedPath);
}
```

### 02 – OpenFileDialog
- Dosya seçimi için kullanılır.
- Multiple dosya seçimi yapılabilir.
- Dosya ismi :
    - **FileName** -> Tek seçimde kullanılır. **String** döndürür.
    - **FileNames** -> Multiple dosya seçiminde kullanılır. **String []** döndürür.
- OpenFile() fonksiyonu ile dosya açılıp program içinde kullanılabilir.
    - Stream olarak çıktı verir.

```cs
OpenFileDialog ofd = new OpenFileDialog();

ofd.InitialDirectory = Environment.GetFolderPath(Environment.SpecialFolder.Desktop);
ofd.Multiselect = true;
ofd.AddExtension = false;
ofd.Filter = "Resim Dosyaları|*.jpg;*.jpeg|Icon Dosyaları|*.ico|Tüm Dosyalar|*.*";
ofd.Title = "Dosya Seç";

var result = ofd.ShowDialog();
if (result == DialogResult.OK)
{
    foreach (var item in ofd.FileNames)
    {
        MessageBox.Show(item);
    }
}
```

### 03 – SaveFileDialog
- OpenFileDialog ile benzerdir.
- Dosya kaydetmek için bir isim girilmesini ve yol almayı sağlar.
- Multiselect özelliği ve OpenFile() metodu yoktur.

```cs
SaveFileDialog sfd = new SaveFileDialog();

sfd.InitialDirectory = Environment.GetFolderPath(Environment.SpecialFolder.Desktop);
sfd.AddExtension = false;
sfd.Filter = "Resim Dosyaları|*.jpg;*.jpeg|Icon Dosyaları|*.ico|Tüm Dosyalar|*.*";
sfd.Title = "Dosya Kaydet";
sfd.DefaultExt = "ico"; // Filter kullanılmadığında geçerlidir.

var result = sfd.ShowDialog();
if (result == DialogResult.OK)
{
    string fName = sfd.FileName;               // Dosya ismini alma
    MessageBox.Show(fName);
    MessageBox.Show(Path.GetExtension(fName)); // Dosya uzantısını bulma
}
```

### 04 – ColorDialog
- Renk seçimi için kullanılır.
- Seçilen renk değeri direk olarak renk işlemleri için kullanılabilir. 

```cs
ColorDialog cd = new ColorDialog();

var result = cd.ShowDialog();
if (result == DialogResult.OK)
{
    MessageBox.Show(cd.Color.ToString());
}
```

### 05 – FontDialog
- Font seçimi için kullanılır.
- Seçilen font değeri, direk olarak font işlemleri için kullanılabilir. 

```cs
FontDialog fd = new FontDialog();

var result = fd.ShowDialog();
if (result == DialogResult.OK)
{
    MessageBox.Show(fd.ToString());
}
```

### 06 – InputBox
- C# içinde mevcut değildir. Referans olarak eklenmelidir. Eklenecek referans :
    - **Microsoft.VisualBasic**
    - Referans ekleme kısmında, Framework grubu içinde bulunur.
- InputBox ile girilen mesajın uzunluğu en fazla 1024 karakter olabilir.
- Geri dönüş tipi **string** türündedir.

```cs
string mesaj = Interaction.InputBox(
    "Mesaj",                // Görüntülenecek Mesaj
    "Pencere başlığı",      // Pencere Başlığı
    "Varsayılan Mesaj",     // Varsayılan Mesaj
    -1,                     // Pencere x pozisyonu
    -1                      // Pencere y pozisyonu
    );
```

### 07 – MessageBox
- Mesaj penceresi içinde bilgi gösterilmesini sağlar.
- Basılan tuş **DialogResult** olarak alınıp işlenebilir. 

```cs
DialogResult result = MessageBox.Show(
    text            : "Gösterilemesi istenen mesaj",
    caption         : "Pencere başlığı",
    buttons         : MessageBoxButtons.YesNoCancel,
    icon            : MessageBoxIcon.Error,
    defaultButton   : MessageBoxDefaultButton.Button1
    );

if (result == DialogResult.Yes) { } // Tuş kontrolü
```