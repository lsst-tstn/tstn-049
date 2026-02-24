# Calibration Reflector

```{abstract}
The Calibration Reflector is mounted on the top end of the TMA and is used to reflect light from the Flatfield Projector onto the Calibration screen. This document describes the projector and how to use it.
```

## Overview

The Rubin Calibration Reflector is an optic mounted on the top end of the TMA that is used to reflect light from the Flatfield Projector to the calibration screen. The flatfield projector is mounted in the center of the calibration screen on the dome. The reflector is an aspheric optic fabricated out of a block of aluminum. It is mounted on hexapod legs that are secured to the top end of the camera and are adjustable by hand. 

```{figure} refl_overview.png
:figclass: technote-wide-content

Calibration Reflector
```

The reflector was manufactured in the NOIRLab instrument shop in Tucson.

All drawings can be found on docushare, here: https://docushare.lsst.org/docushare/dsweb/View/Collection-15468 

## Design
The shape of the asphere is very specific, allowing a ~f/4 beam to be projected in such a way to illuminate the 10m diameter calibration screen with a constant brightness across the screen.

```{figure} refl_optical_presc.png
:figclass: technote-wide-content

Reflector Optical Prescription
```

The optic was milled at the NOIRLab instrument shop, using a laser tracker to confirm the shape. The shape was reconfirmed in the lab.

There are three SMR's attached to the optic that can be used to align it to the optical axis of the TMA. The are symmetrically placed around the Reflector.

There are three cover panels that can be opened and closed using CSC commands. Each panel is connected to a Firgelli Automations Optical Feeback Actuator (part #: FA-OS-35-12-18).

The mirror is attached to the top of the camera via six hexapod legs that extend over the pancake wrap. They are adjustable by hand so the Reflector can be aligned with the optical axis of the TMA. They are held to the structure with restrainer brackets so they can easily be attached to the Reflector

## Installation
Prior to installation, it's necessary to attach pairs of the hexapod legs with their respective restrainer bracket. The hexapod legs are not all identical, so care should be made with the pairing of the hexapods, which are all labelled. 

With the TMA at horizon, a manlift on L8 can be used to install the three hexapod leg pairs, attaching the feet of each hexapod as well as the restrainer bracket. 

The Reflector can now be lifted with the overhead crane on its triangle frame and brought into place with the help of pins on the hexapod lege assemblies. The triangle frame can then be bolted to the hexapod legs.

The Reflector will need to be removed every time the camera is removed

### Cart
Since the Reflector will need to be removed every time the camera is removed, a special cart was constructed for it. When the Reflector is to be removed, first unbolt the triangle frame and lower the reflector on to the cart. The hexapod legs can now be removed and also placed on the cart.

The cart is kept in storage in on the 3rd floor. 

```{figure} reflector_cart.png
:figclass: technote-wide-content

Reflector cart, including a place for the triangle frame and hexapod legs. 
```

## Alignment
Describe how we will measure the optical axis of the TMA, measure points in common, then measure the location of the Reflector. 

Once the reflector is aligned with the optical axis of the TMA, it needs to be aligned with the flatfield projector.

## Electronics
The electronics to open/close the covers are located in the electrical cabinet at the top end of the TMA (TEA-Cabinet 03). The rack is powered and connected to the TEA-AS-02 Port 2, with PDU port 3.

They are connected to the linear actuators via a single power cable.

Each of the three cover panels is attached to a linear actuator. These are all commanded together using Double-Pull Double-Throw switches. 

CIO0 is connected to SSR1 and SSR2 to Open the Reflector.
CIO1 is connected to SSR3 and SSR4 to Close the Reflector.

The switches are commanded using a LabJackT4, which can be found at `tea-reflector.cp.lsst.org`

```{figure} refl_electronics.png
:figclass: technote-wide-content

Electronics for controlling the Reflector covers.
```

### Remote Control 
If for some reason the LabJack and CSC are not working to open the Reflector covers, there is a backup approach. The power cable can be disconnected from the electronics cabinet and attached to the Linear Actuator remote controller box, which requires 12V power (see setup below).

```{figure} refl_remote_setup.png
:figclass: technote-wide-content

Setup for using the remote control for the Reflector cover actuators.
```
When this controller is connected to the Reflector, you should be able to use the small handheld remote (like for a garage) to open and close the reflector. These parts are connected to the triangle frame if needed.

## Control Software
The Reflector runs off of its own CSC, MTReflector.
Github: https://github.com/lsst-ts/ts_mtreflector
XML: https://ts-xml.lsst.io/sal_interfaces/MTReflector.html

There are essentially only two functional commands: `open` and `close`.

If you need to access the Reflector directly through the LabJack, you can use the [Kipling App](https://support.labjack.com/docs/kipling).  there is an Intel NUC in the Laser cabinet that has Kipling already installed, which you can access via Microsoft Remote Desktop at `laser-powermonitor.cp.lsst.org` (`139.229.168.143`). 

## Evaluation
Before shipping to Tucson, we measured the Reflectivity and Scattering properties of the Reflector. The average reflectance is about 80%, where fresh aluminum can have reflectance up to 91% on average. The higher levels of scattering are perhaps not suprising with the manufacturing of the optics

```{figure} reflectance_plot.png
:figclass: technote-wide-content

Measurement of the refletance and scattering properties of the Reflector while in Tucson. 
```

```{figure} reflectivity_drawing.png
:figclass: technote-wide-content

Location of the measurements from the plot above
```

The flatness of the optic, or rather it's consistency with the desired asphere defined above, was measured during and after manufacturing. These measurements were made using a Hexagon Laser Tracker. We carefully touched the surface of the Reflector with a 1-inch retro reflector to get these measurements. The plot below shows the results from measurements made in 2018 and then in 2023. They match quite well, although the measurement errors seem to increase in 2023. It shows that the shape of the milled aluminum piece follows that of the asphere, up to 10 microns, but possibly less than a micron based on the initial measurements.
```{figure} lasertracker_reflector.png
:figclass: technote-wide-content

Measurement of the Reflector relative to the definition of the asphere using the Laser Tracker
```


## Maintenance
The reflector cover actuators are exercised daily during the Daily CalSys Checkout. Monthly, the mirror should be inspected and possibly cleaned.
