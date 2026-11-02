# Wavelength Division Multiplexing (WDM) Simulation

## Aim 
To simulate a WDM system using Python and analyze channel separation and insertion loss.

## Apparatus/Software Required
	Python (NumPy)
	Google Colab or Jupyter Notebook

## Theory
	WDM allows multiple optical signals at different wavelengths to be transmitted simultaneously over a single fiber.
	Channel spacing determines spectral efficiency and crosstalk.
	Insertion loss is the reduction in signal power due to multiplexing/demultiplexing.

## Formula:
"Insertion Loss (dB)"=P_in-P_out
"Channel Spacing"=Δλ

## 1
## Setup Environment
Info
Prepare Python environment for simulation.
	Import NumPy and Matplotlib
	Define channel wavelengths and powers

## 2
## Define WDM Parameters
Specify input wavelengths and powers.
Example: λ = [1550, 1552, 1554] nm, Pin = -2 dBm
	Choose 3 channels
	Assign equal input power

## 3
## Calculate Output Power
Simulate insertion loss for each channel.
Insertion Loss = Pin - Pout
	Assume ~1 dB loss per channel
	Compute Pout

## 4
## Plot WDM Spectrum
Visualize channel separation.
	Use Matplotlib to plot wavelength vs power
	Label each channel peak

## 5
## Analyze Results
Success
Interpret the simulation output.
	Channels separated with ~1–2 dB insertion loss
	Verify spacing Δλ = 2 nm

## Sample Output
 <img width="623" height="478" alt="image" src="https://github.com/user-attachments/assets/7569e8ec-3417-4669-b37b-06029f87655a" />

 <img width="677" height="466" alt="image" src="https://github.com/user-attachments/assets/e937804f-b55d-4de9-ab1e-155e6bd01d8e" />

 <img width="652" height="456" alt="image" src="https://github.com/user-attachments/assets/d22a7a99-0cd4-439e-b49b-b9dde93ab78b" />

## Python Code 
```
import numpy as np
import matplotlib.pyplot as plt

w = np.linspace(1545, 1555, 1000)
c, b, n = 1550, 0.2, 5

def signal(spacing):
    return [np.exp(-(w-(c+(i-2)*spacing))**2/(2*b**2))
            for i in range(n)]

# Graph 1: Individual channels
ch = signal(0.8)
plt.figure()
for i, p in enumerate(ch):
    plt.plot(w, p, '--', label=f'Ch {i+1}')
plt.title("Individual WDM Channels")
plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.legend()
plt.grid()
plt.show()

# Graph 2: Multiplexed signal
plt.figure()
plt.plot(w, np.sum(ch, axis=0))
plt.title("Multiplexed WDM Signal")
plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.grid()
plt.show()

# Graph 3: Effect of channel spacing
plt.figure()
for s in [0.2, 0.8, 1.6]:
    plt.plot(w, np.sum(signal(s), axis=0), label=f'{s} nm')
plt.title("Effect of Channel Spacing")
plt.xlabel("Wavelength (nm)")
plt.ylabel("Power")
plt.legend()
plt.grid()
plt.show()

# Insertion loss
Pin, loss = -2, 1
print("Input Power:", Pin, "dBm")
print("Output Power:", Pin-loss, "dBm")
print("Insertion Loss:", loss, "dB")
```

## Output
<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/a92f9b3d-0b7a-4bb1-99be-3ca4f2eb14a9" />
<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/a2672310-3f91-4421-bfd9-e9c72fc2d15b" />
<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/49f63fcf-a592-4bc4-8e41-58dfdabb91f2" />


## Result 
The WDM system was successfully simulated using Python. Multiple optical signals with different wavelengths were multiplexed into a single optical channel and separated at the receiver.
