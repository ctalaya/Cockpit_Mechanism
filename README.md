# Cockpit de Simulación con Geometría Variable (GT ↔ Fórmula)

## Descripción

Trabajo Fin de Máster que desarrolla el diseño y análisis mecánico de un cockpit
de simulación de conducción capaz de transformar su geometría entre las
configuraciones ergonómicas **GT** y **Fórmula** mediante un mecanismo
reconfigurable sincronizado, accionado por dos entradas independientes: el giro
del asiento sobre el H-Point y un actuador lineal.

El sistema integra estudio antropométrico y ergonómico, diseño conceptual,
análisis cinemático (grados de libertad, ecuación de Grübler-Kutzbach), análisis
dinámico (ecuaciones de Newton-Euler) y validación estructural mediante el método
de elementos finitos (FEM) en ANSYS.

## Contenido del repositorio

```
├── Calculo/        # Proyectos de ANSYS Rigid Dynamics y ANSYS Mechanical
├── Diseño 3D/      # Modelo CAD del mecanismo (CATIA V5)   
```

## Descripción del mecanismo

El mecanismo reconfigurable transforma la posición de conducción entre GT y
Fórmula mediante el movimiento coordinado del asiento, la pedalera y el módulo
volante-pantalla.

**Grados de libertad:** M = 2 (según la ecuación de Grübler-Kutzbach para
mecanismos planos, considerando 8 eslabones, 8 pares inferiores y 3 pares
superiores).

* **Entrada 1 — Giro del asiento (θ1):** el asiento pivota sobre el eje del
H-Point (O), materializado por los componentes Eje y Soporte Eje, solidarios a
la bancada. Un sector de engranaje solidario al asiento engrana con un piñón
(Engranaje Pequeño), que a su vez mueve un Engranaje Grande sobre el mismo eje.
Este engrana con una cremallera solidaria al Volante, que se desplaza guiado
por la Guía Asiento. La traslación del módulo volante-pantalla queda así
completamente determinada por θ1, sin accionamiento propio.
* **Entrada 2 — Actuador lineal:** articulado entre un punto del Asiento (Aa) y
un punto del Brazo Estructural de la Pedalera (Ab). El Brazo Estructural pivota
sobre un punto (Ob) solidario al propio asiento, de forma que su orientación
absoluta resulta de la composición del giro del asiento (θ1) y de su giro
relativo (β) inducido por el actuador. Un engranaje solidario al asiento en Ob
transmite movimiento, mediante cadena, a un segundo engranaje solidario a la
Pedalera (modelado en ANSYS Rigid Dynamics mediante una Constraint Equation
entre las revolutas Asiento-Brazo y Brazo-Pedalera), de modo que la pedalera
gira en proporción directa a β y permanece inmóvil si el actuador no se acciona.

## Requisitos de diseño

* **Rango de usuarios:** estatura entre 150–205 cm, masa entre 50–150 kg
* **Recorridos geométricos GT → Fórmula** (obtenidos por comparación de modelos
antropométricos superpuestos sobre el H-Point):

  * Desplazamiento horizontal del volante: ≈ 103 mm
  * Incremento de altura del volante: ≈ 20 mm
  * Desplazamiento vertical de la pedalera: ≈ 420 mm
  * Variación angular del respaldo: ≈ 22°

## Metodología

1. Definición de requisitos ergonómicos y antropométricos del sistema
2. Generación de alternativas de diseño conceptual y evaluación mediante matriz
de decisión ponderada
3. Selección y descripción detallada de la solución adoptada (sistema de
reconfiguración sincronizado)
4. Modelado CAD 3D del mecanismo en CATIA V5
5. Análisis cinemático: cálculo de grados de libertad y modelo geométrico
6. Análisis dinámico mediante ecuaciones de Newton-Euler, en ANSYS Rigid Dynamics
7. Análisis estructural mediante el método de elementos finitos (FEM) en ANSYS
Mechanical: tensiones, deformaciones, rigidez y factor de seguridad

## Herramientas utilizadas

* **CATIA V5** — modelado 3D del mecanismo
* **ANSYS Rigid Dynamics** — análisis cinemático y dinámico
* **ANSYS Mechanical** — análisis estructural FEM

## Objetivo general

Desarrollar el diseño y análisis mecánico de un cockpit de simulación con
geometría variable, mediante el estudio cinemático y dinámico de un sistema
reconfigurable que permita reproducir diferentes configuraciones de conducción y
determinar los requisitos necesarios para su accionamiento.

## Autor

Carlos Talaya Zamora
Máster Universitario en Ingeniería Industrial — Universidad Internacional de
Valencia (VIU)

