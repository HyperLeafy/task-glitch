# Task Manager – Bug Fix Submission

### **Live Demo**  
👉 https://<your-app>.vercel.app

### **Repository**  
👉 https://github.com/<your-username>/<repo-name>

---

## Overview

This project is a bug-fix submission for the Task Manager application.  
The goal was to identify and resolve injected issues across state management, UI behavior, validation, and data export.  
All fixes have been implemented cleanly with a stable UI, predictable state, and safe data handling.

---

## Fixed Bugs

### **1️⃣ Undo Snackbar Not Closing / State Not Resetting**
- Added `clearLastDeleted()` inside the tasks context.
- Reset `lastDeleted` when Snackbar closes.
- Prevented stale undo behavior or restoring older deleted tasks.

---

### **2️⃣ Delete & Undo Causing Inconsistent State**
- Tasks now cleanly move to `lastDeleted`.
- Undo restores only the most recent deleted task.
- Guards added to avoid double-delete or stale undos.

---

### **3️⃣ Double Dialog Opening (View + Edit + Delete)**
- Added `event.stopPropagation()` to Edit/Delete buttons.
- Clicking a table row opens only the View dialog.
- Action buttons no longer trigger the row click handler.

---

### **4️⃣ ROI / Advanced Metrics Incorrect or Crashing**
- ROI now validated safely:
  - `timeTaken <= 0` → ROI = 0
  - Non-finite values → ROI = 0
- Proper decimal formatting (2 decimals).
- Average ROI now ignores invalid values.
- No more `Infinity`, `NaN`, or crashed UI.

---

### **5️⃣ CSV Export Broken (Corrupted Columns & Quotes)**
- Replaced unstable dynamic headers with fixed, predictable headers.
- Implemented robust CSV escaping for:
  - commas
  - quotes
  - newlines
- CSV now opens correctly in Excel/Google Sheets without corruption.

---

### **6️⃣ Duplicate Tasks on Fast Remount**
- Removed the second opportunistic fetch from `useEffect`.
- Prevented race conditions.
- Task list remains stable and predictable.

---

### **7️⃣ XSS Vulnerability in Notes Field**
- Removed `dangerouslySetInnerHTML`.
- Rendered notes as plain text only.
- Prevents injected HTML or scripts from executing.

---

## Tech Stack
- React + TypeScript  
- Material UI  
- Context API  
- Vercel for deployment  

---

## How to Run Locally

```sh
npm install
npm run dev
