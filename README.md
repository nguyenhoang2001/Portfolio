# Portfolio Website

A static portfolio site that connects to the multi-agent FastAPI backend so visitors can chat with an AI that knows your background.

## Folder Structure

```
portfolio/
├── src/
│   ├── index.html        # Main page — hero, experience, projects, chat widget
│   ├── css/
│   │   └── style.css     # Dark-mode design system
│   └── js/
│       └── chat.js       # SSE streaming chat → FastAPI backend
└── public/
    ├── documents/
    │   └── resume.pdf    # ← drop your resume here
    └── images/
        └── avatar.jpeg    # ← drop your photo here (optional)
```

## Quick Start

1. **Drop your files in:**
   - `public/documents/resume.pdf` — your resume
   - `public/images/avatar.jpeg` — your profile photo

2. **Fill in `src/index.html`:**
   - Update hero bio, name, title
   - Add experience entries in the timeline
   - Add more project cards
   - Update footer links (GitHub, LinkedIn, email)

3. **Open the site locally:**

   ```bash
   # any static server works, e.g.:
   cd portfolio/src
   python3 -m http.server 3000
   # then open http://localhost:3000
   ```

4. **Make sure the backend is running** (for the chat widget):
   ```bash
   uvicorn app.main:app --reload
   ```
   The chat widget defaults to `http://localhost:8000`. Update `API_BASE_URL` in `src/js/chat.js` when you deploy.

## Adding the Resume Agent

When you're ready to add a resume-reading agent:

1. Drop your resume PDF in `knowledge_base/files/` (the existing knowledge base folder).
2. Update `knowledge_base/sources.py` to include your resume as a document source.
3. Rebuild the FAISS index so the retriever agent can search it.
4. The existing `retriever_agent` will automatically be able to answer questions from it.

## Deployment

Since this is a plain HTML/CSS/JS site, you can host it anywhere:

- **GitHub Pages** — push `portfolio/src/` to a `gh-pages` branch
- **Netlify / Vercel** — drag-and-drop or connect your repo
- **Nginx** — serve the `portfolio/src/` directory as the web root

Remember to update `API_BASE_URL` in `chat.js` to your deployed backend URL and configure CORS in the FastAPI app accordingly.
