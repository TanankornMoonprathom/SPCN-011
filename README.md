# SPCN-011
ขั้นตอนการใช้งานของสร้าง vm and ct on Proxmox cluster

1) Create master vm [ ubuntu-22.04 ]
   - สร้าง master vm มา 1 ตัว แล้วทำการ set ค่าพื้นฐานต่างๆ
   - เช็คเวลาด้วย dateและตset update time ด้วยคำสั่ง sudo timedatectl set-timezone Asia/Bangkok
   - ทำการเปิดใช้งาน ip qemu ด้วยคำสั่ง
       - sudo -i
       - apt update
       - apt install qemu-guest-agent
       - systemctl enable qemu-guest-agent
       - และทำการตั้งค่าที่ option ให้เปิดใช้งานตัว Qemu guest agent เป็น Enable 
       ![image](https://user-images.githubusercontent.com/119097663/208229102-b0e420d0-5d6d-4f31-9463-aa16c395178b.png)
       - reboot เพื่อรีระบบ
   1.1) clone from template 2 vm
   - Click ที่ vm(master) > Convert to template
   -  หลังจาก vm(master) กลายเป็นtemplate ให้ Click vm แล้วเลือก Clone เป็นตัวvmใหม่2ตัว
   
      ![image](https://user-images.githubusercontent.com/119097663/208229128-de003402-d69a-4f08-b990-15edbfa3f875.png)   
   - ทำการsetระบบโดย
        - date เพื่อเช็ค timezone
          ![date](https://user-images.githubusercontent.com/117428887/207250064-7dbee734-ba17-4e07-8c8e-bfc448aed275.png) 
        - ทำการเปลี่ยนipของระบบเพื่อไม่ให้ipซ้ำกันโดย
            - sudo -i
            - rm /var/lib/dbus/machine-id
            - nano /etc/machine-id เพื่อลบ id เก่าออก
            - ln -s /etc/machine-id /var/lib/dbus/machine-id เพื่อ link เชื่อมต่อกับ machine-id
            - reboot เพื่อรี ip ใหม่
            - หลังเปลี่ยน ip clone1
              ![image](https://user-images.githubusercontent.com/119097663/208229163-453845a2-f86e-4d9c-b448-04e1c0df3e53.png)
            - หลังเปลี่ยน ip clone2
              ![image](https://user-images.githubusercontent.com/119097663/208229177-60044e3e-c29d-4a06-abfe-cceab1f204c7.png)
 
2) create vm from other os
   - Create VM จากนั้นทำการตั้งค่าที่กำหนดโดยระบบปฏิบัติการที่เลือกใช้คือ linux mint
      - Summary ของ Linux Mint
        ![image](https://user-images.githubusercontent.com/119097663/208229764-6fba4fc4-1e11-465e-bc4e-035d1340f521.png)
      - หน้า console screen
        ![image](https://user-images.githubusercontent.com/119097663/208229809-b6104ab4-5f3e-43b2-8290-10fdb60a0a23.png)  

3) create container template 
   - Click create container template เพื่อสร้าง CT
      - Summary 
        ![image](https://user-images.githubusercontent.com/119097663/208229844-76266e40-45a3-4b65-8ece-3e0a1d0d8b1d.png)
      - console screen 
        ![image](https://user-images.githubusercontent.com/119097663/208230031-529f330b-a87e-4746-afbb-e451c0b8524c.png)
