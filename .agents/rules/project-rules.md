# AI Image Pro Studio — Project Rules

> กฎเหล่านี้บังคับใช้กับการพัฒนาทุกส่วนของโปรเจค อ้างอิงจาก PRD v5.6 และ "Neon Observatory" Design System จาก stitch UI references

---

## 1. Architecture Rules (กฎสถาปัตยกรรม)

- **Single Page Application (SPA):** ทั้งแอปต้องอยู่ในไฟล์ `index.html` ไฟล์เดียว — inline CSS + JavaScript
- **Vanilla JavaScript Only:** ห้ามใช้ Framework (React, Vue, Angular ฯลฯ), ห้ามใช้ buildtools/bundler
- **Technology Stack (ห้ามเบี่ยงเบน):**
  - HTML5, CSS3
  - Tailwind CSS via CDN: `https://cdn.tailwindcss.com?plugins=forms,container-queries`
  - Icons: **Material Symbols Outlined** via Google Fonts CDN
  - Fonts: **Manrope** (headline) + **Inter** (body/label) + Thai fonts (Kanit, Prompt, Sarabun, Sukhumvit)
  - JSZip via CDN (สำหรับ ZIP download)
  - Canvas API (สำหรับ render text บนภาพ)
- **ห้ามใช้** npm packages, node_modules, หรือ CDN อื่นที่ไม่ได้ระบุไว้

---

## 2. Design System Rules — "The Neon Observatory"

### 2.1 Tailwind Config (ต้องใส่ทุกครั้ง)

```js
tailwind.config = {
  darkMode: "class",
  theme: {
    extend: {
      colors: {
        "surface":                  "#0e0e0e",
        "surface-dim":              "#0e0e0e",
        "surface-container-lowest": "#000000",
        "surface-container-low":    "#131313",
        "surface-container":        "#1a1a1a",
        "surface-container-high":   "#20201f",
        "surface-container-highest":"#262626",
        "surface-bright":           "#2c2c2c",
        "surface-variant":          "#262626",
        "background":               "#0e0e0e",
        "on-background":            "#ffffff",
        "on-surface":               "#ffffff",
        "on-surface-variant":       "#adaaaa",
        "primary":                  "#b6a0ff",
        "primary-dim":              "#7e51ff",
        "primary-container":        "#a98fff",
        "primary-fixed":            "#a98fff",
        "primary-fixed-dim":        "#9c7eff",
        "surface-tint":             "#b6a0ff",
        "on-primary":               "#340090",
        "on-primary-fixed":         "#000000",
        "on-primary-container":     "#280072",
        "on-primary-fixed-variant": "#32008a",
        "inverse-primary":          "#6834eb",
        "secondary":                "#c492fe",
        "secondary-dim":            "#b987f2",
        "secondary-container":      "#5d2c92",
        "secondary-fixed":          "#e3c6ff",
        "secondary-fixed-dim":      "#d8b5ff",
        "on-secondary":             "#3e0174",
        "on-secondary-container":   "#e2c5ff",
        "on-secondary-fixed":       "#49147f",
        "on-secondary-fixed-variant":"#67389d",
        "tertiary":                 "#ff97b8",
        "tertiary-dim":             "#ef77a0",
        "tertiary-container":       "#fc81ab",
        "tertiary-fixed":           "#ff8db2",
        "tertiary-fixed-dim":       "#f57ca5",
        "on-tertiary":              "#6a0936",
        "on-tertiary-container":    "#59002b",
        "on-tertiary-fixed":        "#380019",
        "on-tertiary-fixed-variant":"#70103b",
        "error":                    "#ff6e84",
        "error-dim":                "#d73357",
        "error-container":          "#a70138",
        "on-error":                 "#490013",
        "on-error-container":       "#ffb2b9",
        "outline":                  "#767575",
        "outline-variant":          "#484847",
        "inverse-surface":          "#fcf9f8",
        "inverse-on-surface":       "#565555",
      },
      fontFamily: {
        "headline": ["Manrope"],
        "body":     ["Inter"],
        "label":    ["Inter"],
      },
      borderRadius: {
        "DEFAULT": "0.125rem",
        "lg":      "0.25rem",
        "xl":      "0.5rem",
        "full":    "0.75rem",
      },
    },
  },
}
```

### 2.2 กฎ "No-Line" (ห้ามใช้เส้นแบ่ง 1px)

