# Python

### Primitive

- Making the function
  ```python
  def name(argunments):
      return something
  ```

### Clases

- Making the classes

  ```python
  //Class2 is parent.
  class Class1(Class2): //This place can be empty or replace Class2 with ABC to make the class abstact
      def __init__(self, arg1, arg2):
          self.arg1 = arg1
          self.arg2 = arg2
  ```

- Methods

```python
def do_some_sheat(self): // U can add after self any arguments
    return 1
```

- Abstract methods

```python
 @abstractmethod //put this marker before the method for make it abstract
 def abstract_method(self):
    pass
```

Abstract methods doesnt have the realisation. The **can** do something only on kids classes.

### Interfaces

Whats the differents betwen abstract classes and interfaces?
Abstracts classes can contain the don't abstract methods. Abstract methods **can** have the realisation in kids classes and **intarface** have **contract** with class what mean what class **need** to make realistion for all interface methods.

### Levels of abstaction

[Full hello lection](https://www.youtube.com/watch?v=_EHgMxtrOmE)

#### 1 - Special syntax

- **First one is "Моржик"**.
  This just assignment opertator what return assignment elemnt
  ```python
  print(arg := 1)
  ```
  Output
  ```
  15
  ```
- **List comperhansion**
  Have a lot of using scenarios. I demonstrate just a few
  ```python
  squares = [x ** 2 for x in range(10)]
  ```
  Output
  ```
  [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
  ```
  or if we wanna read file what formated like
  ```
  1
  2
  3
  ...
  ```
  we can
  ```python
  file = open("File addres")
  array = [int(x) for x in file]
  ```
  or add if
  ```python
  odds = [x for x in range(10) if x % 2 != 0]
  ```
  Output:
  ```
  [1, 3, 5, 7, 9]
  ```
- **Pattern matching**
  "match/case is the same to switch/case"
  Patterns of pattern matching:

  - Literal pattern

  ```python
  match number:
  case 1:
      print('number is 1')
  case 2:
      print('number is 2')
  ```

  - Capture pattern

  ```python
  match greeting:
  case "":
      print('Hello my friend')
  case name:
      print(f'Hello  {name}')
  ```

  - Wildcard Pattern
    We can use it if got to many cases. \_ - is like defoult value what compatable with every element

  ```python
  match number:
  case 42:
      print("Its’s forty two")
  case _:
      print("I don’t know, what it is")
  ```

  - Class patterns

  ```python
  from dataclasses import dataclass

  @dataclass
  class Coordinate:
      x: int
      y: int
      z: int

  coordinate = Coordinate(1, 2, 3)
  match coordinate:
      case Coordinate(0, 0, 0):
          print('Zero point')
      case _:
          print('Another point')
  ```

  - Constant Value Patterns
  - Sequence Patterns
  - Mapping Patterns

#### 2 - Types

- **1 - lambda calculus**
  Code without lambda function:
  ```python
  def add(x, y):
      return x + y
  print(add(4, 5))
  ```
  Code with lambda function:
  ```python
  add = lambda x, y: x + y //lambda function is anon function
  print(add(4, 5))
  ```
  Output
  ```
  9
  ```

#### 3 - Python Data Model

////

### Working with net

#### Flask

https://youtube.com/playlist?list=PL0lO_mIqDDFXiIQYjLbncE9Lb6sx8elKA&si=q-HkRZxsbLzr_-Cx

#### django
