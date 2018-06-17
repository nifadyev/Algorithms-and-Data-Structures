# Экзаменационный билет №10

## 1. Общая характеристика стандартной библиотеки шаблонов.

В стандарте языка С++ предусматривается наличие в среде программирования стандартной библиотеки шаблонов (Standard Template Library, STL).

Основные понятия библиотеки STL.

Библиотека включает в свой состав большое количество контейнеров, представляющих собой структуры данных, в которых могут храниться объекты.

В числе имеющихся контейнеров:

- `vector<T>` - вектор переменного размера
- `list<T>` - двусвязный список
- `queue<T>` - очередь
- `stack<T>` - стек
- `deque<T>` - дек
- `priority_queue<T>` - приоритетная очередь
- `set<T>` - множество
- `multiset<T>` - множество с повторением элементов
- `map<key,val>` - ассоциативный массив (таблица)
- `multimap<key,val>` - ассоциативный массив с повторением ключей

Для быстрого и эффективного построения вычислительных процедур, библиотека обеспечивает итераторы для всех видов контейнеров, которые представляют унифицированный механизм последовательного доступа к элементам контейнеров.

Общая схема:

- `<класс-контейнер>::iterator Iter;` - объявление итератора
- `Iter = <объект-контейнер>.begin();` - установка на первый элемент
- `Iter != <объект-контейнер>.end();` - проверка на завершение
- `++Iter` – переход к следующему элементу

В зависимости от типа контейнера, итератор может обеспечивать прямой доступ, быть одно- или дву- направленным, предназначенным только для чтения или записи и др. Библиотека содержит для контейнеров большое количество реализованных обобщенных алгоритмов.

В числе таких алгоритмов:

- `for_each()` - вызвать функцию для каждого элемента,
- `find()` - найти первое вхождение элемента
- `find_if()` - найти первое соответствие условию
- `count()`- подсчитать число вхождений элемента
- `count_if()` - подсчитать число соответствий условию
- `replace()` - заменить элемент новым значением
- `copy()` - скопировать элементы
- `unique_copy()` - скопировать только различные элементы
- `sort()` - отсортировать элементы
- `merge()` - объединить отсортированные последовательности и др

## 2. Алгоритм обхода иерархического списка (итератор).

Печать текста: схема обхода

- текст текущей строки
- текст подуровня
- текст следующего раздела текста того же уровня (top-down-next).

```C++
while (1)
{
   if ( pLink != NULL )
   {
       cout << pLink->Str; // обработка звена
       St.push(pLink); // запись в стек
       pLink = pLink->pDown; // переход на подуровень
   }
   else if ( St.empty() )
       break;
   else
   {
       pLink = St.top();
       St.pop(); // выборка из стека
       pLink = pLink->pNext; // переход по тому же уровню
   }
}
```

**Ввод текста из файла**: уровень текста в файле можно выделить строками специального вида (например, скобками '{' и '}').

Общая схема алгоритма:

```
повторить:
ввод строки
ЕСЛИ '}' ТО Завершить
ЕСЛИ '{' ТО Выполнить рекурсивно Ввод_текста
Добавить строку на том же уровне
```