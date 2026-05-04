STM32-BMI270-Embedded-Driver
A high-performance, DMA-optimized C library for the Bosch BMI270 6-axis IMU, specifically designed for STM32F4 and other ARM Cortex-M microcontrollers.

🚀 Why I Built This?
While developing my custom FPV flight controller, I spent days searching for a clean, register-level STM32 driver for the BMI270. Most existing libraries were either too bloated, hidden inside Linux kernel drivers, or written only for Arduino.

I developed this library from scratch to fill this gap. It is specifically optimized for reading high-speed Gyroscope data, which is the heart of any flight control system.

What to Expect
Focus on Performance: This is not a "full-feature" library with every power mode. It is a lean starting point focused on getting clean, fast gyro data for PID loops.

Open for Development: I shared this because I couldn't find it when I needed it. Feel free to take this code, fork it, and add Accelerometer, I2C, or advanced features. It’s a solid foundation for your own projects.

📉 Signal Processing: 
Built-in Biquad FilterRaw data from any IMU contains high-frequency noise caused by motor vibrations and frame resonance. To solve this, I’ve implemented a Second-Order Biquad Low Pass Filter within the driver.Clean Data: Smooths out the 0.01 dps jitter into a rock-solid baseline.

Reduced Latency: Optimized for real-time performance, ensuring the PID loop gets the freshest data without significant delay.

Customizable: You can easily adjust the cutoff frequency ($f_c$) and sampling rate ($f_s$) to match your drone's specific vibration profile.Filter ImplementationThe filter uses a standard Direct Form II transposed structure to ensure stability and efficiency on the STM32's ARM Cortex-M core:$$y[n] = b_0 x[n] + b_1 x[n-1] + b_2 x[n-2] - a_1 y[n-1] - a_2 y[n-2]$$By including this, the driver provides "Flight-Ready" data instead of just raw ADC values.

🛠 Hardware Configuration
BMI270 Pin	  STM32F4 Pin (Typical)	    Function
VCC	            3.3V	                  Power Supply
GND	            GND	                    Ground
CS	            PA4	                    Chip Select (GPIO_Output)
SCK	            PA5	                    SPI Clock (SPI1_SCK)
MISO	          PA6	                    Master In Slave Out (SPI1_MISO)
MOSI	          PA7	                    Master Out Slave In (SPI1_MOSI)

✨ Key Features
SPI DMA Support: Minimizes CPU overhead by using DMA for data transfers.

Precise Calibration: Built-in routine to calculate and remove gyroscope offsets.

The 0x92 Rule: Correctly implements the mandatory "Read Bit" and dummy byte handling required by BMI270.

Low Noise: Achieves stable readings with minimal jitter (approx 0.01 dps at rest).

🤝 Contributing
Since this was created because of a lack of resources, I highly encourage you to contribute! If you add features like Accelerometer support or I2C, please send a Pull Request so we can make this the go-to resource for STM32 users.


