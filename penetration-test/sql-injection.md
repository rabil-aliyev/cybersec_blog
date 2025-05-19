---
description: SQL Injection videosunun mətni
---

# SQL Injection

Çoxumuz web saytların öz SQL məlumat bazaları ilə necə əlaqə saxladıqlarını bilirik. Bizim istədiyimiz dataya uyğun olaraq server daxilində SQL sorğusu yaradılıb məlumat bazasına göndərilir sonra isə bazadan gələn məlumat istifadəçiyə göstərilir. Bəs istifadəçilər bu sorğulara müdaxilə edə bilsə necə olar ?

{% embed url="https://youtu.be/uGczFlWrwPo" %}
Video linki
{% endembed %}

SQL məlumat bazalarını idarə etmək üçün bir sorğu dilidir. Məlumatların əlavə edilməsi, silinməsi, dəyişdirilməsi və sair əməliyyatlar üçün bu dil istifadə edilir. Köhnə bir texnologiya olmasına baxmayaraq günümüzdə hələ öz aktuallığını qorumaqdadır. Misal üçün deyək ki, biz saytımızda bir cədvəl yerləşdirmişik. Və bu cədvəl İD-si göndərilmiş istifadəçinin ad, soyad və yaşını bizə göstərir.

Bu cədvəldə grünməli olan datanın məlumat bazasından sorğulanması üçün SQL istifadə edərək aşağıdakı kimi bir query yazmalı olacağıq.&#x20;

`SELECT first_name, last_name, age FROM users WHERE id = 5' OR 1=1;`

Yeni başlamış bir developer olaraq biz bu sorğunu bazaya göndərmək üçün belə bir pseudo kod yazırıq:

```
const id = request.params.id;
query = "SELECT first_name, last_name, age FROM users WHERE id = " + id;
sql_conn.query(query,(error, resuts) => {
	İf(!error){
		response.json({
			results:results
		})
	}
})
```

Bu kod url parametr olaraq göndərilmiş İD dəyərini alıb sql query-nin sonuna əlavə edəcək və bazaya göndərəcək. Sonra isə heç bir xəta olmazsa məlumatları istifadəçiyə cavab olaraq göndərəcək. Test üçün url a daxil olaraq kodumuzun işləyib işləməməsini test edirik və məlumatlar bizə lazım olan formada görünür. Lakin applicationumuzun işləməsi heç də onun düzgün yazıldığı mənasına gəlmir. Əgər biz parametr olaraq 5 əvəzinə ekranda gördüyümüz PAYLOADI istifadə etsək applicationun qəribə davranışının şahidi olardıq, o bazadakı bütün istifadəçi məlumatlarını bizə göndərdi. Bəs buna səbəbi nədir ?

Yazdığımız kodda ID dəyişkəninin heç bir yoxlama aparılmadan sadəcə əsas sorğuya adi bir mətn kimi birləşdirilməsi SQL İnjection boşluğunu yaradır. SQL injection boşluğu application səviyyəsindəki xətalardan yararlanaraq SQL sorğularına müdaxilə edilməsidir. Attacker application xətasını tapdıqdan sonra backend tərəfindən qurulmuş sorğunu öz istəyinə uyğun tamamlayaraq serverə göndərə bilər. Nəticədə bazadakı məlumatların silinməsi, dəyişdirilməsi və ya yenilərinin əlavə edilməsi mümkün ola bilər. Bunlara nail olmaq üçün attackerin SQL dilindən anlayışlı olması vacibdir. SQL İnjection application təyinatından asılı olaraq istifadəçi tərəfindən data qəbul olunan Cookielərimiz, Headerlər, parametrlər və s. hər yerdə ola bilər.

Applicationda istifadə edilmiş sorğuların quruluşundan asılı olaraq SQL injectionun müxtəlif növləri var.&#x20;

Error based yəni xəta əsasında müəyyənləşdirilən sql injection ları identifikasiya etmək çox rahatdır, bizdən tələb olunan sadəcə sql query quruluşunda sintaksis xətası yaratmaqdır. Bunu isə parametrə adi tək və ya cüt dırnaq artırmaqla həll etmək olar. Əgər biz 5 əvəzinə 5' göndərdiyimiz zaman application bu tip sql xəta mesajı göstərərsə, böyük ehtimal ki orada SQL injection boşluğu var. Bundan sonra məqsədimnizə uyğun querylər quraraq app içərisində öz attack vektorumuzu genişləndirə bilərik.

