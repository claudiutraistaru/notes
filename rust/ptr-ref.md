# Pointer & Reference

## Box

__Problem to solve__: Reference becomes invalid when owner goes out of scope. Need to pass ownership to outside of the original scope.

__Solution__: `Box` is used to store data on the heap and providing a ref/ptr to it. `Box` owns the data. So if `Box` is moved out of a scope to another, the data stays accessible.

__Confusion__: `Box` by nature is not clonable as a reference. It doesn't impl `Clone` trait for certain underlying types, e.g. &str and `Clone` trait objects. So when `Box`'s `clone()` is called, it's doing a deep copy. Not a copy of a reference.

If one wants to create multiple reference to an object, use `Rc` as `Rc` is clonable as a reference.

## Rc & Arc

__Problem to solve__: Multiple reference to a single piece of data in heap.

__Solution__: Reference Counting(`Rc`). Drops the data when reference count goes to zero. `Arc` is the atomic/thread-safe version of `Rc`.

### Note

1. `Rc` and `Arc` has _interior mutability_. When they are declared as immutable(_exterior mutability_), they still needs to keep track of the number of references being cloned. So the counter inside of `Rc`/`Arc` is mutable. Otherwise, it's not reference-counting anymore.
2. For `T` in `Rc<T>` and `Arc<T>`, it is not immutable by nature. In another word, the actual pointer in `Rc<T>` and `Arc<T>` that points to an object of T is interiorly immutable. To make the underlying data mutable, Wrap `T` with `RefCell` or `Mutex`.

## Cells(Cell & RefCell)

__Problem to solve__: You can either have one mutable reference or have several immutable references at a time.

__Solution__: interior mutability to the underlying data. Even when pointers themselves are immutable, the underlying data can mutate.

### Note

1. `Cell` can only be applied to `Copy`able object. `RefCell` can wrap around any type.
2. `Cell` never panics, while `RefCell` may panic.
3. `RefCell` panics when one try to borrow while it is already being borrowed as mutable. Basically, `RefCell` checks the "Rust borrow rules" at runtime instead of compile time. It actually maintains a reference counter internally.
