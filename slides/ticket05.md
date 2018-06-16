# Экзаменационный билет №5

## 1. Представление множества битовой строкой. Оценки сложности по памяти и времени.

<!-- TODO:
- Add more info -->

**Ничего нет (может есть в методичке)**

## 2. Реализация стека с использованием динамически распределяемой памяти.

### Вставка в стек

```C++
    PTDatLink pTemp;
    pTemp = new TDatLink();
    pTemp-> SetDatValue(Val);
    pTemp->SetNextLink(pFirst);
    pFirst = pTemp;
```

### Выборка из стека

```C++
    PTDatLink pTemp = pFirst;
    Val = pFirst->GetDatValue();
    pFirst = pFirst->GetNextLink();
    delete pTemp;
```
