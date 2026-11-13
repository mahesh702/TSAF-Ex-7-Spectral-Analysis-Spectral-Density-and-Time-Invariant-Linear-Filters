# TSAF-Ex-7-Spectral-Analysis-Spectral-Density-and-Time-Invariant-Linear-Filters

## AIM:

To simulate a time series, calculate its spectral density, perform spectral analysis using
the periodogram, and study the effect of a time-invariant linear filter.

## PROGRAM:

```
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

# 1. Generate time vector
n = 600
t = np.arange(n)

# 2. Generate time series: Low frequency (0.01) + High frequency noise (0.35)
x = np.sin(2 * np.pi * 0.01 * t) + 0.8 * np.sin(2 * np.pi * 0.35 * t) + 0.2 * np.random.randn(n)

# 3. Calculate Periodogram & Dominant Frequency
frequency, power = signal.periodogram(x)
dominant_freq = frequency[np.argmax(power)]
print("Dominant Frequency:", dominant_freq)

# 4. Apply a 15-point Moving Average Filter
window = 15
filtered = np.convolve(x, np.ones(window) / window, mode="same")

# 5. Calculate Spectral Density before and after
f1, p1 = signal.periodogram(x)
f2, p2 = signal.periodogram(filtered)

# 6. Visualizations
plt.figure(figsize=(12, 5))
plt.subplot(1, 2, 1)
plt.plot(t, x, label="Original", alpha=0.7)
plt.plot(t, filtered, label="15-pt Filtered", linewidth=2)
plt.title("Time Domain Analysis")
plt.legend()
plt.subplot(1, 2, 2)
plt.plot(f1, p1, label="Original Spectrum", alpha=0.7)
plt.plot(f2, p2, label="Filtered Spectrum", linewidth=2)
plt.title("Frequency Domain (Spectral Density)")
plt.legend()
plt.tight_layout()
plt.show()

```

## OUTPUT:

<img width="742" height="392" alt="image" src="https://github.com/user-attachments/assets/065f2601-6449-43c3-bff4-7efa10668619" />
