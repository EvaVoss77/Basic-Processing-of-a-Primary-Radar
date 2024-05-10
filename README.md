In this work, the basic algorithms used in radar processing are explored to determine the position of an object and infer its movement. Processing is performed on ten reception windows of a pulsed radar, received at intervals of PRP time. The figure outlines how the work will be developed. The functionality of each block is as follows:

- **Adapted filter:** A linear filter whose impulse response is determined to maximize the Signal-to-Noise Ratio (SNR) at the filter output.
- **Moving Target Indicator (MTI) filter:** Exploits the correlation between signals from the same stationary object or low-speed object to mitigate them.
- **Stopped Target Indicator (STI) filter:** In contrast to MTI, this filter enhances signals from stationary objects.
- **Constant False Alarm Rate (CFAR) Threshold:** Estimates a decision threshold adaptively while maintaining a fixed false alarm rate.

![esq](https://github.com/EvaVoss77/Basic-Processing-of-a-Primary-Radar/assets/126124561/7519d65b-3226-4841-bbda-d26563eafd98)

# **Adaptated Filter**

To clean the signal from this noise, an adapted filter is employed to maximize the SNR. To achieve this, the impulse response should have the form:

$ h(t) = s^*(t_0 - t) $

Where $t_0$ is the delay of the signal. Knowing this, the adapted filter was constructed using the signal data considering $t_0 = 0$. Once this filter was applied, it was possible to distinguish some signals. A comparison is made between the signal before and after the filter for the first two reception windows. In both cases, peaks are observed that were not distinguishable before this stage. Within window 1, the peaks located at distances of 20 and 25 km stand out, while in window 2, no peak is observed at 20 km, although one is visualized at 25 km.


# **Moving Target Indicator (MTI) Canceller Filter**

The Figure shows a scheme of an MTI filter, where its impulse response can be observed as follows:

$ H(z) = 1 + h_1z^{-1} + h_2z^{-2} $

The algorithm for performing such filtration involves summing consecutive windows multiplied by the coefficients $ h_1 $ and $ h_2$, so that the amplitude of signals that do not change their phase is reduced at the output.

For the case of a single canceller, two consecutive windows are subtracted, meaning that $h_1 = -1$ and $h_2 = 0$, while for the case of a double canceller, $h_1 = -2$ and $h_2 = 1$.

![mti](https://github.com/EvaVoss77/Basic-Processing-of-a-Primary-Radar/assets/126124561/92c7275b-f7b0-45e2-b7a1-cf73d4c30b8c)

# **Constant False Alarm Rate (CFAR) Threshold**

This threshold, CF, is adaptively constructed for each point of the squared magnitude of the signal, $y_i$, from its non-immediate surrounding $N$ points, $k$, as follows:

$CF_i = \alpha \sum_{j=0}^{N} k_j$

where α is a factor depending on the false alarm probability, Pfa, as follows:

$\alpha = N(P_{fa}^{-1/N} - 1)$

#**Binary Detector**

For detection, a binary detector is implemented, from which it is decided whether a peak corresponds to an object or not. It is considered that the detection of a peak corresponds to the presence of an object when in more than half of the windows, it exceeds the CFAR threshold.
