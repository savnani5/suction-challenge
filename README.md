## Welcome to the Nimble AI Programming Challenge

<p align="center">
 <img src="./assets/ur5e.png" width="35%">
</p>

The goal of this project is develop an algorithm that can predict ideal suctionable areas in cluttered scenes. Suction cups adhere best to flat, smooth and non-porous surfaces -- so something like a sponge wouldn't work since the air would escape from the holes.

<p align="center">
 <img src="./assets/rgb.png" width="35%">
</p>

For example, in the RGB image above, the green areas indicate locations where a suction cup would have maximal gripping success.

Your goal is to train a model that takes as input an RGB-D (rgb + depth) image and outputs a corresponding affordance map of values between 0 and 1 for each pixel in the input image, where values closer to 1 indicate more favorable locations for suction. These affordance maps should be visualized as heatmaps as shown in the  example below. 

<p align="center">
 <img src="./assets/heatmap.png" width="35%">
</p>

**Note 1**. You have the liberty of choosing what modality to use: you may choose to work with depth images alone, rgb images alone, or both modalities combined.  You may also pre-process the inputs if you'd like before feeding them to a model. If you do so please elaborate on what you are doing and why it helps with learning.

**Note 2**. We don't want an overly-parameterized network, so try to avoid pretrained Imagenet variants. We prioritize both accuracy (more specifically precision) and runtime. Be mindful of potential class imbalance when training your networks.

## Given

**1)** We've provided you with an inhouse dataset composed of RGB and Depth images of size `480x640` and their associated labels. Split the data into train and validation sets following standard rules of thumb. 

* `data/train/color/`: contains 465 training images in 24-bit PNG format.
* `data/train/depth/`: contains 465 training images in 16-bit PNG format.
* `data/train/label/`: contains 465 training labels in 8-bit grayscale PNG format.
* `data/test/color/`: contains 35 test images in 24-bit PNG format.
* `data/test/depth/`: contains 35 test images in 16-bit PNG format.
* `utils.py`: contains an example function for loading an RGB image, a Depth image and a label.

## Deliverables

A folder containing the output grasp affordance or 'heat' maps (i.e. pixel-wise probabilities) on the test set. They should be in the same format as the example heatmap shown above saved as PNGs. Additionally please provide a link and invite me as a collaborator (github: skalouche) to a **private** GitHub repo with your solution and a README describing:

*  your implementation details. This includes a description of things like model architecture, loss function, inputs modalities used, data augmentation (if any), reference papers used, etc.
*  what other approaches you would try if given more time.
*  quick instructions on how to run your code.


```
│----test-labels
│     │---- 0.png
│     │---- 1.png
│     │---- ...
│
```


## Evaluation

We'll be evaluating your results using 3 metrics:

* `overall accuracy`: the average overall accuracy
* `per class accuracy`: the average per class accuracy
* `precision`: the average precision

**Why do we care about the precision?** In robotic manipulation, the cost of a false positive is high because it leads to failed grasp attempts. Hence we prefer "restrained" prediction over false, "reckless" predictions.


## GPU Access

We provide the AWS credentials for access to an **Oregon region** EC2 p2.xlarge GPU instance. 

You can access the instance using the web interface or via the following terminal command. Please ensure that `applicationKeyPair.pem` is at the working directory.

`ssh -i "applicantKeyPair.pem" ubuntu@ec2-54-202-136-229.us-west-2.compute.amazonaws.com`

**PLEASE MAKE SURE TO STOP THE INSTANCE WHEN YOU ARE DONE TRAINING**
