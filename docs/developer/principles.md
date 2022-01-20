It is good to abide by some general programming principles when contributing to the MiSTer project. Keeping these good principles in mind will help you 

## Indent with tabs, not spaces

This may be a controversial subject, however there is good reason to indent with tabs instead in this instance. In general, indent with tabs, not spaces. As the project is uploaded to github, spaces are not handled that well by github in terms of diff compares, git blame, formatting, etc... Tabs are more compatible and will be easier for everyone to work with.

## Comment your code

It may take some extra time, but it saves everyone, including yourself, time in the long run. Make sure to be relatively thorough in commenting your code. For example, a good example of commented code from the Atari7800 core in [TIA.sv](https://github.com/MiSTer-devel/Atari7800_MiSTer/blob/cfcb2603d3f718268b5de8b7742798dd5fdbc605/rtl/TIA.sv#L786){target=_blank} starting at line 786:

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

When instantiating this module, this dev added a comment to the end of all of her Inputs and Outputs. One shouldn't assume everyone else knows that `hclk` is `Horizontal clock phase 2` even if the name makes sense to yourself. Other good examples of good comments are separating sections of assignments or port instantiations by category, or explaining the "Why" behind a particularly unintuitive section of code.


