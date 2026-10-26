# PREAVISO

No añadas funcionalidades ni textos que no se pidan en esta especificación. Se permiten los textos solicitados, las etiquetas necesarias para identificar controles y unidades, y mensajes breves de validación, carga o error.

# INTRODUCCIÓN Y DESCRIPCIÓN DE LA APP

Haz una app de cambio de divisas en un solo archivo index.html. El usuario elegirá una divisa origen y una divisa destino e introducirá una cantidad mediante un teclado numérico tipo calculadora que permita sumar, restar, multiplicar y dividir. La app consultará el tipo de cambio en la API de Frankfurter, calculará la conversión en el navegador y mostrará el resultado. Debajo aparecerá una gráfica de datos históricos.

# GRÁFICA DE DATOS HISTÓRICOS

La gráfica será lineal. La fecha inicial predeterminada será el 9 de agosto del año de la petición menos diez y la fecha final será el día de la petición. Ambas fechas podrán modificarse.

Si no existe cobertura para el par desde la fecha inicial predeterminada, esta se ajustará a la primera fecha con datos comunes. La fecha inicial debe ser anterior a la final y la final no puede superar el día actual. Los límites se basarán en los datos disponibles para el par, no en las fechas de creación de las monedas.

Haz una consulta por rangos. La gráfica mostrará cuánto vale una unidad de la divisa origen en la divisa destino. Utilizará todas las observaciones disponibles del rango, ordenadas por fecha, sin inventar cotizaciones para días sin datos. El eje horizontal representará fechas y el vertical, el tipo de cambio.

Justo debajo se mostrarán el mínimo y el máximo de las observaciones recibidas, con sus fechas. Si un extremo se repite, se indicará la primera fecha en que aparece.

Cambiar una fecha válida actualizará automáticamente la gráfica. El rango elegido se conservará en conversiones posteriores. Si el nuevo par tiene una cobertura menor, se ajustará la fecha inicial al primer dato disponible. Si el rango queda sin fechas válidas o no contiene datos, se mostrará un mensaje para que el usuario lo cambie.

Cuando origen y destino coincidan, la gráfica será una línea constante en 1, con mínimo y máximo iguales a 1, sin consultar tipos de cambio.

# DIVISAS Y CAMBIO

Se podrá hacer un cambio entre cualquier divisa que tenga la API de Frankfurter. Los desplegables mostrarán inicialmente «Selecciona divisa», sin monedas preseleccionadas.

Calcula la conversión en el navegador a partir del tipo de cambio obtenido. Ante dudas, contradicciones o ambigüedades sobre la integración con la API, sigue la documentación oficial de Frankfurter.

Si se selecciona la misma divisa de origen y destino, la conversión se calculará localmente con un tipo de cambio de 1, sin consultar tipos de cambio.

Se aceptará cero. Se permitirán resultados intermedios negativos, pero la cantidad final que se convierta no podrá ser negativa. La división por cero impedirá continuar.

No se redondearán los cálculos intermedios ni los tipos de cambio. Las cantidades monetarias mostradas se redondearán a dos decimales. Las cotizaciones y los extremos de la gráfica conservarán suficientes cifras significativas para evitar mostrar como cero un valor positivo.

# INTERFAZ Y FUNCIONAMIENTO

Primera pantalla: Se mostrará el título «INTRODUCE UNA CANTIDAD». Debajo habrá un campo para introducir la cantidad base, con un texto de ejemplo que desaparecerá al enfocar el campo, al mismo tiempo que aparecerá el teclado de calculadora. Se podrán introducir cantidades enteras y decimales. Justo debajo habrá dos desplegables, uno al lado del otro, para seleccionar las divisas de origen y destino, separados por una flecha que apunte hacia la divisa destino. Debajo habrá un botón con el texto «REALIZAR CAMBIO».

Al pulsar «REALIZAR CAMBIO», se resolverá cualquier operación completa pendiente y, si la cantidad y las divisas son válidas, se realizará la conversión. Tras la primera conversión correcta se pasará a la segunda pantalla con animaciones suaves y fluidas, estilo Apple.

Segunda pantalla: El campo original se transformará en un recuadro cuadrado destacado con el resultado de la conversión. Aparecerá un nuevo campo de cantidad base que conservará la cantidad utilizada y permitirá introducir otra distinta. Se mantendrán los desplegables y el botón de confirmación. Debajo del botón aparecerán la gráfica histórica, sus controles de fechas y los valores mínimo y máximo.

Las conversiones posteriores actualizarán la segunda pantalla. Cambiar una cantidad o divisa requerirá pulsar «REALIZAR CAMBIO»; los resultados anteriores se ocultarán mientras no correspondan a la selección actual.

La carpeta ejemplo-frontend contiene dos imágenes orientativas de las pantallas. Si contradicen esta especificación, prevalecerá spec.md.

# OPERACIONES DE TECLADO

Las operaciones se resolverán secuencialmente, como en una calculadora básica: 2 + 3 × 4 = 20. Al pulsar otro operador se resolverá la operación pendiente. Si todavía no se ha introducido el segundo operando, el nuevo operador sustituirá al anterior.

«REALIZAR CAMBIO» resolverá cualquier operación completa antes de convertir. Las operaciones incompletas impedirán la conversión.

El teclado incluirá dígitos, separador decimal, los cuatro operadores, igual, borrar último carácter y limpiar. Se mostrará al enfocar el campo y se ocultará al pulsar fuera o confirmar una conversión válida. También se permitirá usar el teclado físico, aceptando coma o punto como separador decimal.

# ERRORES

Se mostrarán mensajes breves para entradas inválidas, división por cero, fechas inválidas, falta de datos y fallos de conexión. Si falla una consulta, se conservarán los valores introducidos y no se mostrará un resultado incorrecto ni perteneciente a otra selección.

# FRONTEND

Estilo de app bancaria moderna y elegante, con bordes redondeados, colores oscuros (negros) y amarillo como color de realce. Sin emojis. Tipografía sans serif condensada.

Animaciones dinámicas, suaves y modernas, con motion graphics y efectos de liquid glass y metálicos.

# ARCHIVO Y DEPENDENCIAS

La app se entregará únicamente en index.html, con HTML, CSS y JavaScript integrados. No cargará bibliotecas, fuentes ni otros recursos externos; las únicas peticiones externas serán a Frankfurter. Usará una fuente condensada del sistema cuando esté disponible y una alternativa sans serif en caso contrario.
