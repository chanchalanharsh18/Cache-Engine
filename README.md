# CacheEngine

CacheEngine is a robust and cross-platform CPU Cache Simulator written in modern standard C++ (C++11). It simulates the internal working principles of a CPU cache, processing memory trace files to calculate performance metrics such as cache hits, misses, and overall hit rates. 

The primary goal of this project is to provide a highly configurable, educational, and easy-to-use tool to analyze and understand cache behaviors under various structural configurations.

## Features

- **Mapping Techniques**: Supports Direct-Mapped, Fully Associative, and Set-Associative cache mappings.
- **Replacement Policies**: Implements **Random** and **LRU (Least Recently Used)** replacement algorithms for fully associative and set-associative mappings.
- **Write Policy**: Uses a **Write-back** policy by default. The internal architecture defines interfaces making it easily extensible for other policies (e.g., Write-through).
- **Cross-Platform**: Built purely with standard C++11 with zero third-party dependencies, ensuring seamless compilation on Windows, Linux, and macOS.
- **Robust CLI**: Handles a wide range of invalid inputs gracefully and provides clear, interactive console prompts.

## Prerequisites

To build and run the simulator, you will need:
- A C++11 compatible compiler (GCC, Clang, or MSVC)
- [CMake](https://cmake.org/) (Version 3.10 or higher recommended)

## Build Instructions

You can build the project from the root directory using CMake:

```bash
# Configure the build directory
cmake -B build

# Compile the project
cmake --build build
```

## How to Run

### Interactive Mode
You can run the program interactively and answer the configuration prompts (cache size, mapping technique, etc.) directly in your terminal:

```bash
./build/CacheEngine
```

### Automated / Batch Mode
To speed up testing or to repeatedly run the same configurations, you can provide an input file and pass it to the executable via standard input. 

**1. Create a text file with your answers (e.g., `test_input.txt`):**
```text
64
64
1
2
TestData\gcc.trace
e
```
*(This configures a 64KB cache, 64B cache line, Direct Mapped, Write-Back, reads the `gcc.trace` file, and exits after completion).*

**2. Run the program using redirection:**

**On Windows (PowerShell / CMD):**
```cmd
cmd /c ".\build\CacheEngine.exe < test_input.txt"
```

**On Linux / macOS:**
```bash
./build/CacheEngine < test_input.txt
```

## Performance Note

If you only want to view the final summary statistics (hit/miss rate) without tracking the individual status of every single memory access, ensure that the `NDEBUG` macro is defined. In `src/base.h`, keep the following line uncommented:

```cpp
#define NDEBUG // For NDEBUG pattern
```
Disabling `NDEBUG` (removing that line) can result in significantly longer execution times when processing large trace files (e.g., 300,000+ lines).

## Test Data & Traces

Sample trace files are provided in the `TestData/` directory for immediate testing (e.g., `gcc.trace`, `mcf.trace`, `swim.trace`). 

Additional trace files can be generated or downloaded from standard benchmarks (like CSE240A Cache Simulator assignments) or by using dynamic instrumentation tools like [Intel Pin](http://software.intel.com/en-us/articles/pintool-downloads).

## License

This project is open-sourced under the MIT License.
