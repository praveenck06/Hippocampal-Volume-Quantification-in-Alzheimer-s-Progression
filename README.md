# Quantifying Hippocampus Volume for Alzheimer's Progression
### Background

Alzheimer's disease (AD) is a progressive neurodegenerative disorder that results in impaired neuronal (brain cell) function and eventually, cell death. AD is the most common cause of dementia. Clinically, it is characterized by memory loss, inability to learn new material, loss of language function, and other manifestations.

For patients exhibiting early symptoms, quantifying disease progression over time can help direct therapy and disease management.

A radiological study via MRI exam is currently one of the most advanced methods to quantify the disease. In particular, the measurement of hippocampal volume has proven useful to diagnose and track progression in several brain disorders, most notably in AD. Studies have shown a reduced volume of the hippocampus in patients with AD.

The hippocampus is a critical structure of the human brain (and the brain of other vertebrates) that plays important roles in the consolidation of information from short-term memory to long-term memory. In other words, the hippocampus is thought to be responsible for memory and learning (that's why we are all here, after all!)

<figure>
  <img src="EDA\notebook_images\Hippocampus_small.gif" style="margin: 0 auto;">
  </img>
  <figcaption style="text-align: center;">Hippocampus <br>Source: Life Science Databases (LSDB). Hippocampus. Images are from Anatomography maintained by Life Science Databases (LSDB). (2010). CC-BY-SA 2.1jp.</figcaption>
</figure>

###
Humans have two hippocampi, one in each hemisphere of the brain. They are located in the medial temporal lobe of the brain. Fun fact - the word "hippocampus" is roughly translated from Greek as "horselike" because of the similarity to a seahorse observed by one of the first anatomists to illustrate the structure, but you can also see the comparison in the following image.
<figure >
  <img src="EDA\notebook_images\hippocampus-and-seahorse-cropped.jpg" style="height:60px; width:80px; margin: 0 auto;"></img>
  <figcaption style="text-align: center;">Seahorse & Hippocampus <br> Source: Seress, Laszlo. Laszlo Seress' preparation of a human hippocampus alongside a sea horse. (1980). CC-BY-SA 1.0.</figcaption>
</figure>

###
According to <a target="_blank" href="https://www.sciencedirect.com/science/article/pii/S2213158219302542">Nobis et al., 2019</a>, the volume of hippocampus varies in a population, depending on various parameters, within certain boundaries, and it is possible to identify a "normal" range taking into account age, sex and brain hemisphere.

You can see this in the image below where the right hippocampal volume of women across ages 52 - 71 is shown. 

<figure >
  <img src="EDA\notebook_images\nomogram_fem_right.svg" style="height:60px; width:80px;"></img>
  <figcaption style="text-align: center;">Nomogram - Female, Right Hippocampus Volume, Corrected for Head Size<br>Source: Nobis, L., Manohar, S.G., Smith, S.M., Alfaro-Almagro, F., Jenkinson, M., Mackay, C.E., Husain, M.<br>Hippocampal volume across age: Nomograms derived from over 19,700 people in UK Biobank.<br>Neuroimage: Clinical, 23(2019), pp. 2213-1582. </figcaption>
</figure>

###
There is one problem with measuring the volume of the hippocampus using MRI scans, though - namely, the process tends to be quite tedious since every slice of the 3D volume needs to be analyzed, and the shape of the structure needs to be traced. The fact that the hippocampus has a non-uniform shape only makes it more challenging. Do you think you could spot the hippocampi in this axial slice below?



<figure >
  <img src="EDA\notebook_images\mri.jpg" style="height:60px; width:80px;"></img>
  <figcaption style="text-align: center;">Axial slice of an MRI image of the brain</figcaption>
</figure>

### Project Goal 
In this project we built an end-to-end AI system which features a machine learning algorithm that integrates into a clinical-grade viewer and automatically measures hippocampal volumes of new patients, as their studies are acquired and committed to the clinical imaging archive.

We used the dataset that contains the segmentations of the right hippocampus and used the U-Net architecture to build the segmentation model.

After that, we integrated the model into a working clinical PACS such that it runs on every incoming study and produces a report with volume measurements.

### Dataset
We used the "Hippocampus" dataset from the <a target="_blank" href="http://medicaldecathlon.com/">Medical Decathlon competition</a>. This dataset is stored as a collection of NIFTI files, with one file per volume, and one file per corresponding segmentation mask. The original images here are T2 MRI scans of the full brain. As noted, in this dataset we used cropped volumes where only the region around the hippocampus has been cut out. This makes the size of our dataset quite a bit smaller, our machine learning problem a bit simpler and allows us to have reasonable training times.

## Project Steps
### 1. EDA and preparing the dataset for hippocampus segmentation
Here we performed exploratory data analyis and curated the dataset for segmentation model training. Dataset consisted of 263 volumes out of which 3 were out liers (2 of them were CT scans of chest and 1 volume did not accompany with segmentation mask).  
<figure >
  <img src="EDA\notebook_images\image_segmentaion_mask.png"></img>
  <figcaption style="text-align: center;">Image and segmentation mask</figcaption>
</figure>

<figure >
  <img src="EDA\notebook_images\hippocampal_volume_distribution.png"></img>
  <figcaption style="text-align: center;">Hippocampal volume distribution in dataset</figcaption>
</figure>

### Training results
<table>
  <tr>
  <td valign="top">
    <img src="Model Training\images\train_image.png" >
        <figcaption style="text-align: center;">Training image</figcaption>
      </img>
  </td>
  <td valign="top">
    <img src="Model Training\images\val_image.png">
        <figcaption style="text-align: center;">Training mask</figcaption>
    </img>
  </td>
  <td valign="top">
    <img src="Model Training\images\train_prediction.png" >
        <figcaption style="text-align: center;">Training prediction</figcaption></img>
  </td>
  <td valign="top">
    <img src="Model Training\images\train_prob_map.png" >
        <figcaption style="text-align: center;">Training probability map</figcaption></img>
  </td>
  </tr>
<tr>
  <td valign="top">
    <img src="Model Training\images\val_image.png" >
        <figcaption style="text-align: center;">Validation image</figcaption></img>
</td>
  <td valign="top">
    <img src="Model Training\images\val_mask.png" >
        <figcaption style="text-align: center;">Validation mask</figcaption></img>
  </td>
  <td valign="top">
    <img src="Model Training\images\val_prediction.png" >
        <figcaption style="text-align: center;">Validation prediction</figcaption></img>
  </td>
  <td valign="top">
    <img src="Model Training\images\val_prob_map.png" >
        <figcaption style="text-align: center;">Validation probability map</figcaption></img>
  </td>
</tr>
</table>
