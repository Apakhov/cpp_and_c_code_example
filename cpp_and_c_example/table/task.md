Считается, что в конце 70-х годов персональные компьютеры приобрели популярность в немалой степени благодаря так называемым электронным таблицам, позволяющим автоматизировать несложные расчёты. В некотором смысле, в то время электронная таблица была единственной программой, способной приносить обладателю персонального компьютера реальную пользу.

Электронные таблицы широко используются и в наше время (например, Microsoft Excel или LibreOffice Calc). Данные в электронной таблице представляются в виде матрицы, в ячейках которой располагаются значения и формулы. При этом в качестве переменных в формулах фигурируют ссылки на другие ячейки таблицы. Вычисление значений ячеек, заданных формулами, происходит всякий раз, когда изменяются значения ячеек, на которые эти формулы ссылаются.

Рассмотрим эскиз электронной таблицы на языке C++.

Оформим нашу электронную таблицу в виде шаблона класса под названием SuperCalc, параметризованного типом значения, которое может содержаться в ячейке таблицы. Размеры таблицы m×n

будут передаваться конструктору этого класса в качестве параметров, а доступ к отдельным ячейкам таблицы будет предоставлять перегруженная операция «()»:

```c++
template <class T>
class SuperCalc {
public:
    SuperCalc(int m, int n); 
    Cell<T>& operator() (int i, int j);
};
```
Здесь Cell\<T\> – это некоторый класс, который будет представлять ячейку таблицы.

Будет прекрасно, если нам удастся организовать работу с нашей электронной таблицей наиболее естественным образом. Например, запись значения типа T в ячейку таблицы лучше всего оформить в виде присваивания значения этой ячейке:

```c++
SuperCalc<int> table(10, 10);
table(2, 3) = 100;
```

Более того, запись формулы в ячейку было бы неплохо тоже организовать через присваивание этой ячейке выражения, определяющего формулу. Например:
```c++
table(0, 0) = (table(0, 1) + table(0, 2))/2;
```
Отметим исключительно важный момент: присваивание выражения ячейке не должно означать запись в ячейку результата вычисления выражения! Объект класса Cell<T> должен запоминать формулу и выполнять вычисления только тогда, когда его об этом попросят. Кстати, получение значения ячейки можно оформить через приведение её к типу T. Например:
```c++
cout << (int)table(0, 0) << endl;
```
Реализуйте приведённый выше эскиз в виде заголовочного файла supercalc.hpp. Работоспособность шаблона класса SuperCalc будет проверяться сервером на примерах следующего вида:
```c++
#include <iostream>
#include "supercalc.hpp"

using namespace std;

int main()
{
    SuperCalc<int> sc(1, 11);
    
    // sc(0, 10) -- сумма ячеек с sc(0, 0) до sc(0, 9)
    sc(0, 10) = 0;
    for (int i = 0; i < 10; i++) {
        sc(0, 10) += sc(0, i);
    }
    
    // Ввод ячеек sc(0, 0) ... sc(0, 9)
    for (int i = 0; i < 10; i++) {
        int x;
        cin >> x;
        sc(0, i) = x;
    }
    
    // Вывод суммы 
    cout << (int)sc(0, 10) << endl;
    return 0;
}
```

Формулы, запоминаемые в ячейках таблицы, могут содержать значения типа T, ссылки на ячейки, знаки четырёх арифметических операций и унарный минус.

Гарантируется, что в примерах не будут создаваться циклические зависимости между ячейками. Кроме того, в вычислениях не будут участвовать ячейки, в которые предварительно не было записано какое-нибудь значение.