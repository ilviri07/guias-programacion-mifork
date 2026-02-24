
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

En C no existen excepciones, por lo que el control de errores debe diseñarse explícitamente. Una primera opción consiste en devolver un valor especial que indique error. Por ejemplo, podría devolverse -1 o NAN cuando la función reciba un número negativo. El código llamador sería el encargado de comprobar el valor devuelto y actuar en consecuencia. Este enfoque es simple, pero obliga a que el llamador recuerde siempre verificar el resultado.

#include <stdio.h>
#include <math.h>

float raiz(float x) {
    if (x < 0) {
        return -1.0f;  // valor especial de error
    }
    return sqrtf(x);
}

int main() {
    float r = raiz(-4);
    if (r < 0) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}

Una segunda opción consiste en utilizar un parámetro adicional para indicar el estado del error (por ejemplo, mediante punteros). La función devuelve el resultado por un lado y el estado por otro. Esto evita ambigüedades si -1 pudiera ser un valor válido.

#include <stdio.h>
#include <math.h>

float raiz(float x, int *error) {
    if (x < 0) {
        *error = 1;
        return 0.0f;
    }
    *error = 0;
    return sqrtf(x);
}

int main() {
    int error;
    float r = raiz(-4, &error);
    if (error) {
        printf("Error: número negativo\n");
    } else {
        printf("Resultado: %f\n", r);
    }
}


## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

Una excepción es un mecanismo de control de errores que permite señalar que ha ocurrido una situación anómala durante la ejecución de un programa. En lugar de devolver un código de error, se genera un objeto especial que interrumpe el flujo normal del programa y busca un manejador adecuado.

El objetivo de las excepciones es separar el código principal de la lógica de tratamiento de errores. De este modo, las funciones pueden centrarse en su responsabilidad principal, y el tratamiento del error puede realizarse en un nivel superior. Esto mejora la claridad del código y evita la comprobación constante de valores de retorno.


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

En Java, el control de errores se realiza mediante excepciones. Puede definirse un método raiz dentro de una clase Calculadora que lance una excepción si el número es negativo. El control se realiza desde fuera utilizando try-catch.

class Calculadora {

