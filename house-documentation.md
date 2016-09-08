# House Documentation

## Definitions

HA = home automation
(protocol) = insert best communications protocol here.
environmental sensors= all or some of the following: temp, humidity, CO2, CO, motion, light, noise, other gasses
DWV = Drain Waste Vent
DHW = Domestic Hot Water
DCW = Domestic Cold Water
ZCU = Zone Coil Unit
Home Automation / Electronics
all light switches are custom 8 button panels with RGB leds behind them. They use an arduino micro/nano or maybe something else to do local processing. This interfaces with the LEDS and the switches, and also communicates with the rest of the HA network via (protocol). they also have an external contact or two for mechanical SPDT center return switches to turn on basic illumination in the room. they are powered and communicate via ethernet and POE.

Physically they are based on an arduino nano with 1 shield. An additional circuit board is the “User Interface” that has the LEDS and switches on it as well as the switch registers for the LEDS and debounce and mux for the keys

http://www.leviton.com/OA_HTML/ProductDetail.jsp?partnumber=5657-2W&section=47084&minisite=10251 - external SPDT center return switch - decora

http://www.maximintegrated.com/en/products/interface/protection-and-isolation/MAX6818.html - debounce hardware chip

http://www.elcojacobs.com/using-shiftpwm-to-control-rgb-leds-with-arduino/ - another shift register

They are on their own separate VLAN and subnet, and use static IP addressing. The main control program will generate an IP and MAC address for each ardino. The switches have localized code on them so that they do not have to have a server intervening in requests to turn lights on and off, they know what action pressing each button should have and will communicate that. They also can have prebuilt states for the LEDS that are triggered as the buttons are pressed. IE the light is turned on, the LED changes to green. when you press a button on a switch, the local code runs and figures out what actions it needs to run. These actions are both sent directly to the affected device and the management server. Probably through some Protocol built on ethernet and TCP/IP maybe m2m. other things that could be integrated into these switches are environmental sensors such as temp/humidity/motion/an IR receiver. They can also be programmed over the wire, and there also can be a demo mode for the LEDS. Integrate demo mode with DMX somehow. pages of buttons.

all arduinos have some version of a tftp bootloader that enables uploading of sketches over the network. See Here for more details.

basically each input/control device knows its location and has a location specific program running on it. this program will communicate directly with the output devices as well as informing the master controller/database of status changes.

Certain tables in the database are archived either on update or on a timer such as temp

output devices receive these commands but also are monitoring the status of their output and inform the server

each room has several different clusters of environmental sensors in it, also have speakers and mic(s).


each room has at least one touch screen which is used to control and display temperature, and for some simple media controls. Also enables advanced control of the lights in the room.
Program Descriptions/Pseudo code for HA
Code Repository
there is a main console program that helps manage all aspects of the home automation system. Primary features are listed below. Built in C++
provides an overview and status page of all HA devices on the network
manages adding new devices to the HA network.
manages existing devices on the network
allows for remote uploading of code to the arduinos on the network.
provides a front end to the database
has the ability to send commands similar to those the arduinos send from a gui
When opened program appears like a standard gui program. default screen is the overview screen which shows a gui representing all the devices on the network which is detected by pinging the device. Some ideas for how to represent the status of each device: simulated LEDS, list with red and green background. Also has the ability to show the last response from the ping command.
to change the functionality of a button on a light switch, we need to upload a modified sketch to the arduino using tftp.
pull existing sketch file and read it to determine existing configuration
load existing configuration into change gui
(user edits configuration)
regenerate sketch file and save as a different version in an archive.
use arduino command line tools to build the binary file
upload file to tftp server
send a reset packet to the specific arduino’s IP grabbed from database or existing config file.
arduino will reboot and grab new file off of tftp server and flash itself.


Steps for setting up a new device on the network
change the bootloader on all new arduinos to be a tftp compatible bootloader which uses the proper IP and MAC addresses as generated by the program. (may need two reboots to have the IP and MAC addresses stored properly in the EEPROM)
set its location
tell it what to control
generate new sketch and compile it
upload file to tftp server
install arduino in location
reset it manually so it gets its sketch over the network
test to make sure both network reset and buttons are doing what they are supposed to.


HVAC/Water

HVAC system is designed to take advantage of all sources of heating and chilling. Implement thermal storage for both hot and cold.

Primary heat sources are ground or pond source heat pumps and solar hot water panels with a variable capacity electric instant water heater as a backup. Secondary sources will be heat recovery from server farm and other computers/industrial equipment as well as ventilation equipment and excess heat off of chilled water loop.

Primary chilling capacity will be from the ground or pond source heat pumps as well as industrial chillers with vfds. Make ice at night to reduce energy consumption. Dump excess heat into heating thermal storage.

At least two heat pumps, because they cannot heat and cool at the same time.

Each individual subspace (see planning worksheet) will have separate HVAC provided by a mixture of ZCUs and radiant heating depending on the needs of the space. Ventilation will be provided by a central ventilation system that each subspace is attached to.

see HVAC drawing for more information



Ventilation is accomplished using ERVs and HRVs in multiple different zones. Or one big ventilation system in the building core depending on


