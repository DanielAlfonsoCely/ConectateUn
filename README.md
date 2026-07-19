# ConectateUn

Aplicación Android desarrollada en **Java** para conectar estudiantes de la Universidad Nacional de Colombia (UNAL) según afinidad de intereses.  
Proyecto académico de **Estructuras de Datos (2025)** con enfoque en implementación y uso de estructuras personalizadas dentro de un caso real de software móvil.

## 1. Descripción general

**ConectateUn** busca facilitar que estudiantes encuentren otras personas con gustos o intereses similares (académicos, culturales, deportivos, etc.).  
El núcleo del proyecto está en modelar relaciones entre usuarios e intereses usando estructuras de datos eficientes para soporte de búsqueda y recomendaciones.

---

## 2. Objetivo del proyecto

- Aplicar conceptos de estructuras de datos en un entorno Android real.
- Diseñar operaciones de consulta y recomendación con buena complejidad.
- Representar conexiones sociales a partir de afinidad.
- Construir una base técnica mantenible para futuras extensiones (persistencia, escalabilidad, nuevos algoritmos de recomendación).

---

## 3. Enfoque de estructuras de datos

Este proyecto prioriza:

1. **Diseño explícito de estructuras** (en lugar de depender solo de abstracciones de alto nivel).
2. **Análisis de complejidad** para operaciones críticas.
3. **Relación entre teoría y práctica**, demostrando cómo listas, tablas hash y grafos impactan directamente la experiencia de usuario.

---

## 4. Arquitectura técnica

La app sigue una separación por responsabilidades:

- **Capa de presentación (UI Android)**  
  Activities/Fragments, adapters y recursos de interfaz.
- **Capa de lógica de dominio**  
  Reglas de negocio para usuarios, intereses y afinidad.
- **Capa de estructuras de datos**  
  Almacenamiento en memoria, índices de acceso y relaciones entre entidades.

---

## 5. Modelo de dominio

### Entidades base

- **Usuario**
  - ID único
  - Nombre / metadata académica
  - Conjunto/lista de intereses

- **Interés**
  - Identificador o etiqueta
  - Categoría (si aplica)
  - Usuarios asociados

- **Afinidad**
  - Relación entre dos usuarios
  - Puntaje según intereses compartidos

### Relaciones

- **Usuario ↔ Interés**: muchos a muchos.
- **Usuario ↔ Usuario**: relación derivada por similitud (grafo social).

---

## 6. Estructuras de datos y su uso

> Nota: esta sección está redactada para un proyecto de Estructuras de Datos en Java/Android. Si en el código usas nombres concretos (ej. `ListaEnlazada`, `TablaHash`, `GrafoAfinidad`), reemplázalos en este README para que coincidan 1:1 con la implementación.

### 6.1 Listas (lineales)

Uso típico:

- Mantener colecciones de usuarios/intereses.
- Recorridos para renderizar resultados en UI.
- Construcción de rankings o sugerencias.

Aporte técnico:

- Simples de implementar y depurar.
- Útiles cuando prima recorrido secuencial.

---

### 6.2 Tabla Hash (indexación por clave)

Uso típico:

- Búsqueda rápida de usuario por ID/correo/username.
- Acceso por clave a intereses o categorías.
- Evitar búsquedas lineales repetitivas.

Aporte técnico:

- Tiempo promedio de consulta e inserción cercano a **O(1)**.
- Fundamental para mejorar respuesta en dispositivos móviles.

Consideraciones:

- Colisiones (encadenamiento o sondeo).
- Factor de carga y redimensionamiento.

---

### 6.3 Grafo de afinidad

Uso típico:

- Nodo = usuario.
- Arista = existe relación por interés compartido.
- Peso = grado de afinidad.

Aporte técnico:

- Representa naturalmente una red de estudiantes.
- Habilita recomendaciones por vecindad.
- Permite aplicar BFS/DFS para explorar conexiones directas e indirectas.

---

### 6.4 Conjuntos / control de duplicados (si aplica)

Uso típico:

- Evitar repetir intereses por usuario.
- Intersección para cálculo de similitud.

Aporte técnico:

- Simplifica validación de consistencia.
- Reduce ruido en recomendaciones.

---

## 7. Algoritmos principales

### 7.1 Registro y actualización de perfil

1. Validación de datos de entrada.
2. Inserción/actualización en estructura principal.
3. Indexación en hash.
4. Vinculación de intereses al usuario.

---

### 7.2 Cálculo de afinidad entre usuarios

Enfoque común:

- Obtener intereses de A y B.
- Calcular intersección.
- Generar puntaje (ej. conteo simple o métrica normalizada tipo Jaccard).
- Actualizar grafo de afinidad.

---

### 7.3 Recomendación de contactos

Estrategias posibles:

- Top-N vecinos con mayor peso.
- Exploración por niveles (BFS limitado).
- Filtros por categoría/interés común.

---

### 7.4 Búsqueda por interés/comunidad

- Consulta por clave (hash).
- Recuperación de usuarios relacionados.
- Ordenamiento o ranking por nivel de afinidad.

---

## 8. Complejidad computacional

> Complejidades esperadas (pueden variar según implementación exacta).

| Operación | Estructura | Complejidad esperada |
|---|---|---|
| Insertar usuario | Lista/Hash | O(1) promedio (hash) |
| Buscar usuario por ID | Hash | O(1) promedio |
| Agregar interés a usuario | Lista/Set | O(1) amortizado / O(n) |
| Comparar intereses A-B | Listas/Sets | O(i + j) |
| Recorrer conexiones | Grafo (adyacencia) | O(V + E) |

Donde:
- `n`: número de usuarios,
- `i`,`j`: número de intereses por usuario,
- `V`: usuarios (vértices),
- `E`: relaciones de afinidad (aristas).

---

## 9. Flujo funcional

1. El usuario crea o edita su perfil.
2. Selecciona intereses.
3. El sistema actualiza índices y relaciones.
4. Se recalculan puntajes de afinidad.
5. Se muestran recomendaciones en la interfaz.

---

## 10. Stack tecnológico

- **Lenguaje:** Java  
- **Plataforma:** Android  
- **Build system:** Gradle (Kotlin DSL)  
- **IDE recomendada:** Android Studio

---

## 11. Ejecución local

1. Clonar repositorio:
   ```bash
   git clone https://github.com/DanielAlfonsoCely/ConectateUn.git
   ```

2. Abrir el proyecto en Android Studio.

3. Sincronizar dependencias Gradle.

4. Ejecutar en emulador o dispositivo Android físico.

---

## 12. Validación y pruebas recomendadas

- Inserción/eliminación en cada estructura.
- Casos límite: estructuras vacías, duplicados, colisiones hash.
- Correctitud del cálculo de afinidad:
  - sin intereses comunes,
  - uno en común,
  - múltiples en común.
- Consistencia del grafo tras altas/bajas de usuarios.
- Pruebas de rendimiento con crecimiento progresivo de datos.

---

## 13. Limitaciones y mejoras futuras

- Persistencia robusta (Room / backend remoto).
- Ajuste fino de métricas de recomendación.
- Ponderación de intereses por relevancia temporal.
- Visualización de red social (grafo) en UI.
- Pruebas automatizadas de estrés y regresión.

---

## Autor

**Daniel Alfonso Cely**  
Proyecto de curso — Estructuras de Datos (2025)
