# Java — Sistemas operativos y búsqueda de tweets

Colección de proyectos académicos en Java sobre concurrencia, simulación de procesos, interfaces gráficas y consumo de servicios externos. Incluye una solución al problema de los filósofos hambrientos, un visualizador de un modelo probabilístico de CPU y material de búsqueda de tweets con Twitter4J.

Estos ejercicios prácticos fueron realizados durante el cursado de diversas materias mientras estudiaba la **Licenciatura en Análisis de Sistemas (Plan 2010)** de la **Universidad Nacional de Salta**.

**Materia:** ______________________________

## Contenido

- [Estructura](#estructura)
- [Filósofos hambrientos](#filósofos-hambrientos)
- [Visualizador de procesos](#visualizador-de-procesos)
- [Buscador de tweets](#buscador-de-tweets)
- [Compilación y ejecución](#compilación-y-ejecución)
- [Estado y compatibilidad](#estado-y-compatibilidad)
- [Licencia](#licencia)

## Estructura

```text
.
├── Sistemas Operativos/
│   ├── Problema Filosofos Hambrientos/
│   │   └── Solucion Tanenbaum/
│   │       ├── Tanenbaum.java
│   │       ├── clsList.java
│   │       ├── clsNode.java
│   │       └── output.txt
│   └── Visualizador de Planificadores de CPU/
│       ├── principal.java
│       ├── clsVentana.java
│       ├── clsModeloProb.java
│       ├── clsModeloProb2.java
│       ├── clsModeloProb3.java
│       ├── clsListaEnlazada.java
│       ├── clsNodo.java
│       ├── clsDatos.java
│       └── PruebaLista.java
├── Buscador de Tweets/
│   ├── TwitterJ.java
│   └── TwitterAppBuscador/Buscador.java
├── LICENSE
└── README.md
```

## Filósofos hambrientos

[Solucion Tanenbaum](Sistemas%20Operativos/Problema%20Filosofos%20Hambrientos/Solucion%20Tanenbaum/) implementa cinco filósofos como hilos. Cada uno alterna entre pensar, tener hambre y comer, coordinándose mediante semáforos.

| Archivo | Responsabilidad |
| --- | --- |
| `Tanenbaum.java` | Punto de entrada, creación de hilos, estados de los filósofos y coordinación de la toma y devolución de tenedores. |
| `clsList.java` | Lista enlazada que acumula eventos y genera un informe por filósofo. Utiliza un selector gráfico para elegir dónde guardarlo. |
| `clsNode.java` | Nodo que almacena un evento y el enlace al siguiente. |
| `output.txt` | Informe de una ejecución previamente guardada. |

La condición de parada se basa en unos cinco minutos desde el inicio. Como los hilos completan sus operaciones y esperas antes de volver a comprobarla, el cierre puede tardar más. Al terminar, el programa ofrece guardar un archivo `.txt` con los eventos y tiempos acumulados. Las pausas son aleatorias, por lo que los resultados varían entre ejecuciones.

## Visualizador de procesos

La carpeta [Visualizador de Planificadores de CPU](Sistemas%20Operativos/Visualizador%20de%20Planificadores%20de%20CPU/) contiene una aplicación Swing cuya ventana se titula **Modelo Probabilístico**.

Permite seleccionar entre uno y diez procesos, cargar su nombre, hora de inicio, tiempo de CPU y probabilidad de entrada/salida (`% I/O`), calcular una tabla de evolución y exportar los datos y resultados a texto. La opción **P único** permite utilizar un valor común para los procesos.

| Archivo | Responsabilidad |
| --- | --- |
| `principal.java` | Inicia la interfaz gráfica del paquete `proyecto`. |
| `clsVentana.java` | Tablas de entrada y resultados, validaciones, botones de cálculo y guardado. |
| `clsModeloProb.java` | Modelo de cálculo utilizado por la interfaz. |
| `clsListaEnlazada.java` y `clsNodo.java` | Almacenamiento de eventos y resultados mediante una lista enlazada. |
| `clsModeloProb2.java` y `clsModeloProb3.java` | Versiones alternativas de trabajo. Ambas declaran una clase pública llamada `clsModeloProb` en el paquete `defecto`. |
| `clsDatos.java` y `PruebaLista.java` | Clase auxiliar y demostración de lista en el paquete `defecto`. |

El código disponible desarrolla el modelo probabilístico; no contiene una selección de algoritmos clásicos como FIFO o Round Robin. Las versiones alternativas no deben compilarse junto con la aplicación principal: sus nombres de clase no coinciden con los nombres de archivo y utilizan otro paquete.

## Buscador de tweets

[Buscador.java](Buscador%20de%20Tweets/TwitterAppBuscador/Buscador.java), del paquete `BuscadorTweets`, configura Twitter4J mediante OAuth, busca el texto `Argentina vs Uruguay` e imprime el usuario y el contenido de cada resultado. Los valores de credenciales son marcadores de ejemplo.

[TwitterJ.java](Buscador%20de%20Tweets/TwitterJ.java) reúne fragmentos para publicar un tweet, consultar el estado y listar contactos, junto con referencias de consulta. Está incompleto: no declara una clase que contenga sus miembros, tiene nombres inconsistentes y contiene URLs sin comentar. Requiere reorganización antes de compilar.

Esta carpeta no incluye el JAR de Twitter4J, un descriptor de dependencias ni una configuración funcional del servicio. Para recuperar el buscador hay que proporcionar la biblioteca compatible, configurar credenciales fuera del código y revisar la integración y el acceso al servicio. No se verificaron solicitudes externas.

## Compilación y ejecución

Se necesita un **JDK** con `javac` y `java`. Los proyectos de sistemas operativos usan bibliotecas estándar de Java; sus ventanas y selectores de archivos requieren una sesión gráfica.

Los siguientes comandos usan Bash y se ejecutan desde la raíz del repositorio:

```bash
git clone https://github.com/GabrielUnsa/Java.git
cd Java
mkdir -p build/filosofos build/visualizador
```

### Filósofos

```bash
javac -encoding UTF-8 -d build/filosofos \
  "Sistemas Operativos/Problema Filosofos Hambrientos/Solucion Tanenbaum/"*.java
java -cp build/filosofos TanenbaumSolution.Tanenbaum
```

Tras la simulación aparece el diálogo para guardar el informe. Se debe elegir un nombre base: el programa agrega la extensión `.txt`.

### Visualizador

Se seleccionan explícitamente los cinco archivos que forman la aplicación del paquete `proyecto`:

```bash
javac -encoding UTF-8 -d build/visualizador \
  "Sistemas Operativos/Visualizador de Planificadores de CPU/principal.java" \
  "Sistemas Operativos/Visualizador de Planificadores de CPU/clsVentana.java" \
  "Sistemas Operativos/Visualizador de Planificadores de CPU/clsModeloProb.java" \
  "Sistemas Operativos/Visualizador de Planificadores de CPU/clsListaEnlazada.java" \
  "Sistemas Operativos/Visualizador de Planificadores de CPU/clsNodo.java"
java -cp build/visualizador proyecto.principal
```

En la ventana, seleccionar la cantidad de procesos, completar todas las filas y usar horas con formato `HH:MM:SS`. Luego pulsar **Calcular** y, si se desea exportar, **Guardar**. El modelo utiliza el valor de entrada/salida como probabilidad; conviene revisar la escala esperada en `clsModeloProb.java` antes de cargar datos, porque la etiqueta muestra `% I/O` y las validaciones no cubren todos los límites.

## Estado y compatibilidad

No hay un proyecto Maven o Gradle común, dependencias fijadas ni pruebas automatizadas. Los proyectos se compilan por separado y conservan versiones intermedias.

La documentación se preparó mediante revisión de los fuentes y de los paquetes. El entorno no disponía de `javac`, por lo que los comandos de compilación no se ejecutaron ni se probaron las interfaces gráficas. Los cálculos del visualizador y el comportamiento concurrente requieren validación antes de usarlos como referencia de resultados.

## Licencia

Distribuido bajo la [licencia MIT](LICENSE). Copyright © 2025 Gabriel Marmanillo.
