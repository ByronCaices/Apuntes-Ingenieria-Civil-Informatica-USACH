Airline Database - Grupo 4
--

### **Tabla `COMPANIA`**

| Nombre del Campo | Tipo de Datos  | Restricciones | Descripción                        |
| ---------------- | -------------- | ------------- | ---------------------------------- |
| compania_id      | `SERIAL`       | PRIMARY KEY   | Identificador único de la compañía |
| nombre           | `VARCHAR(100)` | NOT NULL      | Nombre de la compañía              |

---

### **Tabla `CLIENTE`**

| Nombre del Campo | Tipo de Datos   | Restricciones                  | Descripción                                   |
|------------------|-----------------|--------------------------------|-----------------------------------------------|
| nro_documento    | `INT`           | PRIMARY KEY, NOT NULL          | Número de documento del cliente               |
| nombre           | `VARCHAR(20)`   | NOT NULL                       | Nombre del cliente                            |
| apellido         | `VARCHAR(20)`   | NOT NULL                       | Apellido del cliente                          |
| nacionalidad     | `VARCHAR(50)`   | NOT NULL                       | Nacionalidad del cliente                      |
| compania_id      | `INT`           | NOT NULL, FOREIGN KEY          | Identificador de la compañía (FK a `COMPANIA`) |

---

<div style="page-break-after: always;"></div>

### **Tabla `VUELO`**

| Nombre del Campo | Tipo de Datos  | Restricciones          | Descripción                                    |
| ---------------- | -------------- | ---------------------- | ---------------------------------------------- |
| vuelo_id         | `SERIAL`       | PRIMARY KEY            | Identificador único del vuelo                  |
| origen           | `VARCHAR(100)` | NOT NULL               | Ciudad de origen del vuelo                     |
| destino          | `VARCHAR(100)` | NOT NULL               | Ciudad de destino del vuelo                    |
| fecha_vuelo      | `DATE`         | NOT NULL               | Fecha del vuelo                                |
| compania_id      | `INT`          | NOT NULL, FOREIGN KEY  | Identificador de la compañía (FK a `COMPANIA`) |
| id_avion         | `INT`          | NOT NULL,  FOREIGN KEY | Id del avión que realiza el vuelo              |

---

### **Tabla `CLIENTE_COMP`**

| Nombre del Campo | Tipo de Datos | Restricciones         | Descripción                                      |
| ---------------- | ------------- | --------------------- | ------------------------------------------------ |
| compra_id        | `SERIAL`      | PRIMARY KEY           | Identificador de la compra                       |
| nro_documento    | `INT`         | NOT NULL, FOREIGN KEY | Número de documento del cliente (FK a `CLIENTE`) |
| vuelo_id         | `INT`         | NOT NULL, FOREIGN KEY | Identificador del vuelo (FK a `VUELO`)           |

---

### **Tabla `SECCION`**

| Nombre del Campo | Tipo de Datos   | Restricciones         | Descripción                           |
|------------------|-----------------|-----------------------|---------------------------------------|
| id_seccion       | `INT`           | PRIMARY KEY, NOT NULL | Identificador de la sección           |
| tipo_seccion     | `VARCHAR(50)`   | NOT NULL              | Tipo de sección (Ej. Económica, VIP)  |

---

<div style="page-break-after: always;"></div>

### **Tabla `PASAJE`**

| Nombre del Campo | Tipo de Datos | Restricciones         | Descripción                                  |
| ---------------- | ------------- | --------------------- | -------------------------------------------- |
| id_pasaje        | `INT`         | PRIMARY KEY, NOT NULL | Identificador del pasaje                     |
| numero_asiento   | `VARCHAR(20)` | NOT NULL              | Número de asiento                            |
| hora_embarque    | `TIMESTAMP`   | NOT NULL              | Hora de embarque                             |
| lugar_destino    | `VARCHAR(50)` | NOT NULL              | Lugar de destino                             |
| puerta           | `VARCHAR(50)` | NOT NULL              | Puerta de embarque                           |
| vuelo_id         | `INT`         | NOT NULL, FOREIGN KEY | Identificador del vuelo (FK a `VUELO`)       |
| id_seccion       | `INT`         | FOREIGN KEY           | Identificador de la sección (FK a `SECCION`) |
| nro_documento    | `INT`         | NOT NULL, FOREIGN KEY | Documento de cliente asociado al pasaje      |

