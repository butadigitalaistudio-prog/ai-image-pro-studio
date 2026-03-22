---
name: neon-observatory-design-system
description: Use this skill when building any UI component for the AI Image Pro Studio project. It provides the exact Neon Observatory design system tokens, component templates, and patterns extracted from the stitch UI references. Apply this skill whenever you need to implement any visual element, layout, or interactive component.
---

# Skill: Neon Observatory Design System

This skill provides copy-paste–ready templates for every UI component in the AI Image Pro Studio app, based on the official stitch UI references.

---

## Quick Reference: Color Tokens

| Token | Hex | Use |
|-------|-----|-----|
| `surface` | #0e0e0e | Base background |
| `surface-container-low` | #131313 | Sidebar, panels |
| `surface-container` | #1a1a1a | Tool groups |
| `surface-container-high` | #20201f | Nested controls |
| `surface-container-highest` | #262626 | Input backgrounds |
| `surface-bright` | #2c2c2c | Hover states |
| `primary` | #b6a0ff | Accent, active |
| `primary-dim` | #7e51ff | Gradient end |
| `secondary` | #c492fe | In-progress chip |
| `tertiary` | #ff97b8 | Upscaling chip |
| `error` | #ff6e84 | Destructive ONLY |
| `on-surface` | #ffffff | Primary text |
| `on-surface-variant` | #adaaaa | Secondary text |
| `outline-variant` | #484847 | Ghost border (at/15% max) |

---

## Required `<head>` Block

```html
<html class="dark" lang="th">
<head>
  <meta charset="utf-8"/>
  <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
  <title>AI Image Pro Studio</title>
  <script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=Manrope:wght@500;600;700;800&family=Kanit:wght@300;400;600;700&family=Sarabun:wght@300;400;600;700&display=swap" rel="stylesheet"/>
  <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet"/>
  <script id="tailwind-config">
    tailwind.config = {
      darkMode: "class",
      theme: {
        extend: {
          colors: {
            "surface": "#0e0e0e", "surface-dim": "#0e0e0e",
            "surface-container-lowest": "#000000",
            "surface-container-low": "#131313",
            "surface-container": "#1a1a1a",
            "surface-container-high": "#20201f",
            "surface-container-highest": "#262626",
            "surface-bright": "#2c2c2c",
            "surface-variant": "#262626",
            "surface-tint": "#b6a0ff",
            "background": "#0e0e0e", "on-background": "#ffffff",
            "on-surface": "#ffffff", "on-surface-variant": "#adaaaa",
            "primary": "#b6a0ff", "primary-dim": "#7e51ff",
            "primary-container": "#a98fff", "primary-fixed": "#a98fff",
            "primary-fixed-dim": "#9c7eff", "on-primary": "#340090",
            "on-primary-fixed": "#000000", "on-primary-container": "#280072",
            "on-primary-fixed-variant": "#32008a", "inverse-primary": "#6834eb",
            "secondary": "#c492fe", "secondary-dim": "#b987f2",
            "secondary-container": "#5d2c92", "secondary-fixed": "#e3c6ff",
            "secondary-fixed-dim": "#d8b5ff", "on-secondary": "#3e0174",
            "on-secondary-container": "#e2c5ff", "on-secondary-fixed": "#49147f",
            "on-secondary-fixed-variant": "#67389d",
            "tertiary": "#ff97b8", "tertiary-dim": "#ef77a0",
            "tertiary-container": "#fc81ab", "tertiary-fixed": "#ff8db2",
            "tertiary-fixed-dim": "#f57ca5", "on-tertiary": "#6a0936",
            "on-tertiary-container": "#59002b", "on-tertiary-fixed": "#380019",
            "on-tertiary-fixed-variant": "#70103b",
            "error": "#ff6e84", "error-dim": "#d73357",
            "error-container": "#a70138", "on-error": "#490013",
            "on-error-container": "#ffb2b9",
            "outline": "#767575", "outline-variant": "#484847",
            "inverse-surface": "#fcf9f8", "inverse-on-surface": "#565555",
          },
          fontFamily: {
            "headline": ["Manrope"],
            "body": ["Inter"],
            "label": ["Inter"],
          },
          borderRadius: {
            "DEFAULT": "0.125rem",
            "lg": "0.25rem",
            "xl": "0.5rem",
            "full": "0.75rem",
          },
        },
      },
    }
  </script>
  <style>
    .material-symbols-outlined {
      font-variation-settings: 'FILL' 0, 'wght' 400, 'GRAD' 0, 'opsz' 24;
      vertical-align: middle;
    }
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: #0e0e0e; }
    ::-webkit-scrollbar-thumb { background: #262626; border-radius: 10px; }
    ::-webkit-scrollbar-thumb:hover { background: #b6a0ff33; }

    .glass-panel {
      background: rgba(32, 32, 31, 0.6);
      backdrop-filter: blur(24px);
    }
    .gradient-primary {
      background: linear-gradient(135deg, #b6a0ff 0%, #7e51ff 100%);
    }
    .text-neon-glow { text-shadow: 0 0 10px rgba(182, 160, 255, 0.4); }

    @keyframes spin-slow {
      from { transform: rotate(0deg); }
      to { transform: rotate(360deg); }
    }
    .animate-spin-slow { animation: spin-slow 2s linear infinite; }

    @keyframes shimmer-move {
      0%   { background-position: -200% 0; }
      100% { background-position: 200% 0; }
    }
    .shimmer {
      background: linear-gradient(90deg, transparent, rgba(182,160,255,0.1), transparent);
      background-size: 200% 100%;
      animation: shimmer-move 2s infinite linear;
    }
  </style>
</head>
<body class="bg-background text-on-background font-body selection:bg-primary selection:text-on-primary overflow-hidden">
```

