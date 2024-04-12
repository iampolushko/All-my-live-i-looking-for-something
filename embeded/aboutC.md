# C

### Facts

CERT recomendations - recomendations to make code more safety

#### Compilation from cmd

gcc - gnu c compiler. Can be used in linux like "gcc main.c" with some argument if u need it. After compiling u will get the "a.out" file. Execute this with "./a.out"

comptilation arguments:
-o app - change name of compiled execute file from averege "a" to "app" in this case(u cant name it like u want)

#### Program structure

"#include" - preprpcessor directive

#### User input

Use function from stdio.h library

```c
scanf_s("%d", &number); // _s - means safety(it don't work withou that)
```

**first argument** is a string with: **%** - just special symbol, **d** - deciminal integer
**second argument** is a reference in that we wil put the user input. **&** - take addres operator, it is says to function where the reference.

### Console output

```
printf("You write a %d\n", number);
```

in **first argument** we got the **%d** what mean the decimimanl integer will be outputed and \n
