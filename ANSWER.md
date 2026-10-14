# ANSWER — ธรรมรัตน์ ไพลสาลี 671540005015-6

- Platform: Vercel
- Production URL: https://ksu-coffee-671540005015-6.vercel.app

## คำตอบ

1. เลือกแพลตฟอร์ม Vercel ซึ่งรันโค้ดด้วยโมเดล Serverless Function (ผ่าน Vercel Build Output API) บน Production ไฟล์ server.js ไม่ได้ถูกรันโดยตรง แต่รหัสการประมวลผลถูกแปลงไปรันใน Serverless Function ของ Vercel แทน
2. ตั้งค่า STUDENT_ID บน Production ที่เมนู Project Settings -> Environment Variables ห้าม commit ไฟล์ .env เพื่อป้องกันความลับหรือความปลอดภัยรั่วไหลสู่ Git Repo สาเหตุที่ /api/info แสดง NOT SET เกิดจากยังไม่ได้ตั้ง Environment Variable ใน Dashboard หรือยังไม่ได้กดยืนยัน/Redeploy เพื่อให้ค่ามีผล
3. ครั้งแรก 0.97 วินาที / ครั้งที่สอง 0.43 วินาที — ต่างกัน เนื่องจากครั้งแรกเป็นการเรียกแบบ Cold Start ที่ระบบ Serverless ต้องเริ่มต้นคอนเทนเนอร์/สภาพแวดล้อมใหม่ ส่วนครั้งที่สองเป็นการเรียกแบบ Warm Start ที่อินสแตนซ์พร้อมทำงานอยู่แล้วจึงตอบสนองได้เร็วขึ้น
4. เมื่อ git push ขึ้น GitHub ตัว Webhook จะแจ้งเตือน Vercel ให้ดึงโค้ดล่าสุดไป Build และ Deploy อัตโนมัติ โดยอัปเดตไฟล์ HTML หน้าเว็บ และฝังรหัส Commit SHA ล่าสุดจาก GitHub เข้าไปในระบบ ทำให้หน้าเว็บเปลี่ยนเป็น Menu v2 และค่า commit ใน /api/info ตรงกับ git log ล่าสุด
5. นำมา deploy แบบตรง ๆ ไม่ได้ เนื่องจากแพลตฟอร์มแบบ Serverless (เช่น Vercel) หรือ PaaS ทั่วไปไม่รองรับการรัน Docker Compose multi-container daemon ในตัว หากต้องการรันระบบที่มี 2 service ต้องแยก deploy เป็น service อิสระ หรือใช้บริการประเภท Container Orchestration / VM เช่น AWS ECS, Render (Multi-service) หรือ Docker Swarm/Kubernetes แทน
