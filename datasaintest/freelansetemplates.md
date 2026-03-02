# Python

import json

with open('result.json', 'r', encoding='utf-8') as f:
    text = json.load(f)

#json при чтении храниться в типе "тег - значения"
#text['messages'] - обращаться к вложенным тегам и к значениям так

with open('file.txt', 'w') as the_file:
        the_file.write(какая_нибудь_строка + "\n")


# SQL
Чтобы запустить службу SQL на windows 10 нажимаем ``win + R`` и вводим команду ``services.msc``, затем ищем сервис с SQL в названии и запускаем его.


