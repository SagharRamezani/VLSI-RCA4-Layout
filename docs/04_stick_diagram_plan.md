# 04 - Stick Diagram Plan

## Goal

This step prepares the stick diagram plan before drawing the real layout in L-Edit.
The project requires:

- Horizontal Active
- Vertical Poly
- Row-based layout
- Maximum row height: 40 lambda
- Latch-up contacts
- DRC error free final layout

## Layout Style

Use the standard CMOS row style:

```text
VDD rail
PMOS active row
routing area
NMOS active row
GND rail
```

Rules for the stick diagram:

- Active must be horizontal.
- Poly must be vertical.
- PMOS devices are placed near VDD.
- NMOS devices are placed near GND.
- Inputs are preferably vertical poly lines.
- Outputs and internal nodes are routed with metal.
- VDD and GND rails must be continuous.

## First Cell to Draw: Inverter

Before drawing the Full Adder, draw and verify a simple inverter cell. This checks that:

- technology file is loaded correctly,
- layers are known,
- contacts work correctly,
- DRC setup works,
- well/substrate contacts are understood.

## Inverter Stick Diagram

Simple inverter connections:

```text
PMOS:
Source -> VDD
Drain  -> OUT
Gate   -> IN
Bulk   -> VDD

NMOS:
Source -> GND
Drain  -> OUT
Gate   -> IN
Bulk   -> GND
```

Stick diagram idea:

```text
VDD  ============================
          |
PMOS active ----[ Poly IN ]---- OUT
          |
          | Metal connection
          |
NMOS active ----[ Poly IN ]---- OUT
          |
GND  ============================
```

**Need L-Edit screenshot:** inverter stick/layout after DRC.

## Full Adder Stick Diagram Direction

For the Full Adder, use a cell-based style:

- keep VDD rail at the top,
- keep GND rail at the bottom,
- use vertical poly for A, B, Cin and complementary signals,
- put carry-related transistors close to the output Cout,
- keep Cout on the right side so it can connect directly to the next FA cell,
- keep Sum accessible as an output pin.

## Signals Needed

External pins of one Full Adder:

```text
A
B
Cin
Sum
Cout
VDD
GND
```

Possible internal/complementary signals:

```text
Abar
Bbar
Cinbar
internal XOR/XNOR nodes
```

If complementary inputs are needed, generate them using local inverters.

## Carry Routing Plan for RCA4

For the 4-bit RCA:

```text
FA0.Cout -> FA1.Cin
FA1.Cout -> FA2.Cin
FA2.Cout -> FA3.Cin
```

Recommended placement:

```text
FA0 | FA1 | FA2 | FA3
```

Keep the carry route short and mostly horizontal.

## Row Height Check

After drawing the cell boundary, measure:

```text
cell height <= 40 lambda
```

If it is larger:

- reduce extra routing space,
- move signals closer while keeping DRC rules,
- simplify internal routing,
- consider splitting into more rows only if needed.

## Checklist

- [ ] Active is horizontal.
- [ ] Poly is vertical.
- [ ] PMOS row is above NMOS row.
- [ ] VDD rail is at the top.
- [ ] GND rail is at the bottom.
- [ ] Carry output is placed near the next cell.
- [ ] Latch-up contacts are planned.
- [ ] Row height can fit under 40 lambda.
