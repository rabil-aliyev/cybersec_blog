---
description: Fundamental PowerShell istifadəsi
---

# PowerShell

Windows PowerShell, İT mütəxəssislərinin sistemləri konfiqurasiya etməsinə və adminstrativ tapşırıqları avtomatlaşdırmasına kömək etmək üçün hazırlanmış, interaktiv terminala sahib skript dilidir. Windows 2008 R2 ilə başlayan hər müasir Windows ƏS-də standart olaraq qurulub.&#x20;

PowerShelldən həm terminal kimi əmrləri tək tək yazmaq həm də **ISE** (Integrated Scripting Environment) olaraq öz skriptlərimizi hazırlamaq üçün istifadə edə bilərik. Hər ikisini çalışdırmaq üçün sadəcə start menusunda adlarını axtara bilərsiniz.&#x20;

![PowerShell Terminalı](<../../../.gitbook/assets/image (11).png>)

![PowerShell ISE (Integrated Scripting Environment)](<../../../.gitbook/assets/image (6).png>)

### PowerShell Scriptlərini çalıştırmaq

PowerShell skriptləri `.ps1` fayllarında saxlanılır. Skripti sadəcə üzərinə 2 dəfə klik etməklə çalışdıra bilməzsiniz, sisteminizə bilmədən zərər verməyinizin qarşısını almaq üçün bu cür dizayn edilib. Bir skripti çalışdırmaq üçün əvvəlcə sağ klik etmək və sonra açılan menudan “PowerShell ilə Çalıştır” (Run with PowerShell) düyməsini basmaq lazımdır.

Windowsda bir policy var ki, bu policy sistemdə `.ps1` fayllarının icrasına icazə verilib verilməməsini müəyyənləşdirir. Bu policy **ExecutionPolicy** adlanır. Sistemimizdə hazırda icazə verilib verilməməsini bilmək üçün PowerShell terminal pəncərəsində aşağıdakı əmri çalışdırırıq:

```
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\Rabil> Get-ExecutionPolicy
Restricted
```

Göründüyü kimi **ExecutionPolicy** hazırda **Restricted** dəyərini verir. "Restricted" sözü ingiliscədən tərcümədə "məhdudiyyət qoyulub" mənasını verir. ExecutionPolicy həmçinin aşağıdakı dəyərləri ala bilər:

1. **Restricted** - Heç bir skriptə icazə verilmir. Standart olaraq belə olur.
2. **AllSigned** - Yalnız güvənilən developerlər tərəfindən imzalanan skriptlərinin çalışdırılmasına icazə verilir.
3. **RemoteSigned** - Həm sizin skriptlərinizin, həm də güvənilən developerlər tərəfindən imzalanan skriptlərinin çalışdırılmasına icazə verilir.
4. **Unrestricted** - Bütün növ skriptlərə icazə verilir.

Sistemimizdə `.ps1` skirptlərini çalışdıra bilmək üçün aşağıdakı əmri istifadə edirik və öz skriptlərimiz çalışsın deyə **ExecutionPolicy** dəyərini **RemoteSigned** edirik:

Əmr: `Set-ExecutionPolicy RemoteSigned`

```
PS C:\Users\Rabil> Set-ExecutionPolicy RemoteSigned

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
PS C:\Users\Rabil>
```

Yuxardakı hissəni bir az sağa sürüşdürsəniz görəcəksiniz ki, bizdən bunu təsdiq etməyimizi istəyir, belə olan halda "Y" (yəni **yes**) yazıb enter sıxırıq.&#x20;

Ola bilər ki sizə **Permission Denied** xətası versin, belə olan halda powershell terminaını Administrator adı ilə başladmaq lazımdır.&#x20;

Fikir verdinizsə bir məlumatı görmək istədiyimiz əmr "**Get**" ilə başladı, onu dəyişdirmək üçün istifadə etdiyimiz əmr isə "**Set**"ilə başladı. İndi isə bu qanuna uyğunluq barədə öyrənək.

### Sadə əmrlər

Linuxda olan **ls**, **pwd**, **cd**, **mkdir**, **echo**, **cat**, **ps** və s. burada da eyni məqsədlə çalışır.

### Cmdlet-lər

