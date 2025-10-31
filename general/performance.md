# ⚡ General Performance Tips

---

## 📑 Table of Contents
- [Prefer prefix increment (`++i`) over postfix (`i++`)](#prefer-prefix-increment-i-over-postfix-i)
- [Check even/odd numbers using bitwise operations](#check-evenodd-numbers-using-bitwise-operations)

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
