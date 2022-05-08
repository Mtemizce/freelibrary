
###Helper.php dosyasına şunu ekleyin:
```php
if (!function_exists('onPageAll')) {
    function onPageAll($url = null, $type = null)
    {
        $onPageResult = '';
        $curl = url()->current();
        switch ($type) {
            case "a":
                $routeUrl = route($url);
                if ($curl == $routeUrl)
                    $onPageResult .= "active";
                else {
                    $onPageResult .= "";
                }
                break;
            case "i":
                $routeUrl = route($url);
                if ($curl == $routeUrl) {
                    $onPageResult .= '<i class="fas fa-angle-double-right right text-success"></i>';
                } else {
                    $onPageResult .= '<i class="fas fa-angle-double-right right "></i>';
                }
                break;
            case "m":
                $parcalanan  = route($url); // Parçalanacak Link
                $parcalama = explode("/", $parcalanan);  // Parçalama İşlemi
                $segmentUrl = Illuminate\Support\Facades\Request::segment(2);
                $mUrlSegment = $parcalama[4];
                if ($segmentUrl === $mUrlSegment)
                    $onPageResult .= "menu-is-opening menu-open";
                else {
                    $onPageResult .= " te";
                }
                break;
            case "ma":
                $parcalanan  = route($url); // Parçalanacak Link
                $parcalama = explode("/", $parcalanan);  // Parçalama İşlemi
                $segmentUrl = Illuminate\Support\Facades\Request::segment(2);
                $mUrlSegment = $parcalama[4];
                if ($segmentUrl === $mUrlSegment)
                    $onPageResult .= "active ".$parcalama[4];
                else {
                    $onPageResult .= "te";
                }
                break;
        }

        return $onPageResult;
    }
}
```

###Sidebar dosyasındaki menü yapınızı aşağıdaki gibi düzenleyin :
```Html
#### Ana Menü açık kalması için "m" 
#### Ana Menü linki active classını alması için "ma" 
#### alt menü active classını alması için "a" 
#### alt menü sağ tarafında aktif/pasif icon çıkması için "i" (html escape yöntemiyle) 

<li class="nav-item  {{ onPageAll('panel.genconf.main', "m") }}"> 
    <a href="#" class="nav-link {{ onPageAll("panel.genconf.main", "ma") }}">
        <i class="nav-icon fas fa-tools"></i>
        <p>Genel Ayarlar <i class="fas fa-angle-left right"></i> </p>
    </a>
    <ul class="nav nav-treeview">
        <li class="nav-item">
            <a href="{{ route('panel.genconf.errorlogs.main') }}" class="nav-link {{ onPageAll('panel.genconf.errorlogs.main', "a") }}">
                <i class="nav-icon fas fa-exclamation-triangle"></i>
                <p>Hata Kayıtları {!! onPageAll('panel.genconf.errorlogs.main', "i") !!}</p>
            </a>
        </li>
    </ul>
</li>
```
