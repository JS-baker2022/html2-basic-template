Проект завершить не смог. Из огромного срока на проект смог выделить 14 часов.

# Сборка для HTML-курсов в HTML Academy
Сборка работает на gulp 4 версии

## Начало
Для работы с репозиторием на вашем компьютере потребуется Git и Node.js (18.x.x). Перед началом работы убедитесь, что все программы работают. Для этого в терминале введите:
- для git
```bash
git --version
```
git примерно ответит
```bash
git version 2.42.0.windows.1
```

![проверка версии git](assets/git.png)

версия не важна. Главное, что git отреагировал и написал ответ

- для node.js
```bash
node -v
```
node.js примерно ответит
```bash
v18.18.0
```

![проверка версии node.js](assets/node.png)

важно, чтобы версия была 18.x.x.

После того как вы убедились, что Git и Node.js работают вам нужно определиться с каким препроцессором вы будете работать на проекте: SASS или Less

### SASS
1. Клонируйте репозиторий `git clone git@github.com:htmlacademy/html2-basic-template.git`
2. Установите зависимости проекта `npm ci`
3. Начните работу `npm start` // должен запуститься браузер

### Less
1. Клонируйте репозиторий `git clone git@github.com:htmlacademy/html2-basic-template.git`
2. Перейдите в ветку с Less-препроцессором `git switch less`
3. Установите зависимости проекта `npm ci`
4. Начните работу `npm start` // должен запуститься браузер

## Структура папок
В каждой папке есть Readme.md файл, который имеет более полное описание по работе с папкой

```
├── .github/                      # Специальная папка для github
│   └── workflows/                # Автоматизация для github actions
│       ├── check.yml             # Запускает линтеры на Гитхабе
│       └──  gh-pages.yml         # Публикует проект и создаёт ссылку на проект
├── source/                       # Исходники проекта
│   ├── fonts/                    # Папка для шрифтов
│   ├── images/                   # Папка для хранения картинок
│   │   └── icons/                # Специальная папка для преобразования svg в спрайт(stack)
│   ├── js                        # Скрипты
│   │   └── script.js             # Главный скрипт
│   ├── sass|less/                # Папка для препроцессорных файлов sass или less
│   │   └── blocks/               # Стили БЭМ-блоков
│   │       └── header.scss       # Стили для конкретного БЭМ-блока
│   │   └── global                # Файл для подключения стилей библиотек из папки
│   │       ├── fonts.scss        # Подключение шрифтов к проекту
│   │       ├── global.scss       # Глобальные стили, которые касаются всего проекта
│   │       └── variables.scss    # Переменные для всего проекта
│   ├── vendor                    # Папка для сторонних бибилотек
│   └──  index.html               # HTML-файл для главной страницы
└── .editorconfig                 # Настройки форматирования текстовых файлов
└── .gitignore                    # Настройки игнорирования файлов для git
└── .stylelintrc                  # Правила для stylelint
└── gulpfile.js                   # Автоматизация для Gulp
└── package.json                  # Зависимости проекта, скрипты, настройки проекта
└── package-lock.json             # Зависимости проекта
└── README.md                     # Документация
```

## Основные команды
- `npm start` - запускает сборку с сервером для разработки проекта
- `npm run build` - создаёт папку `build` с оптимизированными файлами для продакшена

## Дополнительные команды
- `npm run preview` - посмотреть результат работы prod-версии сборки
- `npm run lint` - запустить все проверки. Занимает длительное время
- `npm run lint:bem` - проверить правильно использования БЭМ
- `npm run lint:markup` - проверить HTML-разметку через W3C-валидатор
- `npm run lint:styles` - проверить проект на совместимость с stylelint
- `npm run lint:spaces` - проверить отступы с помощью editorConfig
- `npm run lint:html` - проверить разметку по правилам linthtml

## Работа с разметкой
Все HTML-файлы с разметкой складывайте в папку `source/`.

```bash
├── source/
│   ├──  index.html
│   ├──  catalog.html
│   └──  form.html
```

из папки `source/` сборка переносит файлы в папку `build/`.

```bash
├── build/
│   ├──  index.html
│   ├──  catalog.html
│   └──  form.html
```

## Работа со стилями
Все стили находятся в папке `source/sass/`.

```bash
├── source/
│   ├── sass
│   │   └── blocks/
│   │       └── header.scss
│   │   └── global
│   │       ├── fonts.scss
│   │       ├── global.scss
│   │       └── variables.scss
```

Все БЭМ-блоки и остальные препроцессорные файлы подключайте в `source/sass/styles.scss`.

_styles.scss_
```scss
/* GLOBAL */
@import "global/variables";
@import "global/global";
@import "global/fonts";

/* BLOCKS */
@import "blocks/header";
```

БЭМ-блоки импортируйте в секцию `/* BLOCKS */`.

Все препроцессорные файлы сборка обработает и превратит в `styles.css`. Файл `styles.css` сборка перенесёт в

```bash
├── build/
│   └──  css/
│        └──  styles.css
```

## Работа с графикой
Абсолютно всю графику складывайте в `source/images`.

Векторную графику для спрайта складывайте в `source/images/icons/`. Автоматизация создаст из иконок файл `stack.svg`.

```bash
├── source/
│   ├── images/
│   │   └── icons/
```

Всю графику автоматизация перенесёт в `build/images/`.

```bash
├── build/
│   └──  images/
│        └── icons       # папка для спрайта
│            └── stack.svg # спрайт
│        ├── bg.jpg
│        ├── hero.png
│        └── burger.svg
```

## Работа со шрифтами
Все шрифтовые файлы лежат в `source/fonts/`. Сборка переносит их в `build/fonts/`.

```bash
├── build/
│   └──  fonts/
│        ├──  open-sans.woff2
│        ├──  open-sans.woff
│        ├──  open-sans-bold.woff
│        └──  open-sans-bold.woff

```
## Работа со скриптами
Все скрипты лежат в `source/script/`.

```bash
├── source/
│   ├── js
│   │   ├── script.js
│   │   └── modal.js
```

Сборка переносит их в `build/script/`.
```bash
├── build/
│   ├── js
│   │   ├── script.js
│   │   └── modal.js
```

## Работа со сторонними библиотеками
Для удобства внесения сторонних библиотек в ваш проект, вы можете использовать папку vendor. В этой папке вы можете размещать любые файлы, связанные с внешними библиотеками.

Например, предположим, что вы хотите добавить в проект библиотеку, которая включает в себя как стилевой файл library.css, так и скрипты library.js. Чтобы интегрировать их в ваш проект, следуйте этим шагам:

Положите файлы библиотеки в папку vendor, как показано ниже:

```bash
├── source/
│   └── vendor/
│        ├── library.css
│        └── library.js
```

Если у вас есть несколько библиотек с разными файлами, вы можете группировать файлы одной библиотеки в ее собственную подпапку. Например:
```bash
├── source/
│   └── vendor/
│       └── library/
│             ├── library.css
│             └── library.js
```

При сборке вашего проекта, все файлы из папки vendor будут включены в папку build, сохраняя их структуру. Например:
```bash
├── build/
│   └── vendor/
│        └── library/
│             ├── library.css
│             └── library.js
```

Таким образом, вы можете удобно организовать и внедрить сторонние библиотеки в ваш проект, сохраняя их структуру в папке vendor.
