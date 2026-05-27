# Easy Onboarding Setup Guide

This document provides comprehensive instructions for setting up the Easy Onboarding system locally.

---

## Prerequisites

- **bitbucket** (for cloning repositories)
- **Conda** (for managing Python environments)
- **Node.js** (for frontend development)
- **ngrok** (for public URL exposure)

---

## Step 1: Clone the Repositories

Clone the backend and frontend code from Bitbucket:

**Backend:**
```
https://bitbucket.org/cashlink_rnd/ocr-backend-new/src/main/
```

**Frontend:**
```
https://bitbucket.org/cashlink_rnd/ocr-frontend/src/main/
```

---

## Step 2: Switch to Development Branches

After cloning, switch to the appropriate development branches:

- **Backend Branch:** `ocr-new-v2`
- **Frontend Branch:** `ocr-frontend-v2`

---

## Step 3: Create Python Virtual Environments

Create **two separate** Python environments to avoid package conflicts:

### OCR Environment
```bash
conda create -n myenv python=3.11
conda activate myenv
```

### Face Detection Environment
```bash
conda create -n face-env python=3.11
conda activate face-env
```

> **Note:** Two environments are required because of package conflicts between OCR and Face detection dependencies.

---

## Step 4: Install Dependencies

### For OCR Environment:
```bash
conda activate myenv
pip install pip-tools
pip-compile .\requirements\requirements.in
python -m pip install -r .\requirements\requirements.txt
```

### For Face Environment:
```bash
conda activate face-env
pip install pip-tools
pip-compile .\requirements\requirements-face.in
python -m pip install -r .\requirements\requirements-face.txt
```

### Install Tesseract OCR

1. Download Tesseract from: https://tesseractocr.org/
2. Install it (default path: `C:\Program Files\Tesseract-OCR`)
3. Add to your `.env` file in the backend directory:
```
TESSERACT_CMD=C:\Program Files\Tesseract-OCR\tesseract.exe
```

---

## Step 5: Run the Backend

Start both backend services on their designated ports:

```bash
# For OCR service (port 8001)
uvicorn main:app --reload --port 8001

# For Face service (port 8002) - in a new terminal with face-env activated
uvicorn face_main:app --reload --port 8002
```

---

## Step 6: Setup Frontend

### Install Node.js

1. Download Node.js from: https://nodejs.org/en/download
2. Install it and add to environment variables
   - Reference: [Node.js Setup Tutorial](https://www.youtube.com/watch?v=DdMIKKBVv5M)

### Install Dependencies

```bash
cd your-project-folder
npm install
```

### Setup ngrok for Public URL

1. Download ngrok from: https://ngrok.com/download/windows
2. Extract and move `ngrok.exe` to `C:\ngrok`
3. Create an ngrok account: https://dashboard.ngrok.com/get-started/setup/windows
4. Authenticate and get your token:
   ```bash
   ngrok config add-authtoken YOUR_TOKEN
   ```
5. Aftert this we need to give this and onw public url will be diplay that we need to enter into the env. file 
    ```bash
    PUBLIC_API_BASE_URL_LOCAL
    ```

---

## Step 7: Configure Environment Variables

Update your backend `.env` file with the following paths and URLs:

```env
# Public API URL (update after ngrok authentication)
PUBLIC_API_BASE_URL_LOCAL=http://localhost:8001

# File Storage Paths (adjust based on your project location)
VAULT_PATH=D:\Dwarakesh\Dwarakesh\Project\starnexAI\customer onboard\datastoring\vault
MASKED_PATH=D:\Dwarakesh\Dwarakesh\Project\starnexAI\customer onboard\datastoring\masked

# Tesseract OCR
TESSERACT_CMD=C:\Program Files\Tesseract-OCR\tesseract.exe
```

---

## Step 8: Run the Frontend

Navigate to the frontend directory and start the development server:

```bash
cd ocr-frontend
ng serve -o
```

Or 
```bash
ng serve
```

The application will be available at: `http://localhost/login`

---

## Video Tutorials

Refer to these video tutorials for additional guidance:

- **Node.js Setup:** https://www.youtube.com/watch?v=DdMIKKBVv5M
- **ngrok Setup:** https://www.youtube.com/watch?v=ZKnpP7QGjX8 (Watch up to 2:35)

---

## Video Guide

**Easy Onboarding Product Usage Tutorial:**

refer this link : https://drive.google.com/file/d/1mFzoM0Kyko7FTQ5xbzw_AYn8UulwNXil/view?usp=sharing

For detailed usage instructions of the Easy Onboarding product, please watch the tutorial video link above. 
	
	


	




	

