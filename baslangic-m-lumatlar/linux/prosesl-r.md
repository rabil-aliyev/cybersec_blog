---
description: Sistemdə nə çalışır?
---

# Proseslər

Sistemdə çalışan program və ya prosesləri görmək üçün linuxda **ps** əmri istifadə olunur. Aşağıdakı əmrdə biz bütün prosesləri terminalda görüntüləyəcəyik.

```
kali@kali:~$ ps -aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.2 168128 11508 ?        Ss   11:17   0:03 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    11:17   0:00 [kthreadd]
kali        1224  0.0  0.3 231792 19948 ?        Sl   11:17   0:00 /usr/lib/x86_64-linu
kali        1225  0.0  0.1  45004  6544 ?        Ss   11:17   0:00 /usr/libexec/bluetoo
kali        1228  0.0  0.6 548732 32732 ?        Sl   11:17   0:00 /usr/lib/x86_64-linu
kali        1249  0.0  0.7 416340 41428 ?        Sl   11:17   0:00 /usr/lib/x86_64-linu
root        1252  0.0  0.1 246900  8508 ?        Ssl  11:17   0:00 /usr/libexec/upowerd
kali        1259  0.0  1.2 538380 67652 ?        Sl   11:17   0:01 /usr/bin/python3 /us
root        1262  0.0  0.6 358164 32572 ?        Ssl  11:17   0:03 /usr/libexec/package
kali        1264  0.0  0.0 234000  4708 ?        Sl   11:17   0:00 /usr/libexec/geoclue
                                      ------
                           #UZUN İDİ DEYƏ KƏSDİM ORTASINI
                                      ------
root        2389  0.0  0.0      0     0 ?        I    13:47   0:00 [kworker/0:2-cgroup_
root        2393  0.0  0.0      0     0 ?        I    13:53   0:00 [kworker/1:0-ata_sff
root        2398  0.0  0.0      0     0 ?        I    13:58   0:00 [kworker/1:2-ata_sff
root        2421  0.0  0.0      0     0 ?        I    14:00   0:00 [kworker/u256:1-even
root        2447  0.0  0.0      0     0 ?        I    14:02   0:00 [kworker/0:1-cgroup_
root        2448  0.0  0.0      0     0 ?        I    14:02   0:00 [kworker/1:3]
kali        2454  0.0  0.0   9572  3292 pts/1    R+   14:06   0:00 ps aux
```

İlk sətirdə göründüyü kimi `ps` əmrinə `-aux` parametrini verərək bütün prosesləri görüntülədik. \
**a** - bütün növdən olan proseslər\
**u** - bütün istifadəçilərə aid olan proseslər\
**x** - terminalda çalışmayan (arxa planda çalışanlar) prosesləri də əlavə et.

Əgər biz yalnız **root** adlı istifadəçinin çalışdırdığı prosesləri görmək istəsək bu zaman əmri belə yazmalıyıq:  `ps -auroot` . Yəni **u**-dan sonra gələn hissə istifadəçi adını bildirir.&#x20;

Çalışdırdığınız hər bir əmr və ya program özlüyündə bir və ya birdən artıq proses yaradır. Hər bir prosesin digərlərindən fərqləndirilməsi üçün ona nömrə verilir. Bu nömrələr **PİD** (**P**rocess **Id**entification Number) adlanır. Yuxarıda olan terminal outputunun ikinci sütununda siz bu sözü görə bilərsiniz. Orada gördüyünüz kimi heç bir prosesdə eyni olmamaqla hər prosesin öz nömrəsi var. Məsələn hər-hansı bir prosesi sonlandırmaq istəyiriksə (əvvəlcə buna permission-umuz olmalıdır və ya sudo istifadə edə bilərik) bu halda biz prosesin PİD-ni istifadə edərək `kill` əmrini işlədə bilərik. Məsələn:&#x20;

```
kali@kali:~$ kill 1264
```

Bu əmr əgər heç bir output vermirsə deməli proses uğurla sona çatdırılıb. Əks halda icazənizin olmaması ilə bağlı xəta mesajı görəcəksiniz.

Proseslər siyahısındakı elementlərin bəziləri kvadrat mötərizələrin arasında yazılıb. Bu proseslər hansısa admin tərəfindən deyil adətən sistem tərəfindən başladılan kernel prosesləridir. Kernelin nə olduğuna [buradan](https://rabil-aliyev.gitbook.io/ethical-hacking-az-rbaycanca/baslangic-m-lumatlar/linux/kernel) baxa bilərsiniz.&#x20;