---

## Component Templates

### Top Navigation Bar

```html
<header class="fixed top-0 w-full z-50 bg-[#0e0e0e]/60 backdrop-blur-xl shadow-[0_8px_32px_rgba(0,0,0,0.5)] flex justify-between items-center px-6 h-16">
  <!-- Left: Brand + Nav -->
  <div class="flex items-center gap-8">
    <span class="text-xl font-black bg-gradient-to-br from-violet-300 to-violet-600 bg-clip-text text-transparent font-headline tracking-tight">
      AI Image Pro Studio
    </span>
    <nav class="hidden md:flex gap-6 items-center">
      <a class="font-body text-sm font-medium text-white" href="#">Visual Reference</a>
      <a class="font-body text-sm font-medium text-on-surface-variant hover:text-white transition-colors" href="#">Pro Modifiers</a>
      <a class="font-body text-sm font-medium text-on-surface-variant hover:text-white transition-colors" href="#">Cinema Gear</a>
    </nav>
  </div>
  <!-- Right: Actions -->
  <div class="flex items-center gap-3">
    <button id="btn-reset" class="flex items-center gap-2 px-4 py-2 rounded-full border border-outline-variant hover:bg-surface-bright transition-colors text-sm font-medium text-on-surface">
      <span class="material-symbols-outlined text-sm">refresh</span>
      <span>รีเซ็ต</span>
    </button>
    <button id="btn-inspire" class="flex items-center gap-2 px-5 py-2 rounded-full gradient-primary text-on-primary-fixed font-bold text-sm shadow-[0_0_20px_rgba(182,160,255,0.2)] active:scale-95 transition-transform">
      <span class="material-symbols-outlined text-sm" style="font-variation-settings:'FILL' 1">auto_awesome</span>
      <span>Inspire Me</span>
    </button>
  </div>
</header>
```

---

### Left Sidebar (Control Panel)

