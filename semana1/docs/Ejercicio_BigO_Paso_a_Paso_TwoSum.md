# Ejercicio práctico paso a paso: Análisis Big-O con *Two Sum* (HashMap vs. doble bucle)

## 🎯 Enunciado
Dado un arreglo de enteros `nums` y un entero `target`, devuelve los **índices** de los dos números cuya suma es igual a `target`.  
Si no existen, devuelve `[-1, -1]`.

**Ejemplo**
```
nums = [2, 7, 11, 15], target = 9  ->  salida: [0, 1]   // 2 + 7 = 9
nums = [3, 2, 4],        target = 6  ->  salida: [1, 2]   // 2 + 4 = 6
```

---

## 🎯 Objetivo del análisis
1) Diseñar **dos soluciones** (ingenua y optimizada).  
2) **Contar operaciones** para aproximar el tiempo de ejecución.  
3) Expresar la **complejidad temporal y espacial en notación Big-O**.  
4) Discutir **casos borde** y compararlas.

---

## 1) Solución ingenua: doble bucle (*brute force*)

### Idea
Probar **todas las parejas** `(i, j)` con `i < j` y verificar si `nums[i] + nums[j] == target`.

### Código (JavaScript)
```javascript
function twoSumBruteForce(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
  return [-1, -1];
}
```

### Conteo aproximado de operaciones
- Bucle externo recorre `n` veces.
- Bucle interno recorre en promedio ~`(n-1)/2` veces por cada `i`.
- Comparación y suma en cada iteración → operación constante `c`.

**Tiempo total** (aproximado):  
`T(n) ≈ c * (n * (n-1) / 2) + a*n + b  = (c/2) * (n^2 - n) + a*n + b`  
**Big-O temporal**: `O(n^2)` (los términos cuadráticos dominan).  
**Big-O espacial**: `O(1)` espacio extra (no usa estructuras auxiliares proporcionalmente a `n`).

---

## 2) Solución optimizada: HashMap (Map) en una pasada

### Idea
Mientras recorres el arreglo una sola vez, guarda en un **Map** lo que necesitas para encontrar el complemento.  
Para cada `num`, verifica si ya viste `target - num`. Si sí, devuelve los índices.

### Código (JavaScript)
```javascript
function twoSumMap(nums, target) {
  const map = new Map(); // valor -> índice
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
  return [-1, -1];
}
```
### Explicación function twoSumMap

La función `twoSumMap(nums, target)` resuelve el problema de encontrar dos índices en el arreglo `nums` cuyos valores suman exactamente el valor `target`, utilizando un enfoque eficiente basado en un HashMap (objeto `Map` en JavaScript).

**Funcionamiento paso a paso:**

1. **Inicialización:**  
  Se crea un nuevo objeto `Map` llamado `map`. Este se usará para almacenar cada número del arreglo como clave y su índice como valor.

2. **Recorrido del arreglo:**  
  Se recorre el arreglo `nums` con un ciclo `for`, donde `i` es el índice actual.

3. **Cálculo del complemento:**  
  Para cada elemento `nums[i]`, se calcula el complemento necesario para llegar al `target`:  
  `complement = target - nums[i]`

4. **Verificación en el HashMap:**  
  Se verifica si el complemento ya existe en el `map`.  
  - Si existe, significa que previamente se encontró un número tal que, sumado al actual, da el `target`.  
  - Se retorna un arreglo con los índices: `[map.get(complement), i]`.

5. **Almacenamiento en el HashMap:**  
  Si el complemento no existe, se almacena el valor actual `nums[i]` junto con su índice `i` en el `map`.

6. **Caso sin solución:**  
  Si termina el ciclo sin encontrar una pareja que sume el `target`, retorna `[-1, -1]`.

**Ventajas:**
- Este método tiene complejidad O(n), ya que recorre el arreglo una sola vez y las búsquedas/inserciones en el `Map` son O(1).
- Es mucho más eficiente que la solución de fuerza bruta (O(n²)), especialmente para arreglos grandes.

