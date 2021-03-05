# Parcial práctico - Sección 4 - 202110

## Instrucciones

1. Haga un fork de este repositorio
2. Clone el repositorio bifurcado en su máquina virtual
3. Abra los proyectos en Netbeans
4. En Netbeans vaya a _Services > Databases > JavaDB_ y cree una base de datos que se llame _parcial_ (los demás campos déjelos en blanco)

## Punto 1 (30%). Persistencia

Esta aplicación tiene el propósito de gestionar la información de un marketplace de cafés especiales.

(10%) Cree la entidad _CafeEntity_ en el paquete correspondiente. Un café tiene un nombre, una descripción, un peso (en gramos), el nombre del productor, una presentación (grano o molido), un lote de producción y un id de tipo _Long_ que representa su llave primaria.
 
(10%) Implemente la persistencia de la entidad.
 
(10%) Cree la prueba unitaria en la clase correspondiente para el método crear, la cual valida si está correcta la implementación de la persistencia de la entidad. Al ejecutar la prueba esta debe pasar correctamente.

## Punto 2 (40%). Lógica

Usted debe crear la lógica de aplicación que cubra las reglas de negocio para la entidad _CafeEntity_. Las reglas de negocio para crear un café son:

* No pueden existir 2 cafés con el mismo nombre.
* El peso debe ser un número entero mayor o igual a 250.
* Las únicas presentaciones válidas son "grano" o "molido".

(20%) Crear el método en la capa de lógica que valide las reglas de negocio y solicita persistir en caso de que todas pasen (sólo para el método crear).

(20%) Crear al menos tres pruebas unitarias: una que valida el escenario ideal en que todas las reglas de negocio se aprueban, y otras dos en las que las reglas de negocio fallan. Si las reglas de negocio se cumplen, se debe llamar la persistencia para que el objeto sea persistido, de lo contrario debe lanzar una excepción _BusinessLogicException_ con un mensaje donde se especifique el problema.

## Punto 3 (30%). Pruebas de integración

(5%) Cree la clase _CafeDTO_ con los atributos correspondientes, los getters, los setters y un constructor vacío.
 
(5%) Cree el método toEntity que retorna un objeto _CafeEntity_ con los datos del objeto _CafeDTO_.
 
(5%) Agregue el método constructor que recibe un _CafeEntity_ y haga el mapeo correspondiente entre ambas clases.
 
(5%) Modifique en la clase _CafeResource_ el método createCafe para que llame al método de la lógica que crea la entidad, y retorne al usuario el nuevo objeto creado.

(10%) Haga las pruebas de Postman para la creación de un nuevo recurso. En repositorio cree una carpeta “images” y suba allí las pruebas. Deberá haber mínimo tres pruebas, una donde se cree correctamente el recurso y otras dos donde falle la creación por violación a las reglas de negocio. 

### Prueba 1. Creación correcta de una finca:

```
Method: POST
URL: http://localhost:8080/s4_parcial-api/api/cafes
Body:
{
    "nombre": "Café Juanambú",
    "descripción": "El Café Juanambú se caracteriza por ser 100% café colombiano. Nuestro café proviene de las mejores regiones productoras del país."
    "peso": 500,
    "productor": "Orlando Perdomo Escandón",
    "presentacion": "molido",
    "lote": "LT2513830"
}
Response: 200
```

### Prueba 2. Creación incorrecta por presentación no válida:

```
Method: POST
URL: http://localhost:8080/s4_parcial-api/api/cafes
Body:
{
    "nombre": "Café Juanambú",
    "descripción": "El Café Juanambú se caracteriza por ser 100% café colombiano. Nuestro café proviene de las mejores regiones productoras del país."
    "peso": 500,
    "productor": "Orlando Perdomo Escandón",
    "presentacion": "En grano",
    "lote": "LT2513830"
}
Response: 414
```

### Prueba 3. Creación incorrecta por peso no válido:

```
Method: POST
URL: http://localhost:8080/s4_parcial-api/api/cafes
Body:
{
    "nombre": "Café Juanambú",
    "descripción": "El Café Juanambú se caracteriza por ser 100% café colombiano. Nuestro café proviene de las mejores regiones productoras del país."
    "peso": 157.3,
    "productor": "Orlando Perdomo Escandón",
    "presentacion": "grano",
    "lote": "LT2513830"
}
Response: 414
```

## Entrega

1. Agregue los pantallazos de las pruebas de Postman a la carpeta images de su repositorio

2. Haga commit y push a la rama master de su repo

3. Cree un release de su código con el nombre "Parcial1_S4_2603". 

4. Suba el archivo zip del release como respuesta a la evaluación en Brightspace