```html
<aside class="fixed left-0 top-16 h-[calc(100vh-64px)] w-80 bg-surface-container-low flex flex-col py-4 overflow-y-auto z-40">
  
  <!-- Section Label -->
  <div class="px-6 mb-4">
    <div class="flex items-center gap-2 text-primary mb-4">
      <span class="material-symbols-outlined">image</span>
      <span class="font-medium text-sm">Visual Reference</span>
    </div>
    <!-- Upload Zone -->
    <div class="border-2 border-dashed border-outline-variant rounded-xl p-6 flex flex-col items-center justify-center bg-surface-container-low hover:bg-surface-container transition-colors cursor-pointer group">
      <span class="material-symbols-outlined text-on-surface-variant group-hover:text-primary transition-colors mb-2">cloud_upload</span>
      <p class="text-xs text-on-surface-variant text-center leading-relaxed">ลากภาพมาวางที่นี่<br/><span class="text-on-surface font-semibold">Face Match</span></p>
    </div>
    <button class="w-full mt-3 py-2 text-xs font-bold uppercase tracking-widest text-primary border border-primary/20 rounded hover:bg-primary/10 transition-colors">
      ถอดรหัสรูปภาพ
    </button>
  </div>

  <!-- Art Style Presets -->
  <div class="px-6 mb-4">
    <div class="flex items-center gap-2 text-primary mb-4">
      <span class="material-symbols-outlined">palette</span>
      <span class="font-medium text-sm">Art Styles & Pose</span>
    </div>
    <div class="grid grid-cols-2 gap-2">
      <!-- Active preset: add border-primary/40 -->
      <button class="bg-surface-container-highest text-on-surface py-2 rounded text-[10px] font-bold uppercase tracking-tighter hover:bg-surface-bright border border-transparent active:border-primary/40">Cyberpunk</button>
      <button class="bg-surface-container-highest text-on-surface py-2 rounded text-[10px] font-bold uppercase tracking-tighter hover:bg-surface-bright border border-transparent active:border-primary/40">Cinematic</button>
      <button class="bg-surface-container-highest text-on-surface py-2 rounded text-[10px] font-bold uppercase tracking-tighter hover:bg-surface-bright border border-transparent active:border-primary/40">Anime</button>
      <button class="bg-surface-container-highest text-on-surface py-2 rounded text-[10px] font-bold uppercase tracking-tighter hover:bg-surface-bright border border-transparent active:border-primary/40">3D Render</button>
    </div>
  </div>

  <!-- Cinema Gear -->
  <div class="px-6 mb-4">
    <div class="flex items-center gap-2 text-primary mb-4">
      <span class="material-symbols-outlined">movie_filter</span>
      <span class="font-medium text-sm">Camera & Lighting</span>
    </div>
    <div class="space-y-3">
      <div class="space-y-1">
        <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">Camera Body</label>
        <select class="w-full bg-surface-container-highest border-none rounded text-xs text-on-surface focus:ring-1 focus:ring-primary py-2">
          <option>ARRI Alexa 35</option>
          <option>RED V-Raptor</option>
          <option>IMAX Film</option>
          <option>Sony A7R IV</option>
        </select>
      </div>
      <div class="space-y-1">
        <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">Lens</label>
        <select class="w-full bg-surface-container-highest border-none rounded text-xs text-on-surface focus:ring-1 focus:ring-primary py-2">
          <option>85mm f/1.2</option>
          <option>35mm f/1.4</option>
          <option>Anamorphic 40mm</option>
        </select>
      </div>
      <div class="grid grid-cols-2 gap-2">
        <div class="space-y-1">
          <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">Angle</label>
          <select class="w-full bg-surface-container-highest border-none rounded text-xs text-on-surface focus:ring-1 focus:ring-primary py-2">
            <option>Eye Level</option>
            <option>Low Angle</option>
            <option>Bird's Eye</option>
            <option>Drone Shot</option>
          </select>
        </div>
        <div class="space-y-1">
          <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">Lighting</label>
          <select class="w-full bg-surface-container-highest border-none rounded text-xs text-on-surface focus:ring-1 focus:ring-primary py-2">
            <option>Golden Hour</option>
            <option>Cyberpunk Neon</option>
            <option>Studio Softbox</option>
          </select>
        </div>
      </div>
    </div>
  </div>

  <!-- AI Settings -->
  <div class="px-6 mb-4">
    <div class="flex items-center gap-2 text-primary mb-4">
      <span class="material-symbols-outlined">settings</span>
      <span class="font-medium text-sm">Settings</span>
    </div>
    <div class="space-y-4">
      <!-- AI Engine -->
      <div class="space-y-1">
        <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">AI Engine</label>
        <select class="w-full bg-surface-container-highest border-none rounded text-xs text-on-surface focus:ring-1 focus:ring-primary py-2">
          <option value="flash">Nano Banana 2.5 (Fast)</option>
          <option value="imagen">Nano Banana Pro (Quality)</option>
        </select>
      </div>
      <!-- Aspect Ratio -->
      <div class="space-y-1">
        <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">Aspect Ratio</label>
        <div class="flex gap-2">
          <button class="flex-1 bg-surface-container-highest border border-primary/40 rounded py-2 flex flex-col items-center gap-1">
            <div class="w-4 h-4 border border-on-surface rounded-sm"></div>
            <span class="text-[9px] font-bold">1:1</span>
          </button>
          <button class="flex-1 bg-surface-container-highest hover:bg-surface-bright rounded py-2 flex flex-col items-center gap-1">
            <div class="w-6 h-4 border border-on-surface-variant rounded-sm"></div>
            <span class="text-[9px] font-bold text-on-surface-variant">16:9</span>
          </button>
          <button class="flex-1 bg-surface-container-highest hover:bg-surface-bright rounded py-2 flex flex-col items-center gap-1">
            <div class="w-3 h-5 border border-on-surface-variant rounded-sm"></div>
            <span class="text-[9px] font-bold text-on-surface-variant">9:16</span>
          </button>
        </div>
      </div>
      <!-- Batch Count Slider -->
      <div class="space-y-2">
        <div class="flex justify-between items-center">
          <label class="text-[10px] text-on-surface-variant uppercase font-bold tracking-widest">Image Count</label>
          <span id="batch-count-display" class="text-xs font-bold text-primary">4</span>
        </div>
        <input id="batch-count" class="w-full h-1 bg-surface-variant rounded-lg appearance-none cursor-pointer accent-primary" max="8" min="1" type="range" value="4"/>
      </div>
    </div>
  </div>

  <!-- Generate Button (sticky bottom of sidebar) -->
  <div class="mt-auto px-6 border-t border-outline-variant/10 pt-4 pb-4">
    <button id="btn-generate" class="w-full gradient-primary text-on-primary-fixed font-bold py-3 rounded-xl flex items-center justify-center gap-2 group shadow-[0_0_20px_rgba(182,160,255,0.1)] active:scale-95 transition-transform">
      <span class="material-symbols-outlined text-xl group-hover:rotate-12 transition-transform">bolt</span>
      GENERATE IMAGE
    </button>
  </div>
</aside>
```

