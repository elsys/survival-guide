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

## Потребителски функции

В езикът C могат да се дефинират собствени функции. Тази свобода увеличава експресивността на езика в пъти и позволява на програмиста да гради необходимите абстракции за решаване на сложни проблеми, като му позволява да раздели и изолира отделните части на една система в малки функции с конкретна задача, за които да разсъждава по-лесно. Добре дефинираните функции гарантират коректност за всяка стъпка от алгоритъма за решаване на даден проблем и служат като основа на по-сложни функции.

## Дефиниция на функция

Дефинирането на една функция става по следния начин:

```c
return_type function_name(type1 argname1, type2 argname2) {
   // body of the function
}
```

Нека дефинираме функция, която връща квадратът на едно цяло число:

```c
int square(int number) {
    return number * number;
}
```

Тази дефиниция указва:

* името на функцията - `square`
* входните параметри - в сличая само един, от тип `int,` наречен `number`
* типът на резултата - `int`
* кодът, който се изпълнява при извикването на функцията

Да добавим `main` функцията и да компилираме:

```c
#include <stdio.h>

int square(int number) {
    return number * number;
}

int main() {
    printf("%d squared is %d\n", 5, square(5));
    return 0;
}
```

И в терминала:

```bash
$ gcc -Wall -pedantic -std=c11 square.c
$ ./a.out
5 squared is 25
```

### Извикване на функция

Нека разгледаме следната функция:

```c
float safe_divide(float numerator, float denumerator) {
    if (denumerator == 0.0) {
        return 0.0;
    }
    return numerator / denumerator;
}
```

Резултатът на тази функция представлява резултата от делението на две числа, ако делителят е различен от нула, или  нула, тъй като деление на 0 е недефинирана операция.

Използването тази функция, още наречено извикване на функция, става чрез:

```c
[type result_variable = ]function(argvalue1, argvalue2);
```

Или конкретно:

```c
float ration = safe_divide(4.0, 3.0); // value of ratio is 1.33333...
```

При извикване на функция е необходимо да се зададат стойности за всеки един входен аргумент на функцията. Тези стойности ще бъдат използвани при изчисляване на резултата на функцията. В горния пример присвояваме резултата от извикване на функцията в променливата `ration`.

> Може да извикаме горната функция и без да вземем резултата й.
>
> ```c
> safe_divide(4.0, 3.0);
> ```
>
> Това ще изпълни кода на функцията, но ще игнорира резултата й. Ако тази функция има странични ефекти \(като например да принтира нещо на екрана\) те ще бъдат изпълнени.

Едно от полезните неща при функциите е, че можем да ги извикваме с различни входни параметри.

```c
#include <stdio.h>

float safe_divide(float numerator, float denumerator) {
    if (denumerator == 0.0) {
        return 0.0;
    }
    return numerator / denumerator;
}

int main() {
    float inputs[] = {3.14, 2.71, 42};
    float outputs[3];

    for(int i = 0; i < 3; i++) {
        outputs[i] = safe_divide(inputs[i], 10); // result saved in array with same index
    }

    for(int i = 0; i < 3; i++) {
        printf("%f ", outputs[i]);
    }
    printf("\n");
    return 0;
}
```

```
$ gcc -Wall -pedantic -std=c11 safe_divide.c 
$ ./a.out 
0.314000 0.217000 4.200000
```

### Тяло на функцията

Тялото на функцията е парчето код, което ще се изпълни когато извикаме функцията. В тялото на функцията можем:

* да дефинираме нови променливи \(наречени локални променливи на функцията\)
* извършваме операции – присвояване на стойности, сумиране, изваждане, умножение, и т.н., както и извикване на други функции
* да върнем стойност използвайки служебната дума `return`

Обикновено в тялото на функцията извършваме необходимите стъпки за да получим резултата на функцията и да го върнем използвайки `return`.

При изпълнение на функция ако се достигне до `return`, то изпълнението на функцията приключва и се продължава изпълнението на програмата от мястото, където е била извикана функцията.

```c
#include <stdio.h>

int loopy() {
    for(int i = 0; i < 10; i++) {
        for(int j = 0; j < 10; j++) {
            if (i == 5 && j == 5) { // after some iterations this will be true
                printf("Reached the return, exiting\n");
                return 4;
                printf("unreachable code!!");
            }
        }
    }
    return 2; // never reached
}

int main() {
    printf("Before loopy\n");
    int result = loopy();
    printf("After loopy, result is %d\n", result);
    return 0;
}
```