Electrical
Main power feeds are at medium distribution voltage that is transformed down to 600V or 480V for the main distribution panels.
There is a mostly separate emergency distribution system for electricity. I have large generator hookups on the side of the house which can be interconnected into either the emergency power distribution network or the main network. The emergency network runs e-lighting and special circuits for fridge and freezer. The idea is that most loads are switchable to reduce power consumption either during an emergency or to reduce peak load. I also have manual transfer switches that can interconnect the main grid with my solar system, and my emergency generators if needed. Mostly the solar system is connected via grid synced inverters like normal.
On floor 3M there are 3 120/208V 3 phase company switches and 1 277/480V company switch. Also there is an emergency panel there as well.
on the rest of the maintenance floors there are 1 120/208V company switch.
Hanging 2 circuit 120V 20A cable reels are mounted under above the catwalk level on a evenly spaced grid. grid spacing is 25 ft in both directions, so 10 reels total.
 Courtesy outlets around catwalk are on 10/circuit strings. spacing? Have marked faceplates designating them as courtesy outlets only.
All outlets are colored in relation to what phase they are on. Emergency outlets have red anodized wall plates and are hospital grade.
There are LED lights in the sides of the catwalks to illuminate the walking surface. (“Aisle Lights”) These are hard wired to a dimmer relay box near all the main power panels on 3M. These are LED string rope lights.
Also there are light posts along the catwalks that are for worklight. These are moisture proof hazardous location fixtures that are designed to mount on top of a pole. Spacing?
All other power in the catwalks is going to be fed as temporary power from the power distro panels.
There are big High Bay LED lights mounted under the catwalks to provide general work light for big projects. (calculated 300 lux at 2.5m from floor) More info Here
electrical panels
http://ecmweb.com/code-basics/dwelling-unit-calculations
Other power feeds as appropriate for mobile subspaces.

Structure
From top to bottom in 10’ increments except where noted (numbers in parentheses are elevator floors. *M floors are accessed via prox card and their corresponding button.):
floor above ground is inside the roof. Contains garage, loading dock and entry. ceiling is 10’ high at midpoint. Penthouse(PH)
under that is 13’ of maintenance/utility space. Extra 3’ of space comes from the loading dock. (3M)
third floor (3)
maintenance space (2M)
second floor (2)
maintenance space (1M)
first floor. (15’)This is where the atrium ends (1)
15’ maintenance space. bsmt level. houses data center, storage tanks for grey water reclamation system, main electrical distribution panel and HVAC equipment. Data center and electrical distribution room are isolated from HVAC and grey water tanks by a heavy concrete wall with moisture barrier and bulkhead door to help prevent flooding of the data center. (B)
Sloped roof faces south for solar panels. Has large overhang to help prevent solar heating in summer
House is buried in hill to get extra thermal mass and the walls touching dirt are made of Insulated Concrete Forms.  Other walls are made of glass with high solar heat gain coefficient for passive solar heating. Extend roof into large overhang to reduce solar gain in summer.
loading dock has heated surface. loading dock sections can lower into ramps. There is a slanted roof with heating coils to protect the loading dock.
elevator is designed for the maximum of a:
midsize truck
forklift with full pallet
humans
for safety, dimensions and load rating.
has 1 door at all floors.
elevator doors are 12’ wide by 9’ high. Cab width is  18’. Final interior dimensions will be 10’x18’x12’ (HxWxD).
Elevator has wifi access point and IP camera inside as well as IP contactless smart card reader. Also has utility outlets and maybe outlet for forklift charger
Floor 1 has 1.5" threaded inserts spaced 18" apart on center.
Glass wall faces south, so driveway approaches from north.
Floor 3M has catwalks over the atrium, but they are about 5’ above the floor level so to give as much headroom as possible while still being as far off the ground as possible. Floor of catwalks is expanded mesh.

Site
List of qualities for the site in order of importance
Large ( like 40+ Acres)
Sloped enough for walk out basement facing south (or dry enough to bury house)
Wooded
Has electricity hookups
Has sewer and water hookups (or capacity for well and septic or allows rain water capture)
Within 15-30 minute driving distance of lumber yard and hardware store
Has old buildings on it / is a previously used site to help qualify for more leed credit
Is close to a rail spur

Plumbing
all non DWV plumbing is done using pex.
sewage stacks are in mechanical column in the center.
Design amount of sewage stacks to handle 3x projected load.
Since I will be using reclaimed greywater to flush toilets and water gardens, there will be additional separate DWV stacks for sinks and showers.
all sinks except laundry sink and food prep sinks will go into grey water system.
main sewage stacks will run east and west under the primary hallway on each floor. In addition have a provision for an additional run directly north off of the sewage stacks.
on each floor, provide a 4” Hose connection to the sewage stack to connect temporary items.
in each location where DHW is needed, install an appropriately sized instant hot water heater to feed local fixtures. Or use a heat exchange coil connected to central heated water supply
cold water is run using 1.5” pex or pvc straight up to top floor. At each floor including maintenance floors there is a pex distribution board to feed fixtures on this floor. has ¾” outputs that are converted into ½” outputs to save on tubing costs. (check sizing)
also have the 2 loops for house heating and cooling, as well as equipment cooling (see HVAC for more information).
use purple pex for gray water to toilets. - use large enough tanks, supply line and pumps to allow use of flushometer valves.
2 trench floor drains in floor of kitchen area.
trench drain around perimeter of atrium.

Interior Design



Resources

Desert Home Blog - Home automation, energy savings, swimming pool stuff, rasberry pi stuff, xbee, house clock.

VT Passive House Blog - passivhaus related stuff

Carnation Construction - ICF house. Interesting ideas about construction of concrete house. Provides some good resources for structural design aspects and plumbing. Some electrical stuff is cuckoo but most info is at least part ways right. (non metal rebar)
