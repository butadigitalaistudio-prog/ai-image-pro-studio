Product Requirements Document (PRD)

Project Name: AI Image Pro Studio | Cinema Gear Enhanced
Version: 5.6
Document Date: 22 March 2026
Platform: Web Application (Responsive)

1. Executive Summary (บทสรุปผู้บริหาร)

AI Image Pro Studio เป็นเว็บแอปพลิเคชันสำหรับสร้างภาพด้วย AI ระดับมืออาชีพ ที่ออกแบบมาเพื่อลดกำแพงด้านภาษาและความซับซ้อนในการเขียน Prompt โดยเน้นกลุ่มเป้าหมายที่ต้องการภาพสไตล์ Cinematic และภาพถ่ายสมจริง ตัวแอปพลิเคชันรวมเอาเครื่องมือตั้งแต่การเขียน Prompt (รองรับภาษาไทย), การใช้ภาพอ้างอิง, การตั้งค่ามุมกล้อง/เลนส์แบบตากล้องมืออาชีพ ไปจนถึงระบบ Post-processing เช่น การอัปสเกลภาพ (Upscale), การแก้ไขเฉพาะจุด (Magic Edit) และการใส่ข้อความ (Typography Studio) ไว้ในที่เดียว

2. Target Audience (กลุ่มเป้าหมาย)

Content Creators / Marketers: ผู้ที่ต้องการภาพประกอบคอนเทนต์คุณภาพสูงอย่างรวดเร็ว โดยใช้คำสั่งภาษาไทย

Photographers / Digital Artists: ผู้ที่เข้าใจเรื่องมุมกล้อง เลนส์ และแสง ต้องการ AI ที่ตอบสนองต่อคำศัพท์เฉพาะทาง (Cinema Gear)

General Users: ผู้ใช้ทั่วไปที่ต้องการสร้างภาพสวยงาม แต่ไม่ถนัดเขียน Prompt แบบซับซ้อน (ใช้งานผ่านปุ่ม Preset สไตล์และท่าทาง)

3. Product Goals & Success Metrics (เป้าหมายและตัวชี้วัด)

Goal 1: ผู้ใช้สามารถสร้างภาพคุณภาพสูงได้โดยไม่ต้องมีทักษะ Prompt Engineering เชิงลึก

Goal 2: ระบบทำงานแบบ All-in-one Workspace (สร้าง -> แก้ไข -> ใส่ข้อความ -> Export) จบในหน้าเว็บเดียว

Goal 3: รองรับการทำงานร่วมกับภาษาไทยอย่างสมบูรณ์แบบ (Translate & Image-to-Text)

4. Core Features & Requirements (ฟีเจอร์หลัก)

4.1 ระบบการป้อนคำสั่ง (Prompt & Input Module)

Thai to English Translation: กล่องข้อความรองรับภาษาไทย และมีปุ่ม "แปลภาษา" เพื่อแปลงเป็น Prompt ภาษาอังกฤษที่ AI เข้าใจได้ดีกว่า

Native Prompt View: แสดง Prompt ภาษาอังกฤษที่ระบบแปลงให้ หรือที่ระบบจัดเรียงให้ เพื่อให้ผู้ใช้เห็นคำสั่งจริงที่ส่งไป

Inspire Me (ขอไอเดีย): ปุ่มสุ่มสร้าง Prompt ระดับศิลปินอัตโนมัติด้วย AI

Smart Prompt Assembly: ระบบจะนำ Text Prompt + Art Style + Pose + Cinema Gear มารวมกันอัตโนมัติก่อนส่งให้ AI

4.2 ระบบอ้างอิงภาพ (Visual Reference Module)

Image-to-Image (Reference Mode): อัปโหลดรูปภาพเพื่อใช้เป็นโครงสร้างหรือสไตล์อ้างอิง

Image-to-Prompt (ถอดรหัสรูปภาพ): ระบบ AI วิเคราะห์ภาพที่อัปโหลดและเขียน Prompt ภาษาไทยบรรยายภาพนั้นให้โดยอัตโนมัติ

