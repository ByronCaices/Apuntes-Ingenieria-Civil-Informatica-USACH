#
#
# Concurrencia y sincronización
-  Problemas de sincronización pueden ocurrir tanto en multi y mono procesador
```
typedef struct list {

	int data;
	struct list *next;
} Lista;

//Toda la funcion insert es seccion critica debido a que es pequeña por lo que puedo externalizar mis mecanismos de sincronización

void insert(int item) { 

	struct list *p;
	p = malloc(sizeof(struct list)); //El system call debe ser thread-safe de lo contrario seria SC
	p->data = item;
	p->next = Lista; //read
	Lista = p; //write
	// Si no existiera ese write, no hay SC
	
}
```
Función es correcta si no tuviera multithread 

Cuando dos hebras 
#### Condición de carrera: 
Competencia entre hebras y el resultado de estas acciones que realizan depende del orden en que se ejecuten las hebras.
	
	"En mi código hay tal condición de carrera"
#### Sincronización: 
Método o protocolo para que se acceda de forma segura a los datos

#### Sección crítica:
Trozo de código ejecutado por múltiples hebras en el cual está la condición de carrera (se accede a datos compartidos y al menos una de las hebras escribe sobre los datos)
Suele ser un código no atómico compuesto de muchas interrupciones

- **No hay SC si:**
	- Ninguna hebra modifica los datos (hacer write)
	- Si no hay recursos compartidos
	- Si el proceso es monohebra

_Cual es la SC en la función insert?_

#### Exclusión Mutua
Requerimiento sobre una SC que dice que sólo una hebra puede estar ejecutando dicha SC.

```
// SC
void pop() {
	if (! empty()}
		top--;
}
```
```
// SC
void push(int item) {
	if (! full()) {
		top++;
		data[top] = item
	} else error()
}
```
La EM dice si hay una hebra que esta en pop no puede haber otra en push y viceversa

#### Modelo de Concurrencia

```
Process(i) {
	while (true) {
		codigo no critico
		...
		enterCS();
		SC();
		exitSC();
		..
		codigo no critico
	}
}
```
cuando la puerta esta cerrada la hebra invasora se queda 

#### Requerimientos para una solución correcta de EM

#### Locks

#### Atomicidad
- Una operación es atómica si es que no puede dividirse en partes. Se ejecuta completamente o no se ejecuta y no puede ser interrumpida
- Si es atómico -> Es exclusivo 
- Pero si es Exclusivo no necesariamente es atómico ¿Por qué?
	- Se refiere a código, operaciones, cualquier cosa ejecutable
- **Ilusión de atomicidad:** Uno a veces cree que las cosas son atómicas

```
inc(int &i) {      LOAD i, ACC // carga el acumulador
	i = i + 1;     INC ACC // incrementa el acumulador
}                  STORE ACC, i // almacena el resultado en memoria
```
En el código cada instrucción assembler es atómica pero una de alto nivel *no lo es*

i es un dato compartido y acc es un dato local de la hebra

Una asignación simple del tipo `i = 0` es atómica

#### Solucion por hardware 1:

##### Deshabilitar interrupciones:
 - La sección crítica se ejecuta como si fuera atómica, tiene todo el tiempo del mundo para ingresar a la sección critica, ejecutar todas sus tareas y luego salir de la sección critica y las demás hebras se verán obligadas a esperar
 - Puede producir inanición
 - No sirve en multiprocesadores
 - 

#### Solución por hardware 2:
##### testset()
- Instrucciones que se realizan/ejecutan de forma atómica
```
boolean testset(int &i) { 
	if (i == 0) {
		i = 1;
		return true;
	} else return false;
} 

T(i) {
	while (true) {
		...
		while (!testset(bolt)); //busy-waiting or spin-lock, hebra queda ocupada esperando
		SC();
		bolt = 0;
		...
	}
}

int bolt; // shared
void main() {
	bolt = 0;
	parbegin(T(1), T(2),...,T(n));
}



```
%binarizar, calcular houge, obtener lineas, calcular centro del objeto

