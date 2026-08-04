# 05 - L-Edit Inverter Cell Checklist

## Goal

Before building the Full Adder, create a small inverter cell in L-Edit. This is a safe first layout test.

## Step 1 - Open L-Edit Project

1. Open L-Edit.
2. Open or create the design library.
3. Load the technology file:

```text
morbn20.tdb
```

4. Check that the layer palette is visible.

**Need L-Edit screenshot:** technology/layer palette loaded.

## Step 2 - Check Grid

Set the grid so drawing in lambda-based dimensions is easy.

Recommended action:

- enable visible grid,
- enable snap to grid,
- use the design grid recommended by morbn20.tdb.

Do not invent design-rule numbers. Exact values must be read from the Design Rule Table of morbn20.tdb.

## Step 3 - Create New Cell

Create a new cell:

```text
INV
```

This cell will be used only as a layout practice cell and possibly for complementary signals later.

## Step 4 - Draw Power Rails

Draw two horizontal Metal1 rails:

```text
Top rail    -> VDD
Bottom rail -> GND
```

Use a width allowed by the technology rules.

**This value must be extracted from the Design Rule Table of morbn20.tdb.**

## Step 5 - Draw Active Regions

Draw two horizontal active regions:

```text
PMOS active near VDD
NMOS active near GND
```

The PMOS active must be inside N-Well. The NMOS active is in P-substrate.

## Step 6 - Draw Poly Gate

Draw one vertical Poly line crossing both PMOS active and NMOS active.

This creates:

```text
one PMOS transistor
one NMOS transistor
```

The Poly line is the input pin:

```text
IN
```

## Step 7 - Connect Output

Connect the drains of PMOS and NMOS together with Metal1.

Name this node:

```text
OUT
```

## Step 8 - Connect Sources

Connect:

```text
PMOS source -> VDD
NMOS source -> GND
```

Use contacts where Metal1 connects to diffusion.

## Step 9 - Add Latch-up Contacts

Add:

```text
N-Well tap -> VDD
P-Substrate tap -> GND
```

These contacts are required to avoid floating well/substrate.

**Need L-Edit screenshot:** N-Well contact and substrate contact.

## Step 10 - Define Pins

Define pins on the correct metal layers:

```text
IN
OUT
VDD
GND
```

Recommended:

- IN can be connected from Poly to Metal1 using a contact if needed.
- OUT should be on Metal1.
- VDD and GND pins should be on their rails.

## Step 11 - Run DRC

Run DRC from the L-Edit verification menu.

Depending on version, this may be:

```text
Tools > DRC
```

or

```text
Verify > DRC
```

Goal:

```text
0 DRC errors
```

**Need L-Edit screenshot:** DRC result showing no errors.

## Common Errors

| Error | Likely Cause | Fix |
|---|---|---|
| Poly spacing | poly lines too close | increase spacing |
| Contact enclosure | contact not fully enclosed | enlarge enclosing layer |
| Metal spacing | metal routes too close | move route or increase spacing |
| Active spacing | active regions too close | increase separation |
| Well floating | missing N-Well contact | add tap to VDD |
| Substrate floating | missing substrate tap | add tap to GND |

## Commit Message After This Step

After saving screenshots or notes, commit with:

```powershell
git add docs/04_stick_diagram_plan.md docs/05_l_edit_inverter_cell.md
git commit -m "Add stick diagram and inverter layout plan"
git push
```
