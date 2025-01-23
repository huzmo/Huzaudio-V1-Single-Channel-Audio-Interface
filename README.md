# Huzaudio V1 - Single-Channel-Audio-Interface
The Huzaudio V1 can record musical instruments such as an electric or bass guitar through a standard 1/4" jack onto a computer through a USB-A port. 
|![Image](https://github.com/user-attachments/assets/6939a45c-0f0c-433f-be5a-2fe05eec53c0)|![Image](https://github.com/user-attachments/assets/6231063b-43f3-4933-8657-e58aa7f2eb36)|
|:-:|:-:|


## Hardware
In order to select the right components, I created a diagram that depicted the process needed to complete the task at a high level and then found suitable ICs for each central task. These ICs served as "nodes" and related components and circuitry were selected in reference to manufacturer data sheets. Each component must be a suitable size to solder by hand but also small enough to maintain a compact form factor. 

The PCB was designed using KiCad, a free and open source EDA which provided the tools necessary to design my circuit. The schematic was designed to provide a lower-level representation of the initial flowchart and set the groundwork for a reliable PCB. Each of the squares on the above chart has been "translated" into circuitry and complementary components, such as decoupling capacitors and resistors, have been added. 
![image](https://github.com/user-attachments/assets/432ac4f9-2ff3-4602-8694-038e7be1e174)

The main issue when it comes to mixed signal boards is signal integrity. Knowing this, a great amount of research was conducted to ensure that my board was able to protect the sensitive analog inputs. A 4-layer board was chosen with the following stackup:
| Layer    |   Purpose      |
| -------- |        ------- |
| Layer 1  | Analog Signal  |
| Layer 2  |  Power Plane   |
| Layer 3  |  Ground Plane  |
| Layer 4  | Digital Signal |

The ground plane in between the two signal layers ensures that they are shielded from one another while also providing a short current return path. Analog and digital components are physically segregated from one another, and the ADC serves as a bridge between the two signal types. The above considerations, as well as low-noise ICs ensure that the instrument signal receives little disruption throughout the circuit. 
![Screenshot 2024-11-13 222611](https://github.com/user-attachments/assets/f5198d7e-fc96-484f-9680-99d215ecc69a)

## Software
Firmware for the audio interface must receive the converted digital signal via I2C from the analog-digital converter and send appropriately formatted packets to the computer. Software is written in C on the STM32F103C8T6 using the STM32CUBEIDE. The firmware is currently in development.

## Mechanical
The design for the case is straightforward to ensure functionality. An ample amount of room is provided to ensure that all components fit inside. To shield from EMI, the inside of the case is coated in a conductive material to ensure that EMI cannot leak nor enter and disrupt the sensitive analog signals.

## Simulation
To ensure my design worked before ordering the board, I ran some simulations using KiCad's built-in SPICE simulator. I tested if the input voltage regulators ensured stable power delivery and that the guitar input signal was amplified correctly as seen below.
![Screenshot 2024-12-19 172754](https://github.com/user-attachments/assets/8ecbbb42-d55f-4b9b-8eff-7ac639f1f66e)

## Next Steps
The design for this product was completed during an extended break from university and the prototyping for this project is projected to be held during the following semester break.
