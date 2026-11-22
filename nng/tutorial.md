# Natural Number Game — Tutorial World

NNG에서 자연수는 `0`과 `succ`(다음 수)로만 만들어진다. 덧셈은 두 규칙으로 정의된다.

- `add_zero : a + 0 = a`
- `add_succ : a + succ b = succ (a + b)`

## Level 1 — `rfl`
목표: `37 * x + q = 37 * x + q`

```lean
rfl
```
양변이 글자 그대로 같으면 `rfl`로 닫는다.

## Level 2 — `rw`
가정 `h : y = x + 7`, 목표: `2 * y = 2 * (x + 7)`

```lean
rw [h]
rfl
```
`rw [h]`는 목표의 `y`를 `x + 7`로 바꾼다 (가정의 왼쪽 → 오른쪽). NNG의 `rw`는 끝에 자동으로 `rfl`을 시도하지 않아서 직접 닫는다.

## Level 3 — 숫자
목표: `2 = succ (succ 0)`

```lean
rw [two_eq_succ_one]
rw [one_eq_succ_zero]
rfl
```
숫자 `2`, `1`은 `succ` 사슬의 줄임말이다.

## Level 4–6
완료. 풀이 정리 예정.

## Level 7 — `succ_eq_add_one`
목표: `succ n = n + 1`

```lean
rw [one_eq_succ_zero]   -- n + 1      → n + succ 0
rw [add_succ]           -- n + succ 0 → succ (n + 0)
rw [add_zero]           -- n + 0      → n
rfl
```
처음엔 `rw [add_succ n]`부터 쳐서 실패했다. `1`이 아직 `succ 0` 꼴이 아니라 패턴 `n + succ ?d`가 목표에 없었기 때문.

## Level 8 — `2 + 2 = 4`

```lean
rw [four_eq_succ_three]
rw [three_eq_succ_two]
rw [two_eq_succ_one]
rw [one_eq_succ_zero]   -- 양변을 succ 사슬로 풀기
rw [add_succ]
rw [add_succ]           -- + 오른쪽의 succ를 바깥으로
rw [add_zero]           -- + 0 지우기
rfl
```
배운 점: `a + n`은 `a`에 `succ`를 n번 붙이는 것. `add_zero`는 `add_succ`로 `succ`를 다 빼낸 뒤 `+ 0` 모양이 생겨야 쓸 수 있다.
