# Экзаменационный билет №31

## 1.Конструирование геометрических объектов.

**Геометрический объект** может быть сконструирован с использованием уже существующих объектов

- например, ломаная может быть определена через набор конечных точек составляющих отрезков

```C++
class TChartPolyline : public TChartGroup
{
 public:
    TChartPolyline() { }
    void InsPoint(TChartRoot *pUnit);  // Добавление
    virtual void Show();  // Визуализация
    virtual void Hide();  // Скрытие
    virtual void CalcParams(double t = -1);  // Пересчет параметров
};
```

## 2. Алгоритмы обхода графов. Поиск в ширину.

![](../pictures/ticket31-1.jpg)

![](../pictures/ticket31-2.jpg)
