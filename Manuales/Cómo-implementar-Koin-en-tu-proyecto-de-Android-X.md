
Esta es una guía de como implementar Koin en tu proyecto de Android X.

Koin viene reemplazando a Dagger 2 como inyector de dependencia debido a su sencilla implementación y al no requerir una larga curva de aprendizaje aún mas

## Procedimiento:

### 1. Agregar las dependencias al Gradle:

```css
dependencies {
	implementation 'org.koin:koin-androidx-scope:1.0.2'
}
```

> Puedes obtener la ultima version [aquí](https://github.com/InsertKoinIO/koin#current-version).

### 2. Crear una aplicación en tu proyecto:

Crear una clase que herede de la clase **Application**, luego agregar el método ***startKoin()*** importandolo, en el método **onCreate** para inicializar **Koin** en tu proyecto.

```kotlin  
startKoin(this, listOf())
```
Tu clase aplicación debería verse así:

```kotlin
import org.koin.android.ext.android.startKoin

class MainApplication : Application() {  

    override fun onCreate() {  
        super.onCreate()  
        startKoin(this, listOf())
    }  
}
```


### 3. Registrar tu aplicación en el archivo AndroidManifest:

Es importante que registres tu aplicación para que tu proyecto reconozca la aplicación que creaste como aplicación de inicialización, debes agregarlo con el atributo **name** en tu archivo **AndroidManifest**:

```xml
android:name=".MainApplication"
```

Tu archivo **AndroidManifest** debería verse así:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<manifest xmlns:android="http://schemas.android.com/apk/res/android"  
  xmlns:dist="http://schemas.android.com/apk/distribution"  
  package="demo.android">  
	<dist:module dist:instant="true" />  
	<application
	    android:name=".MainApplication"
	    android:allowBackup="true"  
	    android:icon="@mipmap/ic_launcher"  
	    android:label="@string/app_name"  
	    android:roundIcon="@mipmap/ic_launcher_round"
	    android:supportsRtl="true"
	    android:theme="@style/AppTheme">  
		<activity  
			android:name=".HomeActivity">  
			 <intent-filter> 
				 <action android:name="android.intent.action.MAIN" />  
				 <category android:name="android.intent.category.LAUNCHER" />  
			 </intent-filter>
		</activity>
	</application>  
</manifest>
```

### 4. Crear tu archivo de modulos

Crearemos un archivo de extension **.kt** donde crearemos los modulos para la inyección de dependencia.

Para este ejemplo creare un archivo ***module.kt*** donde creare un modulo e inicializare mi presentador:

```kotlin  
val presenterModule = module {  
  factory { HomePresenter() }  
}
```

En caso tu clase requiera de un contexto en el constructor, **Koin** te brinda un contexto para que lo utilizes con tan solo importarlo, esta :

```kotlin  
import org.koin.android.ext.koin.androidContext

val presenterModule = module {  
  factory { HomePresenter(androidContext()) }  
}
```

Si tu constructor requiere de un parámetro externo como un modelo o cualquier tipo de dato, podemos utilizar la siguiente función:

Para este ejemplo utilizare un adaptador:

```kotlin  
import org.koin.android.ext.koin.androidContext

val presenterModule = module {  
  factory { HomePresenter(androidContext()) }  
}

val adapterModule = module {  
  factory { (model: Model) -> HomeAdapter(model) }  
   // or 
  factory { (model: Model, intParam : Int) -> HomeAdapter(model, intParam) } 
  // or
  factory { (model: Model) -> HomeAdapter(androidContext(), model) } // with context
  // or 
  factory { (model: Model, intParam : Int) -> HomeAdapter(androidContext(), model, intParam) } 
}
```

> Nota: Puedes implementar varios modulos en un mismo archivo **.kt**

### 5. Implementar tu modulo
Para que **Koin** reconozca tu modulo debes relacionarlo en tu clase **Application** simplemente importando tu modulo, donde tu clase quedaría así:

```kotlin
import demo.android.presenterModule  
import demo.android.adapterModule  
import org.koin.android.ext.android.startKoin

class MainApplication : Application() {  

    override fun onCreate() {  
        super.onCreate()  
        startKoin(this, listOf(presenterModule, adapterModule))
    }  
}
```

### 6. Listo para inyectar
Ahora que implementaste la estructura base, estas listo para usar la inyección de dependencia con el método ***inject()*** de la siguiente manera:

```kotlin
private val presenter : HomePresenter by inject()  
```

Si tu constructor requiere de parámetros como en el caso del adaptador sería de la siguiente manera:

```kotlin
private val adapter : HomeAdapter by inject { parametersOf(Model()) }
// or
private val adapter : HomeAdapter by inject { parametersOf(Model(), 2) }
```

Donde tu código debería verse así:

```kotlin  
import android.os.Bundle  
import androidx.appcompat.app.AppCompatActivity  
import kotlinx.android.synthetic.main.activity_home.*
import androidx.recyclerview.widget.LinearLayoutManager
import demo.android.R    

import org.koin.android.ext.android.inject  
import org.koin.core.parameter.parametersOf
  
class HomeActivity : AppCompatActivity() {

	private val presenter : HomePresenter by inject()
	private val homeAdapter : HomeAdapter by inject { parametersOf(Model()) }
  
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        setContentView(R.layout.activity_home)
        recyclerView.layoutManager = LinearLayoutManager(this)
        recyclerView.adapter = homeAdapter
    }   
}
```

### 7. Ejecutar tu aplicación

:red_circle: Tu aplicación esta lista!

Ejecuta tu app y mira la magia de **Koin** en tu proyecto!

### Autor: 
### [David Barbarán](https://github.com/DavidBarbaran) | **Android Developer** :octocat: 
