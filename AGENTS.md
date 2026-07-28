# 🤖 KLLC AI_OS — SYSTEM BRIEFING
### สำหรับ: Codex · Qwen · Antigravity · AI ทุกตัวที่เข้าทำงานในระบบนี้
> **อัปเดตล่าสุด: 2026-07-21**  
> อ่านให้ครบก่อนเริ่มงานทุกครั้ง ห้ามข้าม

---

## ⚠️ สิ่งที่เปลี่ยนไปล่าสุด (Critical Changes)

> [!IMPORTANT]
> โครงสร้าง Google Drive เปลี่ยนใหม่ทั้งหมดเมื่อ **2026-07-21**  
> Path เก่าทั้งหมดที่ขึ้นต้นด้วย `J:\My Drive\AI_OS\` **ใช้ไม่ได้แล้ว**  
> ใช้ path ใหม่ที่ขึ้นต้นด้วย `J:\My Drive\KLLC\` เท่านั้น

---

## 1. เจ้าของระบบ (Owner)

| รายการ | ค่า |
|---|---|
| ชื่อ | Wiphas (วิภาส) |
| Email | wiphas.on@kmitl.ac.th |
| Telegram Chat ID | `1663536770` |
| องค์กร | ห้องสมุด KMITL (KLLC) |

---

## 2. โครงสร้าง Google Drive (Current Structure)

```
J:\My Drive\KLLC\                        ← ROOT ใหม่ (2026-07-21)
│
├── 00_KLLC_INBOX\                       ← 📥 INBOX หลัก
│   ├── AV\                              ← อัปโหลดภาพ/เอกสาร AV ที่นี่
│   ├── CCTV\                            ← อัปโหลดภาพ/เอกสาร CCTV ที่นี่
│   └── DOCS\                            ← TOR, ใบเสนอราคา, ใบเสร็จ, คู่มือ
│
├── 01_OPERATIONS\                       ← ✅ ไฟล์ที่ AI จัดเก็บแล้ว
│   ├── 01_AV\                           ← AV System, Equipment, Network
│   ├── 02_CCTV\                         ← CCTV
│   ├── 03_ROOMS_SPACES\                 ← Meeting Room, Library
│   ├── 04_CHECKLISTS\                   ← Checklist
│   └── 05_INCIDENTS_MA\                 ← Maintenance, MA, Contracts, TOR
│
├── 02_MEETINGS\                         ← บันทึกการประชุม
├── 03_PROJECTS\                         ← โปรเจค
├── 04_MEDIA_CONTENT\                    ← สื่อ/ภาพ
├── 05_AI_AUTOMATION\                    ← 🤖 Pipeline & Scripts (ดูหัวข้อ 3)
├── 06_FINANCE_ADMIN\                    ← การเงิน/บริหาร
├── 07_REFERENCE\                        ← เอกสารอ้างอิง
├── 08_REPORTS\                          ← รายงาน
├── 99_ARCHIVE\                          ← Archive
└── 99_REVIEW_REQUIRED\                  ← รอตรวจสอบ
```

---

## 3. AI Pipeline (05_AI_AUTOMATION)

### ไฟล์สำคัญ
```
J:\My Drive\KLLC\05_AI_AUTOMATION\
├── ai_document_pipeline.py              ← 🤖 Pipeline หลัก (ห้ามแก้โดยไม่ได้รับอนุญาต)
├── run_daemon.bat                       ← รัน daemon (ดับเบิลคลิกได้)
├── daemon_log.txt                       ← Log (อ่านเพื่อ debug)
├── KLLC_Asset_DB.xlsx                   ← ฐานข้อมูล Excel
└── my-tts-project-465902-51299934f336.json  ← Service Account Key (ห้ามลบ/ย้าย)
```

### การทำงาน
1. **Daemon รันทุก 60 วินาที** ใน background
2. สแกน inbox **4 จุด** พร้อมกัน:
   - `00_KLLC_INBOX\AV\`
   - `00_KLLC_INBOX\CCTV\`
   - `00_KLLC_INBOX\DOCS\`
   - `00_KLLC_INBOX\` (root — ไฟล์ที่ drop ลงตรงๆ)
3. ส่งให้ **Gemini 2.5 Flash** วิเคราะห์ + OCR
4. ย้ายไฟล์ไปยัง `01_OPERATIONS/{โฟลเดอร์ที่เหมาะสม}/`
5. บันทึกลง **Excel** + **Google Sheet**
6. ส่ง **Telegram** แจ้งเจ้าของ

### รัน Daemon ใหม่ (ถ้าหยุด)
```powershell
Start-Process -FilePath "C:\Users\Administrator\AppData\Local\Python\bin\python.exe" `
  -ArgumentList '"J:\My Drive\KLLC\05_AI_AUTOMATION\ai_document_pipeline.py" --loop' `
  -WindowStyle Hidden
