# Task 2

## 1. Design principles

### Single Responsibility Principle

`TaxReport` is responsible for obtaining the tax report as a string, while `PDFUtility` is responsible for adapting that report into PDF form. Separating these responsibilities gives them different reasons to change (a change to report-generation logic belongs in `TaxReport`, while a change to PDF formatting belongs in `PDFUtility`).

### Dependency Inversion Principle

The client's high-level report-access logic depends on the abstraction `FormatUtility`, and the concrete `PDFUtility` implements that abstraction. This keeps the client from depending directly on PDF-specific implementation details. 

### Open-Closed Principle

The formatting behavior can be extended by adding another implementation of `FormatUtility`, while leaving the client's interface-based report-access logic and the existing `TaxReport` class unchanged. 

## 2. Design pattern

The design uses the **Adapter pattern**, specifically an object adapter.

- **Client:** `Client`
- **Target interface:** `FormatUtility`
- **Adapter:** `PDFUtility`
- **Adaptee:** `TaxReport`

`TaxReport.getTaxReport(...)` supplies a `String`, but the client accesses reports through `FormatUtility`, with `PDFUtility.getTaxReport(...)` supplying a `PDF`. `PDFUtility` implements the target interface, delegates to the existing `TaxReport` object, and converts the returned string into the PDF representation. This lets the client use the existing reporting functionality through the expected interface without changing `TaxReport`.
