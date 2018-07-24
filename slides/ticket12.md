# Экзаменационный билет №12

## 1.Сборка мусора (Повторное использование памяти)

При удалении разделов текста для освобождения звеньев следует учитывать следующие моменты:

- Обход всех звеньев удаляемого текста может потребовать длительного времени
- При множественности ссылок на разделы текста (для устранения дублирования одинаковых частей) удаляемый текст нельзя исключить – этот текст может быть задействован в других фрагментах текста

Память, занимаемая удаляемым текстом, не освобождается, а удаление текста фиксируется установкой указателей в состояние NULL (например, `pFirst=NULL`).

- Подобный способ выполнения операций удаления текста может привести к ситуации, когда в памяти, используемой для хранения текста, могут присутствовать звенья, на которые нет ссылок в тексте и которые не возвращены в систему управления памятью для повторного использования
- Элементы памяти такого вида носят наименование "**мусора**"
- Наличие "мусора" в системе может быть допустимым, если имеющейся свободой памяти достаточно для работы программ
- В случае нехватки памяти необходимо выполнить "**сборку мусора**".

Возможный подход доступа к системе управления памятью – разработка специальной системы управления при помощи перегрузки операторов `new` и `delete`.

### Общая схема подхода

- Для системы управления память выделяется полностью при начале работы программы
- Вся память форматируется и представляется в виде линейного списка свободных звеньев
- Для фиксации состояния памяти в классе `TTextLink` создается статическая переменная `MemHeader` типа `TTextMem`

```C++
class TTextMem{
    PTTextLink pFirst; // первое звено
    PTTextLink pLast; // последнее звено
    PTTextLink pFree; // первое свободное
```

- Для выделения и форматирования памяти определяется статический метод `InitMemSystem` класса `TTextLink`

```C++
void TTextLink::InitMemSystem(int size) // инициализация памяти
{
    char Line[100];
    char *tmp = new char[sizeof(TTextLink)*size];
    MemHeader.pFirst = (PTTextLink)new char[sizeof(TTextLink)*size];
    MemHeader.pFree = MemHeader.pFirst;
    MemHeader.pLast = (PTTextLink)tmp + size - 1;
    PTTextLink pLink = MemHeader.pFirst;
    for (int i = 0; i < size - 1; i++, pLink++) // размер памяти
        pLink->pNext = pLink + 1;
    pLink->pNext = nullptr;
}
```

- При запросе памяти в операторе new выделяется первое свободное звено

```C++
void* TTextLink::operator new(size_t size) // выделение звена
{
    PTTextLink pLink = MemHeader.pFree;
    if (MemHeader.pFree != nullptr)
        MemHeader.pFree = pLink->pNext;
    return pLink;
}
```

- При освобождение звена в операторе `delete` звено включается в список свободных звеньев

```C++
void operator delete (void *pM)
{
    PTTTextLink pLink = (PTTTextLink)pM;
    pLink->pNext = MemHeader.pFree;
    MemHeader.pFree = pLink;
}
```

- Для различения звеньев «мусора» и текста – маркировка текстовых звеньев и звеньев списка свободных звеньев

## 2. Оценка сложности обработки деревьев поиска.

