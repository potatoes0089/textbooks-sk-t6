# Buku teks — served files

Content-addressed pieces of the KPM textbook PDFs used by Ez-RPH. Each book is
`<shard>/<editionSlug>/<servedSha256>.pNNN`, where a shard is one GitHub
repository per grade (`sjkc-t3` → `textbooks-sjkc-t3`); `manifest.json` lists
every piece with its size and sha256 and gives each book an absolute `baseUrl`,
so a consumer never composes a URL. To rebuild a book:
`cat <servedSha256>.p* > book.pdf` and check `sha256sum book.pdf` against
`servedSha256`. Pages are identical to the source PDF (same page count, same
page numbers, same MediaBox/CropBox/rotation); some books are Ghostscript
/ebook re-encodings to stay under GitHub's 100 MiB per-file limit.

Every re-encode is byte-reproducible: the same source PDF and the same
Ghostscript build (10.06.0, the version this release was verified against)
always produce the same `servedSha256`, so a release can be rebuilt and
checked against `contentManifestSha256`.

`compressed` is true for a transformed served file. A flattened book also has
`flattened: true`; it is an image-only PDF whose page boxes are the source
CropBoxes. The original source PDF remains the identity and overlay authority.

Published by docs/textbook/tools/publish_pdfs.py — do not edit by hand.