    public double raiz(double x) {
        if (x < 0) {
            throw new IllegalArgumentException("Número negativo no permitido");
        }
        return Math.sqrt(x);
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();

        try {
            double resultado = calc.raiz(-4);
            System.out.println("Resultado: " + resultado);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}

En este caso, la función no devuelve un valor especial, sino que lanza una excepción. El método main decide cómo reaccionar ante ese error, lo que permite separar claramente la lógica de cálculo del control de errores.


## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

Lanzar una excepción significa crear un objeto excepción y enviarlo al sistema de ejecución mediante la palabra clave throw. Capturar o controlar una excepción significa interceptarla mediante un bloque catch para gestionar el error. La propagación ocurre cuando un método no captura la excepción y esta sube automáticamente al método que lo llamó.

Cuando se produce la excepción en raiz, la ejecución del método se interrumpe inmediatamente. Si el método que lo llamó no la captura, también se interrumpe, y así sucesivamente por la pila de llamadas. Cada método por el que pasa la excepción termina sin completar su ejecución normal.

Las funciones que no capturan la excepción no se reanudan después. Su ejecución termina abruptamente. En el ejemplo de la raíz, si main no tuviera try-catch, el programa finalizaría mostrando un mensaje de error generado por la máquina virtual.


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

La propagación natural de excepciones evita tener que comprobar manualmente códigos de error tras cada llamada, como ocurre en C. Esto reduce considerablemente la cantidad de código repetitivo y disminuye la probabilidad de olvidar verificar un error.

Además, permite que el tratamiento del error se realice en el nivel más adecuado. Una función intermedia no necesita conocer cómo manejar el error; simplemente deja que se propague. Esto favorece una mejor separación de responsabilidades y un diseño más limpio.


## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

En programación orientada a objetos, las excepciones son objetos. En Java, todas heredan de la clase Exception o RuntimeException. Esto significa que pueden contener atributos y métodos, igual que cualquier otra clase.

Gracias a la encapsulación, una excepción puede almacenar información relevante sobre el error, como un mensaje o datos adicionales. Esto permite diseñar excepciones personalizadas adaptadas a necesidades concretas.

Sí es posible crear excepciones propias heredando de Exception o RuntimeException. Esto resulta útil cuando se desea representar errores específicos del dominio del problema.



## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

Un objeto excepción lleva información esencial como un mensaje descriptivo del error y la traza de la pila (stack trace). Esta traza indica qué métodos estaban activos en el momento del error.

Esta información es muy valiosa cuando el error llega al manejador, ya que permite identificar exactamente dónde se produjo el problema. En C, este contexto no se obtiene automáticamente y debe reconstruirse manualmente.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

Sí es posible tener varios bloques catch asociados a un mismo try. Cada uno puede capturar un tipo distinto de excepción.

Sin embargo, solo se ejecuta un único bloque catch: el primero que coincida con el tipo de la excepción lanzada. Una vez ejecutado ese bloque, los demás no se evalúan.


## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

El bloque finally se utiliza para garantizar la ejecución de código que debe ejecutarse siempre, como cerrar ficheros o liberar recursos, independientemente de si ocurre una excepción.

Ejemplo con catch:

try {
    double r = calc.raiz(-4);
} catch (IllegalArgumentException e) {
    System.out.println("Error");
} finally {
    System.out.println("Liberando recursos");
}

Ejemplo sin catch:

try {
    double r = calc.raiz(-4);
} finally {
    System.out.println("Liberando recursos");
}


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

Sí, el bloque finally puede utilizarse sin catch. En ese caso, se combina con try, y la excepción seguirá propagándose tras ejecutar el finally.

El bloque finally se ejecuta siempre, tanto si ocurre una excepción como si no. Incluso si hay un return dentro del try, el código del finally se ejecuta antes de que el método retorne definitivamente.

## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

Las excepciones controladas (checked) son aquellas que el compilador obliga a capturar o declarar con throws. Las no controladas (unchecked) heredan de RuntimeException y no obligan a su manejo explícito.

Ejemplos de controladas:

IOException

FileNotFoundException

SQLException

Ejemplos de no controladas:

IllegalArgumentException

NullPointerException

ArithmeticException

Situaciones donde se prefieren controladas:

Acceso a ficheros.

Acceso a base de datos.

Comunicación por red.

Situaciones donde se prefieren no controladas:

Argumentos inválidos.

Errores de programación.

Violaciones de precondiciones.


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

throws se utiliza en la firma de un método para indicar que puede lanzar determinadas excepciones. Es obligatorio para excepciones controladas si no se capturan dentro del método.

Es alternativa a capturar la excepción porque permite delegar la responsabilidad del manejo al método llamador. De este modo, la excepción se propaga hacia arriba en la pila de llamadas.

## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

import java.io.*;

public class Lector {

    public void leerFichero(String nombre) throws IOException {
        FileReader fr = null;
        try {
            fr = new FileReader(nombre);
            // lectura
        } finally {
            if (fr != null) {
                fr.close();
            }
        }
    }
}

Aquí se declara throws IOException porque no se desea manejar el error dentro del método. Sin embargo, se utiliza finally para garantizar el cierre del recurso si fue abierto.


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

Sí es posible declarar excepciones no controladas en throws, como RuntimeException, pero no es obligatorio. El compilador no exige su declaración.

El método llamador no está obligado a usar try-catch en ese caso. Declararlas puede servir como documentación, pero no impone manejo obligatorio.


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

Se recomienda usar excepciones controladas cuando el error puede ser recuperable y depende de factores externos (ficheros, red). Se prefieren no controladas cuando el error indica un fallo de programación o una violación de contrato.

No todos los lenguajes distinguen entre ambas. En muchos lenguajes modernos solo existen excepciones no controladas. La opción más habitual fuera de Java es el modelo equivalente a excepciones no controladas.


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

Sí tiene sentido lanzar excepciones dentro de un catch. Puede capturarse una excepción y lanzar otra distinta más adecuada al nivel de abstracción.

También puede relanzarse la misma excepción usando throw e;. Esto tiene sentido cuando se desea registrar información adicional pero no cambiar el tipo de error.

try {
    double r = calc.raiz(-4);
} catch (IllegalArgumentException e) {
    System.out.println("Registrando error");
    throw e;
}


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

Una excepción puede tener como causa otra excepción. Esto permite encapsular un error de bajo nivel dentro de uno de mayor nivel, manteniendo la información original.

class ErrorCalculo extends Exception {
    public ErrorCalculo(String mensaje, Throwable causa) {
        super(mensaje, causa);
    }
}

try {
    double r = calc.raiz(-4);
} catch (IllegalArgumentException e) {
    throw new ErrorCalculo("Error en cálculo matemático", e);
}

Cuando se muestra por pantalla una excepción que tiene causa, la traza incluye también la excepción original, indicando claramente que fue la causa del error principal.

