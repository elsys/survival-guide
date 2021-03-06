# Имплементация

След анализирането на проблема и разбирането на итеративният подход на работа пристъпваме към имплементиране на решение. Използвайки програмният език С ние трябва да пишем нашите решения във файл с разширение `.с` които после ще компилираме до изпълн файл.

Създаваме си такъв файл, като името на файла е добра практика да говори какъв проблем решаваме, в нашият случай ще си направим:

```
$ touch prime_numbers.c
```

Имена от рода на`a.c`, `problem.c`, `exam2.c` не са подходящи.

## Стъпка 1

Първата стъпка е да си напишем скелет на програмата, минималното ни необходимо, които може да бъде компилирано и което ще работи.

```c
#include<stdio.h>

int is_prime(int);

int main() {
    return 0;
}
```

Тук е моментът в който промените ги запазваме и дори можем да се опитаме да компилираме.

```
gcc -Wall --pedantic --std=c11 prime_numbers.c
```

## Стъпка 2

Нека имплементираме нашата функция, която ще ни реши първият подпроблем, а именно намирането дали едно число е просто.

```c
#include<stdio.h>

int is_prime(int);

int main() {


    printf("is 3 prime = %d\n", is_prime(3));
    printf("is 12 prime = %d\n", is_prime(12));
    printf("is 17 prime = %d\n", is_prime(17));
    printf("is 1 prime = %d\n", is_prime(1));

    return 0;
}

int is_prime(int number) {
    for (int i = 2; i < number; ++i) {
        if (number % i == 0) {
            return 0;
        }
    }

    return 1;
}
```

Задължително след като напишем функция, колкото и малка да е тя, я извикваме с няколко различни стойности, за да проверим как се държи. Като гледаме кода виждаме, че не сме тествали нашата функция какво ще върне за 0 и отрицателни стойности.

## Стъпка 3

Променяме нашата `main()` за да проверим за 0 и отрицателните стойнсоти

```c
int main() {

    printf("is 3 prime = %d\n", is_prime(3));
    printf("is 12 prime = %d\n", is_prime(12));
    printf("is 17 prime = %d\n", is_prime(17));
    printf("is 1 prime = %d\n", is_prime(1));
    printf("is 0 prime = %d\n", is_prime(0));
    printf("is -1 prime = %d\n", is_prime(-1));

    return 0;
}
```

което извежда:

```
is 3 prime = 1
is 12 prime = 0
is 17 prime = 1
is 1 prime = 1
is 0 prime = 1
is -1 prime = 1
```

Изглежда, че трябва да променим нашата функция:

```c
int is_prime(int number) {

    if (number < 1) {
        return 0;
    }

    for (int i = 2; i < number; ++i) {
        if (number % i == 0) {
            return 0;
        }
    }

    return 1;
}
```

Добавихме проверката преди обхождането с цикъла, защото ако числото не е валидно просто число тоест е по-малко от 1, то тогава няма смисъл нашата програма да стига до цикъла въобще.

## Стъпка 4

След като имаме работеща функция за едно число, можем да завъртим един цикъл и да изведем N прости числа. Можем да го напишем първо в `main()` и след това да го изнесем за прилежност и четимост във отделна функция.

```c
int main() {

    printf("is 3 prime = %d\n", is_prime(3));
    printf("is 12 prime = %d\n", is_prime(12));
    printf("is 17 prime = %d\n", is_prime(17));
    printf("is 1 prime = %d\n", is_prime(1));
    printf("is 0 prime = %d\n", is_prime(0));
    printf("is -1 prime = %d\n", is_prime(-1));

    printf("Frist 10 prime numbers: ");

    int counter = 0;
    int next_prime = 1;
    while(counter < 10) {
        if (is_prime(next_prime)) {
            printf("%d ", next_prime);
            counter++;
        }
        next_prime++;
    }

    printf("\n");

    return 0;
}
```



