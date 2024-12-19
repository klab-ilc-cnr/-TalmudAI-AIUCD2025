# TalmudAI-AIUCD2025
# Introduction
This page presents the interactions conducted with LLM llama-3.1-8b and llama-3.1-70b-versatile for Hebrew-Aramaic to Italian translation support. Prompts and responses will be provided in Italian.
# Original and Gold Translation
We consider as gold translation the Italian translation provided by a domain expert.
## Original
כֵּיוָן דַּאֲמַר לָהּ חֲצִי פְּרוּטָה פְּסַקָהּ,
## Gold
Dal momento che le ha detto: “Mezza perutà” ha interrotto l’azione
## Querying the LLMs Directly
### The Prompt
    Traduci la seguente frase dall'ebraico-aramaico all'italiano. Non dare spiegazioni, non inserire incisi: “כֵּיוָן דַּאֲמַר לָהּ חֲצִי פְּרוּטָה פְּסַקָהּ”
### The Answer from llama-3.1-8b
Non appena le disse: 'La metà di una prugna è tagliata'
### The Answer from llama-3.1-70b-versatile
Poiché disse a lei mezza peruta, la interruppe.
## Querying the LLMs with Example Context
### The Prompt
    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.
    In CONTESTO troverai un json con degli esempi di traduzione come coppie di stringhe.
    ORIGINALE è la stringa in ebraico-aramaico. TRADUZIONE è la stringa in italiano traducente la stringa ORIGINALE. TRADUZIONE traduce parzialmente ORIGINALE.
    CONTESTO: [
    {
        "ORIGINALE":”כֵּיוָן דַּאֲמַר לָהּ ”לְמָחָר“ פְּסַקָהּ” ,
        "TRADUZIONE": "Dal momento che le dice: “Domani” ha interrotto l’azione”
    },
    {
        "ORIGINALE": “כֵּיוָן דַּאֲמַר לָהּ בִּפְרוּטָה וּפְרוּטָה פְּסַקָהּ לְמִילְּתֵיהּ”,
        "TRADUZIONE": "Dal momento che ha detto: “Con una perutà e con una perutà”, ha interrotto l’azione”
    },
    {
        "ORIGINALE": “כֵּיוָן דַּאֲמַר לָהּ מָנֶה”,
        "TRADUZIONE": "Dal momento che ha detto di darle un manè”
    },
    {
        "ORIGINALE": "כֵּיוָן דַּאֲמַר לָהּ ״וַאֲנִי״",
        "TRADUZIONE": "dal momento che egli le ha detto: “Anche io”"
    },
    {
        "ORIGINALE": "כֵּיוָן דַּאֲמַר לָהּ ״וַאֲנִי״",
        "TRADUZIONE": "Dal momento che egli le ha detto “Anche io”,”
    }
    ]
    Esegui la traduzione della seguente stringa senza darmi ulteriori informazioni stampando esclusivamente la stringa tradotta: “כֵּיוָן דַּאֲמַר לָהּ חֲצִי פְּרוּטָה פְּסַקָהּ”
### The Answer from llama-3.1-8b
Dal momento che le ha detto: “Mezza perutà e poi interrotta l’azione”
### The Answer from llama-3.1-70b-versatile
Dal momento che le dice: “Mezza perutà” ha interrotto l’azione
## BRT score

| | Precision | Recall | F1 |
| ------------- | ------------- | ------------- | ------------- |
| **3.1 8b senza contesto** | 0.6139 | 0.6210 | 0.6174 |
| **3.1 70b senza contesto** | 0.7178 | 0.6867 | 0.7019 |
| **3.1 8b con contesto** | 0.9118 | 0.9514 | 0.9311 |
| **3.1 70b con contesto** | 0.9609 | 0.9500 | 0.9554 |

## BLEU score

| | BLEU 1-gram | BLEU 2-gram | BLEU 3-gram | BLEU n-gram |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| **3.1 8b senza contesto** | 0.08333333333333333 | 4.306075028866568e-155 | 3.918478908927222e-204 | 9.788429383461836e-232 |
| **3.1 70b senza contesto** | 0.07961459006375435 | 3.562756439221896e-155 | 3.0873258504067864e-204 | 7.536728468577135e-232 |
| **3.1 8b con contesto** | 0.7142857142857143 | 0.6629935441317959 | 0.6065355199364347 | 0.5622008276590377 |
| **3.1 70b con contesto** | 0.8300915602566021 | 0.7786949072647974 | 0.7190658730571503 | 0.6407117598241614 |