```

### Business_Node → โฟลเดอร์ปลายทาง
| Business_Node | โฟลเดอร์ |
|---|---|
| AV_System, Equipment, Network, Procurement | `01_OPERATIONS\01_AV\` |
| CCTV | `01_OPERATIONS\02_CCTV\` |
| Meeting_Room, Library | `01_OPERATIONS\03_ROOMS_SPACES\` |
| Maintenance, MA, Contracts, TOR | `01_OPERATIONS\05_INCIDENTS_MA\` |

---

## 4. Credentials & Keys

> [!CAUTION]
> ห้าม commit หรือแชร์ข้อมูลด้านล่างนี้

| รายการ | ตำแหน่ง |
|---|---|
| Gemini API Key | `C:\Users\Administrator\.env` → `GEMINI_API_KEY` |
| DeepSeek API Key | `C:\Users\Administrator\.env` → `DEEPSEEK_API_KEY` |
| Service Account JSON | `J:\My Drive\KLLC\05_AI_AUTOMATION\my-tts-project-465902-51299934f336.json` |
| Service Account Email | `kllc-operations-hub@my-tts-project-465902.iam.gserviceaccount.com` |

### Google Sheet
- **Sheet ID:** `1nMQEaYYig2gPIysLXif3t0vvYP0at9XwIzccuDJpoio`
- **Tab:** `Sheet1`
- **URL:** `https://docs.google.com/spreadsheets/d/1nMQEaYYig2gPIysLXif3t0vvYP0at9XwIzccuDJpoio/`

> [!WARNING]
> Sheet ID มี **`I` (ตัวใหญ่)** ไม่ใช่ `l` (ตัวเล็ก) — เคยทำให้ error 404 มาแล้ว  
> ตรวจสอบจาก URL จริงทุกครั้งที่แก้ไข

---

## 5. Python Environment

```
Python:   C:\Users\Administrator\AppData\Local\Python\bin\python.exe
Version:  3.14 (pythoncore-3.14-64)
```

Packages ที่ต้องใช้ (ติดตั้งแล้ว):
`google-generativeai` · `google-auth` · `google-api-python-client` · `pdfplumber` · `openpyxl` · `Pillow`

