# Экзаменационный билет №15

## 1.Изменение структуры текста (вставка и удаление строк)

```C++
void TText::DelDownLine(void) // Удаление строки в подуровне
{
   if (pCurrent == nullptr)
       SetRetCode(TextErr);
   else if (pCurrent->pDown == nullptr)
       SetRetCode(TextNoDown);
   else if (pCurrent->pDown->IsAtom())
       pCurrent->pDown = pCurrent->pDown->pNext;
}

void TText::InsDownLine(string str) // Вставка строки в подуровень
{
   if (pCurrent == nullptr)
       SetRetCode(TextErr);
   else
   {
       TStr buf; // typedef char TStr[TextLineLength];
       strcpy(buf, str.c_str());
       pCurrent->pDown = new TTextLink(buf, pCurrent->pDown, nullptr);
   }
}
```

## 2. Деревья поиска. Алгоритм удаления.

`ПИКЧИ`
