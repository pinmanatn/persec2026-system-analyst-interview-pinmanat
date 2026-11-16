# แบบทดสอบ — ปิ่นมนัส น่านกาศ

คำตอบแบบทดสอบทั้ง 4 สถานการณ์ พร้อมรายการ Prompt ที่ใช้กับ AI

## ไฟล์ใน Repository

| ไฟล์ | เนื้อหา |
|---|---|
| [scenario-1.md](scenario-1.md) | **Flash Sale แจกคูปอง 1,000 สิทธิ์** — High-Level Architecture, Tech Stack และการแก้ปัญหา Race Condition |
| [scenario-2.md](scenario-2.md) | **การ Mentor Junior Developer** — แนวทางจากประสบการณ์จริง |
| [scenario-3.md](scenario-3.md) | **แจกคูปอง 100 สิทธิ์ ผู้ใช้หลักหมื่นคน** — การปกป้อง Database และป้องกัน Overbooking |
| [scenario-4.md](scenario-4.md) | **การ Hardcode API Key และ URL ของ 3rd-party** — ผลกระทบ แนวทางแก้ไข และการป้องกัน |
| [prompts.md](prompts.md) | Prompt ที่ใช้กับ AI ในแต่ละข้อและแต่ละขั้นตอน |

## สรุปแนวทางหลัก

**สถานการณ์ที่ 1 และ 3 (Flash Sale)**
- Go Modular Monolith (Clean Architecture) บน AWS ใช้ Managed services ทั้งหมด
- Redis Lua script ตัดสินสิทธิ์และส่ง event เข้า Queue แบบ atomic → ไม่มี race condition ไม่แจกเกิน ไม่ซ้ำ
- กรอง traffic ทีละชั้นก่อนถึง Database → PostgreSQL รับแค่จำนวนแถวเท่ากับจำนวนสิทธิ์
- PostgreSQL UNIQUE constraint เป็นด่านสุดท้าย

**สถานการณ์ที่ 2 (Mentoring)** — ใช้คำถามนำให้น้องคิดและ Debug เอง อธิบายเหตุผลและผลกระทบ แล้วให้น้องสรุปสิ่งที่เรียนรู้

**สถานการณ์ที่ 4 (Hardcode Secret)** — คุยแบบไม่ตำหนิ แยกความเสี่ยงของ API Key (Security) กับ URL (Maintenance/Configuration) จัดการ Key ที่หลุด และวางแนวทางป้องกันด้วย Secret Manager และ Secret Scanning

## การดู Diagram

`scenario-1.md` และ `scenario-3.md` มี Diagram ที่เขียนด้วย [Mermaid](https://mermaid.js.org/) ซึ่ง GitHub และ GitLab แสดงเป็นภาพให้อัตโนมัติ
หากเปิดใน VS Code หรือ Cursor ให้ติดตั้ง extension **Markdown Preview Mermaid Support** หรือคัดลอกโค้ดไปเปิดที่ [mermaid.live](https://mermaid.live)

## การใช้ AI

ใช้ Claude ช่วยออกแบบ ตั้งคำถามหาจุดที่ตกหล่น และเรียบเรียงเอกสาร และใช้ ChatGPT รีวิวคำตอบสถานการณ์ที่ 1
การตัดสินใจด้านธุรกิจและแนวทางหลักมาจากผู้เขียนเอง รายละเอียด Prompt ทั้งหมดอยู่ใน [prompts.md](prompts.md)
