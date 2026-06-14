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


# Боковое меню (NavigationView)
Можно Переключатся между фрагментами(или делать что угодно другое, по нажатии на пункты меню, т.к. это просто кнопки) при помощи **выползающего бокового меню**.


### 1. Создадим боковое меню

Луче всего хранить меню в menu resource directory в res. Для этого нужно создать resource directory и выбрать Resource Type - menu

Затем в этой директории создадим новый Menu Resource File

Модифицируем код файла `nav_menu`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    tools:showIn="navigation_view">

    <group
        android:checkableBehavior="single">

        <item
            android:id="@+id/nav_first_fragment"
            android:title="@string/first_fragment"
            android:icon="@drawable/ic_launcher_foreground"/>

        <item
            android:id="@+id/nav_second_fragment"
            android:title="@string/second_fragment"
            android:icon="@drawable/ic_launcher_foreground"/>

        <item
            android:id="@+id/nav_third_fragment"
            android:title="@string/third_fragment"
            android:icon="@drawable/ic_launcher_foreground"/>


    </group>

</menu>
```
В коде для примера добавлены фрагменты, между которыми это меню будет переключать



### 2. Напишем **xml** файл для работы выползающего меню(Доработем файл из примера с фрагментами) 

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--Поменяем androidx.appcompat.widget.LinearLayoutCompat на androidx.drawerlayout.widget.DrawerLayout-->
<androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">


<!--    Создадим LinearLayoutCompat здесь-->
    <androidx.appcompat.widget.LinearLayoutCompat
        android:id="@+id/main"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

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

        <FrameLayout
            android:id="@+id/framelayout"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

        </FrameLayout>

    </androidx.appcompat.widget.LinearLayoutCompat>

    <!--    NavigationView, который ссылается на созданное нами меню, которое и будет выдвигаться сбоку-->
    <com.google.android.material.navigation.NavigationView
        android:id="@+id/nv_side"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        app:menu="@menu/nav_menu"
        android:fitsSystemWindows="true"
        />



</androidx.drawerlayout.widget.DrawerLayout>
```
*Меню будет рабоать, только если оно находится в DrawerLayout вместе с другим Layout. Нарпимер:
```
DrawerLayout
    ЛюбойLayout
    Menu
``` 
т.к. `DrawerLayout` — это специальный контейнер, который умеет прятать один из дочерних элементов за левым или правым краем экрана и выдвигать его по свайпу или программно.

### 2. Теперь добавим обработку нажатий на элементы меню в MainActivity
Пример листенера, который по нажатю на строки(item) в меню переключает фрагменты
```java
package com.example.manypages;

import android.os.Bundle;
import android.widget.FrameLayout;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.ActionBarDrawerToggle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
import androidx.drawerlayout.widget.DrawerLayout;
import androidx.fragment.app.Fragment;
import androidx.fragment.app.FragmentTransaction;

import com.google.android.material.navigation.NavigationView;
import com.google.android.material.tabs.TabLayout;

public class MainActivity extends AppCompatActivity {

    //Создадим экземпляр frameLayout, который будет заменяться на фрагменты
    FrameLayout frameLayout;
    //Создадим экземпляр tabLayout, по нажатию на который будет подставлятся фрагмент.
    //Здесь по сути может быть что угодно, на что можно нажать, например кнопка
    TabLayout tabLayout;

    //Создадим экземпляры для работы с меню
    DrawerLayout drawerLayout;
    NavigationView nv_side;
    

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
        
        //Определим переменные для работы с меню
        drawerLayout = findViewById(R.id.drawer_layout);
        nv_side = findViewById(R.id.nv_side);

        // Обработка нажатий на пункты бокового меню
        nv_side.setNavigationItemSelectedListener(item -> {
            Fragment selectedFragment = null;
            int itemId = item.getItemId();

            if (itemId == R.id.nav_first_fragment) {
                selectedFragment = new FirstFragment();
            } else if (itemId == R.id.nav_second_fragment) {
                selectedFragment = new SecondFragment();
            } else if (itemId == R.id.nav_third_fragment) {
                selectedFragment = new ThirdFragment();
            }

            if (selectedFragment != null) {
                getSupportFragmentManager().beginTransaction()
                        .replace(R.id.framelayout, selectedFragment)
                        .setTransition(FragmentTransaction.TRANSIT_FRAGMENT_OPEN)
                        .commit();
            }

            // Закрываем боковое меню после выбора
            drawerLayout.closeDrawers();

            // Подсвечиваем выбранный пункт (опционально)
            item.setChecked(true);

            return true;
        });

        
    }
}
```
Вот, что получим:

![](/java/javaResourses/androidAppMenuExample.png)


# Карты

Будем использовать OSMdroid карты т.к. они бесплатные


### 1. Добавим зависимости в build.gradle.kts (Module :app)

```kts
plugins {
    alias(libs.plugins.android.application)
}

android {
    namespace = "com.example.osmdroidjavaapp"
    compileSdk {
        version = release(36) {
            minorApiLevel = 1
        }
    }

    defaultConfig {
        applicationId = "com.example.osmdroidjavaapp"
        minSdk = 23
        targetSdk = 36
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            isMinifyEnabled = false
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
}

dependencies {
    implementation(libs.appcompat)
    implementation(libs.material)
    implementation(libs.activity)
    implementation(libs.constraintlayout)
    testImplementation(libs.junit)
    androidTestImplementation(libs.ext.junit)
    androidTestImplementation(libs.espresso.core)

    // Добавлено: OSMDroid для работы с картами OpenStreetMap
    implementation("org.osmdroid:osmdroid-android:6.1.20")
}
```
### 2. Добавим разрешения в AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">


    <!-- ===== Добавим эти разрешения для работы карт ===== -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <!-- ================================= -->

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.OsmDroidJavaApp">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

