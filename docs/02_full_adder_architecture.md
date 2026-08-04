# 02 - Full Adder Architecture Selection

## 1. Source-based requirements

Project requirements:

- Design the layout of a 4-bit Ripple Carry Adder.
- Use L-Edit with `morbn20.tdb` technology.
- Use Horizontal-Active / Vertical-Poly layout style.
- Use row-based layout.
- Each row height must be at most `40 lambda`.
- Add latch-up contacts.
- Final layout must be DRC error free.

Course design approach:

- Start from electronic and transistor-level design.
- Continue with layout design.
- Use SPICE for detailed transistor-level checking when needed.

## 2. Full Adder equations

For one Full Adder:

```text
Sum  = A xor B xor Cin
Cout = AB + ACin + BCin
```

Equivalent carry form:

```text
P    = A xor B
G    = AB
Sum  = P xor Cin
Cout = G + P.Cin
```

This form is useful because `Cout` is the critical signal in a Ripple Carry Adder.

## 3. Truth table

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

## 4. Architecture candidates

### Option 1: Static Complementary CMOS Full Adder

Advantages:

- Full voltage swing.
- Good noise margin.
- No static current in steady state.
- Easier to verify logically.

Disadvantages:

- More transistors.
- Larger layout area.
- More routing inside the cell.

### Option 2: Transmission-Gate Full Adder

Advantages:

- Compact XOR implementation.
- Good full-swing behavior when transmission gates are used.

Disadvantages:

- Needs both true and complementary control signals.
- More internal routing.
- Layout can become harder for a first L-Edit implementation.

### Option 3: Pass-Transistor Logic

Advantages:

- Can reduce transistor count.
- Can be compact.

Disadvantages:

- May have degraded logic levels.
- Needs restoration buffers.
- Less safe for a final DRC-clean layout project.

### Option 4: Mirror Full Adder

Advantages:

- Good choice for transistor-level layout.
- Carry path is regular.
- Better diffusion sharing than a random gate-level implementation.
- Suitable for Ripple Carry Adder because carry propagation is the critical path.

Disadvantages:

- More difficult than basic gate-level drawing.
- Needs careful transistor ordering and stick diagram planning.

## 5. Final choice

For this project, the selected architecture is:

```text
Mirror-style static CMOS Full Adder
```

Reason:

- It is appropriate for transistor-level layout.
- It keeps the carry path more organized.
- It is compatible with Horizontal-Active / Vertical-Poly style.
- It can be arranged as a row-based standard cell.
- It has full-swing CMOS output levels.

If the direct mirror layout becomes too complex in L-Edit, the backup implementation is a hierarchical static CMOS Full Adder using smaller cells:

```text
INV, NAND2, NOR2, XOR2
```

The final report should clearly mention which implementation is actually drawn in L-Edit.

## 6. Signals needed inside one Full Adder

External pins:

```text
A
B
Cin
Sum
Cout
VDD
GND
```

Useful internal signals:

```text
Abar
Bbar
Cinbar
P = A xor B
Pbar
G = AB
```

Only the signals that are actually needed in the final transistor-level circuit should be routed in layout.

## 7. Layout decision for the Full Adder cell

Cell organization:

```text
VDD rail
PMOS active row
Internal Metal routing area
NMOS active row
GND rail
```

Required direction:

```text
Active: horizontal
Poly: vertical
```

Pin placement suggestion:

- Inputs `A`, `B`, `Cin`: preferably from the top or left side.
- Outputs `Sum`, `Cout`: preferably on the right side.
- `Cout` should be placed so it can connect directly to the next cell's `Cin`.
- `VDD` should run as a continuous top rail.
- `GND` should run as a continuous bottom rail.

## 8. Carry path in RCA4

The critical path is usually:

```text
Cin -> C1 -> C2 -> C3 -> Cout
```

So in layout:

- Carry wires must be short.
- Avoid unnecessary jogs.
- Prefer Metal1 for local carry routing.
- Use Metal2 only if crossing is unavoidable.

## 9. Row-height constraint

The cell height must support:

- Top VDD rail.
- PMOS diffusion row.
- Internal routing.
- NMOS diffusion row.
- Bottom GND rail.
- Well/substrate contacts.

Constraint:

```text
row height <= 40 lambda
```

Exact physical distances must be checked using the `morbn20.tdb` Design Rule Table.

## 10. Checklist for this phase

- [x] Full Adder equations written.
- [x] Truth table prepared.
- [x] Candidate architectures compared.
- [x] Mirror-style static CMOS selected.
- [x] Backup gate-level CMOS option defined.
- [x] Internal signals listed.
- [x] Carry path identified as critical.
- [x] Row-based layout direction fixed.
