# 🛡 Dynamic Watermark Overlay for Live Streaming (TikTok LIVE Studio & OBS)

Web-based Dynamic Overlay สำหรับสร้างลายน้ำโปร่งแสงแบบลอยสุ่มพิกเซล (Random Floating Watermark) นำ URL ไปใส่ใน **Browser Source / Link Source** ของ **TikTok LIVE Studio** และ **OBS Studio** ได้ทันทีโดยไม่ต้องเปิดโปรแกรมค้างไว้ในเครื่อง

---

## ✨ ฟีเจอร์เด่น (Key Features)

1. **Anti-Looping & Anti-Reuse (แก้ปัญหา AI จับคลิปวน / ไลฟ์ซ้ำ):**
   - มีโหมด **Real-time Clock** แสดงเวลาระดับมิลลิวินาที ทำให้ทุกเฟรมมีค่าพิกเซลเปลี่ยนแปลงตลอดเวลา (Pixel Entropy)
   - ฟังก์ชัน **Anti-Loop Forensic Token** เปลี่ยนชุดรหัสสุ่มในระดับ Micro-hash ทุกวินาที ตัดปัญหาการถูก AI แพลตฟอร์มตรวจจับ Spatio-temporal Hash
2. **Smooth Random Floating (การเคลื่อนที่สุ่มแบบนุ่มนวล):**
   - คำนวณพิกัดสุ่ม X, Y ภายในขอบเขตหน้าจออัตโนมัติ (รองรับทั้งแนวตั้ง 1080x1920 และแนวนอน 1920x1080)
   - เคลื่อนที่ด้วย CSS GPU Acceleration (`translate3d` + `cubic-bezier`) แบบ 60fps ไม่กระตุก ไม่วาร์ป
3. **100% Transparent & Non-intrusive (โปร่งแสงและไม่บังการคลิก):**
   - พื้นหลังโปร่งใสสนิท ไม่มี Scrollbar
   - ค่าความโปร่งแสงต่ำ (10% - 20% แนะนำ) กลมกลืน ไม่กวนสายตาผู้ชม
   - กำหนด `pointer-events: none` ไม่ขัดขวางการคลิกปุ่มบนหน้าจอ
4. **Visual Studio & URL Generator (`index.html`):**
   - มีหน้าแดชบอร์ดตั้งค่าแบบโต้ตอบ พร้อมหน้าจอจำลอง (Mock UI) ของ TikTok LIVE
   - ปรับแต่งสไลเดอร์แล้วกด **"📋 คัดลอก Link Source"** นำไปวางในโปรแกรมไลฟ์ได้ทันที

---

## 🚀 โครงสร้างไฟล์ในโปรเจกต์

```text
watermark/
├── overlay.html     # หน้าแสดงผลลายน้ำแบบ Overlay บริสุทธิ์ (สำหรับ TikTok LIVE / OBS)
├── index.html       # แดชบอร์ด Studio สำหรับปรับแต่งและสร้างลิงก์ URL อัตโนมัติ
├── vercel.json      # การตั้งค่าสำหรับโฮสต์ขึ้น Vercel แบบ 1-Click
└── README.md        # เอกสารคู่มือการติดตั้งและการใช้งาน
```

---

## 🌐 วิธีนำขึ้นเว็บโฮสติ้งฟรี (Free Public Hosting)

เลือกช่องทางที่สะดวกได้ตามนี้ครับ:

### วิธีที่ 1: GitHub Pages (แนะนำ ง่ายและฟรีตลอดชีพ)
1. นำโฟลเดอร์นี้อัปขึ้น GitHub Repository ของคุณ (ตั้งชื่อเช่น `dynamic-watermark`)
2. เข้าไปที่ **Settings** ของ Repository บน GitHub
3. ไปที่เมนู **Pages** (แถบด้านซ้าย)
4. ในส่วน **Build and deployment > Branch** เลือก `main` หรือ `master` และโฟลเดอร์ `/ (root)` แล้วกด **Save**
5. รอ 1 นาที จะได้ URL เช่น:
   `https://<your-username>.github.io/<repo-name>/overlay.html`

