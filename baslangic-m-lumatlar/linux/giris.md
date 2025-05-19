---
description: Başlanğıc əmrlər
---

# Giriş

Bu yazıda bir neçə populyar Linux əmrləri ilə tanış olacağıq. Biliklərinizi daha çox dərinləşdirmək üçün məqalənin sonundakı xarici mənbələrə üz tuta bilərsiniz.

**Bash** `.sh` skriptlərini dəstəkləyən və mürəkkəb əmrləri icra etməklə bizə istədiyimiz əməliyyatı həyata keçirməyə imkan verən terminal pəncərəsidir.

Terminal pəncərəsini açarkən, öz mühitində dəyişənlərə sahib olan yeni bir Bash prosesi işə salınır. Bu dəyişənlər (Environment variables), terminal sessiyası zamanı işləyən hər hansı bir tətbiqetmənin müxtəlif parametrləri üçün qlobal bir yaddaş formasıdır. Ən çox istinad olunan mühit dəyişkənlərindən biri **PATH**-dir. **PATH** dəyişkəni istifadə olunan program qısayollarının əsl yerini axtarmaqda istifadə olunan qovluqlar çoxluğunu özündə birləşdirir. Mühit dəyişənlərini görüntüləmək üçün `echo` əmri istifadə edilə bilər:

