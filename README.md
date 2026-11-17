1. เนื้อหาสำหรับไฟล์ README.md
Markdown
# DS ML Service

บริการ Machine Learning API สำหรับทำนายราคาบ้าน (California Housing) พัฒนาด้วย Python (Flask / Gunicorn) และบรรจุในรูปแบบ Docker Container

## โครงสร้างโปรเจกต์

```text
ml_service/
├── templates/
│   └── main.html          # หน้าเว็บ UI สำหรับใช้งานผ่านเบราว์เซอร์
├── app.py                 # Web Server และ API Endpoint (/predict)
├── train_model.py         # สคริปต์สำหรับเทรนโมเดลและบันทึกไฟล์ model.pkl
├── Dockerfile             # ไฟล์ตั้งค่าสำหรับสร้าง Docker Image
├── requirements.txt       # รายการ Library ที่ต้องใช้
├── .gitignore             # ไฟล์ยกเว้นการอัปโหลดขึ้น Git
└── README.md              # คู่มือการใช้งานโปรเจกต์
ข้อกำหนดเบื้องต้น (Prerequisites)
ติดตั้ง Docker Desktop และเปิดใช้งานให้เรียบร้อยก่อนเริ่มทำงาน
วิธีการ Build และ Run ด้วย Docker
1. Build Docker Image
เปิด Terminal เข้าไปที่โฟลเดอร์หลักของโปรเจกต์ แล้วรันคำสั่งเพื่อสร้าง Image (ขั้นตอนนี้อาจใช้เวลาสักครู่เพื่อดาวน์โหลด Library และรัน train_model.py สร้างโมเดลภายใน Image):
Bash
docker build -t ds-ml-service .
2. Run Container
เมื่อ Build เสร็จสมบูรณ์ ให้รัน Container โดยเปิดพอร์ต 5001 เพื่อเชื่อมต่อกับ Gunicorn ภายใน Container:
Bash
docker run --rm -p 5001:5001 ds-ml-service
หมายเหตุ: หากต้องการรันแบบทำงานเบื้องหลัง (Detached mode) ให้เปลี่ยน --rm เป็น -d (docker run -d -p 5001:5001 ds-ml-service)

การทดสอบใช้งาน
1. ใช้งานผ่านหน้าเว็บ (Web UI)
เปิดเบราว์เซอร์และเข้าไปที่:
Plaintext
[http://127.0.0.1:5001](http://127.0.0.1:5001)
2. ทดสอบยิง API Endpoint (/predict)
สำหรับ macOS / Linux (Zsh / Bash):
Bash
curl -i -X POST [http://127.0.0.1:5001/predict](http://127.0.0.1:5001/predict) \
  -H "Content-Type: application/json" \
  -d '{"features":[8.3,25.0,6.0,1.0,1200,3.0,34.2,-118.3]}'
สำหรับ Windows (PowerShell):
PowerShell
Invoke-WebRequest -Uri "[http://127.0.0.1:5001/predict](http://127.0.0.1:5001/predict)" `
  -Method POST `
  -Body '{"features":[8.3,25.0,6.0,1.0,1200,3.0,34.2,-118.3]}' `
  -ContentType "application/json"
ตัวอย่างผลลัพธ์ (Response):
JSON
{
  "prediction": 4.038992599999997
}

---

### 2. วิธีสร้างไฟล์และอัปโหลดขึ้น GitHub ทันที

รันคำสั่งนี้ใน Terminal ที่โฟลเดอร์ `/Users/thirrda/Code/ml_service` เพื่อสร้างไฟล์ `README.md` และ Push ขึ้น Git:

```bash
cat << 'EOF' > README.md
# DS ML Service

บริการ Machine Learning API สำหรับทำนายราคาบ้าน (California Housing) พัฒนาด้วย Python (Flask / Gunicorn) และบรรจุในรูปแบบ Docker Container

## โครงสร้างโปรเจกต์

\`\`\`text
ml_service/
├── templates/
│   └── main.html          # หน้าเว็บ UI สำหรับใช้งานผ่านเบราว์เซอร์
├── app.py                 # Web Server และ API Endpoint (/predict)
├── train_model.py         # สคริปต์สำหรับเทรนโมเดลและบันทึกไฟล์ model.pkl
├── Dockerfile             # ไฟล์ตั้งค่าสำหรับสร้าง Docker Image
├── requirements.txt       # รายการ Library ที่ต้องใช้
├── .gitignore             # ไฟล์ยกเว้นการอัปโหลดขึ้น Git
└── README.md              # คู่มือการใช้งานโปรเจกต์
\`\`\`

## ข้อกำหนดเบื้องต้น (Prerequisites)

- ติดตั้ง [Docker Desktop](https://www.docker.com/products/docker-desktop/) และเปิดใช้งานให้เรียบร้อยก่อนเริ่มทำงาน

## วิธีการ Build และ Run ด้วย Docker

### 1. Build Docker Image
เปิด Terminal เข้าไปที่โฟลเดอร์หลักของโปรเจกต์ แล้วรันคำสั่งเพื่อสร้าง Image:

\`\`\`bash
docker build -t ds-ml-service .
\`\`\`

### 2. Run Container
เมื่อ Build เสร็จสมบูรณ์ ให้รัน Container โดยเปิดพอร์ต `5001`:

\`\`\`bash
docker run --rm -p 5001:5001 ds-ml-service
\`\`\`

## การทดสอบใช้งาน

### 1. ใช้งานผ่านหน้าเว็บ (Web UI)
เปิดเบราว์เซอร์และเข้าไปที่: `http://127.0.0.1:5001`

### 2. ทดสอบยิง API Endpoint (`/predict`)

**สำหรับ macOS / Linux (Zsh / Bash):**
\`\`\`bash
curl -i -X POST http://127.0.0.1:5001/predict \
  -H "Content-Type: application/json" \
  -d '{"features":[8.3,25.0,6.0,1.0,1200,3.0,34.2,-118.3]}'
\`\`\`

**สำหรับ Windows (PowerShell):**
\`\`\`powershell
Invoke-WebRequest -Uri "http://127.0.0.1:5001/predict" `
  -Method POST `
  -Body '{"features":[8.3,25.0,6.0,1.0,1200,3.0,34.2,-118.3]}' `
  -ContentType "application/json"
\`\`\`
EOF