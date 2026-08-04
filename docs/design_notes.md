# Design Notes - 4-bit Ripple Carry Adder Layout

## 1. Project Summary

The goal is to design and draw the layout of a 4-bit Ripple Carry Adder in L-Edit using `morbn20.tdb` technology.

Required layout style:

- Horizontal Active
- Vertical Poly
- Row-based layout
- Maximum row height: 40 lambda
- Latch-up contacts must be included
- Final layout must be DRC error free

## 2. Inputs and Outputs

### Inputs

```text
A0 A1 A2 A3
B0 B1 B2 B3
Cin
VDD
GND
```

### Outputs

```text
S0 S1 S2 S3
Cout
```

### Internal Carry Signals

```text
C1 C2 C3
```

## 3. 4-bit RCA Connection

```text
FA0(A0, B0, Cin) -> (S0, C1)
FA1(A1, B1, C1)  -> (S1, C2)
FA2(A2, B2, C2)  -> (S2, C3)
FA3(A3, B3, C3)  -> (S3, Cout)
```

## 4. Full Adder Logic

```text
Sum  = A xor B xor Cin
Cout = AB + ACin + BCin
```

Truth table:

| A | B | Cin | Sum | Cout |
|---|---|-----|-----|------|
| 0 | 0 | 0   | 0   | 0    |
| 0 | 0 | 1   | 1   | 0    |
| 0 | 1 | 0   | 1   | 0    |
| 0 | 1 | 1   | 0   | 1    |
| 1 | 0 | 0   | 1   | 0    |
| 1 | 0 | 1   | 0   | 1    |
| 1 | 1 | 0   | 0   | 1    |
| 1 | 1 | 1   | 1   | 1    |

## 5. Selected Architecture

The first suggested architecture for layout is a Mirror Full Adder.

Reason:

- Good for row-based layout
- Better carry path organization
- More suitable for diffusion sharing
- Useful for Ripple Carry Adder because carry propagation is the critical path

If the layout becomes too complex, the backup option is Static Complementary CMOS using smaller subcells such as XOR, NAND, NOR, and inverter.

## 6. Layout Plan

General cell organization:

```text
VDD rail
PMOS active row
Internal routing area
NMOS active row
GND rail
```

Required layout direction:

```text
Active: horizontal
Poly: vertical
```

Power routing:

- VDD rail at the top of the cell
- GND rail at the bottom of the cell
- VDD and GND rails should continue across all four Full Adder cells

Carry routing:

```text
FA0.Cout -> FA1.Cin
FA1.Cout -> FA2.Cin
FA2.Cout -> FA3.Cin
```

Carry should be short and as straight as possible.

## 7. Latch-up Contacts

Required taps:

- N-Well tap connected to VDD
- P-Substrate tap connected to GND

Suggested placement:

- At the beginning of the RCA row
- At the end of the RCA row
- Between cells if the row becomes wide

Exact spacing must be checked using the `morbn20.tdb` design rules.

## 8. DRC Checklist

Before final submission, check:

- Poly width
- Poly spacing
- Active width
- Active spacing
- Poly extension over Active
- Contact enclosure
- Metal width
- Metal spacing
- Well enclosure
- Well/substrate contacts
- No floating well
- No floating substrate
- No VDD-GND short
- No open carry connection
- Row height <= 40 lambda

Exact numeric rules must be read from the Design Rule Table of `morbn20.tdb`.

## 9. Screenshots Needed for Report

- Full Adder layout
- RCA4 final layout
- DRC error-free result
- Latch-up contacts
- Carry connection between cells
- Final pin names

## 10. Next Step

Next step is to prepare the transistor-level Full Adder design and draw the first stick diagram before starting L-Edit layout.
