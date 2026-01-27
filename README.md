# F407-Sram
## Tổng quan dự án
<img width="841" height="612" alt="image" src="https://github.com/user-attachments/assets/6432fc08-2683-4d0b-8745-808d8acd9f93" />

  - Sơ đồ khối kết nối
  - Mục tiêu thiết kế:
    - Kết nối STM32F407ZGT6 với Sram 4Mbit thông qua bus FSMC
    - Kết nối với IC Ethernet DP83848 thông qua bus RMII

<br/>

![20260127_230926](https://github.com/user-attachments/assets/88cd19f8-fb93-4895-871f-a5c62b6c14a1)
![20260127_231255](https://github.com/user-attachments/assets/0d77397c-8bca-49bf-a3bb-15c36212c802)

<br/>

<img width="942" height="646" alt="image" src="https://github.com/user-attachments/assets/1de4e8c4-da57-446b-a4d4-4e19aa3b36c3" />

<br/>

<img width="1156" height="656" alt="image" src="https://github.com/user-attachments/assets/0b4652c8-3d75-4166-9378-65d2b6a0aa90" />

<br/>

<img width="999" height="679" alt="image" src="https://github.com/user-attachments/assets/66441bcf-404c-4941-b563-5a624e5b95e7" />


<br/>

<img width="903" height="631" alt="image" src="https://github.com/user-attachments/assets/7b25c892-a123-4970-bc40-8e1c303ae177" />

## Thử nghiệm đọc ghi Sram

Thử bằng phương pháp ghi vào đầy vùng nhớ Sram rồi đọc lại, nếu phát hiện sai do khác lúc ghi thì lỗi sẽ được ghi nhận
(Vì đây là phương pháp thử cơ bản để kiểm tra kết nối giữa MCU và Sram, khi thực hiện phức tạp hơn thì vẫn có lỗi xảy ra)

<img width="447" height="265" alt="image" src="https://github.com/user-attachments/assets/03b0b453-4719-48ff-ab5d-e0447bb5592f" />

