# Difference of Gaussian Filter

Gaussian filter enhances specific frequencies while ...

* Horizontal Cells: The negative Gaussian filter, on the other hand, supress particular frequencies.
* Bipolar Cells: On or Off
* Center-Surround:
- On-Center Off-Surround: On Bipolar Cells == Gaussian filter and Off Bipolar Cells == Negative Gaussian filter 


The Difference of Gaussian filters (DoG) are summation of 2 gaussian filters, one positive and one negative.

The positive is usually low variance while the negative is high variance. When subtracted, the frequencies
in the center are still enhanced positively while 

