# Banjul Researcher

**Live:** https://lszoszk.github.io/banjul-researcher/

A search engine over the decisions of the African Commission on Human and Peoples' Rights (Banjul) and the judgments, rulings, orders and separate opinions of the African Court on Human and Peoples' Rights (Arusha), and the Commission's general comments and principles and guidelines, at the level of the numbered paragraph. The name comes from the Banjul Charter, as the African Charter on Human and Peoples' Rights is often called.

Corpus built on 2026-11-27: 1,079 documents (23 of them general comments and guidelines) and 71,758 paragraphs, plus 47 unofficial English machine translations of Commission decisions published only in French.

## What it does

- **Search** every paragraph with phrases, `OR`, `NOT`, prefixes (`indigen*`) and field operators: `violation:7`, `nonviolation:2`, `article:ICCPR-14`, `state:Kenya`, `case:245/02`, `year:2015-2020`, `body:court`. Filters for the body, the type of decision, the respondent State, the year, the language and the operative part only. Results can be grouped by decision or listed by paragraph, and each paragraph links to the PDF at the right page and copies a citation. A link such as `?q="free legal assistance"` opens a search.
- **Check** finds the citations of the Commission and the Court in a pasted text (communication and application numbers, "X v State", "cited above") and checks that the number exists and matches the name, that the pinpointed paragraph exists, and that a quotation matches the decision word for word. The text stays in the browser.
- **Statistics** of decisions by year, respondent State and article found violated.

## Use with your AI assistant

The MCP server [mcp-banjul](https://github.com/lszoszk/mcp-banjul) offers the same search and citation check to Claude, ChatGPT and other assistants that support the Model Context Protocol. Connector address: `https://150.254.115.204/banjul-mcp/mcp` (Claude Code: `claude mcp add --transport http banjul https://150.254.115.204/banjul-mcp/mcp --scope user`).

## How the corpus was prepared

- Sources: the Commission's library at https://achpr-library.uwazi.io and the Court's AJUDATA at https://ajudata.african-court.org (English versions of the Court's documents). Identical files listed twice are kept once.
- Born-digital PDFs are read from their own text layer. Scans (376 files, 7,000 pages) were read again with Chandra OCR 2, because the text layer they carry is too poor to search. Checked against the OCR, the text layer of born-digital files differs in about 0.3% of words; a manual check of 25 OCR paragraphs (1,853 words) against the scans found no word errors.
- Paragraphs are found by their numbers: the longest consistent sequence of numbered paragraphs in a document is taken as its structure. Running heads, footers, footnotes and signature blocks are left out. Documents without numbered paragraphs are split by page.
- Findings of violation. Court: extracted from the operative parts by rules; checked against the statuses the Court records in AJUDATA, they agree in 96% of the violations found and find 93% of those recorded (born-digital judgments; 95% and 84% for scanned judgments). Commission: its library records no findings and the Commission often decides an article only in its reasoning, so the findings of its 176 decisions on the merits are read from the decision by a language model (Claude Sonnet), which must give the paragraph and the exact words each finding rests on; the words are checked automatically against the text. On 68 (decision, article) pairs checked against the text, chosen among the hardest cases, the reader was right in all 68 (the rules in 37); the check set was itself prepared with a model, so this is an upper bound. Alleged articles are those claimed by the complainant or applicant, plus those the body ruled on.
- Machine translations of the 47 French-only Commission decisions follow the method of the HUDOC Researcher translations (instructions, glossary, examples from official translations, automatic checks). On three decisions with an official English version, chrF is 70–80. They are marked as unofficial, are not in the default search, and show the French original paragraph by paragraph.

## Files

| File | Content |
|---|---|
| `index.html` | the whole application |
| `docs.json` | the documents with their metadata and findings (`docs`), section headings (`heads`), build information (`info`) |
| `p0.json` … | the paragraphs: `rows` of `[document index, paragraph number, PDF page, heading index, text]` from position `start` |

## Limits

- The Court is covered in English only; the Commission in the language of its library.
- The text may contain OCR errors, and in two scanned decisions the paragraph numbering could not be recovered. The PDF is the authoritative version.
- Findings and machine translations are research aids: confirm them in the decision before relying on them.

## Licence and citation

Software: PolyForm Noncommercial 1.0.0 (`LICENSE`). Curated dataset (paragraphs, metadata, findings, translations): CC BY-NC-SA 4.0 (`LICENSE-DATA`). The decisions are the work of the Commission and the Court (`NOTICE`). The project is not affiliated with or endorsed by either body, and it is a research aid that does not constitute legal advice.

Szoszkiewicz, Ł. (2026). *Banjul Researcher* [search engine]. Adam Mickiewicz University, Poznań. https://lszoszk.github.io/banjul-researcher/
