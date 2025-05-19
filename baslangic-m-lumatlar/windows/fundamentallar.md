---
description: Giriş
---

# Fundamentallar

### Windows versiyaları

**Şəxsi istifadə üçün Windows OS**&#x20;

_7 və daha əvvəli üçün artıq dəstək yoxdur._

```
Operating System               Version Number

Windows 1.0                    1.04
Windows 2.0                    2.11
Windows 3.0                    3
Windows NT 3.1                 3.10.528
Windows for Workgroups 3.11    3.11
Windows NT Workstation 3.5     3.5.807
Windows NT Workstation 3.51    3.51.1057
Windows 95                     4.0.950
Windows NT Workstation 4.0     4.0.1381
Windows 98                     4.1.1998
Windows 98 Second Edition      4.1.2222
Windows Me                     4.90.3000
Windows 2000 Professional      5.0.2195
Windows XP                     5.1.2600
Windows Vista                  6.0.6000
Windows 7                      6.1.7600
Windows 8.1                    6.3.9600
Windows 10                     10.0.10240
```

**Serverlər üçün Windows OS**

_Server 2008_ _və daha əvvəli üçün artıq dəstək yoxdur._

```
Windows NT 3.51                  NT 3.51
Windows NT 3.5                   NT 3.50
Windows NT 3.1                   NT 3.10
Windows 2000                     NT 5.0     

    Windows 2000 Server
    Windows 2000 Advanced Server
    Windows 2000 Datacenter Server

Windows NT 4.0                   NT 4.0     

    Windows NT 4.0 Server
    Windows NT 4.0 Server Enterprise
    Windows NT 4.0 Terminal Server Edition

Windows Server 2003              NT 5.2     

    Windows Small Business Server 2003
    Windows Server 2003 Web Edition
    Windows Server 2003 Standard Edition
    Windows Server 2003 Enterprise Edition
    Windows Server 2003 Datacenter Edition
    Windows Storage Server

Windows Server 2003 R2           NT 5.2     

    Windows Small Business Server 2003 R2
    Windows Server 2003 R2 Web Edition
    Windows Server 2003 R2 Standard Edition
    Windows Server 2003 R2 Enterprise Edition
    Windows Server 2003 R2 Datacenter Edition
    Windows Compute Cluster Server 2003 (CCS)
    Windows Storage Server
    Windows Home Server

Windows Server 2008               NT 6.0     

    Windows Server 2008 Standard
    Windows Server 2008 Enterprise
    Windows Server 2008 Datacenter
    Windows Server 2008 for Itanium-based Systems
    Windows Server Foundation 2008
    Windows Essential Business Server 2008
    Windows HPC Server 2008
    Windows Small Business Server 2008
    Windows Storage Server 2008
    Windows Web Server 2008

Windows Server 2008 R2            NT 6.1     

    Windows Server 2008 R2 Foundation
    Windows Server 2008 R2 Standard
    Windows Server 2008 R2 Enterprise
    Windows Server 2008 R2 Datacenter
    Windows Server 2008 R2 for Itanium-based Systems
    Windows Web Server 2008 R2
    Windows Storage Server 2008 R2
    Windows HPC Server 2008 R2
    Windows Small Business Server 2011
    Windows MultiPoint Server 2011
    Windows Home Server 2011
    Windows MultiPoint Server 2010

Windows Server 2012               NT 6.2     

    Windows Server 2012 Foundation
    Windows Server 2012 Essentials
    Windows Server 2012 Standard
    Windows Server 2012 Datacenter
    Windows MultiPoint Server 2012

Windows Server 2012 R2            NT 6.3     

    Windows Server 2012 R2 Foundation
    Windows Server 2012 R2 Essentials
    Windows Server 2012 R2 Standard
    Windows Server 2012 R2 Datacenter

Windows Server 2016     2016       NT 10.0
```

### Windows şəbəkələri <a href="#windows-networks" id="windows-networks"></a>

