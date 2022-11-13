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