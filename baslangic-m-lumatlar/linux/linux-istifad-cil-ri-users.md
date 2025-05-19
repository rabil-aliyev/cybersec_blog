---
description: Linux Users
---

# İstifadəçilər və Qruplar

Linuxda da eynən gündəlik istifadə etdiyiniz Windows komputerlərdə olduğu kimi istifadəçi anlayışı var. Bir sistemdə çox sayda, fərqli privilegiyalara(səlahiyyət - privilege,  icazə - permission) malik olan istifadəçi ola bilər. Linux əməliyyat sistemi istifadəçilər haqqında məlumatı `/etc/passwd` fayldında saxlayır.  `cat` əmri vasitəsilə sistemimizdəki passwd faylının kontentini terminalda görüntüləyək:

```
kali@kali:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
mysql:x:104:110:MySQL Server,,,:/nonexistent:/bin/false
dnsmasq:x:113:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
usbmux:x:114:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
tcpdump:x:115:119::/nonexistent:/usr/sbin/nologin
rtkit:x:116:121:RealtimeKit,,,:/proc:/usr/sbin/nologin
_rpc:x:117:65534::/run/rpcbind:/usr/sbin/nologin
statd:x:119:65534::/var/lib/nfs:/usr/sbin/nologin
postgres:x:120:125:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
sslh:x:123:128::/nonexistent:/usr/sbin/nologin
lightdm:x:132:140:Light Display Manager:/var/lib/lightdm:/bin/false
kali:x:1000:1000:Kali,,,:/home/kali:/bin/bash
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
uuidd:x:138:145::/run/uuidd:/usr/sbin/nologin
```

Yuxarıdakı faylda hər sətir 1 istifadəçi məlumatlarını əks etdirir. İstifadəçinin adı, ID-si, özünə məxsus olan qovluq, qısa şərh və standart terminalı bu sətirdə qeyd olunur. Linux istifadəçiləri haqqında məlumatların olduğu digər bir fayl isə `shadow` faylıdır. Bu fayl da həmçinin `/etc/` qovluğunda yerləşir. `passwd`faylından fərqli olaraq `shadow` faylı bütün istifadəçilərə əlçatan deyil. Bunun səbəbi isə `shadow` faylında istifadəçiləri parollarının şifrələnmiş halda saxlamasıdır. `shadow`faylını ələ keçirmiş bir hacker onu müxtəlif alətlər vasitəsilə sındıra və istifadəçi parollarını götürə bilər.

### Qruplar (Groups)

Qruplar ən sadə şəkildə desək, istifadəçilərin toplusudur. Lakin sual yarana bilər, istifadəçiləri qruplaşdırmaq nəyə lazımdır? Bəzən bir sistemdə çox sayda istifadəçi olur. Məsələn web programçılar, devops işləri ilə məşğul olanlar, sistem adminstratorları və s. Əgər biz birdən çox istifadəçinin hər birinə eyni səlahiyyəti tətbiq etmək istəyiriksə, bu zaman onları bir qrupda birləşdirib, həmin səlahiyyəti istifadəçilərə deyil, qrupa veririk. Beləliklə qrupa verdiyimiz bütün səlahiyyətlər qrup üzvlərinə də aid edilir. Deməli qruplar linux əməliyyat sistemində istifadəçi səlahiyyətlərini toplu şəkildə idarə etmək üçün lazımdır. Linux əməliyyat sistemində qrupları görmək üçün `groups` əmri istifadə edilir. Aşağıdakı kimi:

```
kali@kali:~$ groups
kali cdrom floppy sudo audio dip video plugdev netdev bluetooth scanner
```

