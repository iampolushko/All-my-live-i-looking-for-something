## Arrays

! С++ doesn't have any array size check. Its works but using the unexpected memory. It is can crash a system.

```c++
int main()
{
    int crash[10], i;
    for(i=0; i<100; i++) crash[i]=i;
    return 1;
}
```

## Strings

### Base

**String** in c++ is **char** array what ends with (**'\0'**) symbol.

```c++
#include<stdio.h>
int main(void)
{
	char str[5] = "test";
	printf(str);
	return 0;
}
```

(**'\0'**) symbol will be added automaticly.

### Read from keyboard

```c++
#include <iostream>
int main(void)
{
	char user_str[80];
	std::cout << "Write the line: ";
	std::cin.getline(user_str, sizeof user_str);
	std::cout << "You write the: ";
	std::cout << user_str;
	return 0;
}
```

### Functions from <cstring

**Copy** strings with **strcpy_s**

```c++
	char str[80];
	char str2[5] = "test";
	strcpy_s(str, str2);
	std::cout << str;
```

**Add** string to string

```c++
	char str[12] = "Hello ";
	char str2[6] = "world";
	strcat_s(str, str2);
	std::cout << str;
```

**Equals** operation. The 'str1 == str2' is doesnt work with strings

```c++
	char str1[5] = "test";
	char str2[5] = "test";
	if (!strcmp(str1, str2))
	{
		std::cout << "Yes";
	}
	else
	{
		std::cout << "No";
	}
```

! If strings is equals strcmp returns false.

**Line Lengh**. It returns lengh without (**'\0'**)

```c++
	char str1[5] = "test";
	std::cout << strlen(str1);
```

### Functions from <cctype

**isalpha()** - returns true if arguments is symbol from alphabet,
**isdigit()** - returns true if arguments is number,
**isspace()** - true if arguments is space
**ispunct()** - true if dot?

### Array of strings

```c++
char number[2][4] = {"one", "two"};
```

### Указатели

```c++
	int int_reference = 3200; //просто переменная типа int
	int* int_reference_address = &int_reference; //получаем адрес переменной
	int int_reference_by_address = *int_reference_address; //получаем значение переменной по адресу

	std::cout << "Balance address is:" << int_reference_address << '\n'; //0000009B9E37F784
	std::cout << "Balance by address:" << int_reference_by_address << '\n'; //3200

	*int_reference_address = 10;
	std::cout << "Balance with new value by address:" << *int_reference_address << '\n'; //10

	(*int_reference_address)++;
	std::cout << "Incremented balance by address:" << *int_reference_address << '\n'; //11
```

- при объявлении указателей, их нельзя оставлять пустыми, так как это может вызвать ошибки в системе. Если нет возможности их определить, то хотя бы прировняй их к 0.
  ```
  int* ar = 0;
  ```

* имя массива является **указателем** на первый элемент этого массива.
  т.е. в коде ниже обе записи эквивалентны

  ```c++
  	int ar[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  	//вывод всех записей
  	for (int i = 0; i < std::size(ar); i++) {
  		std::cout << ar[i] << " "; // обращение по индексу
  		std::cout << *(ar + i) << " "; // обращение по указателю
  	}
  ```

  p.s. Имя массива - это константный указатель, т.е. ++ или -- применять к нему нельзя

- #### Создание переменных бывает статическим и динамическим(с динамическим выделением памяти)

```c++
	//Статическое
	int i;
	//Динамическое
	int* ptr = new int;
```

- Рассмотрим работу с динамическими переменными

  ```c++
  	//Создание
  	int* ptr = new int;
  	//Работа
  	*ptr = 10;
  	std::cout << *ptr;
  	//Удаление из памяти
  	delete ptr;
  ```

