# Quantifying Hippocampus Volume for Alzheimer's Progression
## Background

Alzheimer's disease (AD) is a progressive neurodegenerative disorder that results in impaired neuronal (brain cell) function and eventually, cell death. AD is the most common cause of dementia. Clinically, it is characterized by memory loss, inability to learn new material, loss of language function, and other manifestations.

For patients exhibiting early symptoms, quantifying disease progression over time can help direct therapy and disease management.

A radiological study via MRI exam is currently one of the most advanced methods to quantify the disease. In particular, the measurement of hippocampal volume has proven useful to diagnose and track progression in several brain disorders, most notably in AD. Studies have shown a reduced volume of the hippocampus in patients with AD.

The hippocampus is a critical structure of the human brain (and the brain of other vertebrates) that plays important roles in the consolidation of information from short-term memory to long-term memory. In other words, the hippocampus is thought to be responsible for memory and learning (that's why we are all here, after all!)

<figure>
  <img src="EDA\notebook_images\Hippocampus_small.gif">
  </img>
  <figcaption>Hippocampus</figcaption>
    <figcaption>Source: Life Science Databases (LSDB). Hippocampus. Images are from Anatomography maintained by Life Science Databases (LSDB). (2010). CC-BY-SA 2.1jp.</figcaption>
</figure>

Humans have two hippocampi, one in each hemisphere of the brain. They are located in the medial temporal lobe of the brain. Fun fact - the word "hippocampus" is roughly translated from Greek as "horselike" because of the similarity to a seahorse observed by one of the first anatomists to illustrate the structure, but you can also see the comparison in the following image.
<figure>
  <img src="EDA\notebook_images\hippocampus-and-seahorse-cropped.jpg"></img>
  <figcaption style="text-align: center;">Seahorse & Hippocampus</figcaption>
  <figcaption style="text-align: center;">Source: Seress, Laszlo. Laszlo Seress' preparation of a human hippocampus alongside a sea horse. (1980). CC-BY-SA 1.0.</figcaption>
</figure>

According to <a target="_blank" href="https://www.sciencedirect.com/science/article/pii/S2213158219302542">Nobis et al., 2019</a>, the volume of hippocampus varies in a population, depending on various parameters, within certain boundaries, and it is possible to identify a "normal" range taking into account age, sex and brain hemisphere.


## Training results
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