---

### Floating Prompt Bar

```html
<div class="fixed bottom-8 left-1/2 -translate-x-1/2 w-[calc(100%-40rem)] max-w-4xl glass-panel border border-outline-variant/30 rounded-full py-2 px-2 flex items-center shadow-2xl z-30">
  <div class="flex-1 flex items-center px-6">
    <input id="prompt-input" class="w-full bg-transparent border-none focus:ring-0 text-on-surface placeholder-on-surface-variant text-sm py-2" placeholder="อธิบายภาพที่คุณต้องการ (รองรับภาษาไทย)..." type="text"/>
  </div>
  <div class="flex items-center gap-2 pr-2">
    <button id="btn-translate" class="w-10 h-10 rounded-full bg-surface-container-high flex items-center justify-center text-on-surface-variant hover:text-white transition-colors" title="แปลภาษา">
      <span class="material-symbols-outlined">translate</span>
    </button>
    <button id="btn-generate-bar" class="gradient-primary text-on-primary-fixed px-6 py-2.5 rounded-full font-bold text-xs flex items-center gap-2 active:scale-95 transition-transform">
      <span>GENERATE</span>
      <span class="material-symbols-outlined text-sm">rocket_launch</span>
    </button>
  </div>
</div>
```

---

### Gallery (Asymmetric Masonry Grid)

```html
<section class="ml-80 flex-1 p-8 overflow-y-auto bg-surface-dim">
  <!-- Prompt Breadcrumb -->
  <div class="flex items-center gap-3 mb-8">
    <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-surface-container text-primary text-xs font-semibold border border-primary/20">
      <span class="material-symbols-outlined text-sm" style="font-variation-settings:'FILL' 1">blur_on</span>
      Denoising
    </div>
    <div class="w-4 h-px bg-outline-variant"></div>
    <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-surface-container text-on-surface-variant text-xs font-semibold">
      <span class="material-symbols-outlined text-sm">auto_fix</span>
      Refinement
    </div>
    <div class="w-4 h-px bg-outline-variant"></div>
    <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-surface-container text-on-surface-variant text-xs font-semibold">
      <span class="material-symbols-outlined text-sm">palette</span>
      Color Grade
    </div>
  </div>

  <!-- Asymmetric Grid -->
  <div id="gallery" class="grid grid-cols-12 gap-6 auto-rows-[250px]">
    <!-- Featured Image (8 cols, 2 rows) -->
    <div class="col-span-8 row-span-2 relative group overflow-hidden rounded-xl bg-surface-container cursor-pointer">
      <img class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105" src="" alt=""/>
      <!-- Hover Overlay -->
      <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity p-6 flex flex-col justify-end">
        <div class="flex gap-2 mb-3">
          <span class="px-2 py-1 rounded bg-secondary/20 text-secondary text-[10px] font-bold uppercase">ล่าสุด</span>
          <span class="px-2 py-1 rounded bg-tertiary/20 text-tertiary text-[10px] font-bold uppercase">4K</span>
        </div>
        <p class="text-white text-sm font-medium">prompt text here...</p>
      </div>
      <!-- Primary border on hover -->
      <div class="absolute inset-0 border-2 border-primary opacity-0 group-hover:opacity-100 transition-opacity rounded-xl pointer-events-none"></div>
    </div>
    <!-- Secondary images: col-span-4 row-span-1, col-span-4 row-span-2, etc. -->
  </div>
</section>
```

