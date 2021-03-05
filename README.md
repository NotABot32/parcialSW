# Parcial práctico - Sección 4 - 202110

## Instrucciones

1. Haga un fork de este repositorio
2. Clone el repositorio bifurcado en su máquina virtual
3. Abra los proyectos en Netbeans
4. En Netbeans vaya a _Services > Databases > JavaDB_ y cree una base de datos que se llame _parcial_ (los demás campos déjelos en blanco)

## Punto 1 (30%). Persistencia

Esta aplicación tiene el propósito de gestionar la información de un conjunto de fincas de recreo.

(10%) Cree la entidad _FincaEntity_ en el paquete correspondiente. Una finca tiene un nombre, una extensión (en metros cuadrados), un municipio al cual pertenece, un clima promedio, un numero de habitaciones, una calificación en número de estrellas y un id de tipo _Long_ que representa su llave primaria.
 
(10%) Implemente la persistencia de la entidad.
 
(10%) Cree la prueba unitaria en la clase correspondiente para el método crear, la cual valida si está correcta la implementación de la persistencia de la entidad. Al ejecutar la prueba esta debe pasar correctamente.

## Punto 2 (40%). Lógica

Usted debe crear la lógica de aplicación que cubra las reglas de negocio para la entidad _FincaEntity_. Las reglas de negocio para crear una finca son:

* No pueden existir 2 fincas con el mismo nombre.
* El número de habitaciones debe ser un entero mayor de cero.

(20%) Crear el método en la capa de lógica que valide las reglas de negocio y solicita persistir en caso de que todas pasen (sólo para el método crear).

(20%) Crear al menos tres pruebas unitarias: una que valida el escenario ideal en que todas las reglas de negocio se aprueban, y otras dos en las que las reglas de negocio fallan. Si las reglas de negocio se cumplen, se debe llamar la persistencia para que el objeto sea persistido, de lo contrario debe lanzar una excepción _BusinessLogicException_ con un mensaje donde se especifique el problema.

## Punto 3 (30%). Pruebas de integración

(5%) Cree la clase _FincaDTO_ con los atributos correspondientes, los getters, los setters y un constructor vacío.
 
(5%) Cree el método toEntity que retorna un objeto _FincaEntity_ con los datos del objeto _FincaDTO_.
 
(5%) Agregue el método constructor que recibe un _FincaEntity_ y haga el mapeo correspondiente entre ambas clases.
 
(5%) Modifique en la clase _FincaResource_ el método createFinca para que llame al método de la lógica que crea la entidad, y retorne al usuario el nuevo objeto creado.

(10%) Haga las pruebas de Postman para la creación de un nuevo recurso. En repositorio cree una carpeta “images” y suba allí las pruebas. Deberá haber mínimo tres pruebas, una donde se cree correctamente el recurso y otras dos donde falle la creación por violación a las reglas de negocio. 

### Prueba 1. Creación correcta de una finca:

```
Method: POST
URL: http://localhost:8080/s1_parcial-api/api/fincas
Body:
{
    "nombre": "Finca la Esperanza",
    "municipio": "Calarcá",
    "clima": 20,
    "habitaciones": 7,
    "calificacion": 5
}
Response: 200
```

### Prueba 2. Creación incorrecta por número de habitaciones no válido:

```
Method: POST
URL: http://localhost:8080/s1_parcial-api/api/fincas
Body:
{
    "nombre": "Finca la Esperanza",
    "municipio": "Calarcá",
    "clima": 20,
    "habitaciones": -4.9,
    "calificacion": 5
}
Response: 414
```

## Entrega

1. Agregue los pantallazos de las pruebas de Postman a la carpeta images de su repositorio

2. Haga commit y push a la rama master de su repo

3. Cree un release de su código con el nombre "Parcial1_S1_2603". 

4. Suba el archivo zip del release como respuesta a la evaluación en Brightspace
