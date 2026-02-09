

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

La programación orientada a objetos se basa en cuatro características fundamentales. La primera es la abstracción, que consiste en representar entidades del mundo real mediante modelos simplificados que contienen solo la información relevante para el problema que se desea resolver. Esto permite centrarse en el qué hace un objeto, más que en cómo lo hace internamente.

La encapsulación implica agrupar datos y comportamiento en una misma unidad (el objeto) y controlar el acceso a sus componentes internos. La herencia permite crear nuevas clases a partir de otras existentes, reutilizando y ampliando su comportamiento. Por último, el polimorfismo permite tratar objetos de distintas clases de forma uniforme, siempre que compartan una misma interfaz o comportamiento común.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

Existen numerosos lenguajes que soportan la programación orientada a objetos. Entre los más populares se encuentra Java, que está diseñado específicamente bajo este paradigma y lo aplica de forma estricta. Otro ejemplo es C++, que permite programación orientada a objetos, aunque también admite estilos procedimentales y estructurados.

También destacan Python, que ofrece orientación a objetos de forma flexible y sencilla, y C#, muy utilizado en el entorno .NET, con un modelo de clases similar al de Java. Todos ellos permiten definir clases, crear objetos y aplicar los principios básicos de la POO.


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

La programación estructurada es un paradigma basado en la organización del código mediante estructuras de control bien definidas, como secuencias, condicionales y bucles. Su objetivo principal es evitar el uso de saltos incontrolados (como goto) y mejorar la legibilidad y mantenibilidad del código, algo muy común en C.

La programación modular va un paso más allá y propone dividir el programa en módulos o bloques independientes, cada uno con una responsabilidad concreta. En C, estos módulos suelen corresponder a ficheros .c y .h, lo que facilita la reutilización y el trabajo en equipo. Sin embargo, los datos y las funciones siguen estando separados, a diferencia de la POO.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

Un objeto en programación orientada a objetos se define por tres elementos clave. El primero es su estado, que viene determinado por los valores de sus atributos o variables internas en un momento dado. Este estado representa la información que almacena el objeto.

El segundo elemento es su comportamiento, que está formado por los métodos que definen qué operaciones puede realizar el objeto. El tercero es su identidad, que permite distinguir un objeto de otro, incluso aunque ambos tengan el mismo estado. Esta identidad suele estar asociada a su posición en memoria.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

Una clase es una plantilla o molde que define cómo serán los objetos: qué atributos tendrán y qué métodos podrán ejecutar. No representa un elemento concreto, sino una definición abstracta. Un objeto, en cambio, es una entidad concreta creada a partir de una clase.

El proceso de crear un objeto a partir de una clase se denomina instanciación, y el objeto resultante se llama instancia de esa clase. Aunque la mayoría de lenguajes orientados a objetos utilizan clases, existen lenguajes basados en prototipos (como JavaScript) que no emplean clases en el sentido tradicional.


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

En Java, los objetos se almacenan dinámicamente en una zona de memoria llamada heap. Las variables no contienen el objeto en sí, sino una referencia a él. Este modelo es distinto al de C/C++, donde se puede decidir explícitamente si una estructura vive en la pila o en memoria dinámica.

La recolección de basura (garbage collection) es un mecanismo automático que se encarga de liberar la memoria de los objetos que ya no se usan. En Java, el programador no libera memoria manualmente, lo que reduce errores como fugas de memoria o accesos inválidos, a cambio de perder control directo sobre la gestión de memoria.


## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

Un método es una función asociada a una clase y que define una operación que pueden realizar sus objetos. A diferencia de las funciones en C, los métodos operan normalmente sobre los atributos del propio objeto al que pertenecen.

La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre dentro de una clase, pero con distinta lista de parámetros. El compilador decide cuál usar según el número y tipo de argumentos proporcionados. Esto permite usar nombres coherentes sin perder flexibilidad.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

Una clase en Java se define con la palabra clave class e incluye atributos y métodos. En este ejemplo se representa un punto en un plano mediante dos coordenadas x e y, y un método que calcula su distancia al origen.

class Punto {
    double x;
    double y;

    double calculaDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}

class Prueba {
    public static void main(String[] args) {
        Punto p = new Punto();
        p.x = 3;
        p.y = 4;
        double d = p.calculaDistanciaAOrigen();
        System.out.println(d);
    }
}