---

### Magic Edit Modal

```html
<!-- Full screen overlay -->
<div id="modal-magic-edit" class="fixed inset-0 bg-black/40 backdrop-blur-[4px] flex items-center justify-center p-6 z-50 hidden">
  <div class="w-full max-w-xl glass-panel p-8 rounded-2xl shadow-[0_32px_64px_rgba(0,0,0,0.6)]">
    <!-- Breadcrumb -->
    <div class="flex items-center gap-3 mb-6">
      <span class="text-[10px] font-semibold uppercase tracking-widest text-on-surface-variant/80">Active Process</span>
      <div class="flex items-center gap-2 text-[10px] font-bold uppercase tracking-widest">
        <span class="text-on-surface-variant/60">Selection</span>
        <span class="material-symbols-outlined text-[12px] text-on-surface-variant/40">chevron_right</span>
        <span class="text-primary text-neon-glow">Refinement</span>
        <span class="material-symbols-outlined text-[12px] text-on-surface-variant/40">chevron_right</span>
        <span class="text-on-surface-variant/60">Synthesis</span>
      </div>
    </div>
    <!-- Header -->
    <h2 class="font-headline text-3xl font-extrabold tracking-tight bg-gradient-to-r from-white via-primary to-violet-400 bg-clip-text text-transparent text-neon-glow">
      Magic Edit
    </h2>
    <p class="text-on-surface-variant text-sm mt-1 mb-6">พิมพ์คำสั่งภาษาไทยเพื่อแก้ไขภาพ</p>
    <!-- Input -->
    <div class="relative group">
      <div class="absolute inset-y-0 left-4 flex items-start pt-4 pointer-events-none">
        <span class="material-symbols-outlined text-on-surface-variant/50 text-xl group-focus-within:text-primary transition-colors">auto_fix_normal</span>
      </div>
      <textarea id="magic-edit-prompt" class="w-full bg-neutral-900/80 border border-white/5 focus:border-primary/50 focus:ring-4 focus:ring-primary/10 rounded-xl pl-12 pr-4 py-4 text-sm text-white placeholder-on-surface-variant/50 resize-none h-32 transition-all" placeholder="เช่น เปลี่ยนพื้นหลังเป็นเมืองไซเบอร์พังค์..."></textarea>
    </div>
    <!-- Quick Chips -->
    <div class="mt-4">
      <p class="text-[10px] font-bold uppercase tracking-widest text-on-surface-variant/60 mb-3">Quick Suggestions</p>
      <div class="flex flex-wrap gap-2">
        <button class="px-3 py-1.5 rounded-full bg-white/5 border border-white/10 hover:border-primary/40 hover:bg-primary/5 text-[11px] font-medium transition-all text-on-surface-variant hover:text-primary">Cyberpunk city background</button>
        <button class="px-3 py-1.5 rounded-full bg-white/5 border border-white/10 hover:border-primary/40 hover:bg-primary/5 text-[11px] font-medium transition-all text-on-surface-variant hover:text-primary">Add neon glasses</button>
        <button class="px-3 py-1.5 rounded-full bg-white/5 border border-white/10 hover:border-primary/40 hover:bg-primary/5 text-[11px] font-medium transition-all text-on-surface-variant hover:text-primary">Make it golden hour</button>
      </div>
    </div>
    <!-- Footer -->
    <div class="flex items-center justify-between mt-8">
      <div class="flex items-center gap-2 text-on-surface-variant/40">
        <span class="material-symbols-outlined text-sm" style="font-variation-settings:'FILL' 1">terminal</span>
        <span class="text-[10px] font-bold tracking-widest uppercase">Gemini Flash Engine</span>
      </div>
      <div class="flex items-center gap-3">
        <button onclick="document.getElementById('modal-magic-edit').classList.add('hidden')" class="px-6 py-2.5 rounded-xl text-sm font-semibold text-on-surface-variant hover:text-white hover:bg-white/5 transition-all">Cancel</button>
        <button id="btn-apply-magic-edit" class="bg-neon-gradient px-8 py-2.5 rounded-xl text-sm font-extrabold text-black shadow-[0_0_20px_rgba(182,160,255,0.2)] hover:shadow-[0_0_30px_rgba(182,160,255,0.4)] hover:brightness-110 active:scale-95 transition-all flex items-center gap-2" style="background:linear-gradient(135deg,#b6a0ff,#7e51ff)">
          <span>Apply Change</span>
          <span class="material-symbols-outlined text-[18px]">bolt</span>
        </button>
      </div>
    </div>
  </div>
</div>
```

