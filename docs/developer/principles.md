Here's some tips and guidelines when contributing to the MiSTer project.

## Indent with tabs, not spaces

This may be a controversial subject to some, however there is good reason to indent with tabs instead of spaces in this instance. The project is uploaded to github and spaces are not handled that well by github in terms of diff compares, git blame, formatting, etc... Tabs are more compatible and will be easier for everyone to work with.

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

## Align ends, assignments, and proper indentation

Try to keep similar elements in our code aligned for readability purposes, for example, in the [EEPROM_24C0x.sv](https://github.com/MiSTer-devel/NES_MiSTer/blob/8dddb6cc01a2a2854a444838e0cfe5a17338060f/rtl/EEPROM_24C0x.sv){target=_blank} file from NES_MiSTer, this:

```sv
// savestate
assign SS_MAP1_BACK[ 2: 0] = (state == STATE_STANDBY)  ? 3'd0 :
							 (state == STATE_TEST)     ? 3'd1 :
							 (state == STATE_ADDRESS)  ? 3'd2 :
							 (state == STATE_WRITE)    ? 3'd3 :
														 3'd4;
```

...is a lot easier to read than this:

```sv
assign SS_MAP1_BACK[ 2: 0] = (state == STATE_STANDBY) ? 3'd0 : (state == STATE_TEST) ? 3'd1 : (state == STATE_ADDRESS) ? 3'd2 : (state == STATE_WRITE) ? 3'd3 : 3'd4;
```

Sure, they both do the same thing, but it was much easier to parse what each thing did quickly. SystemVerilog is not a strongly typed language with regards to indentations, so you won't get compilation errors if you fail to indent your ends accurately. But we should indent them appropriately anyways. For example:

```sv
always @(posedge clk) begin
	if (rst)
		q <=0;
	else
		if (d)
			q <= ~q;
		else
			q <= q;
end
```

Is much easier to read than:

```sv
always @(posedge clk) begin
	if (rst)
		q <=0;
	else
	if (d)
		q <= ~q;
	else
		q <= q;
	end
```

Both will compile, but it takes a little longer for our mind to parse on first glance. Aligning comments at the end of a line is also helpful in improving readability as shown in the `playfield` module example near the top of this page.

## Naming things to be easily understood

In [EEPROM_STM95](https://github.com/MiSTer-devel/Genesis_MiSTer/blob/b15cceff237ebd6cb269119d6ec6f3b1dcbb0a8e/rtl/EEPROM_STM95.sv#L13){target=_blank} in the Genesis core, this module's port instantiation uses `_n` to signify that the signal is "active low":

```sv
module STM95XXX
(
	//...
	input         hold_n,        // Hold (active low)
	input         cs_n,          // Chip Select (active low)
	input         wp_n,          // Write Protect (active low)
	//...
);
```

It's also commented, but now you know after reading this that anytime a signal with `_n` is used, that is an active low signal, it doesn't need to be described as active low in a comment each time it is used from then on.

## If you run out of DSP or Logic space accidentally

If you run out of space in compilation, you might be accidentally implying your code to be put into DSP, which is very limited. You can specify that the compiler use logic instead by using the [multstyle](https://www.intel.com/content/www/us/en/programmable/quartushelp/17.0/index.htm#hdl/vlog/vlog_file_dir_multstyle.htm){target=_blank}:

```sv
(* multstyle = "logic" *) module myModule (
	input clk
)
```

This will force this module into logic space instead of it ever using DSP or block ram. Also you can force a module into DSP the same way with `(* multstyle = "dsp" *)`. The `multstyle` attribute can be used for Module declarations, variable declarations, and binary expressions.


