# Работа с ключами репозитория

| Действие                                             | Команда                                                                                               |                                   Комментарий                                    |
| :--------------------------------------------------- | :---------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------: | ------------------------------ |
| Добавление репозитория                               | `add-apt-repository`                                                                                  |                   Сохраняется в файле `/etc/apt/sources.list`                    |
| Удаление репозитория                                 | `add-apt-repository -r`                                                                               | **ИЛИ** удалить стороку с записью о репозитории из файла `/etc/apt/sources.list` |
| Добавление ключа                                     | `wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub                                   |                               sudo apt-key add -`                                | Скачиваем ключ и добавляем его |
| Удаление старых ключей                               | `apt-key list` - выведение списка ключей<br>`apt-key del <последние 8 символов> `                     |                                                                                  |
| Получение текстовых ключей OpenPGP (c ASCII-Armor)   | `wget https://example.com/key/repo_signing.key`<br>`curl -O https://example.com/key/repo_signing.key` |                        Либо через **wget**, либо **curl**                        |
| Преобразование в бинарный вид и помещаем в хранилище | `gpg --dearmor < repo_signing.key > /usr/share/keyrings/repo-archive-keyring.gpg`                     |
| Удаление ключей из хранилища                         | `rm -f /usr/share/keyrings/repo-archive-keyring.gpg`                                                  |                                                                                  |

Синтаксис записи о репозитории:

- В файле `/etc/apt/sources.list`:

## Об apt-key

[Статья про устаревание apt-key и add-apt-repository](https://habr.com/ru/post/683716/)
[Статья про работу с GPG](https://interface31.ru/tech_it/2022/09/apt-key-is-deprecated-ili-upravlenie-klyuchami-v-sovremennyh-vypuskah-debian-i-ubunt.html)

`apt-key` - это утилита, используемая для управления ключами, которые APT использует для аутентификации пакетов. Она тесно связана с утилитой `add-apt-repository`, которая добавляет внешние репозитории с использованием серверов ключей в список надежных источников установки **APT**. Однако ключам, добавленным с помощью `apt-key` и `add-apt-repository`, _apt_ доверяет глобально. Эти ключи не ограничиваются авторизацией единственного хранилища, для которого они были предназначены. Любой ключ, добавленный таким образом, может быть использован для авторизации добавления любого другого внешнего хранилища, что представляет собой важную проблему безопасности.

Начиная с Ubuntu 20.10, при использовании `apt-key` выдаётся предупреждение о том, что инструмент устареет в ближайшем будущем; аналогичным образом, add-apt-repository также скоро устареет. Хотя эти предупреждения об устаревании строго не запрещают использовать `apt-key` и `add-apt-repository` с Ubuntu 22.04, но игнорировать их не рекомендуется.

## GPG ключи

Поэтому при добавлении репозитория нужно делать следующее:

- Для ключей управляемых локально создать директорию `/etc/apt/keyrings` (Debian 12 и Ubuntu 22.04)
- Дать права 755
- Ключ должен быть в двоичной форме (без ASCII-Armor) и иметь имя `repo-archive-keyring.gpg`, где **repo** - короткая часть имени репозитория.
- Также в строке подключения репозитория можно явно указать связанный с ним ключ: `deb [signed-by=/usr/share/keyrings/repo-archive-keyring.gpg] ...`

На практике очень часто требование снять ASCII-Armor не соблюдается и в /usr/share/keyrings кладется текстовая версия ключа. Однако в документации Debian крайне не советуется так делать. Соотвтственно, есть два варианта процесса добавления ключа в хранилище: когда ключ распространяется в текстовом фирмате и, второй, когда он распространяется в бинарном виде.

В первом случае, мы скачиваем текстовый ключ, преобразуем и отправляем в хранилище. Во втором же можем сразу скачать в хранилище. Ниже показаны оба варианта в вариациях с **wget** и **curl**:
|Вид|Команды
|:--:|:--|
| Тестовый ключ |`wget -O- https://example.com/key/repo_signing.key | gpg --dearmor > /usr/share/keyrings/repo-archive-keyring.gpg`<br><br>`curl https://example.com/key/repo_signing.key | gpg --dearmor > /usr/share/keyrings/repo-archive-keyring.gpg`|
| Бинарный ключ |`wget -O /usr/share/keyrings/repo-archive-keyring.gpg https://example.com/key/repo_signing.key`<br><br>`curl -o /usr/share/keyrings/repo-archive-keyring.gpg https://example.com/key/repo_signing.key`|

### Получение GPG с сервера ключей

Метод используется редко, но знать его нужно. Для того, чтобы получить ключ надо знать его ID, точнее два его последних блока: `gpg --keyserver keyserver.ubuntu.com --recv "KEY-ID"`

После выполнения данной операции в домашней директории пользователя будет создано локальное хранилище в скрытой директории `.gnupg/trustdb.gpg`. Теперь нам нужно экспортировать оттуда ключ в хранилище, команда должна выполняться под тем же самым пользователем, который получил ключ в предыдущей команде, если это root: `gpg --export "KEY-ID" > /usr/share/keyrings/repo-archive-keyring.gpg`

- Если нужно получить текстовый ключ: `gpg --export --armor "KEY-ID" > /usr/share/keyrings/repo-archive-keyring.asc`
- Если ключ получал непривилегированный пользователь, то работаем через tee и sudo: `gpg --export "KEY-ID" | sudo tee /usr/share/keyrings/repo-archive-keyring.gpg >/dev/null`
- Можно сразу получить и экспортировать ключ: `gpg --no-default-keyring --keyring /usr/share/keyrings/repo-archive-keyring.gpg --keyserver keyserver.ubuntu.com ` _(ключ **--no-default-keyring** предписывает не использовать локальное хранилище в домашней директории пользователя, оттуда не будет ничего считываться и не будет ничего записано.)_
