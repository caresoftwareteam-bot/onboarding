# 🧭 Git Handbook

### สำหรับทีมพัฒนา Software / Firmware

คู่มือนี้ออกแบบมาเพื่อใช้เป็น **Git Guideline สำหรับทีมพัฒนา** ที่ทำงานบน

* Windows
* Ubuntu / Linux
* WSL (Windows Subsystem for Linux)

รองรับการใช้งานกับ

* GitHub
* GitLab

เอกสารนี้ไม่มีข้อมูลส่วนตัว เช่น email หรือ repository จริง เพื่อให้สามารถใช้เป็น **เอกสารมาตรฐานของทีม** ได้

---

# 📚 สารบัญ

1. เริ่มต้นใช้งาน Git
2. การติดตั้ง Git (Linux / Ubuntu)
3. การตั้งค่า Git
4. การใช้งานบน Linux / WSL
5. เริ่มต้นโปรเจกต์
6. การจัดการ Branch
7. การเชื่อมต่อ Git
8. Push / Pull Code
9. Merge Branch
10. การลบ Branch
11. การลบ Git Repository
12. Git Workflow สำหรับทีม
13. คำสั่ง Git ที่ใช้บ่อย
14. มาตรฐานการตั้งชื่อ Branch
15. ปัญหาที่พบได้บ่อย
16. ตัวอย่าง .gitignore
17. Development Workflow
18. Commit Message Standard
19. SSH สำหรับ GitLab
20. SSH เมื่อ Port 22 ถูก Block
21. Git Flow Diagram
22. Release Management
23. GitLab CI/CD (ตัวอย่างสำหรับ Firmware)

---

# 1️⃣ เริ่มต้นใช้งาน Git

ตรวจสอบว่าเครื่องติดตั้ง Git แล้ว

```bash
git --version
```

ดาวน์โหลด Git

