# Pointer & Reference

## Box

__Purpose__: `Box` is used to store data on the heap and providing a ref/ptr to it. `Box` owns the data. So if `Box` is moved out of a scope to another, the data moves along.

__Confusion__: `Box` by nature is not clonable as a reference. It doesn't impl `Clone` trait for certain underlying types, e.g. &str and `Clone` trait objects. So when `Box`'s `clone()` is called, it's doing a deep copy. Not a copy of a reference.

If one wants to create multiple reference to an object, use `Rc` as `Rc` is clonable as a reference.