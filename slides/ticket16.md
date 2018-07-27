# Экзаменационный билет №16

## 1.Адаптивная оценка параметров модели в ходе выполнения программ (на примере системы управления несколькими стеками)

- Пусть ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Csigma) есть число перепаковок памяти за некоторый отрезок времени ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5CDelta%20t)
- Величина ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Csigma) зависит от ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Ctheta) и для повышения эффективности функционирования системы следует определить такое ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Ctheta), чтобы число перепаковок было минимально, т.е. ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Cmin_%7B%5Ctheta%7D%20%5Csigma%20%28%5Ctheta%29)

<!-- ![](../pictures/ticket16-1.png) -->

Схема определения оптимального значения ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Ctheta):
- Выполняется оценка величины ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Csigma) на последовательных друг за другом отрезках времени ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5CDelta%20t)

![](../pictures/ticket16-1.png)

- Определяется величина изменения числа выполненных перепаковок: ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5CDelta%5Csigma%20%3D%20%5Csigma%27%20-%20%5Csigma)
- Применяется следующее правило корректировки значения ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Ctheta)

![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5Ctheta%20%3D%20%5Cleft%5C%7B%5Cbegin%7Bmatrix%7D%20%5Ctheta%20&plus;%20%5CDelta%5Ctheta%2C%20%5CDelta%5Csigma%20%5Cleq%200%20%5C%5C%20%5Ctheta%20-%20%5CDelta%5Ctheta%2C%20%5CDelta%5Csigma%20%3E%200%20%5Cend%7Bmatrix%7D%5Cright.)

где ![](http://latex.codecogs.com/svg.latex?%5Clarge%20%5CDelta%5Ctheta) - параметр схемы адаптации

## 2. Оценка сложности обработки деревьев поиска. Понятие сбалансированных и идеально сбалансированных деревьев поиска

**Идеально сбалансированное дерево** - дерево, у которого для каждого его узла количество узлов в левом и правом поддеревьях различаются не более чем на 1.

**Сбалансированное дерево** - дереао, у которого для каждого узла высота левого и правого поддеревьев различаются не более,чем на 1(АВЛ-деревья).

Идеально сбалансированные деревья являются сбалансированными.
Операции обработки сбалансированных деревьев имеют **сложность** log2N.(поиск, вставка, удаление)

![](https://latex.codecogs.com/svg.latex?%5Clarge%20T_%7Bmin%7D%20%3D%201)
![](https://latex.codecogs.com/svg.latex?%5Clarge%20T_%7Bmax%7D%3Dlog2N) (при сбалансированном дереве)
![](https://latex.codecogs.com/svg.latex?%5Clarge%20T_%7Bmax%7D%3DN) (при вырожденном дереве)

- Пусть даны N различных ключей со значениями 1,...N и появление любого ключа равновероятно.
- Пусть первый ключ равен i. Левое поддерево будет содержать (i - 1) узлов, правое поддерево - (n - i) узлов.
![](http://latex.codecogs.com/svg.latex?%5Clarge%20a_N%20%3D%20%5Cfrac%7B1%7D%7BN%7D%20%5Csum_%7Bi%3D1%7D%5EN%20a%5Ei_N) - средняя длина пути дерева с N узлами,
где ![](http://latex.codecogs.com/svg.latex?%5Clarge%20a%5Ei_N) - средняя длина пути в дереве, в котором корень равен i.

![](http://latex.codecogs.com/svg.latex?%5Clarge%20a%5Ei_N%20-%20%28a_%7Bi-1%7D%20&plus;%201%29%5Cfrac%7Bi-1%7D%7BN%7D%20&plus;%201%5Cfrac%7B1%7D%7BN%7D%20&plus;%20%28a_%7BN-i%7D&plus;1%29%5Cfrac%7BN-1%7D%7BN%7D)

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
