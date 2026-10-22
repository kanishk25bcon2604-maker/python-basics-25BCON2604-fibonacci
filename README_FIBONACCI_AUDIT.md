# README Audit: `fibonacci.py`

This audit checks each claim in `README_fibonacci.md` against the actual code in `fibonacci.py`. Claims were verified by reading the code and by running it (Python 3.12.3) with edge-case tests.

## Summary

- **Claims checked:** 16
- **Supported:** 15
- **Not Supported:** 1 (the clone URL, which is a placeholder the code cannot confirm)

## Source Code Audited

```python
def fibonacci(count):
    if count <= 0:
        raise ValueError("Enter a positive number of terms.")

    sequence = [0, 1]

    while len(sequence) < count:
        sequence.append(sequence[-1] + sequence[-2])

    return sequence[:count]

terms = 10
print(f"First {terms} Fibonacci numbers: {fibonacci(terms)}")
```

## Claim-by-Claim Results

| # | Claim in README | Verdict | Evidence from the code |
|---|---|---|---|
| 1 | Generates the first `n` terms of the Fibonacci sequence | Supported | Output matched an independent reference implementation for every count from 1 to 500. |
| 2 | The sequence starts with 0 and 1, and each number is the sum of the two before it | Supported | `sequence = [0, 1]` seeds the list, and the loop appends `sequence[-1] + sequence[-2]`. |
| 3 | Implemented in a single file, `fibonacci.py` | Supported | All logic is in one file. |
| 4 | `fibonacci(count)` returns the first `count` terms as a list | Supported | The function ends with `return sequence[:count]`, and `type(fibonacci(5))` is `list`. |
| 5 | Iterative implementation (no recursion) | Supported | It uses a `while len(sequence) < count` loop and the function never calls itself. |
| 6 | Raises a clear `ValueError` for zero or negative input | Supported | `if count <= 0: raise ValueError(...)`. Both `fibonacci(0)` and `fibonacci(-4)` raised it. |
| 7 | `1` returns `[0]` and `2` returns `[0, 1]` | Supported | Tested directly: `fibonacci(1)` gave `[0]` and `fibonacci(2)` gave `[0, 1]`. The initial list has two items, and the slice `[:count]` trims it for `count = 1`. |
| 8 | No external dependencies | Supported | The file has no `import` statements (confirmed with a search for `import` and `from` lines). |
| 9 | Requires Python 3.6 or higher | Supported | The file uses an f-string, which was introduced in 3.6. Only 3.12 was run, so the lower bound comes from the syntax rule, not a test. |
| 10 | No third-party packages needed | Supported | Same evidence as #8. |
| 11 | `git clone https://github.com/<your-username>/<your-repository>.git` | Not Supported | The code cannot confirm any repository, URL, or folder name, and the URL is a placeholder. |
| 12 | `python fibonacci.py` runs the script | Supported | It ran successfully and printed the expected line. On some systems the command is `python3`. |
| 13 | The script generates as many terms as the `terms` variable at the bottom of the file | Supported | `terms = 10` is followed by `print(f"... {fibonacci(terms)}")`. |
| 14 | Changing it to `terms = 15` works | Supported | `fibonacci(15)` returned `[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377]`. |
| 15 | Output is `First 10 Fibonacci numbers: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]` | Supported | This is the exact output of the script. |
| 16 | Zero or negative input gives `ValueError: Enter a positive number of terms.` | Supported | The message is word for word the same as in the code. |

## Behaviors the README Does Not Mention

### Non-integer input

A float or a string is not rejected with a clear message:

| Input | Result |
|---|---|
| `fibonacci(5.0)` | `TypeError: slice indices must be integers or None or have an __index__ method` |
| `fibonacci(5.5)` | `TypeError: slice indices must be integers or None or have an __index__ method` |
| `fibonacci("a")` | `TypeError: '<=' not supported between instances of 'str' and 'int'` |

The README never says what happens with input that is not a whole number. Note that the float error only appears at the final slice, after the loop has already run.

### Import side effect

Importing the file also runs the example, because the `terms = 10` and `print(...)` lines sit at module level without an `if __name__ == "__main__":` guard. In testing, the example output printed twice: once from running the file directly and once from importing it.

## Test Environment

- Python 3.12.3
- Checks run: direct execution, counts of 1, 2, 3, 15, and 1000, zero and negative input, float input (5.0 and 5.5), string input, comparison against an independent reference implementation for counts 1 to 500, and a search of the file for imports.
