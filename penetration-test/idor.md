---
description: Insecure Direct Object Reference
---

# IDOR

Aşağıda yerləşdirilmiş videoda IDOR-lar haqqında Azərbaycan dilində qısa məlumat ala bilərsiniz.

{% embed url="https://www.youtube.com/watch?v=CRQtfrydtws" %}
IDOR-lar haqqında video
{% endembed %}

Digər istifadəçi məlumatlarının birbaşa bizə görünməsi application-da düzgün qurulmuş access control mexanizminin olmamasını göstərir. Əgər bir application-da access control mexanizmləri düzgün qurulmayıbsa orada OWASP siyahısından yaxşı tanıdığımız Broken Access Control tipli boşluqların çıxma ehtimalı çoxdur. Videoda gördüyümüz boşluq da bu kateqoriyaya aiddir. Bu boşluq IDOR adlanır - **Insecure Direct Object Reference**.

Adından göründüyü kimi boşluq nəzərdə tutulmuş məlumata heç bir səlahiyyət yoxlama mexanizmi olmadan birbaşa əlçatımlılığı təmin edir. Bu əlçatımlılıq zərərverici şəxsin bu məlumatları görməsi, dəyişdirməsi və ya silməsini təmin edə bilər.

IDOR boşluğu urldə və requestin body hissəsindəki parametrlərdə və ya sorğularda göndərilən JSON data daxilində ola bilər.

Tapılan IDOR  boşluğunu report edən zaman developerlərə aşağıdakı məsləhətləri verə bilərik:

* İstifadəçidən gələn requestləri cavablandırmazdan öncə onların bunu etməyə səlahiyyətlərinin olub olmamasını yoxlamaq lazımdır. Bunun üçün müxtəlif növ tokenləri istifadə etmək olar.
* Deyək ki biz istifadeci İD-si və ya Tranzaksiya idsi olaraq bir data tipi seçməliyik. Belə olan halda asan təxmin oluna bilən dəyərlər əvəzinə təxmin olunması daha çətin olan guid və ya uuid kimi random dəyərlər təyin etmək nisbətən təhlükəsiz hesab olunur. Məsələn istifadəçi İD-sinin 1001 yox, uuid (8596f1d0-20eb-4666-a4b6-30d20fca62dd) olması daha yaxşı seçim olardı.
* Əlavə olaraq qeyd etmək lazımdır ki ehtiyac olmadığı halda istifadəci ID-lərinin url parametri olaraq göndərilməsi heç də yaxşı üsul deyil. Onu bizim access tokenimiz daxilindən əldə edərək developerlər applicationu daha təhlükəsiz hala gətirə bilərlər. Bu həm də best practice sayılır.





