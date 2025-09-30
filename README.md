# 🎓 Conversational AI for Tailored Educational Pathways

An end-to-end conversational system that **analyzes a resume**, identifies **skill gaps**, recommends **targeted courses**, and **matches jobs** using ESCO skills — with a simple **Streamlit** UI and **MongoDB Atlas** backend.

---

## 🚀 Executive Summary
- Tackles resume–job **vocabulary mismatch** by aligning to the **ESCO** skills taxonomy (~14k skills).
- **Job matching:** TF-IDF + **cosine similarity** over resume vs. job descriptions to surface top fits.
- **Skill-gap detection:** compares live job needs to the user’s resume and proposes **Coursera/Udemy** courses.
- **Data & app stack:** Streamlit front end, **MongoDB Atlas** for skills and listings, Python data/ML tooling.
- **Evaluation:** precision/recall/F1 and **K-Fold** checks for the job-match pipeline’s stability.

---

## ✨ Features
- **Conversational intake**: goals, current role, skills, location.
- **Resume parsing (PDF)**: extract text and normalize to ESCO skills.
- **Job retrieval & ranking**: fetch/store listings, vectorize text, compute **cosine similarity**, return top N.
- **Skill-gap finder**: detect missing skills vs. current market and generate **course links** (Coursera/Udemy).
- **Persistent storage**: MongoDB Atlas collections for ESCO skills & job listings.
- **Simple UI**: Streamlit app with file upload, inputs (title, location), and results panes.

---

## 🧠 How It Works (Architecture)
**Pipeline**
1. **Ingest**: Upload resume (PDF) → text extraction.
2. **Normalize**: Map detected skills to **ESCO** preferred labels.
3. **Jobs**: Retrieve/refresh job posts; store in MongoDB.
4. **Vectorize**: TF-IDF on resume keywords + job descriptions.
5. **Rank**: Cosine similarity → **Top 5** matches with title/company/link.
6. **Skill gaps**: Compare resume vs. aggregated job requirements → missing skills.
7. **Courses**: Generate direct search links for each missing skill (Coursera/Udemy).
8. **Serve**: Streamlit UI ties it all together.

**Core Components**
- **UI**: Streamlit app (file uploader, inputs, results, loading states).
- **NLP/ML**: `scikit-learn` (TF-IDF, cosine), `re` for keyword matching.
- **Data**: MongoDB Atlas (ESCO Skills collection; Job Listings collection).
- **LLM hook (optional)**: helper to summarize job skill demands / extract missing skills.

---

## 🗂️ Data & Sources
- **ESCO** skills taxonomy for skill normalization and matching.
- **Job postings** (stored in MongoDB) from Indeed (scraped or via API integration).
- **Courses**: outbound links to Coursera/Udemy generated per missing skill keyword.

> ⚠️ For production, replace scraping with a **jobs API** and add rate-limit/error handling.

---

## 🔬 Evaluation
- **Classification-style metrics** on match relevance: **Precision, Recall, F1**.
- **Robustness** with **K-Fold** to check stability across splits.
- Qualitative checks: top-N match inspection, user feedback on course relevance.

---

## 🛠️ Tech Stack
- **Python**: `pandas`, `numpy`, `scikit-learn`, `PyPDF2`, `pymongo`, `re`
- **App**: **Streamlit**
- **DB**: **MongoDB Atlas**

---

## ⚙️ Setup

### 1) Clone & env
```bash
git clone <your-repo-url>
cd <your-repo>
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env     # then open .env and set secrets
