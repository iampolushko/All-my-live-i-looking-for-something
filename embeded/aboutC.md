# C

#### Facts

CERT recomendations - recomendations to make code more safety

#### Compilation from cmd

gcc - gnu c compiler. Can be used in linux like "gcc main.c" with some argument if u need it. After compiling u will get the "a.out" file. Execute this with "./a.out"

comptilation arguments:
-o app - change name of compiled execute file from averege "a" to "app" in this case(u cant name it like u want)

#### Program structure

"#include" - preprpcessor directive

#### Use function from stdio.h library

##### User input

```c
scanf_s("%d", &number); // _s - means safety(it don't work withou that)
```

**first argument** is a string with: **%** - just special symbol, **d** - deciminal integer
**second argument** is a reference in that we wil put the user input. **&** - take addres operator, it is says to function where the reference.

##### Console output

```
printf("You write a %d\n", number);
```

in **first argument** we got the **%d** what mean the decimimanl integer will be outputed and \n

#### unions (объединения)

```c
union tag_value
    {
        int intValue;
        float floatValue
    } value;
    unsigned storedType;
```

#### or и and

Побитовое 'и'

```c
(someShit1) & (someShit2);
```

Побитовое 'или'

```c
(someShit1) | (someShit2);
```

#### Побитовое 'не'

Просто инвертирует биты: **~(01111) = (1000)**

#### Побитовый сдвиг

Так - же его можно назвать умнажением или делением на 2^n
**<<** - сдвиг влево. Добавляет биты вперед: **0b111 << 2 = 0b11100**. Как правло используется, чтобы установить значение(как правило 1) в определенный бит регистра.
**>>** - сдвиг вправо. Удаляте биты с конца: **0b11100 << 2 = 0b111**

#### Изменение битности числа

Предположим, что нам нужно получить восьмибитное число в восьмиричной системе счисления. Для этого используется конструкция "(200 & 0xFF)", где первое число, это число, которое нужно проебразовать, а второе - это число, в бит которого будет происходить преобразование
Рассмотрим 3 примера

```с++
    char reference1 = ("ref" & 0xFF); //0xFF - это восьмеричное число в
    printf("%d \n", reference1);

    char reference2 = (300 & 0xFF);
    printf("%d \n", reference2);

    char reference3 = (256 & 0xFF);
    printf("%d \n", reference3);
```

В результате мы получим вывод

```bash
-56
44
0
```

#### Switch case

Выведет **first**

```c++
    int ref = 1;

    switch (ref)
    {
    case 1:
        printf("first \n");
        break;
    case 2:
        printf("second \n");
        break;
    }
```
