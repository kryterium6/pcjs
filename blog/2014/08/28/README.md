Supporting the 80286
---
The next milestone for PCjs is complete 80286 emulation.  My hope is to have it working by the end of the year.

PCjs version 1.15.0 is the first step on the path to full 80286 support.  It includes changes to the physical
memory manager and separate real-mode and protected-mode address evaluators.  The Debugger supports physical
addresses (eg, %FE05B is the same as F000:E05B, assuming real-mode operation), along with breakpoint commands that
stop execution on port input/output operations.  And the ChipSet component now contains "infrastructure" (a
fancy way of saying "partial support") for multiple PICs, DMA controllers, the 8042 keyboard controller (including
A20 support), and a bit more -- but not much.

One of the challenges is creating a single "universal" version of PCjs that can adapt itself to different machine
types without impacting performance.  There will not be a **pc8088.js** or a **pc80286.js** or whatever.  There will
only be **pc.js**.

Up until now, all PCjs machine XML files assumed an 8088 CPU with a 20-bit bus and a model 5150 or 5160 motherboard.
But now, a machine XML file can specify:

	<computer name="IBM PC AT" buswidth="24"/>
    <cpu model="80286"/>
    <chipset model="5170"/>
	...
	
Conventional emulators are usually NOT able to run original BIOS images, or simulate original PC hardware,
or even run at the same speed as the original PC, making some software difficult or impossible to use.  PCjs takes a
different approach, by attempting to simulate an entire PC as it originally existed.  Which is why a PCjs simulation
of an IBM PC does NOT run at whatever speed your modern PC happens to run in V86-mode or whatever speed your
browser's JavaScript engine tops out at.

No, a PCjs simulation of a 4.77Mhz IBM PC runs at 4.77Mhz.  And a PCjs simulation of a 6Mhz IBM PC AT will run at
6Mhz.  If you want to run the simulation faster, you have that option, but that's not the default.  And I'm not saying
that PCjs is *exact* -- exactness is an exercise I'm leaving for another day and/or to other developers who are even
more obsessive than I am.  I'm just saying that original PCs represent the targets that PCjs is shooting for.

PCjs 1.15.0 can now load and run the IBM 5170 ROM BIOS up to the first 80286-specific opcode, so it's off and running.
Although "running" isn't quite the right metaphor, because the process of bringing a new machine simulation to
completion is a *very* long series of baby steps.

Also, in preparation for this new phase, I recently dug up a variety of old [80286 CPU Documentation](/pubs/pc/reference/intel/80286/)
and posted excerpts.  I'm sure none of this information is "new" at this point, but it might have some historical interest.

Enjoy.
 
*[@jeffpar](http://twitter.com/jeffpar)*  
*August 28, 2014*