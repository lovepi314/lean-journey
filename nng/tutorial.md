# NNG: Tutorial World

Naturals are built from `0` and `succ`. Addition is defined by
- `add_zero : a + 0 = a`
- `add_succ : a + succ b = succ (a + b)`

## 1. rfl
`37 * x + q = 37 * x + q`
```lean
rfl
```

## 2. rw
`h : y = x + 7 ⊢ 2 * y = 2 * (x + 7)`
```lean
rw [h]
rfl
```
NNG's `rw` doesn't try `rfl` at the end, so close it manually.

## 3. numbers
`2 = succ (succ 0)`
```lean
rw [two_eq_succ_one]
rw [one_eq_succ_zero]
rfl
```

## 4–6
done, write-up todo

## 7. succ_eq_add_one
`succ n = n + 1`
```lean
rw [one_eq_succ_zero]  -- n + succ 0
rw [add_succ]          -- succ (n + 0)
rw [add_zero]          -- succ n
rfl
```
Tried `rw [add_succ n]` first. Failed: `1` isn't `succ 0` yet, so there's no `n + succ ?d` in the goal.

## 8. 2 + 2 = 4
```lean
rw [four_eq_succ_three]
rw [three_eq_succ_two]
rw [two_eq_succ_one]
rw [one_eq_succ_zero]
rw [add_succ]
rw [add_succ]
rw [add_zero]
rfl
```
`a + n` = apply `succ` to `a` n times. `add_zero` only works after all the `succ`s are pulled out.