### วิธีที่ 2: Vercel (เร็วและเสถียรมาก)
1. สมัครใช้งาน [Vercel.com](https://vercel.com) (ฟรี)
2. ลากโฟลเดอร์โปรเจกต์นี้ไปวาง (Deploy) หรือเชื่อมต่อผ่าน GitHub Repo
3. จะได้ URL สาธารณะทันที เช่น `https://my-watermark.vercel.app/overlay.html`

### วิธีที่ 3: Cloudflare Pages
1. เข้า [Cloudflare Dashboard](https://dash.cloudflare.com/) > **Workers & Pages**
2. เลือก **Upload assets** แล้วลากไฟล์ทั้งหมดในโฟลเดอร์นี้ขึ้นไปได้ทันที

---

## 🎥 วิธีตั้งค่าใน TikTok LIVE Studio

1. เปิดโปรแกรม **TikTok LIVE Studio**
2. ในแผง **Sources (แหล่งที่มา)** กดปุ่ม **`+ Add Source`** (เพิ่มแหล่งที่มา)
3. เลือก **`Link`**
4. ในช่อง URL ให้วางลิงก์ที่ได้จากตัว Generator เช่น:
   ```text
   https://your-domain.vercel.app/overlay.html?type=clock&opacity=0.15&interval=4&transition=3&safeZone=6
   ```
5. ตั้งค่าขนาดความกว้าง/ความสูงให้ตรงกับฉากไลฟ์:
   - **แนวตั้ง (มือถือ):** Width: `1080`, Height: `1920`
   - **แนวนอน (คอม):** Width: `1920`, Height: `1080`
6. จัดเลเยอร์ (Layer) ของ Link Source ให้อยู่ **บนสุด** เหนือวิดีโอหรือกล้องของคุณ

---

## 🎬 วิธีตั้งค่าใน OBS Studio

1. ในหน้าต่าง **Sources** กดปุ่ม `+`
2. เลือก **`Browser`** (เบราว์เซอร์)
3. วาง URL ลงในช่อง URL
4. กำหนด Width / Height (เช่น `1080` x `1920` หรือ `1920` x `1080`)
5. ติ๊กเครื่องหมายถูกที่:
   - `Shutdown source when not visible`
   - `Refresh browser when scene becomes active`
6. กด **OK**

---

## ⚙️ คู่มือ URL Query Parameters (ปรับแต่งผ่าน URL โดยตรง)

คุณสามารถแก้ไขค่าผ่าน URL Query String ได้เองตามตารางนี้:

| Parameter | ค่าที่รองรับ | ตัวอย่าง | คำอธิบาย |
| :--- | :--- | :--- | :--- |
| `type` | `clock`, `text`, `image`, `hybrid`, `code` | `type=clock` | รูปแบบลายน้ำ (เวลา, ข้อความ, รูปภาพ, รูป+เวลา, รหัสสุ่ม) |
| `text` | ข้อความใดๆ | `text=MyChannel` | ข้อความลายน้ำ (ใช้เมื่อ `type=text` หรือ `hybrid`) |
| `img` | URL รูปภาพ (PNG/SVG) | `img=https://.../logo.png` | ลิงก์รูปภาพโลโก้ (แนะนำภาพพื้นหลังใส) |
| `format` | `time`, `ms`, `full` | `format=ms` | รูปแบบเวลา (`time` = HH:mm:ss, `ms` = ละเอียดระดับเสี้ยววินาที) |
| `antiloop`| `true`, `false` | `antiloop=true` | เปิดโหมดสร้างชุดรหัสสุ่มตัดปัญหา AI จับคลิปวน |
| `opacity` | `0.05` ถึง `1.0` | `opacity=0.15` | ความโปร่งแสง (0.15 = 15%) |
| `interval`| วินาที (เช่น `1.0` ถึง `10.0`) | `interval=4` | ระยะเวลารอในแต่ละจุดก่อนเริ่มสุ่มพิกเซลใหม่ |
| `transition`| วินาที (เช่น `0.5` ถึง `6.0`) | `transition=3.5`| ความเร็วในการเคลื่อนที่ (ยิ่งมากยิ่งนุ่มนวล) |
| `fontSize` | พิกเซล | `fontSize=24` | ขนาดตัวอักษรของเวลา/ข้อความ |
| `size` | พิกเซล | `size=100` | ขนาดความกว้างของรูปภาพโลโก้ |
| `color` | รหัสสี HEX (URL Encoded) | `color=%23ffffff` | สีตัวอักษร (`%23ffffff` = สีขาว) |
| `safeZone`| เปอร์เซ็นต์ขอบจอ (`0` ถึง `20`) | `safeZone=6` | ระยะเว้นขอบจอ ไม่ให้ทับ UI ตะกร้า/แชท |
| `glow` | `true`, `false` | `glow=true` | เงาตัวอักษรเพื่อให้มองเห็นได้ทั้งพื้นหลังมืดและสว่าง |
