# 03 - L-Edit Setup Checklist

This file is a practical checklist for starting the project in L-Edit.

## 1. Open L-Edit and create a design

1. Open L-Edit.
2. Create a new design/library.
3. Load the technology file:

```text
morbn20.tdb
```

4. Save the design in:

```text
ledit/cells/
```

Suggested file name:

```text
rca4_cells.tdb
```

## 2. Check grid and lambda

Before drawing:

- Check the display grid.
- Check snap grid.
- Make sure drawing is aligned to lambda-based grid.
- Do not draw random off-grid shapes.

Exact grid values must be read from the technology setup and design rules.

## 3. First test cell: inverter

Before drawing the Full Adder, draw a simple CMOS inverter.

Pins:

```text
A
Y
VDD
GND
```

Purpose:

- Verify layers.
- Verify contacts.
- Verify N-Well / P-Sub contacts.
- Verify DRC setup.

## 4. Required layers to identify

Find these layers in L-Edit:

```text
N-Well
Active / Diffusion
N-Select
P-Select
Poly
Metal1
Metal2
Contact
Via
```

Layer names may be slightly different depending on the technology display settings.

## 5. Inverter layout style

Use the same style required by the project:

```text
Horizontal Active
Vertical Poly
```

Recommended placement:

```text
VDD rail at top
PMOS active below VDD
Poly input vertical
NMOS active below routing area
GND rail at bottom
```

## 6. Latch-up contacts in test cell

Add:

- N-Well contact connected to VDD.
- P-Substrate contact connected to GND.

Do not leave well or substrate floating.

## 7. Run DRC on inverter

Run DRC before moving to Full Adder.

Check and fix:

- Contact enclosure.
- Metal spacing.
- Poly spacing.
- Active spacing.
- Well enclosure.
- Missing well/substrate contact.
- VDD/GND short.

Target:

```text
0 DRC errors
```

## 8. After inverter is clean

Next cells:

```text
INV
NAND2
NOR2
XOR2
FULL_ADDER
RCA4
```

If using direct mirror Full Adder, create only:

```text
INV helpers if needed
FULL_ADDER
RCA4
```

## 9. Screenshots to collect

Save screenshots in:

```text
screenshots/full_adder/
screenshots/drc/
screenshots/latchup_contacts/
```

Required early screenshots:

- Inverter layout.
- Inverter DRC result.
- Example well/substrate contacts.

## 10. Next action

The next technical step is to draw the transistor-level Full Adder schematic/stick diagram before implementing it in L-Edit.
