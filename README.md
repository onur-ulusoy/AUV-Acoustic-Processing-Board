# Acoustic Processing Board (APB) Hardware

The Acoustic Processing Board (APB) is a specialized hardware project devoted to processing underwater acoustic signals, captured via hydrophones. This repository houses the electronic design and hardware specifications needed to construct or adapt the APB. Serving as a crucial tool for underwater exploration, navigation, and communication, the APB stands as a testament to innovative engineering solutions. This project is developed for ITU AUV Team.

<picture>   <img alt="filter-board" src="Media/pictures/filter-top-back.gif"> </picture>


<p align="center"><em >APB Filter Test Board</em></p>


<picture>   <img alt="dash" src="Media/logos/dash.png"> </picture>


<p align="center">
    <a href="https://auv.itu.edu.tr/">
        <img width="180" src="Media/logos/auv-electronics.png">
    </a>
</p>


<p align="center"><em >AUV Electronics 2022</em></p>

<picture>   <img alt="dash" src="Media/logos/dash.png"> </picture>


<p align="center">
    <a href="https://auv.itu.edu.tr/">
        <img width="600" src="Media/logos/auv.png">
    </a>
</p>


<picture>   <img alt="dash" src="Media/logos/dash.png"> </picture>

<p align="center">
    <img width="1500" src="Media/logos/logos.png">
</p>

<picture>   <img alt="dash" src="Media/logos/dash.png"> </picture>


## Table of Contents
- [Acoustic Processing Board (APB) Hardware](#acoustic-processing-board-apb-hardware)
  - [Table of Contents](#table-of-contents)
  - [Project Description](#project-description)

## Project Description

The Acoustic Processing Board (APB) is a pivotal development in the field of Autonomous Underwater Vehicles (AUVs), designed to accurately detect the positions of underwater objects. To optimize performance, APB is split into two distinct parts: an analog PCB and a digital PCB.

The focus of this repository is the analog PCB, which primarily serves as a bandpass filter for frequencies between 25 and 40kHz. This PCB is designed to filter incoming signals from hydrophones before they are passed onto the digital component of the APB. The board was meticulously designed and simulated using LTspice software, featuring components from Analog Devices. The physical layout of the PCB was then accomplished using Altium Designer.

In addition to the analog PCB, there is a complementary digital PCB. This board is responsible for processing the filtered signals from three hydrophones to determine the location of objects underwater. It employs Fast Fourier Transform (FFT) algorithms for signal processing, and is powered by an STM32 microcontroller.

In the interest of thorough testing and performance optimization, the first iteration of the filter PCB was designed for a single hydrophone. This approach enables focused testing on the filtering capabilities, allowing for incremental improvements and fine-tuning of the board's performance before scaling to a three-hydrophone system.

The APB is a testament to innovative design, offering a unique approach to signal processing for AUVs. It represents a significant contribution to our understanding and exploration of underwater environments. We encourage you to explore the repository, understand the design, and contribute to the ongoing development of this cutting-edge technology.

<picture>   <img alt="filter-board" src="Media/pictures/filter-perspective-1.png"> </picture>





