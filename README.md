# VLSI RCA4 Layout

This repository contains the layout design process of a 4-bit Ripple Carry Adder using L-Edit and `morbn20.tdb` technology.

## Project Requirements

- Design a 4-bit Ripple Carry Adder layout
- Use L-Edit with `morbn20.tdb` technology
- Horizontal Active / Vertical Poly layout style
- Row-based layout
- Maximum row height: 40 lambda
- Include latch-up contacts
- Final layout must be DRC error free

## Design Flow

1. Analyze the project requirements
2. Choose a suitable Full Adder architecture
3. Design the transistor-level Full Adder
4. Draw the stick diagram
5. Create the Full Adder layout in L-Edit
6. Run DRC and fix layout errors
7. Build the 4-bit RCA using four Full Adder cells
8. Connect carry signals between cells
9. Add VDD, GND, well contacts, and substrate contacts
10. Run final DRC
11. Prepare screenshots and final report

## Folder Structure

```text
docs/          Project statement and design notes
ledit/         L-Edit cells and final layout files
screenshots/   Layout, DRC, and latch-up contact screenshots
spice/         Netlists and simulation results
report/        Final report and figures
references/    Course slides and references
```

## Final Deliverables

- Full Adder layout
- 4-bit RCA layout
- DRC error-free screenshot
- Latch-up contact screenshot
- Final report
- Optional SPICE/Verilog simulation files
