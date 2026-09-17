# Task 3

## Design pattern

The class uses the Factory pattern, which encapsulates object creation by selecting and returning a concrete implementation (`GifReader` or `JpegReader`) through the common `ImageReader` type based on the input's image format.

## 1. Why is the constructor private?

`CreateImageReader` provides a static method, so clients can call it directly on the class without creating a `CreateImageReader` object. Making the constructor private prevents clients from constructing unnecessary instances and makes the intended usage clear. The factory method can still construct and return `GifReader` and `JpegReader` objects because their constructors are separate from the factory class's constructor.

## 2. Creating a reader for the GIF image

```java
ImageReader reader = CreateImageReader.createImageReader(fis);
```

The factory detects that `fis` contains a GIF image and returns a `GifReader` initialized with that stream, referenced through the `ImageReader` type. 