![](https://latex.codecogs.com/svg.latex?%5Clarge%20T_%7Bmin%7D%20%3D%201)
![](https://latex.codecogs.com/svg.latex?%5Clarge%20T_%7Bmax%7D%3Dlog2N) (при сбалансированном дереве)
![](https://latex.codecogs.com/svg.latex?%5Clarge%20T_%7Bmax%7D%3DN) (при вырожденном дереве)


![](https://latex.codecogs.com/svg.latex?%5Clarge%20a_N%20%3D%20%5Cfrac%7B1%7D%7BN%7D%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20a%5Ei_N%20%3D%20%5Cfrac%7B1%7D%7BN%7D%5Csum_%7Bi%3D1%7D%5E%7BN%7D%20%28%28a%5Ei_%7Bi-1%7D&plus;1%29%5Cfrac%7Bi-1%7D%7BN%7D%20&plus;%201%5Cfrac%7B1%7D%7BN%7D%20&plus;%20%28a_%7BN-i%7D&plus;1%29%5Cfrac%7BN-i%7D%7BN%7D%29%20%3D%20%5Cfrac%7B1%7D%7BN%7D%28N%20&plus;%20%5Cfrac%7B1%7D%7BN%7D%5Csum_%7Bi%3D1%7D%5E%7BN%7D%5B%28i-1%29a_%7Bi-1%7D%20&plus;%20%28n-i%29a_%7BN-i%7D%5D%29%20%3D%201%20&plus;%20%5Cfrac%7B2%7D%7BN%20*%20N%7D%5Csum_%7Bi%3D1%7D%5E%7BN%7D%28i-1%29a_%7Bi-1%7D%20%3D%201%20&plus;%20%5Cfrac%7B2%7D%7BN%20*%20N%7D%5Csum_%7Bi%3D1%7D%5E%7BN%20%3D%201%7Dia_i)


Из последнего выражения следует:

![](https://latex.codecogs.com/svg.latex?%5Clarge%20%281%29%20a_N%20%3D%201%20&plus;%20%5Cfrac%7B2%7D%7BN%20*%20N%7D%5Csum_%7Bi%3D1%7D%5E%7BN%20%3D%201%7Dia_i%20%3D%201%20&plus;%20%5Cfrac%7B2%7D%7BN%20*%20N%7D%28N-1%29a_%7BN-1%7D%20&plus;%20%5Cfrac%7B2%7D%7BN%20*%20N%7D%5Csum_%7Bi%3D1%7D%5E%7BN%20%3D%202%7Dia_i)

![](https://latex.codecogs.com/svg.latex?%5Clarge%20%282%29%20a_%7BN-1%7D%20%3D%201%20&plus;%20%5Cfrac%7B2%7D%7B%28N-1%29%20*%20%28N-1%29%7D%5Csum_%7Bi%3D1%7D%5E%7BN%20%3D%202%7Dia_i) умножим на  ![](https://latex.codecogs.com/svg.latex?%5Clarge%20%28%28N-1%29/N%29%5E2)

![](https://latex.codecogs.com/svg.latex?%5Clarge%20%283%29%5Cfrac%7B2%7D%7BN%20*%20N%7D%5Csum_%7Bi%3D1%7D%5E%7BN%20%3D%202%7Dia_i%20%3D%28%5Cfrac%7BN-1%7D%7BN%7D%29%5E2%28a_%7BN-1%7D-1%29) подставим (3) в (1)

![](https://latex.codecogs.com/svg.latex?%5Clarge%20%284%29a_N%20%3D%20%5Cfrac%7B2%7D%7BN%20*%20N%7D%28%28N%5E2-1%29a_%7BN-1%7D%20&plus;%202N%20-1%29)

Отсюда можно получить (проверяется подстановкой):

![](https://latex.codecogs.com/svg.latex?%5Clarge%20a_N%20%3D%202%5Cfrac%7BN&plus;1%7D%7BN%7DH_N-3%2C%20H_N%20%3D%201%20&plus;%20%5Cfrac%7B1%7D%7B2%7D%20&plus;%20%5Cfrac%7B1%7D%7B3%7D%20&plus;%20%5Cdots%20&plus;%20%5Cfrac%7B1%7D%7BN%7D)

![](https://latex.codecogs.com/svg.latex?%5Clarge%20H_N%20%3D%20%5Cgamma%20&plus;%20lnN%20&plus;%20%5Cfrac%7B1%7D%7B12N%5E2%7D%20&plus;%20%5Cdots) (формула Эйлера, ![](https://latex.codecogs.com/svg.latex?%5Clarge%20%5Cgamma%20%5Ccong%200%2C577))

![](https://latex.codecogs.com/svg.latex?%5Clarge%20%28N%20%3E%3E%201%29%20%5CRightarrow%20a_N%20%5Ccong%202%5BlnN%20&plus;%20%5Cgamma%5D%20-%203%20%3D%202lnN%20-%20c)

Пусть ![](https://latex.codecogs.com/svg.latex?%5Clarge%20a%5E*_N%20%3D%20log_2N) есть средняя длина пути для идеально сбалансированного дерева

![](https://latex.codecogs.com/svg.latex?%5Clarge%20%5Clim_%7Bn%20%5Cto%20%5Cinfty%7D%20%5Cfrac%7Ba_N%7D%7Ba%5E*_N%7D%20%3D%20%5Cfrac%7B2lnN%7D%7Blog_2N%7D%20%3D%202ln2%20%3D%201%2C386)
