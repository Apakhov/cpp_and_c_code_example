Гипердром – это строка, из букв которой можно составить палиндром. Другими словами, любая буква имеет чётное количество вхождений (возможно, нулевое) в гипердром чётной длины. Если же гипердром имеет нечётную длину, то ровно одна буква имеет нечётное количество вхождений.

Составьте программу rangehd.c, определяющую, является ли указанная подстрока строки гипердромом. Строка время от времени может изменяться.
Формат входных данных

Первая строчка, считываемая со стандартного потока ввода, содержит строку размера n (0 < n ≤ 1000000). Строка состоит из маленьких латинских букв.

Вторая строчка содержит общее количество выполняемых операций m (0 < m ≤ 10000). Каждая из следующих m строчек содержит описание операции.

Операция либо имеет форму HD l r (определить, является ли подстрока, начинающаяся с индекса l и заканчивающаяся индексом r, гипердромом), либо форму UPD i s (заменить подстроку, начинающуюся с индекса i, строкой s).

Формат результата работы программы

Для каждой операции HD вывести в стандартный поток вывода слово «YES», если подстрока является гипердромом, или слово «NO» в противном случае.

Пример работы программы:
 

Входные данные|
--------------|
6             |
HD 0 6        |
HD 1 6        |
HD 0 3        |
UPD 2 qqq     |
HD 0 6        |
HD 1 5        | 
---------------

 Выходные данные|
----------------|
YES             |
NO              |
NO              |
NO              |
YES             |