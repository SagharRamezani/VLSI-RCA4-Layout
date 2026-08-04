# 07 - Inverter DRC Log Template

## Goal

This file is used to record the first practical L-Edit test: drawing a simple CMOS inverter and running DRC.

The inverter is not the final project output, but it is important because it confirms that the technology file, layers, contacts, rails, and DRC setup are working before drawing the Full Adder.

## Inverter Layout Requirements

Use the same style required by the project:

```text
Horizontal Active
Vertical Poly
VDD rail on top
GND rail at bottom
PMOS row above
NMOS row below
```

## Suggested Inverter Structure

Pins:

```text
A
Y
VDD
GND
```

Connections:

```text
PMOS source -> VDD
PMOS drain  -> Y
NMOS drain  -> Y
NMOS source -> GND
PMOS gate   -> A
NMOS gate   -> A
PMOS bulk   -> VDD
NMOS bulk   -> GND
```

## Drawing Order in L-Edit

1. Draw top `VDD` Metal1 rail.
2. Draw bottom `GND` Metal1 rail.
3. Draw PMOS Active horizontally in N-Well.
4. Draw NMOS Active horizontally in substrate area.
5. Draw one vertical Poly line crossing both Active regions.
6. Add Contacts from Active to Metal1.
7. Connect PMOS source to VDD.
8. Connect NMOS source to GND.
9. Join PMOS drain and NMOS drain as output `Y`.
10. Add input pin `A` on Poly or Metal connected to Poly.
11. Add output pin `Y` on Metal1.
12. Add N-Well tap connected to VDD.
13. Add P-Substrate tap connected to GND.
14. Run DRC.
15. Fix all errors.
16. Save screenshot of DRC clean result.

## DRC Result Log

Fill this table after running DRC.

| Run | Date | Cell | Number of Errors | Main Problem | Fix |
|---|---|---|---:|---|---|
| 1 |  | INV_X1_TEST |  |  |  |
| 2 |  | INV_X1_TEST |  |  |  |
| Final |  | INV_X1_TEST | 0 | DRC clean |  |

## Screenshot List

Save screenshots in:

```text
screenshots/inverter/
```

Recommended file names:

```text
screenshots/inverter/01_inv_layout_first_draw.png
screenshots/inverter/02_inv_drc_errors.png
screenshots/inverter/03_inv_drc_clean.png
screenshots/inverter/04_inv_latchup_contacts.png
```

## Notes for Report

Write these points in the final report later:

- A test inverter was first drawn to verify the L-Edit environment.
- The same Horizontal Active / Vertical Poly style was used.
- N-Well contact was connected to VDD.
- Substrate contact was connected to GND.
- Final DRC result was error free.

## Checklist

- [ ] VDD rail exists.
- [ ] GND rail exists.
- [ ] PMOS is inside N-Well.
- [ ] NMOS is in substrate region.
- [ ] Poly is vertical.
- [ ] Active is horizontal.
- [ ] PMOS bulk is connected to VDD.
- [ ] NMOS bulk is connected to GND.
- [ ] Input pin `A` is defined.
- [ ] Output pin `Y` is defined.
- [ ] DRC is clean.
- [ ] Screenshots are saved.

