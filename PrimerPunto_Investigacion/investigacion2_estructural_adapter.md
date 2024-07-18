## Solución

### Categoría: Estructural - Patrón de diseño Adapter (También llamado: Adaptador, Envoltorio, Wrapper) 

### i. Propósito

Adapter es un patrón de diseño estructural que permite la colaboración entre objetos con interfaces incompatibles.
Este patrón actúa como un envoltorio entre dos objetos. Atrapa las llamadas a un objeto y las transforma a un formato y una interfaz reconocible para el segundo objeto.

### ii. Aplicabilidad

:lady_beetle: Utiliza la clase adaptadora cuando quieras usar una clase existente, pero cuya interfaz no sea compatible con el resto del código.

:zap: Explicación: El patrón Adapter te permite crear una clase intermedia que sirva como traductora entre tu código y una clase heredada, una clase de un tercero o cualquier otra clase con una interfaz extraña.

:lady_beetle: Utiliza el patrón cuando quieras reutilizar varias subclases existentes que carezcan de alguna funcionalidad común que no pueda añadirse a la superclase.

:zap: Explicación: Puedes extender cada subclase y colocar la funcionalidad que falta, dentro de las nuevas clases hijas. No obstante, deberás duplicar el código en todas estas nuevas clases, lo cual sería un problema.

Una solución mucho más elegante sería colocar la funcionalidad que falta dentro de una clase adaptadora. Después puedes envolver objetos a los que les falten funciones, dentro de la clase adaptadora, obteniendo esas funciones necesarias de un modo dinámico. Para que esto funcione, las clases en cuestión deben tener una interfaz común y el campo de la clase adaptadora debe seguir dicha interfaz. Este procedimiento es muy similar al del patrón Decorator.

### iii. Ejemplo en Java

El patrón Adapter finge ser una pieza redonda con un radio igual a la mitad del diámetro del cuadrado (en otras palabras, el radio del círculo más pequeño en el que quepa la pieza cuadrada).

Enunciado del ejemplo: Tenemos un sistema legacy que todos los ficheros que exporta son en XML y tenemos una aplicación que procesa ficheros en JSON para realizar procesamiento de datos. Ninguna de las aplicaciones pueden ser cambiadas ya que son utilizadas por más aplicaciones por lo que debemos de añadir un adapter.

Vamos a describir los pasos a seguir para crear nuestro adapter:

- Crear Interfaz Adapter

El primer paso para crear nuestro Adapter es crear una interfaz que sea el punto de entrada para transformar de un formato a otro.

```
interface  IDataAdapter {

  String convert(XMLToJSON xml) throws IOException;

}
```

- Definir la clase de lógica de nuestro Adaptador

En este punto vamos a añadir la lógica necesaria para convertir de XML a JSON. Vamos a definir una clase XML que se encargará de convertir XML a JSON.


```
public class XMLToJSON {

  public XMLToJSON(String xml) {
    this.xml = xml;
  }

  private final String xml;
  public String convertToJSONFromXML() throws IOException {

    //lógica para convertir a JSON

    XmlMapper xmlMapper = new XmlMapper();
    JsonNode node = xmlMapper.readTree(xml.getBytes());
    ObjectMapper jsonMapper = new ObjectMapper();
    return jsonMapper.writeValueAsString(node);

  }
}
```

- Implementar nuestra clase Adaptador

El paso final seeia la creación de una clase que implementa la interfaz que hemos creado antes que se encargará de llamar invocar a la clase que contiene la lógica de conversión. Es decir, nuestra clase adapter hará una llamada a convertToJson().

```
public class XmlToJsonAdapter implements IDataAdapter {

  private final XMLToJSON xmlToJSON;

  public XmlToJsonAdapter(XMLToJSON xml){
    this.xmlToJSON = xml;
  }

  public String convert(XMLToJSON xml) throws IOException {
    return this.xmlToJSON.convertToJSONFromXML();
  }
}
```

Una vez finalizada nuestra clase XmlToJsonAdapter, podríamos invocarlo desde nuestra clase principal de la siguiente manera:

```
public class Application {

  public static String XML_STRING =
      "<?xml version=\"1.0\" encoding=\"UTF-8\"?>" +
          "<root>" +
          "<firstName>John</firstName>" +
          "<lastName>Snow</lastName>" +
          "<age>25</age>" +
          "<spouse/>" +
          "<address>" +
          "<street>237 Harrison Street</street>" +
          "<city>Brooklyn, NY</city>" +
          "<state>New York</state>" +
          "<postalCode>11238</postalCode>" +
          "</address>" +
          "<phoneNumbers>" +
          "<type>mobile</type>" +
          "<number>212 555-3346</number>" +
          "</phoneNumbers>" +
          "<phoneNumbers>" +
          "<type>fax</type>" +
          "<number>646 555-4567</number>" +
          "</phoneNumbers>" +
          "</root>";

  public static void main(String[] args) throws IOException {

    XMLToJSON xmlToJSON = new XMLToJSON(XML_STRING);

    IDataAdapter adapter = new XmlToJsonAdapter(xmlToJSON);
    String json = adapter.convert(xmlToJSON);

    System.out.println(json);
  }
}
```

Esta implementación nos va a permitir respetar principios como responsabilidad única y un código abierto y extensible, cpermitiendo que se puedan crear sin ningún problema más conversores.