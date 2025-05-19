# İstifadəçilər və Qruplar

### System User  (NT Authority \ System) və Administrator

Sistem əslində bir istifadəçi deyil. Sistem texniki cəhətdən təhlükəsizlik prinsipidir. Administrator isə Windows-da standart bir istifadəçidir, yəni default olaraq var. Lakin ən yüksək səlahiyyətlərə sahib istifadəçidir. Sistem və Administrator istifadəçisi arasındakı böyük bir fərq odur ki, əgər komputerimiz bir domainə daxildirsə bu halda komputerimizdəki System istifadəçisi Domain istifadəçisi kimi domenə giriş edə bilir, lakin Administrator edə bilmir. Buna görə də sistem daxilində olan Administrator istifadəçisinə **Local Administrator** da deyilir. Çünki səlahiyyətləri yalnız mövcud komputerdə keçərlidir. Həmçinin bir çox fayllara System istifadəçisinin səlahiyyəti çatsa da Administrator səlahiyyəti çatmır. Bunun bir nümunəsi yerli istifadəçilərə aid hesab məlumatlarını əks etdirən SAM faylıdır. System istifadəçisi bu məlumatı əldə edə bilər, lakin Administrator bu məlumatı əldə edə bilməz.&#x20;

### Adi istifadəçi - User

Normal istifadəçinin Administratordan daha az səlahiyyətləri var. Adminstrator sistemdə lazım olan qədər istifadəçi hesabları yarada və onlara da Administrator səlahiyyəti verə bilər. Məsələn  aşağıdakı əmrlə cmd vasitəsilə yeni bir **hacker** adlı və **parol123** parolu olan istifadəçi əlavə edə və sonra onu Administratorlar qrupuna da əlavə edərək yüksək səlahiyyətlər verə bilərsiniz:

```
net user hacker parol123 /add

# Administrator grupuna əlavə etmək
net localgroup administrators hacker /add
```

### Qruplar

Windows əməliyyat sistemlərində istifadəçi qrupu, kompüterə və ya şəbəkə mənbələrinə eyni giriş hüquqları olan və ümumi təhlükəsizlik səlahiyyətləri olan birdən çox istifadəçi toplusudur.&#x20;
