# ⚡ PHP Performance Tips

---

## 📑 Table of Contents
- [Prefer single quotes over double quotes](#prefer-single-quotes-over-double-quotes)
- [Use [] instead of array_push](#use--instead-of-array_push)

---

## Prefer single quotes over double quotes

When no variable interpolation or escape sequences are needed, use **single quotes**.  
Double quotes cause PHP to scan the string for variables and special characters, which adds minor overhead.

```php
// ✅ Faster — no parsing overhead
echo 'Hello World';

// ❌ Slower — parser checks for variables or escape sequences
echo "Hello World";
```

### 📊 Impact

The performance difference is minimal in most applications, but measurable in large-scale loops or templating code.

### 💡 Rule of thumb

Use single quotes unless you need:
- Variable interpolation ("Hello $name")
- Escape sequences like "\n" or "\t".

---

## Use [] instead of array_push

When adding elements to an array, prefer the `[]` syntax over `array_push()`.
It’s more concise, readable, and slightly faster since it avoids a function call.

**Reference**: [PHP array_push](https://www.php.net/manual/en/function.array-push.php)

```php
$holder = [];

// ✅ Faster
$holder[] = 1;

// ❌ Slower
array_push($holder, 1);
```

### 📊 Impact
Micro difference, but noticeable in high-frequency array insertions (e.g., large data processing loops)

### 💡 Rule of thumb
- Use [] for single element appends.
- Reserve array_push() only when adding multiple elements at once (array_push($arr, 1, 2, 3)).