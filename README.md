# Cockpit_Mechanism

Modelos CAD y de simulación de un cockpit de simulación de conducción con geometría variable, capaz de reconfigurarse entre una posición de conducción tipo GT y una posición tipo Fórmula.

Este repositorio contiene los archivos que sustentan los resultados del Trabajo Fin de Máster **«Diseño y análisis cinemático de un cockpit de simulación de conducción con geometría variable»**, Máster Universitario en Ingeniería Industrial, Universidad Internacional de Valencia (VIU), curso 2025–2026.

**Autor:** Carlos Talaya Zamora
**Director:** José Andrés Alvarado Contreras

---

## Descripción del mecanismo

El mecanismo posee **dos grados de libertad** (criterio de Grübler-Kutzbach) gobernados por dos entradas de accionamiento coordinadas:

1. **Giro del asiento** sobre un eje fijo situado en el H-Point del conductor. Este giro arrastra, mediante un tren formado por un sector dentado, un piñón, un engranaje intermedio y una cremallera, el desplazamiento del módulo volante-pantalla sobre una guía inclinada.
2. **Actuador lineal** que gobierna el brazo estructural de la pedalera y, a través de una transmisión por cadena, el giro de la propia pedalera respecto a dicho brazo.

El H-Point permanece fijo durante toda la transformación, lo que constituye el criterio de diseño fundamental del mecanismo: el conductor no se desplaza en altura, sino que rota alrededor de su propio punto de cadera.

---

## Especificaciones de diseño

Recorridos requeridos para la transición GT → Fórmula, referidos al H-Point:

| Magnitud | Valor |
|---|---|
| Desplazamiento horizontal del volante | 237,39 mm |
| Desplazamiento vertical del volante | 70,64 mm |
| Desplazamiento longitudinal de la pedalera | 69,90 mm |
| Desplazamiento vertical de la pedalera | 553,65 mm |
| Giro del asiento sobre el H-Point | 32,5° |
| Giro absoluto de la pedalera | 21° |
| Desplazamiento del H-Point | 0 mm (punto fijo) |

## Parámetros de las transmisiones

**Tren de engranajes del módulo volante** (módulo m = 2 mm, ancho de cara 20 mm)

| Elemento | z | R primitivo |
|---|---|---|
| Sector dentado del asiento | 291 | 291,0 mm |
| Piñón | 20 | 20,0 mm |
| Engranaje intermedio | 30 | 30,0 mm |

Relación de transmisión i₁ = 14,555 · Recorrido de la cremallera 247,68 mm · Inclinación de la guía 16,58°

**Transmisión por cadena de la pedalera** (ISO 08B, paso 12,7 mm)

| Elemento | z | R primitivo |
|---|---|---|
| Piñón solidario al asiento | 27 | 54,70 mm |
| Piñón solidario a la pedalera | 15 | 30,55 mm |

Relación de transmisión i₂ = 1,7905 · Distancia entre ejes 387,0 mm · Longitud de cadena 82 eslabones (1.041,4 mm)

**Actuador lineal**

Longitud de referencia 150,0 mm · Carrera 17,86 mm · Giro relativo del brazo β = 14,55° · Velocidad de extensión 0,595 mm/s · Tiempo de operación 30 s

---

## Resultados de validación

Contraste entre los requisitos de diseño y los valores obtenidos en la simulación cinemática:

| Magnitud | Requisito | Simulación | Desviación |
|---|---|---|---|
| Desplazamiento horizontal del volante | 237,39 mm | 237,41 mm | 0,01 % |
| Desplazamiento vertical del volante | 70,64 mm | 70,64 mm | 0,00 % |
| Desplazamiento longitudinal de la pedalera | 69,90 mm | 70,09 mm | 0,27 % |
| Desplazamiento vertical de la pedalera | 553,65 mm | 551,46 mm | −0,40 % |
| Giro del asiento sobre el H-Point | 32,50° | 32,504° | 0,01 % |
| Giro absoluto de la pedalera | 21,00° | 21,04° | 0,19 % |

## Resultados dinámicos

Solicitaciones obtenidas en el análisis dinámico, por lateral del mecanismo:

| Magnitud | t = 0 s (GT) | t = 30 s (Fórmula) |
|---|---|---|
| Reacción en el apoyo del H-Point | 1.007,40 N | 1.007,40 N |
| Guía del módulo volante-pantalla | 305,90 N | 305,90 N |
| Revoluta brazo-pedalera | 249,48 N | 249,47 N |
| Revoluta asiento-brazo | 2.469,40 N | 3.511,60 N |
| Pasadores del actuador | 2.455,20 N | 3.667,40 N |
| Fuerza del actuador lineal | 2.455,70 N | 3.665,70 N |
| Par en el eje del H-Point | 141,93 N·m | 138,45 N·m |

