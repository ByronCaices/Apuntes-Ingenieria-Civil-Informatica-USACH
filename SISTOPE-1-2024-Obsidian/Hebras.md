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
 - Si hay un IO en la SC no se le podrá avisar al programa que e lO ha terminado

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
No produce deadlock pero sí puede producir inanición
%binarizar, calcular houge, obtener lineas, calcular centro del objeto


#### Solución por hardware 3: 

##### exchange()

- Mientras la llave no sea la que me sirva entonces la cambio con bolt

```
void exchange(int a, int b) { 
	int tmp; 
	tmp = a; 
	a = b; 
	b = tmp;
}

T(i) {
	int keyi;
	while (true) {
		keyi = 1; //ENTERSC de aqui
		while (keyi != 0)
			exhange(keyi, bolt); //busy-waiting ;;a aqui
		SC();
		exchange(keyi, bolt);
		...
	}
}

int bolt; // shared
void main() {
	bolt = 0;
	parbegin(T(1), T(2),...,T(n));
}

```
- EnterSC de esta solución lamentablemente no es atómico
- ¿Esta solucion satisface el progreso? Cuando una hebra comienza su enter "yo ahora estoy compitiendo por entrar a la SC" si la SC esta vacia ella deberia ser capaz de entrar (bolt = 0) entra a enterSC, toma key=1 y repentinamente hay un CC y ahora entra otra hebra y tambien toma el key=1
- Ahora hay dos hebras con key=1. Sí satisface el progreso pero puede producir inanición. 

En general las soluciones por hardware generan un uso del procesador innecesario (spinlock) además de la posibilidad de producir inanición

#### Solución por software 1:

```
int turno;
T0 {
	while (true) {
		while (turno != 0);
		SC();
		turno = 1;
	}
}

T1 {
	while (true) {
		while (turno != 1);
		SC();
		turno = 0;
	}
}

void main() {
	turno = 0;
	parbegin(T0, T1);
}

```
- Garantiza exclusión mutua. No es posible que dos hebras estén en la sección crítica ya que el turno es cero o es uno.
- Si quiero demostrar que algo no funciona doy un ejemplo, si quiero demostrar que algo funciona debe ser una demostración formal.
- No hay concurrencia, es una ejecución secuencial

#### Solución por software 2:
```
boolean flag[2];
T0 {
	while (TRUE) {
		while (flag[1]);
		flag[0] = true; 
		SC(); 
		flag[0] = FALSE;
	} 
}

T1 {
	while (TRUE) {
		while (flag[0]);
		flag[1] = true; 
		SC(); 
		flag[1] = FALSE;
	} 
}

void main() {
	flag[0] = flag[1] = FALSE;
	parbegin(T0, T1);
}
```

- Satisface progreso pero no el req de EM
- Suben su bandera demasiado tarde

#### Solución por software 3:

```

```

#### Solución de Peterson para dos Hebras:

- Hasta ahora todas son busy-waiting
- Satisface todos los requerimientos
- Yo quiero entrar (subo mi bandera) pero le doy el paso a la otra, mientras la otra quiere entra y sea el turno de la otra, la otra puede entrar de lo contrario si no se cumplen esas dos condiciones yo puedo entrar. 
- **¿Cómo demostrar que satisface EM?**
	- Demostración por contradicción: 
		- Hipótesis: No satisface la EM
			- Entonces la h0 está en SC y la h1 está en SC
			- Si ambas están en SC entonces el while anterior fue false para ambas hebras.
			- t0: `( flag[1]==T && turno==1 )` es false
			- ``
			- t1: `( flag[0]==T && turno==0 )`es false

flag[0] y flag[1] deben ser verdaderas y por ende turno=0 y turno=1 lo cual es una contradicción entonces decir "No satisface a la EM" es falso por tanto sí satisface la EM

![[photo_5037722340577881390_y.jpg]]

panaderia saltado
### Solución de S0:

#### Semáforos y Locks:

###### wait(s): 
- decrementa el semáforo, si el valor resultante es negativo, el proceso se bloquea; sino, continúa suejecución.
###### signal(s):
- incrementa el semáforo, si el valor resultante es menor o igual que cero, entonces se despierta un proceso que fue bloqueado por wait, puede despertar una hebra

el SO garantiza que wait y signal se ejecuten de manera atómica
#### Semáforo binario o mutex


## El problema del productor/consumidor

El problema es la sincronización


Buffer circular/finito: 

in = (in + 1)%n

in: posición donde ingresar el próximo item
out: Posicion del proximo elemento a consumir

buffer infinito solución correcta foto 28/05 13:57 (ejemplo en libro igualmente)

Semaforo contador 

buffer circular: full y empty son semaforos de comunicación y s es un semáforo de EM foto sacada luego de la anterior

## Problema de los filósofos comensales

Produce deadlock pero satisface pero satisface el requerimiento de coordinación correcta(?)


## Problema de los lectores/escritores

Pueden acceder a un recurso todos los lectores que quieran pero no pueden entrar multiples escritores ya que puede desencadenar ¿una CC? y tampoco si hay un escritor con el recurso puede acceder a este un lector y viceversa.

En la primera solución lectores tienen prioridad y puede generar inanición de lectores

#### Solución de libro
- Escritores con prioridad


## Problema típico con semáforos
- No implementan la solución al problema de la EM
- Esto lo vienen a solucionar los monitores
- 
HW,SW,SO,LENG

## Monitores
4 condiciones: EM, Deadlock, Inanicion, Progreso
- Garantiza EM
- Monitor es un módulo de software, es una propiedad/ objeto del lenguaje de programación. Va a encapsular mi aplicación
- 



Qué pasa si pongo un semáforo dentro de un monitor???????

## Sincronización con hebras POSIX

### Mutex
- Provee el mismo servicio que un semáforo binario

trylock: intentar bloquear el mutex
```
pthread_mutex_t m;
pthread_mutex_init(&m, NULL); //importante inicializarlo donde en null van los atributos por defecto
pthread_mutex_lock(m); //entersc()
SC(); //todos los que hagan lock quedan bloqueados en FIFO
pthread_mutex_unlock(m); //exitsc()
```
¿ Qué sucedería si una hebra se bloquea dentro de una SC?
Una VC permite que una hebra se bloquee dentro de una seccion critica y al mismo tiempo libere la SC

Signal despierta a una hebra que este durmiendo pero no abre el mutex, el wait abre el mutex y bloquea(duerne) la hebra que esta haciendo el wait

broadcast de una variable de condicion que es un signal a todas las hebras

# Deadlock e inanicion