Cmdlet əvvəlcədən təyin edilmiş funksiyaya malik olan bir PowerShell əmrinə deyilir. Programlaşdırma dillərində olan operatorlar kimi. Cmdletlər haqqında aşağıdakıları bilməlisiniz:

1. Cmdletlərin 3 növü var: System, User və Custom
2. Cmdletlər nəticələri terminala ya array ya da object olaraq qaytarır (Programlaşdırma dillərindən öyrəndiyimiz array və object).
3. Cmdletlər datanı həm terminalda göstərə həmçinin başqa bir Cmdlet-ə ötürə bilər([Linuxda olan piping](https://rabil-aliyev.gitbook.io/ethical-hacking-az-rbaycanca/baslangic-m-lumatlar/linux/giris#mrl-ri-bir-birin-qosmaq-piping-v-yoenl-ndirm-k-redirection) burada da var.)
4. Cmdletləri yazarkən hansı hərfi böyük hansını kiçik yazdığınızın əhəmiyyəti olmur. Yuxarıda olan əmri SeT-ExeCuTionPolicY formasında yazsaq da işləyəcək yenə.
5. Əgər ardıcıl olaraq bir neçə Cmdlet işlətmək istəyiriksə onları `;` işarəsi ilə ayıraraq ardıcıl yazmalıyıq.

### Cmdletlərin formaları

Cmdletlər adətən bir feil və bir ismin birləşməsindən yaranır. Qısaca məntiqi "**Filan şeyi et, filan obyektə et**". Aşağıda bu feillərdən bəzilərini görə bilərsiniz:

• **Get** - Hansısa datanı əldə etmək üçün. Yuxarıda işlətdik.\
• **Set** - Hansısa parametrin dəyərini dəyişmək üçün. Yuxarıda işlətdik.\
• **Start** - Nəyisə çalışdırmaq üçün\
• **Stop** - Çalışan nəyisə dayandırmaq üçün.\
• **Out** - Hansısa datanı terminala output edilməsini təmin etmək.\
• **New** - Yeni bir şey yaratmaq üçün. (Bu feil deyil, lakin Cmdletlər belə də başlaya bilir.)

Test etmək üçün gəlin sistemimizdəki servisləri görək:

```
PS C:\Users\Rabil> Get-Service                                                                                     
Status   Name               DisplayName
------   ----               -----------
Stopped  AarSvc_14bce3c2    Agent Activation Runtime_14bce3c2
Stopped  ABBYY.Licensing... ABBYY FineReader 12 PE Licensing Se...
Stopped  AdobeUpdateService AdobeUpdateService
Running  AdvancedSystemC... Advanced SystemCare Service 11
Stopped  AGMService         Adobe Genuine Monitor Service
Stopped  AGSService         Adobe Genuine Software Integrity Se...
Stopped  AJRouter           AllJoyn Router Service
Stopped  PeerDistSvc        BranchCache
------------------------------------------------------------------
-------------- ÇOX UZUN OLDUĞU ÜÇÜN KƏSDİM -----------------------
------------------------------------------------------------------
Stopped  workfolderssvc     Work Folders
Stopped  WpcMonSvc          Parental Controls
Stopped  WPDBusEnum         Portable Device Enumerator Service
Running  WpnService         Windows Push Notifications System S...
Running  WpnUserService_... Windows Push Notifications User Ser...
Running  wscsvc             Security Center
Stopped  WsDrvInst          Wondershare Driver Install Service
Running  WSearch            Windows Search
Running  wuauserv           Windows Update

PS C:\Users\Rabil>
```

Yuxarıdakı cmdlet bizə servislərin adını, hazırki vəziyyətlərini və qısa izahlarını gətirdi. Aşağıdakı əmr isə sistemimizdə çalışan prosesləri Bizə göstərir:

```
PS C:\Users\Rabil> Get-Process                                                                                     
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    112       8     2020       1044              2800   0 amdfendrsr
    164      12     2340       1440       0.06   9928   7 amdow
    573      22     5804      87996       5.81   4156   7 AMDRSServ
    419      25    14988      31608       3.11   7472   7 ApplicationFrameHost
    235      16    25472      45896      19.42   6232   7 chrome
    235      15    16004      30288       0.39   6848   7 chrome
   5132      80   257652     272440   3,681.52   7384   7 chrome
    725      38    37496      83300       5.72  17892   7 StartMenuExperienceHost
     87       5      968        380               772   0 svchost
     ---------------------------------------------------------------
    334      19     6880       5328              4380   0 vmware-authd
    265      21     6720      15268       0.11  19932   7 vmware-unity-helper
    229      13     2828       2764              4672   0 vmware-usbarbitrator64
    629      32    72536    2933656   1,522.61  15216   7 vmware-vmx
    577      28    18336      46840      11.44  15596   7 WindowsInternal.ComposableShell.Experiences.TextInput.I...
    170      11     1624       2820               832   0 wininit
    272      12     2608       9284             14980   7 winlogon
    166      10     3788       9432             16344   0 WmiPrvSE


PS C:\Users\Rabil>
```

Hansısa cmdletin necə istifadə edildiyini öyrənmək üçün **`Get-Help`** cmdletini istifadə edə bilərsiniz. Məsələn `Get-Process` cmdleti barədə yardım alaq:

```
PS C:\Users\Rabil> Get-Help Get-Process                                                                            
NAME
    Get-Process

SYNTAX
    Get-Process [[-Name] <string[]>] [-ComputerName <string[]>] [-Module] [-FileVersionInfo]  [<CommonParameters>]

    Get-Process [[-Name] <string[]>] -IncludeUserName  [<CommonParameters>]

    Get-Process -Id <int[]> -IncludeUserName  [<CommonParameters>]

    Get-Process -Id <int[]> [-ComputerName <string[]>] [-Module] [-FileVersionInfo]  [<CommonParameters>]

    Get-Process -InputObject <Process[]> -IncludeUserName  [<CommonParameters>]

    Get-Process -InputObject <Process[]> [-ComputerName <string[]>] [-Module] [-FileVersionInfo]
    [<CommonParameters>]


ALIASES
    gps
    ps


REMARKS
    Get-Help cannot find the Help files for this cmdlet on this computer. It is displaying only partial help.
        -- To download and install Help files for the module that includes this cmdlet, use Update-Help.
        -- To view the Help topic for this cmdlet online, type: "Get-Help Get-Process -Online" or
           go to https://go.microsoft.com/fwlink/?LinkID=113324.



PS C:\Users\Rabil>
```

### Alias-lar

20-ci sətirdə gördüyünüz **ALIASES** hissəsində həmin əmrin qısa adı görünür. Yəni biz `Get-Process` cmdletini sadəcə **ps** və ya **gps** yazaraq icra edə bilərik.

### Parametrlər

Parametrlər icra olunacaq olan cmdlet-in nəyə əsasən icra olunacağını təmin edən dəyərlərdir. Məsələn biz axtarmaq əmri verdiyimiz zaman hansısa açar söz əlavə edirik ki həmin sözü axtarsın. Həmin bu açar söz indiki vəziyyətdə parametr olaraq çıxış edir. İcra olunan program və ya cmdlet öz işini həmin açar sözü tapmaq üçün həyata keçirir. Hər cmdletin özünə uyğun parametrləri var ki cmdletləri daha çox istifadəyə yararlı hala gətirir. Əgər hansısa əmri PowerShell ISE də yazsaq o avtomatik olaraq cmdletin özünə məxsus olan parametrləri təklif edəcək, digər kod editorlarında və ya İDE-lərdə olduğu kimi.

![](<../../../.gitbook/assets/image (4).png>)

Parametr adları cmdletdən sonra əvvəlində tire(-) qoyulmaqla yazılır. Məsələn bizə Servislərdən yalnız `Xbox` servislərini görmək lazımdır. Belə olan halda `Get-Services` əmrini və onun `-Name` parametrini istifadə edəcəyik. Aşağıdakı əmrdə olduğu kimi:

```
PS C:\Users\Rabil> Get-Service -Name Xbox*                                                                            
Status   Name               DisplayName
------   ----               -----------
Stopped  XboxGipSvc         Xbox Accessory Management Service
Stopped  XboxNetApiSvc      Xbox Live Networking Service


PS C:\Users\Rabil>
```

Ulduz işarəsi **wildcard** olaraq çıxış edir. Və adının əvvəlində Xbox ifadəsi olan bütün servisləri gətirir.

{% hint style="info" %}
**Yeri gəlmişkən**

**Wildcard** bir və ya bir neçə simvolu əvəz etmək üçün istifadə olunan simvoldur. Müxtəlif dillərdə müxtəlif simvollarla ifadə edilə bilər( Misal üçün burada ulduz olsa da MySQL-də wildcard olaraq "%" simvolu istifadə olunur). Məsələn biz "Kam\*" ifadəsini axtarış etsək belə olan halda Kamal, Kamil, Kamança və sair kimi "Kam" ilə başlayan nəticələr görünəcək.

Əgər biz "\*can" ifadəsinə görə axtarış etsək nəticələrdə Azərbaycan, Elcan, Fincan və s. nəticələr görəcəyik. Qısaca "can" ilə bitən hər hansı ifadə.

Əgər biz "\*iyya\*" ifadəsi ilə axtarsaq bu zaman Riyaziyyat, Mənəviyyat, Ədəbiyyat və s. kimi əvvəli və sonu necə bitdiyindən aslı olmayaraq ortasında "iyya" ifadəsi olan nəticələr görünəcək.

İndi əsas mövzuya qayıdaq ...
{% endhint %}

Yuxarıda qeyd etdiyimiz **`-Name`** parametri sadəcə bir parametr idi. Onun kimi çox sayda işimizi asanlaşdıracaq parametrlər var. Hansısa bir cmdletin imkanlarından xəbərimiz yoxdursa və mövcud parametrlərini görmək istəyiriksə belə olan halda piping ( `|` ) istifadə edərək `Get-Member` cmdletini istifadə edə bilərik. `Get-Member` cmdleti özündən əvvəl yazılan cmdletin parametrlərini göstərir. Aşağıdakı kimi:

```
PS C:\Users\Rabil> Get-Service | Get-Member                                                                           

   TypeName: System.ServiceProcess.ServiceController

Name                      MemberType    Definition
----                      ----------    ----------
Name                      AliasProperty Name = ServiceName
RequiredServices          AliasProperty RequiredServices = ServicesDependedOn
Disposed                  Event         System.EventHandler Disposed(System.Object, System.EventArgs)
Close                     Method        void Close()
Continue                  Method        void Continue()
CreateObjRef              Method        System.Runtime.Remoting.ObjRef CreateObjRef(type requestedType)
Dispose                   Method        void Dispose(), void IDisposable.Dispose()
Equals                    Method        bool Equals(System.Object obj)
ExecuteCommand            Method        void ExecuteCommand(int command)
GetHashCode               Method        int GetHashCode()
GetLifetimeService        Method        System.Object GetLifetimeService()
GetType                   Method        type GetType()
InitializeLifetimeService Method        System.Object InitializeLifetimeService()
Pause                     Method        void Pause()
Refresh                   Method        void Refresh()
Start                     Method        void Start(), void Start(string[] args)
Stop                      Method        void Stop()
WaitForStatus             Method        void WaitForStatus(System.ServiceProcess.ServiceControllerStatus desiredStat...
CanPauseAndContinue       Property      bool CanPauseAndContinue {get;}
CanShutdown               Property      bool CanShutdown {get;}
CanStop                   Property      bool CanStop {get;}
Container                 Property      System.ComponentModel.IContainer Container {get;}
DependentServices         Property      System.ServiceProcess.ServiceController[] DependentServices {get;}
DisplayName               Property      string DisplayName {get;set;}
MachineName               Property      string MachineName {get;set;}
ServiceHandle             Property      System.Runtime.InteropServices.SafeHandle ServiceHandle {get;}
ServiceName               Property      string ServiceName {get;set;}
ServicesDependedOn        Property      System.ServiceProcess.ServiceController[] ServicesDependedOn {get;}
ServiceType               Property      System.ServiceProcess.ServiceType ServiceType {get;}
Site                      Property      System.ComponentModel.ISite Site {get;set;}
StartType                 Property      System.ServiceProcess.ServiceStartMode StartType {get;}
Status                    Property      System.ServiceProcess.ServiceControllerStatus Status {get;}
ToString                  ScriptMethod  System.Object ToString();


PS C:\Users\Rabil>
```

Gördüyümüz kimi `Get-Service` cmdletinin bütün parametrlərini terminalda göstərdi. Bu parametrlərə əsasən `Get-Service` cmdletinin bizə verəcəyi məlumatları istədiyimizə uyğun formalaşdıra bilirik.&#x20;

### Piping (qoşmaq) ilə daha dəqiq əmrlər

İndi isə piping istifadə edərək əvvəlcə bütün servisləri görüb sonra onların arasından yalnız istifadə olunanları çıxaracağıq. Lakin bu datanı da tam yox, yalnız adlarını göstərəcəyik. Bunu etmək üçün 3 cmdlet-i bir birinə qoşmaq lazımdır:

```
Get-Service | WHERE {$_.status -eq "Running"} | SELECT displayname
```

• `Get-Service` - bütün servisləri çəkmək üçün.

• `WHERE {$_.status -eq "Running"}`  -   WHERE (burada: Harada ki...) ifadəsi bütün datanın arasında yalnız özündən sonrakı hissədə tətbiq edilən filterə uyğun gələn dataları seçir.Programlaşdırma təcrübəsi olanlar üçün qısaca: bir cmdletin return etdiyi data ikinciyə `$_` adı ilə ötürülür.Daha uzun: `$_` - hissəsi hazırki cmdletdən əvvəl gələn cmdlet tərəfindən ötürülmüş datanı bildirir. Yəni ilk cmdletimiz olan `Get-Service` cmdletinin gətirdiyi bütün servislərin siyahısı ikinci cmdletə ötürərkən `$_` olaraq adlandılır ki, lazım olarsa qısa bir adla bütün datanın üzərində əməliyyat aparmaq mümkün olsun. Beləliklə də `$_.status  -eq "Running"` hissəsi bütün data içərisində statusu **Running** ə bərabər olan (`-eq` = equals = bərabərdir) servislərə məxsus bütün datanı gətirir.&#x20;

• `SELECT displayname` hissəsi bizim üçün əmrimizin 1 və 2 ci hissələrindən filterlənmiş bütün data içərisində yalnız displayname-ləri seçir. Yəni istifadəçilərə göstərilən adlarını. Bununla da daha səliqəli data əldə etmiş oluruq.&#x20;

Aşağıdakı kimi:

```
PS C:\Users\Rabil> Get-Service | WHERE {$_.status -eq "Running"} | SELECT displayname

DisplayName
-----------
Advanced SystemCare Service 11
AMD Crash Defender Service
AMD External Events Utility
Application Information
VMware USB Arbitration Service
VMware NAT Service
Windows Biometric Service
------
KƏSDİM
------
Windows Connection Manager
Diagnostic Service Host
WinHTTP Web Proxy Auto-Discovery Service
Windows Management Instrumentation
WLAN AutoConfig
Windows Push Notifications System Service
Windows Push Notifications User Service_14bce3c2
Security Center
Windows Search
Windows Update

PS C:\Users\Rabil>
```

İndi qoşmalarımızın sayını daha çox artıraq və aldığımız nəticəni fayla yazaq. Bunun üçün Out-File cmdleti işlənir və əmrimiz aşağıdakı kimi dəyişir:

`Get-Service | WHERE {$_.status -eq "Running"} | SELECT displayname | Out-File C:\serv.txt`

Aydın olduğu kimi yuxarıdakı 4-cü pipe olunan əmr ona göndərilmiş 1, 2 və 3cü əmrdən keçib gələn datanı C diskində serv.txt adı ilə yaddaşa yazacaq (**Əgər icazəniz varsa, əks halda** "**Access Denied!"**).

### Əksər cmdletlərin Azərbaycan dilində izahı

[Buradan keçid edərək baxa bilərsiniz.](https://rabil-aliyev.gitbook.io/ethical-hacking-az-rbaycanca/baslangic-m-lumatlar/windows/powershell/cmdlet-siyahisi)

### Daha geniş:

[1. https://docs.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.1](https://docs.microsoft.com/en-us/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.1)\
[2. https://www.tutorialspoint.com/powershell/powershell\_operators.htm](https://www.tutorialspoint.com/powershell/powershell_operators.htm)\
[3. https://www.johndcook.com/blog/powershellcookbook/](https://www.johndcook.com/blog/powershellcookbook/)
