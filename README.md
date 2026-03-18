# F407-Sram
## Tổng quan dự án
<img width="841" height="612" alt="image" src="https://github.com/user-attachments/assets/6432fc08-2683-4d0b-8745-808d8acd9f93" />

  - Sơ đồ khối kết nối
  - Mục tiêu thiết kế:
    - Mạch debug STM, yêu cầu thiết lập trở kháng 90 Ohm đối với cổng USB.
    - Mạch USB <-> UART, giao tiếp với STM32.
    - Mạch gắn thẻ SD (sai footprint, không có linh kiện khớp).
    - Kết nối STM32F407ZGT6 với Sram 4Mbit thông qua bus FSMC.
      - Thiết lập trở kháng bus FSMC có giá trị 50 Ohm.
      - Kiểm soát length matching nhỏ nhất có thể (±2mm<).
      - Thêm điện trở nối tiếp để giảm over/undershoot và giảm méo tín hiệu. 
    - Kết nối với IC Ethernet DP83848 thông qua bus RMII (Thất bại).
      - Thiết lập trở kháng cho cổng ETH có giá trị 100 Ohm.
<br/>
<img width="608" height="406" alt="image" src="https://github.com/user-attachments/assets/82d8d18b-c7d7-430c-b1fd-ec1d52fabc15" />

Hình: Kiểm soát length matching(±2mm<)

<img width="637" height="683" alt="image" src="https://github.com/user-attachments/assets/8bb32bc9-315a-4052-a964-605a16c9960f" />

Cách kết nối IC K6R4008V1D:
| Pin Name     | Pin Function       |
|--------------|--------------------|
| A0 - A18     | Address Inputs     |
| WE           | Write Enable       |
| CS           | Chip Select        |
| OE           | Output Enable      |
| I/O1 ~ I/O8  | Data Inputs/Outputs|

  - Được điều khiển bởi các tín hiệu: CS (Chip Select), WE (Write Enable), OE (Output Enable).
  - I/O1–I/O8 tạo thành bus dữ liệu song song 8 bit, hai chiều (bidirectional), dùng cho cả đọc và ghi SRAM tùy theo trạng thái điều khiển.
  - A0–A18 là các đường địa chỉ (19 bit), cho phép truy cập 2¹⁹ = 524,288 địa chỉ, tương ứng dung lượng 4 Mbit (512 KB).

<br/>

![20260127_230926](https://github.com/user-attachments/assets/88cd19f8-fb93-4895-871f-a5c62b6c14a1)
![20260127_231255](https://github.com/user-attachments/assets/0d77397c-8bca-49bf-a3bb-15c36212c802)

Hình: Mạch thi công thực tế
<br/>

<img width="942" height="646" alt="image" src="https://github.com/user-attachments/assets/1de4e8c4-da57-446b-a4d4-4e19aa3b36c3" />

<br/>

<img width="1156" height="656" alt="image" src="https://github.com/user-attachments/assets/0b4652c8-3d75-4166-9378-65d2b6a0aa90" />

<br/>

<img width="999" height="679" alt="image" src="https://github.com/user-attachments/assets/66441bcf-404c-4941-b563-5a624e5b95e7" />


<br/>

<img width="903" height="631" alt="image" src="https://github.com/user-attachments/assets/7b25c892-a123-4970-bc40-8e1c303ae177" />

## Thử nghiệm đọc ghi Sram
<img width="1123" height="478" alt="image" src="https://github.com/user-attachments/assets/038ed791-fa11-497a-98d9-da8b7cdf9562" />
Hình: FMC memory banks (RM0090, Figure 457)

  - Vùng địa chỉ của FMC được chia thành nhiều bank, trong đó Bank 1 (0x6000_0000 → 0x6FFF_FFFF) hỗ trợ các loại bộ nhớ như NOR, PSRAM và SRAM. Đây là vùng được sử dụng để ánh xạ SRAM ngoài trong thí nghiệm.
  - Sử dụng thư viện HAL, thử bằng phương pháp ghi và đọc lại Sram, nếu phát hiện đọc khác ghi thì lỗi sẽ được ghi nhận
(Vì đây là phương pháp thử cơ bản để kiểm tra kết nối giữa MCU và Sram, khi thực hiện phức tạp hơn thì vẫn có lỗi xảy ra)

<br/>

<img width="447" height="265" alt="image" src="https://github.com/user-attachments/assets/03b0b453-4719-48ff-ab5d-e0447bb5592f" />

