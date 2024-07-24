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

### Массивы

```c++

```

### Указатели

```c++
	int int_reference = 3200; //просто переменная типа int
	int* int_reference_address = &int_reference; //получаем адрес переменной
	int int_reference_by_address = *int_reference_address; //получаем значение переменной по адресу

	std::cout << "Balance address is:" << int_reference_address << '\n';
	std::cout << "Balance by address:" << int_reference_by_address << '\n';

	*int_reference_address = 10;
	std::cout << "Balance with new value by address:" << *int_reference_address << '\n';

	(*int_reference_address)++;
	std::cout << "Incremented balance by address:" << *int_reference_address << '\n';

```
