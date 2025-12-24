# Documentación del Proyecto: Analizador Léxico

Este proyecto implementa un analizador léxico utilizando **JFlex** y **Java CUP**. El sistema lee un archivo fuente, identifica los tokens definidos en la especificación léxica, y genera un reporte de salida.

## Características

*   **Identificación de Tokens**: Reconoce palabras clave, literales (enteros, flotantes, booleanos, caracteres, strings), identificadores y operadores.
*   **Manejo de Errores (Modo Pánico)**: Si encuentra un carácter inválido, el analizador lo reporta en la consola y continúa con el siguiente carácter para no detener el proceso de análisis.
*   **Salida Estructurada**: Genera un archivo `salida.txt` listando el tipo de token y su lexema (o valor) asociado.

## Estructura del Proyecto

*   **`src/`**: Código fuente (`.java`, `.flex`, `.cup`).
*   **`lib/`**: Librerías y herramientas necesarias (`jflex`, `cup`).
*   **`bin/`**: Archivos de clase compilados (`.class`).
*   **`test_input.txt`**: Archivo de prueba con código ejemplo.
*   **`salida.txt`**: Archivo generado con los resultados del análisis.

## Requisitos

*   **Java Development Kit (JDK)**: Debe estar instalado y configurado en el PATH del sistema.

> **Nota**: No es necesario instalar JFlex o CUP en el sistema, ya que el proyecto utiliza las versiones incluidas en la carpeta `lib/`.

## Instrucciones de Compilación

### 1. Generar Código Fuente (Lexer y Parser)

Genera las clases `LexerProyUno.java`, `parser.java` y `sym.java` a partir de las especificaciones:

```powershell
java -jar lib/jflex-full-1.9.1.jar src/jflex.flex

java -jar lib/java-cup-11b.jar -destdir src -parser parser -symbols sym src/cup.cup
```

### 2. Compilar Clases Java

Compila el código fuente y coloca los binarios en la carpeta `bin`:

```powershell
# Crea el directorio bin si no existe (opcional si ya existe)
mkdir bin -ErrorAction SilentlyContinue

javac -cp "lib/java-cup-11b-runtime.jar" -d bin src/*.java
```

## Instrucciones de Ejecución

Para ejecutar el analizador, utiliza la clase `Main` indicando el archivo de entrada.

### Sintaxis
```powershell
java -cp "bin;lib/java-cup-11b-runtime.jar" Main <archivo_de_entrada>
```

### Ejemplo de Uso
Para analizar el archivo de prueba `test_input.txt`:

```powershell
java -cp "bin;lib/java-cup-11b-runtime.jar" Main test_input.txt
```

## Salida y Resultados

1.  **Consola**: Verás mensajes indicando el inicio y fin del análisis, así como reportes de **errores léxicos** (caracteres no reconocidos).
2.  **`salida.txt`**: Este archivo contendrá la secuencia de tokens. El formato es:
    ```text
    NOMBRE_TOKEN -> Valor (si aplica)
    ```
    *Ejemplo:*
    ```text
    INT
    IDENTIFIER -> edad
    ASSIGN
    INTEGER_LITERAL -> 18
    ```
