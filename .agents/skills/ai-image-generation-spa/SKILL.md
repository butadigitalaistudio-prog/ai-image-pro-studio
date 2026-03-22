---
name: ai-image-generation-spa
description: Use this skill when implementing any AI API call, generation flow, or SPA feature for AI Image Pro Studio. Covers Google Generative AI API integration, generation settings, image handling, Smart Prompt Assembly, JSZip download, and Canvas text rendering patterns.
---

# Skill: AI Image Generation SPA

Patterns สำหรับ API calls, generation flow, และฟีเจอร์ต่าง ๆ ของ AI Image Pro Studio

---

## API Configuration

```js
// ===== API Config =====
const API_KEY = 'YOUR_GEMINI_API_KEY';
const API_BASE = 'https://generativelanguage.googleapis.com/v1beta';

const MODELS = {
  text:    'gemini-2.5-flash-preview-04-17',        // Translation, Inspire Me, Image-to-Text
  flash:   'gemini-2.5-flash-preview-04-17',        // Fast gen, Magic Edit, Upscale  
  imagen:  'imagen-4.0-generate-001',                // High-quality Text-to-Image
};

const SAFETY_SETTINGS = [
  { category: 'HARM_CATEGORY_HARASSMENT',        threshold: 'BLOCK_ONLY_HIGH' },
  { category: 'HARM_CATEGORY_HATE_SPEECH',       threshold: 'BLOCK_ONLY_HIGH' },
  { category: 'HARM_CATEGORY_SEXUALLY_EXPLICIT', threshold: 'BLOCK_ONLY_HIGH' },
  { category: 'HARM_CATEGORY_DANGEROUS_CONTENT', threshold: 'BLOCK_ONLY_HIGH' },
];
```

---

## Smart Prompt Assembly

รวม Text Prompt + Art Style + Pose + Cinema Gear ก่อนส่งให้ AI

```js
function assemblePrompt() {
  const textPrompt     = document.getElementById('prompt-input').value.trim();
  const selectedStyles = getSelectedPresets('art-style');  // เช่น ['Cinematic', 'Cyberpunk']
  const selectedPoses  = getSelectedPresets('pose');        // เช่น ['Standing']
  const cameraBody     = document.getElementById('sel-camera').value;
  const lens           = document.getElementById('sel-lens').value;
  const angle          = document.getElementById('sel-angle').value;
  const lighting       = document.getElementById('sel-lighting').value;

  const parts = [textPrompt];
  if (selectedStyles.length) parts.push(`Art Style: ${selectedStyles.join(', ')}`);
  if (selectedPoses.length)  parts.push(`Pose: ${selectedPoses.join(', ')}`);
  if (cameraBody) parts.push(`Shot on ${cameraBody}`);
  if (lens)       parts.push(`Lens: ${lens}`);
  if (angle)      parts.push(`Camera Angle: ${angle}`);
  if (lighting)   parts.push(`Lighting: ${lighting}`);
  parts.push('high quality, detailed, professional photography');

  return parts.filter(Boolean).join(', ');
}
```

---

## Text-to-Image Generation (Imagen — Pro Quality)

```js
async function generateWithImagen(prompt, aspectRatio = '1:1', count = 4) {
  const aspectMap = {
    '1:1': '1:1', '16:9': '16:9', '9:16': '9:16',
    '3:2': '3:2', '2:3': '2:3', '21:9': '21:9'
  };
  const response = await fetch(
    `${API_BASE}/models/${MODELS.imagen}:predict?key=${API_KEY}`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        instances: [{ prompt }],
        parameters: {
          sampleCount: count,
          aspectRatio: aspectMap[aspectRatio] || '1:1',
        },
      }),
    }
  );
  if (!response.ok) throw new Error(`Imagen API error: ${response.status}`);
  const data = await response.json();
  // Returns array of base64 images
  return (data.predictions || []).map(p => `data:image/png;base64,${p.bytesBase64Encoded}`);
}
```

