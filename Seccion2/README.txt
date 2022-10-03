/* Variables */

- Trabajar con variables nos facilita el trabajo ya que si elementos que comparten un mismo color 
por ejemplo deben ser cambiados a otro color, solo deberiamos cambiar el valor de una variable
para que esos cambios se apliquen de manera masiva.

- Podemos asignar el contenido de variables en otras variables.

Ejemplo: @colorNaranja: orange;
         @colorTexto: @colorNaranja;


- Si una variable debe estar contenida dentro de comillas. La variable dentro de las comillas se
debe escribir de la siguiente manera @{nombreVariable}.

Ejemplo:

@pathImg: "web/images";

background-image: url("@{pathImg}/iconoTienda.png");


- Podemos hacer operaciones matematicas en los valores de las propiedades. Pero estos deben estar dentro
de parentesis para que la propiead css no los confunda como parametros.

Ejemplo:

@marginGeneral: 20px;

.content{
    margin: (@marginGeneral + 4); //Resultado 24px
}

.sub-content{
    width: (@marginGeneral / 2); //Resultado 10px
}

.parent-broth{
    margin: (@marginGeneral - 10); //Resultado 10px
}

.parent-broth{
    margin: (@marginGeneral * 2); //Resultado 40px
}

.operaciones-combinadas{
    margin: (@marginGeneral + 4) @marginGeneral ((@marginGeneral * 2) + (@marginGeneral / 2)) 12px;
                 1er valor         2do valor                       3er valor                  4to valor
}


- Tambien podremos obtener la longitud de una cadena de texto con .lenght de la siguiente manera:

@textContent: '"cadena de texto".lenght'; //PENDIENTE PARA VER NO FUNCIONA


/*--------------------------------------------------------------------------------------------------*/


/* Anidaciones */

- Las anidaciones es lo que nos permite less para poder crear selectores de manera automatica en css sin que tengamos
que repetir a mano los mismo selectores con algun agregado mas como alguna clase etiqueta o id.

Ejemplo:

.content{
    background-color: black;
    color: #FFF;
    p{
        color: red;
        font-weight: 600;
        span{
            font-size: 20px;
        }
    }
}

//CSS generado

.content {
  background-color: black;
  color: #FFF;
}
.content p {
  color: red;
  font-weight: 600;
}
.content p span {
  font-size: 20px;
}

- Si queremos indicar que todos los <p> con clase .text contenido por la clase .content tenga cierto estilo en css se veria asi:

.content p.text{
    font-family: 'Roboto';
}

-Pero en less para juntar el p con la clase .text lo hacemos anidando a <p> el '&' y despues la clase .text:

.content{
    p{
        &.text{
            font-family: 'Roboto';
        }
    }
}

- Tambien se suele utilizar mucho cuando tenemos que dar estilos a los pseudo elementos ::after y ::before:

Ejemplo malo:

.content{
    p{
        &.text{
            font-family: 'Roboto';
            ::before{
                content:'';
            }
        }
    }
}

//CSS generado malo

.content p.text {
  font-family: 'Roboto';
}
.content p.text ::before { /* esta mal porque el ::before esta separado de p.text */
  content: '';
}

Ejemplo bueno:

.content{
    p{
        &.text{
            font-family: 'Roboto';
            &::before{
                content:'';
            }
        }
    }
}

//CSS generado bueno

.content p.text { /* esta bien porque el ::before esta junto de p.text */
  font-family: 'Roboto';
}
.content p.text::before {
  content: '';
}

/*Metodos nativos de less para asignar a variables*/

cos(int);
ceil(float) /*redondea hacia arriba*/ // Ejemplo ceil(0.32px) el resultado es 1px
floor(float) /*redondea para abajo*/ // Ejemplo floor(0.32px) el resultado es 0px
darken(color, % de oscuridad) /*oscurece el color que le pasemos por parametro*/ //Ejemplo darken(#ffffff, 20%)
lighten(color, % de aclaracion) /*aclara el color que le pasemos por parametro*/
spin(color, grados) /* devuelve un color del circulo cromatico de colores ubicado segun los grados que le asignemos*/ //Ejemplo spin(#00ff00, 180) devuelve #ff00ff
fade(color, % de opacidad) /*devuelve la opcidad o transparencia de un color*/ // Ejemplo box-shadow: fade(#00ff00, 30%); devuleve rgba(0, 255, 0, 0.3)