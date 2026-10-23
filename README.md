name: Generate Word Doc

on:
  workflow_dispatch:

jobs:
  convert_via_pandoc:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Pandoc
        run: sudo apt-get update && sudo apt-get install -y pandoc
      - name: Convert to Word
        run: pandoc -f markdown -t docx -o "my-document.docx" --toc ./README.md
      - name: Upload Word Doc
        uses: actions/upload-artifact@v4
        with:
          name: Word Document
          path: my-document.docx