Union based injection zamanı bir neçə SELECT əmri UNİON operatoru vasitəsilə birləşdirilərək məlumat bazasından daha çox məlumatın çıxarılmasını təmin edir. Attacker burada əvvəlcə applicationun öncədən qurduğu sorğuda məlumat bazasından çəkəcəyi sütun sayını öyrənməlidir. Bunu isə öz əlavə etydiyimiz querydə xəta olmayacağımız zamana qədər sütun sayını artıraraq öyrənə bilərik. Düzgün sütun sayı tapıldığı zaman artıq məqsədə uyğun sorğular quraraq məlumatları serverdən çəkə bilərik.

Bəzi sql injection növləri nəticəni attackerlə bölüşmür. Attacker uğurlu sql injection edə bilib bilmədiyini yalnız application cavablarının status kodları, serverin cavab vermə müddəti və başqa applicationa xas göstəricilərə əsasən təyin edə bilir. Bu tip növlər Blind İnjectionlar adlanır.

Onlardan biri Boolean based blind injection-dır. Bu injection tipi bir növ web applicationa cavabı true və ya false ola biləcək sorğular göndərir. Bu sorğulara əsasən uğurlu olub olmamasına qərar verir.

Məsələn biz bir dəfə bu cür payload göndərərək&#x20;

`http://www.example.com/?id=1' OR 10-5=5`

applicationun true dəyərlərə hansı cavabı göndərdiyini gördükdən sonra aşağıdakı kimi bir payload göndərərək database adının uzunluğunu tapmağa çalışa bilərik. Bunun üçün sadəcə sondakı rəqəmi brute-force məntiqi ilə hər -dəfə dəyişmək lazımdır.

`http://www.example.com/?id=1' AND (length(database())) = 8`

Time based injectionlar məlumat bazasının istifadəçiyə cavab vermə müddətinə əsaslanan injection növüdür. Belə ki əgər applicationa bu cür bir sorğu göndərdiyimiz zaman `http://www.example.com/page.php?id=1' waitfor delay '00:00:10'--`&#x20;

o, cavabı 10 saniyə sonra bizə göstərərsə belə olan halda time based sql injection mövcudluğundan danışa bilərik.

SQL İnjection boşluğundan yararlanan attackerin imkanlarını bu cür ümumiləşdirmək olar: 1. Attacker məlumat bazasından informasiyanı götürə,silə və dəyişə bilər. Buraya İstifadəçi hesabları və başqa həssas məlumatlar da daxildir. 2. SQL İnjection vasitəsilə serverə fayl yazmaq və serverdən fayl oxumaq mümkündür. Bu imkandan istifadə edərək zərərverici şəxs serverin əməliyyat sisteminə düşə bilər. Sonradan isə burada səlahiyyətlərini yüksəldərək öz imkanlarını artıra və ya şəbəkənin digər seqmentlərinə qarşı hücumlar edə bilər.

**SQL İnjection attacklarının qarşısı necə alına bilər:**&#x20;

1\. SQL Sorğumuzu yazarkən onu belə yox, bu formada yazmaq daha təhlükəsizdir. Bu cür istifadə etdiyimiz zaman bazada çalışdırılmazdan öncə SQL sorğusunun konstruksiyası qurulur sonra isə ona parametrlər göndərilir. Bu parametrized query adlanır. //animasya.&#x20;

2\. İstifadəçidən gələn bütün datanı təmizləmək və whitelist əlavə etmək. Məsələn videonun əvvəlində danışdığımız İD parametrini bazaya göndərməzdən öncə onun tam ədəd olub olmamasını yoxlamaq. Və varsa əlavə bütün simvollardan təmizləmək.&#x20;

3\. Məlumat bazamızda least privilege prinsipini tətbiq etmək lazımdır. Yəni heç bir istifadəçidə ehtiyac olanından daha artıq səlahiyət olmamalıdır.&#x20;

4\. Əgər yazdığımız dil dəstəkləyirsə onun PDO imkanlarından istifadə etmək daha yaxşı olardı. Çünki PDO funskionallıqlarında bəzi təhlükəsizlik yoxlamaları əvvəlcədən nəzərə alınmış olur.
