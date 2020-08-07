# Transacciones y control de concurrencia

## Sistemas de Gestión de Bases de Datos
Son sistemas encargados de gestionar el almacenamiento, mantenimiento y consulta de datos. Su principal característica es la concurrencia con la que es requerida las operaciones dentro de ellos manteniendo la integridad de sus datos almacenados.

## Transacciones SQL
Es un conjunto de operaciones hacia determinada base de datos con el objetivo que se asegure el procesamiento correcto de dichas operaciones en su totalidad, es decir "todas" o "ninguna", esto hace referencia al tema de atomicidad. Está deliminada por instrucciones "begin-transaction" y  "end-transaction". 

Existen dos operaciones en SQL dentro de las transacciones. Commit y Rollback. El primero de ellos confirma y e indica la finalización de una transacción satisfactoria, el segundo es una instrucción que indica que una transacción no fue completada correctamente y debe de deshacer los cambios realizados que no estén confirmados, es decir hasta un estado anterior de la base de datos.

Las transacciones poseen cuatro propiedades básicas (ACID)

![d](https://lh3.googleusercontent.com/proxy/FrE-iDoCFiijyV0QOggMdZaqUm-HMLOFQQUtxHkniSFO1G8Ueu97ygGUpCZXCowq8PPgNidYQz71lhAZvbzmtNYLwraabWg_MT4UMFJnFL5VWk33sa4ObtQ29oAd)

### Atomicity
En un conjunto de operaciones dentro de la base de datos esta propiedad asegura que esa secuencia se complete de manera correcta en su totalidad, si hubiese algún problema abandona las operaciones y retrocede a un estado anterior.

### Consistency
Hace referencia a la integridad de los propios datos. Esta propiedad asegura que las transacciones llevan de un estado válido de la base datos a otro estado igualmente válido. También permite asegurar que los datos son exactos y consistentes, es decir que al solicitar cierta información siempre sea la misma si no se ha realizado ningún cambio explícito, y de esa manera resguardar que los datos no se deformen o cambien.

### Isolation
Esta propiedad asegura que diferentes transacciones u operaciones al sistema de base de datos sean independientes y transparentes entre ellas mismas, sin afectar su objetivo.

### Durability
Asegura que una operación realizada de manera exitosa persistirá y no se perderá aunque el sistema falle.

## Log de transacciones
La bitácora de transacciones almacena todos los movimientos que se realicen la base de datos, describiendo el tipo de operación, fecha y hora, e información correspondiente al tipo de operación. 

## Sincronización o chequeo
Un punto de confirmación es un punto la base de datos está o debería estar en un estado consistente. Por ejemplo, al finalziar una transacción o unidad de trabajo lógica la base de datos debe de cambiar a un nuevo estado consistente, es ese punto.

## Concurrencia
Hace referencia que un sistema de base de datos permita recibir múltiples transacciones a la vez y como gestiona sus operaciones. Existen 3 problemas de concurrencia

![d](https://userscontent2.emaze.com/images/90131698-d9b5-419e-9424-8c020cd32d33/e1300486d36da72c3efe64b859ee1f3c.jpg)

1. El problema de la actualización perdida. 
Este problema hace referencia cuando dos transacciones T1 y T2 acceden a los mismos datos, y tienen operaciones que modifiquen esos datos de manera intercalada, lo que podría anular una operación a otra, o hacer uso de algún dato incorrecto.

2. El problema de la dependencia no confirmada
Este problema hace referencia cuando una transacción T1 actualiza un elemento X y luego necesita hacer un rollback, pero otra transacción T2 también tiene acceso a ese elemento X "antes" que se restaure el valor original de X.

3. El problema del análsis inconsistente
Cuando una transacción T1 calcula mediante alguna operación o función agregada sobre varios registros, mientras eso sucede otras transacciones acutalizan los registros que se está utilizando en la transacción T1, es posible que la primera transacción tome valores antes de que sean actualizados o después.

## Bloqueos
Un bloqueo es una restricción o exclusividad para una transacción en específico, es decir que se asegura que durante esa transacción el estado de la base de datos no cambiará mientras se ejecuta dicha transacción.

## Deadlock
Es la situación en la que un conjunto de transacciones se encuentran en estado de espera, mientras los objetos objetivos de cada transacción estén en estado libre provocado por un bloqueo.