- Рассмотрим работу с динамическими массивами

  ```c++
  //Массив можно объявить одним из способов
  int* ar = new int[5];
  int* ar = new int[5] {1, 2, 3, 4, 5};
  ```

  Прмер программы

  ```c++
  	//создаём массив
  	int* ar = new int[10];
  	//заполняем его значениями
  	for (int i = 0; i < 10; i++) {
  		ar[i] = i;
  	}
  	//выводим значения
  	for (int i = 0; i < 10; i++) {
  		std::cout << ar[i];
  	}
  	//очищаем память от массива
  	delete[] ar;
  ```

### classes

- #### constuctors
  Добавим в стандартный конструктор класса аргументы **int firstIntRef** и **int secondIntRef** и создадим публичные методы **returnSummOfConstrucorArgumentsMethod** **returnSummOfMethodArgumentsMethod(int firstIntRef, int secondIntRef)**

```c++
#ifndef TESTCLASSWITHCONSTRUCTOR_H
#define TESTCLASSWITHCONSTRUCTOR_H

class TestClassWithConstructor
{
public:
    TestClassWithConstructor(int firstIntRef, int secondIntRef);

    int returnSummOfConstrucorArgumentsMethod();
    int returnSummOfMethodArgumentsMethod(int firstIntRef, int secondIntRef);

private:
    int firstIntRefInClass;
    int secondIntRefInClass;
};

#endif // TESTCLASSWITHCONSTRUCTOR_H
```

Создадим реализацию всего того, что мы создали в header файле

```c++
#include "testclasswithconstructor.h"

TestClassWithConstructor::TestClassWithConstructor(int firstIntRef, int secondIntRef)
{
    firstIntRefInClass = firstIntRef;
    secondIntRefInClass = secondIntRef;
}

int TestClassWithConstructor::returnSummOfConstrucorArgumentsMethod()
{
    return firstIntRefInClass + secondIntRefInClass;
}

int TestClassWithConstructor::returnSummOfMethodArgumentsMethod(int firstIntRef, int secondIntRef)
{
    return firstIntRef + secondIntRef;
}
```

Создадим экземляр класса, передав аргументы в конструктор и вызовем два его метода.

```c++
    TestClassWithConstructor testClassWithConstructor(10, 10);
    qDebug() << testClassWithConstructor.returnSummOfConstrucorArgumentsMethod();
    qDebug() << testClassWithConstructor.returnSummOfMethodArgumentsMethod(10, 10);
    //В данном случае использутеся вывод в консоль при помощи QDebug, но можно использовать любой другой
```

- #### static classes
  Создаем header файл для статичного класса

```c++
#ifndef TESTCLASSWITHCONSTRUCTOR_H
#define TESTCLASSWITHCONSTRUCTOR_H

class TestClassWithConstructor
{
public:

    static int returnSummOfMethodArgumentsMethod(int firstIntRef, int secondIntRef);
    static int publicIntRef;

private:
    static int privateIntRef;
};

#endif // TESTCLASSWITHCONSTRUCTOR_H
```

Создадим реализацию всего того, что мы создали в header файле

```c++
#include "testclasswithconstructor.h"

int TestClassWithConstructor::returnSummOfMethodArgumentsMethod(int firstIntRef, int secondIntRef)
{
    return firstIntRef + secondIntRef;
}

```

Вызовем методы из статичного класса

```c++
qDebug() << TestClassWithConstructor::returnSummOfMethodArgumentsMethod(10, 10);
```

### sturctures (структуры)

Declaring the structure

```c++
struct person {   // Declare PERSON struct type
    int age;   // Declare member types
    bool gender;
    float weight;
};
```

Structure usage

```c++
    struct person sister;   // C style structure declaration
    person brother;   // C++ style structure declaration
    sister.age = 13;   // assign values to members
    brother.age = 7;

    qDebug() << sister.age; //output the data from structures(you can use any console output way)
    qDebug() << brother.age;
```

also you can define a structures

```c++
struct person {   // Declare PERSON struct type
    int age;   // Declare member types
    bool gender;
    float weight;
} family_member;   // Define object of type PERSON
```

```c++
    family_member.age = 10;
    qDebug() << family_member.age;
```
