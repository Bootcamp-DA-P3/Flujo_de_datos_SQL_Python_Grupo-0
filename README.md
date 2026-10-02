# Flujo de datos de SQL a Python · Proyecto III

Plantilla del **Proyecto III** del Bootcamp de Data Analyst. Copiad esta estructura en el repositorio de vuestro equipo.

> [!IMPORTANT]
> Antes de escribir una sola línea de SQL, **declarad el grano**: ¿qué representa una fila de vuestro dataset?
> Lo escribís en la cabecera de cada `.sql` y en el README de vuestra entrega.

---

## 📁 Estructura

```
.
├── sql/                               ← las TRES consultas, en SQL Workbench
│   ├── df1_actividad_clientes.sql
│   ├── df2_catalogo_productos.sql
│   └── df3_vendedores_popularidad.sql
│
├── src/                               ← el código, en VS Code
│   ├── config.py                        lee las credenciales del .env
│   └── main.py                          conecta, consulta y exporta el CSV
│
├── notebooks/
│   └── limpieza.ipynb                 ← la limpieza final, en Colab o VS Code
│
├── data/                              ← el CSV exportado. NO se sube
│   └── .gitkeep
│
├── .env                               ← vuestras credenciales. NO se sube
├── .env_example                         plantilla del anterior, SÍ se sube
├── .gitignore
├── requirements.txt
└── README.md                          ← documentad aquí vuestras decisiones
```

---

## 🔢 En qué orden crear las cosas

Seguid este orden. Cada paso depende del anterior.

### 1 · Cargad la base de datos

Descargad `olist.sql.gz` de la carpeta de formación y cargadlo en MySQL. Comprobad que funcionó:

```sql
USE olist;
SELECT COUNT(*) FROM orders;   -- 99441
```

### 2 · Las tres consultas — **en MySQL Workbench**

Aquí es donde se piensa. Trabajad en Workbench porque veis el resultado al instante y podéis iterar.

Escribid las tres consultas, **una por fichero**, en `sql/`. Las tres son obligatorias.

En cada fichero, lo primero es la línea del grano:

```sql
-- GRANO DECLARADO: una fila = un pedido entregado
```

Cuando una consulta os convenza, **pegadla en su `.sql`**. Ese fichero es parte de la entrega.

> [!NOTE]
> Las tres consultas van al repositorio aunque **solo una** continúe hasta el CSV y el notebook.
> Se evalúan las tres: demuestran que sabéis recorrer el modelo por caminos distintos.

### 3 · Elegid una de las tres

La que vayáis a limpiar a fondo. Justificad la elección en vuestro README.

### 4 · Las credenciales — **en VS Code**

Copiad `.env_example` a `.env` y poned vuestra contraseña real:

```bash
cp .env_example .env
```

> [!WARNING]
> **`.env` nunca se sube.** Ya está en `.gitignore`. Contiene vuestra contraseña de MySQL.
> El que sí se sube es `.env_example`, con `TU_PASSWORD` de relleno, para que otro sepa qué variables hacen falta.

### 5 · El entorno — **en VS Code**

```bash
python -m venv .venv
.venv\Scripts\activate        # Windows
source .venv/bin/activate     # macOS y Linux
pip install -r requirements.txt
```

### 6 · El código — **en VS Code**

Los dos ficheros vienen con el esqueleto hecho y las funciones vacías.

- **`src/config.py`** — ya está terminado. Lee las credenciales del `.env`. No hay que tocarlo.
- **`src/main.py`** — tiene la estructura y cuatro funciones por implementar, cada una con su `TODO`.

Lo primero es rellenar las tres líneas de arriba del fichero:

```python
CONSULTA = "df1_actividad_clientes.sql"   # cuál de las tres lleváis al CSV
GRANO = ""                                # una fila = ...
CLAVE_DE_GRANO = ""                       # la columna que lo identifica
```

> [!NOTE]
> El script **no arranca** hasta que `GRANO` y `CLAVE_DE_GRANO` estén rellenos. Es a propósito.

Ejecutadlo desde la **raíz del proyecto**, no desde dentro de `src/`:

```bash
python src/main.py
```

Una de las funciones es `comprobar_grano()`: compara el número de filas con el de claves distintas y avisa si el `JOIN` está multiplicando. Implementadla antes que `exportar()`.

### 7 · La limpieza final — **en el notebook**

`notebooks/limpieza.ipynb` lee el CSV de `data/`, termina la limpieza en pandas y exporta el dataset final.

---

## 🧰 Qué se hace en cada herramienta

| Herramienta | Para qué |
| :--- | :--- |
| **MySQL Workbench** | Explorar el modelo, escribir y probar las tres consultas, limpieza preliminar en SQL |
| **VS Code** | El entorno virtual, `config.py`, `main.py` y el control de versiones |
| **Notebook** | Limpieza final en pandas, validación y exportación del dataset |

La frontera: **SQL filtra, une y agrega** en el servidor. **Python hace lo que viene después.**

---

## 🚫 Qué NO se sube al repositorio

Ya está configurado en `.gitignore`. No lo toquéis:

| | Por qué |
| :--- | :--- |
| **`.env`** | Lleva vuestra contraseña de MySQL |
| **`data/`** | Los CSV pesan y se regeneran ejecutando el script. Solo viaja `.gitkeep`, para que la carpeta exista al clonar y el script no falle |
| **`.venv/`** | Se reconstruye con `requirements.txt` |
| **`__pycache__/`** | Lo genera Python |

> [!TIP]
> Antes de vuestro primer commit: `git status`. Si veis `.env` o algún `.csv` en la lista, algo va mal.

---

## ✅ Antes de entregar

- [ ] Las **tres** consultas están en `sql/`, cada una con su grano declarado en la cabecera
- [ ] `README.md` explica qué dataframe elegisteis y por qué
- [ ] `README.md` documenta los criterios de limpieza y las decisiones tomadas
- [ ] `python src/main.py` funciona desde la raíz en una máquina limpia
- [ ] El notebook se ejecuta de arriba abajo sin errores
- [ ] `git status` no muestra `.env` ni ficheros de `data/`
- [ ] Comprobación del grano: `COUNT(*)` coincide con `COUNT(DISTINCT <clave de negocio>)`
