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

## XLSX
Открытие, просмотр, редактирование и сохранение файла
```python
import openpyxl

book = openpyxl.load_workbook('testXLSX.xlsx')
sheet = book.active

print(sheet['A1'].value) #.value позволяет как взять, так и присвоить значение

book.save('testXLSX.xlsx') # сохраняет активный файл
```
Создание файла

```python
import openpyxl

wb = openpyxl.Workbook()
ws = wb.active
ws.title = "TestFromPy"

#Первый способ добавлять данные
ws['A1'] = 'Hello'
ws['B1'] = 'World'

#Второй способ добавлять данные
data = [
    ["test1", "test2"],
    ["test3", "test4"],
    ["test5", "test6"],
]
for row in data:
    ws.append(row)

wb.save("HelloWorld.xlsx")
```

## tips

- ### Получить уникальные значения массива

```python
fruits = ['яблоко', 'груша', 'банан', 'яблоко', 'груша', 'яблоко']
unique_fruits = list(set(fruits)) //set() возвращает словарь, но в целом его в list можно и не преобразововать
print(unique_fruits)
```

- ### Подключение библиотек без интернета
Когда интернет есть загружаем библиотеки в папку (например distrib)

```python
pip download -d "C:\Users\polushkohui\Desktop\distrib" openpyxl
```

Затем из этой папки мы можем подтягивать библиотеки в проект, когда интернета нет
```python
pip install --no-index -f "C:\Users\polushkohui\Desktop\distrib" openpyxl
```
