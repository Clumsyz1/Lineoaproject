# 🧺 Fitcheck Laundry - Online Laundry & Loyalty System (LINE LIFF)

ระบบสั่งซักผ้าออนไลน์และบัตรสะสมแต้มดิจิทัลผ่าน **LINE Front-end Framework (LIFF)** เชื่อมต่อระบบแจ้งเตือน **LINE Flex Message**, **Dialogflow Chatbot**, **Firebase Firestore** และ **Admin Dashboard** ครบวงจร

---

## 🌟 จุดเด่นและฟังก์ชันการทำงาน (Key Features)

### 1. 🔑 ระบบเข้าสู่ระบบ LINE Login (LIFF Authentication)
- เข้าใช้งานแอปพลิเคชันผ่านบัญชี LINE โดยอัตโนมัติ (Seamless Auto Login) ไม่ต้องกรอก username/password
- ดึงข้อมูลโปรไฟล์ผู้ใช้เพื่อยืนยันตัวตนจาก LINE Platform:
  - `userId` (LINE User ID)
  - `displayName` (ชื่อแสดงใน LINE)
  - `pictureUrl` (รูปโปรไฟล์)

---

### 2. 🧺 ระบบสั่งซักผ้าออนไลน์ (Online Laundry Ordering)
- **หมวดหมู่บริการซักรีด:** ซักพับ, ซักรีด, ซักแห้ง/สูท, ชุดเครื่องนอน
- **Real-time Price Calculator:** คำนวณราคารวมแบบเรียลไทม์ตามจำนวนชิ้นผ้า
- **ตัวเลือกการรับ-ส่ง:** 
  - ลูกค้ามาส่ง-รับเองที่ร้าน
  - ให้ทางร้านไปรับ-ส่งถึงที่ (Pickup & Delivery)
- **Location Selector:** ระบุพิกัด GPS บน Google Maps สำหรับการรับ-ส่งผ้า
- **ช่องทางชำระเงิน:** 
  - โอนเงินผ่าน **PromptPay** (พร้อมแสดงเลขบัญชีและคำนวณยอดสุทธิ)
  - เงินสด (Cash on Delivery / In-Store)
- **Coupon System:** รองรับการกดใช้คูปองส่วนลด 100 บาท (จากการสะสมแต้ม) เพื่อหักออกจากยอดรวมอัตโนมัติ

---

### 3. 🎫 ระบบบัตรสะสมแต้มดิจิทัล (Digital Stamp & Loyalty Card)
- **Stamp Display:** แสดงบัตรสะสมแสตมป์ดิจิทัล **10 ดวง** บนหน้าเว็บ LIFF และการ์ด **LINE Flex Message**
- **Auto Stamp Collection:** เมื่อออเดอร์ได้รับการอัปเดตสถานะเป็น **"จัดส่งแล้ว" (Delivered)** ระบบจะเพิ่มแสตมป์สะสมให้อัตโนมัติ **+1 ดวง ต่อ 1 ออเดอร์**
- **Reward Redemption:** เมื่อสะสมครบ **10 ดวง** ลูกค้าสามารถกดปุ่มแลกรับคูปองส่วนลด **100 บาท** บนหน้าเว็บ LIFF
- **Stamp Deduct:** ระบบจะหักแสตมป์ 10 ดวงออก และเพิ่มจำนวนคูปองส่วนลดไว้ใช้งานในครั้งถัดไปทันที

---

### 4. 🖥️ ระบบ Admin Dashboard
- **Kanban / Status Board:** แสดงรายการออเดอร์ซักรีดทั้งหมด แยกตาม 5 สถานะการทำงาน:
  1. ⏳ **รอรับผ้า (Pending)**
  2. 🚚 **รับผ้าแล้ว (Picked Up)**
  3. 🧼 **กำลังซัก (Washing)**
  4. ✨ **ซักเสร็จสิ้น (Completed)**
  5. 📦 **จัดส่งแล้ว (Delivered)**
- **Quick Status Changer:** ปุ่มเลื่อนสถานะออเดอร์ (`◀` `▶`) เพื่ออัปเดตงานได้อย่างรวดเร็ว รองรับ Responsive Display ทั้งบน Desktop และ Mobile
- **Security:** ระบบเข้าสู่ระบบด้วย **Admin Token** ป้องกันผู้ไม่เกี่ยวข้องเข้าถึงข้อมูล

---

### 5. 🔔 ระบบแจ้งเตือนสถานะ Order (LINE Flex Message Notification)
- **Real-time Flex Push:** ทุกครั้งที่ Admin เลื่อนสถานะออเดอร์ ระบบจะสร้างและส่งการ์ดแจ้งเตือน **LINE Flex Message** พร้อมรูปภาพตรงตามสถานะเข้าไปในแชท LINE ของลูกค้าอัตโนมัติ
- **Detailed Summary:** แสดงรายละเอียดครบถ้วนในการ์ด Flex Message:
  - เลขออเดอร์ (Order ID)
  - รายการผ้าที่ซัก / จำนวน
  - นัดหมายวันและเวลา
  - ช่องทางการชำระเงิน
  - ราคารวมก่อนส่วนลด, ส่วนลดที่ใช้, ยอดชำระสุทธิ
  - สรุปจำนวนแสตมป์สะสมปัจจุบัน

