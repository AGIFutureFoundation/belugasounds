# belugasounds — docs note (fork, no code changes)

**Status:** Added to this repo 2026-11-07 by the AGI Future Foundation research-lab loop. This note documents the fork. **No
code changes are included** — it is an upstream fork, and lab
content goes in as docs only, never as a rewrite of upstream code. Any docs
addition needs a human decision on where it lands (fork `docs/` vs upstream PR)
and must respect the upstream's Microsoft CLA / Code of Conduct.

## 1. What it is (verified 2026-11-07)

- **Repo:** `AGIFutureFoundation/belugasounds`, fork of
  **`microsoft/belugasounds`** (API-verified parent; `fork: true`).
- **Branch:** `master`. **Fork created / last updated:** 2026-07-14 (fork date;
  the upstream project is older). **Size:** 233 KB. **Licence:** MIT.
- **Description (verbatim from GitHub):** "Using machine learning to detect
  beluga whale calls in hydrophone recordings."
- **Upstream collaborators (per the README):** Microsoft AI for Earth, Microsoft
  AI for Good Research Lab, and NOAA Alaska Fisheries Science Center.
- **Publication:** Zhong M, Catellote M, Dodhia R, Lavista Ferres J, Keogh M,
  Brewer A. "Beluga whale acoustic signal classification using deep learning
  neural network models." *J. Acoust. Soc. Am.* 147, 1834 (2020).
  (Cited in the README; the paper itself was not re-verified in this pass.)

## 2. File tree (18 files, `master`)

| Path | Size (bytes) | What it is |
|---|---|---|
| `README.md` | 5,668 | Project intro, data, methodology, publications, blogs, contributing (read in full) |
| `step1_extract_spectrograms.py` | 7,738 | Load detection labels; extract audio for detection/non-detection regions; compute and save spectrograms (header read) |
| `step2_save_spectrogram_vector.py` | 4,439 | Save spectrogram vectors (name only — body not read) |
| `step3_model_cnn.py` | 7,413 | CNN built from scratch (AlexNet architecture) |
| `step3_model_densenet.py` | 6,816 | Transfer learning, fine-tuned DenseNet |
| `step3_model_resnet.py` | 6,794 | Transfer learning, fine-tuned ResNet50 |
| `step3_model_vgg16.py` | 6,814 | Transfer learning, fine-tuned VGG16 |
| `step4_model_ensemble.py` | 12,854 | Train the ensemble of the four models (header read; uses sklearn `roc_auc_score`, precision-recall) |
| `step5_extract_spectrograms_for_new_dataset.py` | 2,194 | Spectrogram extraction for a new dataset |
| `step6_full_analysis_scoring_for_new_dataset.py` | 3,314 | Run trained models on a new dataset; expects `./Whale_Acoustics/` + `Model/` paths (header read) |
| `requirements.txt` | 117 | numpy, pandas, glob2, matplotlib, joblib, keras, tensorflow, multiprocess, scipy, **scikit-learn==0.22**, opencv-python |
| `belugawhale.JPG` | 97,360 | Header photo: Chris Garner, Joint Base Elmendorf–Richardson |
| `LICENSE` | 1,162 | MIT (upstream Microsoft licence header in the scripts) |
| `CODE_OF_CONDUCT.md` | 453 | Microsoft Open Source Code of Conduct |
| `SECURITY.md` | 2,865 | Microsoft security policy |
| `.gitignore` | 1,203 | — |

## 3. What the upstream project claims (the repo's claims, not verified here)

- **Goal:** automatically detect and classify beluga whale acoustic signals in
  hydrophone recordings, replacing a NOAA detector that is sensitive but not
  specific (rarely misses whales, many false positives) so conservation teams
  stop reviewing false positives.
- **Population:** Cook Inlet belugas — smallest of five U.S. populations, down
  ~75% since 1979, listed endangered in 2008, **~279 whales as of January 2020**.
- **Data:** hydrophones in permanent moorings in Cook Inlet critical habitat;
  5–7 month deployments, ice-free (May–Sep) or winter (Oct–Apr) 2017–2018, seven
  locations, **>13,000 hours of audio**. Every preliminary-detector detection
  was manually validated by an expert reviewer as true/false; that labelled set
  trained and tested the models.
- **Method:** spectrograms + labels → binary classifier; four CNNs (AlexNet from
  scratch; VGG16, ResNet50, DenseNet transfer-learned + fine-tuned); final
  detector is an ensemble of the four.
- **Data not in the repo:** no audio, labels, or trained models are included.
  The scripts expect local `./Whale_Acoustics/` data. Do not claim the data is
  held by WAVE or the Foundation.

## 4. How it relates to WAVE

- The `bioacoustics-cloud` site description names "belugasounds + the Wild
  Animal Voice Engine as the open core", and the live site's Beluga Sounds card
  links this fork. That is the extent of the verified relationship: a link and a
  description line, not an integration. No WAVE code calls this repo, and no
  belugasounds code calls WAVE.
- Scientific role: this is the loop's one real, published, conservation-deployed
  ML detector — a species/call detector (level 1–2: detection/classification),
  not a decoder. It is the honest template for what WAVE's engine could become
  once an adapter is wired: a detector validated against expert labels, with a
  named population and a published paper.

## 5. What a docs contribution would be (proposal only — nothing staged as code)

This docs contribution to the fork takes the honest, low-risk form of
a single `docs/` note (this file) covering:

1. What the fork is and where upstream lives (`microsoft/belugasounds`), so a
   reader never mistakes the fork for the original.
2. A script map (the step1→step6 table above) — the upstream README describes
   the method but does not map each script to its step.
3. A run-status note: the stack is old (`scikit-learn==0.22`, unpinned
   keras/tensorflow) and **was not run in this pass** — whether the scripts still
   run on current versions is unverified. Do not claim they run.
4. A pointer to the WAVE engine repo as a separate, complementary project
   (detector here, pipeline there), without implying integration that does not exist.

**Do not stage:** code changes, dependency upgrades, re-training, new data, or
any claim about the models' accuracy beyond what the upstream README/paper
states. Performance figures, if ever quoted, must come from the JASA 2020 paper
itself, not from the README summary.

## 6. Honesty lines

- No discovery, cure, treatment, or diagnosis is claimed. This is a whale-call
  detector for conservation monitoring, not a translator.
- The beluga population figures are the upstream project's claims (January 2020
  estimate); they are six years old and must not be presented as current.
- The Foundation is a filed CA nonprofit (Entity No. B20260196664) with **no
  IRS 501(c)(3) determination letter** — never tax-exempt, never tax-deductible.
- No partnership with Microsoft or NOAA is claimed. The collaboration described
  is the upstream project's, between Microsoft and NOAA — not the Foundation's.