### Conteo aproximado de operaciones
- Un solo bucle que recorre `n` elementos → `n` iteraciones.
- En cada iteración: cálculo `complement`, `map.has(...)` y `map.set(...)` → operaciones promedio `O(1)`.

**Tiempo total** (promedio): `T(n) ≈ a*n + b`  
**Big-O temporal**: `O(n)` promedio (en el peor caso teórico por muchas colisiones de hash podría degradar a `O(n^2)`, pero no es común).  
**Big-O espacial**: `O(n)` (el `Map` puede almacenar hasta `n` pares valor-índice).

---

## 3) Comparación de enfoques

| Enfoque          | Tiempo (Big-O) | Espacio (Big-O) | Cuándo usar |
|------------------|-----------------|-----------------|-------------|
| Doble bucle      | `O(n^2)`        | `O(1)`          | Listas pequeñas o cuando no puedes usar memoria extra |
| HashMap (Map)    | `O(n)`          | `O(n)`          | Entrada grande, buscas eficiencia y puedes usar memoria adicional |

---

## 4) Casos borde a considerar
- **No hay solución** → `[-1, -1]`.
- **Múltiples soluciones** → devolver la primera encontrada basta, a menos que se pida lo contrario.
- **Valores repetidos** → el Map maneja bien duplicados, pero recuerda el **orden de índices**.
- **Números negativos** → la lógica no cambia.
- **Arreglo muy grande** → preferir el enfoque `O(n)` por escalabilidad.

---

## 5) Pruebas rápidas

```javascript
console.log(twoSumBruteForce([2,7,11,15], 9));  // [0, 1]
console.log(twoSumBruteForce([3,2,4], 6));      // [1, 2]
console.log(twoSumBruteForce([3,3], 6));        // [0, 1]
console.log(twoSumBruteForce([1,2,3], 7));      // [-1, -1]

console.log(twoSumMap([2,7,11,15], 9));         // [0, 1]
console.log(twoSumMap([3,2,4], 6));             // [1, 2]
console.log(twoSumMap([3,3], 6));               // [0, 1]
console.log(twoSumMap([1,2,3], 7));             // [-1, -1]
```

---

## 6) Paso adicional: tercera vía con *sorting*

1) Ordena el arreglo (y guarda índices originales).  
2) Usa dos punteros (izq/der) para buscar el `target`.

**Complejidad**: ordenar `O(n log n)` + dos punteros `O(n)` → `O(n log n)` tiempo;  
espacio `O(1)` extra si el sort es in-place (en JS el sort puede no ser in-place en todos los motores).

> Útil cuando el uso de memoria extra es un problema y el coste `O(n log n)` es aceptable.

---

## 7) Preguntas de autoevaluación
1) ¿Por qué la solución con Map es `O(n)` en promedio?  
2) ¿Qué condición del input podría degradar el rendimiento de un hash a peor caso?  
3) ¿Cuándo preferirías un algoritmo `O(n^2)` que usa `O(1)` espacio sobre uno `O(n)` que usa `O(n)` espacio?  
4) En el enfoque de *sorting* + dos punteros, ¿por qué el tiempo total es `O(n log n)` y no `O(n)`?

**Respuestas (guía breve):**
1) Porque cada operación `has/get/set` es `O(1)` promedio y recorremos el arreglo una sola vez.  
2) Muchas colisiones de hash o una mala función hash. En la práctica de los *runtime*, suele ser suficientemente buena.  
3) Si `n` es pequeño o la restricción de memoria es muy estricta.  
4) Porque **ordenar** domina el costo con `O(n log n)`; el barrido con dos punteros es lineal.

---

## 8) Extensiones y variaciones
- Devolver **los valores** en lugar de índices.  
- Considerar **índices 1-based**.  
- Si el input está **ordenado**, usar directamente **dos punteros** `O(n)` sin Map.  
- Hacer la versión que devuelve **todas** las parejas.

---

## 9) Conclusión
Aplicar notación Big-O consiste en **razonar** sobre el crecimiento del costo de un algoritmo a medida que `n` aumenta.  
Este ejercicio muestra cómo partir de una solución `O(n^2)` e iterar hacia una de `O(n)` con un HashMap, evaluando **tiempo y espacio**.
