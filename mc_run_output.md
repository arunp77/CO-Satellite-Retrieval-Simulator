(myenv) (venv) arun@ubuntu:~/Documents/co2_measurements$ python run_monte_carlo_with_datasave.py 
HAPI version: 1.3.0.0
To get the most up-to-date version please check http://hitran.org/hapi
ATTENTION: Python versions of partition sums from TIPS-2021 are now available in HAPI code

           MIT license: Copyright 2021 HITRAN team, see more at http://hitran.org. 

           If you use HAPI in your research or software development,
           please cite it using the following reference:
           R.V. Kochanov, I.E. Gordon, L.S. Rothman, P. Wcislo, C. Hill, J.S. Wilzewski,
           HITRAN Application Programming Interface (HAPI): A comprehensive approach
           to working with spectroscopic data, J. Quant. Spectrosc. Radiat. Transfer 177, 15-30 (2016)
           DOI: 10.1016/j.jqsrt.2016.03.005

           ATTENTION: This is the core version of the HITRAN Application Programming Interface.
                      For more efficient implementation of the absorption coefficient routine, 
                      as well as for new profiles, parameters and other functional,
                      please consider using HAPI2 extension library.
                      HAPI2 package is available at http://github.com/hitranonline/hapi2


╔══════════════════════════════════════════════════════════╗
║   CO₂ Retrieval Simulator — Monte Carlo Experiment      ║
║   Author: Arun Kumar Pandey                             ║
╚══════════════════════════════════════════════════════════╝

  Output figures → /home/arun/Documents/co2_measurements/mc_figures/
  Spectral grid   : 2000 points  (6210–6270 cm⁻¹)
  Random seed     : 42

  Data cache directory: /home/arun/Documents/co2_measurements/mc_data/
  (Simulations are skipped automatically if cache files exist)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/noise_ensemble.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=300)
  True XCO₂=430.0 ppm  SNR=250.0  SZA=30.0°  A=0.25