Face Match: โหมดรักษาความสม่ำเสมอของใบหน้า (Upload รูปใบหน้าอ้างอิง) พร้อมปุ่มปรับ Prompt ให้เน้นความสมจริงของบุคคล

4.3 โมดูลปรับแต่งแบบมืออาชีพ (Pro Modifiers)

Art Styles Preset: ปุ่มสำเร็จรูปสำหรับเลือกสไตล์ภาพกว่า 20 สไตล์ (เช่น Cinematic, Anime, Cyberpunk, 3D Render)

Pose & Action Preset: ปุ่มสำเร็จรูปสำหรับกำหนดท่าทาง (เช่น Standing, Sitting, Action)

Cinema Gear & Composition: Dropdown ขั้นสูงสำหรับผู้ที่มีความรู้ด้านภาพถ่าย:

Camera Body: เลือกกล้อง (เช่น ARRI ALEXA, RED, IMAX, ฟิล์มคลาสสิก)

Lens: เลือกเลนส์ (เช่น 85mm f/1.2, เลนส์มุมกว้าง, เลนส์ตาปลา)

Camera Angle: เลือกมุมกล้อง (เช่น Eye-Level, Bird's Eye, Drone Shot)

Lighting: เลือกการจัดแสง (เช่น Golden Hour, Cyberpunk, Studio Softbox)

4.4 การตั้งค่าระบบ AI (Generation Settings)

AI Engines:

Nano Banana 2.5 (Fast) - เน้นความเร็ว

Nano Banana Pro (Quality) - เน้นคุณภาพสูงสุด

Aspect Ratio: เลือกสัดส่วนภาพ (1:1, 16:9, 9:16, 3:2, 2:3, 21:9)

Batch Count: เลือกจำนวนภาพที่ต้องการสร้างต่อครั้ง (1 ถึง 8 ภาพ)

4.5 ระบบคลังภาพ (Gallery & Export)

Masonry Grid Layout: แสดงผลภาพที่สร้างเสร็จแบบสวยงาม จัดเรียงอัตโนมัติ

Badges: แสดงสถานะภาพ (ภาพล่าสุด, ภาพ 4K Upscaled)

Download All (ZIP): ฟังก์ชันดาวน์โหลดภาพทั้งหมดที่สร้างขึ้น พร้อมไฟล์ Text แจ้ง Prompt ในรูปแบบไฟล์ .zip

4.6 สตูดิโอตกแต่งภาพ (Post-Processing Modal)

เมื่อคลิกดูภาพขนาดใหญ่ จะมีเครื่องมือดังนี้:

Magic Edit: พิมพ์คำสั่งภาษาไทยเพื่อแก้ไของค์ประกอบในภาพเฉพาะจุด (Inpainting / Image-to-Image)

Typography Studio: * ใส่ข้อความภาษาไทยลงบนภาพ

รองรับฟอนต์ไทยกว่า 11 แบบ (Google Fonts)

ปรับขนาด, สี, ความกว้างกรอบ, ระยะบรรทัด, เงา, และการจัดวาง (ซ้าย, กลาง, ขวา)

Drag & Drop ขยับตำแหน่งข้อความบนภาพได้อิสระ

Upscale 4K: ขยายขนาดและเพิ่มรายละเอียดภาพให้คมชัดระดับ 4K

Develop (พัฒนาต่อ): นำภาพนี้กลับไปตั้งเป็นภาพอ้างอิง (Reference) เพื่อสร้างภาพเจเนอเรชันถัดไป

Quick 16:9: สั่ง Generate ภาพนี้ใหม่โดยบังคับสัดส่วนเป็น 16:9 แนวนอนทันที

Export with Text: ปุ่มดาวน์โหลดภาพที่จะทำการ Render ข้อความรวมเข้ากับภาพ (Merge Canvas) เป็นไฟล์ PNG ไฟล์เดียว

4.7 ระบบการจัดการ (System Utilities)

Global Reset: ปุ่มรีเซ็ตล้างค่าทุกอย่างในระบบ (รูปภาพ, Prompt, Settings) เพื่อเริ่มต้นใหม่ พร้อม Modal ยืนยัน

Toast Notification: ระบบแจ้งเตือนมุมบนจอ (สถานะสำเร็จ, ข้อผิดพลาด)

5. Technical Specifications (ข้อกำหนดทางเทคนิค)

5.1 Technology Stack

Frontend: HTML5, CSS3

Styling Framework: Tailwind CSS (ผ่าน CDN)

Icons: Lucide Icons (ผ่าน CDN)

Font: Google Fonts (Inter, Kanit, Prompt, etc.)

Utilities: JSZip (สำหรับบีบอัดไฟล์ดาวน์โหลด), Canvas API (สำหรับการ Render Text ลงภาพ)

Architecture: Single Page Application (SPA) เขียนด้วย Vanilla JavaScript (ไม่มี Framework สวมทับ)

5.2 API & AI Models Integration

ระบบเชื่อมต่อกับ Google Generative AI API (generativelanguage.googleapis.com) โดยใช้โมเดลดังนี้:

Text & Translation (gemini-2.5-flash-preview-09-2025): ใช้สำหรับแปลภาษา, สร้างไอเดีย Prompt, และถอดรหัสรูปภาพเป็นข้อความ (Image-to-Text)

Fast Generation & Editing (gemini-2.5-flash-image-preview): ใช้สำหรับ Engine แบบ Fast, การทำ Image-to-Image, Magic Edit และ การ Upscale

High Quality Generation (imagen-4.0-generate-001): ใช้เป็น Engine หลัก (Pro) สำหรับการสร้างภาพจาก Text-to-Image คุณภาพสูง

5.3 Safety & Content Moderation

มีการตั้งค่า safetySettings ใน API เป็นระดับ BLOCK_ONLY_HIGH สำหรับทุกหมวดหมู่ (Harassment, Hate Speech, Explicit, Dangerous)

6. User Experience (UX) & User Interface (UI)

Theme: Dark Mode / Cinematic UI โทนสีเทาเข้ม-น้ำเงิน (Harmony Neutrals) เน้นความดูล้ำสมัยและสบายตาสำหรับผู้ทำงานกราฟิก

Responsive: เลย์เอาต์ปรับเปลี่ยนได้:

Desktop/Tablet: แบ่งจอซ้าย (Controls) / ขวา (Gallery + Prompt Bar)

Mobile: เรียงจากบนลงล่าง (Controls -> Gallery -> Prompt Bar ยึดติดด้านล่าง)

Feedback System: * ปุ่มกดมี State (Active/Disabled/Loading)

เปลี่ยน Icon เป็น Spinner ระหว่างรอ AI ประมวลผล

ป้องกันการกดซ้ำระหว่างระบบทำงาน (SetBusy function)

7. Future Considerations (ข้อเสนอแนะสำหรับการพัฒนาต่อยอด)

User Authentication & Cloud Storage: เพิ่มระบบ Login (เช่น Firebase Auth) เพื่อบันทึกประวัติภาพถ่ายของแต่ละผู้ใช้ลง Cloud (Firestore) แทนที่จะหายไปเมื่อรีเฟรชหน้าเว็บ

History / Prompt Library: ระบบให้ผู้ใช้บันทึก Prompt ที่ชอบเก็บไว้ใช้ส่วนตัว (Favorites)

Advanced ControlNet: หาก API รองรับในอนาคต อาจเพิ่มการตั้งค่า Depth Map หรือ Edge Detection สำหรับการควบคุมภาพอ้างอิงที่แม่นยำขึ้น

Undo/Redo ใน Typography: เพิ่มความสามารถในการย้อนกลับการกระทำในโหมดใส่ข้อความ