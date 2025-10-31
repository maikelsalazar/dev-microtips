# ⚡ PHP Performance Tips

---

## 📑 Table of Contents
- [Prefer single quotes over double quotes](#prefer-single-quotes-over-double-quotes)

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
