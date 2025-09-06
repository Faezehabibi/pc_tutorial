# Difference of Gaussian Filter

Gaussian filter enhances specific frequencies while ...

* Horizontal Cells: The negative Gaussian filter, on the other hand, supress particular frequencies.
* Bipolar Cells: On or Off
* Center-Surround:
- On-Center Off-Surround: On Bipolar Cells in the center == Gaussian filter (lower variance) and Off Bipolar Cells in the surround == Negative Gaussian filter (higher variance)
Since the surround is always broader than center, the surround variance in modeling is higher than center variance.

When subtracted, the frequencies
in the center are still enhanced positively while 

The Difference of Gaussian filters (DoG) are summation of 2 gaussian filters, one positive and one negative.


