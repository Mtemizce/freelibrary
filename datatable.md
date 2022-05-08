### Bu kod bloğu Datatable yüklendikten sonra belirtilen satırda istediğiniz class ı ilgili hücreye (indisini belirttiğiniz) eklemenizi sağlar:

            
```Javascript
"fnRowCallback": function( nRow, aData, iDisplayIndex, iDisplayIndexFull ) {
  $('td:eq(4)', nRow).addClass('text-red');
},

```

#### tabiki datatables fonksiyon tanımlamanızdan hemen sonra yapmalısınız. Örnek:

```Javascript
$('.tableClass').DataTable( {
            "processing": false,
            "serverSide": true,
            "ordering": false,
            "responsive": true,
           "fnRowCallback": function( nRow, aData, iDisplayIndex, iDisplayIndexFull ) {
            $('td:eq(4)', nRow).addClass('text-red');
          },
            
```

***

### Datatable buton, sayfa başına sonuç sayısı, arama, sayfalama gibi özelliklerinin yerlerini değiştirebileceğiniz özellik ise DOM dur. yukarıdaki gibi datatable fonksiyonunu tanımladıktan sonra örnek dom kullanımı şu şekildedir;

 
```Javascript
"dom": '<"div.card-tools"flp><"clear">',
```
