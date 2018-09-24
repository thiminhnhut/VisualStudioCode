# Lập trình C/C++ trên Visual Studio Code

* **Thực hiện:** Thi Minh Nhựt - **Email:** thiminhnhut@gmail.com

* **Thời gian:** Ngày 14 tháng 01 năm 2018

## Nguồn tham khảo

1. [C/C++ for VS Code (Preview)](https://code.visualstudio.com/docs/languages/cpp)

1. [vscode-cpptools](https://github.com/Microsoft/vscode-cpptools/blob/master/Documentation/LanguageServer/MinGW.md)

1. [Setting up Visual Studio Code for Simple C/C++ developmen](https://fatminmin.com/blog/settup-up-vscode.html)

1. [debugging c++ with gdb in visual studio code](https://www.youtube.com/watch?v=agBOQ3SI4R0)

## Nội dung thực hiện

### Cài đặt MinGW trên Windows

* Tải `MinGW` ở địa chỉ: [Minimalist GNU for Windows](http://www.mingw.org/)

* Cài đặt các package sau:

  * `mingw32-gcc-g++` (The GNU C++ Compiler).
  
  * `mingw32-gdb` (The GNU Source-Level Debugger).

* Cài đặt biến môi trường: `Path` với đường dẫn sau: `C:\MinGW; C:\MinGW\bin`.

### Cài đặt Clang trên Windows

* Tải `Clang` ở địa chỉ: [Clang](http://clang.llvm.org/)

### Cài đặt Visual Studio Code

* Tải `Visual Studio Code` ở địa chỉ: [Download Visual Studio Code](https://code.visualstudio.com/download)

### Cài đặt Extension cho C/C++ trên Visual Studio Code

* `C/C++ for Visual Studio Code`.

* `C/C++ Clang Command Adapter`.

* `C/C++ Snippets`.

### Cấu hình thư mục .vscode

* Sau khi cài extension `C/C++ for Visual Studio Code`, sử dụng `Visual Studio Code` mở thư mục có chưa mã nguồn C/C++, sẽ tự động tạo ra thư mục `.vscode`.

* Cấu hình để thư mục `.vscode` có 3 file sau: `c_cpp_properties.json`, `tasks.json` và `launch.json`.

* Để compiler và debugger trên Visual Studio Code, thực hiện các cấu hình sau:

  * Nếu compiler source `C++` thì làm theo các bước bên dưới.

  * Nếu compiler source `C` thì xóa các dòng trong `"includePath"` có chứa `c++`.

  * `Ctrl-Shift-P: C/Cpp: Edit Configurations...`: mở file `c_cpp_properties.json`, thay đổi nội dung như sau (ở đây đang sử dụng `MinGW32-6.3.0`):

        {
            "configurations": [
                {
                    "name": "Win32",
                    "intelliSenseMode": "clang-x64",
                    "includePath": [
                        "${workspaceRoot}",
                        "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++",
                        "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++/mingw32",
                        "C:/MinGW/lib/gcc/mingw32/6.3.0/include/c++/backward",
                        "C:/MinGW/lib/gcc/mingw32/6.3.0/include",
                        "C:/MinGW/include",
                        "C:/MinGW/lib/gcc/mingw32/6.3.0/include-fixed"
                    ],
                    "defines": [
                        "_DEBUG",
                        "UNICODE",
                        "__GNUC__=6",
                        "__cdecl=__attribute__((__cdecl__))"
                    ],
                    "browse": {
                        "path": [
                            "C:/MinGW/lib/gcc/mingw32/6.3.0/include",
                            "C:/MinGW/lib/gcc/mingw32/6.3.0/include-fixed",
                            "C:/MinGW/include/*"
                        ],
                        "limitSymbolsToIncludedHeaders": true,
                        "databaseFilename": ""
                    }
                }
            ]
        }

  * `Ctrl-Shift-P: Tasks: Configure Tasks...`: mở file `tasks.json`, chọn `Create tasks.json file from templates`, chọn `Other`.

  * Trong thư mục `.vscode` sẽ tạo ra file `tasks.json`, thay đổi nội dung như sau:

        {
            // See https://go.microsoft.com/fwlink/?LinkId=733558
            // for the documentation about the tasks.json format
            "version": "2.0.0",
            "tasks": [
                {
                    "label": "Build C++", // Label build source
                    "type": "shell",
                    "command": "g++",
                    "args": [
                        "-g",
                        "helloworld.cpp" // File source cpp
                    ],
                    "group": {
                        "kind": "build",
                        "isDefault": true
                    }
                }
            ]
        }

  * Nhấn `Ctrl-Shift-B` để compiler, nếu compiler thành công sẽ tạo ra file `a.exe`

  * Debugging your code:

    * Nhấn `F5`: chọn `C++ (GDB/LLDB)` để tạo file `launch.json` trong thư mục `.vscode`

    * Thay đổi nội dung file `launch.json` như sau:

            {
                // Use IntelliSense to learn about possible attributes.
                // Hover to view descriptions of existing attributes.
                // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
                "version": "0.2.0",
                "configurations": [
                    {
                        "name": "(gdb) Launch",
                        "type": "cppdbg",
                        "request": "launch",
                        "program": "${workspaceRoot}/a.exe",
                        "args": [],
                        "stopAtEntry": false,
                        "cwd": "${workspaceRoot}",
                        "environment": [],
                        "externalConsole": true,
                        "MIMode": "gdb",
                        "miDebuggerPath": "C:/MinGW/bin/gdb.exe",
                        "setupCommands": [
                            {
                                "description": "Enable pretty-printing for gdb",
                                "text": "-enable-pretty-printing",
                                "ignoreFailures": true
                            }
                        ],
                        "preLaunchTask": "Build C++"
                    }
                ]
            }

    * Sử dụng cặp `key-value`: `"preLaunchTask": "Build C++"` thì khi build chỉ cần nhấn `F5` (không cần nhấn `Ctrl-Shift-B`).

### Compiler và Debugger

* Compiler: `Ctrl-Shift-B`

* Debugger (and Compiler): `F5`
