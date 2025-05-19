---
description: XSS
---

# Cross Site Scripting

Gündəlik istifadə etdiyimiz saytların kodlarına baxmaq üçün brauzerimizin inspekt funskionallığından istifadə etsək, görərik ki, onların əksəriyyətində istifadəçiyə görünən hissənin yazılması üçün JavaScript istifadə olunub. JavaScript veb-saytlarla bağlı olduqca gözəl işlər görməyə imkan versə də, eyni zamanda yeni və unikal boşluqlara imkan yarada bilir. Onlardan biri isə XSS -dir - Cross Site Scripting&#x20;

## Bu boşluğun səbəbi nədir?&#x20;

Bu hücum zamanı zərərverici məqsədə xidmət edən JavaScript kodları qurbanın brauzerində çalışır. Bir vebsayt istifadəçi tərəfindən daxil olunmuş datanı düzgün olaraq təmizləmədən və ya yoxlamadan istifadə edərsə, həmin saytda XSS boşluğunun olması ehtimalı var. &#x20;

## Bu boşluq vasitəsilə nələr etmək olar?&#x20;

XSS boşluğu [SQL Injection](sql-injection.md) boşluğuna nisbətən daha az təhlükəli hesab olunur. Çünki JavaScriptin istifadəçinin ve serverin əməliyyat sistemi üzərində çox məhdud imkanları var. Lakin buna baxmayaraq XSS bəzi hallarda çox təhlükəli ola bilər. Çünkü sayt kodları üçün əlçatan olan bütün məlumatlar, həmçinin zərərverici JavaScript kodlarına də əlçatan olur. Bunlara istifadəçinin cookie-ləri də aiddir.&#x20;

Zərərverici javascript kodlarının səhifəyə inject olunması nəticəsində istifadəçilərin cookie-ləri oğurlana bilər. Bu kodlar attackerin özünə aid ayrı bir saytda yerləşdirilərək boşluğun olduğu saytdan çağırıla bilər. Boşluğun adında olan Cross-Site ifadəsinin səbəbi də budur. Zərərli JavaScript kodlarını inject etmiş attacker həmçinin HTML5 imkanlarını istifadə edərək, istifadəçilərin geolokasiyasını, mikrofonlarını, kameralarını görə və bəzi spesifik fayllarını oxuya bilər. HTML5, bu imkanları istifadəçi razılığından sonra təmin etsə də, sosial mühəndislik yolu ilə istifadəçiləri bunun təhlükəsiz olduğuna inandırmaq olar. XSS həmçinin CSRF hücumlarını həyata keçirmək üçün bir alət olaraq da istifadə oluna bilər.&#x20;

Yuxarıda sadaladığımız imkanlar XSS-in növlərindən asılı olaraq dəyişir. XSS-in ən geniş yayılmış 3 növü var. Bunlar Reflected, Stored və DOM Based adlanır. &#x20;

**Reflected**, XSS -in ən çox rast gəlinən növüdür. Bu növdən olan XSS boşluğunun istifadə olunması üçün attacker öz payloadını serverə göndərilməli olan request içərisinə yerləşdirir. Bunda sonra zərər veməyi planlaşdırdığı insanlara hansısa yol ilə həmin linki çatdırmalı olur. İnsanlar yalnız həmin linki istifadə etdiyi zaman hücum uğurlu ola bilir.&#x20;

**DOM-based XSS**&#x20;

Əgər istifadəçi tərəfindən daxil olunmuş data yoxlanmadan DOM-a yazılmaq üçün istifadə olunarsa belə olan halda saytda DOM-based XSS boşluğu ola bilər. &#x20;

**Stored XSS** isə bundan fərqli olaraq daha təhlükəlidir. Attacker bu boşluğu istifadə edərək sayt kontenti arasında qalıcı olaraq öz zərərverici kodlarını yerləşdirə bilər. Məsələn bu saytdakı hansısa xəbərə yazılmış bir şərh olaraq edilə bilər. Buna görə də StoredXSS həmçinin Persistent XSS olaraq da adlandırılır. Bu daha təhlükəlidir çünki attacker artıq heç kəsi linklərə daxil olmaq üçün inandırmaq məcburiyətində qalmır. Saytın gündəlik istifadəçiləri həmin səhifəni açdıqları zaman zərərli kodlar adi bir şərh olaraq çalışdırılır. Və nəticədə istifadəçilər özləri də hiss etmədən hücumun qurbanına çevrilirlər.&#x20;

Bu boşluğu zərərsizləşdirmək üçün qeyd edəcəyimiz tədbirlər həyata keçirilə bilər:

1. Istifadəçidən gələn dataların yoxlanması və təmizlənməsini həyata keçirmək.&#x20;
2. Escaping və ya Encoding işlətmək. Yəni zərərli olmaq ehtimalı olan simvolları fərqli formata çevirərək istifadə etmək.&#x20;
3. Cookie-lərdə olan HttpOnly flagını istifadə etmək. Çünki HttpOnly flagının aktiv olduğu cookielər JavaScript kodları üçün əlçatan olmur. &#x20;
4. **C**ontent **S**ecurity **P**olicy istifadə etmək. **CSP** vasitəsilə saytın resurslarının haradan çalışdırıla biləcəyinə nəzarəti təmin etmək olar. &#x20;