---

## Text-to-Image Generation (Gemini Flash — Fast)

```js
async function generateWithFlash(prompt, count = 4) {
  const results = [];
  for (let i = 0; i < count; i++) {
    const response = await fetch(
      `${API_BASE}/models/${MODELS.flash}:generateContent?key=${API_KEY}`,
      {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          contents: [{ parts: [{ text: prompt }] }],
          generationConfig: { responseModalities: ['IMAGE', 'TEXT'] },
          safetySettings: SAFETY_SETTINGS,
        }),
      }
    );
    if (!response.ok) throw new Error(`Flash API error: ${response.status}`);
    const data = await response.json();
    const imgPart = data.candidates?.[0]?.content?.parts?.find(p => p.inlineData);
    if (imgPart) {
      results.push(`data:image/png;base64,${imgPart.inlineData.data}`);
    }
  }
  return results;
}
```

---

## Thai → English Translation

```js
async function translateToEnglish(thaiText) {
  const response = await fetch(
    `${API_BASE}/models/${MODELS.text}:generateContent?key=${API_KEY}`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{
          parts: [{
            text: `Translate the following Thai text into a professional English image generation prompt for Stable Diffusion / Imagen AI. Output only the English prompt, nothing else.\n\nThai: ${thaiText}`
          }]
        }],
        safetySettings: SAFETY_SETTINGS,
      }),
    }
  );
  const data = await response.json();
  return data.candidates?.[0]?.content?.parts?.[0]?.text?.trim() || thaiText;
}
```

---

## Image-to-Text (ถอดรหัสภาพ → Thai prompt)

```js
async function imageToPrompt(base64ImageData, mimeType = 'image/jpeg') {
  const response = await fetch(
    `${API_BASE}/models/${MODELS.text}:generateContent?key=${API_KEY}`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{
          parts: [
            { text: 'อธิบายภาพนี้เป็นภาษาไทยในรูปแบบของ prompt สำหรับสร้างภาพด้วย AI อย่างละเอียด รวมถึงสไตล์ สี แสง องค์ประกอบ และบรรยากาศของภาพ' },
            { inlineData: { mimeType, data: base64ImageData } }
          ]
        }],
        safetySettings: SAFETY_SETTINGS,
      }),
    }
  );
  const data = await response.json();
  return data.candidates?.[0]?.content?.parts?.[0]?.text?.trim() || '';
}
```

---

## Inspire Me (สุ่ม Prompt)

```js
async function inspireMe() {
  const themes = ['cyberpunk', 'cinematic portrait', 'fantasy landscape', 'sci-fi', 'anime', 'noir', '3D render', 'surreal'];
  const theme = themes[Math.floor(Math.random() * themes.length)];
  const response = await fetch(
    `${API_BASE}/models/${MODELS.text}:generateContent?key=${API_KEY}`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{
          parts: [{
            text: `สร้าง prompt ภาษาไทยสำหรับสร้างภาพ AI ในสไตล์ "${theme}" ที่สวยงามและสร้างสรรค์ 1 ประโยค ไม่ต้องอธิบายเพิ่ม`
          }]
        }],
        safetySettings: SAFETY_SETTINGS,
      }),
    }
  );
  const data = await response.json();
  return data.candidates?.[0]?.content?.parts?.[0]?.text?.trim() || '';
}
```

---

## Magic Edit (Image-to-Image Inpainting)

```js
async function magicEdit(sourceImageBase64, editPrompt) {
  const translatedPrompt = await translateToEnglish(editPrompt);
  const response = await fetch(
    `${API_BASE}/models/${MODELS.flash}:generateContent?key=${API_KEY}`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{
          parts: [
            { text: `Edit this image: ${translatedPrompt}. Keep the overall composition and style but apply the requested changes.` },
            { inlineData: { mimeType: 'image/png', data: sourceImageBase64 } }
          ]
        }],
        generationConfig: { responseModalities: ['IMAGE', 'TEXT'] },
        safetySettings: SAFETY_SETTINGS,
      }),
    }
  );
  if (!response.ok) throw new Error(`Magic Edit error: ${response.status}`);
  const data = await response.json();
  const imgPart = data.candidates?.[0]?.content?.parts?.find(p => p.inlineData);
  if (!imgPart) throw new Error('No image returned from Magic Edit');
  return `data:image/png;base64,${imgPart.inlineData.data}`;
}
```