---

### Loading / Processing State

```html
<!-- Spinner -->
<div class="relative mb-12">
  <!-- Outer ring -->
  <div class="h-32 w-32 rounded-full border-2 border-primary/20 border-t-primary animate-spin-slow"></div>
  <!-- Inner ring (reverse) -->
  <div class="absolute inset-0 flex items-center justify-center">
    <div class="h-20 w-20 rounded-full border border-secondary/30 border-b-secondary animate-[spin_1.5s_linear_infinite_reverse]"></div>
    <div class="absolute text-primary text-xl font-bold font-headline animate-pulse">AI</div>
  </div>
  <!-- Glow orbs -->
  <div class="absolute -top-4 -right-4 h-8 w-8 rounded-full bg-primary/20 blur-xl animate-pulse"></div>
  <div class="absolute -bottom-2 -left-2 h-6 w-6 rounded-full bg-secondary/20 blur-lg animate-pulse delay-700"></div>
</div>
<h1 class="font-headline text-3xl font-extrabold tracking-tight text-white mb-2">Processing...</h1>
<p class="text-on-surface-variant text-sm mb-8">AI กำลังสร้างภาพของคุณ...</p>
<!-- Progress bar -->
<div class="w-full space-y-2">
  <div class="flex justify-between items-end">
    <span class="text-[10px] font-bold uppercase tracking-[0.2em] text-primary">Diffusion Stage: Denoising</span>
    <span class="font-headline text-lg font-bold text-white" id="progress-pct">0%</span>
  </div>
  <div class="h-1.5 w-full bg-surface-variant rounded-full overflow-hidden">
    <div id="progress-bar" class="h-full bg-gradient-to-r from-primary to-secondary w-0 relative transition-all duration-500">
      <div class="absolute inset-0 shimmer"></div>
    </div>
  </div>
</div>
<!-- Disabled generate button during processing -->
<button class="w-full py-4 rounded-full bg-neutral-800 text-neutral-500 font-bold font-headline flex items-center justify-center gap-3 cursor-not-allowed opacity-80 border border-neutral-700" disabled>
  <span class="material-symbols-outlined animate-spin-slow text-violet-500">sync</span>
  Generating...
</button>
```

---

### Post-Processing Bottom Toolbar

```html
<!-- ใช้ใน Post-Processing modal สำหรับ image view -->
<nav class="fixed bottom-0 left-0 w-full z-50 rounded-t-xl bg-[#131313]/80 backdrop-blur-2xl border-t border-[#b6a0ff]/15 shadow-[0_-8px_32px_rgba(0,0,0,0.5)] flex justify-around items-center px-4 py-3">
  <!-- Active button (gradient) -->
  <button class="flex flex-col items-center bg-gradient-to-br from-[#b6a0ff] to-[#7e51ff] text-white rounded-lg p-2 shadow-[0_0_15px_rgba(182,160,255,0.4)] active:scale-90 transition-transform">
    <span class="material-symbols-outlined">magic_button</span>
    <span class="font-body text-[10px] uppercase tracking-widest font-semibold mt-1">Magic Edit</span>
  </button>
  <!-- Inactive buttons -->
  <button class="flex flex-col items-center text-on-surface-variant p-2 hover:text-white hover:bg-surface-container-high active:scale-90 transition-transform">
    <span class="material-symbols-outlined">title</span>
    <span class="font-body text-[10px] uppercase tracking-widest font-semibold mt-1">Typography</span>
  </button>
  <button class="flex flex-col items-center text-on-surface-variant p-2 hover:text-white hover:bg-surface-container-high active:scale-90 transition-transform">
    <span class="material-symbols-outlined">high_quality</span>
    <span class="font-body text-[10px] uppercase tracking-widest font-semibold mt-1">Upscale 4K</span>
  </button>
  <button class="flex flex-col items-center text-on-surface-variant p-2 hover:text-white hover:bg-surface-container-high active:scale-90 transition-transform">
    <span class="material-symbols-outlined">tune</span>
    <span class="font-body text-[10px] uppercase tracking-widest font-semibold mt-1">Develop</span>
  </button>
  <button class="flex flex-col items-center text-on-surface-variant p-2 hover:text-white hover:bg-surface-container-high active:scale-90 transition-transform">
    <span class="material-symbols-outlined">aspect_ratio</span>
    <span class="font-body text-[10px] uppercase tracking-widest font-semibold mt-1">16:9</span>
  </button>
  <button class="flex flex-col items-center text-on-surface-variant p-2 hover:text-white hover:bg-surface-container-high active:scale-90 transition-transform">
    <span class="material-symbols-outlined">ios_share</span>
    <span class="font-body text-[10px] uppercase tracking-widest font-semibold mt-1">Export</span>
  </button>
</nav>
```

