[slack-link]: https://fisherman-wharf.herokuapp.com/
[slack-badge]: https://fisherman-wharf.herokuapp.com/badge.svg
[travis-link]: https://travis-ci.org/fisherman/fisherman
[travis-badge]: https://img.shields.io/travis/fisherman/fisherman.svg

[fish shell]: https://github.com/fish-shell/fish-shell
[fisherman]: https://github.com/fisherman.sh
[организации]: https://github.com/fisherman
[онлайн]: http://fisherman.sh/#search

[English]: ../../README.md
[Español]: ../es-ES
[简体中文]: ../zh-CN
[日本語]: ../jp-JA
[Русский]: ../ru-RU
[한국어]: ../ko-KR
[Català]: ../ca-ES

[![Build Status][travis-badge]][travis-link]
[![Slack][slack-badge]][slack-link]

# [fisherman] - fish shell plugin manager

fisherman это параллельный менеджер плагинов для [fish shell].

Прочитать этот документ на другом языке: [English], [Español], [日本語], [简体中文], [한국어], [Català].

## Почему?

* Нет конфигурации

* Нет внешних зависимостей

* Не влияет на время старта оболочки

* Использовать его в интерактивном режиме или _a la_ vundle

* Только самое необходимое: установить, обновить, удалить, список и помощь

## Установка

C curl.

```sh
curl -Lo ~/.config/fish/functions/fisher.fish --create-dirs git.io/fisherman
```

C npm.

```sh
npm i -g fisherman
```

## Использование

Установите плагин.

```
fisher simple
```

Установка из нескольких источников.

```
fisher z fzf omf/{grc,thefuck}
```

Установить из URL.

```
fisher https://github.com/edc/bass
```

Установить из gist.

```
fisher https://gist.github.com/username/1f40e1c6e0551b2666b2
```

Установить из локального каталога.

```sh
fisher ~/my_aliases
```

Использовать в интерактивном-режиме. Редактировать fishfile и запустить `fisher`, чтобы удовлетворить изменения.

> [Что такое fishfile и как я могу его использовать?](#6-Что-такое-fishfile-и-как-я-могу-его-использовать)

```sh
$EDITOR fishfile # добавить плагины
fisher
```

Посмотреть, что установлено.

```
fisher ls
@ my_aliases    # этот плагин представляет собой локальный каталог
* simple        # этот плагин является текущим приглашением
  bass
  fzf
  grc
  thefuck
  z
```

Обновить все.

```
fisher up
```

Обновление некоторых плагинов.

```
fisher up bass z fzf thefuck
```

Удалить плагины.

```
fisher rm simple
```

Удалить все плагины.

```
fisher ls | fisher rm
```

Получить помощь.

```
fisher help z
```

## Часто задаваемые вопросы

### 1. Какая версия fish необходима?

fisherman был построен для рыб >= 2.3.0. Если вы используете 2.2.0, добавьте следующий код в ваш `~/.config/fish/config.fish` для [сниппет](#8-Что-такое-плагин) поддержки.

```fish
for file in ~/.config/fish/conf.d/*.fish
    source $file
end
```

### 2. Как мне установить fish на ОС х?

Add fish to the list of login shells in `/etc/shells` and make it your default shell.

```sh
echo "/usr/local/bin/fish" | sudo tee -a /etc/shells
chsh -s /usr/local/bin/fish
```

### 3. Как мне удалить fisherman?

Запустить

```fish
fisher self-uninstall
```

или

```fish
npm un -g fisherman
```

### 4. Совместим fisherman с oh my fish темами и плагины?

Да.

### 5. Почему так положил fisherman данные?

fisherman уходит в `~/.config/fish/functions/fisher.fish`.

Кэш и настройки плагина создается в `~/.cache/fisherman` и `~/.config/fisherman` соответственно.

В fishfile сохраняется в `~/.config/fish/fishfile`.

### 6. Что такое fishfile и как я могу его использовать?

В fishfile `~/.config/fish/fishfile` выводит список всех установленных плагинов.

Вы можете позволить fisherman сохранить этот файл для вас автоматически, или оставить в плагины и запустить `fisher`, чтобы удовлетворить эти изменения.

```
fisherman/simple
fisherman/z
omf/thefuck
omf/grc
```

Этот механизм устанавливает только плагины и отсутствующие зависимости. Чтобы удалить плагин, используйте `fisher rm` вместо этого.

### 7. Где я могу найти список fish плагинов?

Используя поиск в [организации] или [онлайн] поиск для изучения содержимого.

### 8. Что такое плагин?

Плагин является:

1. каталог или git repo с функцией `.fish` файл либо на корневом уровне проекта или внутри `functions` директории

2. тема или приглашение, т.е., `fish_prompt.fish`, `fish_right_prompt.fish` или оба файла

3. фрагмент, т.е., один или более `.fish` файлов внутри папки по имени `conf.d` которые оцениваются fish при запуске оболочки

### 9. Как я могу получит список плагинов в качестве зависимостей для моего плагина?

Создать новый файл `fishfile` в корневом каталоге вашего проекта и записи в зависимости плагин.

```fish
owner/repo
https://github.com/dude/sweet
https://gist.github.com/bucaran/c256586044fea832e62f02bc6f6daf32
```
