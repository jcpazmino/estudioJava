# ¿Qué es aplicar notación Big-O?

Aplicar **notación Big-O** significa **describir la eficiencia de un algoritmo** en función de cuánto crecen sus **tiempo de ejecución** ⏱️ y/o **uso de memoria** 💾 conforme aumenta el tamaño de la entrada (`n`).  

No mide tiempos exactos (segundos), sino cómo **escala** el algoritmo.  

---

## 🔹 ¿Cómo se aplica la notación Big-O?
1. **Identificar las operaciones dominantes** del algoritmo (las que más se repiten o más afectan el tiempo).  
2. **Relacionar el número de operaciones con el tamaño de la entrada** (`n`).  
3. **Expresar el crecimiento en notación Big-O**, simplificando a la peor complejidad (worst case).  

---

## 🔹 Ejemplos prácticos en JavaScript

### O(1) → Tiempo constante
```javascript
let arr = [10, 20, 30];
console.log(arr[0]);  // Acceso directo siempre tarda lo mismo
```

### O(n) → Tiempo lineal
```javascript
let arr = [10, 20, 30];
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);  // Recorre todos los elementos
}
```

### O(n²) → Tiempo cuadrático
```javascript
let arr = [1, 2, 3];
for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
        console.log(arr[i], arr[j]);  // Comparación anidada
    }
}
```

### O(log n) → Tiempo logarítmico
```javascript
function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;
    while (left <= right) {
        let mid = Math.floor((left + right) / 2);
        if (arr[mid] === target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
console.log(binarySearch([1,3,5,7,9,11], 7));  // O(log n)
```

---

## 🔹 ¿Por qué es útil?
- Permite **comparar algoritmos** independientemente del hardware.  
- Ayuda a decidir cuál es más adecuado en casos con **grandes volúmenes de datos**.  
- Evita cuellos de botella en sistemas que requieren escalar.  

👉 En resumen: aplicar Big-O es como ponerle “una etiqueta de eficiencia” a tu algoritmo para saber cómo se comportará cuando los datos crezcan.  
