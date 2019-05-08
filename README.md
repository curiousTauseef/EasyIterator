[![Build Status](https://travis-ci.com/TheLartians/EasyIterator.svg?branch=master)](https://travis-ci.com/TheLartians/EasyIterator)
[![codecov](https://codecov.io/gh/TheLartians/EasyIterator/branch/master/graph/badge.svg)](https://codecov.io/gh/TheLartians/EasyIterator)

# EasyIterator

EasyIterator aims to be a zero-cost C++17 iterator library that simplifies iterator creation.
It adds well-known iterators from other languages to C++, such as `range`, `zip` and `enumerate`. 

## Example

### Iteration

```cpp
using namespace easy_iterator;

std::vector<int> integers(10);
std::vector<std::string> strings(integers.size());

for (auto i: range(integers.size())) {
  integers[i] = i*i;
}

for (auto [i, v, s]: zip(range(integers.size()), integers, strings)) {
  s = std::to_string(i) + "^2 = " + std::to_string(v);
}

for (auto [i, s]: enumerate(strings)) {
  std::cout << "strings[" << i << "] = \"" << s << "\"" << std::endl;
}
```

### Simple iterator creation

```cpp
struct Fibonacci {
  unsigned current = 0;
  unsigned next = 1;

  void advance() {
    auto tmp = next;
    next += current;
    current = tmp;
    return true;
  }
  
  unsigned value() {
    return current;
  }
};

for (auto [i,v]: enumerate(MakeIterable<Fibonacci>())){
  std::cout << "Fib_" << i << "\t= " << v << std::endl;
  if (i > 10) break;
}
```
