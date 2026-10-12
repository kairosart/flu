# Report generation

This lab's walkthrough PDF (`flu-report.pdf`) is generated from these notes by
the `offsec-lab-report` skill. The report layout is fixed:

1. Page 1 — the front-page title card (`frontpage.png`).
2. Page 2 — the cover (lab, OS, flags, summary).
3. Page 3+ — one section per `.md` note in this folder.

Per-lab settings live in `.report.json` (lab name, OS, flags, summary and the
front image), so regeneration is a single command:

```bash
python3 /home/kali/.config/opencode/skill/offsec-lab-report/scripts/md2pdf_weasy.py \
  "/media/sf_Obsidian/Offsec/flu" /tmp/opencode/flu-report.pdf \
  && docker cp /tmp/opencode/flu-report.pdf obsidian:/vaults/Offsec/flu/flu-report.pdf
```

The first command rebuilds the PDF from the notes; the second copies it into the
Obsidian vault (the vault mount is not directly writable, so it goes through the
`obsidian` container).

> [!note]
> This note is listed under `exclude` in `.report.json`, so it is not embedded
> into the generated PDF. Remove it from `exclude` if you want it included.
