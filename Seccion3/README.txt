// Mixins no parametricos

- Son bloques de estilos que podremos reutilizar en cualquier parte de nuestros archivos.
- Primero creamos un bloque de estilos con alguna clase como selector sea que exista o no.
- Y los llamamos desde otro selector con el nombre del bloque, despues parentesis y punto y coma.
- Se los llama no parametricos ya que no reciben valores por parametros en los parentesis.

Por ejemplo:

// creamos el mixin
.bloque-div{
    width: 400px;
    height: 400;
    background-color: brown;
}

.content{
    .bloque-div(); //lo reutilizamos los estilos de .bloque-div
}

// Y se generara en siguiente codigo css

.bloque-div {
  width: 400px;
  height: 400;
  background-color: brown;
}

.content {
  width: 400px;
  height: 400;
  background-color: brown;
}

*Aclaracion: los estilos mixins tambien se veran reflejados en el archivo css

//------------------------------------------------------------------------------------------------

Mixins no parametricos

- Vienen ser lo mismo que los no parametricos con la diferencia que estos reciben valores por parametros.

Por ejemplo:

- Creamos un mixins parametricos

.texts(@font, @background, @color, @weight){ //en el parentesis los valores que mandamos por parametro
    font-family: @font;
    background-color: @background;
    color:@color;
    font-weight: @weight;
}

- Y luego si escribimos el siguiente codigo:

.text-parametrico-1{ //en esta clase llamamos al mixins creado arriba
    .texts('Roboto', rgb(85, 231, 85), rgb(230, 213, 213), 800);
}

- En el css lo veremos de la siguiente forma:

.text-parametrico-1 {
  font-family: 'Roboto';
  background-color: #55e755;
  color: #e6d5d5;
  font-weight: 800;
}

- Tambien podemos hacer mixins que al no recibir valores por paratros estos tengan valores por defecto
actuando como mixins no parametricos:

Por Ejemplo:

.defaults(@color: red, @font-size: 14px, @background: purple){ // parametros con valores ya asignados por defecto
    color: @color;
    font-size: @font-size;
    background-color: @background;
}

- Lo llamamos dentro de una clase sin pasarle valores:

.por-defecto{
    .defaults();
}

- Y el resultado seria el siguiente:

.por-defecto {
  color: red;
  font-size: 14px;
  background-color: purple;
}

//----------------------------------------------------------------------------------------------------------------------------------------------

Condicionales mediante el valor que se pase por parametro o la cantidad de parametros

- Consiste en que dependiendo del valor que pasemos por parametro a un mismo mixin se aplicara un mixin u otro

Por Ejemplo:

.block(temaverde;){ // si pasamos por parametro el valor "temaverde" se aplicaran los siguientes estilos
    background-color: #4acf60;
    color: #4acf60;
    border: 1px solid #4acf60;
}

.block(temaazul){ // si pasamos por parametro el valor "temaazul" se aplicaran los siguientes estilos
    background-color: #1d44c5;
    color: #1d44c5;
    border: 1px solid #1d44c5;
}

Aplicacion:

.header{
    .block(temaverde);
}

.fooder{
    .block(temaazul);
}

Resultado:

.header {
  background-color: #4acf60;
  color: #4acf60;
  border: 1px solid #4acf60;
}
.fooder {
  background-color: #1d44c5;
  color: #1d44c5;
  border: 1px solid #1d44c5;
}


- Tambien podemos diferenciar mixins segun la cantidad de parametros que pasemos

Por Ejemplo:

.style(temaverde;){ // Recibe un parametro osea que para llamar a este mixin debemos pasar un solo valor por parametro
    background-color: #4acf60;
    color: #4acf60;
    border: 1px solid #4acf60;
}

.style(temaazul; @color){ // Recibe dos parametros osea que para llamar a este mixin debemos pasar dos valores por parametro
    background-color: @color;
    color: @color;
    border: 1px solid @color;
}

Resultado:

.home {
  background-color: #4acf60;
  color: #4acf60;
  border: 1px solid #4acf60;
}
.menu {
  background-color: #ce6f6f;
  color: #ce6f6f;
  border: 1px solid #ce6f6f;
}




Condicionales mediante el "WHEN"

- Este condicional es mas explicito y se utiliza como un if de los lenguajes de programacion.
- Operadores que se admiten dentro de las condiciones <, >, <=, >= y =.

- Nomenclatura : 

  .nameMixin(@var(opcional)) when (condición){
    propiedades css
  }

- *PARTICULARIDAD : Si al crear el mixin, le declaramos una variable por parametro que se llame igual a una variable declarada con un valor ya asignado de la misma unidad de medida,
va a tomar como valor de comparacion en la condicion al valor que le pasemos por parametro.

- Ejemplo caso con mismo nombre de variable :

En archivo LESS

@width: 500px;

.desktop(@width) when (@width <= 100px){ //El nombre de la variable que pasamos por parametro es igual que el de la variable que se encuentra arriba. En este caso, dentro de la condicion, el @width es el valor que pasamos por parametro y no el que se declaro en la parte superior de esta linea
    background-color: rgb(200, 255, 0);
}

.prueba{
    .desktop(50px);
}

Archivo CSS generado

.prueba {
  background-color: #c8ff00;
}



- Ejemplo caso con distinto nombre de variable :

@myalto: 500px;
.desktop1(@alto) when (@myalto <= 100px){
    background-color: rgb(200, 255, 0);
}

.altura{
    .desktop1(50px);
    text-align: center;
}




TIPOS DE CONDICIONALES 

Tradicional

.desktop1(@var(opcional)) when (@myalto <= 100px){
    //contenido
}

El que funciona como un OR || se aplicaran los estilos si se cumple alguna de la dos condiciones

.desktop(@var(opcional)) when (@width >= 768px), (@width <= 1400px){
    //contenido
}

El que funciona como un AND && se aplicaran los estilos si se cumple con las condiciones especificadas.

.desktop(@var(opcional)) when (@width >= 768px) and (@width <= 1400px){
    //contenido
}

Para que esta condicion se cumpla, en este when la condicion (@width >= 768px) debe cumplirse. Y la condicion (@width = 5000px) no debe cumplirse ya que esta indicado a su izquierda por un not. 

.desktop(@var(opcional)) when (@width >= 768px) and not (@width = 5000px){
   //contenido
}