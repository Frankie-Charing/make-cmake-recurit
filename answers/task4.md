# Task 4：思考题

## 1. Make 和简单的 build.sh 有什么区别？

一个简单的 `build.sh` 只是把所有 `gcc` 命令从头到尾执行一遍：哪怕只改了一个文件，也会把整个项目重新编译一遍。Make 会根据 target 与依赖文件的时间戳判断哪些产物过期了，只重新编译受影响的目标，再重新链接，实现**增量构建**。项目越大，省下的时间越明显。

## 2. CMake 是编译器吗？

执行 `cmake --build build` 时，最终是谁在编译 C 源文件？

CMake 本身不是编译器，而是一个构建系统生成器：它读取 `CMakeLists.txt`，生成 Makefile / Ninja 等底层构建文件。`cmake --build build` 最终调用底层的 make/ninja，再由它们调用 **gcc（编译器）** 把 C 源码真正编译成机器码。

## 3. 为什么不希望每次都重新编译所有 `.c` 文件？

编译很耗时，尤其是几十上百个源文件的大项目。如果只修改了其中一个 `.c` 文件，其余 49 个文件生成的 `.o` 目标文件并没有变化，可以直接复用，只需要重新编译改动的那个文件、再重新链接即可，从而大幅缩短构建时间。这正是 Make 增量构建的核心价值。

## 自检结果

```text
=== Make & CMake Recruit Check ===

Task 2: Makefile
[PASS] Make task builds and runs correctly

Task 3: CMakeLists.txt
[PASS] CMake task configures, builds and runs correctly

Summary: 2 passed, 0 failed
```
