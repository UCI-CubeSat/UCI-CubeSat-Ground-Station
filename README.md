# UCI-CubeSat-Ground-Station
![Ground Station Block Diagram](https://github.com/UCI-CubeSat/UCI-CubeSat-Ground-Station/blob/main/doc/CubeSAT%20Ground%20Station.jpg)

## RF Links

The ground station infrastructure provides communications functions between the ground and the spacecraft, (1) up/downlink communications on UHF for the Telemetry Beacons and Command Responses from the spacecraft

The UHF component is centered in the 435 to 438 MHz amateur spacecraft service band and utilizes a <circular polarized directional Yagi> antenna with a <RHCP/LHCP polarization sense switch>. The antenna is mounted on an azimuth/elevation antenna positioner. A coax switch connects the UHF antenna to either a Low Noise Amplifier (LNA) for receiving, or a Power Amplifier (PA) for transmitting. The LNA and PA is then connected to a Software Defined Radio (SDR) that provides both UHF RF input and output signals.
  
The SDR used for UHF is the LimeSDR from LimeMicro, which utilizes GnuRadio for modulation and demodulation. The emission type is AFSK at >1200 kb/s, and was chosen for the compatibility with the transceiver radio on the spacecraft, an acceptable performance indicated by the link budget, and is somewhat common in the amateur satellite community.
  
## Antenna positioner

An antenna positioner controller is used to aim the antenna array and is interfaced serially using the EasyComm control protocol accessible through the HamLib control library. The positioner controller is based on the Open Source hardware/software project by K3NG/SatNOGs, and provides the ability for tracking control through HamLib _rotctld_ both locally using GPredict OR our own Python Tracker, or by the SatNOGS Client software which provides interconnectivity to the SatNOGS system over the Internet.

## GnuRadio 

Data is passed into/out of the ground station radio through GnuRadio ModCod blocks and can provide raw IQ sample files from the payload data. Doppler shift can be compensated for in real time using the tracking software and an XML/RPC server in GnuRadio.

## Data
  
The Engineering Control/Telemetry subsystem provides telemetry data to the ground in the form a AFSK modulated data frame (Ax.25/HDLC) in response to a command request. There are several satellite housekeeping commands that can be sent up from the ground to control power, attitude and payload functions, and most importantly a command to reliably shut off all RF transmissions if required.
