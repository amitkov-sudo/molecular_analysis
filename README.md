# Molecular Analysis

A Python script that reads a molecular structure from an `.xyz` file and computes a few basic “molecular analysis” properties: total electron count, a simple multiplicity estimate, molecular charge, and vibrational degrees of freedom.

Version: `0.1`  
Developed by: `Alyx Mitkov` (as referenced in the script output)

## What it does

Given:
- An `.xyz` file containing atomic symbols and Cartesian coordinates
- Whether the molecule is `linear` or `nonlinear`

The script:
1. Parses the XYZ file (number of atoms, atomic symbols, and coordinates)
2. Looks up each element in a built-in element table (atomic numbers / element values)
3. Computes:
   - Total “unpaired electron” count as the sum of the element table values
   - Multiplicity based on parity of that count (`1` if even, `2` if odd)
   - Total electrons as the sum of the element table values
   - Total molecular charge as the sum of the element table values
   - Vibrational degrees of freedom:
     - Linear: `3N - 5`
     - Non-linear: `3N - 6`
4. Writes a formatted text report to an output file.

## Input: XYZ format

The script expects the standard XYZ structure:

1. Line 1: number of atoms (integer)
2. Line 2: comment line (ignored by the script)
3. Lines 3..: one atom per line in the form:
   - `ElementSymbol x y z`

Any invalid coordinate lines are ignored with a console warning.

## Usage

Run the script with Python 3:

```bash
python molecular_analysis.py path/to/structure.xyz linear
```

Or for a non-linear molecule:

```bash
python molecular_analysis.py path/to/structure.xyz nonlinear
```

Notes:
- The second argument is case-insensitive (`linear/nonlinear`).
- The molecule name is derived from the XYZ filename (e.g., `water.xyz` -> `water`).

## Output

The report is written to:

```text
<input_filename>_molecular_analysis.out
```

Example:
- `water.xyz` -> `water_molecular_analysis.out`

## Limitations (as implemented)

This project is a lightweight “script” for simple calculations. In particular, the script’s electron- and charge-related quantities are derived from a built-in element table and then summed; it does not attempt full electronic structure or bonding analysis.

If you want more physically accurate electron configuration / spin-state logic, you can extend the element table and the calculation rules.

## Contributing

Contributions are welcome. If you open a PR, please include:
- A clear explanation of the change
- Updated documentation if you change the input/output behavior
