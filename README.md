# SFND-Radar

This is the Final Project for the Radar Section from the Udacity Sensor Fusion Nanodegree.  

Program steps:  
1. design of a FMCW radar waveform according to the given parameters  
2. simulation of a radar scenario over time for a moving target with constant velocity  
3. calculation of the beat signal in order to generate the Range-Doppler-Map (RDM)  
4. implementation and tuning of the CA-CFAR algorithm in order to remove the noise over the radar measure  
5. plot of the RDM filtered map  

About the CA-CFAR implementation:

1. Initialization of the Training and Guard cells dimensions  
2. First choice of the offset, just to test  
3. Initialization of the noise_level vector (more precisely a matrix for easier handling of the data)  
   with size relative to the number of patch overlappings  
4. Calculation of the Training cells number later used in the averaging  
5. Initialization of the CFAR-filtered RDM matrix as all zeros (this will avoid padding later)  
6. By sliding the patch over the RDM (considering margins), the whole patch is converted  
   with db2pow. Now the subpatch regarding CUT and Guard cells is set to zero in order to give  
   no contribution to the average. By dividing now for the number of Training cells the average  
   is computed. Hence, the noise level is calculated by a backward conversion to Decibel (pow2db)  
7. The signal theshold is now given and by comparing it with the CUT level the CFAR_sig matrix  
   is built  
8. The results are then plotted  
9. A later tuning of the offset and the Training/Guarding cells number is required in order to  
   achieve an optimal performance of the CFAR (the offset can be chosen by giving a conservative value  
   which raises the theshold over the noise peaks in figure 2).  

About the selection of Training, Guard cells and offset:  

  The chosen parameters are the results of what has been said in the previous argumentation. By trying different  
  values it has been possible to achive a satisfying performance similar to the one shown in the walkthrough.  

About the suppression of the non-thresholded cells at the edges:  

   It is sufficient to initialize the CFAR_sig matrix to all zeros with the dimension of the RDM and by  
   indexing it correctly.
