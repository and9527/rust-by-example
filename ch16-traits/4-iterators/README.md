# Iterators

The `Iterator` trait is uesd to implement iterators over collections such as arrays.

The trait requires only a meths to be defined for the `next` element, which may be manually defined in an `impl` block or automatically defined (as in arrays and ranges).

As a point of convenience for common situations, the `for` construct turns some collections into iterators using the `.into_iterator()` method.

## Example

```rust
struct Fibonacci {
    curr: u32,
    next: u32,
}

// Implement `Iterator` for `Fibonacci`.
// The `Iterator` trait only requires a method to be defined for the `next` element.
impl Iterator for Fibonacci {
    type Item = u32;

    // Here we define the sequence using `.curr` and `.next`.
    // the return type is `Option<T>`:
    //     * When the `Iterator` is finished, `None` is returned.
    //     * Otherwise, the next value is wrapped in `Some` and re
    fn next(&mut self) -> Option<u32> {
        let new_next = self.curr + self.next;

        self.curr = self.next;
        self.next = new_next;

        // Since there's no endpoint to a Fibonacci sequence, the `Iterator` 
        // will never return `None`, and `Some` is always returned.
        Some(self.curr)
    }
}

// Returns a Fibonacci sequence generator
fn fibonacci() -> Fibonacci {
    Fibonacci { curr: 1, next: 1 }
}
```
