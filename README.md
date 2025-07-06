# DocuCraft
This is a react app that let users create documentation and tutorials

# 🛠️ DocuCraft App – Technical Blueprint

## 📌 Project Overview

A web application that allows authenticated users to create, edit, manage, and export rich-text work guides. The app features a Microsoft Word-like editor, guide management dashboard, and PDF export functionality.

This version leverages Backend-as-a-Service (BaaS) platforms to reduce infrastructure overhead and accelerate development.

---

## 🧱 Architecture Overview

### 🖼️ High-Level System Architecture (BaaS-First)

```plaintext
+------------------+       +--------------------------+
|   Frontend (SPA) | <---> |  BaaS Platform (API + DB)|
|  (React + Editor)|       | (Firebase / Appwrite)    |
+------------------+       +--------------------------+
         |                          |
         |                          v
         |                  +------------------+
         |                  |  Auth Provider   |
         |                  | (Firebase/Auth0) |
         |                  +------------------+
         |
         v
+------------------+
|  PDF Export Tool |
| (jsPDF / html2pdf)|
+------------------+


---

## ⚙️ Tech Stack
```
<table class="t-table" style="border-spacing: 0px;"><thead><tr><th style="opacity: 1;">Layer</th><th style="opacity: 1;">Technology</th><th style="opacity: 1;">Description</th></tr></thead><tbody><tr><td style="opacity: 1;"><strong>Frontend</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://reactjs.org/" initial="start" animate="end" variants="[object Object]" custom="0">React</button></td><td style="opacity: 1;">SPA framework for UI</td></tr><tr><td style="opacity: 1;"><strong>Editor</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://tiptap.dev/" initial="start" animate="end" variants="[object Object]" custom="0">TipTap</button></td><td style="opacity: 1;">Rich text editor (ProseMirror-based)</td></tr><tr><td style="opacity: 1;"><strong>Styling</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://tailwindcss.com/" initial="start" animate="end" variants="[object Object]" custom="0">TailwindCSS</button></td><td style="opacity: 1;">Utility-first CSS framework</td></tr><tr><td style="opacity: 1;"><strong>Auth</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://appwrite.io/docs/authentication" initial="start" animate="end" variants="[object Object]" custom="0">Appwrite Auth</button></td><td style="opacity: 1;">Built-in email/password and OAuth login</td></tr><tr><td style="opacity: 1;"><strong>Database</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://appwrite.io/docs/databases" initial="start" animate="end" variants="[object Object]" custom="0">Appwrite Database</button></td><td style="opacity: 1;">Stores guide metadata and TipTap JSON</td></tr><tr><td style="opacity: 1;"><strong>Storage</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://appwrite.io/docs/storage" initial="start" animate="end" variants="[object Object]" custom="0">Appwrite Storage</button></td><td style="opacity: 1;">Optional: for image uploads in guides</td></tr><tr><td style="opacity: 1;"><strong>PDF Export</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://github.com/eKoopmans/html2pdf" initial="start" animate="end" variants="[object Object]" custom="0">html2pdf.js</button> or <button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://github.com/parallax/jsPDF" initial="start" animate="end" variants="[object Object]" custom="0">jsPDF</button></td><td style="opacity: 1;">Client-side PDF generation</td></tr><tr><td style="opacity: 1;"><strong>Hosting</strong></td><td style="opacity: 1;"><button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://vercel.com/" initial="start" animate="end" variants="[object Object]" custom="0">Vercel</button> or <button type="button" class="font-bold text-salmon-550 dark:text-midnight-400 hover:underline text-start align-top" data-url="https://www.netlify.com/" initial="start" animate="end" variants="[object Object]" custom="0">Netlify</button></td><td style="opacity: 1;">Deploy frontend</td></tr><tr><td style="opacity: 1;"><strong>CI/CD</strong></td><td style="opacity: 1;">GitHub Actions / Vercel Pipelines</td><td style="opacity: 1;">Continuous deployment and testing</td></tr></tbody></table>
```
---

## 🧩 Feature Breakdown

### 1. Authentication
- Sign up / Login / Logout
- JWT-based session management
- Role-based access (optional)

### 2. Guide Editor
- Rich text formatting (bold, italic, underline, headings)
- Lists, tables, code blocks
- Image embedding (optional)
- Auto-save drafts

### 3. Guide Management
- Dashboard with list of user’s guides
- Create / Edit / Delete guides
- Tagging and search (optional)

### 4. Export Functionality
- Export to PDF (with styles preserved)
- Optional: Export to Markdown or HTML

---

## 🗃️ Database Schema (Simplified)
id (UUID) email password_hash created_at

Guide
id (UUID) user_id (FK) title content (JSON or HTML) created_at updated_at


---

## 🧠 Component Architecture (Frontend)
```plaintext
App
├── AuthProvider
│   └── Handles user session and context
│
├── Router
│   ├── /login           → <LoginPage />
│   ├── /register        → <RegisterPage />
│   ├── /dashboard       → <DashboardPage />
│   ├── /editor/:id      → <EditorPage />
│   └── /new             → <NewGuidePage />
│
├── components/
│   ├── <Navbar />             → Top navigation bar
│   ├── <GuideCard />          → Displays a guide preview in dashboard
│   ├── <RichTextEditor />     → TipTap editor instance
│   ├── <ExportButton />       → Triggers PDF export
│   ├── <GuideList />          → Lists all user guides
│   └── <LoadingSpinner />     → Reusable loading indicator
│
└── utils/
    ├── appwriteClient.js      → Appwrite SDK config
    ├── authHelpers.js         → Login, logout, session helpers
    └── pdfExport.js           → PDF export logic (html2pdf/jsPDF)
---

## 📤 PDF Export Strategy

Client-side (jsPDF + html2canvas)
- Easy to implement
- Good for small to medium documents
- Embed directly in frontend
---

## 🧪 Testing Strategy

| Layer     | Tooling                  |
|-----------|--------------------------|
| Unit      | Jest + React Testing Lib |
| Integration | Cypress / Playwright     |

---

## 🚀 Deployment

- **Frontend**: Vercel
- **CI/CD**: GitHub Actions or Vercel’s built-in pipeline

---

## 📈 Future Enhancements

- Version history for guides
- Real-time collaboration (WebSockets)
- AI-assisted writing (OpenAI API)
- Export to DOCX or Markdown

---

## 🧭 Milestones

1. ✅ Set up project scaffolding (React + Node + DB)
2. ✅ Implement authentication
3. ✅ Build guide CRUD API
4. ✅ Integrate rich text editor
5. ✅ Build dashboard UI
6. ✅ Add PDF export
7. ✅ Polish UI/UX and deploy

---


