## Introduction
We present a solution to the [Fun Challenge 4](https://www.ioccc.org/2025/challenge.html#ferguson) for the IOCCC's 2025/ferguson winning entry.

Written in 2026 by Antoine Mathys.

## Part 1
Let's look at the following code snippet:

```c
c = calloc(1, (F = 9, H * *Q * j)), x = -(tr + R) * *Q / T, d = c == e != d,
Y = (lo + R) * *Q / T, d = c != e != d != d == 2 * d, d *= 2,
y = -(-U + 90) * j / R, x = -x, Z = (-L + 90) * j / R,
d = !-!(c != e) != d - 1 != d + 1, x = -x, Y = -Y, Y = -Y,
d = -!-!(c != e) == d, Y = -Y, d = -d, x = -x, x = -x,
d = c == e != d == !(c == e) != d / 2,
d = d / 2; /* CHANGE != 1 AND PROVE d IS 1 */
if (d = (c != e == !d != d != d == 1 && e != c) != 1 ||
        /* NOW YOU KNOW d IS 1! */ fread(c, -*(S[F]) - d * 3, b * j, q) ^
            j * j * 2)
    X;
```

Before this, `e` and `c` are `0`, and the call to `m()` might have set `e` to `c`. Thus they are both still equal to `0`.

We also replace `!= 1` by `!= N`, for some constant `N`.

The code becomes:

```c
F = 9;
x = -(tr + R) * *Q / T;
Y = -((lo + R) * *Q / T);
y = -(-U + 90) * j / R;
Z = (-L + 90) * j / R;
d = 0;
c = calloc(1, H * *Q * j);
/* CHANGE N AND PROVE d IS 1 */
if ((c != 0) != N)
    X; // returns
/* NOW YOU KNOW d IS 1! */
if (fread(c, -*(S[F]), b * j, q) != j * j * 2)
    X; // returns
```

Changing the value of d before returning is a no-op. Note that `d` stays `0` irrespective of the value of `N`. Thus both comments are erroneous.

If `N` is different from `1`, we have:

```c
...
c = calloc(1, H * *Q * j);
if (c != 0)
    X; // returns
...
```

and a successful call to `calloc()` causes the program to terminate. That is obviously not what we want. Hence `N` must be `1`.

Since `d` is not set again, we observe that it is `0` on entry for the last three calls to `m()`.

## Part 2
Let's now examine this snippet near the beginning of `main()`:

```c
if (m(lo, tr,
      (J = u, H = d + 4, I = J - H, D = *(S + u - 1) + 1,
       d -= *(*(S + 7) + 6), L)) ||
    b ^ j * 2)
    X;
```

We can rewrite it like this:

```c
J = u;
H = d + 4;
I = J - H;
D = &S[u - 1][1];
d = d - S[7][6];
if (m(lo, tr, L) || (b != j * 2))
    X; // returns
```

We note that `d` must be initialized to `-1`. That ensures that `H` is `3`. This is required because it is the number of bytes per pixel in the image file format used.

Since the initial value of `S[7][6]` is `-1`, `d` is also `0` on entry for the first call to `m()`. Therefore `d` is purely a distraction and can be replaced by `0` in `m()`.

If `S[7][6]` and `d` were not initialized to the same value, the first invocation of `m()` would work incorrectly and that would probably lead to a segmentation fault.