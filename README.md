This is  a modular AI content pipeline:

LLM → Brain 🧠
ComfyUI → Eyes 👁
TTS → Voice 🎙
FFmpeg → Editor 🎬
         
         
         ┌───────────────┐
         │  script.txt   │
         └──────┬────────┘
                │
        ┌───────▼────────┐
        │   ComfyUI      │
        │ workflow.json  │
        └───────┬────────┘
                │
           bg.png
                │
        ┌───────▼────────┐
        │   edge_tts     │
        └───────┬────────┘
                │
           voice.mp3
                │
        ┌───────▼────────┐
        │    FFmpeg      │
        └───────┬────────┘
                │
        🎬 final_video.mp4


        script.txt        ← INPUT
workflow.json     ← INPUT

↓ (ComfyUI)
bg.png            ← GENERATED

↓ (TTS)
voice.mp3         ← GENERATED

↓ (FFmpeg)
final_video.mp4   ← OUTPUT 🎬







Create a YouTube Short from a poem → fully automated

🔷 1. HIGH-LEVEL FLOW
[USER INPUT / script.txt]
        ↓
[LLM - Ollama]
        ↓
(script generated)
        ↓
[ComfyUI]
        ↓
(background image)
        ↓
[Edge TTS]
        ↓
(audio narration)
        ↓
[FFmpeg]
        ↓
(final_video.mp4)
🔷 2. COMPONENT BREAKDOWN
🟣 A. SCRIPT GENERATION (Optional stage)

File:

generator.py

Uses:

Ollama (LLaMA)

Output:

script.txt
title.txt
hashtags.txt
🔵 B. IMAGE GENERATION

File:

one_click_short.py → generate_image()

Uses:

ComfyUI API (http://127.0.0.1:8188)
workflow.json

Flow:

script.txt
   ↓
inject into workflow.json
   ↓
POST → ComfyUI
   ↓
ComfyUI runs diffusion
   ↓
image saved → bg.png
🟢 C. AUDIO GENERATION

File:

generate_audio()

Uses:

edge_tts

Flow:

script.txt
   ↓
text-to-speech
   ↓
voice.mp3
🟡 D. VIDEO GENERATION

File:

create_video()

Uses:

FFmpeg

Flow:

bg.png + voice.mp3 + script text
   ↓
drawtext overlay
   ↓
final_video.mp4
🔷 3. FILE FLOW (VERY IMPORTANT)
script.txt        ← INPUT
workflow.json     ← INPUT

↓ (ComfyUI)
bg.png            ← GENERATED

↓ (TTS)
voice.mp3         ← GENERATED

↓ (FFmpeg)
final_video.mp4   ← OUTPUT 🎬
🔷 4. ONE-CLICK PIPELINE FLOW

Your final file (one_click_short.py) does:

1. load_script()
2. generate_image()
3. generate_audio()
4. create_video()
🔷 5. SYSTEM DEPENDENCIES

You must have these running:

✅ Required services
ComfyUI running:
python main.py
✅ Installed libraries
pip install requests edge-tts
✅ Installed tools
FFmpeg (very important)

Check:

ffmpeg -version








