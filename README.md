# **Trabajo final: SIMULACION INCUCAI**

### Materia: Laboratorio de programación I

### Universidad Favaloro

### Lenguaje Utilizado: Python 

### Autores:
``````````````````

Alonso Victoria
GitHub: bici-alonso [https://github.com/bici-alonso]

Pfeifer Zoe
GitHub: z0oee [https://github.com/z0oee]

``````````````````

## Contribuciones:

### Ayudante a cargo: Naddeo Andres

### Profesor: Fernando Mario Romero Munoz

### Acceso a UML: 
https://drive.google.com/file/d/1UeuJuTFKKqsDM7OKON30lkVPS3GfXJ-_/view?usp=sharing

### Sobre el proyecto:
Este trabajo busca simular la organización del sistema del INCUCAI en Argentina. A través de un menú con opciones disponibles, por terminal se controla el funcionamiento, y permite: Cargar un donante/receptor manualmente, inicializar el sistema con objetos ya cargados para probar el funcionamiento sin la necesidad de realizar una carga, evaluar la compatibilidad para trasplantes entre 2 pacientes específicos, activar el protocolo de donaciones e imprimir los datos de donantes/pacientes/centros de salud cargados para INCUCAI.

## Instalación:
Abrir carpeta de Visual Studio Code y ejecutar desde terminal:

```bash
git clone https://github.com/bici-alonso/Final_Alonso_Pfeifer
cd src
python -m venv venv

Windows:
venv\Scripts\activate

MacOS/Linux:
source venv/bin/activate

pip install -r requirements.txt
python main.py
```

## Librerias utilizadas:
* geographiclib
* geopy
* unidecode
* datetime
* random

### Implementación de las librerias
Terminar...


## ORGANIZACION DEL TRABAJO
* Clases creadas:
  1. `Testing:` -->  Crea listas de instancias de pacientes, aviones, ambulancias, helicopteros, especialistas y cirujano generales predefinidos
  2. `Menu:` --> Muestra el menú principal del sistema INCUCAI y gestiona la interacción con el usuario.
  3. `Incucai:` --> Sirve a modo de gestora de las demas clases, no hereda de nadie, pero utiliza metodos de las demas clases. 
  4. `Paciente:` --> Clase abstracta, representa un paciente dentro del sistema del INCUCAI. Establece los atributos comunes entre donantes y   receptores. 
  5. `Donante:` --> Representa a un donante dentro de INCUCAI. Esta clase hereda de Paciente e incorpora atributos y métodos específicos. 
  6. `Receptor:` --> Representa a un receptor dentro de INCUCAI. Esta clase hereda de Paciente e incorpora atributos y métodos específicos 
  7. `Centro_de_salud:` --> Representa un centro médico apto para la gestión de trasplantes, incorporando tanto información administrativa como operativa.
  8. `Organo:` --> Representa un órgano humano extraído para trasplante, gestionando su tipo, fecha y hora de ablación, y controlando su viabilidad en función del tiempo máximo de conservación.
  9. `Vehiculo:` --> Clase Abstracta que representa un vehículo del sistema de transporte del INCUCAI. Modela los atributos basicos y comportamientos comunes de todos los vehículos que participan en los traslados relacionados con donaciones y trasplantes.
  10. `Avion:` --> Clase que representa un avion utilizado en el sistema de transporte del INCUCAI. Hereda de Vehiculo. Se caracterizan por no verse afectados por el tráfico terrestre, por lo que el tiempo de viaje ignora el nivel de tráfico.
  11. `Ambulancia:` --> Clase que representa una ambulancia utilizada en el sistema de transporte del INCUCAI. Hereda de Vehiculo. Las ambulancias se ven afectadas por el tráfico, por lo que el tiempo total de viaje incluye un valor adicional.
  12. `Helicoptero:` --> Clase que representa un helicóptero utilizado en el sistema de transporte del INCUCAI. Hereda de Vehiculo. Se caracterizan por no verse afectados por el tráfico terrestre, por lo que su cálculo de tiempo de viaje ignora el nivel de tráfico.
  13. `Cirujanos:` --> Clase abstracta que representa un cirujano dentro del sistema de trasplantes.
  14. `Especialista:`  --> Representa a un cirujano con una especialidad asociada dentro del sistema de trasplantes. Hereda de la clase Cirujano e incorpora una especialidad médica que afecta la probabilidad de éxito en una operación según el órgano a tratar.
  15. `General:`  --> Representa a un cirujano sin especialidad, hereda de Cirujano y no tiene una tasa de exito mayor por especialidad. 

  -Archivo `main` desde donde se corre el programa, solo contiene el llamado a menu. 

  Para mas informacion sobre los metodos y atributos de las clases visitar enlace a UML. 

## FUNCIONAMIENTO:
Al ejecutar el programa, se da opción 1 para inicializar el programa y acceder al menú o 0 para cerrar. La opción 0 siempre se mantendrá como opción para cerrar el programa.

Al presionar la opción 1 se accede a un menú con todas las opciones del programa:

* La opción 1 será necesaria para el correcto funcionamiento del sistema antes de ejecutar las demás funciones. Inicializa información sobre los distintos centros con objetos base, necesarios para la coordinación de trasplantes.

* Las opciones 2 y 3 habilitan la carga manual de un receptor o de un donante (fallecido) para el sistema INCUCAI; tras una carga exitosa, el/la paciente cargado pasará a formar parte del array que le corresponda de acuerdo a la opción seleccionada.

* Las opciones de menú 4, 5, 6, 7, 14 y 15 refieren a impresiones por terminal de información para el usuario. Sirven a modo de consulta en la interfaz y revisión de un correcto funcionamiento del sistema.

* Las opciones de menú 8 y 12 refieren a la gestión de procedimientos de trasplante. Permiten iniciar un protocolo de trasplante o realizar una donación específica entre un donante y un receptor previamente identificados.

* Las opciones 9, 10, 11 y 13 están orientadas a la búsqueda de información detallada sobre pacientes, ya sea individualmente por DNI o dentro de un centro de salud.


### Tener en cuenta:

* La opcion 1 del menu "Inicializar pacientes anteriores de INCUCAI" sera necesaria antes de correr las opciones que involucren el      transplante, porque realiza tambien, carga de cirujanos asociados a centros y sus vehiculos silenciosamente (Ademas de la carga de receptores y donantes que se muestra por terminal). 

* La opcion 2 del menu "Agregar donante manualmente" se ve limitada a poder cargar donantes fallecidos y que tendran una unica fecha y hora de ablacion general, por lo que todos sus organos seran donados y bajo la misma fecha de ablacion. 

* Para los distintos organos, se consideraron distintos tiempos maximos de conservacion establecidos en horas.

* Los calculos de tiempo de viaje, consideran el nivel de trafico solo en el caso de las ambulancias y ese factor se establece a raiz de un random que varia entre 0.1 y 2. El calculo del tiempo de viaje base es: tiempo_basico=dist/self.velocidad. Al considerar el nivel de trafico es: tiempo_total = tiempo_basico + trafico.

* Existen 3 oportunidades de geolocalizacion de centros medicos, si se cumplieran esos 3 timeouts, el programa igualmente corre y no se frena, pero la geolocalizacion del geopy no figurara para el usuario ni sera tan precisa. 

* La tasa de exito de los transplantes variaran de acuerdo a si se corresponde el tipo de transplante con la especialidad del cirujano que lo realiza. Este comportamiento se especifica en el metodo "exito_operacion()". La probabilidad de éxito depende de si el órgano está dentro de la especialidad del cirujano: Si el órgano pertenece a su especialidad, éxito con probabilidad >= 80% (resultado ≥ 3). Si no pertenece, éxito solo con probabilidad > 50% (resultado > 5).

* Los criterios de compatibilidad entre pacientes son: Tipo de sangre (de acuerdo a array), Compatibilidad HLA (maximo 6 matchs) y la edad, si se trata de un menor de edad involucrado, se considera que deben tener un anio de diferencia como maximo, esto busca representar la diferencia de tamanio real que pueden generarse en los menores (sobre todo en los primeros anios de vida). Busca ser una representacion aproximada. 

* Los centros establecidos se inicializan desde la creacion de un objeto del tipo INCUCAI y no pueden ser modificados por el usuario a menos que se agregue una opcion en el menu que asi lo permita. 

## Métodos mágicos utilizados:

* `__eq__` : utilizado en clase Paciente: compara si dos pacientes tienen mismo DNI. Utilizado en clase Centro: Compara dos centros de salud por nombre y dirección. Retorna True si la comparacion da iguales.

* `__len__` : Utilizada en Cirujano: Retorna la cantidad total de operaciones registradas por el cirujano. Utilizada en Centro: Devuelve la cantidad total de cirujanos y vehículos en el centro.

* `__str__` : Utilizada en clase Especialista: retorna la descripción con nombre y especialidad del cirujano. Utilizada en clase General: retorna la descripción textual del cirujano general, su nombre. Utilizado en clase Centro: Devuelve una representación string del centro (nombre y ubicación) como "Nombre - ciudad, provincia, Argentina". Utilizada en Organo: Devuelve el nombre del órgano capitalizado. Utilizada en Donante: Retorna cadena con nombre, DNI, órganos disponibles y tipo de sangre. Utilizada en Receptor: Retorna cadena con nombre, DNI, órgano a recibir y tipo de sangre.



