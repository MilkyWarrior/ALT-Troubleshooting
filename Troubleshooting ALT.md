## #Фикс  Waydroid выдает ошибку OSProber: failed to start AKA Couldn't get lxc status
https://www.altlinux.org/Waydroid
![[Pasted image 20240730110214.png]]
**Фикс:**
1. Открыть конфиг wayland в lxc `/var/lib/waydroid/lxc/waydroid/config`
	1. Закомментить значение `lxc.apparmor.profile = unconfined`

## #Фикс War thunder запускается без EAC
![[Pasted image 20240730121404.png]]
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
![[Pasted image 20240730132805.png]]
2. Перезапустить libvirtd
	1. `sudo systemctl restart libvirtd`

## #Фикс PortProton не запускает приложение по двойному клику
**Фикс:**
1. Пкм, открыть с помощью - portproton
	1. ![[Pasted image 20240730141906.png]]
2. Пкм, свойства - испольняемый как приложение: выкл
	1. ![[Pasted image 20240730141958.png]]

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
3. Закомментить содержимое ![[Pasted image 20240824102911.png]]
4. В этой же папке открыть `yandex.list`
5. Раскомментить строки http ![[Pasted image 20240824103130.png]]
6. Обновить списки пакетов: `epmu` или `apt-get update`

## ==ОБХОД== Tor Browser как выдаст TypeError
![[Pasted image 20240825193345.png]]
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

