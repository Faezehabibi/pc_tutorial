# Difference of Gaussian Filter (DoG)

The difference of Gaussian filter is made of 2 components: A positive Gaussian filter and a negative Gaussian filter.
The positive Gaussian filter enhances the singnal that matches to its mean value, while
the negative Gaussian filter suppress the singnal that matches to its mean value.
In both filters, the effect decays exponentialy when the signal deviates from the mean of the Gaussian.

The Dog filter is the summation of these two filters in the spatial domain.

<h2> 💡 Intuition </h2>
* Horizontal Cells: The negative Gaussian filter, on the other hand, supress particular frequencies.
* Bipolar Cells: On or Off
* Center-Surround: Opposite effect of surround and center (On-Center Off-Surround and Off-Center On-Surround).
- On-Center Off-Surround (direct excitation in center and direct inhibition in surround): On Bipolar Cells in the center == Gaussian filter (lower variance) and Off Bipolar Cells in the surround == Negative Gaussian filter (higher variance)
Since the surround is always broader than center, the surround variance in modeling is higher than center variance.
* The signal positive amplifies (excited) at the center but it is negatively suppresses (inhibits) in a donate-shape ring surrounding the central domain approaching to zero when going far away.

When subtracted, the frequencies
in the center are still enhanced positively while 

The Difference of Gaussian filters (DoG) are summation of 2 gaussian filters, one positive and one negative.


