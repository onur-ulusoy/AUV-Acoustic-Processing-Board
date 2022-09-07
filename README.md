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
  - [Electronics Design](#electronics-design)
    - [Hydrophone Biasing](#hydrophone-biasing)
    - [Pre-Amplification](#pre-amplification)
    - [6 Pole Butterworth Bandpass Filter](#6-pole-butterworth-bandpass-filter)

## Project Description

The Acoustic Processing Board (APB) is a pivotal development in the field of Autonomous Underwater Vehicles (AUVs), designed to accurately detect the positions of underwater objects. To optimize performance, APB is split into two distinct parts: an analog PCB and a digital PCB.

The focus of this repository is the analog PCB, which primarily serves as a bandpass filter for frequencies between 25 and 40kHz. This PCB is designed to filter incoming signals from hydrophones before they are passed onto the digital component of the APB. The board was meticulously designed and simulated using LTspice software, featuring components from Analog Devices. The physical layout of the PCB was then accomplished using Altium Designer.

In addition to the analog PCB, there is a complementary digital PCB. This board is responsible for processing the filtered signals from three hydrophones to determine the location of objects underwater. It employs Fast Fourier Transform (FFT) algorithms for signal processing, and is powered by an STM32 microcontroller.

In the interest of thorough testing and performance optimization, the first iteration of the filter PCB was designed for a single hydrophone. This approach enables focused testing on the filtering capabilities, allowing for incremental improvements and fine-tuning of the board's performance before scaling to a three-hydrophone system.

The APB is a testament to innovative design, offering a unique approach to signal processing for AUVs. It represents a significant contribution to our understanding and exploration of underwater environments. We encourage you to explore the repository, understand the design, and contribute to the ongoing development of this cutting-edge technology.

<picture>   <img alt="filter-board" src="Media/pictures/filter-perspective-1.png"> </picture>





## Electronics Design

The APB Analog's design is a combination of intricate electronic engineering concepts and high-precision layout work. For an in-depth understanding of its composition, be sure to check the [Full schematics](/LTSpice_Simulation/Full%20Schematic.pdf) and [PCB Schematic Sheets](/Schematic%20Sheets/) These documents not only delineate the arrangement and interconnectivity of the board's components, but also offer insightful details about their specific roles and functionalities. Whether you're interested in the bandpass filtering process, power distribution, or the input/output interfaces, the schematic sheets hold the key to understanding the APB Analog's operational architecture.

### Hydrophone Biasing 

Hydrophone biasing is the first stage in our APB design, and it's vital to the overall functionality of the system. For each of the three hydrophones, a Vhyd- and Vhyd+ and Vcc are the inputs, while Vampin is the output. Importantly, Vhyd- is grounded. This arrangement ensures the correct biasing of the hydrophones, setting the correct operating point for each device and allowing for the effective conversion of underwater acoustic signals into electrical signals.

<p align="center">
    <a>
        <img width="340" src="Media/circuits/hydrophone-biasing.png">
    </a>
</p>

### Pre-Amplification

The pre-amplification stage is another essential component of our APB design, ensuring that the electrical signals produced by the hydrophones are amplified adequately for further processing. This stage also employs three separate units, one for each hydrophone. Vampin is used as the input, while Vfin serves as the output. The pre-amplifier is driven by a high precision op-amp, ensuring low-noise amplification and thereby enhancing the clarity and resolution of the captured signals.

<p align="center">
    <a>
        <img width="320" src="Media/circuits/pre-amplification.png">
    </a>
</p>

### 6 Pole Butterworth Bandpass Filter

To further process the amplified signals, we employ a 6-pole Butterworth bandpass filter. This filter is replicated three times, once for each hydrophone. The selection of this specific filter topology allows for a flat frequency response in the passband, and a fast roll-off rate, making it highly suitable for our signal processing needs. Appropriate capacitor and resistor values were determined using Analog Devices' application notes. The filter takes Vfin as an input and outputs a filtered signal, Vfout. Each operational amplifier in this stage is referenced with Agnd, which is supplied by the analog power supply circuit.

<p align="center">
    <a>
        <img width="1200" src="Media/circuits/butterworth.png">
    </a>
</p>


