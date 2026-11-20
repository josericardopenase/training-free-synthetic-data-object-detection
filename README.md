# Controllable Synthetic Data for Data-Efficient Object Detection

Preprint (IVC 2026): pipeline **sin entrenamiento adicional** para generar datos sintéticos de detección de objetos con modelos de difusión y pseudo-etiquetado automático (Grounded SAM).

**Autores:** Jose R. Peña-Seco, Jonay Suárez-Ramírez, Adrian Penate-Sanchez, Nelson Monzón  
**Afiliaciones:** ULPGC · QAISC

## Resumen breve

Los detectores de objetos dependen de anotaciones caras y poco representativas en dominios reales. Este trabajo propone un pipeline *training-free* que:

1. Genera prompts estructurados (clase, entorno, clima, cantidad) con un LLM (Mistral-7B-Instruct).
2. Sintetiza imágenes con un modelo text-to-image (FLUX).
3. Pseudo-etiqueta con Grounded SAM usando la estrategia **one-category-per-image** para reducir falsos positivos y fallos con etiquetas domain-specific.
4. Entrena detectores (YOLO26, RT-DETR) mezclando datos reales y sintéticos.

**Resultados destacados**

- Hasta **+9.0 pp AP50** en PASCAL VOC con datos completos + sintéticos.
- Hasta **+35.4 pp AP50** en régimen low-data (1 000 imágenes reales).
- En el dataset industrial *Vessels & Boats*, un tercio de datos reales + sintéticos iguala el AP del conjunto real completo.
- La utilidad del sintético depende del dominio (p. ej. beneficios claros en VOC / maritime; transfer limitado en KITTI).

## Página web (GitHub Pages)

La página del proyecto está en [`docs/`](docs/):

| Ruta | Contenido |
|------|-----------|
| `docs/index.html` | Sitio estático del paper (método, figuras, tablas, citación) |
| `docs/assets/figures/` | Figuras del manuscript optimizadas para la web |

La fuente LaTeX del preprint **no** está en `docs/` (GitHub Pages) para evitar filtrarla antes de arXiv.

Código: [training-free-synthetic-data-object-detection](https://github.com/josericardopenase/training-free-synthetic-data-object-detection)

### Activar GitHub Pages

1. Sube el repositorio a GitHub.
2. **Settings → Pages → Build and deployment**
3. Source: **Deploy from a branch**
4. Branch: `main` (o la que uses) · Folder: **`/docs`**
5. La URL quedará en `https://<usuario>.github.io/<repo>/`

Vista local:

```bash
cd docs && python3 -m http.server 8000
# abrir http://localhost:8000
```

## Estructura del repositorio

```
difu-paper/
├── README.md
├── docs/                       # GitHub Pages (público)
│   ├── index.html
│   └── assets/figures/         # 9 figuras web
├── paper/                      # Fuente LaTeX (local; en .gitignore)
├── charts.ipynb
├── dataset_transfer.ipynb
└── training_history/
```

### Figuras en la web (alineadas con el manuscript)

1. Pipeline completo  
2. Ejemplos sintéticos anotados  
3. One-category / etiquetas domain-specific  
4. Escalado VOC (full-data)  
5. Comparación de detectores  
6. Escalado VOC (low-data)  
7–9. Análisis synthetic-to-real (t-SNE domain/cluster + métricas)

## Citación

```bibtex
@article{penaseco2026controllable,
  title={Controllable Synthetic Data Generation for Data-Efficient Object Detection in Real-World Domains},
  author={Pe{\~n}a-Seco, Jose R. and Su{\'a}rez-Ram{\'i}rez, Jonay and Penate-Sanchez, Adrian and Monz{\'o}n, Nelson},
  journal={Image and Vision Computing (preprint)},
  year={2026}
}
```

## Keywords

Synthetic data · diffusion models · automatic annotation · Grounded SAM · pseudo-labeling · one-category-per-image · object detection · low-data regime · lightweight detectors
