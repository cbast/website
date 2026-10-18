# Google Test

Google Test is a C++ framework for writing and running unit tests.

## Example

```cpp
#include <gtest/gtest.h>

int add(int a, int b) { return a + b; }

TEST(AddTest, AddsTwoNumbers) {
	EXPECT_EQ(add(2, 3), 5);
}
```

```bash
g++ -std=c++17 test.cpp -lgtest -lgtest_main -pthread -o test
./test
```

## References

- [Google Test - GitHub](https://github.com/google/googletest)
- [Google Test - User Guide](https://google.github.io/googletest/)
