# Проблема с отображением пользователя на экране приветствия GDM

Баг репорт: <https://bugzilla.altlinux.org/48825>

Связанные баг репорты:

- <https://bugzilla.altlinux.org/47726>
- <https://bugzilla.altlinux.org/47499>

## Краткое описание

- Установка приложения fwupd поломало отображение списка пользователей на экране входа в Gnome
- Анализ показал:
  - что в списке пользователей в gnome-control-center у пользователя стоит признак выключенной учетной записи;
  - в результате работы утилиты dSpy обнаружили что флаг активности учетной записи берется из последней записи файла /etc/shadow где фигурирует пользователь `fwupd-refresher:!*:`, а знак ! - используется системой как интерпретация блокировки пользователя;
  - проверили гипотезы на предмет удаления этого символа, далее добавления нового айтема в конец списка - и гипотезы подтвердились, именно это и послужило причиной блокировки пользователя в gnome-control-center а так-же исключения нашего пользователя из списка доступных на экране авторизации (входа, логина);

Пока специалисты решают данную проблему, нами предложено обходное решение:

## Обходное решение (workaround)

```shell
su -
# дальнейшие действия вы выполняете под свою ответственность
# в случае ошибки, администрация ресурса ответственность не несет :)
nano /etc/shadow
```

```shell
# добавляем в самый конец еще одну строку

fwupd-refresh:!*:19709::::::  # сразу после fwupd-refresh добавляем свой логин
username:*:20000:::::: # usename меняем на свой логин

# - число может быть +/- любым
# - обязательно ШЕСТЬ штук символов :
# - если это nano, вы можете увидеть сообщение об ошибке (игнорируем / читаем выше про ответственность)
# - когда редактирование закончено, можно нажать Ctrl + X
```

Найденое в сети описание структуры файла:

```text
username:$6$.n.:17736:0:99999:7:::
[------] [----] [---] - [---] ----
    |       |     |   |   |   |||+-----------> 9. Неиспользованный
    |       |     |   |   |   ||+------------> 8. Срок годности
    |       |     |   |   |   |+-------------> 7. Период бездействия
    |       |     |   |   |   +--------------> 6. Период предупреждения
    |       |     |   |   +------------------> 5. Максимальный возраст пароля
    |       |     |   +----------------------> 4. Минимальный возраст пароля
    |       |     +--------------------------> 3. Последнее изменение пароля
    |       +--------------------------------> 2. Зашифрованный пароль
    +----------------------------------------> 1. Имя пользователя
```

### Отклонения / Дополнительный эффект

- Появится возможность использовать функцию автологина (не проверяли, но переключатель доступен)
- Сменить имя пользователя (влияет на отображение на экране логина)

![Видео](/hidden-user-in-userlist-workaround/hidden-user-in-userlist-workaround.mp4)