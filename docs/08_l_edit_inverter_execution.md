# 08 - Practical L-Edit Execution: First Inverter Cell

## Goal

This step creates a small test inverter in L-Edit before starting the Full Adder layout.
The purpose is to check:

- `morbn20.tdb` is loaded correctly
- Lambda/grid settings are usable
- PMOS/NMOS drawing flow is clear
- Contacts and Metal1 connections work
- DRC can be executed and fixed
- Screenshot workflow is ready

This test cell is not the final project cell. It is only a safe practice cell before drawing the Full Adder.

---

## Cell Name

Use this cell name:

```text
INV_X1_TEST
```

Save it under the L-Edit project/library that will later contain:

```text
FA_MIRROR_X1
RCA4_TOP
```

---

## Required Layout Style

Follow the project style from the beginning:

```text
Horizontal Active
Vertical Poly
Row-Based
```

For this inverter:

- PMOS row is placed at the top.
- NMOS row is placed at the bottom.
- VDD rail is above PMOS.
- GND rail is below NMOS.
- Poly input line is vertical.
- Output is connected using Metal1.

---

## Suggested Cell Pins

Create these pins:

```text
A
Y
VDD
GND
```

Pin meaning:

| Pin | Meaning |
|---|---|
| A | Input |
| Y | Output |
| VDD | Power rail |
| GND | Ground rail |

---

## Step 1 - Create/Open L-Edit Design

1. Open L-Edit.
2. Create a new design or open the current project library.
3. Load the technology file:

```text
morbn20.tdb
```

Depending on the version, the menu may be one of these:

```text
File > New
File > Open Technology
Setup > Technology
```

If the exact menu is different, use the menu that loads the `.tdb` technology file.

**Screenshot needed:** technology/library loaded in L-Edit.

---

## Step 2 - Check Grid

Set the drawing grid to a lambda-friendly value.

Use:

```text
Setup > Design > Grid
```

or the equivalent grid setting menu in your L-Edit version.

Do not invent design rule numbers. If exact minimum widths or spacings are needed, read them from:

```text
Tools / Setup / Technology / Design Rules
```

or the design rule table of `morbn20.tdb`.

---

## Step 3 - Draw VDD and GND Rails

Use Metal1 for power rails.

Draw:

```text
VDD rail: horizontal Metal1 at top
GND rail: horizontal Metal1 at bottom
```

The rails must be wide enough according to the design rules.

Exact minimum Metal1 width:

```text
Must be read from morbn20.tdb Design Rule Table.
```

---

## Step 4 - Draw PMOS Region

1. Draw N-Well around the PMOS area.
2. Draw PMOS Active horizontally inside N-Well.
3. Add P-Select/P-Implant if required by the technology layer set.
4. Draw vertical Poly crossing the PMOS Active.

This creates the PMOS transistor.

PMOS connections:

| Terminal | Connection |
|---|---|
| Gate | A |
| Source | VDD |
| Drain | Y |
| Bulk | VDD through N-Well tap |

---

## Step 5 - Draw NMOS Region

1. Draw NMOS Active horizontally below the PMOS row.
2. Add N-Select/N-Implant if required.
3. Use the same vertical Poly input line that crosses PMOS and NMOS Active.

This creates the NMOS transistor.

NMOS connections:

| Terminal | Connection |
|---|---|
| Gate | A |
| Source | GND |
| Drain | Y |
| Bulk | GND through substrate tap |

---

## Step 6 - Connect Output Y

Connect PMOS drain and NMOS drain together using Contact + Metal1.

Output node:

```text
Y = common drain node of PMOS and NMOS
```

Add a pin label `Y` on the Metal1 output route.

---

## Step 7 - Connect Input A

The vertical Poly line is the input gate line.

Add a pin label:

```text
A
```

If the project expects pins only on metal, connect Poly to Metal1 using Poly Contact and place the pin on Metal1.

---

## Step 8 - Add Latch-up Contacts

Add both contacts:

```text
N-Well Tap  -> VDD
P-Substrate Tap -> GND
```

For the inverter test:

- Place one N-Well contact near the PMOS row.
- Place one substrate contact near the NMOS row.

Exact tap spacing must be checked from `morbn20.tdb` if the technology gives a maximum spacing rule.

**Screenshot needed:** inverter with N-Well tap and substrate tap visible.

---

## Step 9 - Check Cell Height

Measure the total cell height from the top of VDD rail to the bottom of GND rail.

Constraint for the final project:

```text
Row height <= 40 lambda
```

For this inverter test, try to keep the height compatible with this limit, because the Full Adder row will use the same standard-cell style.

---

## Step 10 - Run DRC

Run DRC using the L-Edit menu, usually one of these:

```text
Tools > DRC
Verification > DRC
Verify > DRC
```

Expected result:

```text
0 DRC Errors
```

If errors appear, fix them one by one.

Common errors:

| Error type | Common reason | Fix |
|---|---|---|
| Metal width | Rail too narrow | Increase Metal1 width |
| Metal spacing | Routes too close | Increase spacing |
| Contact enclosure | Contact not covered enough | Enlarge Active/Metal around contact |
| Poly spacing | Poly lines too close | Move Poly lines apart |
| Well enclosure | N-Well too small | Enlarge N-Well around PMOS |
| Floating well | Missing N-Well tap | Add N-Well tap to VDD |
| Floating substrate | Missing substrate tap | Add substrate tap to GND |

**Screenshot needed:** DRC result showing zero errors.

---

## Files/Screenshots to Save

Save screenshots in:

```text
screenshots/inverter/
```

Recommended screenshot names:

```text
01_inv_layout.png
02_inv_latchup_contacts.png
03_inv_drc_clean.png
```

Save L-Edit layout file/cell in:

```text
ledit/cells/
```

Recommended file/cell name:

```text
INV_X1_TEST
```

---

## Checklist

| Check | Status |
|---|---|
| `morbn20.tdb` loaded | TODO |
| Cell `INV_X1_TEST` created | TODO |
| PMOS drawn | TODO |
| NMOS drawn | TODO |
| Poly vertical input drawn | TODO |
| Active horizontal rows drawn | TODO |
| VDD/GND rails drawn | TODO |
| A/Y/VDD/GND pins created | TODO |
| N-Well tap connected to VDD | TODO |
| Substrate tap connected to GND | TODO |
| DRC run | TODO |
| DRC = 0 errors | TODO |
| Screenshots saved | TODO |