> **ห้ามใช้ `border` สีเต็มในการแบ่งส่วน** — ใช้การ shift โทนสีพื้นหลังแทน

- แบ่ง sidebar กับ canvas: `surface-container-low` (#131313) → `surface-dim` (#0e0e0e)
- ถ้าจำเป็นต้องใช้ border: ใช้ `border-outline-variant/15` (opacity 15% เท่านั้น)
- ห้ามใช้ border opacity 100% เพื่อแบ่งส่วน

### 2.3 Glassmorphism (Glass Panel)

ใช้กับ: Floating toolbar, Prompt bar, Toast notifications, Overlay modals

```css
.glass-panel {
    background: rgba(32, 32, 31, 0.6);  /* หรือ rgba(38, 38, 38, 0.6) */
    backdrop-filter: blur(24px);
    border: 1px solid rgba(255, 255, 255, 0.1);
}
```

### 2.4 Signature Gradient (ปุ่ม CTA หลัก)

ปุ่ม Generate / Apply / Inspire Me **ต้องใช้ gradient นี้เสมอ:**

```css
.gradient-primary {
    background: linear-gradient(135deg, #b6a0ff 0%, #7e51ff 100%);
}
```

- Text บนปุ่ม gradient: `text-on-primary-fixed` (#000000)
- Glow shadow: `shadow-[0_0_20px_rgba(182,160,255,0.2)]`
- Hover: `hover:brightness-110`
- Active: `active:scale-95 transition-transform`

### 2.5 Typography

| Role | Font | ใช้กับ |
|------|------|--------|
| `font-headline` | Manrope 600–800 | Brand name, modal title, display text, ชื่อ workspace |
| `font-body` | Inter 400–600 | Content ทั่วไป, description, prompt text |
| `font-label` | Inter 500–700 | Labels, button text, ปุ่มเล็ก ๆ |

- **Labels:** `text-[10px]` หรือ `text-xs` + `uppercase` + `tracking-widest` + `font-bold` + `text-on-surface-variant`
- **Brand "Neon Observatory":** `bg-gradient-to-br from-violet-300 to-violet-600 bg-clip-text text-transparent font-headline tracking-tight`

### 2.6 Border Radius

| Token | ค่า | ใช้กับ |
|-------|-----|--------|
| `rounded` (DEFAULT) | 0.125rem | Badges, chips เล็ก |
| `rounded-lg` | 0.25rem | Cards ทั่วไป |
| `rounded-xl` | 0.5rem | Panel, modal, containers |
| `rounded-full` | 0.75rem | Buttons, pills, tags |

### 2.7 Shadows — ห้ามใช้ grey shadow ปกติ

| Component | Shadow |
|-----------|--------|
| Primary CTA | `shadow-[0_0_20px_rgba(182,160,255,0.2)]` |
| Hover state | `shadow-[0_0_30px_rgba(182,160,255,0.4)]` |
| Modal | `shadow-[0_32px_64px_rgba(0,0,0,0.6)]` |
| Navbar | `shadow-[0_8px_32px_rgba(0,0,0,0.5)]` |
| Sidebar right | `shadow-[-10px_0_30px_rgba(0,0,0,0.3)]` |
| Bottom toolbar | `shadow-[0_-8px_32px_rgba(0,0,0,0.5)]` |

---

## 3. Layout Rules (กฎ Layout)

### 3.1 Desktop Layout (≥ md breakpoint)

```
┌─────────────────────────────────────────────────────┐
│  Fixed TopNav (h-16, bg-surface/60 backdrop-blur-xl)│
├──────────────┬──────────────────────────────────────┤
│ Fixed Left   │  Main Canvas / Gallery               │
│ Sidebar      │  (bg-surface-dim, overflow-y-auto)   │
│ w-80 or w-20 │                                      │
│ bg-surface-  │                                      │
│ container-low│                                      │
│              │  ┌──────────────────────────────┐   │
│              │  │ Floating Prompt Bar (Fixed)  │   │
│              │  │ bottom-8, glass-panel, pill  │   │
│              │  └──────────────────────────────┘   │
└──────────────┴──────────────────────────────────────┘
```

### 3.2 Mobile Layout (< md breakpoint)

- เรียงจากบน → ล่าง: Controls → Gallery
- Prompt bar: sticky ติดด้านล่าง
- Bottom Nav: Fixed bottom, `rounded-t-xl`, icons + labels

### 3.3 Gallery Grid (Asymmetric Masonry)

```html
<div class="grid grid-cols-12 gap-6 auto-rows-[250px]">
  <!-- Featured Image -->
  <div class="col-span-8 row-span-2 ...">...</div>
  <!-- Secondary Square -->
  <div class="col-span-4 row-span-1 ...">...</div>
  <!-- Tall Side -->
  <div class="col-span-4 row-span-2 ...">...</div>
  <!-- Wide Image -->
  <div class="col-span-8 row-span-1 ...">...</div>
</div>
```

---

## 4. Component Rules (กฎ Components)

### 4.1 Buttons

| Type | Class |
|------|-------|
| Primary CTA | `gradient-primary text-on-primary-fixed rounded-full font-bold shadow-[...] hover:brightness-110 active:scale-95` |
| Secondary | `border border-outline-variant rounded-full hover:bg-surface-bright transition-colors` |
| Preset/Tag | `bg-surface-container-highest text-[10px] font-bold uppercase tracking-tighter rounded hover:bg-surface-bright border border-transparent active:border-primary/40` |
| Icon Button | `w-10 h-10 rounded-full bg-surface-container-high flex items-center justify-center hover:text-white` |

### 4.2 Inputs

```html
<input class="w-full bg-surface-container-highest border-none rounded text-xs 
              text-on-surface focus:ring-1 focus:ring-primary py-2" />
```

### 4.3 Sliders

```html
<!-- Track -->
<div class="h-1 bg-surface-variant rounded-full relative">
  <!-- Fill -->
  <div class="absolute left-0 top-0 h-full w-[64%] bg-primary-container rounded-full"></div>
  <!-- Thumb -->
  <div class="absolute left-[64%] top-1/2 -translate-y-1/2 w-4 h-4 bg-primary rounded-full 
              shadow-[0_0_10px_rgba(182,160,255,0.8)] cursor-pointer"></div>
</div>
```

### 4.4 Toast Notifications

```html
<!-- Top-right corner: fixed top-20 right-8 z-[100] -->
<!-- Success -->
<div class="glass-panel px-6 py-4 rounded-lg flex items-center gap-4 border-l-4 border-primary shadow-2xl">
  <div class="bg-primary/20 p-2 rounded-full">
    <span class="material-symbols-outlined text-primary" style="font-variation-settings:'FILL' 1">check_circle</span>
  </div>
  <div>
    <h4 class="font-headline text-white text-sm font-bold">สำเร็จ!</h4>
    <p class="text-on-surface-variant text-xs">ข้อความอธิบาย</p>
  </div>
  <span class="material-symbols-outlined text-on-surface-variant cursor-pointer hover:text-white">close</span>
</div>
<!-- Error: border-l-4 border-error, bg-error/20, text-error -->
```

### 4.5 Status Chips/Badges

```html
<!-- In Progress (secondary) -->
<span class="px-2 py-1 rounded bg-secondary/20 text-secondary text-[10px] font-bold uppercase">
  In Progress
</span>
<!-- Upscaling (tertiary) -->
<span class="px-2 py-1 rounded bg-tertiary/20 text-tertiary text-[10px] font-bold uppercase">
  Upscaling 4K
</span>
```

### 4.6 Confirmation Modal

```html
<div class="fixed inset-0 bg-neutral-950/80 backdrop-blur-sm z-[150] flex items-center justify-center p-6">
  <div class="bg-surface-container w-full max-w-md rounded-xl shadow-[0_48px_64px_-12px_rgba(0,0,0,0.8)] border border-outline-variant/15 p-8 text-center">
    <div class="w-16 h-16 bg-error/10 text-error rounded-full flex items-center justify-center mx-auto mb-6">
      <span class="material-symbols-outlined text-4xl">restart_alt</span>
    </div>
    <h2 class="font-headline text-2xl font-extrabold text-white mb-3">Reset Workspace?</h2>
    <p class="text-on-surface-variant text-sm mb-8">...</p>
    <div class="flex gap-3">
      <button class="flex-1 px-6 py-3.5 bg-error text-on-error font-bold rounded-full">Confirm</button>
      <button class="flex-1 px-6 py-3.5 bg-surface-container-highest font-bold rounded-full hover:bg-surface-bright">Cancel</button>
    </div>
  </div>
</div>
```

### 4.7 Prompt Breadcrumb

```html
<div class="flex items-center gap-2 text-[10px] font-bold uppercase tracking-widest">
  <span class="text-primary">Denoising</span>
  <span class="material-symbols-outlined text-[12px] text-on-surface-variant/40">chevron_right</span>
  <span class="text-on-surface-variant/60">Refinement</span>
  <span class="material-symbols-outlined text-[12px] text-on-surface-variant/40">chevron_right</span>
  <span class="text-on-surface-variant/60">Color Grade</span>
</div>
```

### 4.8 Post-Processing Bottom Toolbar

```html
<!-- Fixed bottom, rounded-t-xl, glass -->
<nav class="fixed bottom-0 left-0 w-full z-50 rounded-t-xl bg-[#131313]/80 backdrop-blur-2xl 
            border-t border-[#b6a0ff]/15 shadow-[0_-8px_32px_rgba(0,0,0,0.5)] flex justify-around items-center px-4 py-3">
  <!-- ปุ่ม active = gradient, ปุ่มปกติ = gray -->
  <button class="flex flex-col items-center bg-gradient-to-br from-[#b6a0ff] to-[#7e51ff] text-white rounded-lg p-2 shadow-[0_0_15px_rgba(182,160,255,0.4)]">
    <span class="material-symbols-outlined">magic_button</span>
    <span class="text-[10px] uppercase tracking-widest font-semibold mt-1">Magic Edit</span>
  </button>
  <button class="flex flex-col items-center text-[#adaaaa] p-2 hover:text-white hover:bg-[#20201f] active:scale-90 transition-transform">
    <span class="material-symbols-outlined">title</span>
    <span class="text-[10px] uppercase tracking-widest font-semibold mt-1">Typography</span>
  </button>
  <!-- Upscale 4K | Develop | 16:9 | Copy | Export -->
</nav>
```

---

## 5. Animation & Interaction Rules

- ทุก interactive element ต้องมี `transition-colors` หรือ `transition-all duration-200`
- Gallery image hover: `group-hover:scale-105 transition-transform duration-700`
- Button press: `active:scale-95 transition-transform`
- Status dot: `animate-pulse`
- Loading spinner: dual-ring (outer: `border-t-primary animate-[spin_2s_linear_infinite]`, inner: reverse)
- Progress bar shimmer:
  ```css
  @keyframes shimmer-move {
    0%   { background-position: -200% 0; }
    100% { background-position: 200% 0; }
  }
  .shimmer {
    background: linear-gradient(90deg, transparent, rgba(182,160,255,0.1), transparent);
    background-size: 200% 100%;
    animation: shimmer-move 2s infinite linear;
  }
  ```
- **SetBusy pattern:** ปิด/เปิด buttons ระหว่าง AI ประมวลผล เปลี่ยน icon เป็น spinner

---

## 6. Scrollbar Custom

```css
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: #0e0e0e; }
::-webkit-scrollbar-thumb { background: #262626; border-radius: 10px; }
::-webkit-scrollbar-thumb:hover { background: #b6a0ff33; }
```

---

## 7. API Rules

| Model | ใช้สำหรับ |
|-------|-----------|
| `gemini-2.5-flash-preview-09-2025` | Translation (ไทย→อังกฤษ), Inspire Me, Image-to-Text |
| `gemini-2.5-flash-image-preview` | Fast Generation, Image-to-Image, Magic Edit, Upscale |
| `imagen-4.0-generate-001` | High Quality Text-to-Image (Pro engine) |

- Safety: `BLOCK_ONLY_HIGH` ทุก category
- API key: เก็บใน JS constant, ไม่ commit ลง git
- Error: แสดง toast notification เสมอ อย่า crash เงียบ

---

## 8. Thai Language Rules

- UI ทุกส่วนรองรับภาษาไทย (placeholder, label, button)
- Typography Studio ต้องรองรับ fonts ไทย: Kanit, Prompt, Sarabun, Mitr, Sukhumvit Set, Thonburi, Krub, Itim, Pridi, Taviraj, Noto Sans Thai
- Text preview บน canvas: ใช้ `drop-shadow-2xl` หรือ `drop-shadow-[0_0_30px_rgba(182,160,255,0.6)]`
- Character encoding: UTF-8 เสมอ
