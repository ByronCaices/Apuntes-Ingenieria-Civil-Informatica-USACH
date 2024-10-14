
# 1. Motivación

- Bueno, partamos por nuestra motivación como grupo...
- Las nuevas generaciones han comenzado a buscar un...
- Equilibrio entre la vida laboral y personal
- Estudios revelan que trabajadores mejor descansados y felices tienden  a ser más productivos (ojala encontrar un dato)
- Y las Empresas buscan tener esta ventaja competitiva
- Con tal de beneficiar tanto a las empresas como a trabajadores:
- Optimizar las horas de trabajo para mejorar el bienestar de estos sin sacrificar los objetivos diarios, mensuales o la rentabilidad es cada vez más relevante

- ¿Que pasa ante mucha carga laboral? 
- Efectos adversos como cansancio que puede conducir a un bajo rendimiento en la productividad y de hecho...
- Chile actualmente se encuentra en proceso de reducción de horas laborales mediante un plan paulatino de transición de 45 a 40 horas con el fin de no afectar los niveles de producción y utilidad

# 2. Contexto del problema

- Desafío de **disminuir la carga laboral** sin comprometer la producción ni la rentabilidad.
- **Horarios actuales** garantizan la producción y los beneficios esperados.
- **Cualquier cambio** en las horas laborales debe ser cuidadosamente considerado y estudiado en el contexto local.
- **Objetivo**: Encontrar un equilibrio óptimo entre la reducción de carga laboral y la estabilidad operativa.
- **Reevaluación necesaria** de la estructura organizacional e implementación de tecnologías.
- **Evaluación prudente** de las consideraciones antes de implementar cambios.
- **Meta**: Fomentar un entorno de trabajo más positivo y productivo, generando beneficios para toda la comunidad.

# 3. Definición del problema

- **Problema principal**: Reducir las horas trabajadas sin afectar la producción ni las utilidades.
- **Objetivo de la empresa**: Disminuir la jornada laboral manteniendo la eficiencia operativa y la rentabilidad.
- **Estudio necesario**: Realizar un análisis para implementar cambios que mejoren el bienestar de los empleados.
- **Beneficios esperados**: Mejorar el bienestar de los empleados y la comunidad laboral.

---

### Frase que define el problema:

"Encontrar el equilibrio entre la reducción de horas laborales y el mantenimiento de la eficiencia y rentabilidad empresarial."

# 4. Análisis del problema

FALTAAA a

# 5. Modelado del Problema

### Modelado del Problema con 50 Empleados

**Descripción del problema:**

Tenemos una empresa con 50 empleados. Todos los empleados deben ganar un mínimo de $500 a la semana, y deben trabajar un máximo de 40 horas semanales. La empresa tiene un presupuesto semanal de $52000 y la producción total mínima requerida es de 2500 unidades.

### Salarios por hora:
- Empleados 1 al 10 ganan $15 por hora.
- Empleados 11 al 20 ganan $20 por hora.
- Empleados 21 al 30 ganan $25 por hora.
- Empleados 31 al 40 ganan $30 por hora.
- Empleados 41 al 50 ganan $35 por hora.

### Producción por hora:
- Empleados 1 al 10 producen 2 unidades/hora.
- Empleados 11 al 20 producen 3 unidades/hora.
- Empleados 21 al 30 producen 4 unidades/hora.
- Empleados 31 al 40 producen 5 unidades/hora.
- Empleados 41 al 50 producen 6 unidades/hora.

### Variables:
- $x_i$ : Número de horas trabajadas por el empleado $i$ (donde $i = 1, 2, \dots, 50$).
### Función objetivo:

Minimizar la suma total de horas trabajadas por todos los empleados:

$$
\text{Minimizar } Z = \sum_{i=1}^{50} x_i
$$

### Restricciones:

1. **Restricción presupuestaria**: El gasto total en salarios no debe superar los $52.000:

$$
15(x_1 + \dots + x_{10}) + 20(x_{11} + \dots + x_{20}) + 25(x_{21} + \dots + x_{30}) + 30(x_{31} + \dots + x_{40}) + 35(x_{41} + \dots + x_{50}) \leq 52000
$$

2. **Restricción de producción**: La producción total debe ser al menos 2500 unidades:

$$
2(x_1 + \dots + x_{10}) + 3(x_{11} + \dots + x_{20}) + 4(x_{21} + \dots + x_{30}) + 5(x_{31} + \dots + x_{40}) + 6(x_{41} + \dots + x_{50}) \geq 2500
$$

3. **Restricción de salario mínimo**: Cada empleado debe ganar al menos $500 a la semana:
$$
15x_i \geq 500 \quad \text{para } i = 1, 2, \dots, 10
$$
$$
20x_i \geq 500 \quad \text{para } i = 11, 12, \dots, 20
$$
$$
25x_i \geq 500 \quad \text{para } i = 21, 22, \dots, 30
$$
$$
30x_i \geq 500 \quad \text{para } i = 31, 32, \dots, 40
$$
$$
35x_i \geq 500 \quad \text{para } i = 41, 42, \dots, 50
$$

4. **Restricciones de horas mínimas**: Cada empleado debe trabajar a lo más 40 horas a la semana:

$$
x_i \leq 40 \quad \text{para todo } i = 1, 2, \dots, 50
$$