El par alcanza su valor máximo de 151,71 N·m en t = 13,82 s. El mecanismo no presenta un instante crítico común a todas sus piezas: las solicitaciones de origen gravitatorio permanecen constantes, mientras que las asociadas al accionamiento del brazo crecen de forma monótona hasta la configuración Fórmula.

## Verificación resistente de las transmisiones

Acero S275JR, límite elástico 275 MPa.

| Elemento | Tensión | Factor de seguridad |
|---|---|---|
| Sector dentado (Lewis) | 5,69 MPa | 48,3 |
| Piñón (Lewis) | 8,56 MPa | 32,1 |
| Cremallera (Lewis) | 3,80 MPa | 72,5 |
| Cadena ISO 08B-1 (rotura) | T = 775 N | 23,2 |

Ambas transmisiones quedan gobernadas por las exigencias cinemáticas y no por las resistentes, lo que deja un margen de optimización económica pendiente de estudio específico.

---

## Estructura del repositorio

```
Cockpit_Mechanism/
├── Diseño 3D/
│   └── V2/              Modelo tridimensional del mecanismo (CATIA V5)
├── Calculo/             Modelos de simulación y exportaciones de resultados
├── .gitattributes       Configuración de Git LFS
└── README.md
```

### Diseño 3D/V2

Modelo tridimensional completo del mecanismo elaborado en CATIA V5, en sus dos configuraciones extremas. Incluye las cinco piezas estructurales analizadas (eje del H-Point, asiento, brazo estructural de la pedalera, pedalera y soporte del volante-pantalla) y los componentes de las transmisiones.

### Calculo

Modelos de simulación y resultados exportados:

- **Ansys Rigid Dynamics** — análisis cinemático y dinámico del mecanismo completo a lo largo de los 30 s de la transformación.
- **Ansys Mechanical** — análisis estructural estático de cada una de las cinco piezas.
- **Exportaciones de resultados** en formato `.xlsx`, con 603 pasos de tiempo cada una:
  - `Cinematica.xlsx` — giros, velocidades y aceleraciones angulares de los tres ejes principales.
  - `Fuerzas_internas.xlsx` — fuerzas transmitidas en las seis uniones del mecanismo.
  - `Fuerzas_actuador_y_par.xlsx` — fuerza requerida en el actuador lineal y par en el eje del H-Point.

---

## Nota sobre las Constraint Equations

Los engranajes y la transmisión por cadena se han modelado sin dentado, representándolos por sus cilindros primitivos. Las relaciones de transmisión se imponen mediante **Constraint Equations** sobre los grados de libertad de los joints, procedimiento documentado por Ansys para vincular velocidades angulares sin necesidad de modelar el contacto entre dientes.

Esta simplificación es deliberada: el objetivo del análisis es verificar la cinemática de la transformación, no evaluar tensiones de contacto en el dentado. Como consecuencia, el modelo no proporciona fuerzas de engrane ni presiones de contacto, y la transmisión es ideal, sin holguras ni pérdidas por rozamiento.

Debe señalarse que, al no derivarse estas ecuaciones de la geometría sino imponerse explícitamente, el programa reproduce la relación indicada sea o no la correcta. La verificación independiente de las magnitudes de salida frente a los requisitos de partida resulta, por tanto, imprescindible.

---

## Requisitos de software

| Software | Versión empleada |
|---|---|
| CATIA V5 | — |
| Ansys Mechanical / Rigid Dynamics | 2025 R1 |
| Git LFS | Necesario para clonar el repositorio |

## Clonado del repositorio

Los archivos de modelado y simulación se almacenan mediante **Git Large File Storage**. Es necesario instalar Git LFS antes de clonar:

```bash
git lfs install
git clone https://github.com/ctalaya/Cockpit_Mechanism.git
```

Sin Git LFS, el clonado descargará únicamente los punteros a los archivos, no su contenido.

---

## Licencia y uso

Este repositorio se publica con fines académicos, como material de soporte y verificación del Trabajo Fin de Máster referido. Cualquier uso posterior de su contenido debe citar la fuente:

> Talaya Zamora, C. (2026). *Cockpit_Mechanism: modelos CAD y de simulación de un cockpit reconfigurable* [Repositorio de software]. GitHub. https://github.com/ctalaya/Cockpit_Mechanism
