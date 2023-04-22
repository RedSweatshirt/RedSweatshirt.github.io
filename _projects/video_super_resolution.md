---
layout: page
title: Frame Recurrent Video Super Resolution
description: MIT Advances in Computer Vision (6.869) Final Project
img: assets/img/vsr_6869/FRVSRModel.png
importance: 1
category: school
---

<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm-6 mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/lowres.png" title="Low Res Frame" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
        <div class="col-sm-5 mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/RAFRVSR.png" title="Upscaled Frame" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    On the left, a frame from a low resolution video. Right, the same upscaled frame using my model.
</div>

Enhancing Video Quality Using Advanced Neural Networks
In the pursuit of enhancing video quality, I took on an exciting project for my class Advances in Computer Vision (6.869) at MIT in Spring 2022. The project focused on improving the [Frame Recurrent Video Super Resolution](https://arxiv.org/pdf/1801.04590.pdf) (FRVSR) neural network by implementing perceptual loss and incorporating the state-of-the-art [RAFT](https://arxiv.org/pdf/2003.12039.pdf) optical flow network.

#### Motivation

Super-resolution is the process of transforming a low-resolution image or video into a higher-resolution output. This technique is essential in various applications, such as restoring old films, enhancing streaming video quality, and improving the visuals of video games. Traditional methods, like bicubic up-sampling, tend to smooth out textures and edges, causing a loss of high-frequency details. More recent approaches, such as convolutional neural networks (CNNs) and Generative Adversarial Networks (GANs), have shown promising results, but often come with higher computational costs.

The idea behind FRVSR is to use a recurrent network to implement video super-resolution, providing more temporal consistency and spatial awareness of content in a video. FRVSR utilizes SRNet as the super resolution network block, incorporated with FlowNet to  The goal of this project was to enhance the FRVSR network by introducing perceptual loss and replacing the existing FlowNet with the more advanced RAFT network. This would allow the network to focus on high-level content losses while maintaining spatial and temporal consistency.

#### Project Overview

<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/FRVSRModel.png" title="FRVSR Model Diagram" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</div>
<div class="caption">
    The FRVSR Model. Image source: https://arxiv.org/pdf/1801.04590.pdf
</div>
<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/RAFTModel.png" title="RAFT Model Diagram" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</div>
<div class="caption">
    RAFT Flow Network Model. Image source: https://arxiv.org/pdf/2003.12039.pdf
</div>

To achieve this goal, I started with an implementation of the original FRVSR model and updated it, fixing errors and retraining the network multiple times with revised loss functions. I also incorporated a pre-trained implementation of RAFT and rewrote the FRVSR network to work seamlessly with it.

The improved FRVSR network architecture consists of an SRNet super-resolution block and an optical flow network block (RAFT). The previous frame is fed into the flow network, which sends the flow resolution to the super-resolution network, SRNet, to be combined with the actual current low-resolution frame to be upscaled. The SRNet then produces a super-resolved high-resolution output.

The loss functions used in this project include per-pixel loss, perception loss, total variation loss, and flow loss. By experimenting with different weight parameters and RAFT models, I was able to fine-tune the network for improved performance.

#### Loss Functions

In this project, a combination of various loss functions was utilized to optimize the performance of the SRNet model.

1. Per-Pixel Loss: This loss function, calculated using Mean Squared Error (MSE), measures the low-level content differences between the super-resolved output and the ground truth high-resolution image. The equation for per-pixel loss is:

$$L_{\text{per-pixel}} = \sum_{i=1}^{n}(I_{\text{upscaled}}-I_{\text{ground truth}})^2$$

2. Perception Loss: This loss function captures high-level content similarities by measuring the difference in feature representation between the upscaled output and the ground truth image. The equation for perception loss is:

$$L_{\text{perception}} = \sum_{i=1}^{n}(F_{\text{upscaled}}-F_{\text{ground truth}})^2$$
 
3. Total Variation Loss: To reduce noise in the output, this loss function measures the integral of the absolute image gradient under the assumption that an image with significant noise will have a high-valued integral. The equation for total variation loss is:

$$L_{\text{total variation}} = \sum_{i, j}\sqrt{|I_{i+1,j} - I_{i,j}|^2 + |y_{i,j+1}-y_{i,j}|^2}$$
 
4. Flow Loss: To maintain temporal stability between frames, this loss function calculates the Mean Squared Error per-pixel between the predicted high-resolution frame morphed from the flow estimation and the current ground truth low-resolution frame. The equation for flow loss is:

$$L_{flow} = \sum_{i=1}^{n}(I_{\text{flow morphed}}-I_{\text{ground truth low res}})^2$$
 
5. Total Loss: The overall loss function is a combination of the aforementioned losses and is used to optimize the entire network. For a single video in the training set, the loss is averaged across all frames. The equation for total loss is:

$$ L_{\text{total video}} = \sum_{i=1}^{n}(L_{\text{frame n}}) $$

These loss functions work together to create a more accurate and visually pleasing super-resolution output while preserving both low and high-level content similarities and maintaining temporal stability.

#### Training

During the training phase of this project, the Vimeo90k dataset, specifically designed for image super-resolution, was utilized. The dataset consists of 7,824 videos, each containing 7 frames. Both high-resolution (448 x 256 pixels) and low-resolution (112 x 64 pixels) versions of the videos were provided. To simplify the process, low-resolution images were upscaled to the output resolution using Bilinear interpolation before being run through the network and compared to their high-resolution counterparts.

Due to resource limitations, the dataset used for training was restricted to a subset of 2,500 videos, with a 20% validation split. The model was trained on an RTX 2070 Super Max-Q laptop GPU, with each of the 10 epochs taking approximately one hour to complete. This resource-conscious approach allowed for efficient model training while still yielding impressive results.

#### Results and Conclusion

<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/lowres.png" title="Low Res Frame" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/bicubic.png" title="Low Res Frame" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/groundtruth.png" title="Ground Truth Frame" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    On the left, a frame from a low resolution video. Middle, the frame upscaled using traditional bicubic interpolation. Right, the ground truth frame.
</div>

<div class="container">
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/FRVSR.png" title="Upscaled Frame using FRVSR" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.html path="assets/img/vsr_6869/RAFRVSR.png" title="Upscaled Frame using my Model" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
    </div>
</div>
<div class="caption">
    Left, the frame upscaled using the original FRVSR. Right, the frame upscaled using my new model.
</div>

To evaluate the results, I focused on qualitative details, peak signal-to-noise ratio (PSNR), and structural similarity index (SSIM). The improved network produced visually pleasing images with finer texture detail and sharper edges compared to the original FRVSR. However, it also suffered from amplifying noise present in the videos, causing the average PSNR and SSIM to be lower than expected.

Despite this drawback, the modified network shows promise in producing visually pleasing results compared to the original FRVSR when trained on the same dataset and with the same hyperparameters. Further improvements can be made by refining the loss functions, using more robust datasets, and increasing the dataset size, batch size, and number of epochs trained. For this project in particular, due to limited GPU resources and time constraints, the number of epochs trained during the project was lower than desired. This impacted the overall performance of the model, as it could have potentially improved further with additional training time.

In conclusion, this project has demonstrated the potential of enhancing video super-resolution using advanced neural networks and incorporating perceptual loss and RAFT. With further research and optimization, these techniques can be applied in a wide range of applications to significantly improve video quality.

#### Videos
Sample input and output videos are available below.
<center>
    <video controls>
    <source src="/assets/video/orig.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    <div class="caption">
        The ground truth video
    </div>
</center>

<center>
    <video controls>
    <source src="/assets/video/lowres.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    <div class="caption">
        The downscaled low resolution input video
    </div>
</center>

<center>
    <video controls>
    <source src="/assets/video/bicubic.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    <div class="caption">
        Video upscaled using traditional bicubic interpolation
    </div>
</center>

<center>
    <video controls>
    <source src="/assets/video/frvsr.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    <div class="caption">
        Video upscaled using original FRVSR
    </div>
</center>

<center>
    <video controls>
    <source src="/assets/video/rafrvsr.mp4" type="video/mp4">
    Your browser does not support the video tag.
    </video>
    <div class="caption">
        Video upscaled using my method
    </div>
</center>