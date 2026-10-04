# koreasnakefish — TOPIK I

🌐 **เว็บ:** https://khuxxondee.github.io/KoreanSnekeFish/

เว็บเตรียมสอบ TOPIK I: คำศัพท์และไวยากรณ์เรียงตามความถี่ในข้อสอบจริง 10 ชุด พร้อมความหมายไทย/อังกฤษ เสียงอ่าน แฟลชการ์ด และแบบฝึกหัด

ทั้งเว็บอยู่ใน `index.html` ไฟล์เดียว (หน้าเว็บ + โค้ด + ข้อมูล) — ไม่ต้อง build ไม่ต้องมีเซิร์ฟเวอร์

## ไฟล์ใน repo
| ไฟล์ | คืออะไร |
|---|---|
| `index.html` | ตัวเว็บทั้งหมด |
| `CREDITS.md` | แหล่งข้อมูลและเครดิต |
| `.gitignore` | กันไม่ให้ไฟล์ส่วนตัว (`private/`) ขึ้น GitHub |

## อัปเดตเว็บ
แก้ `index.html` แล้วรันใน PowerShell:
```
cd D:\project\KoreanSnekeFish
git add .
git commit -m "update"
git push
```
GitHub Pages จะอัปเดตเว็บเองภายใน 1–2 นาที

## GitHub Pages (ตั้งไว้แล้ว)
- Settings → Pages → Source: **Deploy from a branch** → `main` / `(root)`
- ผูกโดเมน `www.koreasnakefish.com` (ยังไม่ได้ทำ): ใส่ใน Custom domain → ที่ผู้ให้บริการโดเมนเพิ่ม DNS `CNAME` · Name `www` · Value `khuxxondee.github.io` → พอ DNS ใช้ได้ติ๊ก **Enforce HTTPS**

## ข้อมูลในเว็บ
อยู่ในแท็ก `<script id="data" type="application/json">` ของ `index.html`
สร้างจาก notebooks ใน `private/topik1-analysis/` ซึ่งเก็บไว้ในเครื่องเท่านั้น ไม่ขึ้น GitHub (ดู `.gitignore`)

## เครดิต
ดู [CREDITS.md](CREDITS.md) — รายการคำศัพท์/ไวยากรณ์ © Tammy Korean (learning-korean.com) · ข้อสอบ © 국립국제교육원 (NIIED) · ความหมายไทยอ้างอิง krdict (CC BY-SA 2.0 KR)
