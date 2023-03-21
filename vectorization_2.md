# Vectorization Part 2

Let's understand what is happening with vectorization.

### Without Vectorization

Let's create a `for-loop`

```python
for j in range(0,16):
    f = f + w[j] * x[j]
```

A `for-loop` like this runs without vectorization. This piece of code runs one after the other.

- `t0 -> f + w[0] * x[0]`
- `t1 -> f + w[1] * x[1]`
- `...`
- `t15 -> f + w[15] * x[15]`

### With Vectorization

```python
np.dot(w,x)
```

Instead of running each calculations one by one, it does all the computations in parallel.

```
t0 -> 
    w[0] w[1] ... w[15]
    *    *    ... *
    x[0] x[1] ... x[15]
    
t1 ->
    w[0]*x[0] + w[1]*x[1] + ... + w[15]*x[15]
```

Code with vectorization is much faster. The steps are drastically used, and vectorized implmentation of learning algorithms. This improved efficiency is essential to working on the large datasets modern algorithms use.

## Gradient Descent

Let's see an actual example of how this helps. Say you have a problem with 16 parameters and `b`.
We calculate the derivatives of these points and store that as well.

```python
w = np.array([0.5, 1.3, ..., 3.4])
d = np.array([0.3, 0.2, ..., 0.4])
# We ignore b
```

In order to compute, we are looking for `wj = wj - 0.1dj` where `0.1` is the learning rate alpha, for `j = 1 ... 16`.

### Without vectorization
- `w1 = w1 - 0.1d1`
- `w2 = w2 - 0.1d2`
- `...`
- `w16 = w16 - 0.1d16`

```python
for j in range(0,16):
    w[j] - w[j] - 0.1 * d[j]
```

### With Vectorization
```python
w = w - 0.1 * d
```

Behind the scenes, vectorization will be used to implement linear regression. The speed may not look that much better at 16, but at 10000+ is amazing!