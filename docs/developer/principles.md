It is good to abide by some general programming principles when contributing to the MiSTer project. Keeping these good principles in mind will help you 

## Indent with tabs, not spaces

This may be a controversial subject, however there is good reason to indent with tabs instead in this instance. In general, indent with tabs, not spaces. As the project is uploaded to github, spaces are not handled that well by github in terms of diff compares, git blame, formatting, etc... Tabs are more compatible and will be easier for everyone to work with.

## Comment your code

It may take some extra time, but it saves everyone, including yourself, time in the long run. Make sure to be relatively thorough in commenting your code. For example, a good example of commented code from the Atari7800 core by Kitrinx, in [TIA.sv](https://github.com/MiSTer-devel/Atari7800_MiSTer/blob/cfcb2603d3f718268b5de8b7742798dd5fdbc605/rtl/TIA.sv#L786){target=_blank} starting at line 786:

```sv
module playfield
(
	input         clk,     // Master clock
	input         reset,   // System reset
	input logic   clkp,    // Pixel Clock
	input clock_t hclk,    // Horizontal clock phase 2
	input         reflect, // Control playfield, 1 makes right half mirror image
	input         cnt,     // center signal, high means right half
	input         rhb,     // Reset HBlank signal
	input [19:0]  pfc,     // Combined playfield registers
	output logic  pf       // Playfield graphics
);
```

When instantiating this module, Kitrinx added a comment to the end of all of her Inputs and Outputs. One shouldn't assume everyone else knows that `hclk` is `Horizontal clock phase 2` even if the name makes sense to yourself. Another good example of commenting code is to provide hyperlinks to reference material and describe in detail why you did something that isn't intuitive. Here's an example from the same file [TIA.sv](https://github.com/MiSTer-devel/Atari7800_MiSTer/blob/cfcb2603d3f718268b5de8b7742798dd5fdbc605/rtl/TIA.sv#L867){target=_blank} starting at line 867:

```sv
	// The reason for signal this centers around an analog delay of around 21ns which causes an
	// extra clock edge to form if the hmove counter is glitched into remaining on during non-hblank
	// clocks. This was discovered by Crispy and is available in this topic here:
	// https://atariage.com/forums/topic/261596-cosmic-ark-star-field-revisited/
```

Then if someone is wondering why this signal is so confusing and weird, that person can read the reference and not waste time investigating the potentially cryptic code in detail inefficiently, when the work has already been done for them long ago.

Labeling sections of code that can be grouped together with comments can also be very helpful to other devs looking to help contribute code, like in the NeoGeo core, [neogeo.sv line 589](https://github.com/MiSTer-devel/NeoGeo_MiSTer/blob/d260e115c07e11eddd66d47b99110e8d807c57bb/neogeo.sv#L589){target=_blank}:

```sv
// Graphics stuff
wire [23:0] PBUS;
wire [7:0] LO_ROM_DATA;
wire nPBUS_OUT_EN;
```

If you follow the link and look above, youc an see that this tiny comment helps differentiate between the z80 wires and the graphics wires in this section of the code. This allows developers to just ignore the irrelevant code above, and not even read it, since it's a waste of time to do so, most likely, if they want to just fix a graphics bug.


