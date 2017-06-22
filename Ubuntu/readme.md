# Sử dụng Visual Studio Code và PlatformIO trên Ubuntu 16.04

* **Tổng hợp:** Thi Minh Nhựt - **Email:** thiminhnhut@gmail.com

* **Thời gian:** Ngày 31 tháng 05 năm 2017

# Tài liệu tham khảo

1. [Instal PlatformIO Core](http://docs.platformio.org/en/stable/installation.html)

2. [PlatformIO](https://marketplace.visualstudio.com/items?itemName=formulahendry.platformio)

3. [PlatformIO User Guide](http://docs.platformio.org/en/stable/userguide/index.html)

## Cài đặt Visual Studio Code trên Ubuntu

* Tải phiên bản 32 bit hoặc 64 bit dành cho Ubuntu từ địa chỉ: https://code.visualstudio.com/download

* Tải về tiến hành cài đặt bình thường trên hệ điều hành Ubuntu (file .deb).

## Cài đặt nhanh các thư viện trong Visual Studio Code

* Sử dụng phím tắt: `Ctrl + P` và gõ lệnh `ext install tên_thư_viện`.

## Sử dụng Visual Studio Code để lập trình cho vi điều khiển

### Cài đặt PlatformIO Core

* Cho phép user (khác user `root`) truy cập vào cổng `USB/UART` để giao tiếp 
với vi điều khiển:

		sudo usermod -a -G dialout yourusername

	với `yourusername` là tên của user cần thêm vào quyền truy cập.

* Cài đặt `udev`: làm theo hướng dẫn trong file [99-platformio-udev.rules](https://github.com/platformio/platformio-core/blob/develop/scripts/99-platformio-udev.rules)

	+ Tải file [99-platformio-udev.rules](https://github.com/platformio/platformio-core/blob/develop/scripts/99-platformio-udev.rules): [Download](https://github.com/platformio/platformio-core/blob/develop/scripts/99-platformio-udev.rules)
	
	+ Đặt file `99-platformio-udev.rules` vào một trong các thư mục bên dưới: 
	
			/etc/udev/rules.d/99-platformio-udev.rules
			
		hoặc
			
			/lib/udev/rules.d/99-platformio-udev.rules
			
	+ Dùng lệnh:
	
			sudo cp 99-platformio-udev.rules /etc/udev/rules.d/99-platformio-udev.rules
		
		hoặc:
		
			sudo cp 99-platformio-udev.rules /lib/udev/rules.d/99-platformio-udev.rules
			
	+ Restart `udev`:
	
			sudo service udev restart
			
		hoặc:
			
			sudo udevadm control --reload-rules
			
			sudo udevadm trigger
			
	+ Sau khi cài đặt xong rút USB và kết nối lại với vi điều khiển.
	
* Cài đặt PlatformIO: chọn một trong các cách sau đây để cài đặt PlatformIO

	+ Sử dụng `Python Package Manager`:
	
			sudo pip install -U platformio
			
	+ Sử dụng `Script`:
	
		- Tải file [get-platformio.py](https://raw.githubusercontent.com/platformio/platformio/master/scripts/get-platformio.py): [Download](get-platformio.py)
		
		- Cài đặt theo một trong hai cách sau:
		
				sudo python -c "$(curl -fsSL https://raw.githubusercontent.com/platformio/platformio/master/scripts/get-platformio.py)"
				
			hoặc:
			
				sudo python get-platformio.py
				
### Chọn board cho PlatformIO

* Xem mã ID tại địa chỉ [Embedded Boards](http://docs.platformio.org/en/stable/platforms/embedded_boards.html)

* Hoặc sử dụng lệnh:

		platformio boards

### Tạo project mới với PlatformIO

* Tạo project trong thư mục hiện tại:

		platformio init
		
* Tạo project trong thư mục cụ thể khác:

		platformio init -d %PATH_TO_DIR%
		
* Tạo project với Arduino Uno:

		platformio init --board uno
		
	Thay `uno` bằng `ID` của board tương ứng được mô tả trong [Embedded Boards](http://docs.platformio.org/en/stable/platforms/embedded_boards.html).

### Sử dụng PlatformIO để buil và upload code cho vi điều khiển

* Sử dụng giao diện

|No. |Comand                                                         |Shortcut  |F1                                               |Text Editor                    |Symbol     |
|----|---------------------------------------------------------------|----------|-------------------------------------------------|-------------------------------|-----------|
|1   |Build PlatformIO project                                       |Ctrl+Alt+B||PlatformIO: Build                               |PlatformIO: Build              |           |
|2   |Upload firmware to devices                                     |Ctrl+Alt+U|PlatformIO: Upload                               |PlatformIO: Upload             |           |
|3   |Open Serial Monitor                                            |Ctrl+Alt+S|PlatformIO: Open Serial Monitor                  |PlatformIO: Open Serial Monitor|           |
|4   |Search for library                                             |          |PlatformIO: Search Library                       |                               |Library    |
|5   |Install library                                                |          |PlatformIO: Install Library                      |                               |Download   |
|6   |Quick way to open PlatformIO Terminal                          |          |PlatformIO: Open Terminal                        |                               |Terminal   |
|7   |Add Include Path to c_cpp_properties.json for C/C++ extension  |          |PlatformIO: Add Include Path to Settings         |                               |           |
|8   |Combined Build, Upload and Open Serial Monitor with one command|Ctrl+Alt+A|PlatformIO: Build, Upload and Open Serial Monitor|                               |Right Arrow|

* Sử dụng lệnh trong Terminal:

	+ Buil project:
	
			sudo platformio run
			
	+ Upload project:
	
			sudo platformio run --target upload
			
	+ Mở Serial Minotor: thay `9600` thành tốc độ `baud` phù hợp.
	
			sudo platformio device monitor --baud 9600
