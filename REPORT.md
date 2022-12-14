# Отчет по лабораторной работе №1
## Работа со списками и реляционным представлением данных
## по курсу "Логическое программирование"

### студент: Стенин К.А.

## Результат проверки

| Преподаватель  | Дата | Оценка |
| -------------- | ---- | ------ |
| Сошников Д.В.  |      |        |
| Левинская М.А. |      |        |

> *Комментарии проверяющих (обратите внимание, что более подробные комментарии возможны непосредственно в репозитории по тексту программы)*


## Введение
Для работы со списками в императивных языках используются итераторы, а сам список может содержать элементы лишь одного типа - целый, вещественный или символьный. Список же в Прологе - рекурсивная структура в виде набора значений, которую можно представить в виде дерева. Список в Прологе может содержать элементы любого типа, задаётся он головой остальным списком (элементом и хвостом). Можно сравнить список в Прологе с массивами в других языках программирования

## Задание 1.1: Предикат обработки списка

`remo_end_3(L, R)` - удаление последних трёх элементов списка c использованием стандартных предикатов
`not_stand_rem([_],[])` - удаление последних трёх элементов списка без использования стандартных предикатов

Примеры использования:
```prolog
?- remo_end_3([fff, 43, tnh, 685, 3.8, rlyry, 53536], X).
X = [fff, 43, tnh, 685] .

?- not_stand_rem([fff, 43, tnh, 685, 3.8, rlyry, 53536], [fff, 43, tnh, 685]).
true.

?- not_stand_rem([456, wfi, et], X).
X = [].
```

Реализация:
```prolog
remo_end_3(L, R):-append(R, X, L), X = [_,_,_].
```
С помощью стандартного предиката append объединяем исходный список и список, состоящий из трёх пустых элементов, тем самым затирая последние три элемента в исходном списке.

```prolog
not_stand_rem([_],[]) :- !.
not_stand_rem([_,_],[]) :- !.
not_stand_rem([_,_,_],[]) :- !.
not_stand_rem([H|T],[H|Q]) :- not_stand_rem(T,Q).
```
С помощью рекурсивного отсекания т.н. "головы" мы убираем каждый раз по одному элементу из начала. Затем у нас остаются три элемента в конце, которые мы заменяем на пустой список, т.е. стираем.

## Задание 1.2: Предикат обработки числового списка

`middle(L,A)` - нахождение среднего арифметического элементов списка

Примеры использования:
```prolog
?- middle([1,2,3,4,5], X).
X = 3.

?- middle([1,2,8, 212], X).
X = 55.75.

?- middle([1], X).
X = 1.

?- middle([1,2,3,4], 2.5).
true.
```

Реализация:
```prolog
sum([], 0).
sum([H|T], S) :-sum(T, Tail), 
S = Tail + H.
middle(L,A):-sum(L,S), 
length(L,K), 
A is S/K.
```
C помощью вспомогательного предиката sum находится сумма всех элементов списка, затем с помощью стандартного предиката length находим длину и делим первое на второе, получая среднее арифметическое.

## Задание 2: Реляционное представление данных
Хорошая сторона вопроса - доступ к списку оценок за все предметы или к информации о группе мы получаем за О(1).
Плохая сторона - доступ к оценкам уже за О(n).

`student_passed(X)` - Х - фамилия студента. Предикат истинен, если студент сдал все экзамены на 3 балла и выше, и ложен, если студент не сдал хотя бы один экзамен. Рекурсивно просматривается список оценок студента по всем предметам. 

`mark(G, X, Y)` - G - группа студента, Х - фамилия студента, Y - средний балл студента по всем предметам.

Рекурсивно просматриваются оценки студента по всем предметам, затем суммируются, а потом полученное число делится на количество предметов(6).

`not_passed(X, Y)` - Y - количество студентов, получивших оценку 2 по предмету Х. Создается общий список, содержащий списки из оценок всех студентов по всем предметам. Рекурсивно проверяется, содержится ли в голове списка предмет, по которому получена оценка 2 - если содержится, то Y увеличивается на 1, если нет, то просматривается хвост общего списка.

`max_mark_students(G, L)` - в группе G ищутся студенты, имеющие максимальный средний балл в ней. L - список фамилий этих студентов. Ищется максимальный средний балл в данной группе, после чего ищутся студенты этой группы, имеющие такой средний балл.

## Выводы

Эта лабораторная работа - мой первый опыт написания программ на Прологе. Я узнал о реализации многих базовых предикатов этого языка, о списках в Прологе и предикатах работы с ними. Эта работа дала мне возможность узнать основы логического программирования и удивительного языка Пролог. Верите вы мне или нет, но я даже захотел почитать побольше об этом языке, узнать побольше о методике его работы. Мне кажется, что расширение сознания, о котором нам говорил преподаватель уже пошло.)
