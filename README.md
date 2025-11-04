# Retail-CSV-Analytics-Lightweight-NLP

Functional data tasks on a small retail dataset plus regex-based sentence mining. The notebook demonstrates robust CSV I/O with EU formats (encodings/decimal separators/dates), tidy Pandas transformations, basic functional programming patterns, ZIP handling, and simple NLP with regular expressions. Built in Python for the UOC PAC2.

---

## Highlights

* **Robust data loading**: automatic path discovery, multi-encoding fallback (`utf-8`, `latin-1`, `cp1252`), `sep=';'`, `decimal=','`, and `parse_dates`.
* **Clean transformations**: sorting, derived date column, category/product aggregations, payment totals between dates.
* **Functional patterns**: `map`, `filter`, `reduce` used in small utilities over DataFrames/iterables.
* **File operations**: safe ZIP extraction and file size reporting (MiB).
* **Lightweight NLP**: regex with word boundaries to extract sentences containing exact terms from public-domain texts.
* **Simple, readable code** with docstrings and unit-style demos in each exercise cell.

---

## Repository structure

```
.
├── Victor_Suesta_Arribas_PEC2.ipynb   # Main notebook with all exercises (E1–E6)
├── botiga_en_linia.csv                # Retail transactions (EU formatting)
├── Dracula.txt                        # Public-domain text (Gutenberg)
├── SleepyHollow.txt                   # Public-domain text (Gutenberg)
├── LICENSE
└── README.md
```

---

## What’s inside (E1–E6)

**E1 – gcd (Euclid, iterative)**

* `my_gcd(a, b, verbose=False)` mirrors `math.gcd` and can print the algorithm steps.

**E2 – Retail CSV analytics**

* Robust loader → `DataFrame`.
* 2.1: first 100 rows sorted by `Country`, `Date`.
* 2.2: new `Fecha` column in `dd/mm/yyyy`.
* 2.3: `Retorna_productes_categoria(categoria) → dict` with units per product and `_total`.
* 2.4: `Import_total_tipus_pagament(metodo, fecha_ini, fecha_fin) → str` with formatted EUR total.

**E3 – Customer × Country dictionary (FP style)**

* `create_dictionary(ruta_csv, customer_id) → {country: [(product, units), ...]}`
  Uses `map`/`filter`/`reduce` on grouped totals.

**E4 – Product filter via regex-like rules**

* `productos_diccionario_regex(df) → {product: mean_unit_price}` for names containing **“ni”** or **“te”** or starting with **“u”** (case-insensitive).

**E5 – ZIP handling**

* `zip_decompression(zip_path, out_dir)` and
  `tamanio_archivos_mb(dir, name1, name2) → (mb1, mb2)`.

**E6 – Lightweight NLP**

* `process_book(path, pattern) → List[str]`
  Sentence splitter (keeps `.`/`?`), case-insensitive regex with **word boundaries** (e.g., `\b(dracula|castle)\b`, `\bsleep\b`).

---

## Quick start

### Run in Google Colab

1. Upload the four files to your workspace (or mount Drive).
2. Open `Victor_Suesta_Arribas_PEC2.ipynb` and run cells in order.

   * The loader auto-detects typical paths, including Colab Drive folders.

### Run locally

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install pandas
# Open the notebook in Jupyter/VS Code and run top to bottom
```

---

## Example outputs (abridged)

* **E2.4**
  `Por el método de pago Transferència, se han cobrado 682.032,72 Euros entre el 01/01/2023 y el 31/12/2023.`

* **E6 (Dracula)**
  72 sentences matched for `\b(dracula|castle)\b`.
  *(Sleepy Hollow)* 2 sentences matched for `\bsleep\b`.

*(Counts may vary if the CSV/texts are updated.)*

---

## Notes & design choices

* EU-style CSV support (`;` separator, `,` decimal) to prevent silent parse errors.
* Encoding fallback avoids crashes on accented characters; last-resort `errors="replace"`.
* Word-boundary regexes ensure **exact** matches (e.g., `Castle` but not `Newcastle`).
* Printing/demo blocks are included to make grading straightforward and reproducible.

---

## License

MIT — see `LICENSE`.

---

## Author

Víctor Suesta — M.Sc. Data Science (UOC).
Feel free to open issues or suggestions for improvements.
