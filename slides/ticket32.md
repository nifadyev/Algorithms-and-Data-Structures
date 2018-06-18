# Экзаменационный билет №32

## 1.Комбинирование геометрических объектов (плексы).

# `НЕТУ ЧОТА`

## 2. Реализация алгоритма обхода графа.

Алгоритмы обхода (итератор)

```C++
TSearchMode; // способ обхода
PTGraphNode pCurrNode; // текущая вершина
// Достигнутые, но не обработанные вершины
TDataRoot *pStream;
// Множество вершин, достигнутых в ходе обхода
TBitField *pFound;
```

**Инициализация `(Reset)`**

- Инициализация структур
- Вставка первой вершины в поток `pStream` и ее отметка в множестве `pFound`
- Выполнение метода `GoNext`

**Проверка завершения `(IsGraphEnded)`**

```C++
return pCurrNode == NULL // тукущее звено?
```

**Переход к следующей вершине графа `(GoNext)`**

- Получить вершину из потока `pStream`
- Поместить смежные вершины, если они еще остались не достигнуты, в поток `pStream`
- Отметить смежные вершины в множестве pFound

```C++
    int Reset (void); // установить на первую вершину
    int IsGraphEnded (void) const; // обход завершен?
    int GoNext (void); // переход к следующей вершине
    PTGraphNode GetCurrNode (void) { return pCurrNode; } // доступ
    PTGraphPath GetShortestPath (string fn, string ln); // поиск кратчайшего пути
protected:
    virtual void Print (ostream &os); // печать графа
};
typedef TGraph * PTGraph;
// end of tgraph.h
```
