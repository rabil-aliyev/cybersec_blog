---
description: CronJobs
---

# Zamanlanmış tapşırıqlar

Cron daemon, sisteminizdə prosesləri planlı bir zaman intervalı ilə həyata keçirən daxili bir Linux komponentidir. Cron əvvəlcədən təyin olunmuş əmrlər və skriptlər üçün crontab (cron cədvəlləri) qurur. Müəyyən bir sintaksis istifadə edərək istifadəçilər özlərinə lazım olan skript və ya programları zaman intervalı ilə periodik olaraq çalışdıra bilərlər. Məsələn sizə hər gün saat 5-də /tmp qovluğunu silmək lazımdırsa bunu cronjob-lar vasitəsilə etmək olar.

### CronJob yaratmaq

Cronjob yaratmaq üçün iki üsul var var. Birincisi, aşağıdakı qovluqlara istədiyiniz skriptləri qoymaqla. Adlarından da başa düşmək olar ki yerləşdirəcəyiniz skriptlər hansı zaman intervalında çalışacaq.

```
/etc/cron.daily
/etc/cron.hourly
/etc/cron.weekly
/etc/cron.monthly
```

İkinci üsul isə terminalda yeni cron yaratmaq üçün nəzərdə tutulan `crontab -e` əmri istifadə etməkdir. Bu əmrdən sonra sizin üçün crontab faylı açılır və siz orada crontab-ın öz sintaksisinə uyğun formada istədiyiniz skriptləri və onların çalışma intervalını qeyd edə bilərsiniz.&#x20;

### Sintaksis nümunələri

Hər gün saat 4 də `/opt/restartServer.sh` skriptini çalışdır:

```
0 3 * * * /opt/restartServer.sh
```

Hər ayın 2-ci günü, 16:30-da:

```
30 16 2 * * /opt/restartServer.sh
```

Hər Bazar günü (**sun** - Sunday) saat 04:05-də:

```
5 4 * * sun /opt/restartServer.sh
```
