## DATATABLE ve DATAGRID KONTROLÜ
- Datatable genellikle verilerin tutulduğu, DataGrid ise verilerin gösterildiği araç olarak kullanılır.
- DataColumn, DataRow ve DataCell özellikleri
- DataTable içine yeni column ekleme

```cs
DataTable dt = new DataTable();

// 1. Yöntem
dt.Columns.Add("İsim", typeof(string));
dt.Columns.Add("Soyisim", typeof(string));
dt.Columns.Add("Yaş", typeof(int));

// 2. Yöntem
DataColumn clm = new DataColumn("Meslek", typeof(string));
dt.Columns.Add(clm);

dataGridView1.DataSource = dt;
```

- DataTable için yeni Row ekleme

```cs
// 1. Yöntem
dt.Rows.Add("serhat", "sönmez", 21, "Yazılım");

// 2. Yöntem
DataRow dr = dt.NewRow();
dr[0] = "Ahmet";
dr[1] = "Kaya";
dr[2] = 30;
dr[3] = "Müzisyen";
dt.Rows.Add(dr);
```

- DataTable üzerinde değişiklikleri kaydetme ve yapılan değişiklikleri algılama 

```cs
// Verileri onaylama
dt.AcceptChanges();

// Yeni Eklenen, silinen, güncellenen verileri okuma
DataTable dtAdded       = dt.GetChanges(DataRowState.Added);
DataTable dtModified    = dt.GetChanges(DataRowState.Modified);
DataTable dtDeleted     = dt.GetChanges(DataRowState.Deleted);

// Son verileri görüntüleme
foreach (DataRow dr1 in dtAdded.Rows)
    MessageBox.Show(
        dr1[0].ToString());

// Düzenlenmeden önceki verileri görüntüleme
foreach (DataRow dr2 in dtModified.Rows)
    MessageBox.Show(
        dr2[0, DataRowVersion.Original].ToString());
```

- DataGridView üzerinde okuma yapma

```cs
// Bir Hücre Okuma
string cell1 = this.dataGridView1.CurrentCell.Value.ToString();
MessageBox.Show(cell1);

// Tüm Satır Okuma
var satir = this.dataGridView1.CurrentRow;
foreach (DataGridViewCell item in satir.Cells)
{
    MessageBox.Show(item.Value.ToString());
}
```

- DataGridView özellikleri
    - Column üzerine tıklayarak sıralama yapılabilir.
    - Düzenlemeyi açıp kapayabilirsiniz.
    - Cell yerine tüm row seçimi yapabilirsiniz.