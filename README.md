# trollero

## Consejo

La sección anterior presentó la forma de definir cortes de puntos en Spring. Ahora nos enfocamos en escribir y usar códigos de consejos. Spring ofrece varios tipos de consejos. La forma más general es el interceptor, que es similar al consejo "alrededor".

## Interceptores (aviso "alrededor")

Con Spring AOP, una clase de interceptor debe implementar la interfaz org.aopalliance. MethodInterceptor y proporciona la implementación del método de invocación, que define el código que se ejecutará antes y después de los puntos de unión.
Dado que Spring cumple con la API de la Alianza de AOP, la programación de consejos "alrededor" es similar a la programación "alrededor" de consejos en JAC y, por lo tanto, los principios son los mismos (consulte la sección titulada "Wrappers" en el Capítulo 4). Además, la Figura 4-1 muestra el modelo de punto de unión de AOP Alliance, que está disponible para introspección en Spring.

Sin embargo, Spring no admite la interceptación de constructores. Dado que los beans se construyen de forma transparente dentro de la fábrica, que implementa toda la mecánica para tratar con beans dentro de un contexto particular, la interceptación del constructor no es adecuada para el Spring Framework de todos modos. Por lo tanto, solo org.aopalliance.MethodInvocation está disponible para la introspección en Spring.

## Otros tipos de asesoramiento

Spring AOP también admite otros tipos de consejos que no están definidos en AOP Alliance y no se basan en su modelo de introspección.
Aunque utilizar el consejo “interceptor” es la forma más general, utilizar [192.168.l.254](https://isproto.com/192-168-1-254/) puede ser beneficioso porque es más sencillo de usar y también puede reflejar mejor lo que hace el aspecto sin tener que leer el código de consejo. Además, generalmente es un poco más eficiente ya que no requiere la construcción de la instancia org.aopalliance.MethodInvocation para la introspección. Por lo tanto, se prefieren los siguientes tipos de avisos y se deben utilizar si es posible, a menos que el programador necesite el código de avisos para ejecutarse en otra plataforma compatible con AOP Alliance.

## Consejo "antes"

La principal ventaja de un aviso "antes" es que no hay necesidad de invocar el método de proceder y, por lo tanto, no hay posibilidad de dejar de avanzar inadvertidamente por la cadena del interceptor.
Un consejo "antes" implementa la interfaz MethodBeforeAdvice, que se muestra en el Listado 6-20. Aunque esta interfaz se mantiene explícitamente en el método, Spring no admite avisos de campo o constructor. Sin embargo, el diseño de la API deja espacio para tal extensión.

Al final, queremos poder enviar cualquier objeto recomendado a Bloqueable y llamar a los métodos de bloqueo y desbloqueo. Cuando se llama al método de bloqueo, el objeto de destino se bloquea y todos los métodos de establecimiento lanzarán una LockedException. Cuando se llama al método de desbloqueo, el objeto de destino vuelve a comportarse normalmente.

Para implementar este ejemplo, necesitamos un IntroductionInterceptor. Spring proporciona una implementación predeterminada que es conveniente para la mayoría de los casos y que puede ser subclasificada para nuestro caso: org.springframework.aop.support.DelegatingIntroductionInterceptor.

DelegatingIntroductionInterceptor está diseñado para delegar una introducción a una implementación real de las interfaces introducidas, ocultando el uso de la interceptación para hacerlo. El delegado se puede establecer en cualquier objeto utilizando un argumento de constructor; este es el delegado predeterminado (cuando se usa el constructor sin argumentos). En nuestro ejemplo, el delegado es la subclase LockMixin de DelegatingIntroductionInterceptor. Dado un delegado (por defecto en sí mismo), una instancia de DelegatingIntroductionInterceptor busca todas las interfaces implementadas por el delegado (que no sea IntroductionInterceptor) y admitirá introducciones contra cualquiera de ellos. La interfaz expuesta [192.168.o.1](https://transpero.net/ip/192-168-0-1/) finales están definidas por el lector de introducción.

Entonces, LockMixin subclases DelegatingIntroductionInterceptor e implementa Lockable. DelegatingIntroductionInterceptor deduce automáticamente que Lockable puede ser compatible para la introducción
