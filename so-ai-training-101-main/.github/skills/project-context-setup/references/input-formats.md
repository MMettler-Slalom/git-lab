# Input Format Handling

Notes for extracting content from each supported source format. The goal
is always: get faithful plain text into context so facts can be cited.

## Markdown (.md) and Plain Text (.txt)

Read directly. No conversion needed. Watch for:
- Front matter (YAML) that may carry metadata
- Embedded code fences or tables — preserve structure when quoting

## Word Documents (.docx)

`.docx` is a zip file containing `word/document.xml`. On Windows
PowerShell, extract with:

```powershell
$src = "path\to\doc.docx"
$dst = "$env:TEMP\doc_extract"
Add-Type -AssemblyName System.IO.Compression.FileSystem
# Copy first to avoid file locks if the doc is open elsewhere
Copy-Item $src "$env:TEMP\copy.docx" -Force
[System.IO.Compression.ZipFile]::ExtractToDirectory("$env:TEMP\copy.docx", $dst, $true)
Get-Content "$dst\word\document.xml" -Raw
```

The XML is verbose. Strip tags or scan with `Select-String` for the
fields you need. If the doc is large, ask the user for a `.md` or `.txt`
export.

**Common gotcha:** if the source file is in the workspace and open in
Word, file-lock errors occur. Copy to `$env:TEMP` first.

## PDF (.pdf)

Prefer asking the user for a text export. If extraction is needed,
suggest the user run a tool locally (e.g., `pdftotext`, or VS Code's
PDF preview copy-paste). Do not attempt OCR.

## Email Exports (.eml, .msg)

- `.eml` is plain MIME — readable as text; pull `Subject`, `From`,
  `Date`, and the body.
- `.msg` is a binary Outlook format. Ask the user to export to `.eml`
  or paste the body as text.

## Transcripts (.vtt, .srt)

Both are line-based. Strip the timestamps and speaker labels into a
running narrative, but preserve speaker attribution — speaker identity
is often the key to disambiguating claims.

## Multi-file Projects

When the user provides multiple sources:
- Treat them as one corpus, but keep track of which source each fact
  came from.
- When sources conflict, record both versions in the output file's
  Open Questions or Validation Recommended section, with attribution.
- If sources cover different scopes (e.g., one is org-wide, one is a
  single team), call that out in the initial check-in so the user can
  decide whether to combine or split outputs.
