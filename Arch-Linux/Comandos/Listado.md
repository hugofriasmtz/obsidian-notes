# Guía para listar archivos y directorios en Linux

En sistemas basados en Linux y Unix, el comando fundamental para visualizar el
contenido del sistema de archivos es `ls` (*list*). Esta guía cubre desde su
uso básico hasta combinaciones avanzadas, visualización de permisos y
herramientas complementarias.

## 1. Comando básico: `ls`

Por defecto, `ls` muestra los nombres de los archivos y directorios del
directorio actual en orden alfabético. Los archivos ocultos y los detalles
técnicos no se muestran.

```bash
ls
```

También puedes especificar una ruta para consultar otro directorio sin cambiar
de ubicación:

```bash
ls /var/log
```

## 2. Opciones fundamentales

### 2.1. Mostrar archivos ocultos: `-a` y `-A`

En Linux, cualquier archivo o directorio cuyo nombre comience con un punto (`.`)
se considera oculto.

- `-a` (`--all`): muestra todos los archivos, incluidos `.` (directorio actual)
  y `..` (directorio superior).

  ```bash
  ls -a
  ```

- `-A` (`--almost-all`): muestra los archivos ocultos, pero omite `.` y `..`.

  ```bash
  ls -A
  ```

### 2.2. Vista detallada: `-l`

Muestra información completa: permisos, número de enlaces, propietario, grupo,
tamaño y fecha de última modificación.

```bash
ls -l
```

### 2.3. Tamaños legibles: `-h`

Por defecto, `-l` muestra los tamaños en bytes. La opción `-h`
(*human-readable*) convierte los valores a unidades más fáciles de leer, como
`K`, `M` o `G`. Normalmente se utiliza junto con `-l` o `-s`.

```bash
ls -lh
```

### 2.4. Ordenar la salida

- `-t`: ordena por fecha de modificación, con los archivos más recientes
  primero.

  ```bash
  ls -lt
  ```

- `-r`: invierte el orden del listado.

  ```bash
  ls -lr
  ```

- `-S`: ordena por tamaño, de mayor a menor.

  ```bash
  ls -lhS
  ```

- `-X`: agrupa y ordena alfabéticamente por extensión.

  ```bash
  ls -lX
  ```

### 2.5. Listado recursivo: `-R`

Lista el contenido del directorio actual y el de todas sus subcarpetas.

```bash
ls -R
```

### 2.6. Indicadores y tipos de archivo: `-F` y `-d`

- `-F` (`--classify`): añade un símbolo al final de cada nombre para indicar el
  tipo de archivo:

  | Símbolo | Tipo de archivo |
  | --- | --- |
  | `/` | Directorio |
  | `*` | Archivo ejecutable |
  | `@` | Enlace simbólico |
  | `=` | Socket |
  | `\|` | FIFO o tubería nombrada |

  ```bash
  ls -F
  ```

- `-d` (`--directory`): lista el directorio en sí, en lugar de su contenido.
  Es especialmente útil al combinarlo con comodines o rutas específicas.

  ```bash
  ls -ld /var/log
  ```

## 3. Desglose de la salida de `ls -l`

Cada línea de `ls -l` representa un elemento con esta estructura:

```text
-rw-r--r-- 1 usuario desarrolladores 4.2K Mar 10 14:30 app.log
```

| Campo | Significado | Explicación |
| :---: | :---------- | :---------- |
| 1 | Permisos | Tipo de archivo (`-` normal, `d` directorio, `l` enlace) seguido de los permisos de usuario, grupo y otros (`rwx`). |
| 2 | Enlaces duros | Cantidad de enlaces directos al mismo inodo. |
| 3 | Propietario | Usuario propietario del archivo. |
| 4 | Grupo | Grupo al que pertenece el archivo. |
| 5 | Tamaño | Tamaño del archivo en bytes o con formato legible usando `-h`. |
| 6 | Fecha | Fecha y hora de la última modificación. |
| 7 | Nombre | Nombre del archivo o directorio. |

## 4. Combinaciones habituales

### 4.1. Vista completa: `ls -lah`

Muestra todos los archivos, incluidos los ocultos, en formato detallado y con
tamaños legibles.

```bash
ls -lah
```

### 4.2. Archivos más recientes al final: `ls -ltr`

Ordena por fecha de modificación (`-t`) y muestra el resultado en orden
inverso (`-r`).

```bash
ls -ltr

# Con tamaños legibles
ls -lhtr
```

### 4.3. Encontrar archivos grandes: `ls -lhS`

Lista los archivos ordenados de mayor a menor tamaño.

```bash
ls -lhS
```

### 4.4. Mostrar el número de inodo: `ls -li`

Muestra el identificador único del sistema de archivos. Es útil para
diagnosticar problemas relacionados con enlaces duros o archivos eliminados.

```bash
ls -li
```

## 5. Filtrado con comodines (*globbing*)

`ls` utiliza la expansión de comodines del intérprete de comandos, como Bash o
Zsh:

```bash
# Archivos con una extensión específica
ls -lh *.pdf

# Archivos cuyo nombre comienza con un patrón
ls log_*

# Un único carácter variable
ls archivo?.txt

# Archivos cuyo nombre comienza con un número y termina en .csv
ls [0-9]*.csv
```

## 6. Comandos alternativos y complementarios

### 6.1. `tree`

Muestra la estructura de directorios en forma de árbol visual.

```bash
tree

# Limitar la profundidad a dos niveles
tree -L 2
```

### 6.2. `find`

Permite buscar y listar archivos según criterios avanzados, como antigüedad,
tamaño o permisos.

```bash
# Archivos .conf de /etc modificados en los últimos dos días
find /etc -name "*.conf" -mtime -2
```

### 6.3. `eza` (o `exa`)

Es una alternativa moderna a `ls`, escrita en Rust. Añade integración con Git,
colores, cabeceras e iconos.

```bash
eza -lah --git --icons
```

## 7. Tabla resumen

| Comando | Función principal |
| :------ | :---------------- |
| `ls` | Listado simple estándar. |
| `ls -a` | Muestra todo, incluidos `.` y `..`. |
| `ls -A` | Muestra archivos ocultos sin incluir `.` ni `..`. |
| `ls -l` | Formato largo con permisos, tamaño y propietarios. |
| `ls -lh` | Formato largo con tamaños legibles. |
| `ls -t` | Ordena por fecha de modificación. |
| `ls -S` | Ordena por tamaño, de mayor a menor. |
| `ls -r` | Invierte el orden del listado. |
| `ls -R` | Lista directorios y subdirectorios de forma recursiva. |
| `ls -lah` | **Recomendado:** vista detallada con tamaños legibles. |
| `ls -ltr` | **Recomendado:** vista detallada con lo más reciente al final. |
| `ls -d */` | Lista únicamente los directorios de la ruta actual. |
