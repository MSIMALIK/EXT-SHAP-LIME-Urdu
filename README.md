# EXT-SHAP-LIME-Urdu

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-brightgreen.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Explainable AI](https://img.shields.io/badge/Explainable_AI-SHAP_%26_LIME-blue.svg)](https://github.com/MSIMALIK/EXT-SHAP-LIME-Urdu)

An Explainable Artificial Intelligence (XAI) project for generating and visualizing **SHAP** and **LIME** explanations for **Urdu and other right-to-left (RTL) languages**.

The repository provides two complementary components:

* **SHAP_RTL** — RTL-aware SHAP plots, feature attribution analysis, and LLM-assisted explanations for Urdu, Arabic, Persian, and Hebrew.
* **LIME_RTL** — Local text explanations, notebook visualizations, and LLM-assisted linguistic analysis, with a primary focus on Urdu.

---

## 🏗️ Methods & Components

### SHAP_RTL

The SHAP component includes:

* **RTL visualization functions** — Bar, waterfall, beeswarm, force, summary, decision, dependence, scatter, and heatmap plots.
* **Language-specific rendering** — Font selection, Arabic-script shaping, and bidirectional text handling.
* **RTLSHAPExplainer** — An interactive workflow for plots, feature analysis, and optional RTL/English explanations.
* **SHAPRTL** — A convenience wrapper with a default TF-IDF and Logistic Regression classifier, plus support for custom compatible classifiers and vectorizers.
* **Language experiments** — Notebooks for Urdu, Arabic, Persian, and Hebrew.
* **OCR evaluation** — Scripts and saved outputs for studying rendering quality using Character Error Rate (CER).

### LIME_RTL

The LIME component includes:

* **RTLLimeExplainer** — Local explanations for a trained classifier and text vectorizer.
* **Word-level feature weights** — Positive and negative contributions to the predicted class.
* **Notebook visualization** — Interactive HTML output and Matplotlib plotting code.
* **LLM-assisted analysis** — Linguistic descriptions of selected features and optional English translations.
* **Example analysis** — A notebook and screenshots demonstrating the explanation workflow.

The current LIME adapter expects a model with `classes_` and `predict_proba()`, and a vectorizer with `transform()`.

---

## 📁 Repository Structure

The following tree shows the main files and folders. Font contents, screenshots, packaging metadata, OCR CSV results, and other supporting files are condensed.

```text
EXT-SHAP-LIME-Urdu/
│
├── README.md
├── LICENSE
│
├── SHAP_RTL/
│   ├── README.md
│   ├── setup.py
│   ├── pyproject.toml
│   ├── __init__.py
│   ├── explainer.py
│   ├── rtl_utils.py
│   ├── rtl_utils_hebrew.py
│   ├── SHAP_RTL_package.egg-info/
│   ├── shap_rtl/
│   │   ├── __init__.py
│   │   ├── explainer.py
│   │   ├── wrapper.py
│   │   ├── rtl_utils.py
│   │   ├── rtl_utils_hebrew.py
│   │   └── plots/
│   │       ├── __init__.py
│   │       ├── _bar_rtl.py
│   │       ├── _beeswarm_rtl.py
│   │       ├── _decision_rtl.py
│   │       ├── _dependence_rtl.py
│   │       ├── _force_rtl.py
│   │       ├── _heatmap_rtl.py
│   │       ├── _scatter_rtl.py
│   │       ├── _summary_rtl.py
│   │       └── _waterfall_rtl.py
│   ├── Datasets/
│   │   ├── L-HSAB.txt
│   │   ├── NUHONS.csv
│   │   ├── PHate.csv
│   │   └── hebrew_cleaned.csv
│   ├── Testing/
│   │   ├── Final_testing.ipynb
│   │   ├── Test_Arabic.ipynb
│   │   ├── Test_Persian.ipynb
│   │   ├── Test_Urdu.ipynb
│   │   └── Test_hebrew.ipynb
│   ├── fonts/
│   └── ocr_experiment/
│       ├── run_ocr_test.py
│       ├── diagnose.py
│       ├── extract_words_arabic.py
│       ├── data/
│       ├── diagnose/
│       ├── fonts/
│       └── tessdata/
│
└── LIME_RTL/
    ├── README.md
    ├── LICENSE
    ├── requirements.txt
    ├── setup.py
    ├── assets/
    ├── config.json
    ├── tokenizer.json
    ├── tokenizer_config.json
    └── src/
        ├── __init__.py
        ├── urdu_lime.egg-info/
        └── urdu_lime/
            ├── __init__.py
            ├── explainer.py
            ├── analysis.ipynb
            ├── test.py
            ├── logic for all RTL .py
            └── Jameel Noori Nastaleeq Regular.ttf
```

* `SHAP_RTL/shap_rtl/` — Installable SHAP package.
* `SHAP_RTL/shap_rtl/plots/` — RTL-aware SHAP plotting functions.
* `SHAP_RTL/Datasets/` — Dataset files used in language experiments.
* `SHAP_RTL/Testing/` — Language-specific experiment notebooks.
* `SHAP_RTL/fonts/` — Fonts for RTL text rendering.
* `SHAP_RTL/ocr_experiment/` — Rendering diagnostics, OCR resources, and evaluation outputs.
* `LIME_RTL/src/urdu_lime/` — Installable LIME package and example analysis.
* `LIME_RTL/assets/` — Screenshots of explanation outputs.

---

## 🚀 Installation & Setup

Use **Python 3.10 or newer** for the current source, which includes modern type annotations.

Clone the repository:

```bash
git clone https://github.com/MSIMALIK/EXT-SHAP-LIME-Urdu.git
cd EXT-SHAP-LIME-Urdu
```

Install the SHAP component and its supporting visualization dependencies:

```bash
python -m pip install -e ./SHAP_RTL
python -m pip install scikit-learn ipython jupyter pillow uharfbuzz freetype-py
```

Install the LIME component:

```bash
cd LIME_RTL
python -m pip install -r requirements.txt
python -m pip install matplotlib pillow jupyter
cd ..
```

The LIME requirements file includes an editable installation of its package.

### API Configuration

The LLM features use credentials loaded from environment variables or a local `.env` file:

* **SHAP** — `GROQ_API_KEY` with `api_type="groq"`, or `GITHUB_TOKEN` with `api_type="github"`.
* **LIME** — `GITHUB_TOKEN` for the current GitHub Models integration, configured with `gpt-4o-mini`.

Keep credentials outside version control. Direct SHAP plotting does not require an LLM API key.

### Usage

Import SHAP plotting functions:

```python
from shap_rtl.plots import bar, waterfall, beeswarm
from shap_rtl.rtl_utils import set_current_language

set_current_language("Urdu")

# shap_values must be an existing shap.Explanation.
# Use a single instance for waterfall, and compatible SHAP data for each plot.
bar(shap_values)
waterfall(shap_values[0])
```

Import the LIME adapter:

```python
from urdu_lime.explainer import RTLLimeExplainer

# model and vectorizer must already be fitted.
explainer = RTLLimeExplainer(
    model=model,
    vectorizer=vectorizer,
    language="Urdu",
)

text = "یہ ایک مثال ہے"
explanation, predicted_index = explainer.explain_instance(
    text,
    num_features=10,
)
```

Open the notebooks in `SHAP_RTL/Testing/` and `LIME_RTL/src/urdu_lime/analysis.ipynb` for the experiment workflows. Adjust dataset and font paths to your local environment.

**Implementation note:** The current LIME `plot_matplotlib()` method calls `_fix_for_plot()`, which is not defined in that class. This helper must be implemented before running that plotting method or the full LIME analysis workflow.

For OCR experiments, install Tesseract separately and add the experiment dependencies:

```bash
python -m pip install pytesseract jiwer
cd SHAP_RTL/ocr_experiment
python run_ocr_test.py --setup
python run_ocr_test.py --demo
```

---

## ⚠️ Content Notice

Some datasets, notebooks, and example outputs contain offensive, abusive, hateful, or threatening expressions used in language-classification research.

These materials are included for research and academic purposes.

---

## 📄 License

This repository is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

## 👤 Authors & Contributors

**Muhammad Shahid Iqbal Malik**  
GitHub: [@MSIMALIK](https://github.com/MSIMALIK)

**Rameesha Zia** — Listed alongside Dr. Shahid Iqbal Malik in the LIME package metadata.

