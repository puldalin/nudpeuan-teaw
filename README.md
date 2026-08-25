# นัดเพื่อนเที่ยว 🌿

เว็บนัดวันเที่ยวสำหรับกลุ่มเพื่อน 10 คน ทุกคนที่เปิดเว็บเห็นข้อมูลชุดเดียวกัน อัปเดตแบบเรียลไทม์ (ไม่ต้องกดรีเฟรช)

## ก่อนรันต้องทำ 2 อย่าง

### 1. สร้างโปรเจกต์ Firebase (ฟรี ไม่ต้องผูกบัตร)

1. เข้า https://console.firebase.google.com → กด **"Add project"** ตั้งชื่ออะไรก็ได้ (เช่น `nudpeuan-teaw`)
2. เมื่อเข้าโปรเจกต์แล้ว ที่เมนูซ้าย ไปที่ **Build → Firestore Database** → กด **"Create database"**
   - เลือกโหมด **"Start in test mode"** (เปิดให้อ่าน/เขียนได้ฟรีเป็นเวลา 30 วัน เหมาะกับกลุ่มเพื่อนที่ไว้ใจกัน — ดูหัวข้อ "เรื่องความปลอดภัย" ด้านล่างด้วย)
   - เลือก location ใกล้ๆ (เช่น `asia-southeast1`)
3. กลับไปหน้า Project overview → กดไอคอน **`</>`** (Add app → Web)
   - ตั้งชื่อ app อะไรก็ได้ → กด Register app
   - จะได้ค่า config (apiKey, authDomain, projectId ฯลฯ) **คัดลอกเก็บไว้** จะใช้ในขั้นตอนถัดไป

### 2. ตั้งค่าไฟล์ .env

1. คัดลอกไฟล์ `.env.example` แล้วเปลี่ยนชื่อเป็น `.env`
2. เอาค่าจาก Firebase config ที่คัดลอกไว้มาใส่ให้ตรงกับแต่ละบรรทัด เช่น
   ```
   VITE_FIREBASE_API_KEY=AIzaSyXXXXXXXXXXXXXXXX
   VITE_FIREBASE_AUTH_DOMAIN=nudpeuan-teaw.firebaseapp.com
   VITE_FIREBASE_PROJECT_ID=nudpeuan-teaw
   VITE_FIREBASE_STORAGE_BUCKET=nudpeuan-teaw.appspot.com
   VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
   VITE_FIREBASE_APP_ID=1:123456789:web:abcdef123456
   ```

## รันทดสอบในเครื่อง

```bash
npm install
npm run dev
```

เปิด `http://localhost:5173` จะเห็นเว็บทำงานได้เลย

## เอาขึ้น GitHub

```bash
git init
git add .
git commit -m "นัดเพื่อนเที่ยว"
git branch -M main
git remote add origin https://github.com/<username>/<repo-name>.git
git push -u origin main
```

⚠️ ไฟล์ `.env` จะไม่ถูกอัปขึ้น GitHub อัตโนมัติ (กันไว้ใน `.gitignore` แล้ว) เพราะมีค่าลับของ Firebase อยู่ — ปลอดภัยแล้ว ไม่ต้องกังวล

## Deploy ขึ้นเว็บจริง (แนะนำ Vercel)

1. เข้า https://vercel.com → Sign up ด้วย GitHub
2. กด **"Add New → Project"** → เลือก repo ที่เพิ่ง push ไป
3. ในหน้าตั้งค่า ไปที่ **Environment Variables** → ใส่ค่าทั้ง 6 ตัวจาก `.env` ของคุณทีละตัว (ชื่อ + ค่า)
4. กด **Deploy** รอสักครู่ จะได้ลิงก์เว็บถาวร เช่น `nudpeuan-teaw.vercel.app`

ทุกครั้งที่แก้โค้ดแล้ว push ขึ้น GitHub ใหม่ Vercel จะ deploy เวอร์ชันล่าสุดให้อัตโนมัติ

## เรื่องความปลอดภัย

โหมด "test mode" ของ Firestore เปิดให้ใครก็ตามที่รู้ลิงก์ Firebase project อ่าน/เขียนข้อมูลได้ (จะหมดอายุใน 30 วันแล้วต้องต่ออายุ หรือปรับ rules เอง) เหมาะกับใช้งานในกลุ่มเพื่อนเล็กๆ ที่ไว้ใจกัน ถ้าอยากปลอดภัยขึ้น ไปที่ Firestore → Rules แล้วตั้งกฎเองภายหลังได้ครับ
