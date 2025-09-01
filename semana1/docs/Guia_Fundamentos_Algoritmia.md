---
title: Guía de Estudio - Fundamentos de Algoritmia y Resolución de
  Problemas
---

Esta guía detalla el primer bloque del roadmap: Fundamentos de
Algoritmia y Resolución de Problemas. El objetivo es desarrollar lógica,
rapidez y pensamiento algorítmico a través del estudio teórico y la
práctica en plataformas de programación.

# 🔹 Objetivo Principal

Desarrollar lógica, rapidez y pensamiento algorítmico para resolver
problemas de programación de manera eficiente y escalable.

# 🧩 ¿Qué es un algoritmo?

Un algoritmo es un conjunto de pasos lógicos y ordenados para resolver
un problema. En programación, se traduce en código que toma una entrada,
procesa la información y devuelve una salida.

Ejemplo: Algoritmo para encontrar el mayor de dos números:\
1. Recibir dos números.\
2. Compararlos.\
3. Devolver el mayor.

# 📚 Estructuras de Datos Básicas a Dominar

-   Listas / Arrays: Colección de elementos ordenados. Operaciones
    clave: insertar, eliminar, recorrer, buscar.

-   Pilas (Stacks): LIFO (Last In, First Out). Ejemplo: sistema de
    deshacer (Ctrl+Z).

-   Colas (Queues): FIFO (First In, First Out). Ejemplo: sistema de
    turnos en un banco.

-   Árboles: Estructura jerárquica con nodos y ramas. Ejemplo: árbol de
    directorios en un sistema operativo.

-   Grafos: Conjunto de nodos conectados por aristas. Ejemplo: red
    social (usuarios = nodos, amistades = conexiones).

# ⚡ Plataformas para Practicar

\- HackerRank: ideal para problemas básicos y práctica de lógica.\
- LeetCode: orientado a entrevistas técnicas con problemas de fácil a
difícil.\
\
Consejo: Resolver al menos un problema fácil al día e ir aumentando la
dificultad. Revisar soluciones de otros para aprender diferentes
enfoques.

# 📊 Habilidades a Desarrollar

-   Analizar un problema: identificar qué pide exactamente.

-   Diseñar un algoritmo: usar la estructura de datos adecuada.

-   Evaluar eficiencia: aplicar notación Big-O (tiempo y espacio).

-   Optimizar soluciones: mejorar código a versiones más rápidas y
    limpias.

# 📝 Ejemplo Práctico

Problema: Encontrar el primer número repetido en una lista.

def primer_repetido(lista):\
vistos = set()\
for num in lista:\
if num in vistos:\
return num\
vistos.add(num)\
return None\
\
print(primer_repetido(\[3, 5, 2, 3, 6, 2\])) \# Resultado: 3

\- Estructura usada: set (para buscar en O(1)).\
- Complejidad: O(n) en tiempo.