> [!IMPORTANT]
> **ห้ามสร้าง `.venv` ใน `J:\My Drive\`** ทุกกรณี  
> ถ้าต้องการ venv ให้สร้างใน `C:\` เท่านั้น  
> `.venv` ใน Drive = sync ไฟล์นับพันโดยไม่จำเป็น (เคยเกิดแล้ว)

---

## 6. Google Apps Script (ที่ติดอยู่กับ Google Sheet)

> [!WARNING]
> มี error ซ้ำ **288 ครั้ง** ตั้งแต่ 2026-07-19 เนื่องจาก `SpreadsheetApp.getUi()` ถูกเรียกใน time-based trigger

**กฎเหล็กของ Apps Script:**
- `SpreadsheetApp.getUi()` → ใช้ได้เฉพาะใน `onOpen()` และ `onEdit()` **เท่านั้น**
- **ห้ามเรียก** `getUi()` ในฟังก์ชันที่รันจาก time-based trigger เด็ดขาด
- ใช้ `Logger.log()` หรือ `appendRow()` แทนใน trigger functions

**โค้ดที่แก้ไขแล้ว:** ให้เปิด Google Sheet → Extensions → Apps Script → วางโค้ดจากไฟล์ที่ AI Antigravity เตรียมไว้ → รัน `setupTrigger()`

---

## 7. กฎสำหรับ AI ทุกตัว

### ✅ ต้องทำ
- อ่านไฟล์ `AGENTS.md` นี้ก่อนเริ่มงาน **ทุกครั้ง**
- ตรวจสอบ `daemon_log.txt` ก่อน debug
- ใช้ **path ใหม่** `J:\My Drive\KLLC\` เสมอ
- Backup script ก่อนแก้ไขทุกครั้ง
- Kill daemon เก่าก่อน start ใหม่
- เมื่อแก้ไข pipeline → copy ไปที่ `05_AI_AUTOMATION\ai_document_pipeline.py`

### ❌ ห้ามทำ (เด็ดขาด)
- **ห้ามใช้ path เก่า** `J:\My Drive\AI_OS\...` — path นั้นหายไปแล้ว
- **ห้ามลบไฟล์ใน `01_OPERATIONS\`** โดยไม่ได้รับอนุญาต
- **ห้ามสร้าง `.venv` ใน `J:\My Drive\`**
- **ห้ามเรียก `getUi()` ใน Apps Script trigger**
- **ห้ามแก้ไข Sheet ID** โดยไม่ตรวจสอบ URL จริงก่อน
- **ห้ามแชร์ Google Sheet แบบ Public**
- **ห้าม hardcode credentials** ลงใน script — ใช้ `.env` เท่านั้น

---

## 8. ปัญหาที่เคยเกิดและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|---|---|---|
| Path not found | ใช้ path เก่า `AI_OS\...` | เปลี่ยนเป็น `J:\My Drive\KLLC\...` |
| Google Sheet 404 | Sheet ID มี `l` แทน `I` | ดู URL จริง แก้ตรงตัวอักษร |
| Apps Script error 288 ครั้ง | `getUi()` ใน trigger | ลบ `getUi()` ออกจาก trigger functions |
| SA JSON not found | ถูก archive ไปพร้อม cleanup | ใช้ path ใหม่: `05_AI_AUTOMATION\*.json` |
| ไฟล์ inbox ไม่ถูก process | Daemon หยุด / path เก่า | รัน daemon ใหม่ด้วย path ใหม่ |
| `.venv` พันโฟลเดอร์ใน Drive | สร้าง `.venv` ใน `J:\` โดยตั้งใจ | ลบ `.venv` ทั้งหมด ใช้ `C:\` แทน |
| Gemini 429/503 | Rate limit | Pipeline retry อัตโนมัติ 4 ครั้ง |
| `J:\` unmount | GoogleDriveFS.exe หยุด | Restart process |

---

## 9. Metadata Fields (AI สกัดจากไฟล์)

| Field | ความหมาย | Default |
|---|---|---|
| `category` | AV / CCTV | ตาม inbox |
| `brand_model` | ยี่ห้อ/รุ่น | `ไม่ระบุ` |
| `asset_id` | เลขครุภัณฑ์ | `ไม่มี` |
| `location` | สถานที่ | `ไม่ระบุ` |
| `status_note` | สถานะ | `ต้องตรวจสอบ` |
| `Date` | YYYY-MM-DD (CE) | วันที่ไฟล์ถูกสร้าง |
| `Doc_Type` | ประเภทเอกสาร | `Photo_Evidence` |
| `Business_Node` | โฟลเดอร์ปลายทาง | `AV_System` |
| `Vendor_Name` | ผู้ขาย | `Unknown` |
| `Amount` | มูลค่า (บาท) | `0.0` |
| `Summary` | สรุปย่อภาษาไทย 1 ประโยค | — |

**รูปแบบชื่อไฟล์หลังประมวลผล:**  
`{Date}_{Doc_Type}_{Project}_{Vendor}{ext}`  
ตัวอย่าง: `2026-07-21_Photo_Evidence_KLLC_ITFocus.jpg`

---

## 10. Changelog

| วันที่ | รายการ |
|---|---|
| **2026-07-21** | Drive restructure: path ย้ายจาก `AI_OS\` → `KLLC\` / แก้ SA JSON path / แก้ Apps Script error 288 ครั้ง / อัปเดต pipeline ทั้งหมด |
| 2026-07-17 | แก้ Sheet ID (`l`→`I`), เพิ่ม DOCS inbox, ลบ .venv/ขยะ, แก้ loop ซ้ำซ้อน |
| 2026-07-14 | สร้าง daemon loop, เพิ่ม fallback, ปรับ interval |
| 2026-07-13 | เริ่มต้นระบบ, สร้างโฟลเดอร์, ทดสอบ pipeline ครั้งแรก |

---

> **อัปเดตไฟล์นี้ทุกครั้งที่มีการเปลี่ยนแปลงระบบสำคัญ**  
> Path: `J:\My Drive\KLLC\AGENTS.md`
