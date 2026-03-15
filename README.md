# Mitigating Occupational Gender Bias in English-to-Spanish Machine Translation

This repository contains the code and data for **"Mitigating Occupational Gender Bias in English-to-Spanish Machine Translation: A Multi-Stage Detection and Correction Pipeline."** Our work audits major commercial MT systems (Google Translate, DeepL, and SYSTRAN) and introduces a modular pipeline that detects gender-neutral-to-gendered translation errors and corrects them through a targeted, form-level discriminative approach.

## Data

We use [WinoMT]([url](https://github.com/gabrielStanovsky/mt_gender)), comprised of WinoBias and Winogender. We kept only the 3168 instances that comprised WinoBias and dropped the data from Winogender, due to differences in sentence version construction.

## The Problem

Machine Translation systems often rely on stereotypical heuristics. For example, when translating *"The physician hired a housekeeper and told **him** to work every day,"* many models ignore the masculine cue (**him**) and default to the Spanish feminine stereotype: ***la ama de llaves***.

## Pipeline Architecture

Instead of "black-box" end-to-end generation, our pipeline is split into two interpretable stages:

1. **Stage 1: Mismatch Detection** A supervised binary classifier (TF-IDF + Logistic Regression) that analyzes bilingual context and structured metadata to flag translations where the realized Spanish gender contradicts the English source.
2. **Stage 2: Gender-Aware Correction** A form-level predictor that determines the correct Spanish profession form, which is then safely reinserted into the original sentence using a conservative local agreement adjustment.

## Key Results

* **Audit:** Identified a significant "Stereotype Gap" across all commercial systems, particularly in anti-stereotypical contexts.
* **Detection:** Achieved a **0.76 Accuracy / 0.58 F1** using structured bilingual inputs.
* **Correction:** Our modular approach resolved **98.8%** of audited mismatches in our controlled test subset.
