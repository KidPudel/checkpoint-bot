# Checkpoint bot

## Настройка

### Кратко

1. Подключение к удаленному серверу
2. Установка нужных пакетов
3. Создание проекта
4. Публикование на github

## 1. Подключение к удаленному серверу

- Скачать WireGuard для того, чтобы иметь защищенный тунель между разработчиком и удаленным сервером.\
  [Скачать wireguard](https://www.wireguard.com/install/)
- Получить конфигурацию тунеля, а затем добавить её в тунель\
  Она будет выглядеть примерно так:

```squitconf
[Interface]
PrivateKey =
Address =

[Peer]
PublicKey =
AllowedIPs =
Endpoint =
PersistentKeepalive =
```

- Для начального подключения и проверок использовались терминалы (bash, powershell)\
  Подключение реализуется с помощью ssh команды.

```console
ssh username@hostname
```

- Для дальнейшей работы ислользовался [Visual Studio Code](https://code.visualstudio.com/download), потому что он имеет расширение для подключения и работы на удаленном сервере (Remote - SSH)

## 2. Установка нужных пакетов

Для работы на сервере вам понадобятся следующие пакеты

**Со стороны локальной машины**

- [dotnet](https://dotnet.microsoft.com/en-us/download)
- Расширение для VSCode _Remote - SSH_
- Расширение для VSCode _C#_

**Со стороны сервера**

- wget

```console
sudo apt-get install wget
```

- [подробная инструкция dotNet SDK для Linux](https://docs.microsoft.com/ru-ru/dotnet/core/install/linux-ubuntu)

```console
wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb

sudo dpkg -i packages-microsoft-prod.deb

sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-6.0
```

- Расширение для VSCode _C#_

## 3. Создание проекта

Чтобы создать проект в VSCode нужно открыть терминал

> CTRL + `

далее в открывшимся терминале _bash_ нужно перейти в деректорию где вы хотите сооздать проект:

```bash
cd ~/projects
```

Чтобы создать сам проект введите следующую команду:

```bash
dotnet new console [--name <ИМЯ ВАШЕГО ПРОЕКТА>]
```

После этого вам нужно перейти в деректорию вашего нового проекта и добавить workspad библиотеки для создания workspad бота.
Если у вас уже есть эти покеты на вашей машине, чтобы добавить эти покеты на удаленную среду вам понадобиться WSL linux.\
Далее нужно окрыть WSL и ввести следующую команду:

```bash
scp ./directory_where_is_your_file/filename remote_username@remote_hostname:/destination_directory
```

Тепер, на удаленном сервере в VSCode терминале введите команду:

```bash
dotnet nuget add source <ПУТЬ К ИСТОЧНИКУ> [--name <ИМЯ НОВОГО ИСТОЧНИКА>]
```

Проверете новый источник:

```bash
dotnet nuget list source
```

Теперь добавьте нужные вам покеты:

```bash
dotnet add package <ИМЯ> [-s <ИМЯ ИСТОНИКА>] [-v <Версия>]
```