---


### **Tabla `COSTO`**

| Nombre del Campo | Tipo de Datos   | Restricciones                  | Descripción                                   |
|------------------|-----------------|--------------------------------|-----------------------------------------------|
| id_costo         | `INT`           | PRIMARY KEY, NOT NULL          | Identificador del costo                       |
| monto_costo      | `INT`           | NOT NULL                       | Monto del costo                               |
| id_pasaje        | `INT`           | NOT NULL, FOREIGN KEY          | Identificador del pasaje (FK a `PASAJE`)      |

---

### **Tabla `MODELO`**

| Nombre del Campo | Tipo de Datos   | Restricciones         | Descripción                           |
|------------------|-----------------|-----------------------|---------------------------------------|
| id_modelo        | `INT`           | PRIMARY KEY, NOT NULL | Identificador del modelo de avión     |
| nombre_modelo    | `VARCHAR(20)`   | NOT NULL              | Nombre del modelo de avión            |

---

### **Tabla `AVION`**

| Nombre del Campo   | Tipo de Datos | Restricciones         | Descripción                                    |
| ------------------ | ------------- | --------------------- | ---------------------------------------------- |
| id_avion           | `SERIAL`      | PRIMARY KEY           | Identificador del avión                        |
| anio_avion         | `TIMESTAMP`   | NOT NULL              | Fecha de adquisición del avion                 |
| material_avion     | `VARCHAR(50)` | NOT NULL              | Material del avión                             |
| cantidad_pasajeros | `INT`         | NOT NULL              | Capacidad de pasajeros                         |
| id_modelo          | `INT`         | NOT NULL, FOREIGN KEY | Identificador del modelo (FK a `MODELO`)       |
| compania_id        | `SERIAL`      | NOT NULL, FOREIGN KEY | Identificador de la compañía (FK a `COMPANIA`) |

---


### **Tabla `SUELDO`**

| Nombre del Campo | Tipo de Datos   | Restricciones         | Descripción                                 |
| ---------------- | --------------- | --------------------- | ------------------------------------------- |
| id_sueldo        | `SERIAL`        | PRIMARY KEY           | Identificador del sueldo                    |
| fecha_pago       | `TIMESTAMP`     | NOT NULL              | Fecha de pago del sueldo                    |
| cantidad_sueldo  | `DECIMAL(10,2)` | NOT NULL              | Monto del sueldo                            |
| id_empleado      | `INT`           | NOT NULL, FOREIGN KEY | Identificado del empleado (FK a `EMPLEADO`) |


---

### **Tabla `EMPLEADO`**

| Nombre del Campo | Tipo de Datos  | Restricciones         | Descripción                                    |
| ---------------- | -------------- | --------------------- | ---------------------------------------------- |
| id_empleado      | `SERIAL`       | PRIMARY KEY           | Identificador del empleado                     |
| nombre_empleado  | `VARCHAR(100)` | NOT NULL              | Nombre del empleado                            |
| anios_servicio   | `INT`          | NOT NULL              | Años de servicio                               |
| cargo_empleado   | `VARCHAR(50)`  | NOT NULL              | Cargo del empleado                             |
| compania_id     | `INT`          | NOT NULL, FOREIGN KEY | Identificador de la compañía (FK a `COMPANIA`) |

---

### **Tabla `EMP_VUELO`**

| Nombre del Campo | Tipo de Datos | Restricciones         | Descripción                                  |
| ---------------- | ------------- | --------------------- | -------------------------------------------- |
| id_emp_vuelo     | `SERIAL`      | PRIMARY KEY           | Identificador de la asignación               |
| vuelo_id         | `INT`         | NOT NULL, FOREIGN KEY | Identificador del vuelo (FK a `VUELO`)       |
| id_empleado      | `INT`         | NOT NULL, FOREIGN KEY | Identificador del empleado (FK a `EMPLEADO`) |

---