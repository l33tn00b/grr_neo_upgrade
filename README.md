# grr_neo_upgrade
Upgrading the German RepRap (GRR) Neo to be a useable printer

I've been using a German RepRap Neo 3D Printer for quite a while now.
But it has somehow always left me wanting. Oozing was terrible, precision wasn't really superb. Speed sucked. But why? The mechanics are not quite rock solid but very decent. It has a metal frame and a z-axis spindle. On the other hand there are some design choices that are at best questionable. T3 pulleys and belts? The DD2 extruder, directly fixed to the extruder's stepper motor (good luck with the threads, the spring load gets fed into these with hilariously short screws). No cooling fan. 

I bought the printer at a discount. It had been used as a display/demonstration unit at a local electronics market (think Best Buy). Actually, I can't remember the date, it must have been around 2015/2016. 

I feel a bit sad about the fact that German RepRap abandoned the printer. There still is a repetier firmware available on GitHub. But the last changes are from four years ago: https://github.com/GermanRepRap/Repetier-Firmware 

# Active Cooling
Pretty much a month after having bought it. That greatly improved long/thin prints.
See https://www.thingiverse.com/thing:646029

# Hotend Upgrade
The stock hotend is one of the main reasons why prints are crappy. I learned a great deal declogging it. Filament tends to get stuck because of a bad/non-existing heat break. So the filament melts up in the PTFE tube. Now, I have an E3D V6. 
See https://www.thingiverse.com/thing:971035 for the mounting parts.
Hotend assembly is at https://e3d-online.dozuki.com/Guide/V6+Assembly/6?lang=en.
You will have to shorten the belts to fit these into Kakadu's hotend mount. This is not a problem since you'll never want to return to the stock hotend.
Issues on the way were:
* Fitting the new cables (thicker heater cartridge supply cables) into the cable guide.
* The E3D's nozzle is slightly higher than the stock nozzle. Printing on 3mm glass, now. The additional half (or so) millimetre makes up for that.
* The Y-Endstop needs to be moved to the right. This is due to the new carriage being a bit wider. Keep the screw in its slightly rotated position towards the back of the printer. Else the carriage will collide with it but not trigger the endstop.

# Firmware Upgrade
The printer comes with a repetier firmware v0.82. Nowadays, repetier is at v1.0.3. So while I was at the hotend upgrade I decided to update the firmware as well. The main reason was that I had to recompile anyway (because of the new thermistor included in the E3D v6).
Don't be fooled by E3D's "this is easy". I had to update the bootloader as well. Assuming that you already have the Arduino IDE installed and that you're in possession of a programmer...
## Firmware compilation
1) get and install teensyduino
2) compile repetier firmware for teensy++2.0 in arduino ide
3) export hex file (will be written to your sourcecode directory) (DON'T FORGET THIS AFTER CHANGING configuration.h !)
## Booloader Upgrade
1) get hid bootloader from http://blog.lincomatic.com/?p=548
2) get ready for programming (I'm using a JTAGICE3)
3) flash bootloader 
4) when done, you should see a message in the lower right corner of the screen indicating a successful installation of a HID input device :)
5) flash newly compiled firmware (assuming the firmware file is in a subfolder called "Repetier"): hid_bootloader_cli -mmcu=at90usb1286 .\Repetier\Repetier.ino.TEENSY2PP.hex (don't forget to set and remove the BOOT jumper)

See files for the configuration with the E3D v6 hotend. There also is a compiled image.
After removing the printer's back side for the nth time I decided it was time for a boot jumper extension dangling at the side. Makes firmware upgrades/changes much easier.

# Lighting
There's nothing to see, here... literally. Without additional lighting it's pretty hard to see what is going on inside the printer. The main contributing factor surely is the solid side/rear walls. So I got a cheap 12V LED stripe from aliexpress (https://www.aliexpress.com/item/32333870936.html?spm=a2g0s.9042311.0.0.27424c4dBqQZxE), cut it to size and mounted it above the front opening on 3D-printed 45° mounts. 

# Extruder Upgrade
As previously stated: The extruder is an utter piece of cr.p. To fix this, I've added a Bondtech BMG extruder. It is driven by a Trinamic stepper. There is an adapter on Thingiverse: https://www.thingiverse.com/thing:3010010
Catch is: The holes for mounting the extruder adapter do not fit the holes on Kakadu's Hotend mount. So you either do the entire thing at once with Mechanotronikum's files (including his Hotend Mount). Or you take the modified parts I'm providing here (https://github.com/l33tn00b/grr_neo_upgrade/blob/master/adapter_loecher_angepasst.stl).

# Various Fixes
## Printrboard Rev D
Duh. Someone please adjust the (lead free?!?) reflow solder process parameters. I've always had that strange feeling with the Micro USB jack. Guess what? It came off today. Rock solid contact for the tabs connecting +-Signal/GND/+5V. Not so much for the chassis of the jack. Luckily, only the Sense Pin's trace came off the PCB. That one wasn't connected anyway. So I spent the better half of the evening looking for my bag of USB connectors. Finally found them and soldered a new SMT USB jack onto the board. Lead, please. Somehow, I have a feeling of knowing why I usually choose through-hole USB connectors. Even when using SMT connectors, there are some that provide two little tabs that go into holes on the PCB. Much better transfer of mechanical loads when plugging/unplugging. The jack probably held such a long time only because of not being used very often: GRR's Neo uses an old-fashioned USB B type connector that is internally wired to the Micro USB jack. 

# To Do
* Adjustable Z axis end switch. The stock one is calibrated to a printing bed height that is based on 2mm PMMA plus BuildTak. I now print on glass which fits nicely with the E3D V6's slightly higher nozzle..
* Heated Bed (parts are here) to prevent warping when printing on glass. Plus finally printing material other than PLA.
* Replace Printrboard (Duet3D WiFi is on its way).
* Replace T3 belts and pulleys with standard T2.5 (distant future. Parts are here, though).
