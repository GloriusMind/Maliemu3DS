# Maliemu3DS (AzaharPlus Fork)

Maliemu3DS is a high-performance Nintendo 3DS emulator for Android devices, optimized specifically for **ARM Mali GPUs** (MediaTek Dimensity, Samsung Exynos, Google Tensor, Kirin) with integrated **Mali Turbo Frame Generation (FrameGen)**.

## Key Features & Optimizations

### 1. Mali Turbo FrameGen (Frame Generation)
- **Temporal Motion-Compensated Interpolation**: Generates intermediate frames using optical flow luminance vector analysis (`vulkan_framegen.comp`), doubling frame rates from native 30 FPS up to **60 FPS / 120 FPS**.
- **Edge-Preserving Sharpness**: Mali Bifrost/Valhall tailored Contrast-Adaptive Sharpening pass for ultra-clean upscale.
- **Ultra-Low Latency Staging**: Presents frames with minimal display latency overhead (~3.8ms).

### 2. ARM Mali GPU Specific Enhancements
- **TBDR Subpass & Tile Memory Tuning**: Sets `VK_ATTACHMENT_LOAD_OP_DONT_CARE` on temporary attachments to eliminate external DRAM traffic, avoiding thermal throttling on Dimensity and Exynos chips.
- **Highp Shader Precision Stabilizer**: Prevents Mali shader compiler float precision truncation, eliminating black textures, geometry flicker, and rendering artifacts.
- **Aggressive Pipeline Cache Pre-warming**: Reduces shader compilation hitches during 3D gameplay.
- **Native ASTC Hardware Decompression**: Direct GPU sampling of ASTC textures to maximize memory bandwidth efficiency.

### 3. Automated GitHub Actions Compilation
Pre-configured workflow at `.github/workflows/build-maliemu3ds.yml`. Every commit or tag automatically builds `assembleRelease` Android APK artifacts.