```bash
$ gcc -Wall -pedantic -std=c11 loopy.c
$ ./a.out 
Before loopy
Reached the return, exiting
After loopy, result is 4
```

### Няколко аргумента

Когато функцията приема няколко аргумента, то при нейното извикване стойностите трябва да бъдат подадени в същия ред, в който са били дефинирани. Да разгледаме следния пример:

```c
#include <stdio.h>

float clamp(float min, float max, float f) {
    if (f < min) {
        return min;
    }
    if (f > max) {
        return max;
    }
    return f;
}

int main() {
    float min = 1.0;
    float max = 3.14;
    float input;
    scanf("%f", &input);

    float clamped = clamp(1.0, 3.14, input);

    printf("%f clamped is %f\n", input, clamped);
    return 0;
}
```

```bash
$ gcc -Wall -pedantic -std=c11 clamp.c
$ ./a.out
20
20.000000 clamped is 3.140000
```

При изпълнение на функцията `clamp` стойността на `min` ще е 1.0, `max` ще е 3.14, a `f` ще има стойност, каквато потребителят е въвел от клавиатурата – в случая 20.

Аргументите на една функция могат да имат различни типове, като тогава при извикването й трябва типовече на входните стойности да съвпадат.

```c
void fun(int i, float f, char c) { /* function body */ }
```

```c
fun(2, 2.17, 'H');
```

> void е специален тип, който може да се използва за тип на върнатата стойност и той указва, че функцията не връща нищо. Във void функциите можем да използваме командата return; без стойност за да прекратим изпълнението.

## Декларация на функция

Нека опитаме да компилираме следната програма:

```c
#include <stdio.h>

int main() {
    greet_person("Gosho");
    return 0;
}

void greet_person(char *name) {
    printf("Hello, %s\n", name);
}
```

Получаваме следния warning когато компилираме:

```bash
$ gcc -Wall -pedantic -std=c11 greet.c 
greet.c: In function ‘main’:
greet.c:4:1: warning: implicit declaration of function ‘greet_person’ [-Wimplicit-function-declaration]
 greet_person("Gosho");
 ^~~~~~~~~~~~
greet.c: At top level:
greet.c:8:6: warning: conflicting types for ‘greet_person’
 void greet_person(char *name) {
      ^~~~~~~~~~~~
greet.c:4:1: note: previous implicit declaration of ‘greet_person’ was here
 greet_person("Gosho");
 ^~~~~~~~~~~~
```

Това предупреждение \(възможно е и да бъде грешка\) се появява, защото се опитваме да използваме функцията greet\_person, преди да сме я декларирали. Когато компилаторът срещне извикването й в main функцията, той не знае как да провери дали входните параметри и зададените стойности за извикването на функцията съвпадат.

> В случая компилаторът все пак успява да намери дефиницията на функцията greet\_person по-надолу в кода и успява да компилира тази програма \(имаме само warning, а не error\). Ако компилираме програма с повече от един файл липсващата декларация ще доведе до компилационна грешка \(ще засегнем темата за работата с няколко файлове по-подробно в главата [Препроцесор](/programming-in-c/c-basics/preprotsesor.md)\).

В този случай е необходимо да напишем декларация.

```c
#include <stdio.h>

void greet_person(char *name); // greet_person declaration

int main() {
    greet_person("Gosho");
    return 0;
}

void greet_person(char *name) {
    printf("Hello, %s\n", name);
}
```

```
$ gcc -Wall -pedantic -std=c11 greet.c 
$ ./a.out
Hello, Gosho
```

Декларацията на функция е в следния формат:

```c
return_type function_name(type1 [argname1], type2 [argname2]);
```

Имената на аргументите при декларация, за разлика от дефиницията, не са задължителни. Също така при декларацията не пишем тялото на функцията – чрез декларацията казваме на компилатора само, че същесвува такава функция и как изглежда тя, не и какво точно прави. Това е достатъчно за да могат да се извършат проверки на типовете и резултата.

> Въпреки че декларациите не са задължителни се счита за добра практика да се пишат винаги. Декларациите ще станат необходими при работа с header файлове, което ще ще разгледаме в следващи глави.

## Упражнение

1. Разгледайте какви аргументи приемат и какво връщат стандартните функции
   1. strcmp
   2. fgets
   3. strncpy
2. Дефинирайте



