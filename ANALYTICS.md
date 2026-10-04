# ดูสถิติการใช้งานเว็บ (Google Analytics 4)

เว็บเปิดสาธารณะผ่าน GitHub Pages: **https://khuxxondee.github.io/KoreanSnekeFish/**

> ⚠️ **GitHub → Insights → Traffic นับแค่คนที่เข้าหน้า repo** ไม่ได้นับคนที่ใช้เว็บ
> ถ้าอยากรู้ว่ามีคนใช้เว็บกี่คน ต้องดูใน Google Analytics ตามคู่มือนี้

ใน `index.html` ใส่โค้ด GA4 และจุดเก็บ event ไว้แล้ว **เหลือแค่ใส่ Measurement ID ของคุณ** (ตอนนี้ยังเป็น `G-XXXXXXXXXX` เลยยังไม่นับ)

---

## 1) สร้าง Google Analytics (ครั้งเดียว ~10 นาที)

1. เข้า <https://analytics.google.com> → login ด้วย Google account
2. **Admin** (ไอคอนเฟือง ซ้ายล่าง) → **Create → Property**
   - Property name: `koreasnakefish` · Time zone: **Thailand** · Currency: **Thai Baht**
3. ใส่ข้อมูลธุรกิจตามจริง (เลือกอะไรก็ได้ ไม่มีผลกับการนับ)
4. เลือกแพลตฟอร์ม **Web**
   - Website URL: `khuxxondee.github.io` · Stream name: `koreasnakefish web`
   - เปิด **Enhanced measurement** ไว้ (นับการเลื่อนหน้า, คลิกลิงก์ออกนอกเว็บให้อัตโนมัติ)
5. จะเห็น **Measurement ID** หน้าตาแบบ `G-AB12CD34EF` → ก๊อปไว้

## 2) ใส่ ID ในเว็บแล้ว push

เปิด `index.html` หาบรรทัดนี้ (อยู่ใน `<head>` ช่วงบน ๆ):

```js
window.KSF_GA_ID = "G-XXXXXXXXXX";
```
เปลี่ยนเป็น ID ของคุณ เช่น `window.KSF_GA_ID = "G-AB12CD34EF";` แล้ว

```bash
git add index.html
git commit -m "Add Google Analytics ID"
git push
```
รอ GitHub Pages อัปเดต 1–2 นาที

## 3) เช็กว่านับได้แล้ว

1. เปิดเว็บในมือถือหรือเบราว์เซอร์อื่น กดเล่นสัก 2–3 แท็บ
2. GA → **Reports → Realtime** → ต้องเห็น “Users in last 30 minutes” อย่างน้อย 1 และเห็น event เช่น `page_view`, `vocab_open`
3. อยากเห็นทุก event แบบละเอียด: เปิดเว็บด้วย `?ga_debug=1` แล้วดูที่ **Admin → DebugView**

> รายงานปกติ (ไม่ใช่ Realtime) จะมีตัวเลขหลังจากนี้ประมาณ **24–48 ชั่วโมง** — ไม่ต้องตกใจถ้าวันแรกยังว่าง

## 4) ไม่นับตัวเอง

