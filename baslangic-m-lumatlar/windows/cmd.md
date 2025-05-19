---
description: Köhnə dost
---

# CMD

Windowsda Powershelldən əlavə həmçinin bənzər funskiyanı yerinə yetirən CMD-da var. CMD sözü ingiliscədə olan **C**o**mm**an**d** sözündən gəlir, "əmr" mənasını verir. Artıq zaman keçdikcə PowerShell ilə əvəzlənməyə doğru getsə də, hələ də çox sayda istifadəçisi var. Aşağıda ən çox istifadə olunan cmd əmrləri yerləşdirilib.

Başlanğıcda qeyd edim ki hansısa əmri görmüsüz, lakin nə iş yaradığını bilmirsinizsə, belə olan halda **help** əmrini istifadə edərək əmrə aid kömək mətnini oxuya bilərsiz. Məsələn: `help taskkill`

### Fayllarla iş

| **Əmr**       | **İzah**                                              |
| ------------- | ----------------------------------------------------- |
| del fayl.txt  | Faylı silir                                           |
| md yeniqovluq | "yeniqovluq" adlı qovluq yaradır                      |
| dir           | Cari qovluğun daxilindəki fayl və qovluqları göstərir |
| dir /A        | Gizli olan fayl və qovluqları da göstərir             |
| type fayl.txt | fayl.txt içindəki mətni terminalda göstərir           |

### Şəbəkə

| **Əmr**     | **İzah**                               |
| ----------- | -------------------------------------- |
| netstat -an | Şəbəkə qoşulmaları və dinlənən portlar |
| ipconfig    | Şəbəkə adapteri və konfiqurasiyası     |
| ping        | Digər hosta ping göndərmək             |
| tracert     | Trace Route -a baxmaq üçün.            |

### Proseslər

| **Əmr**               | **İzah**                                              |
| --------------------- | ----------------------------------------------------- |
| tasklist              | Prosesləri göstərir                                   |
| taskkill /PID 1854 /F | 1854 nömrəli prosesi bitirməyə məcbur edir(F = force) |

### İstifadəçi və Qruplar

| net users                               | Sistemdəki istifadəçiləri göstərir                                 |
| --------------------------------------- | ------------------------------------------------------------------ |
| net user rabil rabil123 /add            | Sistemdə **rabil** adlı və **rabil123** şifrəli istifadəçi yaradır |
| net localgroup Administrator rabil /add | Rabil adlı istifadəçini Administrator qrupuna əlavə edir           |
| net localgroup /domain                  | Komputerin domaində olub olmadığını yoxlamaq                       |
| net users /domain                       | Domaində olan istifadəçilərə baxmaq                                |

### Digərləri

| **Əmr**                                 | **İzah**                                       |
| --------------------------------------- | ---------------------------------------------- |
| shutdown /s /t 0                        | komputeri söndürür, 0-saniyə sonra, yəni indi. |
| shutdown /r /t 0                        | komputeri anında yenidən başladır (restart)    |
| systeminfo                              | sistem məlumatlarını göstərir                  |
| wmic localdisk get deviceid, volumename | Sistemdə qoşulu hard disk hissələrini göstərir |

### SMB paylaşımlarına daxil olmaq

`net use` əmri vasitəsilə digər komputerdə paylaşılmış bir qovluğu öz komputerimizdə aça bilərik. Əmrin sintaksisi aşağıdakı kimidir:

```
net use G: \\Paylaşanın IP adresi\QovluqAdı

#Məsələn
net use G: \\192.168.1.116\Skriptler
```

Bu əmrdən sonra bizim sistemdə G diski yaranacaq, və biz bu diskə daxil olduğumuz zaman **192.168.1.116** adresli komputerin **Skriptlər** qovluğunun daxilini görəcəyik. Bu proses Windowsda **mapping** olaraq adlandılır.

İşimiz bitdikdən sonra əgər G diskini silmək istəyiriksə **`/del`** parametri köməyimizə çatar:

```
net use G: /del
```

[Bu mövzuda daha geniş oxumaq üçün buraya daxil olun.](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/gg651155\(v=ws.11\))
