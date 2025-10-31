# 🧠 Code Micro Tips

Small, practical programming tips to write **cleaner, faster, and more maintainable code**.  
Each tip focuses on micro-optimizations, readability improvements, or subtle language behaviors.

---

## 📂 Structure

| Folder | Description |
|--------|--------------|
| `general/` | Tips that apply across all programming languages (naming, readability, design). |
| `php/` | Language-specific micro-optimizations, syntax tricks, and best practices. |

---

## 🧩 Example Tip

### Prefer prefix increment (++i) over postfix (i++)
In most languages (C, C++, Java, PHP, JavaScript, etc.), **`++i`** increments the variable and returns the new value directly,  
while **`i++`** returns a *copy* of the old value, then increments — creating an unnecessary temporary object.

```c
// ✅ Faster — increments directly
++i;

// ❌ Slightly slower — returns old value before incrementing
i++;
```

#### 📊 Impact:
Negligible in high-level code, but measurable in tight loops or performance-critical sections (e.g. millions of iterations in C/Java).

#### 💡 Rule of thumb:
Use ++i when you don’t need the previous value.
Use i++ only if you explicitly need the value before incrementing.

### 🚀 Goal
Collect small but valuable insights that make code:
- **More efficient** ⚡
- **More readable** 📖
- **More maintainable** 🔧
