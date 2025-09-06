# Difference of Gaussian Filter (DoG)

The difference of Gaussian filter is made of 2 components: A positive Gaussian filter and a negative Gaussian filter.
The positive Gaussian filter enhances the singnal that matches to its mean value, while
the negative Gaussian filter suppress the singnal that matches to its mean value.
In both filters, the effect decays exponentialy when the signal deviates from the mean of the Gaussian.

The Dog filter is the summation of these two filters in the spatial domain. The summation of 
two gaussian filters with different variance (spread from the center) brings a contrast enhancing 
effect to the filter. If the positive Gaussian filter have low variance, while the negative Gaussian 
speads more broader. The filter output (the summation value) is high when the signals is positive 
in the center and negatively spreaded out in the spatial suround and relatively negligible (or zero) otherwise.

<h2> 💡 Intuition </h2>


