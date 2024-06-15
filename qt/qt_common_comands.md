#### Qt Ui gide

- For add the new window.cpp and window.ui we need to click on project folder and choose "add new" => choose the "qt" in "files and classes" list and "qt designer form class" in central list => follow the app instructions

- For create new "button clicked" in window.cpp function you need to open ui file in designer => add the button => click on it => click on "Go to slot" => choose "clicked".

#### Всплывающие окна

- Just a massage
  ```c++
  QMessageBox::about(this, "Заголовок", "Текст внутри");
  ```

* Error window (Like first but whith scarry red christ)

  ```c++
    QMessageBox::critical(this, "Заголовок", "Текст внутри");
  ```

* Warning window(Like first but whith scarry yellow screamer)

  ```c++
    QMessageBox::warning(this, "Заголовок", "Текст внутри");
  ```

* Information window(Like first but with information symbol)

  ```c++
    QMessageBox::information(this, "Заголовок", "Текст внутри");
  ```

* Question window and how to get data from it.

  ```c++
    QMessageBox::StandardButton questionButton = QMessageBox::question(this, "Заголовок", "Текст с вопросом внутри", QMessageBox::Yes | QMessageBox::No);

    if(questionButton == QMessageBox::Yes) {
        qDebug() << "Yes button has been pushed";  /*Just a qt console output. You need to include the <QDebug>*/
    } else {
        qDebug() << "No button has been pushed";  /*qt console output too*/
    }
  ```

#### Переход на другую страницу

```c++

```
