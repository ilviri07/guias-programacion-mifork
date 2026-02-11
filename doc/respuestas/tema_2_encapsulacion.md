
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

En Programación Orientada a Objetos, la encapsulación y la ocultación de información buscan separar el “qué hace” un objeto del “cómo lo hace”. Esto significa que los detalles internos de una clase (datos y lógica interna) no deben ser accesibles directamente desde el exterior, sino únicamente a través de una interfaz bien definida.

La ocultación de información permite que los atributos internos no puedan ser modificados de forma arbitraria desde otras partes del programa. En lugar de acceder directamente a los datos, se obliga a utilizar métodos que controlan cómo se consultan o modifican.

Entre las ventajas principales se encuentran: mayor robustez del programa, facilidad de mantenimiento, reducción de errores al evitar usos indebidos de los datos, y posibilidad de cambiar la implementación interna sin afectar al resto del código. Además, favorece un diseño más claro y modular.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

La interfaz pública de una clase es el conjunto de métodos y miembros accesibles desde el exterior, es decir, aquellos declarados como public. Esta interfaz define cómo otras clases pueden interactuar con los objetos de dicha clase.

Desde el punto de vista de la encapsulación, la interfaz pública actúa como un contrato: se garantiza que esos métodos estarán disponibles y funcionarán según lo esperado, mientras que los detalles internos permanecen ocultos.

La ocultación de información se apoya en esta idea, ya que solo se expone lo estrictamente necesario. Todo aquello que no forme parte de la interfaz pública puede cambiarse sin afectar a las clases que usan el objeto.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

Es importante diseñar cuidadosamente la interfaz pública de una clase porque es la parte visible y dependiente para el resto del programa. Una mala decisión en esta interfaz puede provocar dependencias innecesarias o usos incorrectos del objeto.

Cambiar la interfaz pública no suele ser fácil, ya que cualquier modificación puede obligar a cambiar todo el código que utiliza esa clase. Esto es especialmente problemático en proyectos grandes o librerías reutilizables.

Por este motivo, se recomienda exponer pocos métodos, bien definidos, y evitar mostrar detalles internos. Una interfaz pequeña y clara facilita la evolución del programa a largo plazo.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

Las invariantes de clase son condiciones que deben cumplirse siempre para que un objeto esté en un estado válido. Por ejemplo, que una coordenada no sea negativa o que un contador no baje de cero.

La ocultación de información ayuda a mantener estas invariantes porque impide que el estado interno sea modificado directamente desde fuera. De este modo, solo los métodos de la propia clase pueden cambiar los datos, y pueden hacerlo de forma controlada.

Gracias a esto, se reduce el riesgo de que un objeto quede en un estado inconsistente, algo similar a proteger estructuras internas en C usando funciones en lugar de acceso directo.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

public class Punto {
    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}
En este ejemplo, la clase Punto encapsula dos coordenadas internas (x e y) que no son accesibles directamente desde fuera. Esto evita que otras clases modifiquen los valores sin control.

La interfaz pública de la clase está formada por el constructor y el método calcularDistanciaAOrigen. Son los únicos puntos de acceso permitidos.

La palabra clave public indica que un miembro es accesible desde cualquier clase, mientras que private indica que solo puede usarse dentro de la propia clase. Esto es la base de la ocultación de información en Java.


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

En Java, los modificadores public y private se pueden aplicar a clases, atributos, métodos y constructores. Sin embargo, las clases de nivel superior solo pueden ser public o tener visibilidad por defecto.

Aplicar estos modificadores permite controlar qué partes del código son accesibles desde otras clases y cuáles permanecen ocultas. Esto es especialmente importante para los atributos.

Gracias a estos modificadores, Java ofrece un control de acceso más explícito que C, donde la ocultación suele depender de convenciones y archivos .h.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

Además de public y private, existen otros tipos de visibilidad. En Java existen cuatro: public, private, protected y visibilidad por defecto (package-private).

La visibilidad protected permite el acceso desde subclases, y la visibilidad por defecto limita el acceso al mismo paquete. Esto proporciona un control más fino que solo público o privado.

En otros lenguajes, como C++, existen mecanismos similares (public, private, protected). En lenguajes más dinámicos, la ocultación puede ser más flexible o basada en convenciones.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

Los miembros privados están ocultos para otras clases, pero no para otras instancias de la misma clase. Una instancia puede acceder a los atributos privados de otra instancia del mismo tipo.

public double calcularDistanciaAPunto(Punto otro) {
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}


En este ejemplo, aunque x e y son privados, se pueden acceder desde otra instancia porque el acceso ocurre dentro de la misma clase.

Esto permite implementar operaciones entre objetos sin romper la encapsulación, ya que el acceso sigue estando controlado por la propia clase.


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

Los métodos getter y setter son métodos públicos que permiten leer o modificar atributos privados. Un getter devuelve el valor de un atributo, y un setter permite cambiarlo.

Estos métodos actúan como un punto de control, donde se pueden validar valores o mantener invariantes antes de modificar el estado interno del objeto.

Su uso es preferible al acceso directo a los atributos, ya que permite cambiar la implementación interna sin afectar al código cliente.


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

Cuando se dice que la ocultación de información mejora la “seguridad” del programa, no se refiere a seguridad informática ni a evitar ataques externos.

Se refiere a la seguridad lógica del código, es decir, a evitar usos incorrectos, estados inválidos o modificaciones no deseadas de los datos internos.

Es una forma de protección frente a errores de programación, no frente a ataques maliciosos.

## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

