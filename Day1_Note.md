## DevOps Jenkins & GitHub Actions & N8N - Day 1

### 📋 สารบัญ

1. [ภาพรวมหลักสูตร](#ภาพรวมหลักสูตร)
2. [พื้นฐานและการติดตั้งเครื่องมือ DevOps CI/CD](#พื้นฐานและการติดตั้งเครื่องมือ-devops-cicd)
3. [พื้นฐานการใช้งาน Git และ GitHub](#พื้นฐานการใช้งาน-git-และ-github)
4. [พื้นฐานการใช้งาน Docker](#พื้นฐานการใช้งาน-docker)

## โปรแกรม (Tool and Editor) ที่ใช้อบรม

1. **Visual Studio Code**
2. **Java JDK 21.x**
3. **Node.js 22.x**
4. **Python 3.1x**
5. **Docker Desktop**
6. **Git**

> แนะนำ 
> หลักสูตรนี้ใช้ Java JDK เวอร์ชั่น 17 หรือ 21 เท่านั้น (เก่าหรือใหม่กว่านี้ไม่รองรับ)
> หลักสูตรนี้ใช้ Node.JS เวอร์ชั่น 22 ขึ้นไป
> หลักสูตรนี้ใช้ Python เวอร์ชั่น 3.10 ขึ้นไป
---

## การตรวจสอบความเรียบร้อยของเครื่องมือที่ติดตั้งบน Windows / Mac OS / Linux

เปิด Command Prompt บน Windows หรือ Terminal บน Mac ขึ้นมาป้อนคำสั่งดังนี้

### Visual Studio Code
```bash
code --version
```

### Node JS
```bash
node -v
npm -v
npx -v
```

### Java JDK
```bash
java -version
set JAVA_HOME
where java
```

### Python
```bash
# Windows
python --version
pip --version

# Mac / Linux
python3 --version
pip3 --version
```

### Docker
```bash
docker --version
docker compose version
docker info
```

### Git
```bash
git version
```

---

## พื้นฐานการใช้งาน Git

- เริ่มต้นใช้งาน Git ในโปรเจ็กต์
- การตั้งค่า , การ clone , คำสั่งพื้นฐาน

#### 1. Git First time setup
```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
> คำสั่งนี้จะทำให้ Git รู้ว่า ใครเป็นคนทำการ commit โค้ด และทำเพียงครั้งเดียวเท่านั้น

คำสั่งเช็คข้อมูลที่กำหนดไว้

```bash
git config  --list
git config  --global --list
```

#### 2. Set Default branch "main"
```bash
# ตั้งค่า default branch เป็น main
git config --global init.defaultBranch main

# ตรวจสอบหลังตั้งค่า
git config --list
git config --list --show-origin
```
> Git มีการตั้งค่าได้ 3 ระดับ ซึ่งจะถูกอ่านเรียงต่อกันตามลำดับ
> 1. System: การตั้งค่าสำหรับทุก User บนเครื่องคอมพิวเตอร์นี้
> 2. Global: การตั้งค่าสำหรับ User ของคุณคนเดียว (ไฟล์ ~/.gitconfig)
> 3. Local: การตั้งค่าสำหรับโปรเจกต์นั้นๆ โปรเจกต์เดียว (ไฟล์ .git/config ในโฟลเดอร์โปรเจกต์)

#### 3. Git Workflow

##### 3.1 สร้างโฟลเดอร์โปรเจ็กต์ใหม่
```bash
mkdir devops-jenkins-github-actions-n8n/basic-git
cd devops-jenkins-github-actions-n8n/basic-git
```

##### 3.2 เริ่มต้น git ในโฟลเดอร์
```bash
git init
```

##### 3.3 สร้างไฟล์ greeting.txt
```bash
echo "Greeting message line 1" >> greeting.txt
```

##### 3.4 ตรวจสอบสถานะ
```bash
git status
```

##### 3.5 เพิ่มไฟล์เข้า staging area
```bash
git add greeting.txt
```

##### 3.6 ตรวจสอบสถานะ
```bash
git status
```

##### 3.7 commit ไฟล์
```bash
git commit -m "Initial commit"
```

##### 3.8 ตรวจสอบสถานะ
```bash
git status
```

##### 3.9 แก้ไขไฟล์ greeting.txt
```bash
echo "hiy" >> greeting.txt
```

##### 3.10 ตรวจสอบสถานะ
```bash
git status
```

##### 3.11 เพิ่มไฟล์เข้า staging area
```bash
git add greeting.txt
or
git add .
```

##### 3.12 ตรวจสอบสถานะ
```bash
git status
```

##### 3.13 commit ไฟล์
```bash
git commit -m "Add line 2 to greeting.txt"
```

##### 3.14 ตรวจสอบสถานะ
```bash
git status
```

##### 3.13 commit ไฟล์
```bash
git commit -m "Add line 2 to greeting.txt"
```

##### 3.14 ตรวจสอบสถานะ
```bash
git status
```

##### 3.15 ดูประวัติการ commit
```bash
git log
```

##### 3.16 ดูประวัติการ commit แบบย่อ
```bash
git log --oneline
git log --oneline --graph --decorate --all
```

##### 3.17 ดูความแตกต่างของไฟล์
```bash
# ปกติ
git diff HEAD~1 HEAD greeting.txt

# สีสันสวยงาม
git diff --color HEAD~1 HEAD greeting.txt

# แบบมีบริเวณบรรทัดเพิ่ม-ลบ
git diff --color --unified=5 HEAD~1 HEAD greeting.txt
```

##### 3.18 เพิ่มไฟล์ README.md
```bash
echo "# Basic Git" >> readme.txt
git add readme.txt
git commit -m "Add readme.txt"
git status
git log --oneline
```

##### 3.19 ย้อนกลับและแก้ไขการเปลี่ยนแปลง (Undo/Repair)

##### วิธีที่ 1: Git Reset --hard (การย้อนเวลาแบบทำลายล้าง) 💣
`git reset --hard <commit>` ทำ 3 อย่างพร้อมกัน:

1. ย้าย HEAD: ย้ายตัวชี้ (HEAD) และ Branch ปัจจุบันกลับไปที่ <commit> ที่ระบุ
2. ล้าง Staging Area: ทำให้ Staging Area (index) ตรงกับสถานะของ <commit> นั้น
3. ล้าง Working Directory: ลบการเปลี่ยนแปลงทั้งหมด ในไฟล์ที่คุณกำลังทำงานอยู่ (ที่ยังไม่ได้ commit) ให้กลับไปเหมือนกับ <commit> นั้น

แสดงภาพกราฟิก
```plaintext
HEAD -> main
 o---o---o---o---o  main (HEAD)
          ^
          |
        <commit>
          |
          +-- Staging Area (index) ถูกล้าง
          |
          +-- Working Directory ถูกล้าง
```

> สรุป: เป็นคำสั่งสำหรับ "ทิ้งทุกอย่าง" ที่ทำหลังจาก <commit> นั้นไป แล้วย้อนเวลากลับไปจุดนั้นอย่างถาวร

```bash
git reset --hard <commit>
git status
git log --oneline
```

##### วิธีที่ 2: Git Reset --soft (การย้อนเวลาแบบเก็บงาน) 🛠️
`git reset --soft <commit>` ทำ 2 อย่าง:

1. ย้าย HEAD: ย้ายตัวชี้ (HEAD) และ Branch ปัจจุบันกลับไปที่ <commit> ที่ระบุ
2. เก็บการเปลี่ยนแปลง: ทำให้การเปลี่ยนแปลงทั้งหมดใน Staging Area (index) ยังคงอยู่

แสดงภาพกราฟิก
```plaintext
HEAD -> main
 o---o---o---o---o  main (HEAD)
          ^
          |
        <commit>
          |
          +-- Staging Area (index) ยังคงอยู่
          |
          +-- Working Directory ยังคงอยู่
```

> สรุป: เป็นคำสั่งสำหรับ "ย้อนกลับ" ไปยัง <commit> ที่ระบุ แต่ยังคงเก็บการเปลี่ยนแปลงทั้งหมดใน Staging Area (index) ไว้

```bash
git reset --soft <commit>
git status
git log --oneline
```

##### วิธีที่ 3: Git Revert (การย้อนกลับแบบสร้าง commit ใหม่) 🔄
`git revert <commit>` สร้าง commit ใหม่ที่ย้อนกลับการเปลี่ยนแปลงที่ทำใน <commit> ที่ระบุ โดยไม่เปลี่ยนแปลงประวัติของ commit

แสดงภาพกราฟิก
```plaintext
HEAD -> main
 o---o---o---o---o  main (HEAD)
          ^
          |
        <commit>
          |
          +-- Staging Area (index) ถูกล้าง
          |
          +-- Working Directory ถูกล้าง
          |
        +---o  main (HEAD) (commit ใหม่ที่ย้อนกลับ)
        |
      <commit>
        |
        +---o  main (HEAD)
```
> สรุป: เป็นคำสั่งสำหรับ "ย้อนกลับ" การเปลี่ยนแปลงที่ทำใน <commit> ที่ระบุ โดยสร้าง commit ใหม่ที่ทำการย้อนกลับนั้น

```bash
git revert <commit>
git status
git log --oneline
```

##### วิธีที่ 4: Git Checkout (การแวะดูอดีต) 🕵️‍♂️

`git checkout <commit>` ทำหน้าที่แตกต่างออกไป:

1. ย้าย HEAD: ย้ายตัวชี้ (HEAD) ไปยัง <commit> ที่ระบุ แต่ ไม่ได้ย้าย Branch ตามไปด้วย สิ่งนี้จะทำให้คุณเข้าสู่สถานะที่เรียกว่า "detached HEAD"

2. อัปเดต Working Directory: ทำให้ไฟล์ใน Working Directory ของคุณตรงกับสถานะของ <commit> นั้น เพื่อให้คุณสามารถดูหรือทดสอบโค้ด ณ จุดนั้นได้

แสดงภาพกราฟิก
```plaintext
HEAD -> main
 o---o---o---o---o  main (HEAD)
          ^
          |
        <commit>
          |
          +-- Staging Area (index) ถูกล้าง
          |
          +-- Working Directory ถูกล้าง
          |
        +---o  main (HEAD) (commit ใหม่ที่ย้อนกลับ)
        |
      <commit>
        |
        +---o  main (HEAD)
```
> สรุป: เป็นคำสั่งสำหรับ "สลับไปดู" โค้ดในอดีตชั่วคราว เมื่อคุณดูเสร็จแล้ว สามารถใช้ git checkout <branch-name> (เช่น git checkout main) เพื่อกลับมาที่ปัจจุบันได้อย่างปลอดภัย โดยที่ประวัติ commit และงานล่าสุดของคุณยังอยู่ครบ

> สรุปถ้า commit ปัจจุบันมี error ในโค้ดและอยากย้ายกลับไปเริ่มใหม่ใน commit ก่อนหน้าแนะนำให้ใช้ git reset --hard <commit> เพื่อย้อนกลับไปยัง commit ที่ต้องการ

```bash
git reset --hard HEAD~1
```

เพราะเป้าหมายของคุณคือ "ทิ้ง commit ล่าสุดที่มีปัญหา และย้อนกลับไปเริ่มต้นใหม่ที่ commit ก่อนหน้านั้น"

`git reset --hard HEAD~1` จะทำสิ่งที่คุณต้องการทุกอย่าง:

- ลบ commit ล่าสุด ที่มี error ออกจากประวัติของ Branch
- ล้างการเปลี่ยนแปลงทั้งหมด ที่มาจาก commit ที่ผิดพลาดนั้นออกจากโค้ดของคุณ
- ทำให้ไฟล์ทั้งหมดในโปรเจกต์ของคุณกลับไปอยู่ในสถานะที่สมบูรณ์ ณ commit ก่อนหน้า พร้อมให้คุณเริ่มทำงานต่อได้ทันที

#### 4. เชื่อมต่อและจัดการ Remote (Remotes)
##### 4.1 สร้าง Remote Repository บน GitHub
1. ไปที่ [GitHub](https://github.com) และล็อกอินเข้าสู่ระบบ
2. คลิกที่ปุ่ม "New" เพื่อสร้าง Repository ใหม่
3. กรอกชื่อ Repository เช่น `basic-git`
4. เลือก Public หรือ Private ตามต้องการ
5. คลิกที่ปุ่ม "Create repository"

##### 4.2 เชื่อมต่อ Local Repository กับ Remote Repository
```bash
git remote add origin <remote-repository-URL>
git branch -M main
git push -u origin main
```

##### 4.3 ตรวจสอบ Remote ที่เชื่อมต่ออยู่
```bash
git remote -v
```

##### 4.4 ดึงข้อมูลจาก Remote Repository
```bash
git pull origin main
```

##### 4.5 ส่งข้อมูลไปยัง Remote Repository
```bash
git push origin main
```

#### 5. การจัดการ Branches
##### 5.1 สร้าง Branch ใหม่
```bash
git branch <branch-name>

# หรือ
git checkout -b <branch-name>

# เช่น
git branch develop

# หรือ
git checkout -b develop
```

##### 5.2 สลับไปยัง Branch ที่ต้องการ
```bash
git switch <branch-name>

# หรือ
git checkout <branch-name>

# เช่น
git switch develop
# หรือ
git checkout develop
```

>  git switch (ผู้เชี่ยวชาญด้านการสลับ 🚂)
> git switch ถูกสร้างขึ้นมาใหม่ (ใน Git เวอร์ชัน 2.23) โดยมีวัตถุประสงค์เดียวคือ การสลับ Branch
> หน้าที่ชัดเจน: ใช้สำหรับเปลี่ยนจาก Branch หนึ่งไปยังอีก Branch หนึ่งเท่านั้น
> ปลอดภัยกว่า: git switch จะ ป้องกัน ไม่ให้คุณสลับ Branch หากการสลับนั้นจะทำให้งานที่คุณทำค้างไว้ (แต่ยังไม่ได้ commit) สูญหาย มันจะเตือนให้คุณ commit หรือ stash งานก่อน ซึ่งช่วยลดความผิดพลาดได้มาก

> git checkout (มีดพกสวิส)
> git checkout เป็นคำสั่งที่มีความสามารถหลากหลายมากกว่า มันสามารถใช้ได้ทั้งการสลับ Branch, การสร้าง Branch ใหม่, การแวะดู commit ในอดีต, และการกู้คืนไฟล์จาก commit ก่อนหน้า
> ความสามารถหลากหลาย: git checkout สามารถทำได้หลายอย่างในคำสั่งเดียว ซึ่งทำให้มันมีความซับซ้อนและอาจทำให้เกิดความสับสนได้
> เสี่ยงต่อความผิดพลาด: เนื่องจาก git checkout มีหลายหน้าที่ มันอาจทำให้ผู้ใช้เผลอทำสิ่งที่ไม่ต้องการ เช่น การสลับ Branch โดยไม่ตั้งใจและสูญเสียงานที่ยังไม่ได้ commit

##### 5.3 สร้างไฟล์ใหม่และ commit ใน Branch ใหม่
```bash
touch develop_file.txt
git add develop_file.txt
git commit -m "เพิ่มไฟล์ใหม่ใน Branch develop"
git push -u origin develop
```

##### 5.4 รวม Branch กลับไปยัง main
```bash
git checkout main
git merge develop
```

##### 5.5 ลบ Branch ที่ไม่ต้องการ
```bash
git branch -d develop
```

#### 6. การแก้ไขข้อขัดแย้ง (Merge Conflicts)
##### 6.1 สร้างข้อขัดแย้ง
```bash
git checkout develop
echo "Hello from develop" > conflict.txt
git add conflict.txt
git commit -m "เพิ่มไฟล์ conflict.txt ใน Branch develop"
git push -u origin develop
```

```bash
git checkout main
echo "Hello from main" > conflict.txt
git add conflict.txt
git commit -m "เพิ่มไฟล์ conflict.txt ใน Branch main"
git push origin main
```

##### 6.2 พยายามรวม Branch
```bash
git merge develop
# จะเกิดข้อขัดแย้ง
git status
# แก้ไขไฟล์ conflict.txt
git add conflict.txt
git commit -m "แก้ไขข้อขัดแย้งในไฟล์ conflict.txt"
git push origin main
```
> แนวทางการแก้ไขข้อขัดแย้ง
> 1. เปิดไฟล์ที่มีข้อขัดแย้งในโปรแกรมแก้ไขข้อความ (เช่น VS Code)
> 2. ค้นหาส่วนที่มีข้อขัดแย้ง ซึ่งจะถูกทำเครื่องหมายด้วย `<<<<<<<`, `=======`, และ `>>>>>>>`
> 3. ตัดสินใจเลือกว่าจะเก็บส่วนใด หรือผสมผสานกัน
> 4. ลบเครื่องหมายข้อขัดแย้งทั้งหมดออกจากไฟล์
> 5. บันทึกไฟล์และปิดโปรแกรมแก้ไขข้อความ
> 6. ใช้คำสั่ง `git add <file>` เพื่อทำเครื่องหมายว่าได้แก้ไขข้อขัดแย้งแล้ว
> 7. ใช้คำสั่ง `git commit` เพื่อสร้าง commit ใหม่ที่บันทึกการแก้ไขข้อขัดแย้ง

#### 7. การใช้งาน .gitignore
> ไฟล์ .gitignore ใช้เพื่อบอก Git ว่าไม่ต้องติดตาม (track) หรือไม่ต้องรวมไฟล์หรือโฟลเดอร์บางอย่างในระบบควบคุมเวอร์ชัน
##### 7.1 สร้างไฟล์ .gitignore
```bash
echo "node_modules/" >> .gitignore
echo "*.log" >> .gitignore
echo "dist/" >> .gitignore
echo ".env" >> .gitignore
```
---

## พื้นฐานการใช้งาน Docker
- การติดตั้ง Docker Desktop
- การใช้งานคำสั่งพื้นฐานของ Docker
- การสร้างและจัดการ Container
- การสร้าง Dockerfile และ Docker Image
- การใช้งาน Docker Compose

#### 1. การติดตั้ง Docker Desktop
- ดาวน์โหลดและติดตั้ง Docker Desktop จาก [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
- ตรวจสอบการติดตั้งโดยรันคำสั่ง:
```bash
docker --version
docker compose version
docker info
```

#### 2. การใช้งานคำสั่งพื้นฐานของ Docker
##### 2.1 รัน hello-world container
```bash
docker run hello-world
```
> คำสั่งนี้จะดาวน์โหลดและรัน container ที่แสดงข้อความต้อนรับจาก Docker

##### 2.2 ดูรายการ container ที่กำลังรันอยู่
```bash
docker ps
docker ps -a  # ดู container ทั้งหมดรวมถึงที่หยุดแล้ว
```

##### 2.3 หยุด container
```bash
docker stop <container_id>
```

##### 2.4 ลบ container
```bash
docker rm <container_id>
```

##### 2.5 ดูรายการ image ที่มีอยู่
```bash
docker images
docker image ls
```
##### 2.6 ลบ image
```bash
docker rmi <image_id>
```

#### 3. การสร้างและจัดการ Container
##### 3.1 รัน container จาก image
```bash
docker run -d -p 8880:80 --name mynginx nginx
```
> คำสั่งนี้จะรัน Nginx container ในโหมด detached และแมปพอร์ต 80 ของ container ไปยังพอร์ต 8880 ของโฮสต์

##### 3.2 เข้าสู่ shell ของ container
```bash
docker exec -it mynginx /bin/bash
# หรือ
docker exec -it mynginx /bin/sh
```

##### 3.3 ดู log ของ container
```bash
docker logs mynginx
```

#### 4. การสร้าง Dockerfile และ Docker Image

##### 4.1 สร้างโฟลเดอร์โปรเจ็กต์
```bash
mkdir basic-docker/docker-node-app
cd basic-docker/docker-node-app
```

##### 4.2 สร้างไฟล์ package.json
```bash
npm init -y
```

##### 4.3 กำหนดสคริปต์ใน package.json
```json
{
  "name": "docker-node-app",
  "version": "1.0.0",
  "description": "A simple Node.js app for Docker",
  "main": "index.js",
  "scripts": {
    "dev": "nodemon index.js",
    "start": "node index.js"
  },
  "author": "Your Name",
  "license": "ISC",
  "dependencies": {
    "express": "^4.18.2",
    "nodemon": "^2.0.22"
  }
}
```
> nodemon เป็นเครื่องมือที่ช่วยในการพัฒนา Node.js โดยจะทำการรีสตาร์ทเซิร์ฟเวอร์อัตโนมัติเมื่อมีการเปลี่ยนแปลงในโค้ด

##### 4.4 สร้างไฟล์ index.js
```javascript
const express = require('express')
const app = express()

// ทำ url ให้สามารถเข้าถึงได้
app.get('/', (req, res) => {
  res.send('Hello World!')
})

// run the server
app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000')
})
```

##### 4.5 สร้างไฟล์ Dockerfile

> ไฟล์ Dockerfile เป็นไฟล์ข้อความธรรมดาที่ใช้กำหนดขั้นตอนการสร้าง Docker Image โดยระบุฐานของ image, การติดตั้ง dependencies, การคัดลอกไฟล์, การตั้งค่าพอร์ต และคำสั่งที่ต้องรันเมื่อ container เริ่มทำงาน

```Dockerfile
# โหลด image ของ node จาก docker hub
FROM node:alpine

# กำหนด directory ที่จะใช้เก็บไฟล์ของโปรเจค
WORKDIR /app

# คัดลอกไฟล์ package.json และ package-lock.json ไปยัง directory ที่กำหนดไว้
COPY package*.json ./

# ติดตั้ง package ที่ระบุในไฟล์ package.json
RUN npm install

# ติดตั้ง nodemon เพื่อใช้ในการรันโปรเจค
RUN npm install -g nodemon

# คัดลอกไฟล์ทั้งหมดไปยัง directory ที่กำหนดไว้
COPY . .

# ระบุ port ที่จะใช้
EXPOSE 3000

# รันคำสั่ง npm run dev เมื่อ container ถูกสร้างขึ้น
CMD ["npm", "run", "dev"]
```

##### 4.6 สร้าง Docker Image
```bash
docker build -t docker-node-app .
```

##### 4.7 รัน Docker Container
```bash
docker run -d -p 3300:3000 --name mydockerapp docker-node-app
```

#### 5. การใช้งาน Docker Compose
##### 5.1 สร้างไฟล์ docker-compose.yml
```yaml
networks:
  nodejs_network:
    name: nodejs_network
    driver: bridge

services:

  # NodeJS App
  nodejs:
    build:
      context: .
      dockerfile: Dockerfile
      tags:
        - "mynodeapp:1.0"
    container_name: mynodeapp
    volumes:
      - .:/app
      - /app/node_modules
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
      - CHOKIDAR_USEPOLLING=true # สำหรับ Windows เพื่อให้ nodemon ทำงานได้
    networks:
      - nodejs_network
    restart: always

  # MongoDB
  mongodb:
    image: mongo
    container_name: mongodb
    ports:
      - "28017:27017"
    networks:
      - nodejs_network
    restart: always
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
    name: mongo_data
    driver: local
```

##### 5.2 รัน Docker Compose
```bash
# เช็คความถูกต้องของไฟล์ docker-compose.yml
docker compose config

# รัน Docker Compose
docker compose up -d

# หรือถ้ามีการเปลี่ยนแปลงไฟล์ Dockerfile หรือ docker-compose.yml
docker compose up -d --build
```

##### 5.3 ตรวจสอบสถานะของ Container
```bash
docker compose ps
```

##### 5.4 หยุดและลบ Container
```bash
docker compose down

# หรือถ้าต้องการลบข้อมูลทั้งหมดรวมถึง volume
docker compose down -v

# หรือถ้าต้องการลบ image ด้วย
docker compose down --rmi all -v
```

#### 6. DockerHub (การใช้งาน Docker Hub)
##### 6.1 สร้างบัญชีผู้ใช้บน Docker Hub
- ไปที่ [Docker Hub](https://hub.docker.com/) และสมัครสมาชิก
- สร้าง Repository ใหม่บน Docker Hub
  - คลิกที่ปุ่ม "Create Repository"
  - กรอกชื่อ Repository เช่น `mynodeapp`
  - เลือก Public หรือ Private ตามต้องการ
  - คลิกที่ปุ่ม "Create"

> สำหรับการใช้งาน Docker Hub แนะนำให้ใช้บัญชีแบบ Public เพราะจะง่ายต่อการเข้าถึงและใช้งานร่วมกับผู้อื่น
> เวอ์ร์ชันฟรีของ Docker Hub มีข้อจำกัดในการสร้าง Repository แบบ Private และมีข้อจำกัดในการดึง (pull) image จาก Repository ในระยะเวลาหนึ่ง

##### 6.2 เข้าสู่ระบบ Docker Hub ผ่าน Command Line
```bash
docker login
```

##### 6.3 การ Tag Image และ Push ขึ้น Docker Hub

| คำสั่ง | คำอธิบาย |
|--------|-----------|
| `docker tag <image>:<old_tag> <username>/<repo>:<new_tag>` | สร้างแท็กใหม่ให้ image เพื่อเตรียม push |


```bash
docker tag mynodeapp:1.0 <your-dockerhub-username>/mynodeapp:1.0
```

##### 6.4 ดัน (Push) Docker Image ไปยัง Docker Hub

| คำสั่ง | คำอธิบาย |
|--------|-----------|
| `docker push <username>/<repo>:<tag>` | อัปโหลด image พร้อมแท็กขึ้น Docker Hub |

```bash
docker push <your-dockerhub-username>/mynodeapp:1.0
```

##### 6.5 ดึง (Pull) Docker Image จาก Docker Hub

| คำสั่ง | คำอธิบาย |
|--------|-----------|
| `docker pull <username>/<repo>:<tag>` | ดาวน์โหลด image จาก Docker Hub |

```bash
docker pull <your-dockerhub-username>/mynodeapp:1.0
```
---

## สิ่งที่เรียนรู้ใน Day 1

✅ พื้นฐานการใช้งาน Git และ GitHub
✅ การติดตั้งและตั้งค่าเครื่องมือที่ใช้ในหลักสูตร
✅ การสร้างและจัดการ Repository ด้วย Git
✅ การสร้างและจัดการ Branches ใน Git
✅ การแก้ไขข้อขัดแย้ง (Merge Conflicts) ใน Git
✅ การสร้างและจัดการ Docker Container
✅ การสร้าง Docker Image ด้วย Dockerfile
✅ การใช้งาน Docker Compose เพื่อจัดการหลาย Container
✅ การใช้งาน Docker Hub สำหรับเก็บและแชร์ Docker Image

---

## หมายเหตุ

- ใช้ Node.js เวอร์ชั่น 22.x
- ใช้ Java JDK เวอร์ชั่น 17 หรือ 21 เท่านั้น (เก่าหรือใหม่กว่านี้ไม่รองรับ)
- ใช้ Python เวอร์ชั่น 3.10 ขึ้นไป
- ใช้ Docker Desktop เวอร์ชั่นล่าสุด
- ใช้ Git เวอร์ชั่นล่าสุด
- ใช้ Visual Studio Code เวอร์ชั่นล่าสุด
- ใช้ Git Bash (สำหรับ Windows) หรือ Terminal (สำหรับ Mac/Linux)

## สรุป
ขอให้สนุกกับการเรียนรู้ DevOps Jenkins & GitHub Actions & N8N ครับ!