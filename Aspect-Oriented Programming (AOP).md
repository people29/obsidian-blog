##### Aspect-Oriented Programming (AOP)

แนวคิดการเขียนโปรแกรมที่ช่วยให้เราแยก "สิ่งที่ต้องทำซ้ำๆ" ออกจาก business code

ลองนึกภาพงานทั่วไป เช่น:
> - การบันทึกข้อมูล (Logging): ทุกครั้งที่ฟังก์ชันทำงาน, มีการเข้า/ออก, หรือเกิดข้อผิดพลาด ต้องเขียนโค้ดบันทึกทุกที่
> - การตรวจสอบสิทธิ์ (Security): ก่อนเข้าถึงข้อมูลสำคัญ ต้องเช็คสิทธิ์ของผู้ใช้ทุกครั้ง

งานเหล่านี้เรียกว่า "ความกังวลแบบข้ามผ่าน" (Cross-cutting Concerns) เพราะมันกระจายอยู่ทั่วโค้ด ทำให้:
> - โค้ดหลักดูรกและเข้าใจยาก
> - เกิดโค้ดซ้ำซ้อน
> - แก้ไขยาก หากต้องการเปลี่ยนวิธี Log หรือตรวจสอบสิทธิ์

**แนวคิดของการทำงาน:**
> 1. ดึง "ความกังวล" (Concerns) เหล่านี้ออกมาเป็นโมดูลพิเศษ เรียกว่า **"Aspect" (แง่มุม)**
> 2. ระบุว่า Aspect นี้จะ **"ทำอะไร" (Advice)** และ **"ตรงไหนในโค้ด" (Join Point/Pointcut)** เช่น "ก่อนเรียกทุกฟังก์ชันของ Service"
> 3. แล้วระบบจะ "ถักทอ เรียบเรียง" (Weaving) Aspect เหล่านั้นเข้ากับโค้ดหลักให้เองโดยอัตโนมัติ


**ผลลัพธ์คือ:** business code จะดู clean ขึ้น มีแค่ logic การทำงานจริงๆ ทำให้ดูแลและแก้ไขได้ง่าย