---

### Typography Studio Sidebar

```html
<aside class="fixed right-0 top-16 h-[calc(100vh-128px)] w-80 z-40 flex flex-col border-l border-[#b6a0ff]/10 bg-[#131313] shadow-[-10px_0_30px_rgba(0,0,0,0.3)]">
  <!-- Header -->
  <div class="p-6 border-b border-outline-variant/15">
    <h3 class="text-white font-black text-sm uppercase tracking-wider">Typography Studio</h3>
    <p class="text-on-surface-variant text-xs">Post-Processing</p>
  </div>
  <!-- Tabs -->
  <div class="flex bg-surface-container-low border-b border-outline-variant/10">
    <button class="flex-1 py-4 flex flex-col items-center gap-1 border-r-4 border-primary text-white bg-surface-container-high">
      <span class="material-symbols-outlined text-lg">match_case</span>
      <span class="text-[10px] font-semibold uppercase tracking-wider">Font</span>
    </button>
    <button class="flex-1 py-4 flex flex-col items-center gap-1 text-on-surface-variant hover:bg-surface-container hover:text-primary transition-all">
      <span class="material-symbols-outlined text-lg">palette</span>
      <span class="text-[10px] font-semibold uppercase tracking-wider">Color</span>
    </button>
    <button class="flex-1 py-4 flex flex-col items-center gap-1 text-on-surface-variant hover:bg-surface-container hover:text-primary transition-all">
      <span class="material-symbols-outlined text-lg">format_size</span>
      <span class="text-[10px] font-semibold uppercase tracking-wider">Size</span>
    </button>
    <button class="flex-1 py-4 flex flex-col items-center gap-1 text-on-surface-variant hover:bg-surface-container hover:text-primary transition-all">
      <span class="material-symbols-outlined text-lg">format_align_center</span>
      <span class="text-[10px] font-semibold uppercase tracking-wider">Align</span>
    </button>
  </div>
  <!-- Controls -->
  <div class="flex-1 overflow-y-auto p-6 space-y-6">
    <!-- Text input -->
    <div class="space-y-2">
      <label class="text-xs font-semibold text-on-surface-variant uppercase tracking-widest">Thai Text</label>
      <textarea id="typography-text" class="w-full bg-surface-container-highest border-none rounded-lg text-on-surface p-4 text-lg min-h-[100px] shadow-inner focus:ring-1 focus:ring-primary" placeholder="พิมพ์ข้อความที่นี่..."></textarea>
    </div>
    <!-- Font list -->
    <div class="space-y-3">
      <label class="text-xs font-semibold text-on-surface-variant uppercase tracking-widest">Thai Fonts</label>
      <div class="grid grid-cols-1 gap-2">
        <button class="w-full flex items-center justify-between p-3 rounded-lg bg-surface-container-high border-l-2 border-primary text-on-surface">
          <span class="font-bold">Kanit</span>
          <span class="material-symbols-outlined text-primary text-sm" style="font-variation-settings:'FILL' 1">check_circle</span>
        </button>
        <button class="w-full flex items-center justify-between p-3 rounded-lg bg-surface-container hover:bg-surface-bright transition-all text-on-surface-variant">
          <span>Sarabun</span>
        </button>
        <button class="w-full flex items-center justify-between p-3 rounded-lg bg-surface-container hover:bg-surface-bright transition-all text-on-surface-variant">
          <span>Prompt</span>
        </button>
      </div>
    </div>
    <!-- Slider: Font Size -->
    <div class="space-y-2">
      <div class="flex justify-between text-[11px] font-bold text-on-surface-variant">
        <span>FONT SIZE</span>
        <span class="text-primary" id="font-size-val">64px</span>
      </div>
      <div class="h-1 bg-surface-variant rounded-full relative">
        <div class="absolute left-0 top-0 h-full w-[64%] bg-primary-container rounded-full"></div>
        <div class="absolute left-[64%] -top-1.5 h-4 w-4 bg-primary rounded-full shadow-[0_0_10px_rgba(182,160,255,0.8)] cursor-pointer"></div>
      </div>
    </div>
    <!-- Alignment -->
    <div class="space-y-2">
      <label class="text-[10px] font-bold uppercase tracking-widest text-on-surface-variant">Alignment</label>
      <div class="flex gap-1 bg-surface-container-high p-1 rounded-lg">
        <button class="flex-1 py-2 rounded hover:bg-surface-bright flex justify-center"><span class="material-symbols-outlined text-sm">format_align_left</span></button>
        <button class="flex-1 py-2 rounded bg-surface-bright flex justify-center"><span class="material-symbols-outlined text-sm text-primary">format_align_center</span></button>
        <button class="flex-1 py-2 rounded hover:bg-surface-bright flex justify-center"><span class="material-symbols-outlined text-sm">format_align_right</span></button>
      </div>
    </div>
  </div>
  <!-- Apply button -->
  <div class="p-5 border-t border-outline-variant/15 bg-surface-container">
    <button id="btn-apply-typography" class="w-full py-3 bg-gradient-to-br from-[#b6a0ff] to-[#7e51ff] rounded-full text-on-primary-fixed font-bold text-sm shadow-[0_0_20px_rgba(182,160,255,0.4)] hover:brightness-110 active:scale-95 transition-all">
      Apply Typography
    </button>
  </div>
</aside>
```

