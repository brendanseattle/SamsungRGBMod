# Samsung KG-1 RGB Mod
### (GXE-1395, etc)


<img src="https://user-images.githubusercontent.com/41927604/220743506-b7152c7e-c2c3-4ae7-84ff-f4fe36de7ed9.jpg" width="600" />


RGB Mod for Samsung KG-1 CRT televisions.

Written by Brendan Eddy (FlyingFlygon). Credits to:
* MarkOZLAD for method and diagrams
* Syntax for method

## Overview

This mod is a standard RGB mux mod for televisions with separate micom and Y/C jungle chips. We will inject our external RGB signal into the TV's On Screen Display (OSD) video circuit. We will utilize the set's existing composite video line for our external sync. And we will switch to our external RGB signal by sending a 5V signal to the OSD blanking circuit.

Contrary to popular belief, this mod is NOT the same as [The 8-Bit Guy's Samsung RGB mod](https://www.youtube.com/watch?v=DLz6pgvsZ_I). That set is a Samsung TXD-1372 with chassis K-1. The board layout, component labels, resistor values, and chassis are ALL different than this Samsung GX! The mod is very similar nonetheless, but I want to dispel that rumor officially. 

See following diagram for an overview of what the OSD RGB Mux circuit looks like. (Note these chip names and pins are specific to the Sanyo set. Can be ignored for the purposes of this guide)

<img src="https://user-images.githubusercontent.com/41927604/166302867-327fab37-5817-43e2-9fba-3f42af5b9b40.png" width="600" />

##### Credit to Syntax and MarkOZLAD


## Components Needed

I will be detailing the mod using a SCART connector. You can instead choose a BNC/RCA jacks and an external 5V switch. I will point out where changes need to be made if you choose that route.

For this mod you will need:
* Properly shielded wires (I chose 20AWG silicone wire)
* 1 1N4148 diode
* 3 560 Ohm inline resistors
* 3 75 Ohm inline resistors
* External input connectors: your choice of a SCART female port, or 4 BNC female jacks (or use existing RCA jacks, see Notes section)
* Nice to have: male cut RCA plug for enabling stereo audio


## Plan and Diagrams

This mux mod is quite simple as the inline resistors are a good value to keep the OSD visible while including our external RGB signal. We should not replace these inline resistors, instead we use them directly. 

### Stock OSD video circuit:

< INSERT PIC HERE >

### RGB lines with no diodes (the implementation I chose):

< INSERT PIC HERE >

### RGB lines with diodes (could help reduce interference):

< INSERT PIC HERE >

### Blanking

< INSERT PIC HERE >

### Note
We came up with the 560 Ohm value through the following calculation:

<img src="https://user-images.githubusercontent.com/41927604/220768772-27fb691a-f2d7-45d0-9f61-729408e0a467.png" width=500 />

If you choose to use diodes, you can instead use a 680 Ohm resistor:

<img src="https://user-images.githubusercontent.com/41927604/220768921-c24301c1-f9e4-4cf4-9ff5-3a016d8bd0c5.png" width=500 />


## Modification Steps

1. Remove the grounding resistors on the RGB lines: R944, R945, and R946
<img src="https://user-images.githubusercontent.com/41927604/220769576-20058d2b-778a-4ed1-b205-17c86059d0a8.jpg" width=300 />

2. Place jumper wire on resistor R948 to jump it to ground, disabling the closed caption display circuit. This circuit is known to dim the image. See [MarkOZLAD's Samsung RGB mod guide](https://shmups.system11.org/viewtopic.php?f=6&t=63425&p=1338231#p1338231) for more info.
<img src="https://user-images.githubusercontent.com/41927604/220771492-5b87d2a2-c7b3-46b3-9d99-a8a85d46bd23.jpg" width=500 />

3. Remove jumper wire J104 which is located right off the composite input AV1. If you do not do this step, the mod can still work, but you will have an OSD message overlay which states "Connect the AV1 jacks". Once this jumper is removed, that check is disabled and the message goes away.
<img src="https://user-images.githubusercontent.com/41927604/220771207-de021c2a-4e79-4d3a-933c-ed9d86dad4d9.jpg" width=400 />

4. Desolder the leg of resistor R918 that's on the side near the Micom chip. Insert the cathode end of a 1N4148 diode in its place. Solder the remaining legs of the diode and R918 together. 
<img src="https://user-images.githubusercontent.com/41927604/220772991-4f8cba79-4992-4f97-b221-62ac76f86776.jpg" width=500 />

5. Connect your RGB and blanking wires to the board. 
- 5V Blanking goes in between the diode and R918 (see pic above)
- Red, green, and blue go to the EXITING end of resistors R941, R942, R943 respectively. 
<img src="https://user-images.githubusercontent.com/41927604/220773624-30d379ed-e951-419b-9226-bb78a758b761.jpg" width=500 />

6. Connect your ground, composite (sync) and (if using SCART) audio wires to the board. All of these can be obtained directly from the pins on AV1 like so:
<img src="https://user-images.githubusercontent.com/41927604/220775309-83d883dd-388d-45ec-bf21-887e5e9ccce3.jpg" width=700 />

7. Prepare your SCART/BNC connectors. Inline resistors are 560 Ohms. Terminating resistors are 75 Ohms. Make sure grounds are connected. My implementation uses SCART:

<img src="https://user-images.githubusercontent.com/41927604/220775943-9c7145ae-bd40-4531-bb32-a7271725b6ba.jpg" width=300/> <img src="https://user-images.githubusercontent.com/41927604/220775997-83d248c0-c2b5-4622-b7a5-18518732cf72.jpg" width=300 /> <img src="https://user-images.githubusercontent.com/41927604/220776044-4492f19a-40af-4086-84c9-54ca0b170f9b.jpeg" width=300 />

## Considerations

Once you have connected everything and it's working, you may notice a couple things:

1. The RGB input will likely look too bright/washed out. Even though our signal is 0.7V, it seems these Samsungs display the analog RGB quite bright. The fix for this is to reduce the screen voltage a tad. Using a small philips screwdriver, reduce the "Screen" potentiometer which is located on the back of the flyback transformer. A small reduction will result in a perfect balance of colors in RGB. Note, this will reduce the brightness of the composite input. You can increase the default menu's Brightness and Picture settings to compensate for this, because the RGB bypasses them anyway.
2. 


## Notes, Tips, and Tricks


## Sources and Further Readings

* [Shmups RGB mod thread](https://shmups.system11.org/viewtopic.php?p=1342960)
