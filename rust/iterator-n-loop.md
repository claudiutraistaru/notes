# Iterator N Loop

## Borrow in a for loop

```rust
for x in y.someVec {
// ...
}
```
If y is immutable and  elements in `someVec` dosn't impl `Copy` or `Clone`, this won't compile.
In order to borrow element inside of `y.someVec`, it needs to be rewritten as:
```
for x in &y.someVec {
// ...
}
```

*Notice, reference symbol is put in front of the vec not the element.


