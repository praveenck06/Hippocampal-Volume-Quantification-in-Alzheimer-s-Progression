# Quantifying Hippocampus Volume for Alzheimer's Progression
### Background

Alzheimer's disease (AD) is a progressive neurodegenerative disorder that results in impaired neuronal (brain cell) function and eventually, cell death. AD is the most common cause of dementia. Clinically, it is characterized by memory loss, inability to learn new material, loss of language function, and other manifestations.

For patients exhibiting early symptoms, quantifying disease progression over time can help direct therapy and disease management.

A radiological study via MRI exam is currently one of the most advanced methods to quantify the disease. In particular, the measurement of hippocampal volume has proven useful to diagnose and track progression in several brain disorders, most notably in AD. Studies have shown a reduced volume of the hippocampus in patients with AD.

The hippocampus is a critical structure of the human brain (and the brain of other vertebrates) that plays important roles in the consolidation of information from short-term memory to long-term memory. In other words, the hippocampus is thought to be responsible for memory and learning (that's why we are all here, after all!)

<figure>
  <img src="EDA\notebook_images\Hippocampus_small.gif" style="margin: 0 auto;">
  </img>
  <figcaption style="text-align: center; font-size: small;">Hippocampus <br>Source: Life Science Databases (LSDB). Hippocampus. Images are from Anatomography maintained by Life Science Databases (LSDB). (2010). CC-BY-SA 2.1jp.</figcaption>
</figure>

###
Humans have two hippocampi, one in each hemisphere of the brain. They are located in the medial temporal lobe of the brain. Fun fact - the word "hippocampus" is roughly translated from Greek as "horselike" because of the similarity to a seahorse observed by one of the first anatomists to illustrate the structure, but you can also see the comparison in the following image.
<figure >
  <img src="EDA\notebook_images\hippocampus-and-seahorse-cropped.jpg" style="height:260px; width:400px; margin: 0 auto;"></img>
  <figcaption style="text-align: center; font-size: small;">Seahorse & Hippocampus <br> Source: Seress, Laszlo. Laszlo Seress' preparation of a human hippocampus alongside a sea horse. (1980). CC-BY-SA 1.0.</figcaption>
</figure>

###
According to <a target="_blank" href="https://www.sciencedirect.com/science/article/pii/S2213158219302542">Nobis et al., 2019</a>, the volume of hippocampus varies in a population, depending on various parameters, within certain boundaries, and it is possible to identify a "normal" range taking into account age, sex and brain hemisphere.

You can see this in the image below where the right hippocampal volume of women across ages 52 - 71 is shown. 

<figure >
  <img src="EDA\notebook_images\nomogram_fem_right.png" style="height:360px; width:300px;"></img>
  <figcaption style="text-align: center; font-size: small;">Nomogram - Female, Right Hippocampus Volume, Corrected for Head Size<br>Source: Nobis, L., Manohar, S.G., Smith, S.M., Alfaro-Almagro, F., Jenkinson, M., Mackay, C.E., Husain, M.<br>Hippocampal volume across age: Nomograms derived from over 19,700 people in UK Biobank.<br>Neuroimage: Clinical, 23(2019), pp. 2213-1582. </figcaption>
</figure>

###
There is one problem with measuring the volume of the hippocampus using MRI scans, though - namely, the process tends to be quite tedious since every slice of the 3D volume needs to be analyzed, and the shape of the structure needs to be traced. The fact that the hippocampus has a non-uniform shape only makes it more challenging. Do you think you could spot the hippocampi in this axial slice below?



<figure >
  <img src="EDA\notebook_images\mri.jpg" style="height:360px; width:300px;"></img>
  <figcaption style="text-align: center; font-size: small;">Axial slice of an MRI image of the brain</figcaption>
</figure>

### Project Goal 
In this project we built an end-to-end AI system which features a machine learning algorithm that integrates into a clinical-grade viewer and automatically measures hippocampal volumes of new patients, as their studies are acquired and committed to the clinical imaging archive.

We used the dataset that contains the segmentations of the right hippocampus and used the U-Net architecture to build the segmentation model.

After that, we integrated the model into a working clinical PACS such that it runs on every incoming study and produces a report with volume measurements.

### Dataset
We used the "Hippocampus" dataset from the <a target="_blank" href="http://medicaldecathlon.com/">Medical Decathlon competition</a>. This dataset is stored as a collection of NIFTI files, with one file per volume, and one file per corresponding segmentation mask. The original images here are T2 MRI scans of the full brain. As noted, in this dataset we used cropped volumes where only the region around the hippocampus has been cut out. This makes the size of our dataset quite a bit smaller, our machine learning problem a bit simpler and allows us to have reasonable training times. Data is present

## Project Steps
### 1. EDA and preparing the dataset for hippocampus segmentation
Here we performed exploratory data analyis and curated the dataset for segmentation model training. Dataset consisted of 263 volumes out of which 3 were out liers (2 of them were CT scans of chest and 1 volume did not accompany with segmentation mask). Data is located in <code>data/TrainingSet</code>. <code> EDA/EDA.ipynb</code> contains code for curating the dataset
<figure >
  <img src="EDA\notebook_images\image_segmentaion_mask.png"></img>
  <figcaption style="text-align: center; font-size: small;">Image and segmentation mask</figcaption>
</figure>

###
<figure >
  <img src="EDA\notebook_images\hippocampal_volume_distribution.png"></img>
  <figcaption style="text-align: center; font-size: small;">Hippocampal volume distribution in dataset</figcaption>
</figure>


### 2. Training a segmentation CNN

We used PyTorch to train the segmentation model and Tensorboard to visualize the results.<code>Model Training/src/run_ml_pipeline.py</code> contains code for training the segmentaion model
<figure >
  <img src="ModelTraining\Train_val_loss_plot.svg"></img>
  <figcaption style="text-align: center; font-size: small;">Train and Validation loss plot</figcaption>
</figure>

##### Model predictions
<table>
  <tr>
  <td valign="top">
    <img src="ModelTraining\images\train_image.png" >
        <figcaption style="text-align: center; font-size: small;">Training image</figcaption>
      </img>
  </td>
  <td valign="top">
    <img src="ModelTraining\images\val_image.png">
        <figcaption style="text-align: center; font-size: small;">Training mask</figcaption>
    </img>
  </td>
  <td valign="top">
    <img src="ModelTraining\images\train_prediction.png" >
        <figcaption style="text-align: center; font-size: small;">Training prediction</figcaption></img>
  </td>
  <td valign="top">
    <img src="ModelTraining\images\train_prob_map.png" >
        <figcaption style="text-align: center; font-size: small;">Training probability map</figcaption></img>
  </td>
  </tr>
<tr>
  <td valign="top">
    <img src="ModelTraining\images\val_image.png" >
        <figcaption style="text-align: center; font-size: small;">Validation image</figcaption></img>
</td>
  <td valign="top">
    <img src="ModelTraining\images\val_mask.png" >
        <figcaption style="text-align: center; font-size: small;">Validation mask</figcaption></img>
  </td>
  <td valign="top">
    <img src="ModelTraining\images\val_prediction.png" >
        <figcaption style="text-align: center; font-size: small;">Validation prediction</figcaption></img>
  </td>
  <td valign="top">
    <img src="ModelTraining\images\val_prob_map.png" >
        <figcaption style="text-align: center; font-size: small;">Validation probability map</figcaption></img>
  </td>
</tr>
</table>

 ### 3.Integrating into a Clinical Network

 Here we tried to create AI product that can be integrated into a clinical network and provide the auto-computed information on the hippocampal volume to the clinicians. 

 <figure >
  <img src="EDA\notebook_images\network-setup.png"></img>
  <figcaption style="text-align: center; font-size: small;">Clinical Network setup emulation</figcaption>
</figure>

Specifically, we have the following software in this setup:
 <li>MRI scanner is represented by a script <code>Project Inference/src/deploy_scripts/send_volume.sh</code>. When we run this script it will simulate what happens after a radiological exam is complete, and send a volume to the clinical PACS</li>
 <li>PACS server is represented by Orthanc deployment that is listening to DICOM DIMSE requests on port 4242. Orthanc also has a DicomWeb interface that is exposed at port 8042, prefix /dicom-web. Our PACS server is also running an auto-routing module that sends a copy of everything it receives to an AI server</li>
 <li>Viewer system is represented by OHIF. It is connecting to the Orthanc server using DicomWeb and is serving a web application on port 3000.</li>
 <li> AI server is represented by a couple of scripts. <code>Project Inference/src/deploy_scripts/start_listener.sh</code>brings up a DCMTK's <code>storescp</code> and configures it to just copy everything it receives into a directory. 

####
<code>Project Inference/src/inference_dcm.py</code> will analyze the directory of the AI server that contains the routed studies, find the right series to run the AI algorithm on, will generate report, and push it back to PACS.
<figure >
  <img src="ProjectInference\out\segment_overlay_image_3_for_question.png"></img>
</figure>
<figure >
  <img src="ProjectInference\out\inference_in_OHIF_viewer.png"></img>
</figure>
<figure >
  <img src="ProjectInference\out\grid_view.png"></img>
  <figcaption style="text-align: center; font-size: small;"> Region of hippocampus as predicted by the model on the OHIF image-viewer using different layouts.</figcaption>
</figure>


### Validation Plan
We also tried to draft a validation plan of AI product to clear the regulatory bar for commercializing
<code>ProjectInference\ValidationPlanForHippocampAi.md</code>


### Acknowledgement

This project has been completed as a part of <a href="https://www.udacity.com/course/ai-for-healthcare-nanodegree--nd320" rel="nofollow">AI for Healthcare</a>


### License
This project is licensed under the terms of MIT License.
