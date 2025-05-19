---
description: Bash scripting
---

# Bash skript dili

Bash skript dili bizə uzun işləri qısa zamanda həll etməyə imkan verir. Bu script dilinin fayl formatı `.sh` -dır. Aşağıda müxtəlif kod nümunələrini görəcəksiz. O kodları icra etmək üçün onları bir `.sh` faylına yazıb sonra `chmod +x fayladi` etməklə çalışdırma icazəsi veririk. Sonra isə əvvəlinə `./` əlavə edərək çalışdırıb istədiyimiz əmri yerinə yetiririk.

Kodların əvvəlində, ilk sətirdə olan `#!/bin/bash` ifadəsi kodun `/bin/` qovluğundakı `bash` programı vasitəsilə çalışdırılmalı olduğunu bildirir.

Həmçinin kodlar daxilində şərh yazmaq istəsək `#` simvolundan sonra yaza bilərik.

### Fayl kontentini dövrə salmaq

Biz fayldakı hər sözü dövrə salıb içərisindəki hər bir sətir üçün hansısa əmri yerinə yetirmək istəyiriksə aşağıdakı kod bu işdə bizə kömək edə bilər:

```
#!/bin/bash

for setir in $(cat test.txt);do
    echo $setir
done
```

Yuxarıdakı skriptdə biz 3-cü sətirdə **test.txt** faylını oxutdurub onun hər sətrini **setir** olaraq adlandırmasını istədik. 4-cü sətirdə hər bir **setir**-i `echo` əmri ilə ekrana yazdırmasını istədik və son olaraq done ifadəsi ilə dövrün bitməsini göstərdik. Aşağıda skriptin çalışma və işləməsini görürsünüz:

```
kali@kali:~$ chmod +x script.sh 
kali@kali:~$ ./script.sh 
Linux_OS
Facebook
Windows_OS
Mac_OS_X
Google
HTC
Apple
```

Gördüyünüz kimi fayldakı hər sətri terminala çıxardı. İndi isə əmri dəyişək və yalnız içərisində **OS** ifadəsi olan sözləri göstərsin, yəni əməliyyat sistemi olanları. Belə olan halda biz **grep** əmrini istifadə edə bilərik. Yuxarda yazdığımız ilk skriptdə yalnız 4-cü sətirdə aşağıdakı dəyişikliyi etmək lazımdır:

```
#!/bin/bash

for setir in $(cat test.txt);do
    echo $setir | grep OS
done
```

Nəticə:

```
kali@kali:~$ ./script.sh 
Linux_OS
Windows_OS
Mac_OS_X
```

### For dövrləri

Digər programlaşdırma dillərində olduğu kimi burada da for dövrü var. Aşağıdakı skriptlə biz 0-da daxil olmaqlda 10-dan kiçik olan tam ədələri terminala yazdıra bilərik. Bu dövr 10 dəfə həyata keçir və hər dövrdə **eded** adlı dəyişənimiz 1 vahid artır sonra isə terminala yazılır.&#x20;

```
#!/bin/bash

for ((eded = 0; eded < 10; eded++)); do
    echo $eded
done
```

Müəyyən sayda dövr həyata keçirməyin bir digər üsulu da `seq` əmrini işlətməkdir. `seq` əmri python-da gördüyümüz `range()` ifadəsinin bash-dakı oxşarıdır. Bu isə aşağıdakı kimi istifadə oluna bilər:

```
#!/bin/bash
#1 - 100 arasında olan tam ədədləri terminala yazdırmaq

for x in `seq 1 100`; do
    echo $x
done
```

### IF / Else - şərt ifadələri

Aşağıdakı skriptdə 3-cü sətirdə şərt qoyuruq, şərt ödənilərsə 4-cü sətri icra edəcək, ödənilməzsə heç nə etməyəcək. **fi** ifadəsi kodda olan **if bloku**nun bitməsini göstərir.

```
#!/bin/bash

if [ 10 > 3 ]; then
    echo "Shert odenildi!"
fi
```

Şərt ödənilmədiyi halda hansısa əmri icra etmək istəyiriksə bu zaman `else` operatorunu işlədirik:

```
#!/bin/bash

if [ 10 == 3 ]; then
    echo "Shert odenildi!"
else
    echo "Shert odenilmedi!"
fi
```

### Arqumentlər (Commandline Arguments)

Bəzən skriptin dinamik dəyişənlərə əsasən çalışmağını istəyirik. Məsələn hər dəfə daxil etdiyimiz adı istifadə edərək terminalda onu salamlayan bir skript yazmaq üçün skript hər zaman çalışdırılmazdan əvvəl bizdən ad tələb edəcək. Bu halda skriptə arqumentlər göndərmək lazım olur. Argumentlər terminalda script adı yazıldıqdan sonra göndərilir. Məsələn biz grep əmrini istifadə edib hansısa sözü filter etməsi üçün ona arqument göndəririk. `grep OS` - bu kodda olan "OS" ifadəsi bir arqumentdir. Skriptin nəyə əsasən çalışacağını müəyyən edir.&#x20;

Yuxarıda dediyimiz kimi bir skript yazaq. Skript arqument kimi bir ad alsın və onu salamlasın. Arqumentləri kod daxilində çağırmaq üçün PHP dilindən bəri gözlərimizi ağrıdan $ simvolunu istifadə edirik:

```
#!/bin/bash

echo "Xoş gəldin $1 !"
```

Çalışdırmaq:

```
kali@kali:~$ ./script.sh Şuşa
Xoş gəldin Şuşa !
```

Gördüyünüz kimi `$1` ifadəsinin yardımı ilə terminalda skriptə göndərdiyimiz 1-ci arqumenti çağırıb kodda istifadə etdik.
