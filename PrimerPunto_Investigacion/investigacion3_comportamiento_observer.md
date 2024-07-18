## Solución

### Categoría: Comportamiento – Patrón de diseño Observer

### i. Propósito

Observer es un patrón de diseño de comportamiento que te permite definir un mecanismo de suscripción para notificar a varios objetos sobre cualquier evento que le suceda al objeto que están observando.

### ii. Aplicabilidad

:lady_beetle: Utiliza el patrón Observer cuando los cambios en el estado de un objeto puedan necesitar cambiar otros objetos y el grupo de objetos sea desconocido de antemano o cambie dinámicamente.

:zap: Explicación: Puedes experimentar este problema a menudo al trabajar con clases de la interfaz gráfica de usuario. Por ejemplo, si creaste clases personalizadas de botón y quieres permitir al cliente colgar código cliente de tus botones para que se active cuando un usuario pulse un botón.

El patrón Observer permite que cualquier objeto que implemente la interfaz suscriptora pueda suscribirse a notificaciones de eventos en objetos notificadores. Puedes añadir el mecanismo de suscripción a tus botones, permitiendo a los clientes acoplar su código personalizado a través de clases suscriptoras personalizadas.

:lady_beetle: Utiliza el patrón cuando algunos objetos de tu aplicación deban observar a otros, pero sólo durante un tiempo limitado o en casos específicos.

:zap: Explicación: La lista de suscripción es dinámica, por lo que los suscriptores pueden unirse o abandonar la lista cuando lo deseen.


### iii. Ejemplo en Java

- Observer: Define una dependencia uno-a-muchos entre objetos para que, cuando un objeto cambie de estado, todos sus dependientes sean notificados y actualizados automáticamente.

```
public interface Observer{
    void update();
}
public class ConcreteObserver implements Observer{
    @Override
    public void update() {
        System.out.println("Updated");
    }
}
public class Subject {
    private List <Observer> observers = new ArrayList<>();
    public void addObserver(Observer observer){
        observers.add(observer);
    }
    public void notufyObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }
}

```

- Para saber: en Spring, se puede utilizar ApplicationEvent y ApplicationListener.