# 🗜️ Advanced File Compressor & Decompressor

A full-featured **Java Swing desktop application** for lossless file compression, decompression, comparison, and history tracking — built entirely with the standard JDK, zero external dependencies.

---

## 📝 Description

Advanced File Compressor & Decompressor is a feature-rich desktop application built with Java Swing that lets users compress and decompress files using four different lossless algorithms — Huffman Coding, GZIP, ZIP, and LZW — all through a clean, modern graphical interface without needing any external libraries beyond the standard JDK.

The application opens with a dashboard of navigation cards, each leading to a dedicated section. The **Compress** panel allows users to browse or drag and drop any file, preview its contents (text files show the first 500 lines, images render a scaled thumbnail), choose a compression algorithm and level via a slider, set an output folder and filename, then compress with a single click. A live progress bar tracks the operation, which runs on a background thread to keep the UI fully responsive.

After compression, a results panel displays the original size, compressed size, space saved, compression ratio, time taken, and processing speed — alongside a custom-drawn bar chart and pie chart rendered using Java **Graphics2D**, with no third-party chart library.

The **Decompress** panel auto-detects the algorithm from the file extension, restores the original file, and performs a **SHA-256 integrity check** by comparing the decompressed file's hash against the hash stored from the original compression session.

The **Compare** panel lets users select any two files and runs a byte-level diff — reporting file sizes, SHA-256 and MD5 hashes, whether the files are identical, and the exact byte offsets where differences occur.

All compression activity is automatically saved to a **persistent history log**. The History panel provides a searchable, sortable table with options to delete entries, export to CSV, or clear all records. The **Settings** panel offers light/dark theme switching, a default compression level, and a default output folder.

---

## 🚀 Features

### 🗜️ Compression
- Browse or **drag & drop** any file
- **Text preview** — first 500 lines for code/text files
- **Image preview** — scaled thumbnail for JPG/PNG/GIF/BMP
- **4 algorithms:** Huffman Coding, GZIP, ZIP, LZW
- **Compression level slider** (1–9) for ZIP and GZIP
- Custom output folder and filename
- Live **progress bar** (background thread — UI never freezes)
- Full **result panel**: size, ratio, time, speed, charts

### 📂 Decompression
- Auto-detects algorithm from `.huff`, `.lzw`, `.gz`, `.zip`
- Live progress bar
- **SHA-256 integrity check** against original hash from history

### 🔍 File Comparison
- Compare **any two files** byte by byte
- Reports: file sizes, SHA-256 hash, MD5 hash
- Shows exact **byte offsets** where differences occur

### 📋 Compression History
- Auto-saved to `~/.afc_history.csv` (persists across restarts)
- Sortable **JTable** — click any column to sort
- **Search** by filename or algorithm
- Export history to CSV, delete entries, clear all

### ⚙️ Settings
- **Light / Dark theme** toggle (header button or Settings panel)
- Default compression level (pre-fills Compress slider)
- Default output folder (pre-fills both panels)

### 📊 Custom Charts (no library)
- **Bar chart**: Original vs Compressed size (Graphics2D)
- **Pie chart**: Compressed portion vs Space saved

---

## 🛠️ Tech Stack

| | |
|---|---|
| Language | Java 11+ |
| UI Framework | Java Swing (JDK built-in) |
| Build Tool | Apache Maven |
| Compression | Huffman (custom), LZW (custom), GZIP, ZIP (JDK) |
| Hashing | SHA-256, MD5 via `java.security.MessageDigest` |
| Threading | `SwingWorker` for all background I/O |
| Charts | Custom `Graphics2D` painting |
| History | Local CSV (`~/.afc_history.csv`) |
| File I/O | `BufferedInputStream/OutputStream` (64KB buffers) |
| Drag & Drop | `TransferHandler` + `DataFlavor.javaFileListFlavor` |

---

## 📁 Project Structure

```
AdvancedFileCompressor/
├── src/
│   └── main/
│       └── java/
│           └── com/mycompany/advancedfilecompressor/
│               └── AdvancedFileCompressor.java
├── pom.xml
├── .gitignore
├── README.md
├── PROJECT_OVERVIEW.txt
├── PROJECT_ARCHITECTURE.txt
├── FEATURES.txt
├── SOURCE_CODE_EXPLANATION.txt
└── IMPLEMENTATION_STEPS.txt
```

---

## ⚙️ Prerequisites

- Java JDK 11+
- Apache Maven 3.6+

---

## 🏃 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-username/AdvancedFileCompressor.git
cd AdvancedFileCompressor

# Build the project
mvn clean package

# Run the JAR
java -jar target/AdvancedFileCompressor.jar

# OR run via Maven
mvn exec:java
```

---

## 📂 Supported File Formats

| Extension | Algorithm | Direction |
|---|---|---|
| `.huff` | Huffman Coding (custom) | Compress + Decompress |
| `.gz` | GZIP / DEFLATE (JDK) | Compress + Decompress |
| `.zip` | ZIP / DEFLATE (JDK) | Compress + Decompress |
| `.lzw` | LZW (custom) | Compress + Decompress |

---

## 🎨 UI Overview

| Panel | Description |
|---|---|
| Dashboard | 7 color-coded navigation cards |
| Compress | File info + preview + options + result + charts |
| Decompress | Auto-detect + integrity check |
| Compare | Byte-level diff + hash report |
| History | Searchable, sortable, exportable table |
| Settings | Theme + default level + default folder |
| Help | HTML user guide + algorithm explanations |

---

## 🔐 SHA-256 Integrity Verification

When you compress a file, its **SHA-256 hash is stored** in history. When you later decompress it, the app recomputes the hash and compares:

| Result | Meaning |
|---|---|
| ✅ Green — Integrity Verified | Hashes match — file is intact |
| ❌ Red — Corrupted File | Hash mismatch — file may be damaged |
| ⚠️ Orange — No record | No history found to compare against |

---

## 🧠 Algorithm Internals

**Huffman Coding** — Builds a binary prefix-code tree from byte frequencies. More frequent bytes get shorter codes, less frequent ones get longer codes. Stores the frequency table in the output file header for lossless reconstruction.

**GZIP** — Wraps Java's `GZIPOutputStream` which uses the DEFLATE algorithm (LZ77 + Huffman coding). Compression level 1–9 exposed via a custom `LeveledGZIPOutputStream` subclass.

**ZIP** — Single-entry ZIP archive using `ZipOutputStream`. Preserves the original filename in the entry metadata. Supports compression levels 1–9.

**LZW** — Dictionary-based compression. Builds a string-to-code table during compression, grows to 65,535 entries, then auto-resets. Uses 16-bit code output via a custom `BitOutputStream`.

---

## 📌 Known Limitations / TODOs

- [ ] Batch compression (multiple files in one ZIP)
- [ ] Password-protected ZIP encryption
- [ ] Drag & drop on Decompress panel
- [ ] Chart export as PNG
- [ ] GitHub Actions CI pipeline
- [ ] Dark mode polish for JTable headers

---

## 👨‍💻 Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)

---

## 📄 License

This project is licensed under the MIT License. See `LICENSE` for details.
