# Brecha Digital Territorial — Región Cusco, Perú

## Descripción del proyecto y pregunta de investigación

Este proyecto mide la **brecha digital territorial** en la región de Cusco, Perú, comparando dos indicadores derivados de satélite:

- **Luces nocturnas NASA VNL 2025** (EPSG:4326): proxy de urbanización y actividad económica.
- **Densidad de cobertura de red móvil OSIPTEL 2019** — kernel de 50 m (EPSG:32719): indicador de acceso a internet móvil.

**Pregunta de investigación:** ¿En qué zonas de la región Cusco existe una desconexión entre el nivel de urbanización y el acceso a conectividad móvil, y qué territorios presentan mayor riesgo de exclusión digital?

---

## Estructura del repositorio

```
raster-digital-divide/
│
├── data/                             # Datos de entrada (solo locales, no en repo)
│   ├── VNL_cusco_2025.tif
│   └── kernel_cobmovil2019_50m.tif
│
├── notebooks/
│   └── digital_divide_cusco.ipynb   # Notebook principal de análisis
│
├── output/
│   ├── vnl_norm.tif                 # VNL normalizado [0–1]
│   ├── conn_norm.tif                # Conectividad normalizada [0–1]
│   ├── ibd_brecha_digital.tif       # Índice de Brecha Digital [-1, 1]
│   ├── clasificacion_brecha.tif     # Clasificación territorial 4 clases
│   └── dashboard_brecha_digital.png # Panel compuesto final (150 dpi)
│
├── README.md
└── requirements.txt
```

---

## Dependencias e instalación

```bash
pip install -r requirements.txt
```

Versiones mínimas requeridas:

| Librería    | Versión |
|-------------|---------|
| rasterio    | ≥ 1.3.0 |
| numpy       | ≥ 1.24.0 |
| matplotlib  | ≥ 3.7.0 |
| scipy       | ≥ 1.10.0 |
| seaborn     | ≥ 0.12.0 |
| pandas      | ≥ 2.0.0 |
| jupyter     | ≥ 1.0.0 |

---

## Cómo ejecutar el notebook

1. **Clona el repositorio** y coloca los datos en `data/`:
   ```bash
   git clone <url-repo>
   cd raster-digital-divide
   # Copia VNL_cusco_2025.tif y kernel_cobmovil2019_50m.tif en data/
   ```

2. **Instala dependencias:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Ejecuta el notebook:**
   ```bash
   cd notebooks
   jupyter notebook digital_divide_cusco.ipynb
   # O para ejecutar desde línea de comandos:
   jupyter nbconvert --to notebook --execute --inplace digital_divide_cusco.ipynb
   ```

4. Los archivos de salida se generarán automáticamente en `output/`.

---

## Descripción de archivos de salida

| Archivo | Descripción |
|---|---|
| `vnl_norm.tif` | Luces nocturnas VNL normalizadas al rango [0, 1] mediante percentiles [2–98]. |
| `conn_norm.tif` | Conectividad móvil reproyectada a EPSG:4326 y normalizada [0, 1]. |
| `ibd_brecha_digital.tif` | Índice de Brecha Digital = VNL_norm − Conn_norm. Valores positivos = brecha activa. |
| `clasificacion_brecha.tif` | Clasificación 2×2 con umbral 0.15: 1=Urbana conectada, 2=División urbana, 3=Rural conectada, 4=División crítica. |
| `dashboard_brecha_digital.png` | Panel compuesto con los 6 mapas temáticos del análisis completo. |

---

## Principales hallazgos

La región Cusco muestra una **correlación débil** entre iluminación nocturna y cobertura móvil, lo que evidencia que la expansión de red no ha seguido el ritmo de urbanización. La clasificación territorial revela que la mayoría del territorio cae en la categoría **"División Crítica"** (alta VNL, baja conectividad), con focos de brecha digital activa concentrados en los valles interandinos y corredores viales periurbanos. Las zonas de mayor riesgo de exclusión social coinciden con áreas de alta ruralidad y escasa actividad económica nocturna, especialmente en el cuadrante suroriental de la región.

---

## Datos fuente

- **VNL 2025:** NASA Black Marble — VIIRS Day/Night Band. EPSG:4326.
- **Cobertura móvil 2019:** OSIPTEL Perú — kernel de densidad a 50 m. EPSG:32719.
- **Descarga:** [Google Drive — Carpeta del proyecto](https://drive.google.com/drive/folders/16oP-IEX8EWklvuigtt-cTWJfDdD4E0ec?usp=drive_link)
