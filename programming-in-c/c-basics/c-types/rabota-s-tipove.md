# Работа с типове и променливи

## Присвояване на стойности

Използваме операторът равно \(=\) като от лявата страна седи променливата, а от дясната стойността

```c
char* sentence = "Survival Guide FTW!";
```

## Аритметични операции и асоциативност

Ще разгледаме основните математически операции поддържани от всички числени типове в С. Те са:

* Събиране
* Изваждане
* Умножение
* Целочислено деление
* Деление с остатък

```c
int evil_number = 666;
int ultimate_answer = 42;
int result = 0;

// add
result = evil_number + ultimate_answer;

// subtract
result = evil_number - ultimate_answer;

// multiply
result = evil_number * ultimate_answer;

// mod
result = evil_number % ultimate_answer;

// devide
result = evil_number / ultimate_answer;
```

В случая на деление на две числа, има особеност - резултата в който пишем делението е целочислен тип, затова компилатора ще загръгли и ще отреже дропбната част. За да получим резултат с дробна част, трябва да го запишем в променлива от тип число с плаваща запетая.

```c
float accured_result = evil_number / ultimate_answer;
```

Сега получаваме резултат **`15.000000`**, който явно не е верен, това се дължи на факта, че делим две целочислени числа. Резултатът пак ще е целочислено число, но записано във променлива от тип `float` - дробната част се изпуска, отново.

```c
float accured_result = evil_number / (float) ultimate_answer;
```

### Асоциативност



