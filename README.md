# Ion-Trap-SuperResolution-Spectroscopy
Super-resolution spectral estimation and Bayesian system-error correction for 
Penning-trap mass spectrometry of highly charged ions (HCI). 
Developed at Institute of Modern Physics, CAS.

## Physics Problem
In a Penning trap, the magnetron and modified cyclotron motions of a single 
highly charged ion (e.g., Xe44+) are coupled and buried in strong noise 
(SNR < -10 dB). Classical FFT fails to resolve frequency spacing < 1 kHz.

## Algorithmic Solutions
- **MUSIC (Multiple Signal Classification)**: Eigen-decomposition of the 
  autocorrelation matrix to separate signal and noise subspaces, enabling 
  super-resolution frequency estimation (resolved 0.3 kHz spacing).
- **Bayesian Hierarchical Model**: Priors for image-charge shift and magnetic 
  field drift; posterior correction via MCMC (No-U-Turn Sampler) to push 
  relative mass uncertainty from 1e-6 to 1e-7.

## Tech Stack
Python 3.10 | NumPy | SciPy | Matplotlib | emcee (MCMC) | Jupyter

## Key Files
- `music_spectrum.py` — Core MUSIC algorithm with model-order selection (AIC/BIC)
- `bayesian_correction.py` — Hierarchical Bayesian model for systematic error
- `ion_simulation.py` — Ion trajectory simulator under non-ideal E/B fields
- `data/` — Simulated and experimental time-series data (anonymized)
- `notebooks/` — Step-by-step tutorials from raw signal to final mass

## Run
pip install -r requirements.txt
python demo.py --signal data/xe44_noisy.txt --snr -10

## Transferable Insight
The signal-subspace + Bayesian-regularization framework is mathematically 
isomorphic to super-resolution image reconstruction (e.g., SIM, FPM) and 
compressed-sensing MRI. See `docs/transfer_notes.md` for mapping.
