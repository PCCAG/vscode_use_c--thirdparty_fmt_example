

要在VSCode中使用vcpkg安装的库，并确保它们在MinGW-w64中可用

1. **安装vcpkg：** 确保您已经使用vcpkg安装了您需要的库。如果还没有安装，请按照vcpkg的文档进行安装。
2. **查找vcpkg的安装目录：** 打开命令提示符或终端，输入以下命令，找到vcpkg的安装目录：

   ```bash
   vcpkg integrate install
   ```

   此命令将显示vcpkg的集成目录，例如 `C:\vcpkg\installed\x64-windows`。
3. **配置MinGW-w64：** 确保您已经安装了MinGW-w64，并确保其在系统路径中。在vcpkg的集成目录中，通常有一个 `scripts`目录，里面包含了用于配置不同工具链的脚本。运行适合MinGW-w64的脚本：

   ```bash
   .\scripts\buildsystems\vcpkg.cmake -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release
   ```

   这将生成一个 `toolchain-mingw.cmake` 文件，稍后将在VSCode中使用。
4. **在VSCode中配置：** 打开您的项目文件夹，创建一个名为 `.vscode` 的文件夹，然后在其中创建一个名为 `settings.json` 的文件。在 `settings.json` 文件中添加以下内容：

   ```json
   {
       "cmake.configureSettings": {
           "CMAKE_TOOLCHAIN_FILE": "C:/vcpkg/scripts/buildsystems/vcpkg.cmake"
       }
   }
   ```

   请根据您的实际路径修改上述路径。
5. **调整CMake配置：** 在您的项目中，确保 `CMakeLists.txt` 文件引用了您需要的库，同时指定它们在vcpkg中的安装目录。例如：

   ```cmake
   find_package(fmt CONFIG REQUIRED)
   target_link_libraries(your_target PRIVATE fmt::fmt)
   ```

   确保库的名称和版本与vcpkg中的一致。
6. **构建项目：** 使用VSCode中的CMake工具构建项目。您应该能够看到MinGW-w64使用vcpkg安装的库进行构建。

请注意，确保在配置VSCode时使用正确的路径，以便让它找到vcpkg和MinGW-w64。此外，确保vcpkg的Triple（目标三元组）与MinGW-w64的Triple匹配，以便正确链接库。
