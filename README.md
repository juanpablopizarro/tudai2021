# Trabajo Practico
## TUDAI 2021

Crear una funcion que dada una cadena con un formato determinado genere una instancia de una estructura con los valores de los campos correspondientes al formato de la cadena. Por ejemplo:

````
TX03ABC
````

Deberá generar una estructura con los siguientes valores:

````
{TX 3 ABC}
````

Donde la estructura deberá tener una definicion del tipo:

```golang
type Result struct {
    Type    string 
    Value   string
    Length  int
}
```

La cadena de caracteres tiene el siguiente formato:

* los primeros dos caracteres son el tipo
* los segundos dos caracteres son el largo del valor
* los siguientes N caracteres son el valor, donde N es el valor del bullet anterior.

Entonces `NN040001` equivale a:

````
Type=NN
Length=04
Value=0001
````

## Consideraciones
* Agregar test de unidad
* Se espera una cobertura del 80% o mas
* Tener en cuenta distintos casos para los test, por ejemplo cadenas inválidas.
* Usar go modules (`go mod`)
* Entregar un repositorio de github publico con el `README.md` que explique la solucion que hicieron
* Se pueden hacer grupos de 2 o 3 integrantes.

## Tests
Para ejecutar tests con el mismo codigo pero con varios casos de prueba se puede generar un dataset de la siguiente forma:

```golang
func TestParser(t *testing.T) {
	var cases = []struct {
		Input   string // input string in order to be parsed
		Success bool   // paser result
		Type    string // the input type
		Value   string // the input value
		Length  int    // value length
	}{
		{"TX02AB", true, "TX", "AB", 2},
		{"NN100987654321", true, "NN", "0987654321", 10},
		{"TX06ABCDE", false, "", "", 0},
		{"NN04000A", false, "", "", 0},
	}

	for _, testData := range cases {
		r, err := ParseString([]byte(testData.Input))
        // acá agregar chequeos propios del test por ejemplo:
        // assert.Equal(t, err == nil, testData.Success)
	}
}
```