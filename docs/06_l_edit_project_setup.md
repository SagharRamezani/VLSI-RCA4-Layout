# 06 - L-Edit Project Setup

## Goal

In this step we create the first L-Edit project for the 4-bit RCA layout project and prepare the design environment before drawing any real cell.

The final project requirement is a 4-bit Ripple Carry Adder layout in L-Edit using `morbn20.tdb`, with Horizontal Active / Vertical Poly style, row-based layout, maximum row height of `40 lambda`, latch-up contacts, and DRC error-free result.

## Files to Create in This Step

Suggested L-Edit files:

```text
ledit/cells/inverter_test.tdb
```

If your L-Edit saves a different extension or design file format, keep the file in:

```text
ledit/cells/
```

## Step 1: Open L-Edit

Open L-Edit from Windows.

If the program asks for a technology file, select:

```text
morbn20.tdb
```

If it does not ask automatically, load the technology from the technology/setup menu. The exact menu name depends on the L-Edit version, but it is usually one of these:

```text
File > Open Technology
Setup > Technology
Technology > Load Technology
```

## Step 2: Create a New Design Library

Create a new layout/design file and save it as:

```text
inverter_test
```

Save it inside:

```text
ledit/cells/
```

Do not start directly with the full adder. First, build and DRC-check a simple inverter.

## Step 3: Check Grid and Unit

Before drawing, check the grid.

Recommended practical setup:

```text
Display grid: ON
Snap grid: ON
Use lambda-based drawing if available
```

If L-Edit shows units in micron instead of lambda, do not invent the numeric rules. Read the exact values from the `morbn20.tdb` technology rule table.

Write down the grid setting in the report later.

## Step 4: Create Cell Names

Create these cells gradually:

```text
INV_X1_TEST
FA_MIRROR_X1
RCA4
```

For now only create:

```text
INV_X1_TEST
```

## Step 5: Layer List to Identify

Find the exact layer names in L-Edit. The names can vary slightly with the technology file.

Typical layers needed:

```text
N-Well
Active / Diffusion
N-Select
P-Select
Poly
Contact
Metal1
Metal2
Via
```

For the inverter test, you need at least:

```text
N-Well
Active
P-Select
N-Select
Poly
Contact
Metal1
```

## Step 6: Save the Empty Project

Save the L-Edit file before drawing.

Recommended commit after saving:

```powershell
git add ledit/cells
git commit -m "Add initial L-Edit inverter test file"
git push
```

Only do this after the L-Edit file is created and saved.

## Checklist

- [ ] L-Edit opens correctly.
- [ ] `morbn20.tdb` is loaded.
- [ ] Grid is visible.
- [ ] Snap grid is enabled.
- [ ] Cell `INV_X1_TEST` is created.
- [ ] File is saved inside `ledit/cells/`.
- [ ] No layout drawing has been started before checking technology layers.

