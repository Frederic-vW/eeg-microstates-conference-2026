# eeg-microstates-conference-2026
mstsa notebooks for EEG microstates conference 2026, Pescara, Italy

**Author:** Frederic von Wegner, UNSW Sydney, Aug-Sep 2026.  
[UNSW profile](https://research.unsw.edu.au/people/dr-frederic-von-wegner), [ResearchGate](https://www.researchgate.net/profile/Frederic-Wegner/research), [Google Scholar](https://scholar.google.com.au/citations?hl=en&pli=1&user=3dMJpvcAAAAJ) 

## A crash course in advanced EEG microstate analysis

This workshop gives a survey over recently developed time series analysis tools for the analysis of EEG microstate sequences.

The workshop uses the new Python package mstsa (= microstate time series analysis): [PyPi](https://pypi.org/project/mstsa/), [GitHub repo](https://github.com/Frederic-vW/mstsa).

Familiarity with the basics of EEG microstate analysis is assumed:
- Michel CM, Bréchet L (2026) EEG microstates: from methodological foundations to clinical translation. Trends in Neurosciences 49(5):S0166–2236(26)00074–3. https://doi.org/10.1016/j.tins.2026.01.004
- Michel CM, Koenig T (2018) EEG microstates as a tool for studying the temporal dynamics of whole-brain neuronal networks: a review. NeuroImage 180:577–593. https://doi.org/10.1016/j.neuroimage.2017.11.062

All analyses start with back-fitted and potentially smoothed microstate sequences. Clustering algorithms are not contained or explored, these can be found in other open source software packages:
- Thomas Koenig's Matblab package: [GitHub repo](https://github.com/ThomasKoenigBern/microstates)
- Victor Férat's Pycrostates: [GitHub repo](https://github.com/vferat/pycrostates/), [homepage](https://pycrostates.readthedocs.io/en/latest/)

## Content
The content is delivered as 10 interactive Python notebooks (.ipynb). Most results are pre-computed and cached in ./data/cache to bypass longer computation times if needed.  
_Suggestion_: If you wish to run the computations on your computer, make a backup copy of the cache folder before emptying it. Notebooks will always try to re-load precomputed data from ./data/cache. You can always recover the cached data from the [GitHub repo](https://github.com/Frederic-vW/eeg-microstates-conference-2026/tree/main). 

### Classical microstate parameters - effects of smoothing
- `00_microstate_parameters.ipynb`
- Compute the classical microstate parameters duration, occurrence and coverage and study the influence of sequence smoothing during preprocessing

### First-order syntax - null hypothesis and side effects of randomization
- `01_first_order_syntax_limitations.ipynb`
- Run and interpret the common first-order syntax test
- Explore its limitations and critically assess alternatives

### Assessing non-Markovian dynamics
- `02_assessing_non-markovianity.ipynb`
- Statistically test low-order Markov properties
- Explore non-Markovian microstate sequence features

### Time series complexity - validation on a statistical physics model
- `03_potts_complexity.ipynb`
- Study type I and type II complexity metrics, namely entropy rate (ER) and excess entropy (EE)

### Higher-order interactions - selecting a valid history length
- `04_optimum-history-length.ipynb`
- Study the relationship between sequence length, i.e. the number of samples in your microstate sequences, and how this affects the reasonable history length of higher-order (multivariate) microstate metrics

### The Hurst phenomenon (persistence) - contributing factors
- `05_Hurst_phenomenon.ipynb`
- Compute Hurst exponents to study persistence ($0.5<H<1$)
- Assess 'non-fractal' mechanisms contributing to persistence

### Towards K-invariance?
- `06_K-invariance.ipynb`
- A perspective: can we find metrics that give similar results for different cluster numbers $K$ ?

### A clinical example: microstate biomarkers of Alzheimer dementia (AD) Pt. 1 (classical parameters)
- `07_dementia_duration_occurrence_coverage.ipynb`
- The first of three notebooks to exemplify microstate biomarker search on a dementia dataset
- Step 1: Compute the classical microstate parameters (duration, occurrence, coverage) 

### A clinical example: microstate biomarkers of Alzheimer dementia (AD) Pt. 2 (complexity)
- `08_dementia_complexity.ipynb`
- Step 2: Compare microstate sequence complexity between control and AD subjects

### A clinical example: microstate biomarkers of Alzheimer dementia (AD) Pt. 3 (higher-order syntax: entropy rate and sample entropy)
- `09_dementia_higher_order_syntax.ipynb`
- Step 3: Compare higher-order syntax properties (entropy rate, sample entropy) between control and AD subjects

## Datasets
This workshop has preprocessed microstate sequences taken from the following sources.
1. LEMON / MPILMBB database
    - eyes-closed resting state microstate sequences (`_EC_ms_`); 1206 files, average length 1 minute, at 250 Hz (mean around 16,000 samples/sequence)
        - Different clusterings (`K4`, `K5`, `K6`)
        - Four smoothing methods: parametric smoothing with window half-size 1, 3, 9 samples (`b1`, `b3`, `b9`) and GFP peak interpolation (`ip`)
    - Preprocessing and microstate computation as in:  
    von Wegner F, Hermann G, Tödt I et al (2025) Higher-order EEG microstate syntax and surrogate testing. Comput Biol Med. https://doi.org/10.1101/2025.01.07.631820
    - A. Babayan, M. Erbey, D. Kumral, et al., A mind-brain-body dataset of MRI, EEG, cognition, emotion, and peripheral physiology in young and old adults, Sci. Data 6 (2019) 180308, http://dx.doi.org/10.1038/sdata.2018.308.
    - Original dataset: https://openneuro.org/datasets/ds000221/versions/1.0.0
2. Dementia dataset
    - Resting-state eyes-closed EEG from 3 groups: healthy controls (CN, n=29), Alzheimer Disease (AD, n=36), fronto-temporal dementia (FTD, n=23); the notebook included here only looks at CN vs. AD
    - Preprocessing and microstate computation as in:  
    von Wegner, F, Hermann, G, Tödt, I et al. (2026) A Quantitative Comparison of Two Methods for Higher-Order EEG Microstate Syntax Analysis. Brain Topography (2026) 39:45 https://doi.org/10.1007/s10548-026-01196-5
    - Dataset published by: Miltiadous A, Tzimourta KD, Afrantou T et al (2023) A dataset of scalp EEG recordings of alzheimer’s disease, frontotemporal dementia and healthy subjects from routine EEG. Data 8(6):95. https://doi.org/10.3390/data8060095
    - Original dataset: https://openneuro.org/datasets/ds004504/versions/1.0.9
3. Potts system
    - A discrete-valued model from statistical physics that undergoes a phase transition when the free parameter 'temperature'. Used to validate microstate complexity metrics.
    - Processing as in: von Wegner, F, Wiemers, M, Hermann, G et al. (2023) Complexity measures for EEG microstate sequences: Concepts and algorithms, Brain Topogr. 37 (2) 296–311, http://dx.doi.org/10.1007/s10548-023-01006-2.
    - More example data is stored in this [GitHub repo](https://github.com/Frederic-vW/potts-complexity)

## Requirements
- Python 3.8+ (Linux, Windows, or Mac)
- The [`mstsa`](https://pypi.org/project/mstsa/) package, which pulls in its
  own dependencies (`numpy`, `scipy`, `matplotlib`, `numba`, `cffi`)
  automatically:
  ```bash
  pip install mstsa
  ```
  A virtual environment is recommended:
  ```bash
  python3 -m venv mstsa-env
  source mstsa-env/bin/activate      # Windows: mstsa-env\Scripts\activate
  pip install mstsa
  ```
- A way to run `.ipynb` notebooks — not included with Python or `mstsa`, so
  pick one:
  - **JupyterLab** (no other setup needed):
    ```bash
    pip install jupyterlab
    jupyter lab
    ```
  - **VS Code**: install the *Jupyter* extension (usually prompted
    automatically the first time you open a `.ipynb` file), then open any
    notebook and select the environment you installed `mstsa` into as the
    kernel.
  - **[JupyterLab Desktop](https://github.com/jupyterlab/jupyterlab-desktop)**:
    a standalone app if you'd rather avoid the command line entirely.
