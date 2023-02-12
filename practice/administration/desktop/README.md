# Установка и настройка Xubuntu

## Установка

### Проблемы

## Настройка

### FSTAB

В моей конфигурации оборудования предполагается, что система установлена на SSD диск, а домашняя папка пользователя - на HDD. Таким образом для того, чтобы я мог пользоваться свои каталогом и для повышения времени жизни SSD, нужно примонтировать некоторые каталоги определённым образом. В этом поможет редактирование файла `/etc/fstab`.

### Установка пакетов

Разделим пакеты на те, что есть в репозиториях дистрибутива, те, которые устанавливаются из своих репозиториев, и те, которые устанавливаются из deb-пакетов.

#### Пакеты из сторонних репозиториев

К таким в первую очередь отнесём Google Chrome, VS Code.

Рассмотрим общий порядок работы с ними.

- загрузить ключ репозитория
- добавить сам репозиторий
- обновить список пакетов

> Команды для работы с репозиториями и ключами [здесь](key-work.md)

##### Google Chrome

Скажу сразу, что при установке этого браузера у меня происходило странное явление, вернее сказать полное отсутствие каких-либо ожидаемых явлений при вызове установленного пакета `google-chrome-stable`.

Первым делом я пыался исправить ситуацию тем, что удалял браузер с корнем: `sudo apt purge google-chrome-stable` и ручным затиранием каталога конфигурации в домашней директории: `rm -rf ~/.config/google-chrome`

### Настройка интерфейса

```shell
sudo apt install ssh
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  ncurses-term openssh-server openssh-sftp-server ssh-import-id
Предлагаемые пакеты:
  molly-guard monkeysphere ssh-askpass
Следующие НОВЫЕ пакеты будут установлены:
  ncurses-term openssh-server openssh-sftp-server ssh ssh-import-id
```

```shell
sudo apt list --upgradable
Вывод списка… Готово
alsa-ucm-conf/kinetic-proposed,kinetic-proposed 1.2.6.3-1ubuntu4.1 all [может быть обновлён с: 1.2.6.3-1ubuntu4]
apt-transport-https/kinetic-proposed,kinetic-proposed 2.5.3ubuntu0.1 all [может быть обновлён с: 2.5.3]
apt-utils/kinetic-proposed 2.5.3ubuntu0.1 amd64 [может быть обновлён с: 2.5.3]
apt/kinetic-proposed 2.5.3ubuntu0.1 amd64 [может быть обновлён с: 2.5.3]
chromium-codecs-ffmpeg-extra/kinetic-proposed 1:85.0.4183.83-0ubuntu2.22.10.1 amd64 [может быть обновлён с: 1:85.0.4183.83-0ubuntu2]
fwupd-signed/kinetic-proposed 1.51~22.10.1+1.2-3ubuntu0.2 amd64 [может быть обновлён с: 1.44+1.2-3]
libapt-pkg6.0/kinetic-proposed 2.5.3ubuntu0.1 amd64 [может быть обновлён с: 2.5.3]
libcanberra-gtk3-0/kinetic-proposed 0.30-10ubuntu1.22.10.1 amd64 [может быть обновлён с: 0.30-10ubuntu1]
libcanberra-gtk3-module/kinetic-proposed 0.30-10ubuntu1.22.10.1 amd64 [может быть обновлён с: 0.30-10ubuntu1]
libcanberra0/kinetic-proposed 0.30-10ubuntu1.22.10.1 amd64 [может быть обновлён с: 0.30-10ubuntu1]
libmbim-glib4/kinetic-proposed 1.28.0-1~ubuntu22.10.1 amd64 [может быть обновлён с: 1.27~git20220823-0ubuntu1]
libmbim-proxy/kinetic-proposed 1.28.0-1~ubuntu22.10.1 amd64 [может быть обновлён с: 1.27~git20220823-0ubuntu1]
libmm-glib0/kinetic-proposed 1.20.0-1~ubuntu22.10.1 amd64 [может быть обновлён с: 1.19~git20220905-0ubuntu2]
libqmi-glib5/kinetic-proposed 1.32.0-1ubuntu0.22.10.1 amd64 [может быть обновлён с: 1.31~git20220823-0ubuntu2]
libqmi-proxy/kinetic-proposed 1.32.0-1ubuntu0.22.10.1 amd64 [может быть обновлён с: 1.31~git20220823-0ubuntu2]
libunwind8/kinetic-proposed 1.6.2-0ubuntu1.1 amd64 [может быть обновлён с: 1.6.2-0ubuntu1]
libvte-2.91-0/kinetic-proposed 0.70.0-1ubuntu1 amd64 [может быть обновлён с: 0.70.0-1]
libvte-2.91-common/kinetic-proposed 0.70.0-1ubuntu1 amd64 [может быть обновлён с: 0.70.0-1]
linux-firmware/kinetic-proposed,kinetic-proposed 20220923.gitf09bebf3-0ubuntu1.4 all [может быть обновлён с: 20220923.gitf09bebf3-0ubuntu1.3]
linux-generic/kinetic-proposed 5.19.0.35.32 amd64 [может быть обновлён с: 5.19.0.31.28]
linux-headers-generic/kinetic-proposed 5.19.0.35.32 amd64 [может быть обновлён с: 5.19.0.31.28]
linux-image-generic/kinetic-proposed 5.19.0.35.32 amd64 [может быть обновлён с: 5.19.0.31.28]
modemmanager/kinetic-proposed 1.20.0-1~ubuntu22.10.1 amd64 [может быть обновлён с: 1.19~git20220905-0ubuntu2]
python3-software-properties/kinetic-proposed,kinetic-proposed 0.99.27.1 all [может быть обновлён с: 0.99.27]
software-properties-common/kinetic-proposed,kinetic-proposed 0.99.27.1 all [может быть обновлён с: 0.99.27]
software-properties-gtk/kinetic-proposed,kinetic-proposed 0.99.27.1 all [может быть обновлён с: 0.99.27]
ubuntu-advantage-tools/kinetic-proposed 27.13.5~22.10.1 amd64 [может быть обновлён с: 27.13.3~22.10.1]
vim-common/kinetic-proposed,kinetic-proposed 2:9.0.0242-1ubuntu1.1 all [может быть обновлён с: 2:9.0.0242-1ubuntu1]
vim-runtime/kinetic-proposed,kinetic-proposed 2:9.0.0242-1ubuntu1.1 all [может быть обновлён с: 2:9.0.0242-1ubuntu1]
vim-tiny/kinetic-proposed 2:9.0.0242-1ubuntu1.1 amd64 [может быть обновлён с: 2:9.0.0242-1ubuntu1]
vim/kinetic-proposed 2:9.0.0242-1ubuntu1.1 amd64 [может быть обновлён с: 2:9.0.0242-1ubuntu1]
xxd/kinetic-proposed 2:9.0.0242-1ubuntu1.1 amd64 [может быть обновлён с: 2:9.0.0242-1ubuntu1]

```