Un miembro de instancia pertenece a cada objeto individual, mientras que un miembro de clase pertenece a la clase en sí y es compartido por todas las instancias.

En Java, los miembros de clase se declaran con la palabra clave static. Estos miembros también pueden ser private o public.

Por tanto, los miembros de clase también pueden ocultarse, y la encapsulación se aplica igualmente a ellos.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

Sí tiene sentido que los constructores sean privados en ciertos casos. Esto se utiliza cuando se quiere controlar estrictamente la creación de objetos.

Por ejemplo, en patrones como Singleton o cuando se emplean métodos factoría, el constructor privado impide crear instancias directamente.

De esta forma, se refuerza la encapsulación incluso en la fase de creación de objetos.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

public class Punto {
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
        maxX = Math.max(maxX, x);
        maxY = Math.max(maxY, y);
    }
}
Los miembros de clase se indican con static. En este caso, maxX y maxY almacenan información global a todos los objetos Punto.

Estos valores se actualizan cada vez que se crea un nuevo punto, permitiendo conocer los máximos históricos.

Aunque son de clase, siguen estando encapsulados gracias a private.


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

public static Punto crearRedondeado(double x, double y) {
    return new Punto(Math.round(x), Math.round(y));
}
Este método es un método factoría porque crea objetos sin usar directamente el constructor desde fuera.

Se ha utilizado static porque el método no pertenece a una instancia concreta, sino a la clase Punto.

Este enfoque permite controlar cómo se crean los objetos y aplicar lógica adicional.


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

private double[] coordenadas = new double[2];
Al usar un array interno, la representación cambia, pero si los métodos públicos siguen siendo los mismos, la interfaz pública no se modifica.

Gracias a la encapsulación, el código cliente no se ve afectado por este cambio. Solo la implementación interna se ha alterado.

Esto demuestra uno de los beneficios clave de la ocultación de información.


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

Aunque un atributo tenga getter y setter, no es recomendable declararlo público. Hacerlo público elimina cualquier control futuro.

La convención más habitual es declarar todos los atributos como privados y acceder a ellos mediante métodos.

Esto está directamente relacionado con las invariantes de clase, ya que los setters pueden validar valores antes de modificar el estado.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

Una clase inmutable es aquella cuyos objetos no pueden cambiar de estado una vez creados. No existen métodos que modifiquen sus atributos.

Un método modificador es aquel que cambia el estado del objeto. No todos los métodos modificadores son setters, ya que pueden tener otro nombre o lógica.

Las clases inmutables tienen ventajas como mayor seguridad, facilidad de razonamiento y uso seguro en entornos concurrentes.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

No es recomendable incluir setters siempre por convención. Cada setter expone una forma de modificar el estado interno.

En muchos casos, permitir modificaciones arbitrarias rompe invariantes o genera dependencias innecesarias.

Se recomienda añadir setters solo cuando realmente tenga sentido desde el punto de vista del diseño.


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

La clase String en Java es inmutable. Al concatenar dos cadenas, se crea un nuevo objeto String.

Esto implica que concatenar repetidamente puede ser ineficiente en términos de memoria y rendimiento.

Para concatenaciones repetidas, se debe usar StringBuilder o StringBuffer, que son mutables.


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

En POO, los objetos pueden compararse por identidad o por contenido. La identidad indica si son el mismo objeto en memoria.

El método equals en Java permite comparar por contenido. Por defecto, equals se comporta igual que ==, comparando referencias.

Las cadenas en Java deben compararse usando equals, no con ==, para comparar su contenido.


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

Las clases wrapper envuelven tipos primitivos en objetos, por ejemplo int → Integer.

En Java, este proceso puede ser automático mediante autoboxing. Estas clases permiten tratar valores primitivos como objetos.

No todos los lenguajes necesitan wrappers; algunos no distinguen entre tipos primitivos y objetos.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

Un tipo enumerado representa un conjunto finito de valores posibles. En Java, un enumerado es una clase especial.

Los enumerados en Java pueden tener atributos, métodos y constructores privados.

Esto mejora la encapsulación al asociar comportamiento y datos a cada valor posible.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado. Añade además cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

public enum Mes {
    ENERO(31, 1), FEBRERO(28, 2), MARZO(31, 3), ABRIL(30, 4),
    MAYO(31, 5), JUNIO(30, 6), JULIO(31, 7), AGOSTO(31, 8),
    SEPTIEMBRE(30, 9), OCTUBRE(31, 10), NOVIEMBRE(30, 11), DICIEMBRE(31, 12);

    private int dias;
    private int ordinal;

    private Mes(int dias, int ordinal) {
        this.dias = dias;
        this.ordinal = ordinal;
    }

    public int getDias() {
        return dias;
    }

    public int getOrdinal() {
        return ordinal;
    }

    public boolean esDePrimavera(boolean hemisferioNorte) {
        return hemisferioNorte ? (this == MARZO || this == ABRIL || this == MAYO)
                               : (this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE);
    }

    public boolean esDeVerano(boolean hemisferioNorte) {
        return hemisferioNorte ? (this == JUNIO || this == JULIO || this == AGOSTO)
                               : (this == DICIEMBRE || this == ENERO || this == FEBRERO);
    }

    public boolean esDeOtoño(boolean hemisferioNorte) {
        return hemisferioNorte ? (this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE)
                               : (this == MARZO || this == ABRIL || this == MAYO);
    }

    public boolean esDeInvierno(boolean hemisferioNorte) {
        return hemisferioNorte ? (this == DICIEMBRE || this == ENERO || this == FEBRERO)
                               : (this == JUNIO || this == JULIO || this == AGOSTO);
    }
}
