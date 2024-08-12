* Đầu tiên sẽ kiểm tra file thuộc loại nào
![image](https://github.com/user-attachments/assets/b0e02357-e9a2-457b-8f44-6e2e20b3fb18)
* Sau đó dùng ida để đọc pseudo code của file này
![image](https://github.com/user-attachments/assets/465a7a7a-1107-4e08-8280-636face43183)
* Ta thấy nó khởi tạo 5 biến include : buf,v5,v6,v7,v8
* Tiếp theo là set null cho 4 biến v5,v6,v7,v8
![image](https://github.com/user-attachments/assets/8e5ea8f0-834d-4a6e-971c-5058b63d96f0)
* Ở dòng 15 ta thấy nó read 48 byte trong khi biến buff chỉ khai báo 16 byte như vậy byte thứ 17 sẽ tràn xuống v5.
* Nhìn ở dòng if ta thấy nếu 3 biến v5,v6,v7 khác không thì nó sẽ tạo cho mình 1 cái shell
* Thì đấy chính là mục tiêu của chúng ta. Nhập vào từ biến buff để nó tràn xuống các biến v5,v6,v7 thì 3 biến này sẽ khác không và hoàn thành thử thách này.
![image](https://github.com/user-attachments/assets/d24501bb-1b53-45ea-b079-3f65b8cb3533)
