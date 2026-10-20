## Punto 2 – Conocer la aplicación--  
1. ¿Qué archivo contiene la regla de cálculo?
El archivo que contiene la regla de calculo es el archivo src/services/precios.ts, donde se encuentra la función calcularPrecioFinal, encargada de aplicar el descuento al precio original

2. ¿Qué archivo define la ruta HTTP?
EL archivo que define la ruta HTTP es el archivo src/app.ts, que utiliza Express.js para definir las rutas y manejar las solicitudes HTTP

3. ¿En qué se diferencian sus responsabilidades?
En lo que se diferencian sus responsabilidades es precios.ts que se encarga de la lógica de negocio, es decir, calcular el precio final. En cambio, app.ts recibe las solicitudes HTTP, llama a la función correspondiente y devuelve una respuesta al cliente

## 3. Ejecutar las pruebas disponibles-- 

1. ¿Qué comportamiento exige la prueba calcularPrecioFinal(1000, 150)?
El comportamiento que exige la prueba es que la función rechace los descuentos superiores al 100 % y lance un error de tipo RangeError, ya que ese porcentaje no es válido

2. ¿Qué hace realmente el código?
Lo que hace realmente el codigo que la función actualmente no valida el porcentaje de descuento. Por eso, cuando recibe un precio de 1000 y un descuento del 150 %, realiza el cálculo y devuelve -500 en lugar de lanzar un error

## 4. Interpretar la falla
1. ¿Qué total devuelve actualmente un descuento del 150 % sobre $1.000?
El total que devuelve actualmente un descuento del 150 % sobre $1.000 es -500, porque calcula un descuento de $1.500 sobre el precio original de $1.000
2. ¿Por qué ese resultado no cumple la regla de negocio?
Este resultado no cumple la regla de negocio porque un descuento no debería superar el 100 % del precio original. Al permitir un 150 %, la función genera un precio negativo, que no es válido

3. ¿Por qué la prueba falla si la función terminó de ejecutarse?
La prueba falla porque espera que la función lance un error de tipo RangeError, pero el código realiza el cálculo y devuelve -500 sin generar ningún error. Por eso, el resultado no coincide con el comportamiento esperado

## 5. Corregir la función de cálculo


## 6. Agregar pruebas unitarias
1. ¿La validación actual lo rechaza?
La validacion actual si lo rechaza porque utiliza Number.isFinite(precio) para verificar que el precio sea un número finito. Al detectar NaN, lanza un RangeError, evitando realizar el cálculo con un valor inválido

## 7. Primera prueba de integración HTTP
1. ¿Por qué esta comprobación es de integración y no solamente una prueba unitaria?
Porque comprueba el funcionamiento conjunto de la ruta HTTP de Express y el servicio de cálculo. Verifica que, al enviar un descuento inválido del 150 %, la API responda con el código HTTP 400 y un mensaje de error, en lugar de probar únicamente la función de cálculo

## 8. Diferenciar pruebas y verificación de tipos
1. ¿Por qué conviene utilizar tanto typecheck como npm test?
Porque ambos permiten detectar errores diferentes. typecheck verifica que los tipos de datos utilizados en TypeScript sean correctos, mientras que npm test comprueba que las funciones y rutas de la aplicación se comporten como se espera. Utilizar ambos ayuda a mejorar la calidad y confiabilidad del software 

