<h1>Retina and LGN</h1>

<!-- 
![PC_brain](https://github.com/user-attachments/assets/33fdb152-4c3a-49fc-8eb1-b5d0bc88a263)
![PC_brain](https://github.com/user-attachments/assets/36260004-c917-4b27-bff8-55e06d53879b)
-->

<img src="images/PC_brain.jpeg" width="400" align="right"/>


Retina preprocess the input information before sending to the brain's visual processing system. 
When the light beam hits an object and reflects, if it finds its way to our Retina, the retina acts 
like a receive which absorb the information and process it. This early stage processing happens prior 
to the moment that our brain perception starts. In order to reduce the processing computation in the 
visual cortex the Retina reduces the redundancy and only sends the informative signals (the information worth mentioning).

<!-- ============================= -->
<h2> 💡 Intuition </h2>

**What goes into the Retina?**
Retina is the door to the brain. The Retina's input is the light with different intensities.
The process starts when the light hits the Retina ($t=t_0$). The goal is to pre-processing 
the visual sensory information and prepare for furthure process by the higher brain areas. 


**What happens in the Retina?**
Retina's converts the light received to electrical signal.
In the Retina the input stimuli is processed further through multiple 
stages before sending to the higher levels. Retina uses center-surround 
organization for receptive fields to acts like Difference
of Gaussian ([DoG](https://github.com/Faezehabibi/pc_tutorial/blob/62cfad85eed9072791307301d11e3cd0f675507f/DoG.md)) 
filter for the input signal. In the spatial domain (static input pattern), it 
enhance the edges, spatial contrasts, or discontinuities in general, and 
reduces uniform data. It reduces redundancy to avoid unnecessary processing
of the information by the higher areas of the brain.

<!-- 
components
*Horizontal Cells: The negative Gaussian filter, on the other hand, supress particular frequencies.
*Bipolar Cells: On or Off
* Center-Surround: Opposite effect of surround and center (On-Center Off-Surround and Off-Center On-Surround).
- On-Center Off-Surround (direct excitation in center and direct inhibition in surround): On Bipolar Cells in the center == Gaussian filter (lower variance) and Off Bipolar Cells in the surround == Negative Gaussian filter (higher variance)
Since the surround is always broader than center, the surround variance in modeling is higher than center variance.
* The signal positive amplifies (excited) at the center but it is negatively suppresses (inhibits) in a donate-shape ring surrounding the central domain approaching to zero when going far away.
-->


**What goes out from the Retina?**
The Retina's output is the electrical signal encoding the information in the intput light intensities.
The last processing stage in Retina is called Retina Ganglion Cell (RGC) 
which passes the Retina's final processed information upward
to its next processor Lateral geniculate nucleus (LGN).


<!-- ============================= -->
<h2> 📝 Math </h2>




<!-- ============================= -->
<h2> 👩🏼‍💻 NGC-Learn Implementation </h2>


  

