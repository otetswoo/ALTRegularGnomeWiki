# Flatseal

Flatseal — это графическая утилита для просмотра и управления вашими приложениями Flatpak.

## Установка из репозитория 

**Flatseal** можно установить любым привычным и удобным способом:

**Установка через терминал**

::: code-group

```shell[apt-get]
su -
apt-get update
apt-get install flatseal
```
```shell[epm]
epm -i flatseal
```
:::

## Установка c помощью Flatpak

При наличии пакета [Flatpak](/flatpak), можно установить **Flatseal** одной командой:

```shell
flatpak install flathub com.github.tchx84.Flatseal
```

## Настройки

### Поделиться

Список подсистем, совместно используемых c хост-системой 

| Имя                 |     Тип     |                   Описание                   |   `flatpak override` эквивалент   |
|:--------------------|:-----------|:--------------------------------------------|:---------------------------------|
| Сеть | Переключатель | Разрешить приложению доступ к сети. | `--share=network` и `--unshare=network` |
| Межпроцессные коммуникации | Переключатель | Совместно используйте пространство имен IPC с хостом. | `--share=ipc` и `--unshare=ipc`|


### Сокет

Список известных сокотев, доступных в песочнице

| Имя                 |     Тип     |                   Описание                   |   `flatpak override` эквивалент   |
|:--------------------|:-----------|:--------------------------------------------|:---------------------------------|
| Оконная система X11 | Переключатель | Разрешить приложению открываться в оконном интерфейсе X11. | `--socket=x11` и `--nosocket=x11` |
| Оконная система Wayland | Переключатель | Разрешить приложению открываться в оконном интерфейсе Wayland. | `--socket=wayland` и `--nosocket=wayland`|
| Резервный вариант для оконной системы X11 | Переключатель | Разрешить приложению открываться в окне X11, когда Wayland недоступен. Для корректной работы необходимо включить cокет "оконная система X11" | `--socket=fallback-x11` и `--nosocket=fallback-x11` | 
| Звуковой сервер PulseAudio | Переключатель | Разрешите приложению воспроизводить звуки или получать доступ к микрофону при использовании PulseAudio. | `--socket=pulseaudio` и `--nosocket=pulseaudio`|
| Сеансовая шина D-Bus | Переключатель | Разрешить приложению доступ ко всей шине сеанса. | `--socket=session-dbus` и `--nosocket=session-dbus` |
| Системная шина D-Bus | Переключатель | Разрешить приложению доступ ко всей системной шине | `--socket=system-dbus` и `--nosocket=system-dbus` |
| SSH агент | Переключатель | Разрешить приложению использовать проверку подлинности по SSH | `--socket=ssh-auth` и `--nosocket=ssh-auth` |
| Смарт-карты             | Переключатель | Разрешить приложению использовать смарт-карты | `--socket=pcsc` и `--nosocket=pcsc` |
| Система печати          | Переключатель | Разрешить приложению использовать системы печати. | `--socket=cups` и `--nosocket=cups` |
| Каталоги GPG агента     | Переключатель | Разрешить приложению доступ к каталогам GPG-агента | `--socket=gpg-agent` и `--nosocket=gpg-agent` |

## Устройство

Список всех устройств, доступные в песочнице.

| Имя                 |     Тип     |                   Описание                   |   `flatpak override` эквивалент   |
|:--------------------|:-----------|:--------------------------------------------|:---------------------------------|
| Ускорение графического процессора | Переключатель | Разрешить приложению доступ к прямому рендерингу графики, чтобы воспользоваться преимуществами ускорения графического процессора. | `--device=dri` и `--nodevice=dri` |
| Устройства ввода | Переключатель | Разрешить доступ к устройству ввода. | `--device=input` и `--nodevice=input` |
| Виртуализация | Переключатель | Разрешить приложению поддерживать виртуализацию. | `--device=kvm` и `--nodevice=kvm` |
| Общая память | Переключатель | Разрешить приложению доступ к общей памяти. | `--device=kvm` и `--nodevice=kvm` |
| Все устройства | Переключатель | Разрешить приложению доступ ко всем устройствам, таким как веб-камера и внешнии устройства. | `--device=all` и `--nodevice=all` |

## Источники и ссылки

- https://github.com/tchx84/Flatseal/blob/master/DOCUMENTATION.md