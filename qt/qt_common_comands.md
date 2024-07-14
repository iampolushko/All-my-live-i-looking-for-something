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

В файл .h на странице, с которой будем переходить

```c++
#include "SecondWindow.h"

private:
    Ui::MainWindow *ui;
    SecondWindow *window;
```

Для свершения перехода в файле .cpp на странице, с которой будем переходить

```c++
    window = new InfoWindow(this);
    window->show();
```

Если нам нужно закрыть или скрыть окно

```c++
    this->close();
    this->hide();
```

#### Подключение к sqlite

В файле .pro добавляем sql в этой строчке через пробел

```c++
QT       += core gui sql
```

В файле .h добавляем зависимости

```c++
#include <QSqlDatabase>
#include <QSqlQuery>
#include <QSqlTableModel>
#include <QSqlError>
```

В файле .cpp

```c++
db = QSqlDatabase::addDatabase("QSQLITE");
db.setDatabaseName("D:/All_projects/qtProjects/userdata.db");

 if (db.open())
    {
        QSqlQuery query = QSqlQuery(db);
        query.exec("SELECT * FROM users");
        while (query.next()) {
            QString lastname = query.value(0).toString(); // В value находиться номер стобца
            qDebug() << lastname;
        }

        ui->statusbar->showMessage("Успешное подключение к бд");
    }
    else
    {
        ui->statusbar->showMessage("Ошибка при подключении к бд: " + db.lastError().databaseText());
    }
```

#### Получение данных по https

```c++
QT       += core gui network
```

```c++
#include <QtNetwork>
#include <QtGui>
#include <QtCore>
```

```c++
 ui->setupUi(this);

    QNetworkAccessManager Manager;

    QUrl APIurl("https://api.country.is/9.9.9.9");

    QNetworkRequest request(APIurl);

    QNetworkReply *reply = Manager.get(request);

    QEventLoop loop;
    QObject::connect(reply, &QNetworkReply::finished, &loop, &QEventLoop::quit);
    loop.exec();

    if(reply->error() == QNetworkReply::NoError)
    {
        qDebug() << "Error : " << reply->errorString();
        QString Response = reply->readAll();
        qDebug() << "API Response : " << Response;
    }
    else
    {
        qDebug() << "Error : " << reply->errorString();
    }
```
