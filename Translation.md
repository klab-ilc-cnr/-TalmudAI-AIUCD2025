# TalmudAI-AIUCD2025
# Introduction
This page presents interactions conducted with llama-3.1-70b for translation support from Hebrew-Aramaic to Italian. Suggestions and answers will be provided in Italian.

We randomly selected a total of 300 source-target pairs from the Talmud, each accompanied by translation memory (TM) hints. Each suggestion contained the source string, the target string (i.e., the translation), and the similarity score between the source and the suggested source.
The pairs were filtered to include only those with at least 3 suggestions with a similarity score greater than or equal to 50%. These were then provided to the LLM for translation, first without the suggestions and then with a context composed of the list of suggestions.

Evaluation measures were calculated for the candidate translations against the domain expert-verified target, and the delta between the version with and without suggestions was derived for each. The measures used are: SacreBLEU, BERTscore and Meteor score.
# Source and Target
Source indicates the original Hebrew-Aramaic string, while target indicates the Italian translation. The translation provided by a domain expert is considered the gold reference. We speak of gold reference instead of gold standard because these translations are not necessarily literal but may contain explanatory expansions against a cryptic Hebrew text.
# Prompt template without context
    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.
    Scrivi esclusivamente la traduzione di {testo ebraico} senza scrivere nient'altro.
# Prompt template with context
    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.

    Nel CONTESTO troverai esempi di traduzione nella forma di coppie 
    dove SOURCE è il testo in ebraico-aramaico e TARGET è il testo in italiano.

    I "target" non sono traduzioni letterali di "source" ma possono essere state espanse dal traduttore per una migliore comprensione.

    Non produrre una traduzione concatenando i suggerimenti.

    CONTESTO:
    SOURCE="hebrew segment",TARGET="italian segment"
    …
    SOURCE="hebrew segment",TARGET="italian segment"

    Scrivi esclusivamente la traduzione di {testo ebraico} senza scrivere nient'altro.
# Results
On the metrics considered for our 300 pairs, we calculated averages, obtaining the following results:


|| Bleu | Bert | Meteor |
| --- | --- | --- | --- |
| **LLM** | 11.0939 | 0.7283 | 0.2097 |
| **LLM+TM** | 35.7756 | 0.8273 | 0.5082 |
| **Delta** | 222.48%| 13.60% | 142.37% |


Out of 300 pairs, for 237 we found higher scores for the translation provided by an LLM with context (LLM+TM). If we consider the scores for “positive” results only, we see the following averages:


|| Bleu | Bert | Meteor |
| --- | --- | --- | --- |
| **LLM** | 9.3677 | 0.7213 | 0.1831 |
| **LLM+TM** | 41.9555 | 0.8480 | 0.5656 |
| **Delta** | 347.87%| 17.57% | 208.89% |


The remaining 63 pairs have at least one measure with a negative delta.

We asked a domain expert to evaluate these 63 pairs by anonymizing the origin of the contained strings. The results of the evaluation indicate that out of 63 pairs were identified:

- 18 cases in which both translations were acceptable;
- 4 cases in which the translation of the LLM alone is acceptable;
- 16 cases in which the translation of the LLM with TM is acceptable;
- 25 cases in which no candidate translation was acceptable.

# "Positive" example
Consider a pair which, according to the metrics, gets general improvements from the presence of prompts. The full prompt with hints for the pair passed to the LLM is:

    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.

    Nel CONTESTO troverai esempi di traduzione nella forma di coppie dove "source" è il testo in ebraico-aramaico e "target" è il testo in italiano.
    
    I "target" non sono traduzioni letterali di "source" ma possono essere state espanse dal traduttore per una migliore comprensione.
    
    Non produrre una traduzione concatenando i suggerimenti.
    
    CONTESTO:
    
    "source"="כֵּיוָן דַּאֲמַר לָהּ ”לְמָחָר“ פְּסַקָהּ,","target"="Dal momento che le dice: “Domani” ha interrotto l’azione,"
    
    "source"="כֵּיוָן דַּאֲמַר לָהּ בִּפְרוּטָה וּפְרוּטָה פְּסַקָהּ לְמִילְּתֵיהּ,","target"="Dal momento che ha detto: “Con una perutà e con una perutà”, ha interrotto l’azione,"
    
    "source"="כֵּיוָן דַּאֲמַר לָהּ מָנֶה","target"="Dal momento che ha detto di darle un manè,"
    
    "source"="כֵּיוָן דַּאֲמַר לָהּ ״וַאֲנִי״ –","target"="Dal momento che egli le ha detto “Anche io”,"
    
    "source"="כֵּיוָן דַּאֲמַר לָהּ ״וַאֲנִי״ –","target"="dal momento che egli le ha detto: “Anche io”,"
    
    Scrivi esclusivamente la traduzione di כֵּיוָן דַּאֲמַר לָהּ חֲצִי פְּרוּטָה פְּסַקָהּ senza scrivere nient'altro

We then see the data produced by the processing including metrics:

|  | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>כֵּיוָן דַּאֲמַר לָהּ חֲצִי פְּרוּטָה פְּסַקָהּ</p> |
| **Target** | Dal momento che le ha detto: ‘Mezza perutà’ ha interrotto l’azione |
| **LLM** | Poiché disse a lei mezza peruta, la interruppe |
| **LLM+TM** | Dal momento che le dice: ‘Mezza perutà’ ha interrotto l’azione |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 0.0 | 63.4047 | inf% |
| **BERTscore** | 0.7239 | 0.9845 | 35.99% |
| **MeteorScore** | 0.0327 | 0.8792 | 2588.68% |

# "Negative" example
Consider a pair which, according to metrics, seems to worsen its metrics in the version with prompts compared to the LLM alone. The full prompt with hints for the pair passed to the LLM is:

    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.

    Nel CONTESTO troverai esempi di traduzione nella forma di coppie dove "source" è il testo in ebraico-aramaico e "target" è il testo in italiano.
    
    I "target" non sono traduzioni letterali di "source" ma possono essere state espanse dal traduttore per una migliore comprensione.
    
    Non produrre una traduzione concatenando i suggerimenti
    
    CONTESTO:
    
    "source"="הֶיתֵּר נְדָרִים","target"="Le norme sul proscioglimento dei voti (hettèr nedarìm)"
    
    "source"="אַף נְדָרִים","target"="anche per i nedarìm,"
    
    "source"="וּמַה נְּדָרִים","target"="e come per i nedarìm,"
    
    "source"="וּמַה נְּדָרִים","target"="e come per i nedarìm,"
    
    "source"="וּמַה נְּדָרִים","target"="E come per i nedarìm,"
    
    Scrivi esclusivamente la traduzione di נְדָרִים, senza scrivere nient'altro.

We then see the data produced by the processing including metrics:

|  | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>נְדָרִים,</p> |
| **Target** | Per quanto riguarda le offerte di voto, |
| **LLM** | Voti |
| **LLM+TM** | nedarìm |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 0.0 | 0.0 | 0.00% |
| **BERTscore** | 0.654 | 0.5737 | -12.28% |
| **MeteorScore** | 0.0 | 0.0 | 0.00% |