Müəssisə daxilindəki bütün Windowsları bir biri ilə əlaqələndirməyin 2 üsulu var:

1. Server-Client modeli: Domain Sistemi
2. Peer-to-Peer model: Workgroup

### Windows Domain şəbəkəsi

Windows domenində bütün istifadəçilər bir domen idarəedicisinə (**Domain Controller - DC**) bağlıdır. Beləliklə, iş komputerinizə giriş edərkən domain controller ilə doğrulama (**authentication**, qısaca **auth**) aparılır. Domain Controller təhlükəsizliklə bağlı qayda və ya siyasətləri (**policy**) müəyyənləşdirir: şifrənin uzunluğu nə qədər olmalıdır, nə qədər vaxtdan bir dəyişdirilməlidir, hansı mürəkkəbliyə malik olmalıdır və s. Bir istifadəçi işdən çıxarsa,  domain controllerdən onun hesabı silinər və o işçi artıq müəssisədəki komputerlərə giriş edə bilməz. Domen controlleri idarə edən şəxs (**Domain Admin**) həm də domaində/müəssisədə olan hər şeyə nəzarət edir, bütün komputerlərdə ən yüksək səlahiyyətə malik olur. Bir pentester olaraq, domain admin səlahiyyətləri ilə Domain Controller-ə giriş əldə etmək əlbəttə ki, çox əhəmiyyətlidir. Bu artıq sizin bütün şəbəkəni ələ keçirməyiniz deməkdir.

Komputerinizə daxil olarkən sizi yoxlayan sistem Domain Controller olduğu üçün hesabınıza şəbəkədəki hər hansı bir komputerdən də daxil ola bilərsiniz. Bu ümumiyyətlə domen tipli şəbəkəyə xas xüsusiyyətdir. Bir Domain şəbəkəsi qurmaq üçün Domain Controller kimi ən azı bir Windows Server-ə ehtiyacınız var.

### Policy (Siyasət)

Bu termini windowsdan danışarkən tez-tez görə bilərsiniz. Bir domaində və ya bir komputerdə nələrə icazə verilməsi və nələrə icazə verilməməsi Policy-lərlə tənzimlənir. Məsələn bir Domain Admin müəssisədəki heç kəsin şifrəsinin uzunluğunun 8 simvoldan az olmasını istəmir və ya Control Panelin istifadəçilərdə görünməsini istəmir. Bu tip məqsədlərə nail olmaq üçün Group Policy vasitəsilə sadəcə bir policy yazır. Bu policy domaində olan bütün komputerlərə tətbiq olunur və bütün komputerlər bu siyasət əsasında fəaliyyət göstərirlər.

### Group Policy

