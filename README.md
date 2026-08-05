# HSK Atelier 汉语工坊

Chinese revision web app (HSK 1 → 6). One HTML file, external data.

## Run

Data is JSON loaded via `fetch`, so a tiny local server is required:

```bash
python3 -m http.server 8080     # or: npx serve
# then open http://localhost:8080
```

## Structure

```
index.html          → the complete app (UI + learning engine)
data/manifest.json  → level index
data/hsk1.json      → HSK 1 course data (English)
```

## Adding a level (HSK 2 → 6)

1. Create `data/hsk2.json` following the `hsk1.json` schema:
   - `id`, `level`, `title`, `hanzi`, `tagline`
   - `chapters[]`: `title`, `short`, `covers`, `intro`, `words[] {hanzi, pinyin, mean}`, `grammar[] {title, rule, examples[] {hanzi, pinyin, mean}}`
   - `memo {structures[], tones[], pitfalls[]}` and `production[] {prompt, answer {hanzi, pinyin}}`
2. In `data/manifest.json`, set `"available": true` for that level.
3. Done — UI, progress, audio and exercises work automatically.

> Each word must appear **only once** per file (progress is keyed by character).

## Built-in pedagogy

- **Active recall**: flashcards + MCQs (guess before you see)
- **Light spaced repetition**: a word is mastered after 3 correct answers in a row, plus a Daily review queue
- **Multi-sensory**: zh-CN voice (normal + slow 🐢), tone-colored pinyin
- **Interleaving**: “All mixed” mode
- **Production**: self-assessed mini-quiz (7 sentences)
- Progress, day streak 🔥 and settings (hidden pinyin, auto audio) stored in `localStorage`