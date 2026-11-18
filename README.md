# Civic Audit site v2: DRAFT, NOT PUSHED

This is the upgraded version of https://ayaanrustagi.github.io/civic-audit/ (repo `ayaanrustagi/civic-audit`). It was built on 18 Nov 2026 from `latest/data/parsed/results.json` by `ec/tools/build_data.py` and `ec/tools/build_site.py`. `ec/tools/check_site.py` self-checks it for private names, numbers matching the data, anchors and files, and external links.

New in v2: a hero finding, four case studies, an error explorer (filter by body, severity, type, meeting page or article, and text search; filters are kept in the URL), Citizen Portal's words side by side with the record and links to both, methods with the checker accuracy table, limits and strengths, a "Response from Citizen Portal" placeholder, downloadable CSV and JSON of all 1,999 claims and 128 error rows, a how-to-cite block (text and BibTeX), and about the author, ethics and AI-use sections.

The red Draft banner, `noindex, nofollow` and the `[DRAFT]` title are kept until Ayaan confirms the labels and 1 Dec 2026 has passed.

To rebuild after the labels change: rerun the pipeline report, then run
`python3 ec/tools/build_data.py && python3 ec/tools/build_site.py && python3 ec/tools/check_site.py`.
