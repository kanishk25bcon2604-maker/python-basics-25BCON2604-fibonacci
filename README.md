# Fibonacci Sequence Generator

A simple Python program that generates the first `n` terms of the Fibonacci sequence.

## Description

The Fibonacci sequence starts with 0 and 1, and each following number is the sum of the two numbers before it: `0, 1, 1, 2, 3, 5, 8, 13, ...`

This project implements that sequence in a single, easy-to-read Python file, `fibonacci.py`. The `fibonacci(count)` function returns the first `count` terms as a list.

## Features

- Returns the first `count` Fibonacci numbers as a list
- Iterative implementation (no recursion)
- Raises a clear `ValueError` for zero or negative input
- Correctly handles small inputs: `1` returns `[0]` and `2` returns `[0, 1]`
- No external dependencies

## Requirements

- Python 3.6 or higher
- No third-party packages

## Installation

Clone the repository and move into the project folder:

```bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

## Usage

Run the script from the command line:

```bash
python fibonacci.py
```

The script generates as many terms as the value assigned to the `terms` variable at the bottom of `fibonacci.py`. To generate a different number of terms, change that value:

```python
terms = 15
print(f"First {terms} Fibonacci numbers: {fibonacci(terms)}")
```

## Example

```python
terms = 10
print(f"First {terms} Fibonacci numbers: {fibonacci(terms)}")
```

Output:

```text
First 10 Fibonacci numbers: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

Passing zero or a negative number raises an error:

```text
ValueError: Enter a positive number of terms.
```
