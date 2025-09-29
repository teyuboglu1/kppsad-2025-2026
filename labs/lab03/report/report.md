---
## Front matter
title: "Отчет по лабораторной работе №3"
subtitle: "Компьютерный практикум по статистическому анализу данных"
author: "Еюбоглу Тимур, НПИбд-01-22"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: false # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Основная цель работы — освоить применение циклов функций и сторонних для Julia
пакетов для решения задач линейной алгебры и работы с матрицами.

# Выполнение лабораторной работы

## Циклы while и for 

Для различных операций, связанных с перебором индексируемых элементов структур
данных, традиционно используются циклы while и for.

Синтаксис while

``` Julia
while <условие>
    <тело цикла>
end
```

Примеры использования цикла while (рис. [-@fig:001]):

![Примеры использования цикла while](image/01.png){#fig:001}

Такие же результаты можно получить при использовании цикла for.

Синтаксис for

``` Julia
for <переменная> in <диапазон>
    <тело цикла>
end
```

Примеры использования цикла for (рис. [-@fig:002]):

![Примеры использования цикла for](image/02.png){#fig:002}

Пример использования цикла for для создания двумерного массива, в котором значение каждой записи 
является суммой индексов строки и столбца (рис. [-@fig:003]):

![Пример использования цикла for для создания двумерного массива](image/03.png){#fig:003}

## Условные выражения

Довольно часто при решении задач требуется проверить выполнение тех или иных
условий. Для этого используют условные выражения.

Синтаксис условных выражений с ключевым словом:

``` Julia
if <условие 1>
    <действие 1>
elseif <условие 2>
    <действие 2>
else
    <действие 3>
end
```

Примеры использования условного выражения (рис. [-@fig:004]):

![Пример использования условного выражения](image/04.png){#fig:004}

## Функции

Julia дает нам несколько разных способов написать функцию. 

Примеры способов написания функции (рис. [-@fig:005]):

![Примеры способов написания функции](image/05.png){#fig:005}

По соглашению в Julia функции, сопровождаемые восклицательным знаком, изменяют
свое содержимое, а функции без восклицательного знака не делают этого (рис. [-@fig:006]):

![Сравнение результатов вывода](image/06.png){#fig:006}

В Julia функция map является функцией высшего порядка, которая принимает функцию
в качестве одного из своих входных аргументов и применяет эту функцию к каждому
элементу структуры данных, которая ей передаётся также в качестве аргумента.

Функция broadcast — ещё одна функция высшего порядка в Julia, представляющая собой обобщение 
функции map.Функция broadcast() будет пытаться привести все объекты
к общему измерению, map() будет напрямую применять данную функцию поэлементно.

Примеры использования функций map() и broadcast() (рис. [-@fig:007]):

![Примеры использования функций map() и broadcast()](image/07.png){#fig:007}

## Сторонние библиотеки (пакеты) в Julia

Julia имеет более 2000 зарегистрированных пакетов, что делает их огромной частью
экосистемы Julia. Есть вызовы функций первого класса для других языков, обеспечивающие интерфейсы сторонних функций. Можно вызвать функции из Python или R,
например, с помощью PyCall или Rcall.

С перечнем доступных в Julia пакетов можно ознакомиться на страницах следующих
ресурсов:
- https://julialang.org/packages/
- https://juliahub.com/ui/Home
- https://juliaobserver.com/
- https://github.com/svaksha/Julia.jl

При первом использовании пакета в вашей текущей установке Julia вам необходимо
использовать менеджер пакетов, чтобы явно его добавить:

``` Julia
import Pkg
Pkg.add("Example")
```

При каждом новом использовании Julia (например, в начале нового сеанса в REPL
или открытии блокнота в первый раз) нужно загрузить пакет, используя ключевое слово
using:

Например, добавим и загрузим пакет Colors:

``` Julia
Pkg.add("Colors")
using Colors
```

Затем создадим палитру из 100 разных цветов:

``` Julia
palette = distinguishable_colors(100)
```

А затем определим матрицу 3 × 3 с элементами в форме случайного цвета из палитры,
используя функцию rand:

``` Julia
rand(palette, 3, 3)
```

Пример использования сторонних библиотек (рис. [-@fig:008]):

![Пример использования сторонних библиотек](image/08.png){#fig:008}

## Самостоятельная работа

Выполнение задания №1 (рис. [-@fig:009] - рис. [-@fig:012]):

![Выполнение задания №1](image/09.png){#fig:009}

![Выполнение задания №1](image/10.png){#fig:010}

![Выполнение задания №1](image/11.png){#fig:011}

![Выполнение задания №1](image/12.png){#fig:012}

Выполнение задания №2 (рис. [-@fig:013]):

![Выполнение задания №2](image/13.png){#fig:013}

Выполнение задания №3 (рис. [-@fig:014]):

![Выполнение задания №3](image/14.png){#fig:014}

Выполнение задания №4 (рис. [-@fig:015]):

![Выполнение задания №4](image/15.png){#fig:015}


Выполнение задания №5 (рис. [-@fig:016]):

![Выполнение задания №5](image/16.png){#fig:016}

Выполнение задания №6 (рис. [-@fig:017]):

![Выполнение задания №6](image/17.png){#fig:017}

Выполнение задания №7 (рис. [-@fig:018] - рис. [-@fig:019]):

![Выполнение задания №7](image/18.png){#fig:018}

![Выполнение задания №7](image/19.png){#fig:019}

Выполнение задания №8 (рис. [-@fig:020] - рис. [-@fig:022]):

![Выполнение задания №7](image/20.png){#fig:020}

![Выполнение задания №7](image/21.png){#fig:021}

![Выполнение задания №7](image/22.png){#fig:022}

Выполнение задания №9 (рис. [-@fig:023]):

![Выполнение задания №9](image/23.png){#fig:023}

Выполнение задания №10 (рис. [-@fig:024] - рис. [-@fig:025]):

![Выполнение задания №10](image/24.png){#fig:024}

![Выполнение задания №10](image/25.png){#fig:025}

Выполнение задания №11 (рис. [-@fig:026]):

![Выполнение задания №9](image/26.png){#fig:026}

# Вывод

В ходе выполнения лабораторной работы было освоено применение циклов функций и сторонних для Julia
пакетов для решения задач линейной алгебры и работы с матрицами.

# Список литературы. Библиография

[1] Julia Documentation: https://docs.julialang.org/en/v1/
