# Regular-expression
 A simple guide on how to use regular expressions in java scrip
 
 La manipulación de textos es una actividad casi inseparable en el desarrollo de aplicaciones. En muchas ocasiones necesitamos realizar una o varias acciones si se cumplen determinadas condiciones, pero muchas veces esas condiciones no son tan triviales. En estas circunstancias es donde las **expresiones regulares** juegan su papel. Las **expresiones regulares** son un lenguaje utilizado para describir patrones en cadenas de caracteres. Forman un pequeño y separado lenguaje dentro de la mayoría de muchos de los lenguajes ya existentes. No es un lenguaje fácil de leer, pero es una herramienta muy poderosa que simplifica mucho tareas de procesado de cadenas de caracteres. En este artículo les muestro una pequeña introducción a esta poderosa herramienta.

En **Java Script** se pueden crear expresiones regulares utilizando una *notación literal* o *notación de objeto*:

```JavaScript
//literal notation
let re = /aa/i
//object notation
let re = new RegExp('aa', 'i')
```
También se puede utilizar las dos formas combinadas de esta manera:

```JavaScript
let re = new RegExp(/aa/, 'i')
```

En los dos casos se establece la expresión regular ```aa``` con el atributo o **flag** ```i```.

## Propiedades
Las expresiones regulares, como cualquier otro objeto consta de una serie de propiedades, a continuación se muestran algunas de las más importantes:

1. ```.source``` Retorna un string con la expresión regular creada.
2. ```.flag``` Retorna un string con los atributos asignados a la expresión regular.
3. ```.global``` Comprueba si el atributo ```g``` esta activado.
4. ```.ignoreCase``` Comprueba si el atributo ```i``` esta activado.
5. ```.multiline``` Comprueba si el atributo ```m``` esta activado

Los atributos o **flag** en las expresiones regulares se definen después del último ```/``` en el caso de la notación literal, o como segundo parámetro en el caso de la notación de objeto. A continuación algunos atributos y su funcionamiento:

1. ```i``` o ```ignoreCase``` Se emplea para discriminar mayúsculas y minúsculas.
2. ```g``` o ```global``` Se define cuando se desea realizar una búsqueda global, osea seguir buscando hasta la última coincidencia.
3. ```m``` o ```multiline``` Permite que los operadores de inicio y fin (```^``` , ```$```) traten los finales de linea ```\n``` o ```\r```. 
4. ```u``` o ```unicode``` Interpreta el patrón como un código unicode.

## Métodos

Los dos métodos fundamentales de las expresiones regulares son:

1. ```test(str)``` Retorna ```true``` si coincide en la expresión regular con ```str``` o ```false``` encaso contrario.
2. ```exec(str)``` Retorna un ```array``` con las coincidencias encontradas.

## Caracteres especiales

Dentro de una expresión regular se pueden emplear ciertos caracteres que hacen a la expresión regular más específica.

1. ```.``` Especifica cualquier carácter.
2. ```^``` Delimita el inicio del patrón.
3. ```$``` Delimita el fin del patrón.
4. ```[]``` Especifica un rango de caracteres.
5. ```[^]``` Especifica que no exista ninguno de los caracteres del rango.
6. ```|``` Establece lo que esta a la izquierda o lo que esta a la derecha.
7. ```*``` El carácter anterior puede aparecer 0 o más veces.
8. ```+``` El carácter anterior puede aparecer 1 o más veces.
9. ```?``` El carácter anterior puede aparecer o no aparecer.
10. ```{n}``` El carácter anterior puede aparecer n veces.
11. ```{n,}``` El carácter anterior puede aparecer n o más veces.
12. ```{n,m}``` El carácter anterior puede aparecer de n a m veces.
13. ```(x)``` Se captura el patrón x y se guarda una o sucesivas veces.
14. ```(?:x)``` No se captura el patrón x.
15. ```x(?=y)``` Se captura solo si x esta seguido de y.
16. ```x(?!y)``` Se captura solo si x no esta seguido de y.
17. ```\``` Invierte el significado de un carácter.
18. ```\t``` Tabulador.
19. ```\r``` Retorno de carro **CR**.
20. ```\n``` Retorno de linea **LF**.
21. ```\d``` Un dígito de 0 a 9.
22. ```\D``` No exista dígito de 0 a 9.
23. ```\w``` Letra mayúscula, minúscula o dígito.
24. ```\W``` No exista letra mayúscula, minúscula o dígito.
25. ```\s``` Espacio en blanco (**ESPACE**, **TAB**, **LF** o **FF**).
26. ```\S``` No exista espacio en blanco (**ESPACE**, **TAB**, **LF** o **FF**).
27. ```\xN``` Carácter hexadecimal número **N**.
28. ```\uN``` Carácter unicode número **N**.

### Veamos algunos ejemplos

Declararemos la siguiente expresión regular:
```JavaScript
let  re = /.i.e/i
```
Ahora comprobaremos empleando el método ```test()``` la coincidencia en los siguientes casos:

```JavaScript
re.test('life') //true
re.test('wifi') //false
re.test('wife') //true
re.test('DIVE') //true (i permite mayúsculas/minúsculas)
```

Si se desea que un carácter especial forme parte del patron se procede de la siguiente manera:

```JavaScript
//Buscando coincidencias con ".com"

/.com/.test('.com') // true (Tener en cuenta que el punto es comodín)
/.com/.test('acom') //true (Da true con cualquier cosa delante)
/\.com/.test('.com') //true (Solución correcta)
/\.com/.test(acom) //false
```

### Ejemplos con ```[] [^] |```

```JavaScript
let re = /[ae]/i

