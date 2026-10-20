# NewsLens — Fake News Detection

An explainable, browser-based news analysis project by Govind Mishra.

## Run

No dependencies or API key needed. Open `dist/index.html` directly, or run:

```bash
python -m http.server 8000 --directory dist
```

Then open http://localhost:8000.

## Features

- Responsive dark interface with animated neural particles, glowing orb, orbit rings and scan effect; reduced-motion support.
- Paste news or upload a text file; transparent English language-warning rules.
- Train a real Multinomial Naive Bayes classifier from your own labeled CSV.
- Unicode tokenization, duplicate removal, conflicting-label rejection, reproducible stratified train/test split, Laplace smoothing.
- Held-out accuracy, fake-class precision and recall (not invented benchmarks).
- Local analysis history, reopen, clear and text report downloads.
- No backend, external inference, tracking or uploaded article storage. Google Fonts is the only external design resource; system fonts work offline.

## Training

Use UTF-8 CSV with `text,label` headers. Labels are `real` or `fake`. Minimum 10 distinct articles per class; maximum 5,000 rows and 2 MB. Quote fields containing commas or line breaks, and escape embedded quotes with two quotes.

Use independently verified, licensed articles. Similar articles from the same event can leak across random splits; for serious evaluation, prepare independent time/source-separated datasets. The 20% test portion is held out; the deployed classifier remains the model trained on the 80% training portion. There is no pretrained model bundled and no claim of production accuracy.

Default mode uses rules, not ML. Training activates the classifier. Model and up to 30 analyses persist in browser localStorage; use Model lab > Remove trained model and History > Clear history to remove them. Avoid sensitive material on shared devices.

## Structure

- `dist/index.html`: application interface
- `dist/style.css`: responsive design and effects
- `dist/engine.js`: CSV parsing, classification and evaluation
- `dist/app.js`: application state and browser interactions
- `tests/engine.test.cjs`: core behavior checks

## Test

```bash
node tests/engine.test.cjs
```

## Limitations

This is an educational fake-news classification project, not a fact-checking service. Styling cannot establish truth; neither can a model prediction. No live web verification or source retrieval is performed. English-only rule patterns do not assess Hindi text; custom models can tokenize Unicode scripts, but need representative labeled training data. No calibrated probability is presented. Dataset bias, topic shortcuts, and distribution shift can produce wrong classifications.
