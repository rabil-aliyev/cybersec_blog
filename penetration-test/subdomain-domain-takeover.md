---
description: DNS rekordları unudulanda ..
---

# Subdomain/Domain Takeover

Deyək ki, böyük bir şirkətimiz var, bu şirkətin isə öz həcminə ekvivalent çox sayda domain və subdomainləri var. Təbii ki domain və subdomainlərin çalışması üçün onlara aid DNS rekordları olmalıdır. Lazım olduqca [DNS](https://book.cybersec.az/terminalogiya#dns-domain-name-server) rekordlarımızı yaradıb subdomainlərimizi harasa yönəldirik, onlar işləməyə başlayır sonra işimiz bitir və biz istifadə etdiyimiz cloud resursumuzu silirik. Bununla bərabər DNS Rekordlarımızı da artıq ehtiyac olmadığı üçün silirik.

**Bəs silməsək ?**

Əvvəlcə baxaq ki bizim domain necə olur ki bizim [dropletə](https://book.cybersec.az/terminalogiya#dns-domain-name-server) və ya hansısa resursumuza aid faylları client-ə göstərə bilir? Ən sadə formada biz domain aldıqdan sonra resurs provayderimizin _nameserver_-lərini yazaraq bu domainin ora yönəldilməsini istəyirik. Resurs provayderimizə aid kontrol panelimizdə isə bu domainin hansısa dropletimizə (resursumuza) yönləndiriləcəyini konfiqurasiya edirik. Son olaraq isə resursumuzun içərisində öz web serverimizi konfiqurasiya etmək qalır.

İndi isə qayıdaq daha əvvələ. Bəs işimiz bitdiyi zaman resursu silib 1-ci addımda qeyd etdiyimiz provayderimizin nameserver-lərini silməsək nə baş verə bilər?

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Əslində domain takeoverlərin texniki izahı çox da mürəkkəb deyil. Bu sadəcə bir domain və ya subdomain üzərində kontrolun digər şəxs tərəfindən ələ keçirilməsidir. Uğurla domain takeover edə bilmiş şəxs həmin domaində istədiyi kontenti yerləşdirə və bunu fərqli məqsədlər üçün istifadə edə bilər. Lakin bu yalnız lap əvvəldə qeyd etdiyim silinməsi unudulan DNS rekordunun mövcud olduğu müddət daxilində keçərli olacaq. Əgər DNS rekordu silinərsə və ya dəyişdirilərsə belə olan halda takeover mümkün olmayacaq. Domain Takeover müxtəlif hallarda baş verə bilər. Misal üçün bir neçə case-ə baxaq:

#### **CASE 1**

Deyək ki bir domainimiz(domain.com) var. Bu domainə aid daha bir subdomainimiz (sub.domain.com) də var ki bu subdomain [CNAME](https://book.cybersec.az/terminalogiya#dns-domain-name-server) rekordu ilə başqa bir domainə (example.com) yönləndirilib. Əgər qeyd etdiyimiz example.com nə vaxtsa expire olarsa və digər bir şəxs o domaini almağa müvəffəq olarsa belə olan halda həmin şəxs sub.domain.com üzərində kontrol əldə etmiş olacaq. Və o subdomain içərisindəki kontenti idarə edə biləcək.

#### CASE 2

Cloud xidmətləri son illərdə populyarlıq qazanır. İstifadəçi yeni Cloud xidməti aldıqdan sonra Cloud provayderi (Amazon, Google, DigitalOcean və s.) əksər hallarda yaradılmış resursa daxil olmaq üçün istifadə olunan unikal domen adı yaradır. Şirkət tərəfindən alınmış Cloud xidmətinin public olması nəzərdə tutulursa (məsələn, e-commerce), şirkət onun öz domenində bir subdomain kimi yerləşdirilməsini istəyə bilər. Məsələn shop.company.com.

Bunun üçün şirkət yaratdığı CNAME DNS rekordu ilə öz subdomainini aldığı cloud servisinə yönəldir və servisdəki resursunu öz istəyinə uyğun quraraq ondan istifadə edir. Bir müddət sonra bu resursa ehtiyac qalmır və şirkət bu resursu deaktiv etməyə qərar verir və silir. Lakin DNS -də hələ də rekordlar qalmaqdadır. Belə olan halda o subdomain üçün gələn requestlər hələ də servis provayderinə yönəldilir.

Bunu identifikasiya edə bilmiş bir şəxs həmin servis provayderində bir resurs alaraq o domain üçün gələn requestlərin öz resursu tərəfindən qəbul olunacağını konfiqurasiya edir. Köhnə DNS rekordu hələ də qaldığı üçün hərşey attackerin istədiyi kimi baş verir və bütün requestlər attacker tərəfindən hazırlanmış resursa gəlir. Bununla da o subdomain üzərində kontrolu əldə etmiş olur.

Buradakı əsas problem bundadır ki, cloud servis provayderləri domainin kimə məxsus olmasını təsdiqləmədən onların konfiqurasiyasına icazə verir.

Bunun qarşısını almaq üçün öz resurslarımızın deaktiv edilməsi ilə bağlı standart prosedurları müəyyənləşdirilməliyik. Belə bir prosedur müəyyənləşdirmək və orada əvvəlcə DNS Rekordlarının silinməsini təmin etmək lazımdır.

#### Domain takeover boşluğunu necə identifikasiya etmək olar ?&#x20;

Bunun üçün çox sayda repolar hazırlanıb. Bu repolarda takeoverin mümkünlüyünü göstərən xüsusiyyətlər və bunu avtomatlaşdırmaq üçün skriptlər var. Aşağıdakı repolardan faydalanaraq bugbounty üçün və ya sifariş əsasında pentestini həyata keçirdiyiniz şirkətdə bu boşluğu axtara bilərsiniz:

* [https://github.com/EdOverflow/can-i-take-over-xyz](https://github.com/EdOverflow/can-i-take-over-xyz)&#x20;
* [https://github.com/punk-security/dnsReaper](https://github.com/punk-security/dnsReaper)
* [https://github.com/haccer/subjack](https://github.com/haccer/subjack)
* [https://github.com/anshumanbh/tko-sub](https://github.com/anshumanbh/tko-subs)
* [https://github.com/ArifulProtik/sub-domain-takeover](https://github.com/ArifulProtik/sub-domain-takeover)
* [https://github.com/SaadAhmedx/Subdomain-Takeover](https://github.com/SaadAhmedx/Subdomain-Takeover)
* [https://github.com/Ice3man543/SubOver](https://github.com/Ice3man543/SubOver)
* [https://github.com/m4ll0k/takeover](https://github.com/m4ll0k/takeover)
* [https://github.com/antichown/subdomain-takeover](https://github.com/antichown/subdomain-takeover)

