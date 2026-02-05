# Кастомизация стилей док.проекта

MkDocs Material поддерживает расширенную настройку оформления сайта с помощью подключения дополнительного файла со стилями `extra.css`.

!!! note "Справка"
    CSS — это язык стилей, который определяет внешний вид веб-страниц. CSS описывает, как элементы HTML должны отображаются на экране.

## Подключение extra.css

1. Откройте рабочую директорию проекта.
2. В корне папки `docs` создайте папку `stylesheets`.
3. В корне папки `stylesheets` создайте файл `extra.css`.
4. Подключите файл `extra.css` в конфиге проекта:

    ```yaml title="mkdocs.yml"
    extra_css:
      - stylesheets/extra.css
    ```

## Настройка цветовой схемы

В файле `extra.css` вы можете менять настройки стандартных светлой и тёмной цветовых схем:

```css title="extra.css"
/* Настройки светлой схемы */

[data-md-color-scheme="default"] {
  --md-primary-fg-color: #0B61A4; /*Основной цвет*/
  --md-accent-fg-color: #1565C0; /*Акцентный цвет*/
  --md-typeset-a-color: #0e70e0; /*Цвет ссылок*/
  --md-default-bg-color: #f0f8ff; /*Фоновый цвет*/
  --md-default-fg-color: #353535; /*Основной цвет текста (абзацы, списки, подзаголовки, nav и toc)*/
  --md-code-bg-color: #ffffff; /*Цвет фона блока кода*/
  --md-code-fg-color: #5c5b5b; /*Цвет текста в блоке кода*/
  --md-default-fg-color--light: #4e4d4d; /*Цвет h1 и заголовков блоков toc и nav*/
}

/* Настройки тёмной схемы */

[data-md-color-scheme="slate"] {
  --md-primary-fg-color: #0B61A4; /*Основной цвет*/
  --md-accent-fg-color: #1565C0; /*Акцентный цвет*/
  --md-typeset-a-color: #0e70e0; /*Цвет ссылок*/
  --md-default-bg-color: #f0f8ff; /*Фоновый цвет*/
  --md-default-fg-color: #353535; /*Основной цвет текста (абзацы, списки, подзаголовки, nav и toc)*/
  --md-code-bg-color: #ffffff; /*Цвет фона блока кода*/
  --md-code-fg-color: #5c5b5b; /*Цвет текста в блоке кода*/
  --md-default-fg-color--light: #4e4d4d; /*Цвет h1 и заголовков блоков toc и nav*/
}
```

Также вы можете создать свою цветовую схему и подключить её вместо стандартных в mkdocs.yml:

```css title="extra.css"
/* Настройки светлой темы */

[data-md-color-scheme="my-scheme"] {
  --md-primary-fg-color: #0B61A4; /*Основной цвет*/
  --md-accent-fg-color: #1565C0; /*Акцентный цвет*/
  --md-typeset-a-color: #0e70e0; /*Цвет ссылок*/
  --md-default-bg-color: #f0f8ff; /*Фоновый цвет*/
  --md-default-fg-color: #353535; /*Основной цвет текста (абзацы, списки, подзаголовки, nav и toc)*/
  --md-code-bg-color: #ffffff; /*Цвет фона блока кода*/
  --md-code-fg-color: #5c5b5b; /*Цвет текста в блоке кода*/
  --md-default-fg-color--light: #4e4d4d; /*Цвет h1 и заголовков блоков toc и nav*/
  --md-footer-bg-color: #25567B; /*Цвет футера*/
}
```

```yaml title="mkdocs.yml"
theme:
…
  palette: # Настройки тем
    - scheme: my-scheme
```

!!! info "Примечание"
    Для изменения цвета выберите нужную переменную в `extra.css` и введите hex-код цвета или нажмите на квадратик и выберите нужный цвет в палитре.

    Для подбора сочетающихся цветов вы можете воспользоваться [цветовым кругом](https://colorscheme.ru/){target=_blank}.

## Настройка шрифтов

С помощью `extra.css` вы можете переопределить параметры текста: шрифт, начертание, цвет, размер:

```css title="extra.css"
/*Параметры текста статей*/
.md-typeset {
    font-family: 'Tahoma, arial';
    font-weight: 600;
    font-size: 25px;
    color: #4b5563;
}
/*Параметры текста nav и toc*/
.md-nav {
    font-family: 'Tahoma, arial';
    font-weight: 400;
    font-size: 16px;
    color: #4b5563;
}
```

Также вы можете настроить параметры отдельных элементов текста, например, заголовков:

```css title="extra.css"
.md-content h1, .md-content h2, .md-content h3, .md-content h4 {
    font-family: 'Roboto Mono';
    font-weight: 600;
    color: #4b5563;
}
```

Или сочетать разные настройки:

```css title="extra.css"
.md-typeset {
    font-family: 'Tahoma, arial';
    font-weight: 600;
    font-size: 25px;
    color: #4b5563;
}

.md-content h1, .md-content h2, .md-content h3, .md-content h4 {
    font-family: 'Roboto Mono';
    font-weight: 600;
    color: #4b5563;
}

.md-content h1 {
    font-size: 30px;
}

.md-content h2 {
    font-size: 24px;
}

.md-content h3 {
    font-size: 21px;
}

.md-content h4 {
    font-size: 18px;
}
```

!!! info "Важно!"
    Настройки отдельных элементов текста (например, класс `.md-content h1`) переопределяют общие настройки (класса `.md-typeset`).