============================================================
  Sample 100/300  (0.1s elapsed)
  Sample 200/300  (0.3s elapsed)
  Sample 300/300  (0.4s elapsed)
  Done. 300/300 converged in 0.4s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 300                           │
  │  Bias      : -0.019 ppm                        │
  │  Precision : 0.481 ppm                        │
  │  RMSE      : 0.481 ppm                        │
  │  Mean σ    : 0.468 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  300 samples  ->  /home/arun/Documents/co2_measurements/mc_data/noise_ensemble.npz  (6.0 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/xco2_sweep.npz'

============================================================
  MODE 2 — XCO₂ Sweep  (N=80)
  Range: 380.0–480.0 ppm  SNR=300.0
============================================================
  Sample 25/80
  Sample 50/80
  Sample 75/80
  Done. 80/80 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : XCO₂ Sweep                    │
  │  N samples : 80                            │
  │  Bias      : -0.007 ppm                        │
  │  Precision : 0.349 ppm                        │
  │  RMSE      : 0.349 ppm                        │
  │  Mean σ    : 0.390 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  80 samples  ->  /home/arun/Documents/co2_measurements/mc_data/xco2_sweep.npz  (3.5 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/random_scenes.npz'

============================================================
  MODE 3 — Random Scene Ensemble  (N=400)
  XCO₂ ~ N(420.0,15.0) ppm
  Albedo ~ U(0.05,0.40)   SZA ~ U(10°,70°)   SNR ~ U(150,400)
============================================================
  Sample 100/400  (0.4s elapsed)
  Sample 200/400  (0.8s elapsed)
  Sample 300/400  (1.2s elapsed)
  Sample 400/400  (1.6s elapsed)
  Done. 400/400 converged in 1.6s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Random Scenes                 │
  │  N samples : 400                           │
  │  Bias      : +0.045 ppm                        │
  │  Precision : 0.413 ppm                        │
  │  RMSE      : 0.415 ppm                        │
  │  Mean σ    : 0.432 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  400 samples  ->  /home/arun/Documents/co2_measurements/mc_data/random_scenes.npz  (19.6 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/snr_sens_0075.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=150)
  True XCO₂=435.0 ppm  SNR=75  SZA=30.0°  A=0.25
============================================================
  Sample 100/150  (0.1s elapsed)
  Done. 150/150 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 150                           │
  │  Bias      : -0.098 ppm                        │
  │  Precision : 1.542 ppm                        │
  │  RMSE      : 1.545 ppm                        │
  │  Mean σ    : 1.570 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  150 samples  ->  /home/arun/Documents/co2_measurements/mc_data/snr_sens_0075.npz  (4.0 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/snr_sens_0100.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=150)
  True XCO₂=435.0 ppm  SNR=100  SZA=30.0°  A=0.25
============================================================
  Sample 100/150  (0.2s elapsed)
  Done. 150/150 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 150                           │
  │  Bias      : -0.069 ppm                        │
  │  Precision : 1.157 ppm                        │
  │  RMSE      : 1.160 ppm                        │
  │  Mean σ    : 1.178 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  150 samples  ->  /home/arun/Documents/co2_measurements/mc_data/snr_sens_0100.npz  (4.0 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/snr_sens_0150.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=150)
  True XCO₂=435.0 ppm  SNR=150  SZA=30.0°  A=0.25
============================================================
  Sample 100/150  (0.2s elapsed)
  Done. 150/150 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 150                           │
  │  Bias      : -0.044 ppm                        │
  │  Precision : 0.772 ppm                        │
  │  RMSE      : 0.773 ppm                        │
  │  Mean σ    : 0.785 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  150 samples  ->  /home/arun/Documents/co2_measurements/mc_data/snr_sens_0150.npz  (3.9 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/snr_sens_0200.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=150)
  True XCO₂=435.0 ppm  SNR=200  SZA=30.0°  A=0.25
============================================================
  Sample 100/150  (0.1s elapsed)
  Done. 150/150 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 150                           │
  │  Bias      : -0.032 ppm                        │
  │  Precision : 0.579 ppm                        │
  │  RMSE      : 0.580 ppm                        │
  │  Mean σ    : 0.589 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  150 samples  ->  /home/arun/Documents/co2_measurements/mc_data/snr_sens_0200.npz  (3.9 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/snr_sens_0300.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=150)
  True XCO₂=435.0 ppm  SNR=300  SZA=30.0°  A=0.25
============================================================
  Sample 100/150  (0.1s elapsed)
  Done. 150/150 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 150                           │
  │  Bias      : -0.021 ppm                        │
  │  Precision : 0.386 ppm                        │
  │  RMSE      : 0.387 ppm                        │
  │  Mean σ    : 0.393 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  150 samples  ->  /home/arun/Documents/co2_measurements/mc_data/snr_sens_0300.npz  (3.9 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/snr_sens_0400.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=150)
  True XCO₂=435.0 ppm  SNR=400  SZA=30.0°  A=0.25
============================================================
  Sample 100/150  (0.1s elapsed)
  Done. 150/150 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 150                           │
  │  Bias      : -0.015 ppm                        │
  │  Precision : 0.290 ppm                        │
  │  RMSE      : 0.290 ppm                        │
  │  Mean σ    : 0.295 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  150 samples  ->  /home/arun/Documents/co2_measurements/mc_data/snr_sens_0400.npz  (3.9 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/sza_sens_010.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=100)
  True XCO₂=435.0 ppm  SNR=250.0  SZA=10°  A=0.25
============================================================
  Sample 100/100  (0.2s elapsed)
  Done. 100/100 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 100                           │
  │  Bias      : -0.048 ppm                        │
  │  Precision : 0.459 ppm                        │
  │  RMSE      : 0.461 ppm                        │
  │  Mean σ    : 0.485 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  100 samples  ->  /home/arun/Documents/co2_measurements/mc_data/sza_sens_010.npz  (3.2 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/sza_sens_020.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=100)
  True XCO₂=435.0 ppm  SNR=250.0  SZA=20°  A=0.25
============================================================
  Sample 100/100  (0.2s elapsed)
  Done. 100/100 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 100                           │
  │  Bias      : -0.048 ppm                        │
  │  Precision : 0.454 ppm                        │
  │  RMSE      : 0.457 ppm                        │
  │  Mean σ    : 0.480 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  100 samples  ->  /home/arun/Documents/co2_measurements/mc_data/sza_sens_020.npz  (3.2 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/sza_sens_030.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=100)
  True XCO₂=435.0 ppm  SNR=250.0  SZA=30°  A=0.25
============================================================
  Sample 100/100  (0.2s elapsed)
  Done. 100/100 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 100                           │
  │  Bias      : -0.047 ppm                        │
  │  Precision : 0.446 ppm                        │
  │  RMSE      : 0.449 ppm                        │
  │  Mean σ    : 0.471 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  100 samples  ->  /home/arun/Documents/co2_measurements/mc_data/sza_sens_030.npz  (3.2 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/sza_sens_045.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=100)
  True XCO₂=435.0 ppm  SNR=250.0  SZA=45°  A=0.25
============================================================
  Sample 100/100  (0.2s elapsed)
  Done. 100/100 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 100                           │
  │  Bias      : -0.045 ppm                        │
  │  Precision : 0.427 ppm                        │
  │  RMSE      : 0.429 ppm                        │
  │  Mean σ    : 0.450 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  100 samples  ->  /home/arun/Documents/co2_measurements/mc_data/sza_sens_045.npz  (3.2 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/sza_sens_055.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=100)
  True XCO₂=435.0 ppm  SNR=250.0  SZA=55°  A=0.25
============================================================
  Sample 100/100  (0.1s elapsed)
  Done. 100/100 converged in 0.1s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 100                           │
  │  Bias      : -0.043 ppm                        │
  │  Precision : 0.409 ppm                        │
  │  RMSE      : 0.411 ppm                        │
  │  Mean σ    : 0.429 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  100 samples  ->  /home/arun/Documents/co2_measurements/mc_data/sza_sens_055.npz  (3.2 KB)
  Cache miss ->  running simulation and saving to '/home/arun/Documents/co2_measurements/mc_data/sza_sens_065.npz'

============================================================
  MODE 1 — Noise Ensemble   (N=100)
  True XCO₂=435.0 ppm  SNR=250.0  SZA=65°  A=0.25
============================================================
  Sample 100/100  (0.2s elapsed)
  Done. 100/100 converged in 0.2s

  ┌──────────────────────────────────────────────┐
  │  Mode      : Noise Ensemble                │
  │  N samples : 100                           │
  │  Bias      : -0.040 ppm                        │
  │  Precision : 0.387 ppm                        │
  │  RMSE      : 0.389 ppm                        │
  │  Mean σ    : 0.401 ppm                        │
  └──────────────────────────────────────────────┘
  Saved  100 samples  ->  /home/arun/Documents/co2_measurements/mc_data/sza_sens_065.npz  (3.2 KB)

============================================================
  Generating figures …
============================================================
  → Saved: /home/arun/Documents/co2_measurements/mc_figures/mc_01_noise_ensemble.png
  → Saved: /home/arun/Documents/co2_measurements/mc_figures/mc_02_xco2_sweep.png
  → Saved: /home/arun/Documents/co2_measurements/mc_figures/mc_03_random_scene.png
  → Saved: /home/arun/Documents/co2_measurements/mc_figures/mc_04_snr_sensitivity.png
  → Saved: /home/arun/Documents/co2_measurements/mc_figures/mc_05_sza_sensitivity.png
  → Saved: /home/arun/Documents/co2_measurements/mc_figures/mc_06_bias_precision_summary.png

============================================================
  All done in 458.3s
  6 figures saved to: /home/arun/Documents/co2_measurements/mc_figures
  MC data cached in:  /home/arun/Documents/co2_measurements/mc_data
============================================================