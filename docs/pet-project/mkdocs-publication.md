# Публикация проекта

Для публикации домашнего проекта мы будем использовать сервис **GitHub Pages** и скрипт [ghp-import](https://github.com/c-w/ghp-import){target=_blank}.

GitHub Pages — это бесплатный хостинг от GitHub, предоставляющий возможность публиковать статические сайты.

## Ручная публикация

1. Откройте командную строку (консоль или терминал в VS Code) в рабочей директории проекта.
2. Переключитесь на master-ветку и обновите её с помощью команды `git pull`.
3. Выполните команду для сборки и публикации сайта:

    ```
    mkdocs gh-deploy
    ```

    * Команда создаёт html-сайт и с помощью скрипта [ghp-import](https://github.com/c-w/ghp-import){target=_blank} фиксирует файлы в ветке gh-pages и отправляет её на сервер.

    * При обновлении ветки `gh-pages` сайт автоматически публикуется на GitHub Pages.

    * В ответе на команду в терминале отобразится URL вашего сайта:

        ```
        INFO    -  Your documentation should shortly be available at: https://novillero.github.io/dac-advanced/
        ```

!!! info "Важно!"
    Команда `mkdocs gh-deploy` оставляет после себя папку `site` в рабочей директории. Не забудьте удалить эту папку после сборки и публикации сайта.

Проверьте свои текущие настройки публикации:

1. Откройте репозиторий в гитхабе и перейдите на вкладку **Settings**;
2. В левом меню выберите пункт **Pages**;
3. На этой странице указаны настройки публикации сайта на GitHub Pages. Посмотрите на установленные значения:

    * Sourse — `Deploy from a branch`;
    * Branch — `gh-pages; folder — /(root)`.

Это значит, что ваш сайт публикуется из ветки, ветка для публикации — `gh-pages`.

## Автоматическая публикация

Вы можете настроить автоматическую публикацию документации с помощью **GitHub Actions**.

**GitHub Actions** — это сервис автоматизации задач, с помощью которого можно настраивать CI/CD проектов.

Для автоматической сборки и публикации проекта вам понадобится создать *Workflow* и настроить события, которые будут его запускать.

**Workflow** — это автоматизированный процесс, который запускается при определённых событиях в репозитории (например, пуш в мастер-ветку). Workflow представляет собой yaml-файл, внутри которого описана последовательность шагов, которые нужно выполнить.

1. Откройте рабочую директорию проекта в VS Code.
2. Отколите новую ветку от мастер-ветки.
3. Создайте новую папку `.github`в корне проекта.
4. Внутри папки .github создайте папку `workflows`.
5. В папке `workflows` создайте файл `ci.yml`.
6. Откройте файл `ci.yml` и добавьте в него текст:

    ```yaml title="ci.yml"
    name: ci
    on:
      push:
        branches:
          - master
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v3
          - uses: actions/setup-python@v4
            with:
              python-version: 3.x
          - uses: actions/cache@v2
            with:
              key: ${{ github.ref }}
              path: .cache
          - run: pip install mkdocs-material
          - run: mkdocs gh-deploy --force
    ```

7. Сохраните файл. Создайте коммит, опубликуйте ветку и отправьте изменения на сервер.
8. Откройте удалённый репозиторий в GitHub, создайте Pull Request и влейте ваши изменения в ветку `master`.
9. Перейдите в раздел **Actions → All workflow**. В списке workflow появилась новая запись — это и есть ваш новый автоматический процесс. После завершения процесса (все галочки станут зелёными) сайт обновится.

В данном workflow вы указали триггер для запуска — push в ветку `master`. Теперь при любом пуше в мастер-ветку будет запускаться сборка и публикация вашего проекта.

!!! info "Важно"
    Если вы используете в проекте внешние плагины, вы должны прописать их установку в шагах workflow:

    ```yaml title="ci.yml"
    name: ci
    on:
      push:
        branches:
          - master
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v3
          - uses: actions/setup-python@v4
            with:
              python-version: 3.x
          - uses: actions/cache@v2
            with:
              key: ${{ github.ref }}
              path: .cache
          - run: pip install mkdocs-material
          - run: pip install pip install mkdocs-glightbox # шаг для установки плагина mkdocs-glightbox
          - run: mkdocs gh-deploy --force
    ```