[https://git-scm.com/downloads](https://git-scm.com/downloads)

---

# 2️⃣ ติดตั้ง Git บน Ubuntu / Linux

```bash
sudo apt update
sudo apt install git -y
```

ตรวจสอบ

```bash
git --version
```

---

# 3️⃣ ตั้งค่า Git ครั้งแรก

```bash
git config --global user.name "Developer"
git config --global user.email "developer@example.com"
```

ตรวจสอบ

```bash
git config --list
```

---

# 4️⃣ การใช้งานบน Linux / WSL

ตัวอย่าง path บน Linux

```bash
/home/user/project
```

ตัวอย่าง path บน WSL

```bash
/mnt/c/Users/username/project
```

เข้า project

```bash
cd /path/to/project
```

ดูไฟล์

```bash
ls
```

---

# 5️⃣ เริ่มต้นโปรเจกต์

```bash
cd path/to/project

git init

git add .

git commit -m "Initial commit"
```

---

# 6️⃣ การสร้าง Branch

```bash
git checkout -b feature/new-feature
```

ดู branch

```bash
git branch
```

กลับ main

```bash
git checkout main
```

---

# 7️⃣ การเชื่อมต่อ Git

เพิ่ม remote repository โดยใช้ HTTPS :

**GitHub**
```bash
git remote add origin https://github.com/<username>/<repository>.git
```
**GitLab**
```bash
git remote add origin https://gitlab.com/<username>/<repository>.git
```
ตรวจสอบว่าเชื่อมสำเร็จ:

```bash
git remote -v
```

---

# 8️⃣ Push Code

```bash
git push -u origin main
```

Push branch

```bash
git push -u origin feature/new-feature
```

---

# 9️⃣ Pull Code

```bash
git pull
```

เฉพาะ branch

```bash
git pull origin feature/new-feature
```

---

# 🔟 Merge Branch

```bash
git checkout main

git merge feature/new-feature
```

ลบ branch

```bash
git branch -d feature/new-feature
```

---

# 1️⃣1️⃣ ลบ Branch

```bash
git branch -D feature/old-branch
```

ลบบน remote

```bash
git push origin --delete feature/old-branch
```

---

# 1️⃣2️⃣ ลบ Git Repository

Linux / WSL

```bash
rm -rf .git
```

Windows

```powershell
Remove-Item -Recurse -Force .git
```

---

# 1️⃣3️⃣ Git Commands ที่ใช้บ่อย

| Command           | Description      |
| ----------------- | ---------------- |
| git status        | ตรวจสอบสถานะไฟล์ |
| git add .         | เพิ่มไฟล์        |
| git commit -m     | commit           |
| git log --oneline | ดู commit        |
| git diff          | ดูการเปลี่ยนแปลง |
| git branch        | ดู branch        |
| git merge         | merge branch     |
| git push          | push code        |
| git pull          | pull code        |

---

# 1️⃣4️⃣ Branch Naming Convention

| Type    | Format         |
| ------- | -------------- |
| feature | feature/<name> |
| bugfix  | bugfix/<issue> |
| test    | test/<name>    |
| release | release/v1.x   |
| hotfix  | hotfix/<issue> |

---

# 1️⃣5️⃣ ปัญหาที่พบได้บ่อย

Push ถูกปฏิเสธ

```bash
! [rejected] main -> main (fetch first)
```

แก้

```bash
git pull origin main

git push
```

หรือ

```bash
git pull --rebase origin main
```

---

# 1️⃣6️⃣ ตัวอย่าง .gitignore

```gitignore
build/
dist/
out/

.pio/

.vscode/

*.log
*.bin
*.elf
```

---

# 1️⃣7️⃣ Development Workflow

```
Developer
   │
Create Branch
   │
Develop Feature
   │
Commit
   │
Push
   │
Merge Request
   │
Review
   │
Merge
```

---

# 1️⃣8️⃣ Commit Message Standard

รูปแบบ

```
<action> <description>
```

ตัวอย่าง

```
add CAN driver
fix motor timeout
update display UI
```

---

# 1️⃣9️⃣ SSH สำหรับ GitLab

สร้าง SSH key

```bash
ssh-keygen -t ed25519 -C "developer@example.com"
```

ดู public key

```bash
cat ~/.ssh/id_ed25519.pub
```

นำไปเพิ่มที่

GitLab → Settings → SSH Keys

---

# 2️⃣0️⃣ SSH เมื่อ Port 22 ถูก Block

แก้ไฟล์

```bash
nano ~/.ssh/config
```

เพิ่ม

```
# GitLab SSH over 443
Host gitlab.com
    HostName altssh.gitlab.com
    User git
    Port 443
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
    PreferredAuthentications publickey
```

ทดสอบ

```bash
ssh -T git@gitlab.com
```

---

# 2️⃣1️⃣ Git Flow Diagram

```
main
 │
 ├─ feature/new-ui
 ├─ feature/can-driver
 │
 ├─ bugfix/motor-timeout
 │
 └─ release/v1.0
```

แนวคิด

main = stable code

feature branch = พัฒนา feature

bugfix = แก้ bug

release = เตรียม release

---

# 2️⃣2️⃣ Release Management

ตัวอย่าง version

```
v1.0
v1.1
v1.2
```

สร้าง release branch

```bash
git checkout -b release/v1.0
```

Tag version

```bash
git tag v1.0

git push origin v1.0
```

---

# 2️⃣3️⃣ GitLab CI/CD Example (Firmware)

ตัวอย่าง `.gitlab-ci.yml`

```yaml
stages:
  - build

build_firmware:
  stage: build
  script:
    - echo "Building firmware"
```

CI/CD ใช้เพื่อ

* ตรวจสอบว่า build ผ่าน
* ป้องกัน code ที่ build ไม่ได้
* ทำ automation

---

# ✅ สรุป

Git ช่วยให้ทีมสามารถ

* ทำงานร่วมกันได้
* ติดตามการเปลี่ยนแปลงของ code
* ลดความเสี่ยงในการสูญหายของข้อมูล

Best practice

* commit บ่อย
* ใช้ branch แยกงาน
* review ก่อน merge

---

# 🔒 Security Note

เอกสารนี้ไม่มีข้อมูลจริง เช่น

* email
* username
* repository URL

เพื่อความปลอดภัยในการเผยแพร่
