- title : FsReveal
- description : Введение в FsReveal
- author : Зайнуллин Фархад
- theme : white
- transition : default

***

# FsReveal
## Введение

Зайнуллин Фархад

tg: @Kleidemos

***

### Что есть FsReveal? 

- Генерирует презентации на [reveal.js](http://lab.hakim.se/reveal-js/#/) из [markdown](http://daringfireball.net/projects/markdown/)
- Использует [FSharp.Formatting](https://github.com/tpetricek/FSharp.Formatting) для разбора markdown файлов

***
### Reveal.js

- Фреймворк для легкой генерации визуально привлекательных презентаций **на HTML**.

> **Atwood's Law**: any application that can be written in JavaScript, will eventually be written in JavaScript.

---

##### Минимальный пример рабочей презентации на Reveal.js

```html
<html>
	<head>
		<link rel="stylesheet" href="css/reveal.css">
		<link rel="stylesheet" href="css/theme/white.css">
	</head>
	<body>
		<div class="reveal">
			<div class="slides">
				<section>Slide 1</section>
				<section>Slide 2</section>
			</div>
		</div>
		<script src="js/reveal.js"></script>
		<script>
			Reveal.initialize();
		</script>
	</body>
</html>
```

---

##### Дерево слайдов

```html
<div class="reveal">
	<div class="slides">
		<section>Single Horizontal Slide</section>
		<section>
			<section>Vertical Slide 1</section>
			<section>Vertical Slide 2</section>
		</section>
	</div>
</div>
```

---

##### Markdown

```html
<section data-markdown>
	<textarea data-template>
		## Page title

		A paragraph with some text and a [link](http://hakim.se).
	</textarea>
</section>
```

***

### FSharp.Formatting

1. Берет fsx или md файлы.
1. Творит магию.
1. Выдает HTML / LaTeX файлы.
1. Могет в подсветку синтаксиса и вывод типов для HTML.

---

#### Markdown

```markdown
# First-level heading

    [hide]
    let print s = printfn "%s" s

Some more documentation using `Markdown`.

    [module=Hello]
    let helloWorld() = print "Hello world!"

## Second-level heading
With some more documentation

    [lang=csharp]
    Console.WriteLine("Hello world!");
```

---

#### F# Script

```fs
(**
# First-level heading
Some more documentation using `Markdown`.
*)

(*** include: final-sample ***)

(** 
## Second-level heading
With some more documentation
*)

(*** define: final-sample ***)
let helloWorld() = printfn "Hello world!"
```

---

# Магия

---

HTML или LaTex

---

#### А еще:

* Выполнение кода и использование результата.
* Собственные обработчики деревьев.
* Работа с обычным md.
* Подсветка и подсказки:
    * Больше для fsx.
    * Меньше для md.

---
- data-background : images/tooltips.gif

![](images/tooltips.gif)

***

### Что было сделано

_Приблизительно_

1. Выяснили, что жрет Reveal.Js.
1. Научили FSharp.Formatting генерировать соответствующую структуру.
1. Научили FSharp.Formatting обрабатывать конфиги.
1. Научили Reveal.Js использовать FSharp.Formatting для анализа F#.
1. Автоматизировали генерацию презентаций.
1. Написали сервер для realtime представления.
1. Собрали все в один проект для упрощенной работы.


---

- data-background: images/coincidence.jpg
- data-background-repeat: repeat
- data-background-size : 400px

![](images/FsRevealScheme.png)


***

### Подсветка синтаксиса

#### F# 

    let a = 5
    let factorial x = [1..x] |> List.reduce (*)
    let c = factorial a

_С подсказками._

---

#### C# 

    [lang=cs]
    using System;

    class Program
    {
        static void Main()
        {
            Console.WriteLine("Hello, world!");
        }
    }

_Здесь и далее без подсказок_

---

#### JavaScript

    [lang=js]
    function copyWithEvaluation(iElem, elem) {
        return function (obj) {
            var newObj = {};
            for (var p in obj) {
                var v = obj[p];
                if (typeof v === "function") {
                    v = v(iElem, elem);
                }
                newObj[p] = v;
            }
            if (!newObj.exactTiming) {
                newObj.delay += exports._libraryDelay;
            }
            return newObj;
        };
    }


---

#### Haskell

    [lang=haskell]
    recur_count k = 1 : 1 : zipWith recurAdd (recur_count k) (tail (recur_count k))
            where recurAdd x y = k * x + y

    main = do
      argv <- getArgs
      inputFile <- openFile (head argv) ReadMode
      line <- hGetLine inputFile
      let [n,k] = map read (words line)
      printf "%d\n" ((recur_count k) !! (n-1))

*code from [NashFP/rosalind](https://github.com/NashFP/rosalind/blob/master/mark_wutka%2Bhaskell/FIB/fib_ziplist.hs)*

---

### SQL

    [lang=sql]
    select *
    from
    (select 1 as Id union all select 2 union all select 3) as X
    where Id in (@Ids1, @Ids2, @Ids3)

*sql from [Dapper](https://code.google.com/p/dapper-dot-net/)*

---

### LaTeX

**Bayes' Rule**

$ \Pr(A|B)=\frac{\Pr(B|A)\Pr(A)}{\Pr(B|A)\Pr(A)+\Pr(B|\neg A)\Pr(\neg A)} $

```LaTeX
$ \Pr(A|B)=\frac{\Pr(B|A)\Pr(A)}{\Pr(B|A)\Pr(A)+\Pr(B|\neg A)\Pr(\neg A)} $
```

***

## Демки

---

### Первая загрузка проекта

Вбиваем [fsreveal](https://yandex.ru/search/?text=fsreveal) в ближайшем поисковике.

---

### Куда писать

---

### Куда рыть

***

### Что дальше?

---

### Использовать
#### С нуля

* Мелкие ненормированные презентации
* Есть код на F#
* Много кода на поддерживаемых языках

---

#### После допиливания

* Несильно нормированные презентации
* Чудовищно много кода

---

### Развивать
#### Что?

* DSL для основных фич Reveal.Js
* Сложные методы взаимодействия
    * Синхронизация на всех устройствах
    * Контроль доступа
    * Параллельные группы вертикальных слайдов
    * И т.д.

---
* data-background : lightgrey

#### Как?

```md
---
* data-background : lightgrey

### Слайд на светло сером фоне
---
```

***

### Спасибо за внимание

***

### Вопросы?