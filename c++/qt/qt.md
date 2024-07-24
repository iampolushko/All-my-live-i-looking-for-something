# Project structure

first.pro - config file(have the project name. 'First' in this case.)

#### Header

заголовочные файлы. Они инклюдятся в source файлах.
mainwindow.h

#### Sources folder

main.cpp - main load file

mainwindow.cpp - file with all ui logic(like controller in javafx)

#### Forms

mainwidow.ui - file with ui(design)

p.s. last

#### Qt Ui gide

##### Adding the new page

- For add the new window.cpp and window.ui we need to click on project folder and choose "add new" => choose the "qt" in "files and classes" list and "qt designer form class" in central list => follow the app instructions

- For create new "button clicked" in window.cpp function you need to open ui file in designer => add the button => click on it => click on "Go to slot" => choose "clicked".

#### Tips

Check that: https://habr.com/ru/articles/270649/
