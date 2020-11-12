# SOGNO - microservices oriented power system automation

## Vision

The energy decarbonisation increases the share of renewables based distributed generation that is connected to the distribution level of grids. Similarly, the electrification of mobility and heating as well as the flexibility offered by customers result in new power profiles and have a
large impact on the operation of distribution grids. Network reinforcements are not sufficient any longer to deal with the increasing complexity of distribution systems. The deployment of advanced distribution management systems down to the low voltage network is required.

SOGNO aims at facilitating the transition to a modular microservices based control center software solution for distribution system operators. This allows operators to adapt faster because components can be updated more independently from each other. It provides system operators and automation software developers with an open source framework that exposes open APIs to plug in new automation functions and supports industry standards such as CIM IEC61970 and IEC61850. The vision is to integrate today’s SCADA systems with SOGNO and gradually move functionalities into microservices.

A preliminary set of automation functionalities will be provided together with the framework and should be further developed as part of the SOGNO project:
- state-estimation
- load prediction
- voltage control

The functionalities developed as part of the project will not be treated differently from any other SOGNO compatible automation functions developed externally and use the same interfaces. Due to modules for real-time simulation, the SOGNO project supports a seamless integration of
development, testing and deployment. New automation functionalities can be developed and thoroughly tested against a virtual real-time representation of the power system.

## Architecture

Here goes the description of the architecture independent of specific function / service implementations.

## Implementation

### Services

- [packaging catalogue](https://git.rwth-aachen.de/acs/public/catalogue)
- [state estimation](https://git.rwth-aachen.de/acs/public/automation/pyvolt)
- [load forecasting](https://git.rwth-aachen.de/acs/public/automation/plf)
- [coordinated voltage control](https://git.rwth-aachen.de/acs/public/automation/covee)
- [real-time simulation](https://github.com/dpsim-simulator)
- [real-time simulation monitoring](https://github.com/VILLASframework/VILLASweb)
- [(protocol) gateway for real-time applications](https://github.com/VILLASframework/VILLASnode)
- [IEC CIM adapters](https://github.com/cim-iec)

### API specifications

- [DPsim-CIM API](https://git.rwth-aachen.de/acs/public/cim/cimpy-server/-/blob/master/openapi.yaml)
- [VILLASnode (daemon)](https://git.rwth-aachen.de/acs/public/villas/node/-/blob/master/doc/openapi.yaml)
- [VILLASnode (relay)](https://git.rwth-aachen.de/acs/public/villas/node/-/blob/master/doc/openapi.yaml)
- [VILLASweb](https://git.rwth-aachen.de/acs/public/villas/web-backend-go/-/blob/master/doc/api/swagger.yaml)
- [FIWARE](https://github.com/FIWARE/specifications)