---

## Upscale 4K

```js
async function upscale4K(sourceImageBase64) {
  const response = await fetch(
    `${API_BASE}/models/${MODELS.flash}:generateContent?key=${API_KEY}`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        contents: [{
          parts: [
            { text: 'Upscale this image to 4K resolution. Enhance details, sharpness, and clarity while maintaining the original composition and style. Output a higher resolution, more detailed version.' },
            { inlineData: { mimeType: 'image/png', data: sourceImageBase64 } }
          ]
        }],
        generationConfig: { responseModalities: ['IMAGE', 'TEXT'] },
        safetySettings: SAFETY_SETTINGS,
      }),
    }
  );
  if (!response.ok) throw new Error(`Upscale error: ${response.status}`);
  const data = await response.json();
  const imgPart = data.candidates?.[0]?.content?.parts?.find(p => p.inlineData);
  if (!imgPart) throw new Error('No image returned from Upscale');
  return `data:image/png;base64,${imgPart.inlineData.data}`;
}
```

---

## Main Generate Flow

```js
async function handleGenerate() {
  if (isBusy) return;
  const rawPrompt = document.getElementById('prompt-input').value.trim();
  if (!rawPrompt) { showToast('กรุณาใส่ Prompt ก่อน', 'error'); return; }

  setBusy(true);
  showProgressOverlay(true);

  try {
    // 1. Assemble smart prompt
    const finalPrompt = assemblePrompt();

    // 2. Choose engine
    const engine = document.getElementById('sel-engine').value; // 'flash' or 'imagen'
    const aspectRatio = getSelectedAspectRatio(); // '1:1', '16:9', etc.
    const count = parseInt(document.getElementById('batch-count').value || '4');

    let images = [];
    if (engine === 'imagen') {
      images = await generateWithImagen(finalPrompt, aspectRatio, Math.min(count, 4));
    } else {
      images = await generateWithFlash(finalPrompt, count);
    }

    // 3. Render to gallery
    renderGallery(images, finalPrompt);
    showToast('สร้างภาพสำเร็จ!', 'success');

  } catch (err) {
    console.error(err);
    showToast(`เกิดข้อผิดพลาด: ${err.message}`, 'error');
  } finally {
    setBusy(false);
    showProgressOverlay(false);
  }
}
```

---

## Download All as ZIP

```js
async function downloadAllAsZip(images, prompt) {
  // Requires: <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
  const zip = new JSZip();
  const folder = zip.folder('ai-image-pro-studio');

  images.forEach((dataUrl, i) => {
    const base64 = dataUrl.split(',')[1];
    folder.file(`image_${String(i+1).padStart(2,'0')}.png`, base64, { base64: true });
  });

  // Include prompt as text file
  folder.file('prompt.txt', `Prompt Used:\n${prompt}\n\nGenerated by AI Image Pro Studio`);

  const blob = await zip.generateAsync({ type: 'blob' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `ai-images-${Date.now()}.zip`;
  a.click();
  URL.revokeObjectURL(url);
}
```

---

## Export with Text (Canvas Merge)

