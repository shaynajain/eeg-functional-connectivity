# EEG Functional Connectivity States (Alpha Band)

This project explores how alpha-band (8–13 Hz) EEG functional connectivity differs between resting state and motor execution using coherence-based network analysis.

The goal is to build an end-to-end computational neuroscience pipeline, from raw EEG signals to interpretable graph-theoretic metrics, using real human neurophysiological data.

---

## Dataset

**EEG Motor Movement/Imagery Dataset (EEGMMIDB)**  
Hosted on PhysioNet:  
https://physionet.org/content/eegmmidb/1.0.0/

- Subject analyzed: **Subject 1**
- EEG recorded with **64 scalp electrodes**
- Sampling rate: **160 Hz**
- Conditions used:
  - **Run 1**: Baseline (eyes open, resting state)
  - **Run 3**: Motor execution (left vs right fist movement)

The dataset was accessed programmatically using the `mne.datasets.eegbci` interface.

---

## Scientific Question

How does alpha-band functional connectivity organization differ between rest and motor execution when controlling for network density?

---

## Methods

### Preprocessing
- EEG data were loaded from EDF files using MNE-Python.
- Channels were renamed and aligned to the standard **10–20 electrode montage**.
- Signals were band-pass filtered to the **alpha frequency range (8–13 Hz)**.
- Data were segmented into **2-second overlapping epochs** (50% overlap).

### Functional Connectivity
- Pairwise **coherence** was computed between all EEG channels for each epoch.
- Coherence values were averaged across epochs to form a connectivity matrix per condition.
- Connectivity matrices were symmetrized to reflect undirected functional coupling.

### Network Construction
- Each EEG channel was treated as a **node**.
- Edge weights corresponded to alpha-band coherence values.
- To control for network density, the **top 200 strongest connections** were retained for both conditions.

### Graph Analysis
- Networks were analyzed using graph-theoretic metrics:
  - **Degree** (node connectivity)
  - **Clustering coefficient** (local segregation)
- Networks were visualized using true **electrode scalp coordinates** derived from the montage.

---

## Results

When controlling for the number of edges, alpha-band functional networks exhibited:

- **Higher mean clustering during rest** compared to motor execution
- **Matched mean degree across conditions** by design

This suggests that resting-state alpha activity is organized into more locally clustered functional modules, whereas motor execution is associated with reduced local segregation and more distributed connectivity.

---

## Visualizations

The repository includes:
- Alpha-band coherence heatmaps for rest and task
- Scalp-layout functional connectivity networks
- Bar plots comparing graph metrics across conditions

All figures are saved in the `figures/` directory.

---

## Limitations

- Analysis was performed at the **sensor level** and may be influenced by volume conduction.
- Results are based on a **single subject** and are intended as an exploratory pilot study.
- Connectivity was measured using coherence, which captures synchronization but not directionality.

---

## Tools & Libraries

- Python
- MNE-Python
- NumPy
- Matplotlib
- NetworkX

---

## Future Directions

- Extend analysis to additional subjects
- Compare alpha-band results with beta-band connectivity
- Examine lateralization effects over motor cortex (e.g., C3 vs C4)
- Explore alternative connectivity measures (e.g., phase-lag index)

---

## Acknowledgments

Dataset provided by PhysioNet. Analysis performed for educational and exploratory research purposes.
