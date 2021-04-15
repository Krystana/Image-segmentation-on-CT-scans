IN PROCESS!

# Image-segmentation-on-CT-scans
image segmentation of the liver on CT scans using a U-net architecture neural network 


The project: 

As my final project of the data science bootcamp at Spiced Academy I chose to do image segmentation on CT scans inspired by this article: 
https://towardsdatascience.com/medical-images-segmentation-using-keras-7dc3be5a8524.
I chose to use a U-net architecture neural network and adapt my workflow based on these papers: 

 - Ronneberger et al.: 
 https://arxiv.org/pdf/1505.04597.pdf
 - Christ et al.: 
 https://arxiv.org/pdf/1702.05970.pdf
 - Klambauer et al.: 
 https://arxiv.org/abs/1706.02515
 
 
The dataset: 
 
The IRCAD dataset is available here: 
https://www.ircad.fr/research/3d-ircadb-01/
 
It consists of 3-dimensional CT scans in 2D slices of 20 patients in DICOM format, coming with organ masks/ground truths for different organs including the liver. As 17 of 20 patients display hepatic tumors, this dataset can also be used to segment tissue abnormalities in the liver and the simple segementation of the organ is more challenging due to inconsistent shapes. 

The data is structured in folders for each patient, containing subdirectories for the original scans and the corresponding masks for different organs. 

Stacking the 2D scans back together, a complete patient scan of the original size looks like this: 



The workflow: 

To handle the DICOM format I used the pydicom library: https://pydicom.github.io/
The original patient scans and masks, originally in 512 * 512 pixels were first scaled to 64 * 64  and later to 128 * 128 pixels to reduce training time.
The original scans were scaled to Hounsfield units between -1000 & 400 and then normalized to values between 0 and 1. The masks were binarized to values 0 & 1. 

First models were trained on the complete data with a shuffled train-test-split of 80/20. 
To be able to predict on a complete patient's scan I later decided to cut off a patient from the raw data and use only 19/20 patients for a train-test-split of 0.95. This decreased model performance but made it possible to visualize a complete CT scans with the predicted liver mask. 

Train and test data was saved and uploaded to google drive to be able to train the model on a google colab GPU. The model was then saved and downloaded to make predictions on the test data and the complete patient scan. 



The model: 

results: 

future work: 
