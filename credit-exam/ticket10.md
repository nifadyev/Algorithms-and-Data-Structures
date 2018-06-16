# Билет №10
## История развития билд-систем (от shell до CMake и IDE).

## Вводная информация

* Исторически сложилось, что разработчики применяли автоматизацию сборки для вызова компиляторов и линковщиков из скрипта сборки, в отличие от вызова компилятора из командной строки
* Довольно просто при помощи командной строки передать один исходный модуль компилятору, а затем и линковщику для создания конечного объекта
* Однако, при попытке скомпилировать или слинковать множество модулей с исходным кодом, причём в определенном порядке, осуществление этого процесса вручную при помощи командной строки выглядит слишком неудобным
* Гораздо более привлекательной альтернативой является скриптовый язык, поддерживаемый утилитой Make
    * Данный инструмент позволяет писать скрипты сборки, определяя порядок их вызова, этапы компиляции и линковки для сборки программы.
    * GNU Make также предоставляет такие дополнительные возможности, как например, «зависимости» («makedepend»), которые позволяют указать условия подключения исходного кода на каждом этапе сборки
    * Это и стало началом автоматизации сборки.
    * Основной целью была автоматизация вызовов компиляторов и линковщиков
* По мере роста и усложнения процесса сборки разработчики начали добавлять действия до и после вызовов компиляторов, как например, проверку (check-out) версий копируемых объектов на тестовую систему
* Термин «автоматизация сборки» уже включает в себя управление и действия до и после компиляции и линковки, так же как и действия при компиляции и линковке.

## История

* shell скрипты

compile.sh:

```tbd
#!/bin/sh
cc -c main.c
cc -c lib.c
cc -o program main.o lib.o
```

* make, 1977 год

Makefile:

```tbd
OBJ = main.o lib.o
program: $(OBJ)
        cc -o program $(OBJ)
$(OBJ): defines.h
```

* Autotools
    * Было де-факто стандартом и до сих пор используется, но:
        * слишком сложно
        * только Unix
        * sh, m4
        * зависимости

Makefile.am:

```tbd
bin_PROGRAMS = hello
hello_SOURCES = main.c lib.c
```

configure.ac:

```tbd
AC_INIT([program], [1.0], [sample@mail.org])
AM_INIT_AUTOMAKE([-Wall -Werror foreign])
AC_PROG_CC
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([
 Makefile
])
AC_OUTPUT
```

Для запуска:

```tbd
autoreconf --install
./configure
make
```

## CMake

    * Широкая поддержка разнообразных целевых платформ и IDE
    * Максимальная свобода в выборе окружения разработки (в рамках одной команды!)
    * В настоящий момент является стандартом де-факто для С++ проектов
    * Основной "недостаток" — собственный язык
    * Поначалу инструмент кажется нетривиальным, но очень удобен впоследствии
    * Дает членам команды максимальную свободу в выборе инструментов (OC, IDE или простой текстовый редактор)
    * Обеспечивает переносимость и является стандартом де-факто\
    для кросс-платформенных С++ проектов

### CMake workflow

* `CMakeLists.txt` — файл, описывающий порядок сборки приложения
* Плохая практика хранить все файлы (в том числе и исполняемые) в одной директории
* Хорошая практика - располагать файлы по директориям src, include, build, test и т.д.



## UNIX. Философия и преимущества при автоматизации.

## Философия UNIX

* Пишите программы, выполняющие одну задачу и выполняющие ее хорошо (Write programs that do one thing and do it well)
* Пишите программы для совместной работы (Write programs to work together)
* Пишите программы, обрабатывающие/использующие текстовые потоки, так как текстовые потоки - универсальный интерфейс (Write programs to handle text streams, because that is a universal interface)

## Преимущества при автоматизации

* Огромное количество утилит на любой случай жизни (find, cron, tar, sed, и т.д.)
* Вместе со скриптовыми языками (Bash, Perl, Python, etc) предоставляет широчайшие возможности для автоматизации