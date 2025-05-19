# Servislər

Servis, istifadəçilərin interaktiv nəzarəti xaricində, arxa planda işləyən bir proqramdır. Bu xidmətlərin bəziləri əməliyyat sisteminin işləməsi üçün çox vacib olsalar da istifadəçilər tərəfindən də servislər çalışdırıla bilər.

Unix və ya Linux kimi sistemlərdə servislər **daemon** kimi də tanınır. Bəzən bu servislərin ya daemonların adı **d** hərfi ilə bitir. Məsələn, sshd - SSH məqsədi ilə işləyən servisin adıdır.

İndi isə Linux-da xidmətlərin siyahısını terminalda görüntüləyək:

```
kali@kali:~$ sudo systemctl list-unit-files --type service --all
```

Aşağı ox və ya maus diyircəyi ilə hərəkət etməklə bütün servisləri görmək mümkündür. Çıxmaq üçün `q` düyməsi və ya `Ctrl + C` basılmalıdır.  Əgər bizə yalnız hazırda çalışan servisləri görüntüləmək lazımdırsa `sudo systemctl | grep running` əmri ilə bütün servislərdən yalnız "running" (çalışan) olanları görüntüləyirik:

```
kali@kali:~$ sudo systemctl | grep running
  proc-sys-fs-binfmt_misc.automount                                                   loaded active running   Arbitrary Executable File Formats File System Automount Point                                                    
  init.scope                                                                          loaded active running   System and Service Manager                                                                                       
  session-2.scope                                                                     loaded active running   Session 2 of user kali                                                                                           
  accounts-daemon.service                                                             loaded active running   Accounts Service                                                                                                 
  cron.service                                                                        loaded active running   Regular background program processing daemon                                                                     
  -------
  #Kəsdim
  -------
  syslog.socket                                                                       loaded active running   Syslog Socket                                                                                                    
  systemd-journald-audit.socket                                                       loaded active running   Journal Audit Socket                                                                                             
  systemd-journald-dev-log.socket                                                     loaded active running   Journal Socket (/dev/log)                                                                                        
  systemd-journald.socket                                                             loaded active running   Journal Socket                                                                                                   
  systemd-udevd-control.socket                                                        loaded active running   udev Control Socket                                                                                              
  systemd-udevd-kernel.socket                                                         loaded active running   udev Kernel Socket
```

Servislərin statusları olur. Bu onların hazırda olan vəziyyətini göstərir.&#x20;

**Enabled** - hazırda çalışan və heç bir problemi olmayan\
**Disabled** - çalışmayan amma lazım olanda problemsiz şəkildə çalışdırıla biləcək\
**Masked** - Disabled-in daha güclü versiyası. Unmask olunmayana qədər çalışa bilməyəcək.\
**Static** - Bu servislər yalnız digər servislərin bu servisə ehtiyac duyduğu zaman işləyəcək.

### Servisləri idarə etmək

```
#Çalışdırmaq
kali@kali:~$ sudo systemctl start [servis_adi]

#Vəziyyətini öyrənmək
kali@kali:~$ sudo systemctl status [servis_adi]

#Aktivləşdirmək
kali@kali:~$ sudo systemctl enable [servis_adi]

#Deaktiv etmək
kali@kali:~$ sudo systemctl disable [servis_adi]

#Yenidən başladmaq
kali@kali:~$ sudo systemctl disable [servis_adi]
```