### 3. Добавим в activity_main.xml карту и кнопку для определения местоположения

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <org.osmdroid.views.MapView
        android:id="@+id/map_view"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />

    <Button
        android:id="@+id/btn_location"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_margin="16dp"
        android:text="Показать местоположение" />

</LinearLayout>
```
### 4. MainActivity.java, в котром функционал отображения карты, постоянной метки и функционал обратотки кнопки для определения местоположения

```java
package com.example.osmdroidjavaapp;

import android.Manifest;
import android.content.Context;
import android.content.pm.PackageManager;
import android.location.Location;
import android.location.LocationListener;
import android.location.LocationManager;
import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;
import org.osmdroid.config.Configuration;
import org.osmdroid.tileprovider.tilesource.TileSourceFactory;
import org.osmdroid.util.GeoPoint;
import org.osmdroid.views.MapView;
import org.osmdroid.views.overlay.Marker;

public class MainActivity extends AppCompatActivity {

    private static final int LOCATION_PERMISSION_REQUEST = 100;
    private MapView mapView;
    private Button locationButton;
    private LocationManager locationManager;
    private Marker currentLocationMarker; // для маркера текущего положения

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Инициализация конфигурации OSMDroid
        Configuration.getInstance().load(
                getApplicationContext(),
                getSharedPreferences("osmdroid", MODE_PRIVATE)
        );

        setContentView(R.layout.activity_main);

        mapView = findViewById(R.id.map_view);
        locationButton = findViewById(R.id.btn_location);

        setupMap();
        setupLocationButton();

        // Тестовый маркер (Красная площадь)
        addMarker(56.317805, 44.000051, "Airsoft rus");

        // Инициализация LocationManager
        locationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);
    }

    private void setupMap() {
        mapView.setTileSource(TileSourceFactory.MAPNIK);
        mapView.setMultiTouchControls(true);
        mapView.getController().setZoom(12.0);
        mapView.getController().setCenter(new GeoPoint(55.751244, 37.618423));
    }

    private void setupLocationButton() {
        locationButton.setOnClickListener(v -> {
            // При нажатии проверяем разрешение и запрашиваем, если нужно
            if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                    != PackageManager.PERMISSION_GRANTED) {
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
                        LOCATION_PERMISSION_REQUEST);
            } else {
                getMyLocation();
            }
        });
    }

    // Получение последнего известного местоположения
    private void getMyLocation() {
        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                != PackageManager.PERMISSION_GRANTED) {
            return;
        }

        Location lastKnownLocation = locationManager.getLastKnownLocation(LocationManager.GPS_PROVIDER);
        if (lastKnownLocation == null) {
            lastKnownLocation = locationManager.getLastKnownLocation(LocationManager.NETWORK_PROVIDER);
        }

        if (lastKnownLocation != null) {
            updateMapToLocation(lastKnownLocation);
        } else {
            // Если нет последнего известного, запрашиваем обновление (один раз)
            locationManager.requestSingleUpdate(LocationManager.GPS_PROVIDER, new LocationListener() {
                @Override
                public void onLocationChanged(@NonNull Location location) {
                    updateMapToLocation(location);
                }

                @Override
                public void onProviderEnabled(@NonNull String provider) {}
                @Override
                public void onProviderDisabled(@NonNull String provider) {}
                @Override
                public void onStatusChanged(String provider, int status, Bundle extras) {}
            }, null);
            Toast.makeText(this, "Запрос GPS... подождите", Toast.LENGTH_SHORT).show();
        }
    }

    private void updateMapToLocation(Location location) {
        GeoPoint userLocation = new GeoPoint(location.getLatitude(), location.getLongitude());
        mapView.getController().setCenter(userLocation);
        mapView.getController().setZoom(15.0);

        // Удаляем старый маркер местоположения, если есть
        if (currentLocationMarker != null) {
            mapView.getOverlays().remove(currentLocationMarker);
        }

        currentLocationMarker = new Marker(mapView);
        currentLocationMarker.setPosition(userLocation);
        currentLocationMarker.setAnchor(Marker.ANCHOR_CENTER, Marker.ANCHOR_BOTTOM);
        currentLocationMarker.setTitle("Вы здесь");
        currentLocationMarker.setIcon(ContextCompat.getDrawable(this, android.R.drawable.ic_menu_mylocation));
        mapView.getOverlays().add(currentLocationMarker);
        mapView.invalidate();

        Toast.makeText(this, "Широта: " + location.getLatitude() + "\nДолгота: " + location.getLongitude(),
                Toast.LENGTH_LONG).show();
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == LOCATION_PERMISSION_REQUEST) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                getMyLocation();
            } else {
                Toast.makeText(this, "Разрешение не получено", Toast.LENGTH_SHORT).show();
            }
        }
    }

    private void addMarker(double latitude, double longitude, String title) {
        Marker marker = new Marker(mapView);
        marker.setPosition(new GeoPoint(latitude, longitude));
        marker.setAnchor(Marker.ANCHOR_CENTER, Marker.ANCHOR_BOTTOM);
        marker.setTitle(title);
        marker.setIcon(ContextCompat.getDrawable(this, android.R.drawable.star_on));
        mapView.getOverlays().add(marker);
        mapView.invalidate();
    }
}
```