```
kali@kali:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Mühit dəyişənləri bəzən işlərimizi çox asanlaşdıra bilər. Məsələn siz gələcəkdə bir server üçün penetration test həyata keçirən zaman (təbii ki icazəli) onun **İP** ünvanını hər dəfə, hər əmrdə yazmaq əvəzinə yeni bir mühit dəyişəni yaradaraq o İP ünvanını o dəyişənə təyin edə bilərik. Beləliklə hər dəfə o İP ünvanını yazmaq əvəzinə, aşağıdakı misalda olduğu kimi sadəcə `$ip` yaza bilərik:

```
kali@kali:~$ export ip=10.10.10.64
kali@kali:~$ ping -c 1 $ip
```

`export` əmri yeni mühit dəyişəninin yaradılması üçün istifadə olunur. Yaradılmış dəyişənə müraciət etmək üçün dəyişən adının qarşısına `$` işarəsi qoyularaq yazılır. Sistemdə olan mühit dəyişənlərinə `env` əmri ilə baxmaq olar.&#x20;

### Fundamental əmrlər

Linux əməliyyat sistemində əksər əmrlər özünə məxsus istifadə qaydasını əks etdirmək üçün `man` və ya `manual` adlı səhifələr təmin edir. Bu səhifələrə baxmaq üçün linuxda man əmri istifadə edilir. Man səhifələri vasitəsilə hansı linux əmrinin nə işə yaradığını daha asan öyrənə bilərik. Aşağıdakı şəkildə **`whoami`** əmrinə məxsus man səhifəsini görüntülədik.&#x20;

```
kali@kali:~$ man whoami
```

![man whoami](https://cdn-images-1.medium.com/max/720/1*fDPlQDAkbZU1QmO_3yRNlw.png)

Göründüyü kimi `description` hissəsində bu əmrin nə üçün istifadə edildiyi həmçinin müəllif, müəllif hüquqları və başqa detallar haqqında məlumatlar verilib. Bu səhifəni bağlamaq üçün **q** düyməsi sıxılır.

Linuxda hal-hazırda terminalın aktiv olduğu qovluqdakı faylları terminaldan görüntüləmək üçün **`ls`** əmri istifadə olunur. Fərqli qovluğa keçid etmək üçün **`cd`** əmri, olduğun qovluğun hansı olduğuna baxmaq üçün isə **`pwd`** əmri istifadə edilir. **`mkdir`** əmrinin köməyi ilə terminalın aktiv olduğu qovluq daxilində yeni qovluq yaratmaq olar. Bunları ardıcıl olaraq aşağıdakı şəkildə görə bilərsiniz.

![](https://cdn-images-1.medium.com/max/720/1*Is1Z9z-Pk8268dYj0lU0jg.png)

### Faylları axtarmaq

Faylları axtarmaq üçün əsasən **`locate`** və ya **`find`** əmri istifadə edilir. Aşağıda əmrlərdən sonra faylın adını yazmaqla faylları necə axtara biləcəyimizi görə bilərik. **`find`** əmri özündən sonra ad ilə axtarış etmək istənildiyi halda **`-name`** parametr adı tələb etdiyi halda, **`locate`** əmri isə yalnız parametrin özünü tələb edir.&#x20;

![](https://cdn-images-1.medium.com/max/720/1*V7lCP3Ad2W-ICGkCTp2w7A.png)

Əmrlərin sintaksisinin fərqli olduğunu görürük. Minlərlə əmrləri görəcəyimizi hesaba qatarsaq bu qədər əmrin hər birinə aid sintaksis və parametrləri əzbərləmək heç də asan olmadığını görərik. Bunun üçün əksər əmrlərin man səhifəsinə baxmaq və ya əmri yalnız **`-h`** parametri ilə çalışdıraraq (həmişə yox amma 90%) kömək səhifəsinə baxmaq olar. Aşağıda **`locate`** əmrinin kömək səhifəsini görürsünüz.

```
kali@kali:~$ locate -h
```

![](https://cdn-images-1.medium.com/max/720/1*dUk_z5DS0bPmvMiL3IAgig.png)

### **Tarixçə**

Terminalda yazdığınız əmrlər terminalın tarixçəsində saxlanılır. Bu tarixçəni görmək üçün sadəcə terminalda `history` yazmaq kifayətdir.

```
kali@kali:~$ history
1 echo $PATH
2 export ip=10.10.10.64
3 ping -c 1 $ip
```

Yuxarıda mənim terminalda yazdığım son 3 əmri görürsünüz. Hər hansı bir əmri yenidən lazımdırsa, o əmri təkrar təkrar yazmağa ehtiyac yoxdur. Əmrin tarixçədəki indeksini istifadə etməklə bunu etmək olar. Məsələn yuxarıda indeksi 3 olan əmri yenidən icra etmək üçün aşağıdakı kimi yazmaq olar:

```
kali@kali:~$ !3
```

Göründüyü kimi sadəcə terminalda əmr indeksi qarşısına nida yazaraq hər-hansı əmri yenidən icra etmək olar. Terminalda icra olunan son əmri yenidən icra etmək üçün isə sadəcə iki dəfə nida (`!!`) yazmaq kifayətdir.

### **Əmrləri bir birinə qoşmaq (Piping) və yönləndirmək (Redirection)**

Terminalda icra olunan hər bir əmr özünə məxsus olan məlumat axınlarına (data streams) malikdir. Bu məlumat axınları aşağıdakı kimi qruplaşdırılır:

1. Standart Input (STDIN) — Programa istifadəçi və ya sistem tərəfindən verilən məlumatlar. Məsələn aşağıdakı ping əmrində ip ünvanı STDIN hesab olunur: `kali@kali:~$ ping`` `**`10.10.10.64`**
2. Standart Output (STDOUT) — Program icra edildikdən sonra istifadəçiyə göstərdiyi nəticə.
3. Standart Error (STDERR) — Program icra edilərkən yaranan xətalar.

Terminaldakı əmrləri bir birinə qoşmaq üçün **|**- işarəsi (`shift + \`)istifadə edilir. Maraqlıdır bəs nəyə görə əmrləri bir birinə qoşmaq lazımdır?

Bəzən elə hallar yaranır ki, bir əmr nəticəsində yaranan outputun(STDOUT) digər bir əmrdə istifadə olunması lazım gəlir. Məsələn siz sistemdəki çalışan proseslər içərisindən yalnız `python` olanları seçmək istəyirsiniz. Belə olan halda siz `ps aux` əmrini istifadə etməklə sistemdəki prosesləri terminala çıxarıb orada python olanları saya bilərsiniz. Lakin bu işi daha da qısaltmaq və asanlaşdırmaq üçün bizim köməyimizə əmrləri bir birinə qoşmaq (pipng) gəlir.

Əvvəlcə bütün prosesləri görək. Sağ tərəfdəki scroll-bar-dan da gördüyünüz kimi şəkildə göründüyünün daha 3 qatı qədər proses var və bunların arasında python olanları seçmək heç də az vaxt deyil.

![ps aux əmri ilə bütün prosesləri görmək](https://cdn-images-1.medium.com/max/720/1*R6yx-3dCo1rUIM3HwYoWow.png)

İndi isə 2 əmri bir birinə qoşaraq məqsədimizə çataq. Əvvəlcə `ps aux` köməyi ilə bütün prosesləri görüb, sonra isə `grep` əmri ilə yalnız python olanları göstərək. Bunun üçün aşağıdakı kimi əmr qurmaq lazımdır:

```
kali@kali:~$ ps aux | grep python
```

![Əmrləri birləşdirərək yalnız python proseslərini görmək](https://cdn-images-1.medium.com/max/720/1*tfX2oWe1OIby42TvdquoqQ.png)

Yuxarıdakı şəkildən də göründüyü kimi 2 əmri birləşdirərək yalnız özümüzə lazım olan prosesləri görüntüləyə bildik.

### Yönləndirmək (Redirection)

İndi isə **yönləndirmək** (redirection) haqqında danışaq. Tutaq ki, bizə yuxarıdakı kimi içərisində python olan prosesləri tapmaq və onları bir mətn faylına yazmaq lazımdır. Bu halda yönləndirmə istifadə edə bilməsək əmrlərin adını kopyalayıb yeni bir fayl yaradıb həmin faylda manual olaraq yazmalı olacağıq. Yönləndirmə istifadə olunduğu halda bunlara ehtiyac qalmır. Əmrlərin nəticəsini fayla yönləndirmək üçün `>` işarəsi istifadə olunur. Aşağıdakı şəkildə bizə lazım olan proseslərin tapılıb bir fayla yönləndirilməsini və `cat` əmri vasitəsilə oxunmasını görə bilərsiniz:

![Əmrləri birləşdirərək yalnız python proseslərini görmək və çıxan nəticəni fayla yönləndirmək](https://cdn-images-1.medium.com/max/720/1*I1N4xEdyMig6faV5WspFfg.png)

Linuxda yönləndirmək istədiyimiz məlumat axını(data stream) tipini özümüz müəyyənləşdirə bilərik. Məsələn bizə bir əmrin icrasından sonra yaranan yalnız errorları fayla yazmaq lazımdırsa belə olan halda yönləndirmə işarəsindən əvvəl **2** lazımdır. Çünki errorlar üçün olan məlumat axını 2 nömrəli indeksə təyin olunub. Eynən aşağıdakı kimi:

```
kali@kali:~$ ./yoxduBeleProgram 2> xetaMetni.txt
```

![](https://cdn-images-1.medium.com/max/720/1*4muPFzZ47i2VnxEbV0iRfQ.png)

Yuxarıdakı şəkildə mövcud olmayan bir proqramı icra etməyə çalışdıq əgər error yaranarsa fayla yazmasını istədik. Gördüyünüz kimi belə proqramın olmadığı haqqında xətanı faylı oxuyaraq görə bildik.&#x20;

#### &#x20;
