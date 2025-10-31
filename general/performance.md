# ⚡ General Performance Tips

---

## 📑 Table of Contents
- [Prefer prefix increment (`++i`) over postfix (`i++`)](#prefer-prefix-increment-i-over-postfix-i)
- [Check even/odd numbers using bitwise operations](#check-evenodd-numbers-using-bitwise-operations)
- [Prioritize Common Cases First](#prioritize-common-cases-first)

---

## Prefer prefix increment (`++i`) over postfix (`i++`)

In most languages (C, C++, Java, PHP, JavaScript, etc.), **`++i`** increments the variable and returns the new value directly,  
while **`i++`** returns a *copy of the old value*, then increments — creating an unnecessary temporary object.

```c
// ✅ Faster — increments directly
++i;

// ❌ Slightly slower — returns old value before incrementing
i++;
```

### 📊 Impact
Negligible in high-level code, but measurable in tight loops or performance-critical sections (e.g., millions of iterations in C/Java).

### 💡 Rule of thumb
Use `++i` when you don’t need the previous value.
Use `i++` only if you explicitly need the value before incrementing.

---

## Check even/odd numbers using bitwise operations

Prefer bitwise operators over modulo for parity checks.

```c
// ✅ Faster — if false, number is even
if (number & 1) {
    // odd
} else {
    // even
}

// ❌ Slightly slower
if (number % 2 == 0) {
    // even
}
```

### 📊 Impact
Modulo involves division, which is slower than bitwise operations on most CPUs.

### 💡 Rule of thumb
Use `number & 1` when you only care about parity (even/odd).
Use `%` when code readability matters more than micro-optimization.

---

## Prioritize Common Cases First

When evaluating multiple conditions, **handle the most common or expected cases first**.
This reduces unnecessary comparisons and improves performance by helping the CPU’s **branch predictor** make accurate guesses about control flow.

```c
// Example: Validating user input
// ✅ Better — common valid cases first
if (age >= 18 && age <= 100) {
    approveRegistration();
} else if (age < 18) {
    rejectMinor();
} else {
    rejectInvalidAge();
}

// ❌ Worse — rare or invalid cases first
if (age < 0) {
    rejectInvalidAge();
} else if (age < 18) {
    rejectMinor();
} else if (age > 100) {
    rejectInvalidAge();
} else {
    approveRegistration();
}
```

In the first version, the system immediately processes the **normal case** (ages 18–100)
and skips rare edge conditions like minors or invalid data.
This makes the code both clearer and more efficient when executed repeatedly (e.g., processing millions of records).

### 📊 Impact

Modern CPUs use branch prediction to anticipate which path an if statement will take.
If the prediction is wrong, the pipeline is flushed — a small but costly delay.
By prioritizing the most frequent conditions, you reduce branch mispredictions and save cycles in tight loops or heavy workloads.

Even in interpreted languages, this logic short-circuits unnecessary checks,
saving time across large datasets or repeated validations.

### 💡 Rule of thumb
- **Put frequent or expected cases first**.
- Move **rare or exceptional conditions** to the end.
- Use this technique mainly in **hot paths** or **performance-sensitive areas**.
- Keep readability as a priority — clarity is also performance.
