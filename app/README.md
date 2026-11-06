# Manga Cleaner — Xóa chữ manga miễn phí, chạy 100% trong trình duyệt

Web tĩnh (HTML/CSS/JS thuần): chọn nhiều ảnh hoặc cả thư mục, AI phát hiện chữ manga
và tự xóa bằng inpainting, rồi đóng gói kết quả thành file ZIP để tải về.

- **Miễn phí hoàn toàn, không cần API key** — model AI chạy local bằng ONNX Runtime (WASM).
- **Ảnh không bao giờ rời khỏi thiết bị** — không có server, không upload.
- Chạy được trên **PC và Android** (trình duyệt Chrome khuyên dùng).

## Cách dùng
1. Mở `index.html` qua một web server tĩnh (hoặc deploy lên GitHub Pages — xem dưới).
2. Đợi trang tải model AI (~95MB, chỉ tải 1 lần, sau đó dùng cache của trình duyệt).
3. **Chọn ảnh** (điện thoại: nhấn giữ để chọn nhiều ảnh cùng lúc) hoặc **Chọn cả thư mục**.
4. Bấm **Bắt đầu xóa chữ**. Xong thì bấm **Tải về file ZIP**.
5. Nhấn vào từng ảnh trong danh sách để tải riêng từng ảnh.

> **Lưu ý tốc độ:** model chạy bằng CPU qua WASM nên tốc độ phụ thuộc vào máy —
> một trang ~1024×1536 mất khoảng 1–3 phút trên máy yếu, nhanh hơn đáng kể trên
> máy/điện thoại mới. Model chỉ tải 1 lần (~95MB), các lần sau dùng cache.

## Deploy lên GitHub Pages
```bash
git init
git add .
git commit -m "Manga Cleaner"
git branch -M main
git remote add origin https://github.com/<ten-ban>/manga-cleaner.git
git push -u origin main
```
Sau đó: repo **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
Vài phút sau web chạy tại `https://<ten-ban>.github.io/manga-cleaner/`.

> File model `assets/models/comic-text-detector.onnx` (~95MB) nhỏ hơn giới hạn 100MB/file
> của GitHub nên có thể đẩy trực tiếp. Nếu muốn nhẹ hơn, dùng Git LFS cho file này.

## Chạy local
```bash
python3 -m http.server 8000
# mở http://localhost:8000
```

## Thành phần & license
| Thành phần | Nguồn | License |
|---|---|---|
| Model phát hiện chữ `comic-text-detector.onnx` | github.com/dmMaze/comic-text-detector (ONNX: huggingface.co/mayocream/comic-text-detector-onnx) | Apache-2.0 |
| ONNX Runtime Web | npm `onnxruntime-web@1.18.0` | MIT |
| OpenCV.js | npm `@techstark/opencv-js@5.0.0-release.1` | Apache-2.0 |
| JSZip | npm `jszip@3.10.2` | MIT hoặc GPLv3 |
