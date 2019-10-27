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

# Firmware Upgrade
The printer comes with a repetier firmware v0.82. Nowadays, repetier is at v1.0.3. So while I was at the hotend upgrade I decided to update the firmware as well. The main reason was that I had to recompile anyway (because of the new thermistor included in the E3D v6).
