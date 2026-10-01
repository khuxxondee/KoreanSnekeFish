# koreasnakefish — TOPIK I

เว็บเตรียมสอบ TOPIK I: คำศัพท์และไวยากรณ์เรียงตามความถี่ในข้อสอบจริง 10 ชุด พร้อมความหมายไทย/อังกฤษ เสียงอ่าน แฟลชการ์ด และแบบฝึกหัด

ทั้งเว็บอยู่ใน `index.html` ไฟล์เดียว (หน้าเว็บ + โค้ด + ข้อมูล) — ไม่ต้อง build ไม่ต้องมีเซิร์ฟเวอร์

## ขึ้นเว็บด้วย GitHub Pages
1. Push repo นี้ขึ้น GitHub (ตั้งเป็น **Public**)
2. Settings → Pages → Source: **Deploy from a branch** → Branch: `main` / `(root)` → Save
3. Custom domain: `www.koreasnakefish.com` → Save
4. ที่ผู้ให้บริการโดเมน เพิ่ม DNS: `CNAME` · Name `www` · Value `<username>.github.io`
5. เมื่อ DNS ใช้ได้ ติ๊ก **Enforce HTTPS**

อัปเดตเว็บ: แก้ `index.html` → `git add . && git commit -m "update" && git push`

## Google Analytics
วางโค้ด GA (gtag.js) ไว้ใน `<head>` ของ `index.html` ก่อน push

## ข้อมูลในเว็บ
อยู่ในแท็ก `<script id="data" type="application/json">` ของ `index.html`
สร้างจากโปรเจกต์ `topik1-analysis` (เก็บใน repo **private** แยกต่างหาก — ดู `.gitignore`)

## เครดิต
ดู [CREDITS.md](CREDITS.md) — รายการคำศัพท์/ไวยากรณ์ © Tammy Korean (learning-korean.com) · ข้อสอบ © 국립국제교육원 (NIIED) · ความหมายไทยอ้างอิง krdict (CC BY-SA 2.0 KR)
