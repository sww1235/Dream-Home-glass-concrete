Pool
Pool is separate unit, on wheels
15*30 ft curved pool approx 5ft deep
6-8ft walk way around
6-8 ft off the ground
All 4 walls and floor made out of 4 inch acrylic
Use variable speed pump with simplest controller possible
3 possibilities for pump control
Simplest manufacturer specific control using relay inputs for speed selection (simplest)
Custom built H bridge controller (cheapest?)
Industrial motor controller with replacement motor (most reliable?)
Look at maintenance requirements of UV/ozone sanitizer vs UV/salt chlorine system. Does ozone system need chlorine system as well.
Look at automating analysis of pool water: ORP, pH, temp in several spots
Potentially use a sample method instead of a continuous method for pH
Look into spectrophotometric measurements for pH and ORP, potentially using sample and indicator method or continuous sampling method. Whatever has less maintenance requirements.
Test tubes- use valve to draw sample out of pipe after filter and after treatment plant into separate tubes
Dosing pumps to deliver indicator into tubes
Spectrometer used to measure color
Filter is sand filter, with pre screen filter
Steel support structure
On wheels. Potentially with self drive.
All equipment self contained except for makeup water supply and electricity.


Architecture/Detail Elements
Look at “The Witness” game for ideas about aesthetics w/ colored glass and lights.
Large panes of colored glass in window wall


Structural Modifications
Change size of atrium to 150’x300’. Think similar to arena.
Arena area has 10’ high glass airwalls in outside wall. Glass is super insulated. Also has a row of super insulated windows higher up in the wall. This is instead of wall o’ glass idea.
Maybe change size of server/utility basement to be a bit larger.
Extend hallways on upper floors with recessed catwalks out to end of atrium and doors on end of residential hallways.
Change size of residential area to 84’x42’ to allow for use of common material sizes and to reduce waste
Bedroom size is 12’x14’, with a 6’x6’ bathroom (sink, toilet, shower) and a 6’x6’ closet on the 12’ side. (Total size =12’x20’)
This results in a maximum of 14 bedrooms per floor due to (84*42)/(12*20)=14.7
change size of house to shrink down living area to 75’ wide, maybe smaller as well, maybe shrink depth as well.
add concrete anchors to main floor on new layer - use duplicate array tool.
http://www.strongtie.com/products/anchorsystems/mechanical/drop-in/productdata.html#dropin - concrete inserts
vectorworks tutorials http://archdraftingvectorworks.blogspot.com/?m=1
do some space planning of living space floors
If built on land with water access, then add boat house w/ wet/dry dock on side of house.
If built on land with high water table, then remove basement and move equipment to a sunken portion of the first floor. Also, look into just pouring a massive block of concrete and moving the whole house up on stilts or blocks, so the weight bearing capacity of the arena floor is not reduced. Add drains in concrete block.
If land does not have suitable slope for house embedding, then move penthouse and garage to ground floor.
If no slope but low water table, then bury house in ground a la earthships
Think about eliminating one floor of living space.
Think about shrinking down living space even more, width + depth but keep first floor connection


Where am I going to actually build this (land purchasing)
5 options really, Pacific northwest, Colorado, Minnesota, North East (maine, massachusetts, etc), gulf coast
Pacific Northwest
Access to water and boating. Plenty of potential waterfront property b/c seattle and islands
Has seasons + cold + snow
Lots of rain
grey
Colorado
Goldilocks climate
Sun!
No boating!
Skiing (not really a huge plus)
Mountains + Camping + backpacking
High school and college here - memories
Probably build in mountains- fire season + hunting
Minnesota
Worst climate, snow + mosquitos
Grey all winter
Memories - elementary school + family friends + birthplace
Cultural institutions are great
Boating access, on great loop route
North East
Similar to Pacific Northwest but harsher climate
Even more boating access in certain parts of the area
Not as much land available so prices are higher, plots are smaller
Grey and wet winters, mosquitos in summer
Gulf Coast
Hurricanes
Warm climate but rainy/foggy in certain parts of coast. Depends on latitude
Boating access fantastic, may have issues finding large parcels of land as latitude goes negative
Access to the Bahamas via boat


Landscaping
add landmass to house cad drawing + do landscaping https://techboard.vectorworks.net/ubbthreads.php?ubb=showflat&Number=186074
Try again due to greater amounts of ram


Electrical/Automation
add hardware debounce chips to user interface panel
add a reset chip for ethernet chip. Use ethernet shield R3 schematics - check if already implemented.
Reimplement circuits in KiCAD
finish routing circuit boards
might want to change the way the leds are wired to the shift registers due to the library needing a specific wiring layout
estimate nbr of smart light switches needed.
look at designing a touch screen controller as well.
learn more about web control of arduino.


Partition Wall Design
think about design for temp walls.
preliminary design is 2x4 walls with drywall and metal studs
most panels are 4’ wide x 8’ tall - some smaller ones for filling gaps and 2’ x 4’ ones for filling in up to the 10’ ceiling. May actually want to make 10’ tall versions for that purpose specifically.
2 standard versions, one with electrical and data outlets, and one without.
electrical and data outlets are fed up to the top and terminate with standard connectors. Electrical terminates with a system (similar to) the Hubbell Zone distributed electrical wiring system system for under floor wiring for flex space offices.
other wall coverings?
connection system? some sort of slot system with a central bar insert, maybe a cam system. need to integrate it into the sides of the wall sections so the seam is pretty much invisible. maybe just plan on having a seam and needing to tape and spackle it every time (figure out how much that would damage the drywall.) maybe another wall covering that is fire resistant but allows for more abuse i.e. pulling off seam tape and masking compound. Or just make the seams part of the wall decoration, ie hide them using visual tricks.
Need lifting points on top and bottom.
Frame needs to be strong enough to support entire wall from top or bottom


Todo for software projects
need to implement led control for push button controller - have both option to change directly when a push button is pressed, as well as polling the command and control server for updated status.
need to finish software for server side
need to write command and control software.
-needs to generate code for specific arduino client/server
to choose a function that a button will do
- select from list of servers
- then select from list of functions provided by server
- select led color to associate with the state change caused by the function.
-needs to interface with database to track various clients/servers and states.
has a table of clients/servers (mac address, static ip address, location, hostname, type)
has a table for each client/server that lists the states of inputs/outputs
track IP (if static addressing) and mac addresses and generate new ones for new devices if necessary
manage bootloader deployment
manage new device creation
manage tftp server with sketches and compile/upload/reset arduino clients and servers.
needs to respond to http requests from control clients with their specific status. format is 1 line, ‘\n’ ends response, under 100 chars.
