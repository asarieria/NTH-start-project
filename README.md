# Стартовый проект с gulp

Установка: выполнить в папке проекта: `npm i`.

Использование: `npm start` (дабы не ставить глобально 4-ю версию gulp, которая сейчас в альфе). После `npm start` можно через пробел указать задачу. К примеру `npm start less` выполнит только задачу `less` из `gulpfile.js` (полный список задач смотри в `gulpfile.js`).

`port=3004 npm start` — для запуска сервера автообновлений на указанном порту.



## Парадигма

- Используется именование классов и файлов по БЭМ.
- Каждый БЭМ-блок в своей папке внутри `/src/blocks/` (less, js, картинки, разметка; обязателен только less-файл).
- Есть глобальные файлы: css, js, шрифты, картинки, less-файлы (переменные, глобальная стилизация...).
- Есть диспетчер подключений `/src/less/style.less`. Если в нем импортирован less-файл какого-либо блока, этот блок считается используемым (обрабатывается его js и доп. файлы).


### Блоки

Каждый блок лежит в `/src/blocks/` в своей папке. Каждый блок — как минимум, папка и одноимённый less-файл.

Возможное содержимое блока:

```bash
block-name/               # Папка блока
  img/                    # Изображения, используемые блоком
  demo-block.less         # Главный стилевой файл блока
  demo-block--mod.less    # Отдельный файл модификатора блока (если объемный и нужен не на всех проектах)
  demo-block.js           # Главный js-файл блока
  demo-block--mod.js      # js-файл для отдельного модификатора блока 
  demo-block.html         # Варианты разметки (только как документация блока или как вставляемый фрагмент)
  demo-block.css          # Добавочный css (копируется как отдельный файл в `build/css`)
  readme.md               # Какое-то пояснение
```



## Подключение блоков

Если в диспетчере подключений (`/src/less/style.less`):

```
@import "../blocks/demo-block/demo-block.less";
```

То указанный файл будет взят в компиляцию стилей, а так же:
- в обработку будет взят js-файл блока: `src/blocks/demo-block/demo-block.js` (если существует и не пустой)
- в обработку будет взят css-файл блока: `src/blocks/demo-block/demo-block.css` (если существует и не пустой)
- в обработку будут добавлены все картинки блока: `src/blocks/demo-block/img/*.{jpg,jpeg,gif,png,svg}`


```
@import "../blocks/demo-block/demo-block.less";
@import "../blocks/demo-block/demo-block--mod.less";
```



## Назначение папок

```bash
build/          # Сюда собирается проект, здесь работает сервер автообновлений.
src/            # Исходные файлы
  _include/     # - фрагменты html, обще для всех страниц
  blocks/       # - блоки (компоненты) проекта
  css/          # - глобальный css-файл (будет скопирован только если существует и не пустой)
  fonts/        # - шрифты проекта (никак не обрабатываются, см. http://jaicab.com/localFont/)
  img/          # - глобальные картинки (будут обработаны только из корня этой папки, подпапки игнорируются)
  js/           # - глобальный js-файл (обработается только если существует и не пустой)
  less/         # - диспетчер подключений и глобальные стили
  _blocks_library.html  # библиотека блоков проекта
  index.html            # главная страница проекта
```