```js
async function exportWithText(imageDataUrl, textConfig) {
  // textConfig: { text, font, size, color, x, y, align, shadow, lineHeight }
  const img = new Image();
  img.src = imageDataUrl;
  await new Promise(resolve => img.onload = resolve);

  const canvas = document.createElement('canvas');
  canvas.width = img.naturalWidth;
  canvas.height = img.naturalHeight;
  const ctx = canvas.getContext('2d');

  // Draw base image
  ctx.drawImage(img, 0, 0);

  // Draw text
  ctx.font = `${textConfig.size}px "${textConfig.font}"`;
  ctx.fillStyle = textConfig.color || '#ffffff';
  ctx.textAlign = textConfig.align || 'center';

  if (textConfig.shadow) {
    ctx.shadowColor = 'rgba(0,0,0,0.8)';
    ctx.shadowBlur = 20;
  }

  const x = textConfig.x ?? canvas.width / 2;
  const y = textConfig.y ?? canvas.height / 2;

  // Multi-line support
  const lines = textConfig.text.split('\n');
  const lh = textConfig.lineHeight || textConfig.size * 1.4;
  lines.forEach((line, i) => {
    ctx.fillText(line, x, y + (i * lh));
  });

  // Download as PNG
  const url = canvas.toDataURL('image/png');
  const a = document.createElement('a');
  a.href = url;
  a.download = `ai-image-with-text-${Date.now()}.png`;
  a.click();
}
```

---

## Base64 Utilities

```js
// File → base64
function fileToBase64(file) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = () => resolve(reader.result.split(',')[1]);
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
}

// dataURL → base64 (strip prefix)
function dataUrlToBase64(dataUrl) {
  return dataUrl.split(',')[1];
}
```

---

## Gallery State Management

```js
// Global state
const state = {
  images: [],        // Array of { dataUrl, prompt, isUpscaled }
  referenceImage: null,   // base64 for Image-to-Image
  faceImage: null,        // base64 for Face Match
  selectedAspect: '1:1',
  selectedStyles: [],
  selectedPoses: [],
};

function renderGallery(newImages, prompt) {
  // Append to state.images
  newImages.forEach(dataUrl => {
    state.images.unshift({ dataUrl, prompt, isUpscaled: false });
  });

  const gallery = document.getElementById('gallery');
  gallery.innerHTML = '';

  // Asymmetric masonry pattern
  const patterns = [
    { cols: 'col-span-8', rows: 'row-span-2' },  // Featured
    { cols: 'col-span-4', rows: 'row-span-1' },
    { cols: 'col-span-4', rows: 'row-span-2' },
    { cols: 'col-span-8', rows: 'row-span-1' },
  ];

  state.images.forEach((img, i) => {
    const pattern = patterns[i % patterns.length];
    const div = document.createElement('div');
    div.className = `${pattern.cols} ${pattern.rows} relative group overflow-hidden rounded-xl bg-surface-container cursor-pointer`;
    div.innerHTML = `
      <img class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105" src="${img.dataUrl}" alt="AI Generated"/>
      <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity p-6 flex flex-col justify-end">
        ${img.isUpscaled ? '<span class="px-2 py-1 rounded bg-tertiary/20 text-tertiary text-[10px] font-bold uppercase mb-2 w-fit">4K Upscaled</span>' : ''}
        <p class="text-white text-sm font-medium line-clamp-2">${img.prompt}</p>
      </div>
      <div class="absolute inset-0 border-2 border-primary opacity-0 group-hover:opacity-100 transition-opacity rounded-xl pointer-events-none"></div>
    `;
    div.addEventListener('click', () => openPostProcessing(i));
    gallery.appendChild(div);
  });
}
```

---

## Global Reset

```js
function resetWorkspace() {
  // Show confirmation modal first (see project-rules.md for modal HTML pattern)
  document.getElementById('modal-reset').classList.remove('hidden');
}

function confirmReset() {
  // Clear state
  state.images = [];
  state.referenceImage = null;
  state.faceImage = null;
  state.selectedStyles = [];
  state.selectedPoses = [];

  // Clear UI
  document.getElementById('prompt-input').value = '';
  document.getElementById('gallery').innerHTML = '';
  document.getElementById('modal-reset').classList.add('hidden');

  showToast('รีเซ็ต Workspace เรียบร้อย', 'success');
}
```
