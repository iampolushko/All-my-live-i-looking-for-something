# Прорядок выозова методов в Activity
![](/java/javaResourses/androidAppStructure.png)


# Fragments
Это база, без которого настоящее, взрослое мобильное приложение не обходится
## Порядок/пример создания:

### 1. Создание самих фрагментов
Нажимаем на `com.example.'имя проекта'` и выбираем необходимый **Fragment**. Проделаем так необходимое количество раз(в нашем случае 3 шт.). В папке `com.example.'имя проекта'` появятся java файлы, а в `res/layout/` появятся xml файлы для наших Fragment.

### 2. Изменение xml файла для Activity, в котором будут отображаться фрагменты
В нашем случае у нас есть MainActivity. Изменим его xml файл под названием `activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.LinearLayoutCompat xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

<!--    Разберём пример для TabLayout-->
    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tablayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#075E53"
        app:tabIndicator="@color/white"
        app:tabSelectedTextColor="@color/white"
        >

        <com.google.android.material.tabs.TabItem
            android:id="@+id/tab1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/first"
            />

        <com.google.android.material.tabs.TabItem
            android:id="@+id/tab2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/second"
            />

        <com.google.android.material.tabs.TabItem
            android:id="@+id/tab3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/third"
            />

    </com.google.android.material.tabs.TabLayout>

<!--    Этот FrameLayout будет меняться, при нажатии на разные TabItem-->
    <FrameLayout
        android:id="@+id/framelayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    </FrameLayout>



</androidx.appcompat.widget.LinearLayoutCompat>
```

Так это выглядит:

![](/java/javaResourses/androidAppFragmentExample.png)

### 3. Изменение cpp файла для Activity, в котором будут отображаться фрагменты

```c++
package com.example.manypages;

import android.os.Bundle;
import android.widget.FrameLayout;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
import androidx.fragment.app.Fragment;
import androidx.fragment.app.FragmentTransaction;

import com.google.android.material.tabs.TabLayout;

public class MainActivity extends AppCompatActivity {

    //Создадим экземпляр frameLayout, который будет заменяться на фрагменты
    FrameLayout frameLayout;
    //Создадим экземпляр tabLayout, по нажатию на который будет подставлятся фрагмент.
    //Здесь по сути может быть что угодно, на что можно нажать, например кнопка
    TabLayout tabLayout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);

        //Определим экземпляры
        frameLayout = (FrameLayout) findViewById(R.id.framelayout);
        tabLayout = (TabLayout) findViewById(R.id.tablayout);

        //Покажем фрагмент, который будет отображаться изначально. Если его не указывать, то мы бедем видеть просто содержимое frameLayout
        getSupportFragmentManager().beginTransaction().replace(R.id.framelayout, new FirstFragment())
                .addToBackStack(null)
                .commit();

        //Меняем фрагмент по нажатию
        tabLayout.setOnTabSelectedListener(new TabLayout.OnTabSelectedListener() {
            @Override
            public void onTabSelected(TabLayout.Tab tab) {
                Fragment fragment = null;
                switch (tab.getPosition()){
                    case 0:
                        fragment = new FirstFragment();
                        break;
                    case 1:
                        fragment = new SecondFragment();
                        break;
                    case 2:
                        fragment = new ThirdFragment();
                        break;
                }

                getSupportFragmentManager().beginTransaction().replace(R.id.framelayout, fragment)
                        .setTransition(FragmentTransaction.TRANSIT_FRAGMENT_OPEN)
                        .commit();
            }

            @Override
            public void onTabUnselected(TabLayout.Tab tab) {

            }

            @Override
            public void onTabReselected(TabLayout.Tab tab) {

            }
        });

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
```

Теперь мы можем как угодно менять c++ и xml у фрагментов. Так же, как и у activity.