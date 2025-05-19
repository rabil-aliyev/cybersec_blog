---
description: Sintaksis və nümunələr
---

# PowerShell Skriptləri

PowerShell scriptlərindən anlayışlı olmaq vacibdir. Ona görə ki, ən çox istifadə olunan əməliyyat sistemi Windows ƏS-dir. Hər birində PowerShell olduğunu nəzərə alsaq, bunu öyrənməyiniz sizi hər birindən rahat istifadə etməyə imkan verir.&#x20;

Powershelldə dəyişənlər **`$`** işarəsi ilə yaradılır və çağırılır. Bu səhifədə bir neçə powershell skripti vasitəsilə mövzunu daha da rahat başa düşülən hala gətirməyə çalışacağam.&#x20;

Bu hissə müxtəlif vaxtlarda yenilənə bilər.

## IF/ELSE istifadəsi

```
$x = 64

if($x -le 30){
   write-host("X 30dan kiçik və ya bərabərdir!")
}else {
   write-host("X 30dan böyükdür.")
}
```

3-cü sətirdə if ifadəsi mötərizənin içini yoxlayıb şərtin doğru olduğu halda 4, olmadığı halda 6 cı sətri icra edəcək. Əgər **`x`** dəyişəni 30-dan kiçik ya da bərabər olarsa onda 4-cü sətir, olmazsa 6-cı sətir icra olunacaq.

**`-le`** ifadəsi "**l**ess than or **e**qual" mənasını verir. Yəni, kiçikdir və ya bərabərdir. 3-cü sətirdə iki dəyəri müqayisə etmək üçün istifadə olunub. Bu və oxşar ifadələri [**Operatorlar**](powershell/operatorlar.md) səhifəsində izah etmişdim.&#x20;

## ForEach dövrləri

Əlimizdə bir fayl var, faylın hər sətrini yoxlayıb, yalnız içərisində success sözü olan sətirlər üçün hansısa əmri icra etmək istəyirik. O halda **`ForEach`**&#x76;ə **`-like`** operatorunu işlədə bilərik.

```
$file = Get-Content -Path ./fayl.txt
foreach ($setir in $file) {
    if($setir -like "*success*"){
        Write-Host $setir
    }
}
```

1-ci sətirdə **`$file`** adlı dəyişəni yaradıb ona faylın məzmununu verdik. 2-ci sətirdə dövrü başladdıq və **`$file`** dəyişəninin hər sətrini **`$setir`** adlandıraraq hər birini tək-tək dövrdən keçirdik. 3-cü sətirdə hazırki dövrdə olan sətrin daxilidə "success" ifadəsinin olub olmadığını wildcard və **`-like`** operatoru vasitəsilə  yoxladıq. Olduğu halda 4-cü sətirdəki **`Write-Host`** vasitəsilə terminala yazdıq.

## &#x20;PingSweeper

{% hint style="info" %}
Bu skript sürətli olmadığı üçün çox da işimizə yaramır. Düzgün çalışır amma sürətli deyil. Ona görə də real tapşırıqlar zamanı bunu işlətməyəcəyik.
{% endhint %}

Olduğumuz şəbəkədə bizdən başqa olan Hostları tapmaq üçün belə bir skript istifadə oluna bilər. Tutaq ki biz hansısa bir serverə düşmüşük və indi ordan şəbəkədəki digər komputerləri və serverləri axtarmaq istəyirik. Belə olan halda yuxarıdakı kimi bir skript bizim üçün 255 ip addresə ping ataraq onların var olub olmadıqlarını bizə deyəcək.&#x20;

{% hint style="info" %}
Bəzən komputer və serverlər elə ayarlana bilər ki ping-ə (icmp) cavab verməsin. Yəni əgər bir komputerə ping atdınız və oradan cavab gəlmədisə, bu 100% demək deyil ki, host yoxdur. Bəlkə də var amma ping bağlıdır və ya şəbəkə elə ayarlanıb ki olduğunuz komputerdən o hostla əlaqə qurmağa səlahiyyətiniz yoxdur. Bu da nəzərə alınmalıdır.
{% endhint %}

```
$range = 0..255
foreach($sonluq in $range) {
    $IP = "192.168.1.$sonluq"
    if(Test-Connection -ComputerName $IP -count 1 -Quiet)
    {
        Write-Host "Host tapıldı: $IP" -ForegroundColor Green
    } else {
        Write-Host "Host tapılmadı: $IP" -ForegroundColor Red
    }
}
```

• 1-ci sətirdə biz 0-dan 255-ə qədər ədədlərin olduğu bir çoxluq (array) yaratdıq. \
• 2-ci sətirdə foreach operatoru vasitsilə bu çoxluğun elementlərinin hər birini **`$sonluq`** olaraq adlandırıb dövr yaratdıq. \
• 3-cü sətirdə **`$IP`** adlı dəyişən yaradıb dəyərinin əvvəlini sabit saxladıq, çünki bizimlə eyni şəbəkədə olan komputerlərin IP ünvanının ilk 3 hissəsi bizimki ilə eynidir. Yalnız sonuncu hissəsini hər dövrdə dəyişə bilmək üçün ip adresin son hissəsini **`$sonluq`** dəyişəni ilə tamamladıq. \
• 4-cü sətirdə **`Test-Connection`** cmdleti vasitəsilə 3-cü sətirdə yaradılan IP ünvanına test bağlantısı edərək pingə cavab verilib verilmədiyini yoxlayırıq. Əgər cavab versə **True**, verməzsə **False** dəyərini alacaq.\
• 6-cı sətir if operatorunun şərtinin True olduğu halda icra olunacaq. Terminalda yaşıl rəngdə "Host tapıldı" yazaraq IP adresi göstərəcək.\
• 8-ci sətir if operatorunun şərtinin False olduğu halda icra olunacaq. Terminalda qırmızı rəngdə "Host tapılmadı" yazaraq IP adresi göstərəcək.

## Daha geniş məlumatlar üçün:

• [https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1)

• [https://www.tutorialspoint.com/powershell/index.htm](https://www.tutorialspoint.com/powershell/index.htm)

