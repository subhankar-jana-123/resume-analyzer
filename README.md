# Resume Matcher

Reads resumes (PDF, DOCX, TXT), extracts skills, scores them against job descriptions, and recommends skills to learn.

## Run
    pip install -r requirements.txt
    uvicorn app.main:app --reload
Open http://127.0.0.1:8000 and upload `sample_resume.txt`. API docs: /docs.

## How it works
- **Parsing:** pypdf / python-docx, then regex for name, email, years of experience.
- **Skill extraction:** taxonomy of ~45 skills with aliases in `app/skills.py` (add your own).
- **Scoring:** 65% skill coverage + 35% TF-IDF cosine similarity (`app/nlp.py`).
- **Gap analysis:** missing skills per job, ranked by how many of the top 3 roles they unlock.
- **Storage:** SQLite (`candidates`, `jobs`); six sample jobs are seeded.

## Ideas to extend
Sentence-embedding similarity, spaCy NER, auth, job import, tests.
