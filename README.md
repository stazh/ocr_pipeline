# Lokale OCR-Pipeline (Jupyter + Tesseract + Calamari/Fraktur)

Diese Repo enthält bereits `testbild.png` sowie zwei Notebooks:

- `notebooks/01_setup_local_ocr.ipynb`
- `notebooks/02_ocr_pipeline_tesseract_calamari.ipynb`

## 1) Lokale Voraussetzungen (getesteter Weg)

Systempakete (macOS/Homebrew):

```bash
brew install tesseract tesseract-lang python@3.11
```

Virtuelle Umgebung mit Python 3.11:

```bash
/opt/homebrew/bin/python3.11 -m venv .venv311
.venv311/bin/pip install --upgrade pip setuptools wheel
.venv311/bin/pip install jupyterlab pytesseract pillow numpy matplotlib calamari-ocr==2.3.1
```

Jupyter-Kernel für die `.venv311` registrieren:

```bash
.venv311/bin/python -m ipykernel install --user --name ocr_venv311 --display-name "OCR (.venv311)"
```

Hinweise:

- Für Tesseract-Fraktur brauchst du passende Sprachdaten (z. B. `frk`). Mit `tesseract-lang` sind sie enthalten.
- Das Calamari-Frakturmodell arbeitet hier besser auf **Zeilenbildern**. Die Zeilensegmentierung macht das Notebook via Tesseract.

## 2) Calamari-Frakturmodell installieren (dein gewünschtes Modell)

Das gewünschte Modell kommt aus `calamari_models/fraktur_19th_century`:

```bash
git clone https://github.com/Calamari-OCR/calamari_models.git models/calamari_models
```

Die Notebooks sind bereits auf dieses Ensemble-Modell verdrahtet:

- `models/calamari_models/fraktur_19th_century/0.ckpt.json`
- `models/calamari_models/fraktur_19th_century/1.ckpt.json`
- `models/calamari_models/fraktur_19th_century/2.ckpt.json`
- `models/calamari_models/fraktur_19th_century/3.ckpt.json`
- `models/calamari_models/fraktur_19th_century/4.ckpt.json`

## 3) Notebooks starten

Vom Repo-Root:

```bash
.venv311/bin/jupyter lab
# oder
.venv311/bin/jupyter notebook
```

Wähle im Notebook den Kernel **"OCR (.venv311)"** und führe dann in dieser Reihenfolge aus:

1. `notebooks/01_setup_local_ocr.ipynb`
2. `notebooks/02_ocr_pipeline_tesseract_calamari.ipynb`

## Outputs

Ergebnisse landen in:

- `outputs/tesseract_testbild.txt`
- `outputs/calamari_testbild.txt`
- Zeilenbilder in `outputs/lines/`
- sowie Calamari-Rohoutput in `outputs/calamari/`