เปิด `https://khuxxondee.github.io/KoreanSnekeFish/?notrack=1` **หนึ่งครั้งในทุกเครื่อง/เบราว์เซอร์ที่คุณใช้** → เครื่องนั้นจะไม่ถูกนับอีก
(อยากให้นับอีกครั้ง: `?notrack=0`) · เปิดไฟล์ในเครื่องตัวเอง (file:// หรือ localhost) ไม่ถูกนับอยู่แล้ว

## 5) ลงทะเบียน custom dimension (ทำครั้งเดียว — สำคัญ)

event ของเว็บส่งรายละเอียดมาด้วย (เช่น คำศัพท์ไหน, โหมดไหน) แต่ GA จะ **ไม่แสดงในรายงานจนกว่าจะลงทะเบียน** และนับเฉพาะข้อมูลหลังลงทะเบียน → ทำทันทีหลังขั้นที่ 2

**Admin → Data display → Custom definitions → Create custom dimension** (Scope = **Event**) สร้างทีละตัว:

| Dimension name (ตั้งเองได้) | Event parameter | ใช้ดู |
|---|---|---|
| Word | `word` | คำศัพท์ที่ถูกเปิดดู |
| Grammar | `grammar` | ไวยากรณ์ที่ถูกเปิดดู |
| Tier | `tier` | ระดับความสำคัญ (A/B/C/D) |
| Section | `section` | ค้นหาจากหน้าไหน (vocab / grammar) |
| Practice mode | `mode` | โหมดแบบฝึกหัด |
| Practice scope | `scope` | ขอบเขตคำ (A / AB / ABC) |
| Flashcard result | `result` | got_it / not_yet |
| Vocab view | `view` | list / card |
| Filter | `filter` | กดตัวกรองอะไร |
| Audio speed | `speed` | normal / slow |

และ **Create custom metric** (Scope = Event, Unit = Standard):

| Metric name | Event parameter |
|---|---|
| Score % | `score_pct` |

> คำค้นหา (`search_term`) GA มี dimension **Search term** ให้อยู่แล้ว

---

## ดูอะไรได้บ้าง — ไปที่เมนูไหน

| อยากรู้ | ไปที่ |
|---|---|
| วันนี้มีคนใช้อยู่ไหม | **Reports → Realtime** |
| มีคนเข้ากี่คน / คนใหม่ vs คนเดิม | **Reports → Reports snapshot** หรือ **Engagement → Overview** |
| **ส่วนไหนของเว็บถูกใช้มากที่สุด** | **Engagement → Pages and screens** (ดูคอลัมน์ *Page title*: Menu / Vocabulary / Grammar / Practice) |
| ฟีเจอร์ไหนถูกกดบ่อย | **Engagement → Events** (ดูตาราง event ด้านล่าง) |
| คนมาจากไหน (Facebook, Google, LINE…) | **Acquisition → Traffic acquisition** |
| ประเทศ / เมือง | **User attributes → Demographic details** |
| มือถือหรือคอม / เบราว์เซอร์ | **Tech → Tech details** |
| คนกลับมาใช้ซ้ำไหม | **Engagement → Retention** (หรือ Explore → Cohort exploration) |
| ใช้เวลาในเว็บนานแค่ไหน | **Engagement → Overview** → *Average engagement time* |

### รายงานเจาะลึก (Explore)
**Explore → Free form** แล้วตั้งค่าแบบนี้:

- **คำศัพท์ที่คนเปิดดูมากที่สุด** → Rows: `Word` · Values: `Event count` · Filter: `Event name` exactly matches `vocab_open`
- **ไวยากรณ์ยอดนิยม** → Rows: `Grammar` · Values: `Event count` · Filter: `Event name` = `grammar_open`
- **คนค้นหาอะไร (และเว็บยังไม่มี)** → Rows: `Search term`, `Section` · Values: `Event count` · Filter: `Event name` = `search`
- **คะแนนแบบฝึกหัดแต่ละโหมด** → Rows: `Practice mode` · Values: `Event count`, `Score %` (ตั้งเป็น average) · Filter: `Event name` = `practice_finish`
- **คนทำแบบฝึกหัดจนจบกี่ %** → เทียบ Event count ของ `practice_start` กับ `practice_finish`

ดูบนมือถือได้ด้วยแอป **Google Analytics** (iOS / Android)

---

## รายการ event ที่เว็บส่ง

| Event | เกิดเมื่อ | พารามิเตอร์ |
|---|---|---|
| `page_view` | เปิดแท็บ Menu / Vocabulary / Grammar / Practice | `page_title` |
| `vocab_open` | กดเปิดดูคำศัพท์ | `word`, `tier`, `word_rank` |
| `grammar_open` | กดเปิดดูไวยากรณ์ | `grammar`, `tier` |
| `search` | พิมพ์ค้นหา (หยุดพิมพ์ 1.5 วิ) | `search_term`, `section` |
| `vocab_filter` | กดตัวกรอง tier / ชนิดคำ / Listening | `filter`, `value` |
| `vocab_view` | สลับ List ↔ Flashcards | `view` |
| `flashcard_grade` | กด Got it / Not yet | `result`, `tier`, `in_session` |
| `practice_start` / `practice_finish` | เริ่ม / ทำแบบฝึกหัดจบ | `mode`, `scope`, `questions`, `score`, `score_pct` |
| `daily_session_start` / `daily_session_complete` | เริ่ม / จบ session ประจำวันในหน้า Menu | `new_words`, `due_words`, `score_pct` |
| `audio_play` | กดฟังเสียง | `speed`, `tab` |

GA เก็บให้เองอัตโนมัติด้วย: `first_visit`, `session_start`, `user_engagement`, `scroll`, `click` (ลิงก์ออกนอกเว็บ)

อยากเพิ่ม event ใหม่: ใน `index.html` เรียก `track("ชื่อ_event", {param: ค่า})` (ชื่อใช้ a–z, 0–9, `_` ไม่เกิน 40 ตัว และห้ามซ้ำชื่อที่ GA สงวนไว้ เช่น `session_start`, `first_visit`)

## ความเป็นส่วนตัว
- ไม่ส่งชื่อ อีเมล หรือข้อมูลส่วนตัวไป GA · GA4 ไม่เก็บ IP address
- footer ของเว็บแจ้งผู้ใช้ว่ามีการใช้ Google Analytics นับแบบไม่ระบุตัวตน
- GA ใช้ cookie — ถ้าวันหนึ่งเว็บโตและอยากทำตาม PDPA เข้มขึ้น ค่อยเพิ่มแบนเนอร์ขอความยินยอม (cookie consent)

## ถ้าผูกโดเมน www.koreasnakefish.com ภายหลัง
ไม่ต้องแก้อะไรใน GA — Measurement ID เดิมใช้ได้กับทุกโดเมน
