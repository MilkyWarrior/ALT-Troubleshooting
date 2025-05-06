## #Фикс  Waydroid выдает ошибку OSProber: failed to start AKA Couldn't get lxc status
https://www.altlinux.org/Waydroid
**Фикс:**
1. Открыть конфиг wayland в lxc `/var/lib/waydroid/lxc/waydroid/config`
	1. Закомментить значение `lxc.apparmor.profile = unconfined`

## #Фикс War thunder запускается без EAC
**Фикс:**
1. Создание каталога /etc/ssl/certs/
	1. `sudo mkdir /etc/ssl/`
	2. `sudo mkdir /etc/ssl/certs/`
2. Копирование сертификата из корня игры в созданный каталог
	1. `sudo cp путь-установленной-игры/ca-bundle.crt /etc/ssl/certs/`
3. Правка файла `congif.blk` в папке с игрой
	1. добавить значение `use_eac:b=yes` под `gameplay`

## #Фикс Virt-manager нет прав доступа к другим дискам
**Фикс:**
1. Раскомментить `user` и `group` в `/etc/libvirt/qemu.conf` и приравнять их к имени пользователя
2. Перезапустить libvirtd
	1. `sudo systemctl restart libvirtd`

## #Фикс PortProton не запускает приложение по двойному клику
**Фикс:**
1. Пкм, открыть с помощью - portproton
2. Пкм, свойства - испольняемый как приложение: выкл


## #Фикс  Portproton не использует видеокарту в играх(проблема лишь для одной игры)
**Фикс:**
1. Установка `i586-xorg-dri-radeon`
P.S. Ошибка скорее всего возникает в играх, запускающихся в 32-битном режиме

##  #Фикс Waydroid не вставляет буфер обмена из хоста
**Фикс:**
1. установка `wl-clipboard` `pyclip`
2. авторизация в гугл

## #Фикс  Bluetooth мышка не подключается
**Фикс:** 
1. Подключить к другому устройству и отсоединиться
2. Снова попробовать подключиться

## ==ОБХОД== Civilization 6 не запускается дальше загрузки ERR_ACCES_VIOLATION 0x0
**Обход** 
1. скачать нативную версию цивы

##  ==Обход==  #Фикс resolv.conf сбрасывается после перезагрузки
**Обход:** использовать dnsmasq со своим конфигом
**Фикс:** установить `libnss-resolve`

## #Фикс  База репозиториев откинулась
**Фикс:**
1. Перейти в папку `/etc/apt/sources.list.d`
2. Открыть файл `alt.list`
3. Закомментить содержимое 
4. В этой же папке открыть `yandex.list`
5. Раскомментить строки http
6. Обновить списки пакетов: `epmu` или `apt-get update`

## ==ОБХОД== Tor Browser как выдаст TypeError
**Обход:**
- Использовать бинарник с офиц сайта
##  #Фикс Игры по типу  Arknights, COD не грузятся дальше сплэша лого компаний

**Фикс:**
1. Войти в  `waydroid shell` (CLI command)
2. ввести следующее: `chmod 777 -R /sdcard/Android /data/media/0/Android /sdcard/Android/data /data/media/0/Android/obb /mnt/*/*/*/*/Android/data /mnt/*/*/*/*/Android/obb`

## #Фикс  Megasync не запускается

**Фикс:**
1. Скачать с офиц сайта версию по-новее, в репозиториях альта она устаревшая
2. перепаковать и установить `epmi --repack *файл*`
3. открыть терминал, перейти, используя `cd` в следующую папку: `/home/ilya/.local/share/data/Mega Limited/MEGAsync`
4. с помощью `nano` добавить в `MEGAsync.cfg` пункт `QT_QPA_PLATFORM=xcb`
5. установить модуль `qt5-graphicaleffects`
> Если не удается войти - https://github.com/meganz/MEGAsync/issues/1035

## #Фикс  Davinchi не запускается
**Фикс:** https://github.com/H3rz3n/Davinci-Resolve-Fedora-38-39-40-Fix/blob/main/Davinci-POST-INSTALL-Fix-Fedora-39.sh

## #Фикс  OBS не работают горячие клавиши 
*Частичное решение*: Запустить OBS в Xwayland
```
#!/bin/bash
QT_QPA_PLATFORM=xcb obs
```
 Запустить либо в терминале, либо создать скрипт с текстом выше и добавить его как команду в редакторе меню под ярлыком  obs
 > Данный способ позволяет работать горячим клавишам obs в других приложениях, работающих в xwayland. но не в самом wayland(рабочем столе в том числе)

**Фикс:**
1. Нужно скачать  [`obs-cmd`](https://github.com/grigio/obs-cmd), сделать исполняемым и перенести в `/usr/local/bin`
2. В самом obs studio нужно включить websocket(Сервис $\rightarrow$  Настройки сервера websocket )
3. Далее в настройках gnome перейти во вкладку клавиатура $\rightarrow$ комбинации клавиш $\rightarrow$  дополнительные комбинации клавиш
4. создать свою комбинацию клавиш с командой ```
```
начать запись
obs-cmd -w obsws://айпи сервера websocket:порт/пароль websocket recording start
завершить запись
obs-cmd -w obsws://айпи сервера websocket:порт/пароль websocket recording stop
остановить запись
obs-cmd -w obsws://айпи сервера websocket:порт/пароль websocket recording pause
возообнить запись
obs-cmd -w obsws://айпи сервера websocket:порт/пароль websocket recording resume
```
Другие вариации написаны на домашней странице `obs-cmd`

## #Фикс Фаерволл блочит соединения gsconnect/kdeconnect
**Фикс:**
1. Добавить правила `iptables`: 
```
sudo iptables -A INPUT -p udp --dport 1714:1764 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 1714:1764 -j ACCEPT
```
2. Сохранить изменения
```
sudo iptables-save > /etc/sysconfig/iptables
```
3. Далее в `/etc/net/ifaces/default/options`  (файл) нужно изменить следующие параметры: 
```
CONFIG_FW=yes
FW_TYPE=iptables
```
А в `etc/net/ifaces/default/fw/options`:
```
IPTABLES_HUMAN_SYNTAX=yes
```
4. Выполнить команды: 
```
efw default filter INPUT rule accept tcp from any to 192.168.1.100 dport 1714:1764  
efw default filter INPUT rule accept udp from any to 192.168.1.100 dport 1714:1764
```
5. Перезапустить брэндмауер 
```
sudo efw default restart
```
 6.  Если необходимо, можно дополнительно еще перезагрузить пк
