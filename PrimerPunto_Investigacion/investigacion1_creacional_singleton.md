## Solución

### Categoría: Creacional - Patrón de diseño Singleton 

### i. Propósito

Singleton es un patrón de diseño creacional que nos permite asegurarnos de que una clase tenga una única instancia, a la vez que proporciona un punto de acceso global a dicha instancia.
El patrón tiene prácticamente los mismos pros y contras que las variables globales. Aunque son muy útiles, rompen la modularidad del código.
No se puede utilizar una clase que dependa del Singleton en otro contexto. Tendrás que llevar también la clase Singleton. La mayoría de las veces, esta limitación aparece durante la creación de pruebas de unidad.

### ii. Aplicabilidad

:lady_beetle: Utiliza el patrón Singleton cuando una clase de tu programa tan solo deba tener una instancia disponible para todos los clientes; por ejemplo, un único objeto de base de datos compartido por distintas partes del programa.

:zap: Explicación: El patrón Singleton deshabilita el resto de las maneras de crear objetos de una clase, excepto el método especial de creación. Este método crea un nuevo objeto, o bien devuelve uno existente si ya ha sido creado.

:lady_beetle: Utiliza el patrón Singleton cuando necesites un control más estricto de las variables globales.

:zap: Explicación: Al contrario que las variables globales, el patrón Singleton garantiza que haya una única instancia de una clase. A excepción de la propia clase Singleton, nada puede sustituir la instancia en caché.

Ten en cuenta que siempre podrás ajustar esta limitación y permitir la creación de cierto número de instancias Singleton. La única parte del código que requiere cambios es el cuerpo del método ```getInstance```.

### iii. Ejemplo en Java

- Singleton: asegura que una clase tonga solo una instancia y proporciona un punto de acceso global a ella.

```
public class Singleton{
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance(){
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

- Para saber: en Spring, los beans definidos con @Component, @Service, @Repository, o @Controller son singletons por defecto.