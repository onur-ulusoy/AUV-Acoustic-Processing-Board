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
    - [Analog Power Supply](#analog-power-supply)
    - [ADC Buffering](#adc-buffering)
  - [Simulation](#simulation)
  - [Filter Test Board](#filter-test-board)

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

### Analog Power Supply

The analog power supply is an integral part of our design. Va is the input, and Agnd is the output. This unit provides the necessary power for all analog sections of the APB. Va and Agnd form the positive and negative poles of the op-amp in the other circuits. By generating a stable and low-noise power supply, this circuit ensures that the operational amplifiers and other analog components function optimally, minimizing signal distortion and maintaining high signal-to-noise ratios.

<p align="center">
    <a>
        <img width="600" src="Media/circuits/analog-power-supply.png">
    </a>
</p>

### ADC Buffering

ADC buffering serves as the bridge between the analog and digital domains of our APB design. This stage, replicated three times for each hydrophone, takes the filtered signal, Vfout, as input and provides Vadc as output. The buffer, a unity gain amplifier (1x amp), plays a critical role in this system. Its purpose is to isolate the preceding stages from the ADC load. This isolation prevents any impedance mismatch that could degrade the signal quality. By using a buffer, we ensure that the signals processed by the ADC reflect as closely as possible the filtered signals from the bandpass filter stage, enabling accurate digital representation of the original acoustic signals.

<p align="center">
    <a>
        <img width="320" src="Media/circuits/adc-buffering.png">
    </a>
</p>


## Simulation

The APB analog subsystem was thoroughly simulated using LTspice, a high-performance SPICE simulator. LTspice offers a variety of capabilities, including enhanced SPICE and an integrated waveform viewer, making it a powerful tool for circuit analysis.

The simulation process involved the use of specific op-amps from Analog Devices. This choice of op-amps was driven by their favorable characteristics, such as low noise, high precision, and their performance within the frequency band of interest.

To ascertain the effectiveness of our 6-pole Butterworth bandpass filter design, we carried out frequency domain analysis. The results are demonstrated in the Bode plot below. As can be seen, the filter provides a passband for frequencies between 25 and 40 kHz, while attenuating frequencies outside this band. This frequency range was chosen specifically to match the operating range of the hydrophones and the acoustic signals they receive.

The simulation results validate the performance of the filter design and provide confidence in its ability to function as intended in the real-world application.

<p align="center">
    <a>
        <img width="1800" src="Media/circuits/bode-plot.png">
    </a>
</p>


## Filter Test Board

As part of our development and testing process, we designed a standalone PCB specifically for testing the performance of the filter stage and associated circuits. This board, known as the Filter Test Board, includes only the Butterworth filter, ADC buffering, and pre-amplification circuits, all for just a single hydrophone. 

The Filter Test Board contains crucial components from our original APB analog design that we aimed to test in isolation. We included the Butterworth filter stage, which is the centerpiece of our acoustic processing, to evaluate its frequency response and signal attenuation properties. The Pre-Amplification stage is also included, as it plays a crucial role in enhancing the signals coming from the hydrophone. Additionally, the ADC Buffering stage is incorporated into it. This stage is crucial for isolating the ADC load from the preceding stages, thereby preserving signal integrity. By focusing on these critical parts, the Filter Test Board allows us to verify the operation and performance of the main building blocks of our system without the interference of other elements. As a summary, It is basically includes cruical parts to process one hydrophone signal.


To aid in testing, we've added test points at key output locations like Vampin or Vfin as you can see in the below pcb picture, allowing for easy hook-up of measurement equipment such as oscilloscopes or signal generators. This way, we can inject signals and observe the system's response directly. We gave some voltages such as 1.65V directly to get rid of some power circuits.

Furthermore, we've chosen to use industrial-grade connectors for power supply and signal output. These connectors provide robust, reliable connections, crucial for both testing and eventual deployment.