Se crea una instancia con new, se asignan valores a sus atributos y se invoca el método usando el operador punto, de forma similar a acceder a campos de un struct, pero con comportamiento asociado.


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

El punto de entrada de un programa en Java es el método main, cuya firma es fija. Este método se ejecuta sin necesidad de crear un objeto, lo que explica el uso de la palabra clave static, que indica que el método pertenece a la clase y no a una instancia.

static no se utiliza solo en main, también puede aplicarse a atributos y otros métodos compartidos por todas las instancias. Cuando se combina con final, se indica que el valor no puede cambiar (en atributos) o que el método no puede ser redefinido, lo que resulta útil para constantes o comportamientos fijos.

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

Para compilar un programa Java desde la línea de comandos se utiliza javac, que transforma el código fuente .java en archivos .class. Para ejecutar el programa se emplea el comando java, indicando la clase que contiene el método main.

Java es un lenguaje compilado e interpretado: el código se compila a byte-code, que no es código máquina nativo, sino un formato intermedio. Este byte-code es ejecutado por la máquina virtual de Java (JVM), lo que permite que el mismo programa funcione en distintos sistemas sin recompilar.


## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

La palabra clave new se utiliza para crear un nuevo objeto en memoria y obtener una referencia a él. Durante este proceso se invoca automáticamente un constructor, que es un método especial encargado de inicializar el objeto.

Un constructor tiene el mismo nombre que la clase y no devuelve ningún valor. Por ejemplo:

class Empleado {
    String dni;
    String nombre;
    String apellidos;

    Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;
        this.nombre = nombre;
        this.apellidos = apellidos;
    }
}


## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

La referencia this apunta al objeto actual, es decir, a la instancia sobre la que se está ejecutando un método. Se utiliza para acceder a los atributos del objeto y para evitar ambigüedades cuando los parámetros tienen el mismo nombre.

El nombre this no es universal: en C++ se utiliza this, pero en otros lenguajes puede variar. Un ejemplo en la clase Punto sería:

double distanciaA(Punto otro) {
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

Método distanciaA

Este nuevo método recibe otro objeto Punto como parámetro y calcula la distancia entre ambos puntos usando la fórmula euclídea. Se emplea this para referirse al punto actual.

double distanciaA(Punto otro) {
    double dx = this.x - otro.x;
    double dy = this.y - otro.y;
    return Math.sqrt(dx * dx + dy * dy);
}


Este enfoque muestra cómo los objetos interactúan entre sí pasando referencias como parámetros, algo fundamental en la POO.


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

En Java, los parámetros siempre se pasan por valor, pero es importante matizar. Cuando se pasa un objeto, lo que se copia es la referencia, no el objeto en sí. Por tanto, modificar los atributos del objeto dentro del método afecta al objeto original.

En cambio, cuando se pasa un tipo primitivo como int, se copia directamente su valor. Si se modifica dentro del método, el cambio no se refleja fuera, ya que se trabaja sobre una copia independiente.


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

toString() es un método que existe en todas las clases de Java, ya que se hereda de Object. Su función es devolver una representación en forma de texto del objeto, útil para depuración o salida por pantalla.

Otros lenguajes tienen mecanismos similares, como operadores de conversión a cadena. Un ejemplo en Punto sería:

public String toString() {
    return "Punto(" + x + ", " + y + ")";
}


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?

Una clase se parece a un struct en C en el sentido de que ambos agrupan datos relacionados. Sin embargo, el struct solo contiene datos, mientras que la clase integra datos y comportamiento en una misma unidad.

Además, las clases incorporan conceptos como encapsulación, constructores, control de visibilidad y herencia. Para que un struct se comportase como una clase, sería necesario asociarle funciones, controlar el acceso a sus campos y definir un ciclo de vida del objeto, cosas que C no ofrece de forma nativa.


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

Una clase como Punto puede emularse en C usando un struct para los datos y una función que opere sobre él. El struct contiene los campos x e y, y la función recibe dicho struct (normalmente por puntero) para calcular la distancia al origen.

typedef struct {
    double x;
    double y;
} Punto;

double calculaDistanciaAOrigen(const Punto *p) {
    return sqrt(p->x * p->x + p->y * p->y);
}


En este caso, this no existe como concepto del lenguaje. Su papel lo cumple el parámetro p, que se pasa explícitamente a la función. En Java ese paso es implícito al llamar a un método; en C debe hacerse de forma manual.
