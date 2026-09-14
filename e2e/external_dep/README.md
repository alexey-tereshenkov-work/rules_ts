Generate a large `lib.ts` file (adjust `N` to control the file size):

```
node -e '
const N = 40000;
const out = [];
out.push("// Auto-generated synthetic benchmark file - no semantic value.");
for (let i = 0; i < N; i++) {
  const prev = i > 0 ? `I${i - 1}` : "null";
  out.push(`interface I${i} { a: number; b: string; c: boolean; d: ${prev}; }`);
  out.push(`type T${i}<T> = { [K in keyof T]: T[K] };`);
  out.push(`function f${i}(a: I${i}): T${i}<I${i}> { return a; }`);
  out.push(`function g${i}(x: number): number { return x + ${i} * 2 - 1; }`);
  out.push(`class C${i} { method(a: I${i}): T${i}<I${i}> { return a; } value = ${i}; }`);
}
require("fs").writeFileSync("lib.ts", out.join("\n") + "\n");
console.log("wrote", out.length + 1, "lines");
'
```