---

### Toast Notification (JS Function)

```js
function showToast(message, type = 'success') {
  const container = document.getElementById('toast-container');
  const isSuccess = type === 'success';
  const toast = document.createElement('div');
  toast.className = `glass-panel px-6 py-4 rounded-lg flex items-center space-x-4 border-l-4 
    ${isSuccess ? 'border-primary' : 'border-error'} shadow-2xl pointer-events-auto max-w-sm mb-3`;
  toast.innerHTML = `
    <div class="p-2 rounded-full ${isSuccess ? 'bg-primary/20' : 'bg-error/20'}">
      <span class="material-symbols-outlined ${isSuccess ? 'text-primary' : 'text-error'}" 
            style="font-variation-settings:'FILL' 1">${isSuccess ? 'check_circle' : 'error'}</span>
    </div>
    <div class="flex-1">
      <h4 class="font-headline text-white text-sm font-bold">${isSuccess ? 'สำเร็จ!' : 'เกิดข้อผิดพลาด'}</h4>
      <p class="text-on-surface-variant text-xs mt-0.5">${message}</p>
    </div>
    <span class="material-symbols-outlined text-on-surface-variant cursor-pointer text-lg hover:text-white" onclick="this.closest('div').remove()">close</span>
  `;
  container.appendChild(toast);
  setTimeout(() => toast.remove(), 4000);
}
```

Required HTML: `<div id="toast-container" class="fixed top-20 right-8 z-[100] flex flex-col pointer-events-none"></div>`

---

### SetBusy Pattern (JS)

```js
let isBusy = false;

function setBusy(busy) {
  isBusy = busy;
  const btn = document.getElementById('btn-generate');
  if (busy) {
    btn.disabled = true;
    btn.innerHTML = `
      <span class="material-symbols-outlined animate-spin-slow">sync</span>
      <span>Generating...</span>
    `;
    btn.classList.replace('gradient-primary', 'bg-neutral-800');
    btn.classList.add('cursor-not-allowed', 'opacity-80', 'text-neutral-500');
  } else {
    btn.disabled = false;
    btn.innerHTML = `
      <span class="material-symbols-outlined text-xl group-hover:rotate-12 transition-transform">bolt</span>
      GENERATE IMAGE
    `;
    btn.classList.replace('bg-neutral-800', 'gradient-primary');
    btn.classList.remove('cursor-not-allowed', 'opacity-80', 'text-neutral-500');
  }
}
```
