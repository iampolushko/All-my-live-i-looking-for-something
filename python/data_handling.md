## csv

Reading

```python
names = []
import csv
with open('data.csv', 'r', encoding='utf-8') as file: # u also can use w to write csv
    csv_reader = csv.reader(file)
    for line in csv_reader:
        names.append(line[1]) #get data from every line
```

Writing

```python
with open('data.csv', 'w', encoding='utf-8') as file:
    # file.write("random shit" + "\n") #this is works too
    writer = csv.writer(file)
    writer.writerow(("elem1", "elem2", "elem3"))
```

While using tag **'w'** if file not existing it's will make a new one

## sqlite

```python
import sqlite3

db = sqlite3.connect("identifier.sqlite")

c = db.cursor()

c.execute("SELECT * FROM table")
print(c.fetchone()) #get line

db.close()
```

## tips

- Получить уникальные значения массива

```python
fruits = ['яблоко', 'груша', 'банан', 'яблоко', 'груша', 'яблоко']
unique_fruits = list(set(fruits)) //set() возвращает словарь, но в целом его в list можно и не преобразововать
print(unique_fruits)
```
