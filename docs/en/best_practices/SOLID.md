## SOLID Principles

SOLID principles help structure C++ code so it is easier to maintain, extend, and test.

## Example

This class mixes invoice calculations, persistence, and printing:

```cpp
class Invoice {
	double total = 0;
public:
	void add(double price) { total += price; }
	void save() { /* write total to a file */ }
	void print() { /* send total to a printer */ }
};
```

Separate responsibilities and depend on an abstraction for persistence:

```cpp
class Invoice { double total = 0; public: void add(double p) { total += p; } double amount() const { return total; } };
struct InvoiceStore { virtual void save(const Invoice&) = 0; virtual ~InvoiceStore() = default; };
class InvoiceService {
	InvoiceStore& store;
public:
	explicit InvoiceService(InvoiceStore& s) : store(s) {}
	void save(const Invoice& invoice) { store.save(invoice); }
};
```

## Reference

- [SOLID Principles - Wikipedia](https://en.wikipedia.org/wiki/SOLID)
