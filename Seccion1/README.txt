/*Comentarios*/

En los archivos .less se pueden escribir comentarios con '//' el cual nos permite escribir comentarios solo de una linea.
Y estos comentarios no seran visibles cuando se generen los .css.

Ejemplo:

//escribiendo mi comentario en una sola linea sin salto de linea

Luego tenemos los comentarios con '/**/' el cual nos permite realizar comentarios de una sola linea o en linea multiples.
Y estos comentarios si seran visibles cuando se generen los .css.

Ejemplo:

/*comentario en una sola linea*/

/*
    comentario
    en 
    lineas
    multiples
*/

/*--------------------------------------------------------------------------------------------------*/

/*Variables en archivos .less*/

- Se declaran comenzando con un '@' y el nombre por ejemplo @colorRojo.
- Luego ':' y el valor de alguna propiedad css que queramos que tenga la variable.
- Estas se pueden reutilizar las veces que queramos.

Ejemplos: 

@background: blue;
@fontSize: 14px;
@displayFlex: flex;


/*--------------------------------------------------------------------------------------------------*/

/*Importaciones de archivos .less dentro de un .less*/

- Podemos importar todo el contenido de distintos archivos .less dentro de otro archivo .less.
- Pero al momento de realizar las importaciones es importante tener en cuenta el orden en el que 
importamos estos archivos.
- Ya que si por ejemplo importamos primero un .less donde se aplican estilos a un boton y luego importamos un .less
donde tenemos declarados la variables las cuales usa el .less que importamos anteriormente, los estilos no seran
aplicados porque se estan utilizando variables que aun no han sido traidas.
- Para realizar la importacion dentro de un archivo .less primero debemos escribir la palabra reservada '@import', 
a continuacion entre comillas el nombre del archivo .less asi 'variables.less' y luego el punto y coma ';'.


Ejemplo para importar archivos .less dentro de otro archivo .less y en orden correcto:

@import 'fuentes.less';
@import 'variables.less';
@import 'estilos.less';

Ejemplo de importaciones en el orden incorrecto:

@import 'estilos.less'; /* si este archivo es llamado antes que los demas, los estilos no seran aplicados ya que esta utilizando variables y fuentes que aun no fueron llamados */
@import 'fuentes.less';
@import 'variables.less';


- No necesariamente debemos importar los archivos .less al inicio de los archivos, sino tambien podemos importarlos donde queramos o
importarlos dentro de los selectores que precisemos y ese selector tendra acceso a las variables y sera padre de los estilos que contenga ese less 
dependiendo si ese less este importado de manera general o no.
- Si tenemos un import general y otro dentro de un selector y los dos tienen nombre de variables iguales, quien tendra mas prioridad es la variable que
se encuentra dentro del .less importado en el selector.

Ejemplo:

@import 'fuentes.less';
@import 'variables.less';
@import 'estilos.less'; /* tiene variable @verdeBancor */

.content-especifico{
    .import-especifico{
        @import 'especifico.less'; /* solo se tiene acceso a variables como @verdeBancor pero la variable de este import tendra mas prioridad */
        background-color: @verdeBancor;
    }
}

Ejemplo 2:

@import 'fuentes.less';
@import 'variables.less';

.content-especifico{
    .import-especifico{
        @import 'especifico.less'; /* si este import no esta declarada de manera ganeral los estilos que contenga este less seran hijos del actual selector y tomara con priorodad sus variables */
        background-color: @verdeBancor;
    }
}