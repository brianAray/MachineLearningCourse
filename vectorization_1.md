# Vectorization Part 1

## Example to Understand Vectorization

### Parameters and Features
- `w = [w1 w2 w3]`
    - `n = 3`
- `b` is a number
- `x = [x1 x2 x3]`

We can represent this in Python with `NumPy`.

> Main thing to note is that mathematical notation counts from 1, but programming counts from 0

```python
w = np.array([1.0, 2.5, -3.3])
b = 4
x = np.array([10, 20, 30])
```

Without vectorization we could write it like this

`f_wb(x) = w1*x1 + w2*x2 + w3*x3 + b`

```python
f = w[0] * x[0] +
    w[1] * x[1] +
    w[2] * x[2] + b
```

But what happens if `n` becomes 1000000?

We could write this with a `for-loop`

```python
f = 0
for j in range(0,n):
    f = f + w[j] * x[j]
f = f + b
```

When using `range(0,n)`, `j` will be `0 ... n-1` and will not include `n`. Typically this is written like `range(n)` but it is included for emphasis.

This still doesn't use vectorization and isn't that efficient.

## Vectorization

`f_wb(x) = w . x + b`

```python
f = np.dot(w,x) + b
```

This implements the mathematical dot product with `w` and `x` then add `b`. This method is the vectorized method. It results in the code running much faster than the previous implementation. Behind the scenes, the `numpy` dot function uses parallel hardware in your computer. This works in your local system and your GPU. It is the ability of the `dot` function to use parallel systems that make it so much faster.

This is much better than doing it manually, and is recommended.