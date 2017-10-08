# Функции в C

---

Функциите в езика C биват два вида - стандартни функции \(идващи от стандартната библотека[^1] на C\) и функции, дефинирани от потребителите.

## Стандартни функции

Стандартът за C дефинира набор от функции, които идват заедно с компилатора и мога да бъдат използвани от програмистите наготово. Това са например:

* функциите свързани с работа със символни низове, дефинирани в хедъра `<string.h>` - `strlen`, `strcpy`, `strcmp` и други
* от `<stdio.h>`, за работа с вход/изход - `scanf`, `printf`, `fgets` и други.
* математическите функции от `<math.h>`

и други.

Нека разгледаме функцията `strlen` чрез командата man.

```bash
$ man strlen
STRLEN(3)                      Linux Programmer's Manual                      STRLEN(3)

NAME
       strlen - calculate the length of a string

SYNOPSIS
       #include <string.h>

       size_t strlen(const char *s);

DESCRIPTION
       The  strlen()  function  calculates  the  length  of the string pointed to by s,
       excluding the terminating null byte ('\0').

RETURN VALUE
       The strlen() function returns the number of characters in the string pointed  to
       by s.
[ ... ]
```

В тази страница можем да видим декларацията й:

```c
size_t strlen(const char *s);
```

Виждаме, че функцията `strlen` приема указател към символен низ \(масив от чар-ове\), и връща стойност от тип size\_t.

> Типът size\_t е дефинират \(чрез typedef\) да бъде цяло число без знак в стандартната библотека &lt;stddef.h&gt;

## Как да дефинираме функция?



## Упражнение

1. Разгледайте какви аргументи приемат и какво връщат стандартните функции
   1. strcmp
   2. fgets
   3. strncpy
2. 
[^1]: [https://www.tutorialspoint.com/c\_standard\_library/index.htm](https://www.tutorialspoint.com/c_standard_library/index.htm)

