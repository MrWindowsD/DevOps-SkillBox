# DevOps-SkillBox
## Как запустить ВМ на Windows
1. Для начала стоит создать ВМ. Для этого можем воспользоваться Yandex.Cloud или любой другой платформой для создания ВМ.  
Также для ВМ нам понадобиться SSH ключ, его можно создать при помощи PuTTYgen, после его создание необходимо сохранить приватную версию ключа, в ВМ будем использовать публичную версию. 
2. После создания ВМ и его успешного запуска (это происходит автоматически, если правильно создать ВМ) нам нужно к нему подключиться, для этого мы запускаем программу PuTTY и в разделе "Session" заполняем публичный IP-adderss (который был выдан вашей ВМ), порт: 22 (классика), название (Saved Sessions) и для входа выбираем "Only on clean exit", после чего сохраняем данную сессию.  
3. После чего нам нужно запустить PuTTY Pageant и добавить туда свой приватный SSH ключ, после чего выходим.  

Теперь мы можем подключаться к нашей ВМ. Для этого в PuTTY загружаем нашу ранее подготовленную сессию и нажимаем на "Open" и у нас запускается консоль, где мы для входа используем свой логин и пароль. После успешного входа мы увидим в консоли имя_пользователя@название_вм:~$  
## Установка необходимых пакетов
Для выполнения поставленных нами задач мы установим на ВМ следующие пакеты: 
- GIt — это бесплатная распределенная система управления версиями с открытым исходным кодом, предназначенная для быстрой и эффективной обработки любых проектов, от небольших до очень крупных.  
- Docker — программное обеспечение для автоматизации развёртывания и управления приложениями в средах с поддержкой контейнеризации. Позволяет «упаковать» приложение со всем его окружением и зависимостями в контейнер, который может быть перенесён на любую Linux-систему с поддержкой cgroups в ядре, а также предоставляет среду по управлению контейнерами.
- Любой текстовый редактор. К примеру **Nano**  

Начнём по порядку. Дня начала по традиции обновляем все репозитории. Для этого вводим команду:  
`sudo apt-get update`. Напоминаю, что в нашем случае у нас стоит _Ubuntu_.  
Теперь устанавливаем необходимые пакеты:  
`sudo apt-get install git docker.io nano`  
Отлично. Установка пакетов закончена. Теперь можем приступать к работе с ВМ !  

## Непрерывная интеграция (CI)
CI (Continuous Integration) — в дословном переводе «непрерывная интеграция». Имеется в виду интеграция отдельных кусочков кода приложения между собой. CI позволяет делать такие проверки автоматически. Он используется в продвинутых командах разработки, которые пишут не только код, но и автотесты. 
В данном разделе мы узнаем о том, как произвести деплой нашего проекта.  

1. Для начала нам нужен сервис, который поможет в CI, к примеру _GitLub_. После регистрации нам нужно создать пустой репозиторий, а также подключить ранее созданный SSH ключ.
2. Нам нужно перенести наш ранее созданный репозиторий на _GitLub_, так как мы использовали _GitHub_ нам понадобиться следующие команды. **Прежде чем переносить репозиторий убедитесь в том, что ваши изменения перенесены с локального на виртуальный репозиторий (на сервер, где храниться </>)**  
Для начала нам стоит узнать название нашего репозитория командой:  
`git remote`. Обычно это "origin".  
После чего мы можем убедиться в том, что это действительно тот репозиторий который нам нужен, а не какой-то другой командой:  
`git remote show -n origin`  
После того как мы в этом убедились, нам нужно переименовать наш репозиторий:  
`git remote rename origin [new_name]`  
Дальше нам нужно просто через ссылку добавить наш репозиторий:  
`git remote add origin https://gitlab.com/userName/repoName.git`. Проверяем командой `git remote` и убеждаемся в том, что у нас теперь два репозитория, один _origin_, другой тот что мы задавали ранее.  
Теперь нам остаётся только запушать наши изменения на сервер:  
`git push -u origin master`   


---

# Flatris
[![Flatris](flatris.png)](https://flatris.space/)

[![Build Status](https://travis-ci.org/skidding/flatris.svg?branch=master)](https://travis-ci.org/skidding/flatris)

> **Work in progress:** Flatris has been recently redesigned from the ground up and turned into a multiplayer game with both UI and server components. This has been an interesting journey and I plan to document the architecture in depth. **[Stay tuned](https://twitter.com/skidding)**.

[![Flatris](flatris.gif)](https://flatris.space/)

> **Contribution disclaimer:** Flatris is a web game with an opinionated feature set and architectural design. It doesn't have a roadmap. While I'm generally open to ideas, I would advise against submitting unannounced PRs with new or modified functionality. That said, **bug reports and fixes are most appreciated.**

Thanks [@paulgergely](https://twitter.com/paulgergely) for the initial flat design!

Also see [elm-flatris](https://github.com/w0rm/elm-flatris).


## Setup and running

```
yarn install
yarn test
yarn build
yarn start
```

Go to http://localhost:3000
