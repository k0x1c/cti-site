---
title: "Disclosures"
description: "Security vulnerabilities I have responsibly disclosed. All findings were reported to the affected vendors and patched before public disclosure."
ShowToc: false
ShowReadingTime: false
---

Security vulnerabilities I have responsibly disclosed. All findings were reported to the affected vendors and patched before public disclosure.

| CVE / ID | Product | Summary | Severity | Date | References |
|---|---|---|---|---|---|
| CVE-2026-34724 | Zammad | server-side template injection to RCE via the new AI Agent feature | High (8.7) | 2026-04-08 | [CVE](https://nvd.nist.gov/vuln/detail/CVE-2026-34724), [GHSA](https://github.com/zammad/zammad/security/advisories/GHSA-fg9w-jg8f-4j94), [Blog post](/posts/zammad-ssti-rce-ai-agent-cve-2026-34724/) |
| CVE-2026-34719 | Zammad | direct-request server-side request forgery (SSRF) via webhooks | High (8.3) | 2026-04-08 | [CVE](https://nvd.nist.gov/vuln/detail/CVE-2026-34719), [GHSA](https://github.com/zammad/zammad/security/advisories/GHSA-2vgc-vfh2-rw75), [Blog post](/posts/zammad-ssrf-webhooks-cve-2026-34719/) |
| CVE-2026-34718 | Zammad | stored XSS / phishing via `data:` URI HTML sanitizer bypass | Moderate (5.3) | 2026-04-08 | [CVE](https://nvd.nist.gov/vuln/detail/CVE-2026-34718), [GHSA](https://github.com/zammad/zammad/security/advisories/GHSA-c2cf-9fc7-jhf3), [Blog post](/posts/zammad-data-uri-xss-cve-2026-34718/) |
