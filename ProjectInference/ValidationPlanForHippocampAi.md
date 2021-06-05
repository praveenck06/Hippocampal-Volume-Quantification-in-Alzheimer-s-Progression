# Validation plan for HippocampAi
## What is the intended use of the product?
The intended use of HippocampAi is to automatically segment and compute the volume of hippocampus from MRI scans. Hippocampus is automatically detected and overlaid as mask over the hippocampus for the radiologist. The volume of the segmentation is automatically computed and provided for inclusion in the final report.  The computation of volume is performed just after the image accusation.

## How was the training data collected?
Dataset used for HippocampAi is collected from Medical Decathlon competition. This dataset is stored as a collection of NIFTI files, with one file per volume, and one file per corresponding segmentation mask. The original images here are T2 MRI scans of the full brain but for our model training we used the cropped volumes where only the region around the hippocampus has been cut out.

## How did you label your training data?
All data has been labeled verified by an expert human rater (Radiologist), and with the best effort to mimic the accuracy required for clinical use.

## How was the training performance of the algorithm measured and how is the real-world performance going to be estimated?
The training performance of the algorithm is measured by using the following evaluation metrics:
•	Dice Similarity Coefficient
•	 Jaccard Distance
•	Sensitivity 
•	Specificity

The real-world performance would be comparison between the volume calculated by the radiologist and the HippocampAi

## What data will the algorithm perform well in the real world and what data it might not perform well on?
Since the model is trained only on the cropped volume of the T2 MRI scans it will perform well only on the cropped volumes and not on the entire T2 MRI scans.