Group Policy, Domain Admin-lərin istifadəçilər və komputerlər üçün xüsusi konfiqurasiyaları həyata keçirməsinə imkan verən iyerarxik bir infrastrukturdur. Group Policy ilk növbədə təhlükəsizlik vasitəsidir və təhlükəsizlik siyasətlərini istifadəçilərə və kompüterlərə tətbiq etmək üçün istifadə edilə bilər. Bu siyasətlər kollektiv olaraq Group Policy Objects ( **GPOs** ) adlanır. GPO-ları idarə etmək üçün **Group Policy Management Console** istifadə olunur. Group Policy-lər, [gpresult](https://searchwindowsserver.techtarget.com/definition/gpresult) və gpupdate kimi [t](https://searchwindowsserver.techtarget.com/definition/gpresult)erminal alətləri ilə də idarə edilə bilər .

### Active Directory

Windows 2000-dən bəri Domain Şəbəkəsində istifadəçilərin və konfiqurasiyaların mərkəzi məlumat bazasını saxlamaq üçün **Active Directory** istifadə edilmişdir.

### Domain controller

Hər hansı bir Windows kompüteri bir domen controller olaraq konfiqurasiya edilə bilər. Domain Controller istifadəçi və domen arasındakı qarşılıqlı əlaqənin bütün təhlükəsizlik amillərini idarə edir. Adətən Domain Controller kimi konfiqurasiya edilmiş birdən çox komputer olur. Hər hansı birinin problemi olması halında domain fəaliyyətinin tam dayandırmasın deyə.&#x20;

### SMB (Port: 445,139)

Başı bəlalı Server Message Block (SMB), istifadəçilərin uzaq kompüterlər və serverlərlə ünsiyyət qurmalarını təmin edən bir şəbəkə protokoludur - resurslardan istifadə etmək, faylları paylaşmaq, açmaq və redaktə etməyi təmin edir. Keçdiyi inkişaf dövrü ərzində tez-tez təhlükəsizlik boşluqları (security vulnerability) aşkarlanıb. Bu boşluqlar isə sistemi ələ keçirməyə şərait yaradıb. Ona görə də həm Windows həm Linux (Linuxda **Samba** adlanır) sistemlərdə SMB təhlükəsizliyinə və ən son versiyanın istifadə olunduğuna əmin olmaq lazımdır.

### Kerberos (Port: 88)

Kerberos şəbəkədə bir təsdiqləmə protokoludur. Bu Windows tərəfindən deyil, çox daha əvvəl hazırlanmışdır. Orijinal protokol bir çox unix sistemi tərəfindən istifadə olunur. Windows Kerberos protokolunun öz versiyasını hazırlayıb, beləliklə Windows-a məxsus NT-kernelləri ilə işləyir. Kerberos Domain-də istifadəçiləri doğrulamaq üçün istifadə olunur. \
Əksər hallarda 88-ci portu açıq olan bir komputer Domain Controller kimi qəbul edilə bilər. Bir istifadəçi domenə daxil olduqda Active Directory istifadəçinin kimliyini təsdiqləmək üçün Kerberos istifadə edir. İstifadəçi parolunu daxil etdikdə birtərəfli şifrələnir sonra isə Kerberos ilə Active Directory-ə göndərilir və şifrə bazası ilə müqayisə olunur. Orada olan Key Distribution Center (KDC) istifadəçi komputerinə bir TGI bileti ilə cavab verir.&#x20;

### Workgroup

Workgroup arxitekturası domen sistemindən fərqli çalışır. Belə ki, Workgroup peer-peer ideyasına əsaslanır və domen şəbəkəsində olduğu kimi server-client deyil. Daha kiçik şəbəkələr üçün istifadə olunur. Kompüter workgroup-un bir hissəsidirsə, domenin bir hissəsi ola bilməz. Bir workgroup arxitekturasında hər bir kompüterin öz təhlükəsizlik parametrləri olur. Beləliklə, workgroup üçün bütün təhlükəsizlik parametrlərindən məsul olan tək bir komputer yoxdur. Bu yaxşıdır, çünki tək bir uğursuzluq bütün şəbəkəyə təsir etmir. Bu həmçinin pisdir, çünki istifadəçilərin komputerlərini təhlükəsiz şəkildə quracaqlarına etibar etmək çətindir.&#x20;

### Registry **(Qeydiyyat)**

Windows haqqında danışarkən **registry** sözünü tez-tez eşidə bilərsiniz. Bəs nədir bu registry?

Windows Registry, ƏS və ya onu istifadə edən hər hansı bir tətbiq tərəfindən istifadə edilən aşağı səviyyəli (**low-level**) parametrləri saxlayan iyerarxik struktura malik bir verilənlər bazasıdır. Linux-da **registry** üçün heç bir ekvivalent (qarşılıq) yoxdur. Əksər konfiqurasiyalar Linuxdakı mətn sənədlərində edilir. Adətən `/etc` qovluğunda programlara aid parametr və ya konfiqurasiyaları görmək olar. Qısa olaraq Windows registry-də həm Windows-a aid, həm də, digər programlara aid parametrlər saxlanılır.

Registrydə dəyişiklik etmək üçün Windowsda həm **cmd, powershell** həm də **regedit.exe** istifadə oluna bilər. Yəni həm terminaldan həm də özünə məxsus olan programdan dəyişiklik edə bilərsiniz.&#x20;

### SAM

Təhlükəsizlik Hesabları Meneceri (**S**ecurity **A**ccounts **M**anager), istifadəçi adları və şifrələrini özündə əks etdirən Windows əməliyyat sistemindəki (ƏS) bir verilənlər bazasıdır.

SAM-da hər bir istifadəçi hesabına aid lokal şəbəkə (LAN) parolu və Windows parolu ola bilər. Kimsə komputeri istifadə etmək üçün sistemə daxil olmağa çalışırsa və giriş məlumatarı ilə SAM-dakı hansısa bir hesab uyğun gəlirsə, nəticədə həmin şəxsin sistemə daxil olmasına imkan verilir. İstifadəçi adı və ya parollar SAM-dakı hər hansı bir hesabla uyğun gəlmirsə, məlumatın yenidən daxil edilməsini tələb edən bir səhv mesajı qaytarılır. İstifadəçi kompüter hər dəfə açıldıqda və ya yenidən işə salındıqda identifikasiya məlumatlarını daxil etmək istəmirsə, bu funksiya aradan qaldırıla bilər.

### Driverlər (Sürücülər)

Sürücü(Driver) termini üçün tək bir dəqiq tərif vermək çətindir. Ən əsas mənada sürücü, əməliyyat sistemi və **qurğunun** bir-biri ilə əlaqə qurmasına imkan verən bir proqram komponentidir. Bu cümlədə işlənən qurğu sözü komputerinizin həm daxili hissələrinə həm də xarici komponentlərinə (kamera, klaviatura, mikrofon və s.) aiddir. Məsələn, programın bir qurğudan məlumatları oxuması lazım olduğunu düşünək. Bizim misalımızda bu kamera olsun. Programımız kameradan gələn görüntünü ekranda istifadəçiyə göstərmək istəyir (Skype kimi). Kameranı dizayn edən və istehsal edən eyni şirkət tərəfindən yazılmış sürücü, məlumat əldə etmək üçün kamera ilə necə əlaqə qurmacağını bilir. Sürücü kameradan məlumat aldıqdan sonra məlumatları əməliyyat sisteminə qaytarır. Əməliyyat sistemi isə öz növbəsində gələn məlumatları göstərməsi üçün programa göndərir.

### .BAT

`.bat` fayllarına Linuxda olan bash skriptlərinin Windows qarşılığı da demək olar. Batch skriptlərini hazırlamaq üçün sadəcə Windowsda çalışdırmaq istədiyiniz əmrləri bir faylda alt-alta yazıb sonra isə faylı `.bat` sonluğu ilə yaddaşda saxlamalısınız. Bu skriptlər `cmd` tərəfindən icra edilir.&#x20;

### DLL - Dynamic Link Library

DLL, eyni zamanda birdən çox proqram tərəfindən istifadə edilə bilən kod və məlumatları özündə birləşdirən bir kitabxanadır. Məsələn, Windows əməliyyat sistemlərində Comdlg32 adlı DLL faylı Dialog pəncərələrinin (aşağıdakı şəkildə gördüyünüz tipli pəncərələr) yaradılması ilə əlaqəli funksiyaları yerinə yetirir. Hər bir proqram, dialog pəncərəsi göstərmək üçün bu DLL-dəki funksiyanı istifadə edə bilər. DLL faylları hazırlanmış kodun təkrar istifadəsini və yaddaşın səmərəli istifadəsini təmin etməyə kömək edir.

![](<../../.gitbook/assets/image (7).png>)

**.dll** fayllarından əlavə eyni funksiyanı həyata keçirən başqa fayl tipləri də var. Misal olaraq `.ocx`, `.cpl` və `.drv` fayl tiplərini göstərə bilərik.
