# Run LLMs Locally Using `llama.cpp` (Windows | Linux | macOS)

This guide shows how to run **Large Language Models (LLMs)** locally on your laptop using **`llama.cpp` + GGUF models**.

>  No GPU required (CPU-only).
>  Works offline.
>  Fully private.

---

##  What This Covers

* Install `llama.cpp`
* Download a GGUF model
* Run and chat locally
* Run a local server (browser + API)
* **Windows-specific troubleshooting (real-world issues & fixes)**

---

##  Supported OS

*  Windows (Native + WSL)
*  Linux (Ubuntu/Debian)
*  macOS (Intel + Apple Silicon)

---

##  Recommended Model (Laptop Friendly)

**Qwen2.5-7B-Instruct (Q4_K_M)**

* ~4–5 GB
* Good reasoning
* Fast on CPU
* Stable for beginners

---

##  1. Install `llama.cpp`

###  Build

**Linux / macOS**

**Windows (PowerShell + CMake + VS Build Tools)**

```
https://github.com/ggml-org/llama.cpp/blob/master/docs/install.md
```

##  2. Create Model Directory

**macOS / Linux**

```bash
mkdir ~/llm-models && cd ~/llm-models
```

**Windows (PowerShell)**

```powershell
mkdir C:\llm-models
cd C:\llm-models
```

---

##  3. Install Python + Hugging Face CLI

### macOS

```bash
brew install python
pip install huggingface_hub
```

### Linux (Ubuntu)

```bash
sudo apt update
sudo apt install python3-pip -y
pip install huggingface_hub
```

###  Windows (Important – Real Setup Issues & Fixes)

> This is where most people get stuck 

#### Step 1: Install Python

Download and install from:
 [https://www.python.org](https://www.python.org/)

 **IMPORTANT:** During installation, check:

```
Add Python to PATH in ``sysdm.cpl``
```

---

#### Step 2: If `python` or `pip` not working in PowerShell

If you see:

```
'python' is not recognized
```

 Fix by adding Python manually to Environment Variables:

* Search: **Environment Variables**
* Edit **Path**
* Add:

```
C:\Users\<your-user>\AppData\Local\Programs\Python\Python3x\
C:\Users\<your-user>\AppData\Local\Programs\Python\Python3x\Scripts\
```

Restart PowerShell.

Verify:

```powershell
python --version
pip --version
```

---

#### Step 3: Install Hugging Face CLI

```powershell
pip install huggingface_hub
```

Verify:

```powershell
hf --help
```

---

## 4. Download Model

```bash
hf download bartowski/Qwen2.5-7B-Instruct-GGUF \
--include "Qwen2.5-7B-Instruct-Q4_K_M.gguf" \
--local-dir <path where you want to installl>
```

Verify:

```bash
ls -lh
```

Expected file:

```
Qwen2.5-7B-Instruct-Q4_K_M.gguf (~4–5GB)
```

---

## 5. Run the Model

### macOS

```bash
./llama-cli -m ~/llm-models/Qwen2.5-7B-Instruct-Q4_K_M.gguf
```

### Linux

```bash
./llama-cli -m ~/llm-models/Qwen2.5-7B-Instruct-Q4_K_M.gguf
```

### Windows (Native)

```powershell
llama-cli.exe -m C:\llm-models\Qwen2.5-7B-Instruct-Q4_K_M.gguf
```

### Windows (WSL – Recommended)

```bash
./llama-cli -m ~/llm-models/Qwen2.5-7B-Instruct-Q4_K_M.gguf
```

---

## 6. Chat with the Model

After loading:

```
>
```

Example:

```
Explain Kubernetes in simple terms
```

Exit:

```
Ctrl + C
```

---

##  7. Improve Performance (Threads)

Check CPU cores:

**macOS**

```bash
sysctl -n hw.ncpu
```

**Linux**

```bash
nproc
```

**Windows**

```powershell
echo %NUMBER_OF_PROCESSORS%
```

Run with threads:

```bash
./llama-cli -m model.gguf -t 8
```

---

##  8. Run as Local Server

### macOS

```bash
./llama-server -m ~/llm-models/model.gguf
```

### Linux

```bash
./llama-server -m ~/llm-models/model.gguf
```

### Windows

```powershell
llama-server.exe -m C:\llm-models\model.gguf
```

---

##  9. Open Web UI

Open:

```
http://localhost:8080
```

You’ll get a browser-based chat interface.

---

##  10. API Usage

```bash
curl http://localhost:8080/completion \
-d '{
  "prompt": "Explain Docker",
  "n_predict": 200
}'
```

---

##  Real Use Cases

*  Local chatbot
*  AI agents (LangChain / CrewAI)
*  DevOps automation
*  Code generation
*  RAG pipelines

---

##  Limitations

* Slower than GPU
* RAM heavy for large models
* Limited context vs cloud LLMs

---
##  Windows Troubleshooting (Real Issues Faced)

###  Issue 1: Python not recognized
Fix: Added Python to PATH

###  Issue 2: pip not working in PowerShell
Fix: Restart terminal after environment setup

###  Issue 3: hf command not found
Fix: Ensure Scripts folder is in PATH

##  Key Learnings

* LLMs can run locally using quantized GGUF models
* `llama.cpp` enables cross-platform inference
* CPU-based AI is practical for real workflows
* Windows setup needs extra environment configuration

---

##  Author

**Aman Shrivastav**

Cloud & DevOps Engineer | AWS | Azure | Linux | AI Enthusiast

---

##  Support

If this helped you:

* ⭐ Star the repo
*  Fork it
*  Share with others

---

**Keep Learning**
