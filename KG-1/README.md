# Samsung GX RGB Mod (Chassis KG-1)
### (GXE1395, etc)

<img src="https://user-images.githubusercontent.com/41927604/220997443-2e474486-9f2d-4723-8472-cfb9404142ba.jpg" width=600 />


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

There is some discourse online that lowering the inline resistors value will help with the video brightness. In my experience with reducing it to a 1k Ohm resistor, the video quality stayed the same, but the OSD was barely visible. For this reason I recommend using the stock 3.9k Ohm.

### Video lines:

| Stock OSD Video Circuit | RGB Mod with no diodes on video lines | RGB Mod with diodes on video lines |
|---|---|---|
| <img src="https://user-images.githubusercontent.com/41927604/220828059-deafe6e0-40ba-42ce-857c-10e34435e4eb.jpg" width=400 /> | <img src="https://user-images.githubusercontent.com/41927604/220828227-b56e5a78-aa9f-41d4-8200-63b81405d5e7.jpg" width=400 /> | <img src="https://user-images.githubusercontent.com/41927604/220828538-e4e19ef1-278b-4874-a95d-23515fdbaccf.jpg" width=400 /> |

### Blanking line:

| Stock OSD Blanking circuit | External Blanking Mod |
|---|---|
|<img src="https://user-images.githubusercontent.com/41927604/220828168-74032190-1e10-49ec-a7c9-af522c035b13.jpg" width=400 />|<img src="https://user-images.githubusercontent.com/41927604/220828701-04059627-d5ce-4cc9-baac-0a253bda3a10.jpg" width=400 />|

### Note
We came up with the 560 Ohm value through the following calculation:

<img src="https://user-images.githubusercontent.com/41927604/220768772-27fb691a-f2d7-45d0-9f61-729408e0a467.png" width=500 />

If you choose to use diodes, you can instead use a 680 Ohm resistor:

<img src="https://user-images.githubusercontent.com/41927604/220768921-c24301c1-f9e4-4cf4-9ff5-3a016d8bd0c5.png" width=500 />

Blanking calculations are below: 

<img src="https://user-images.githubusercontent.com/41927604/220781839-a1bf47bd-b9d8-478b-b294-00c96f85b5d3.png" width=500 />


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

8. Cut necessary holes in the back housing to fit your connectors. 

### Note

The subwoofer on this TV takes up large channels to the left and right of the neckboard. Also, the space to the left of the AV inputs is either very close to heatsinks, resulting in no room for connectors, or directly next to the flyback transformer, which can interfere with your signals. [See here for a demonstration on the effect of the FBT when the SCART port is too close](https://imgur.com/a/o7InOs2)

With these in mind, I found the best place for my SCART port to be directly under the neckboard. This isn't the prettiest spot, but it ended up having no negative effect on my signals, and did not interfere with the subwoofer's housing.

<img src="https://user-images.githubusercontent.com/41927604/220791367-2b9ea47f-1a7a-4f1c-94a4-576b5eda04ee.jpg" width=300 /> <img src="https://user-images.githubusercontent.com/41927604/220791432-3cc6863d-8365-4ac6-8be5-ad2149cbb80c.jpg" width=400 /> <img src="https://user-images.githubusercontent.com/41927604/221000079-f0ed4a35-57a2-44e4-973a-a583632bceb6.jpg" width=300 />


## Read This!

Once you have connected everything and it's working, you may notice a couple things:

1. The RGB input will likely look too bright/washed out. Even though our signal is 0.7V, it seems these Samsungs display the analog RGB quite bright. The fix for this is to reduce the screen voltage a tad. Using a small philips screwdriver, reduce the "Screen" potentiometer which is located on the back of the flyback transformer. A small reduction will result in a perfect balance of colors in RGB. Note, this will reduce the brightness of the composite input. You can increase the default menu's Brightness and Picture settings to compensate for this, because the RGB bypasses them anyway.
2. Like all RGB mods, the screen will be shifted to the left a little bit due to us passing sync through the composite input. To fix this, you can use the service menu to increase the HS (Horizontal Shift) value. To access the service menu, turn the TV off, and hit Mute -> 1 -> 8 -> 2 -> Power on the remote in quick succession. 
3. If using SCART, you will find that the audio is mono. You can fix this by plugging in a dummy RCA cable to the Right audio jack of the AV inputs. This signals the set to use stereo audio. (You can make a permanent change by closing this circuit under the board, but doing it this way allows you to still use mono audio signals if you want, such as from an NES.)


## Results

<img src="https://user-images.githubusercontent.com/41927604/220997645-248ebcdb-785f-4de8-b7ff-e4520761cc80.jpg" width=500 /> <img src="https://user-images.githubusercontent.com/41927604/220997775-44966f6e-0a0d-40bf-a635-9255c55efe88.jpg" width=500 />

<img src="https://user-images.githubusercontent.com/41927604/220997961-5e86b3bd-eac2-4169-975e-a4031ada6848.jpg" width=500 /> <img src="https://user-images.githubusercontent.com/41927604/220997998-4de27121-480d-4937-86c0-d3ebd1bf1685.jpg" width=500 />

<img src="https://user-images.githubusercontent.com/41927604/220998194-a10a4283-d908-4bf7-8462-95129af923e6.jpg" width=500 /> <img src="https://user-images.githubusercontent.com/41927604/220998213-f4a7c0b1-4b64-449d-8e2d-44e928c7e2db.jpg" width=500 />

## Notes, Tips, and Tricks

1. This TV is equipped with AV out jacks, which mirror the composite video and audio left and right channels. Some folks have used these jacks as their red, green, and blue inputs. To do this, you would need to cut the traces on the board to these pins, and inject your RGB lines to the pins inplace. You would then plug sync into the composite RCA jack as well as the existing audio L and R jacks.
2. From what I can tell, GX mode on the front controls and remote seems to combine audio channels a bit. All I really found is that it reduces the amount of stereo separation in the audio. For this reason, I recommend not using GX mode (aka using AV mode). 
3. I have not had any interference issues with this set when using high quality cables. However, in the pursuit of clean video signals, you can always opt to use inline diodes on the RGB lines as I mentioned above. For more info on reducing interference, see [Sunthar's guide here](https://sector.sunthar.com/guides/crt-rgb-mod/noise-and-bars.html)

## Sources and Further Readings

* [Shmups RGB mod thread](https://shmups.system11.org/viewtopic.php?p=1342960)
* [MarkOZLAD's Samsung RGB mod guide](https://shmups.system11.org/viewtopic.php?f=6&t=63425&p=1338231#p1338231)