---

### 6. 🤖 ระบบ Dialogflow Chatbot Integration
- **Fulfillment Webhook Engine:** เชื่อมต่อกับ Dialogflow via `POST /dialogflow-webhook`
- **Smart Intents:**
  - 💬 พิมพ์ **"เช็คสถานะ"** ➔ ระบบดึงสถานะออเดอร์ล่าสุดของลูกค้า ตอบกลับเป็น Flex Card
  - 🎫 พิมพ์ **"แสตมป์"** หรือ **"แต้มสะสม"** ➔ ระบบดึงจำนวนแสตมป์ล่าสุด ตอบกลับเป็น Flex Card บัตรสะสมแสตมป์
  - 🗺️ พิมพ์ **"Location"** หรือ **"โลเคชั่น"** ➔ ส่งแผนที่ร้านเข้าแชท LINE
  - 🏷️ พิมพ์ **"Promotion"** หรือ **"โปรโมชั่น"** ➔ ส่ง Auto Message แจ้งโปรโมชั่นปัจจุบัน
  - 💰 พิมพ์ **"สอบถามราคา"** ➔ ส่ง Quick Reply ให้เลือกว่าจะดูราคาผ้าประเภทไหน

---

### 7. 🗄️ ระบบฐานข้อมูล (Database Schema - Firebase Firestore)
จัดเก็บข้อมูลแบบ Cloud NoSQL ใน **Firebase Firestore**:
- `users`: ข้อมูลสมาชิก LINE User ID, ชื่อ, รูปภาพ, จำนวนแสตมป์สะสม, จำนวนคูปอง
- `services` / `rates`: อัตราค่าบริการแต่ละหมวดหมู่และประเภทผ้า
- `orders`: รายการออเดอร์, สถานะ, พิกัด GPS, สรุปราคา, วิธีชำระเงิน
- `stamps_history` / `coupons`: ประวัติการสะสมและการแลกใช้งานคูปอง

---

### 8. 📱 LINE Official Account Rich Menu
สร้างและกำหนดค่า Rich Menu ผ่าน LINE Messaging API (ผ่าน Postman / Script setup):
1. **สั่งซักผ้า / จองคิว:** เปิดหน้าเว็บ LIFF เพื่อสั่งซักผ้าออนไลน์
2. **เช็คสถานะออเดอร์:** ส่งคำสั่งเช็คสถานะออเดอร์ซักรีดปัจจุบันแบบ Flex Message
3. **บัตรสะสมแสตมป์:** เปิดการ์ดบัตรสะสมแสตมป์ดิจิทัลเพื่อเช็คแต้มและแลกคูปอง
4. **อัตราค่าบริการ:** เปิดหน้าเช็คราคาค่าบริการซักรีดทุกประเภท
5. **ตำแหน่งร้าน / แผนที่:** เปิด Google Maps นำทางมายังร้าน Fitcheck Laundry
6. **ติดต่อร้านค้า:** แสดงข้อมูลการติดต่อ และเบอร์โทรศัพท์ของทางร้าน

---

## 🛠️ เทคโนโลยีที่ใช้ (Tech Stack)

| ส่วนประกอบ | เทคโนโลยี |
|---|---|
| **Frontend / LIFF App** | HTML5, CSS3, JavaScript (ES6+), LINE Front-end Framework (LIFF SDK) |
| **Backend REST API** | Node.js, Express.js |
| **Database** | Firebase Firestore Cloud DB |
| **Messaging & Chatbot** | LINE Messaging API, LINE Flex Message, Dialogflow ES / CX (Fulfillment Webhook) |
| **Cloud Deployment** | Vercel (Frontend & Serverless REST API Engine) |

---

## 🚀 การติดตั้งและตั้งค่าโปรเจกต์ (Installation & Setup)

### 1. Clone Repository & Install Dependencies
```bash
git clone https://github.com/your-username/fitcheck-laundry.git
cd fitcheck-laundry
npm install
```

### 2. Configure Environment Variables (`.env`)
สร้างไฟล์ `.env` ที่ root directory แล้วใส่ค่าต่าง ๆ ดังนี้:

```env
PORT=3000
ADMIN_TOKEN=your_secret_admin_token

# LINE Credentials
LINE_CHANNEL_ACCESS_TOKEN=your_line_channel_access_token
LINE_CHANNEL_SECRET=your_line_channel_secret
LIFF_ID=your_liff_id

# Firebase Admin SDK Credentials
FIREBASE_PROJECT_ID=your_firebase_project_id
FIREBASE_CLIENT_EMAIL=your_firebase_client_email
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
```

### 3. Run Locally
```bash
npm start
# หรือพัฒนาในโหมด dev
npm run dev
```

---

## ☁️ Deployment

- **Frontend & Backend Server:** นำขึ้น Vercel Cloud Server รองรับ Node.js Serverless Functions
- **Database:** Firebase Firestore Cloud Database

---

## 👨‍💻 ผู้จัดทำ (Developer)

- **Developer:** Clumsyz

