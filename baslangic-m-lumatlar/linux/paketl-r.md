---
description: Həmçinin yeni programların yüklənməsi
---

# Paketlər

Linuxu Windows dan ayıran digər bir amil də yeni proqramların yüklənmə qaydasıdır. Windows-da hansısa programı yükləmək üçün internetdə dolaşmalı və sonra o programı yükləyə biləcəyiniz bir mənbə tapmalı, təhlükəsiz olduğundan əmin olduqdan sonra onu yükləyib qurmalısınız. Windowsda komputerinizə zərərli və ya aldadıcı proqramların yüklənməsi çox tez-tez ola bilər, əgər yeni istifadəçisinizsə bu daha tez-tez qarşılaşa biləcəyiniz problemə çevrilir. Linux-da bu ümumiyyətlə problem deyil. Linux Distroları istədiyiniz programları və paketləri yükləyə biləcəyiniz öz proqram deposuna (**repository** və ya qısaca **repo**) malikdir. Bu depolar hər şeyin pulsuz olduğu bir program mağazası rolunu oynayır.

Linux ƏS-nin müxtəlif distrolarının öz proqram repo-ları var. Məsələn, Debian **apt**, Redhat **rpm**, Arch isə **pacman** istifadə edir. Kali linux da yeni programları sistemə həm **`apt`** (Advanced Package Tool) , həm sadəcə internetdən **`.deb`** faylını yükləməklə qurmaq olar.

### APT istifadə etmək

APT sistemə paketləri, digər alət və programları yükləyə biləcəyimiz bir alətdir (toolset). Bu toolset Debian bazalı linux distrolarında istifadə edilir. Kali də bir debian bazalı sistem olduğu üçün biz sistemimizə yeni alətləri qurmaq üçün APT istifadə edə bilərik.

APT-da olan paketlərin siyahısı daimi olaraq bizim sistemin daxilində keşlənərək (cache) saxlanılır. Bununla da biz yeni tool qurmaq istədiyimiz zaman APT öz daxili faylları vasitəsilə bu tool-a aid faylları haradan götürüb sistemimizə quracağına qərar verə bilir (təbii ki əgər belə bir tool varsa). Bu daxili bazanı yeniləmək üçün aşağıdakı əmr istifadə edilir:&#x20;

```
kali@kali:~$ sudo apt update
```

![sudo apt update](https://cdn-images-1.medium.com/max/720/1*vLTZ-uff9Ze-6H-JrDfsWg.png)

APT daxili bazası yeniləndikdən sonra sistemdə olan bütün komponentləri və əməliyyat sisteminin özünü yeniləmək üçün isə aşağıdakı əmr istifadə olunur:

```
kali@kali:~$ sudo apt upgrade
```

Yeni bir program və ya aləti sistemə qurmaq üçün aşağıdakı əmr işlədilir:

```
kali@kali:~$ sudo apt install {programin adi}
```

Mötərizələrin içərisində qurmaq istədiyimiz program və ya alətin adını yazırıq və bizə müəyyən miqdarda yaddaş istifadə edəcəyi ilə bağlı verəcəyi bildirişə **Y** hərfi və enter sıxaraq razılıq veririk. Eynən aşağıda olduğu kimi:

![](https://cdn-images-1.medium.com/max/720/1*dkmQTS73EUuhHLEl4ODWFQ.png)

### DEB fayllarını istifadə etmək

Programı sistemə yükləməyin digər yolu isə onu `.deb` faylı olaraq internetdən yükləyib, terminalda o faylın olduğu qovluğa gedib sonra isə aşağıdakı əmri daxil etməkdir. Tutaq ki biz Nessus adlı programın deb faylını yükləmişik və o hazırda bizim Downloads qovluğumuzdadır. Bu zaman onu qurmaq aşağıdakı kimi olacaq:&#x20;

```
kali@kali:~$ cd Downloads/
kali@kali:~/Downloads$ sudo dpkg -i Nessus_x64.deb
```

![](https://cdn-images-1.medium.com/max/720/1*Cw7al6J425aKQeucLQrsTg.png)

Yüklənmiş programları sistemdən silmək üçün isə aşağıdakı əmr işlədilir:

```
kali@kali:~$ sudo apt remove --purge {program adı}
```

Mötərizələrin içərisində silmək istədiyimiz program və ya alətin adını yazırıq və bizə müəyyən miqdarda yaddaşın boşaldılacağı ilə bağlı verəcəyi bildirişə **Y** hərfi və enter sıxaraq razılıq veririk. Bu da eynən aşağıda olduğu kimi:

![](https://cdn-images-1.medium.com/max/720/1*aYpeOYJmL-RonAcvYP7fqg.png)
