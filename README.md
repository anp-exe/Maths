# Maths: Notes and Exercises

Link to my notes and exercises: **[Math notes](Math.ipynb)**

These notes are made using Jupyter Notebook and were created to help understand and apply linear algebra techniques; specifically obtaining a reduced row‑echelon form (RREF) using various methods through SymPy.

## SymPy Matrix.rref

The `Matrix.rref()` method returns the reduced row‑echelon form of a matrix and the indices of pivot variables.

Signature:

```python
rref(iszerofunc=<function _iszero>,
     simplify=False,
     pivots=True,
     normalize_last=True,
    )
```

Return
: A tuple (rref_matrix, pivot_indices) when `pivots=True`, otherwise just the row‑reduced matrix.

### Parameters

- `iszerofunc` : Function
  - A function used for detecting whether an element can act as a pivot. By default `lambda x: x.is_zero` is used.
- `simplify` : Function or bool
  - A function used to simplify elements when looking for a pivot. By default SymPy’s `simplify` is used. Can be set to `False` to disable.
- `pivots` : bool
  - If `True`, a tuple containing the row‑reduced matrix and a tuple of pivot columns is returned. If `False`, just the row‑reduced matrix is returned.
- `normalize_last` : bool
  - If `True`, pivots are *not* normalized to 1 until after all entries above and below each pivot are zeroed. This makes the row reduction fraction‑free until the last step. If `False`, each pivot is normalized to 1 immediately and the naive row reduction is used.

### Why `normalize_last` matters

Using `normalize_last=True` can improve performance and avoid introducing fractions during intermediate steps (useful for exact integer arithmetic). Setting it to `False` gives the classical algorithm where pivots are normalized as soon as they're chosen.

## Examples

Python examples using SymPy:

```python
from sympy import Matrix
from sympy.abc import x

# A symbolic matrix
m = Matrix([[1, 2], [x, 1 - 1/x]])

# rref returns (matrix, pivot_indices)
rref_result = m.rref()
print(rref_result)
# (Matrix([[1, 0], [0, 1]]), (0, 1))

# Unpacking
rref_matrix, rref_pivots = m.rref()
print(rref_matrix)
# Matrix([[1, 0], [0, 1]])
print(rref_pivots)
# (0, 1)
```

Another quick numeric example illustrating rationals vs floats:

```python
from sympy import Matrix, S

M_float = Matrix([[1, 2], [3, 4]]) * (1/3)     # Python float division
M_rational = Matrix([[1, 2], [3, 4]]) * S(1)/3  # SymPy Rational

print("Float matrix:\n", M_float)
print("Rational matrix:\n", M_rational)
```

## Notes

- Use `S(1)/3` or `Rational(1, 3)` when you want exact fractions in SymPy instead of floating point numbers.
- The examples assume you have SymPy installed (add `sympy` to `requirements.txt`).
