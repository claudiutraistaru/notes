# Rust closure

## closure is a trait(interface) in rust

I believe closure is consisted of: 1. function pointer 2. variables that are captured.

## Three different traits

| Trait | Reusability | Environment accessibility |
| ----- | ----------- | ------------------------- |
| Fn | Always | borrows immutably |
| FnMut | Always | borrows mutably |
| FnOnce | Once | take ownership |

_environment_ here means _enclosing scope_

Another interesting point is that closures can be completely replaced with a struct that takes environment as function argruments. Of course, you need to know which variable in your environment you want to capture. So using a struct is less flexible. You might need to make more changes when you later decide to start to use another variable in your environment.

## _move_ doesn't always mean `FnOnce`

This example below is copied from [this github issue](https://github.com/rust-lang/book/issues/781#issuecomment-311204028).
This demonstrate how closure can just be a custom struct. And it also show how _move_ closure doesn't always have to be FnOnce.

I think one of the biggest confusion about closure is working with _move_ and `FnOnce`.

By definition, _move_ closure will take ownership of variables captured from environment. `FnOnce` also indicates taking ownership rather than borrowing.

But they are not the same. _move_ closure doesn't always implement `FnOnce`. Look at the following diagram:

_move_ closure ---> taking ownership of vars captured from environment ---> all values have `Copy` trait ---> impl `Fn`
                                                              \--> not all values have `Copy` trait ---> impl `FnOnce`

## All closure impl `FnOnce`

Because all closures will be able to run at least once.




