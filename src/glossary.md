---
title: "Segment Glossary"
description: "Glossary of terms used in the Segment documentation"
hide_toc: true
hide-feedback: true
layout: page
---
<span id="doc-content" />

{% for entry in site.data.glossary %}### **{{ entry[0] }}**
{{ entry[1] | markdownify }}
{% endfor %}