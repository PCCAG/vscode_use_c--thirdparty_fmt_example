### 编译静态库：

1. **编译静态库的命令：**

   ```bash
   g++ -c -o mylib.o mylib.cpp   # 编译源文件
   ar rcs libmylib.a mylib.o     # 创建静态库
   ```
2. **注意事项：**

   - 使用 `-c` 选项编译源文件为目标文件。
   - 使用 `ar` 命令创建静态库，`rcs` 分别表示创建、替换、生成索引。
   - 静态库的命名一般以 `lib` 开头，以 `.a` 结尾，例如 `libmylib.a`。

### 编译动态库：

1. **编译动态库的命令：**

   ```bash
   g++ -fPIC -shared -o libmylib.so mylib.cpp
   ```
2. **注意事项：**

   - 使用 `-fPIC` 选项生成位置独立的代码，这对于动态库是必要的。
   - 使用 `-shared` 选项生成共享库。
   - 动态库的命名一般以 `lib` 开头，以 `.so` 结尾，例如 `libmylib.so`。
   - 如果需要在编译时指定库的版本信息，可以使用 `-Wl,-soname,libmylib.so.x` 选项。

### 使用静态库：

1. **编译使用静态库的程序：**

   ```bash
   g++ -o my_program my_program.cpp -L/path/to/libs -lmylib
   ```
2. **注意事项：**

   - 使用 `-L` 选项指定静态库文件的搜索路径。
   - 使用 `-l` 选项指定要链接的静态库的名称。

### 使用动态库：

1. **编译使用动态库的程序：**

   ```bash
   g++ -o my_program my_program.cpp -L/path/to/libs -lmylib
   ```
2. **注意事项：**

   - 使用 `-L` 选项指定动态库文件的搜索路径。
   - 使用 `-l` 选项指定要链接的动态库的名称。
   - 运行时可能需要设置 `LD_LIBRARY_PATH` 或使用 `-Wl,-rpath,/path/to/libs` 选项指定动态库的搜索路径。

### 通用注意事项：

1. **符号可见性：**

   - 对于动态库，可以使用 `-fvisibility=hidden` 选项隐藏内部符号。
2. **版本号：**

   - 对于动态库，可以使用 `-Wl,-soname,libmylib.so.x` 选项指定库的版本信息。
3. **编译选项的顺序：**

   - 在编译程序时，源文件应该在最后，库和目标文件的顺序也有讲究。
4. **依赖关系：**

   - 注意库之间的依赖关系，确保正确地链接所有必要的库。
