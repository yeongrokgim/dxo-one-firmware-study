# dxo-one-firmware-study
experimental study to extend lifespan of DxO One camera

# Introduction
As of July 2019, DxO One, is still awesome. But it has discontinued more than a year ago.
https://www.digitaltrends.com/photography/dxo-one-discontinued/
There is a official website of open-source oriented project exist, but it seems inactive.
https://openone.dxo.com/
As openone project is not serving any resources, I tried some stuff.

# Materials Used
1) DxO One (iOS connector)
2) 4GB microSD card
3) iFixit Jimmy ( https://ko.ifixit.com/Store/Tools/Jimmy/IF145-259 )
4) Ubuntu VM
5) Firmware file (DXOCARD_3.2.0.ecef5ef809.BIN, MD5 : 2e6ee13da79cc8963cacb2854281a2fb, can be extractred during firmware update process on iOS App; or ask DxO to get one)

# References before doing something
1) it seems DxO One has Ambarella A9 series SoC
https://www.goprawn.com/forum/ambarella-cams/14041-dxo-one-ambarella-a9s35-sony-imx183
2) GoPro Hero (=<5) series has Ambarella SoCs too, and custom scripts are available, known as autoexec.ash
2-1) Ambarella SoC works as a two seperated parts; RTOS(ThreadX) and a Linux system to support wifi and more

# Hardware side
1) Looking for a debug pin
To open this, you have to poke wide and thin blade between black and silver gaps, the enclonsure hold each other with clap-on latch. Keep spudger above silver part and below black part.
I hoped I could found debug pins on PCBs, but I couldnt' find any.
2) I could name IC partnames after opening up metal shield.
ADAU 13828CPZ (audio codec?)
SPANSION ML04G200BH100 (NAND storage, guess only stores Linux systems)
SAMSUNG K4P8G304E0-AGC2 (DRAM)
Ambarella A9-A1-RH S1433 N93WA-D ANM1N1 A9S35 (SoC)

# Software side
1) binwalk couldn't extract partitions.
2) fwparster in gopro-fw-tools ( https://github.com/evilwombat/gopro-fw-tools ) seperated firmware file to 5 sections (0 - 4)
2-1) ubi_reader ( https://github.com/jrspruitt/ubi_reader ) extracted internal Linux partiton from section_4
2-2) Linux system has limited features, mainly to support Wi-Fi connection between smartphone and DxO One
2-3) modifying filesystem and repack, then upload to device will allow you to connect camera, but I didn't tried.
3) run 'strings' to get some clues inside firmware files worked, many potential commands and device-specfic commands in RTOS found.

# autoexec.ash side
1) if there is a file named 'autoexec.ash' exists, RTOS tries to run this script on built-in shell (known as AmbaShell)
2) as we have no screen or uart output, we have to redirect them.
3) in AmbaShell, storage management is dos-like. c:\ is your SDcard root, a:\ and b:\ are where internal data stored (possibly device-specific calibration files?)
4) you can write commands in autoexec.ash, but you may want to redirect output to file like this : help > c:\help.log
4-1) it doesn't work with 't dxo something' commands; it requires different approach; write 't dxo console 8' to autoexec.ash to redirect all output to sdcard:\console_debut.txt



