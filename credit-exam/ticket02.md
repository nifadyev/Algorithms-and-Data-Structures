# Билет 2
## Языки разметки (XML, YAML, JSON). Назначение, плюсы и минусы каждого из них.
__Язык разметки__ — набор символов или последовательностей, вставляемых в текст для передачи информации о его выводе или строении.

## XML (eXtensible Markup Language)

### Достоинства

* Распространённость
* Поддержка многими редакторами
* Поддержка многими языками программирования
* позволяет стандартизировать вид файлов-данных в виде текста, который будет понятен человеку
* поддержка Юникод
* возможность описания записей, списков, деревьев, форматированного текста
* описание структур и имен полей, как описание значения полей, иными словами – это самодокументируемый формат
* строго определенные требования к анализу и синтаксис, позволяющие быть простым, непротиворечивым и эффективным
* иерархическая структура подходит для описания любых документов, кроме видео и аудио файлов, растровых изображений, двоичных данных и сетевых структур данных

### Недостатки

* Плохо воспринимается человеком в исходнике
* Неудобно редактировать
* Довольно сложная грамматика (90 паттернов)
* Нет возможности поточной обработки
* Не совместим с бинарными данными
* избыточный синтаксис
* размер документа больше, чем документа в других форматах передачи текстовых данных
* для большого количества задач можно использовать более простые решения
* отсутствие общепринятой методологии
* неоднозначность моделирования

### Примеры использования

* Отчеты различных утилит (результаты тестирования)
* Сериализация структур данных
* Конфигурационные файлы (в том числе для построения)


## YAML (YAML Ain't Markup Language)

### Достоинства

* легко понятен человеку
* ориентирован на удобство ввода-вывода типичных структур данных многих языков программирования
* переносим между языками программирования
* выразительный и расширяемый
* лёгкий в реализации и использовании
* Поддержка поточной обработки

### Недостатки

* Крайне сложная грамматика (210 паттернов).
* Не совместим с бинарными данными
* содержит много пространств отступа
* не настолько популярен как XML или JSON
* для каждого языка приходится писать собственный парсер
* нельзя применять стандартные преобразования
* нельзя создавать составные документы

### Примеры использования

* Конфигурационные файлы
* Сериализованные данные

## JSON (JavaScript Object Notation)

### Достоинства

* распространённость
* поддержка многими редакторами
* поддержка многими языками программирования
* довольно простая грамматика (30 паттернов)
* функционально и синтаксически является подмножеством YAML
* скорость выполнения
* поддержка реляционных данных
* поддержка расширяемых типов данных помимо примитивов: строк, чисел, логических значений и т. д.
* расширяемость (увеличить данные легче, нежели чем в XML)
* наладка и налаживание погрешностей


### Недостатки
* безопасность (вызов eval())
* нет возможности поточной обработки 

### Примеры использования

* Cериализация структур, часто в веб-приложениях



## Google Test. Назначение, возможности (и unit-testing фреймворков вообще), использование.
## Краткая информация

* Популярный фреймворк для написания модульных тестов на С++ разработанный Google.
* Проект c BSD-лицензией (допускает использование в закрытых коммерческих проектах).
*. Используется в целом ряде крупных проектов
    * Chromium, LLVM компилятор, OpenCV
* Написан на C++, строится при помощи CMake
     * Поддерживает: Linux, Mac OS X, Windows, Cygwin, Windows CE и Symbian
* Как правило используется в консольном режиме, но существует вспомогательное GUI.

## Типичные возможности unit-testing фреймворков

* Удобное добавление тестов
    * Простая регистрация новых тестов
    * Набор функций-проверок (`assert`)
    * Общие инициализации и деинициализации
* Удобный запуск тестов
    * Пакетный режим
    * Возможность фильтрации тестов по именам
* Часто допускают интеграцию с IDE
* Генерация отчета в стандартном XML-формате
    * Возможность последующего автоматического анализа
    * Публикация на web-страницах проекта

## Возможности Google Test

* Автоматическое развервертывание тестов (Automatic test discovery)
* Большой набор assertions, возможность создавать пользовательские assertions (Rich set of assertions, user-defined assertions)
* "Смертельные" тесты (Death tests)
* Критические и некритические сбои (Fatal and non-fatal failures)
* Параметризуемые по типу или по значению тесты (Value- and type-parameterized tests)
* Различные опции по запуску тестов (Various options for running the tests)
* Генерация отчета в XML формате (XML test report generation)

## Порядок использования Google Test

* Каждый тест реализован как функция, с использованием макроса `TEST()` или `TEST_F()`.
    * `TEST()` не только определяет, но и "регистрирует" тест.
* Новые тесты добавляются в тот же test suite, их могут быть тысячи.
* При необходимости test suite разбивается на несколько
    * Корректность и производительность
    * Быстрый (pre-commit) и полный (ночной)

### Пример
```cpp
#include <gtest/gtest.h>

TEST(MathTest, TwoPlusTwoIsFour) {
  EXPECT_EQ(2 + 2, 4);
}
```