re.test('a') //true
re.test('E') //true por el i
re.test('Z') //false

re = /[^ae]/i
re.text('a') //false
re.text('e') //false
re.test('Z') //true

re = /dog|foot/
re.test('dog') //true
re.test('DOG') //false
re.test('foot') //true
re.test('fot') //false
```

### Veamos un ejemplo cuando la búsqueda es en el inicio o en el final de una cadena.

```JavaScript
let re = /^co/i
re.test('solution') //false (no empieza con "co")
re.test('code') //true

re = /ing$/i;
re.test('run') //false (no termina en ing)
re.test('running') //true 
```

Si queremos buscar textos después de *espacios*, *comas* o *puntos* o simplemente limites de palabras utilizamos ```\b```.

```JavaScript
let re = /od\b/
re.test('The good doctor.') //true (después de good hay espacio)

re = /go\d/
re.test('The good doctor.') //false (después de go sigue la palabra)
 
re = /end\b/
re.test('The end') //true (luego de end termina la cadena)

re.test('The end.') //true (luego de end hay un signo de puntuación)
```

### Veamos como aplicar ```* + ? {n} {n,} {n,m}```
```JavaScript
let re = /a*/

re.test('') //true el carácter anterior aparece 0 veces
re.test('a') //true el carácter anterior aparece 1 vez
re.test('aba') //true el carácter anterior aparece 2 veces
re.test('bcd') //true el carácter anterior aparece 0 veces 
```

```JavaScript
let re = /a+/
re.test('') //false el carácter anterior aparece 0 veces
re.test('a') //true el carácter anterior aparece 1 vez
re.test('aba') //true el carácter anterior aparece 2 veces
re.test('bcd') //false el carácter anterior aparece 0 veces 
```

Cuando se desea indicar que no es relevante que aparezca un carácter opcional se usa ```?```.
```JavaScript
let re = /doctors?/i

re.test('The good doctors.') //true
re.test('The good doctor.') //true
re.test('The good boy') // false
``` 

Si se requiere especificar exactamente el número de repeticiones se utilizan ```{n} {n,} {n, m}```.
```JavaScript
//Número formado por tres dígitos o más

let re = /\d{3}/
re.test(12) //false
re.test(123) //true
re.test(1234) //true
```

Para especificar un numero exactamente de n dígitos lo único que haría falta seria limitar el patrón:

```JavaScript
let re = /^\d{3}$/
re.test(12) //false
re.test(123) //true
re.test(1234) //false

//tres o mas dígitos
re = /^\d{3,}$/

re.test(12) // false
re.test(1234) // true

//entre 2 y 4 dígitos
re = /^[0-9]{2,4}$/

re.test(1) // false
re.test(123) // true
re.test(1234) //true
re.test(12345) // false
```

  Note que se puede utilizar tanto ```\d``` como ```[1-9]``` para referirse a cualquier dígito de 0 a 9.

El método ```exec(src)``` muy parecido al método ```indexOf(src)``` nos permite encontrar coincidencias dentro de ```src```. Si no se establece el atributo ```g``` la búsqueda sera hasta la primera coincidencia. Al establecer el atributo ```g``` el método retornará distinto de ```null``` mientras existan coincidencias.

```JavaScript
//Todas las palabras de 5 letras
let re = /\b([a-z]{5})\b/ig;
let str = "Lorem ips dolor sit, amet consectetur adipisicing elit."

let res = re.exec(str)
while(res !== null){
	res = re.exec(str);
}

//Output

[
    "Lorem", 
    "Lorem", 
     index: 0, 
     input: "Lorem ips dolor sit, amet consectetur adipisicing elit.", 
     groups: undefined
]
[
    "dolor", 
    "dolor", 
    index: 10, 
    input: "Lorem ips dolor sit, amet consectetur adipisicing elit.", 
    groups: undefined
]
```

También se puede utilizar el método ```match``` pasándola la expresión regular como argumento y se obtendrá un resultado similar.

```JavaScript
let re = /\b([a-z]{5})\b/ig;
let str = "Lorem ips dolor sit, amet consectetur adipisicing elit."

str.match(re)

//Output
["Lorem", "dolor"]
```

Otro método que utiliza expresiones regulares es el método ```replace()```.

```JavaScript
let str = "The god doctor"
str.replace(/[aeou]/, 'gi') // Thi gid dictir
```
Existen muchos más métodos que usan expresiones regulares, te invito a descubrirlos.

### Como último ejemplo veremos algo más práctico. Un patrón para analizar url.

```JavaScript
let parse_url = /^(?:([A-Za-z]+):)?(\/{0,3})([0-9.\-A-Za-z]+)(?::(\d+))?(?:\/([^?#]*))?(?:\?([^#]*))?(?:#(.*))?$/

let url1 = "http://www.ora.com:80/goodparts?q#fragment"

let url2 ="https://api.edamam.com/search/search?q=pollo&app_id=82&app_key=d65"

let result = parse_url.exec(url1)
 
let names = ['url', 'scheme', 'slash', 'host', 'port', 'path', 'query', 'hash'];
 
for (let i = 0; i < names.length; i += 1) {
    document.writeln(names[i] + ':\n', result[i]);
}

//Output
url1:
    url: http://www.ora.com:80/goodparts?q#fragment
    scheme: http
    slash: //
    host: www.ora.com
    port: 80
    path: goodparts
    query: q
    hash: fragment

url2:
    url: https://api.edamam.com/search/search?q=pollo&app_id=82&app_key=d65
    scheme: https
    slash: //
    host: api.edamam.com
    port: undefined
    path: search/search
    query: q=pollo&app_id=82app_key=d6592
    hash: undefined
```