### Resumen del modelo

El objetivo es minimizar $Z = \sum_{i=1}^{50} x_i$, sujeto a las restricciones mencionadas. Estas restricciones aseguran que el presupuesto no se exceda, la producción mínima se cumpla, y que cada empleado trabaje un mínimo de 40 horas y gane al menos $500 a la semana.

Este modelo puede ser resuelto utilizando métodos de optimización lineal, como el algoritmo simplex, para determinar la cantidad óptima de horas que cada empleado debe trabajar para cumplir con las condiciones impuestas. 

# Propuesta de solución computacional

```
from scipy.optimize import linprog

# Número de empleados

n_empleados = 50

# Coeficientes de la función objetivo (Minimizar Z = x1 + x2 + ... + x50)

c = [1] * n_empleados

# Salarios por hora y producción por hora por grupo de empleados

salarios = [15] * 10 + [20] * 10 + [25] * 10 + [30] * 10 + [35] * 10

produccion = [2] * 10 + [3] * 10 + [4] * 10 + [5] * 10 + [6] * 10

# Restricción presupuestaria

A_presupuesto = [salarios]

# Restricción de producción

A_produccion = [[-p for p in produccion]]

# Restricciones de salario mínimo (si * xi >= 500)

A_salario_minimo = [[-s if i == j else 0 for i in range(n_empleados)] for j, s in enumerate(salarios)]


# Unir todas las restricciones en una matriz A

A = A_presupuesto + A_produccion + A_salario_minimo


# Lado derecho de las restricciones

b = [52000, -2500] + [-500] * n_empleados

# Cambiar los límites de las variables a un máximo de 40 horas (0 <= xi <= 40)

x_bounds_max_40 = [(0, 40)] * n_empleados

# Resolver el problema nuevamente usando el método simplex con el límite superior de 40 horas

result_max_40_hours = linprog(c, A_ub=A, b_ub=b, bounds=x_bounds_max_40, method='highs')

print(result_max_40_hours)
```


- **Horas trabajadas por cada empleado**:
    - Empleados 1 al 10: 33.3 horas.
    - Empleados 11 al 20: 25 horas.
    - Empleados 21 al 30: 20 horas.
    - Empleados 31 al 40: 16.67 horas.
    - Empleados 41 al 50: 14.29 horas.
    
- **Valor mínimo de la función objetivo** (suma total de horas trabajadas): Z=1092.86 horas.
    

### Interpretación:

- Todos los empleados trabajan menos de 40 horas a la semana, ajustándose a la nueva restricción.
- El modelo distribuye las horas entre los empleados de manera que la producción y el presupuesto se cumplan, respetando el máximo de horas.

![[Pasted image 20240829113336.png]]
### Comentarios sobre la variabilidad en las horas trabajadas:

1. **Desigualdad en la carga de trabajo**:
    
    - La distribución de horas no es uniforme, lo que indica que algunos empleados están asumiendo una mayor carga de trabajo que otros. Esto podría ser un indicio de que no todos los empleados son igualmente necesarios a tiempo completo.
2. **Identificación de roles para contratos part-time**:
    
    - Los empleados que están trabajando menos de 20 horas, por ejemplo, podrían ser considerados para roles part-time. Esta información puede ayudar a la empresa a optimizar sus costos laborales, contratando a algunos empleados a tiempo parcial en lugar de a tiempo completo.
    - 
3. **Optimización del presupuesto**:
    
    - Contratar empleados part-time podría liberar presupuesto que podría ser redistribuido o ahorrado. Dado que algunos empleados están trabajando significativamente menos horas, podría no ser eficiente mantenerlos como empleados a tiempo completo.
4. **Flexibilidad en la gestión del personal**:
    
    - El modelo sugiere que la empresa podría ser más flexible en la gestión de su personal, permitiendo que ciertos puestos sean cubiertos por empleados part-time. Esto también podría ser atractivo para empleados que prefieren o necesitan trabajar menos horas, como estudiantes, padres, o personas con otras responsabilidades.

### Potencial para empleos part-time:

1. **Empleados en el rango más bajo de horas trabajadas**:
    
    - Los empleados que trabajan entre 14 y 20 horas podrían ser candidatos ideales para contratos part-time. Esto no solo sería beneficioso para optimizar el presupuesto, sino que también podría mejorar la satisfacción laboral de los empleados al permitirles trabajar menos horas si así lo prefieren.
2. **Ajuste de roles y tareas**:
    
    - La empresa podría reevaluar las tareas asignadas a estos empleados y considerar si ciertas funciones o roles podrían ser realizados en menor tiempo sin comprometer la eficiencia o la producción. Esto podría llevar a una reestructuración de ciertos puestos para adaptarlos a contratos part-time.



### Comentarios sobre la variabilidad en las horas trabajadas:

1. **Desigualdad en la carga de trabajo**:
2. **Identificación de roles para contratos part-time**:
3. **Optimización del presupuesto**:
4. **Flexibilidad en la gestión del personal**:
    
    
- El modelo sugiere que la empresa podría ser más flexible en la gestión de su personal, permitiendo que ciertos puestos sean cubiertos por empleados part-time. Esto también podría ser atractivo para empleados que prefieren o necesitan trabajar menos horas, como estudiantes, padres, o personas con otras responsabilidades.
