# Task 4

## 1. Design pattern

The design uses the **Composite pattern**, which lets clients treat individual objects and groups of objects uniformly through a common interface.

- `Product` is the component interface, defining `price()`.
- `DVD` and `Book` are leaves, each providing its own price.
- `Shelf` is the composite, it implements `Product` and contains a collection of `Product` objects.

A client can call `price()` on a single book, a DVD, or an entire shelf without needing to distinguish between them. Because a shelf is also a `Product`, shelves can contain other shelves, forming a hierarchy.

## 2. Implementation of `Shelf.price()`

The method sums the prices of all products on the shelf:

```java
@Override
public int price() {
    int total = 0;
    for (Product product : products) {
        total += product.price();
    }
    return total;
}
```

An empty shelf costs `0`. If a product is another shelf, its own `price()` method computes its contents' total, so nested shelves are handled recursively.
