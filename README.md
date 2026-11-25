SPP-AGF

SPP-AGF (Advanced Graphical Framework for SPP) — графический фреймворк для создания 2D-приложений на языке программирования S++ с использованием SDL2.

Проект использует оригинальный компилятор SPP: "f35clt2/sppc" (https://github.com/f35clt2/sppc).

Текущая версия: 0.1.2
Платформа: Windows 10/11
Графический backend: SDL2
Язык: S++
Лицензия: GNU GPL v3.0

«В этой версии графические функции AGF вызываются через C Foreign Function Interface ("stdc:RunC"). Синтаксис "import agf" пока не поддерживается.»

---

Содержание

1. Возможности
2. Требования
3. Установка
4. Сборка и запуск
5. Структура проекта
6. Первое приложение
7. Обучение языку S++
8. Графический API AGF
9. Компилятор S++
10. Решение проблем
11. Лицензия

1. Возможности

SPP-AGF предназначен для создания графических 2D-приложений.

Основные возможности:

- Создание графических окон.
- Обработка событий SDL2.
- Очистка и обновление экрана.
- Установка цвета рисования.
- Отрисовка прямоугольников.
- Вывод текста.
- Интеграция с языком S++.
- Использование оригинального SPP-компилятора.

2. Требования

Для работы необходимы:

Компонент| Назначение
Windows 10/11| Операционная система
MSYS2| Среда разработки
GCC| C-компилятор
SDL2| Графическая библиотека
pkg-config/pkgconf| Поиск библиотек
Git| Загрузка исходников
sppc| Компилятор S++

Все компоненты GCC и SDL2 должны принадлежать одному окружению MSYS2.

3. Установка

Шаг 1. Установка MSYS2

Скачайте MSYS2:

https://www.msys2.org/

После установки откройте терминал MSYS2 UCRT64.

Обновите пакеты:

pacman -Syu

Если терминал попросит перезапуск, откройте его снова и выполните:

pacman -Su

Шаг 2. Установка зависимостей

Для UCRT64:

pacman -S --needed base-devel mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-SDL2 mingw-w64-ucrt-x86_64-pkgconf git

Шаг 3. Загрузка SPP-AGF

git clone https://github.com/p2l0a1t4on-commits/SPP-AGF.git

Перейдите в каталог:

cd SPP-AGF

Шаг 4. Установка SPP

Запустите:

setup_sppc.bat

Этот сценарий подготавливает оригинальный компилятор SPP.

Компилятор также доступен отдельно:

https://github.com/f35clt2/sppc

Важно: проект использует оригинальный SPP-компилятор, а не отдельный нативный Windows-компилятор.

4. Сборка и запуск

После установки всех зависимостей откройте командную строку в корне проекта.

Выполните:

build.bat

После успешной сборки запустите:

build\agf_hello.exe

Должно открыться демонстрационное графическое окно.

5. Структура проекта

SPP-AGF/
│
├── vendor/
│   └── sppc/
│
├── include/
│
├── src/
│
├── examples/
│
├── build/
│
├── setup_sppc.bat
├── build.bat
│
├── LICENSE
└── README.md

Описание:

- "vendor/sppc" — оригинальный компилятор SPP.
- "include" — заголовки и интерфейсы AGF.
- "src" — исходный код графического фреймворка.
- "examples" — демонстрационные программы.
- "build" — результаты сборки.
- "setup_sppc.bat" — подготовка компилятора.
- "build.bat" — сценарий сборки.

6. Первое приложение

SPP-AGF использует язык S++.

Пример стандартной программы:

import stdsys;

declare function Main() {
    printf("Hello from SPP-AGF!");
        stdsys:exit(0);
        }

        Для графики используется интерфейс AGF через C FFI.

        Основные функции:

        agf_init
        agf_poll_events
        agf_clear
        agf_present
        agf_set_color
        agf_fill_rect
        agf_draw_text
        agf_shutdown

        Точные параметры функций необходимо брать из актуальных заголовков в "include/" и рабочего примера в "examples/".

        7. Обучение языку S++

        7.1. Основы синтаксиса

        S++ — статически типизированный язык.

        Каждая инструкция завершается символом ";".

        Объявление переменных выполняется через "declare".

        declare int number = 10;
        declare str name = "Bashid";
        declare bool enabled = true;

        7.2. Типы данных

        Тип| Описание
        "int"| Целое 64-битное число
        "float"| Число с плавающей точкой
        "str"| Строка UTF-8
        "bool"| Логическое значение
        "path"| Путь к файлу
        "array"| Динамический массив
        "undef"| Специальное значение "nil"

        Пример:

        declare int age = 18;
        declare float speed = 3.14;
        declare str title = "My application";
        declare bool running = true;
        declare array numbers = [1, 2, 3];
        declare undef empty = nil;

        Также доступна форма объявления с "var":

        declare var message: str = "Hello";

        Тип после двоеточия обязателен.

        7.3. Изменение переменных

        declare int counter = 10;

        counter = 20;
        counter = counter + 5;

        Для изменения типа переменной используется специальная конструкция:

        overwrite counter : counter && type : float;

        7.4. Арифметика

        Поддерживаются:

        declare int a = 10 + 5;
        declare int b = 10 - 5;
        declare int c = 10 * 5;
        declare int d = 10 / 5;
        declare int e = 10 % 3;

        Побитовые операции:

        declare int x = 7;

        declare int a = x & 3;
        declare int b = x | 8;
        declare int c = x ^ 2;
        declare int d = ~x;
        declare int e = x << 2;
        declare int f = x >> 1;

        Составные операции используют "run":

        run x += 10;
        run x *= 2;
        run x -= 5;

        7.5. Логические операторы

        Вместо "&&" и "||" для логических выражений используются слова:

        - "and"
        - "or"
        - "not"

        Пример:

        declare bool a = true;
        declare bool b = false;

        declare bool result = a and not b;

        7.6. Условия

        declare int age = 18;

        if (age >= 18) {
            printf("Adult");
            } else {
                printf("Underage");
                }

                Условия обязательно заключаются в круглые скобки.

                7.7. Циклы

                Цикл "for" использует три части, разделённые запятыми:

                for (declare int i = 0, i < 10, i++) {
                    printf("Number: <i>");
                    }

                    7.8. Функции

                    Функции объявляются через "declare function".

                    declare function add(int a, int b) -> int {
                        return a + b;
                        }

                        Вызов:

                        declare int result = add(10, 20);

                        Функция без возвращаемого значения:

                        declare function sayHello() {
                            printf("Hello!");
                            }

                            Значения параметров по умолчанию:

                            declare function multiply(int value, int factor = 2) -> int {
                                return value * factor;
                                }

                                Именованные аргументы:

                                declare int result = multiply(factor=5, value=10);

                                7.9. Структуры

                                Структуры объявляются через "declare struct".

                                declare struct Point {
                                    int x;
                                        int y;
                                        };

                                        declare Point position = Point();

                                        position.x = 100;
                                        position.y = 200;

                                        7.10. Массивы

                                        Создание:

                                        declare array numbers = [10, 20, 30];

                                        Добавление элементов:

                                        numbers:amend(40);
                                        numbers:amendToIndex(15, 1);

                                        Изменение:

                                        numbers[0] = 99;

                                        Получение количества элементов:

                                        declare int size = numbers:length();

                                        Удаление:

                                        numbers:removeLast();
                                        numbers:removeByIndex(1);

                                        7.11. Работа со строками

                                        declare str greeting = "Hello";

                                        concat(greeting, " World!");

                                        printf(greeting);

                                        Получение символов:

                                        declare str first = greeting:getFromIndex(0);

                                        Разделение:

                                        declare array words = greeting:split(" ");

                                        Поиск:

                                        declare int index = greeting:getIndexFromElement("World");

                                        Повторение:

                                        declare str repeated = "Hi " * 3;

                                        7.12. Импорт модулей

                                        Стандартные модули подключаются через "import".

                                        import stdsys;
                                        import stdmath;

                                        Пример математических функций:

                                        declare float value = stdmath:sqrt(64.0);

                                        Обрати внимание: вызовы функций модулей используют двоеточие.

                                        7.13. Обработка ошибок

                                        S++ поддерживает "attempt", "catch" и "sabotage".

                                        declare bool errorCaught = false;

                                        attempt {
                                            sabotage 139;
                                            } catch {
                                                errorCaught = true;
                                                };

                                                7.14. C Foreign Function Interface

                                                Для интеграции с C используется "stdc:RunC".

                                                stdc:RunC({
                                                    printf("Hello from C!");
                                                    });

                                                    Этот механизм позволяет использовать нативный C-код.

                                                    Для компиляции программ с C FFI необходимо указывать:

                                                    --allow-foreign

                                                    Используйте эту возможность только с доверенным кодом.

                                                    8. Графический API AGF

                                                    Основные функции графического слоя:

                                                    Функция| Назначение
                                                    "agf_init"| Инициализация AGF
                                                    "agf_poll_events"| Обработка событий
                                                    "agf_clear"| Очистка экрана
                                                    "agf_present"| Отображение кадра
                                                    "agf_set_color"| Установка цвета
                                                    "agf_fill_rect"| Заливка прямоугольника
                                                    "agf_draw_text"| Вывод текста
                                                    "agf_shutdown"| Завершение работы

                                                    Типы аргументов и точные сигнатуры смотри в заголовках проекта.

                                                    9. Компилятор S++

                                                    SPP-AGF использует оригинальный "sppc".

                                                    Основные команды:

                                                    Проверка программы:

                                                    sppc main.spp --check

                                                    Компиляция:

                                                    sppc main.spp -o app --allow-foreign

                                                    Оптимизированная сборка:

                                                    sppc main.spp -o app -O3 --allow-foreign

                                                    Отладочная сборка:

                                                    sppc main.spp -o app -g --allow-foreign

                                                    Форматирование:

                                                    sppc fmt main.spp

                                                    Другие полезные параметры:

                                                    Параметр| Назначение
                                                    "-O0"| Без оптимизации
                                                    "-O1"| Базовая оптимизация
                                                    "-O2"| Повышенная оптимизация
                                                    "-O3"| Максимальная стандартная оптимизация
                                                    "-Os"| Оптимизация размера
                                                    "-g"| Отладочная информация
                                                    "--check"| Проверка исходника
                                                    "--sanitize"| AddressSanitizer и UBSan
                                                    "--allow-foreign"| Разрешение foreign-операций
                                                    "--emit-c"| Вывод сгенерированного C
                                                    "--keep-c"| Сохранение C-файла

                                                    10. Решение проблем

                                                    Ошибка: sppc не найден

                                                    Запустите:

                                                    setup_sppc.bat

                                                    Проверьте наличие каталога:

                                                    vendor/sppc

                                                    Ошибка: SDL2 не найдена

                                                    Установите SDL2 через MSYS2.

                                                    Проверьте, что GCC и SDL2 принадлежат одному окружению.

                                                    Ошибка: Permission denied

                                                    Попробуйте запустить терминал с необходимыми правами и проверьте разрешения на выполнение файлов.

                                                    Ошибка компиляции stdc:RunC

                                                    Добавьте:

                                                    --allow-foreign

                                                    Проверьте корректность C-кода внутри блока.

                                                    Ошибка отсутствующей SDL2 DLL

                                                    Добавьте каталог "bin" соответствующего окружения MSYS2 в PATH.

                                                    Не используйте DLL из неизвестных источников.

                                                    Окно сразу закрывается

                                                    Проверьте цикл обработки событий. Приложение должно регулярно обрабатывать события, рисовать кадр и обновлять окно.

                                                    Ошибки синтаксиса S++

                                                    Проверьте:

                                                    - наличие ";" после инструкций;
                                                    - правильность объявления типов;
                                                    - круглые скобки в условиях;
                                                    - запятые в цикле "for";
                                                    - корректность имён переменных и функций.

                                                    11. Лицензия

                                                    SPP-AGF распространяется под лицензией GNU General Public License v3.0.

                                                    Полный текст лицензии находится в файле "LICENSE".

                                                    Оригинальный SPP-компилятор и SDL2 являются отдельными компонентами со своими лицензионными условиями.

                                                    ---

                                                    SPP-AGF — создавай графические приложения на S++!

                                                    Repository: https://github.com/p2l0a1t4on-commits/SPP-AGF

                                                    SPP Compiler: https://github.com/f35clt2/sppc