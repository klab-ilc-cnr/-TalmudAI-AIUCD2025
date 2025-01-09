# TalmudAI-AIUCD2025
# Introduction
This page presents the interactions conducted with llama-3.1-70b for Hebrew-Aramaic to Italian translation support. Prompts and responses will be provided in Italian.

We randomly selected a total of N source-target pairs from the Talmud, each accompanied by translation memory (TM) suggestions. Each hint contained the source string, the target string (i.e., the translation), and the similarity score between the source and the suggested source.
We then filtered the pairs keeping only those with at least 3 suggestions with a similarity score greater than or equal to 50%. The resulting 66 pairs were provided to the LLM for translation, first without the suggestions and then with a context composed of the list of suggestions.

Rating measures were calculated for the candidate translations against the domain expert-verified target, and the delta between the version with and without suggestions was derived for each. The measures used are: SacreBLEU, BERTscore and Meteor score.
# Source and Target
Source indicates the original Hebrew-Aramaic string, while target indicates the Italian translation. The translation provided by a domain expert is considered the gold standard.
# Prompt template without context
    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.
    Scrivi esclusivamente la traduzione di {testo ebraico} senza scrivere nient'altro.
# Prompt template with context
    Sei un esperto di traduzioni dall'ebraico-aramaico all'italiano.

    Nel CONTESTO troverai esempi di traduzione nella forma di coppie 
    dove SOURCE è il testo in ebraico-aramaico e TARGET è il testo in italiano.
    CONTESTO:
    SOURCE="hebrew segment",TARGET="italian segment"
    …
    SOURCE="hebrew segment",TARGET="italian segment"

    Scrivi esclusivamente la traduzione di {testo ebraico} senza scrivere nient'altro.
# Results
Out of 66 pairs, for 54 we found higher scores for the translation provided by an LLM with context. 


|| **SacreBLEU** | **BERTscore** | **Meteor** |
| ------------- | ------------- | ------------- | ------------- |
| **LLM+TM** | 0,5869 | 0,7695 | 0,3551 |
| **LLM** | 0,1845 | 0,8911 | 0,7180 |
| **(LLM+TM)-LLM** | 218,07% | 15,80% | 102,17% |


The remaining 12 pairs have at least one measure with a negative delta.

We asked a domain expert to evaluate these 12 pairs by anonymizing the origin of the contained strings. The results of the evaluation indicate that out of 12 pairs were identified:

- 5 cases in which both translations were acceptable;
- 2 cases in which the translation of the LLM alone is acceptable;
- 2 cases in which the translation of the LLM with TM is acceptable;
- 3 cases in which no candidate translation was acceptable.
# Complete Output


| **N. 1** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מֵאֵימָתַי קוֹרִין אֶת שְׁמַע בָּעֲרָבִין?</p> |
| **Target** | Da quando si legge lo Shemà‘ della sera? |
| **LLM** | Da quando si recita lo Shemà di sera? |
| **LLM+TM** | Da quando si recita lo Shemà‘ della sera? |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 23.3569 | 59.6949 | 155.58% |
| **BERTscore** | 0.9222 | 0.9744 | 5.66% |
| **MeteorScore** | 0.6792 | 0.8951 | 31.79% |

___



| **N. 2** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מִשָּׁעָה שֶׁהַכֹּהֲנִים נִכְנָסִים לֶאֱכוֹל בִּתְרוּמָתָן</p> |
| **Target** | Dall’ora in cui i kohanìm entrano a mangiare la loro terumà |
| **LLM** | Dall'ora in cui i sacerdoti entrano per mangiare la loro offerta. |
| **LLM+TM** | Dall’ora in cui i kohanìm entrano a mangiare la loro terumà. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 22.2652 | 91.3101 | 310.10% |
| **BERTscore** | 0.7942 | 0.96 | 20.88% |
| **MeteorScore** | 0.5213 | 0.9921 | 90.31% |

___



| **N. 3** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>עַד סוֹף הָאַשְׁמוּרָה הָרִאשׁוֹנָה,</p> |
| **Target** | fino alla fine della prima veglia; |
| **LLM** | fino alla fine del primo turno di guardia |
| **LLM+TM** | Fino alla fine della prima veglia |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 21.1918 | 80.9107 | 281.80% |
| **BERTscore** | 0.8057 | 0.9329 | 15.79% |
| **MeteorScore** | 0.4147 | 0.8676 | 109.21% |

___



| **N. 4** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>דִּבְרֵי רַבִּי אֱלִיעֶזֶר.</p> |
| **Target** | queste sono le parole di rabbì Elièzer. |
| **LLM** | Le parole di Rabbi Eliezer. |
| **LLM+TM** | parole di rabbì Elièzer |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 22.0896 | 34.5721 | 56.51% |
| **BERTscore** | 0.7421 | 0.8374 | 12.84% |
| **MeteorScore** | 0.4808 | 0.5222 | 8.61% |

___



| **N. 5** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וַחֲכָמִים אוֹמְרִים:</p> |
| **Target** | E i Chakhamìm (Saggi) dicono: |
| **LLM** | E i saggi dicono: |
| **LLM+TM** | Mentre i Saggi dicono: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 16.5158 | 13.1345 | -20.47% |
| **BERTscore** | 0.8122 | 0.8123 | 0.01% |
| **MeteorScore** | 0.5792 | 0.4099 | -29.23% |

___



| **N. 6** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>עַד חֲצוֹת.</p> |
| **Target** | Fino a mezzanotte. |
| **LLM** | Fino a mezzanotte. |
| **LLM+TM** | fino a mezzogiorno |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 100.0 | 31.9472 | -68.05% |
| **BERTscore** | 1.0 | 0.8039 | -19.61% |
| **MeteorScore** | 0.9922 | 0.4808 | -51.54% |

___



| **N. 7** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>רַבָּן גַּמְלִיאֵל אוֹמֵר:</p> |
| **Target** | Rabbàn Gamlièl dice: |
| **LLM** | Rabban Gamliel dice: |
| **LLM+TM** | Rabbàn Gamlièl dice: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 31.9472 | 100.0 | 213.02% |
| **BERTscore** | 0.9264 | 1.0 | 7.94% |
| **MeteorScore** | 0.4688 | 0.9922 | 111.65% |

___



| **N. 8** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>עַד שֶׁיַּעֲלֶה עַמּוּד הַשַּׁחַר.</p> |
| **Target** | Fino allo spuntare dell’alba (‘ammùd hashàchar). |
| **LLM** | Finché non sorga la colonna del mattino. |
| **LLM+TM** | fino allo spuntare dell’alba |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.7677 | 29.8475 | 526.04% |
| **BERTscore** | 0.6687 | 0.8093 | 21.03% |
| **MeteorScore** | 0.0431 | 0.5251 | 1118.33% |

___



| **N. 9** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אָמְרוּ לוֹ:</p> |
| **Target** | gli dissero: |
| **LLM** | Gli dissero: |
| **LLM+TM** | Gli dissero: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 100.0 | 100.0 | 0.00% |
| **BERTscore** | 0.9472 | 0.9472 | 0.00% |
| **MeteorScore** | 0.9815 | 0.9815 | 0.00% |

___



| **N. 10** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>לֹא קָרִינוּ אֶת ”שְׁמַע“.</p> |
| **Target** | Non abbiamo detto lo Shemà‘. |
| **LLM** | Non abbiamo recitato "Shemà". |
| **LLM+TM** | non abbiamo recitato ”Shemà“ |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 15.2072 | 16.2334 | 6.75% |
| **BERTscore** | 0.8327 | 0.8263 | -0.77% |
| **MeteorScore** | 0.4509 | 0.3704 | -17.85% |

___



| **N. 11** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אָמַר לָהֶם:</p> |
| **Target** | Disse loro rabbàn Gamlièl: |
| **LLM** | Disse loro: |
| **LLM+TM** | Disse loro: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 23.6435 | 23.6435 | 0.00% |
| **BERTscore** | 0.7658 | 0.7658 | 0.00% |
| **MeteorScore** | 0.5324 | 0.5324 | 0.00% |

___



| **N. 12** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וְלֹא זוֹ בִּלְבַד אָמְרוּ,</p> |
| **Target** | E non solo riguardo a quel precetto dello Shemà‘ lo dissero, |
| **LLM** | E non solo dissero |
| **LLM+TM** | e non solo per questo l'hanno detto? |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 13.546 | 12.606 | -6.94% |
| **BERTscore** | 0.6608 | 0.7148 | 8.17% |
| **MeteorScore** | 0.3099 | 0.2356 | -23.98% |

___



| **N. 13** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מִצְוָתָן עַד שֶׁיַּעֲלֶה עַמּוּד הַשַּׁחַר;</p> |
| **Target** | può essere compiuto fino allo spuntare dell’alba: |
| **LLM** | fino a quando non sorga la colonna del mattino |
| **LLM+TM** | può essere compiuta fino allo spuntare dell’alba |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.8735 | 41.1134 | 743.61% |
| **BERTscore** | 0.6592 | 0.9522 | 44.45% |
| **MeteorScore** | 0.0505 | 0.8018 | 1487.72% |

___



| **N. 14** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>הֶקְטֵר חֲלָבִים וְאֵבָרִים –</p> |
| **Target** | la bruciatura del grasso e delle membra dei sacrifici |
| **LLM** | Brucia il grasso e le interiora |
| **LLM+TM** | la bruciatura del grasso e delle membra |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 9.5354 | 72.598 | 661.35% |
| **BERTscore** | 0.7873 | 0.9201 | 16.87% |
| **MeteorScore** | 0.2155 | 0.7943 | 268.58% |

___



| **N. 15** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מִצְוָתָן עַד שֶׁיַּעֲלֶה עַמּוּד הַשַּׁחַר,</p> |
| **Target** | può essere compiuta fino allo spuntare dell’alba, |
| **LLM** | fino a quando non sorga la colonna del mattino |
| **LLM+TM** | possono essere compiuti fino allo spuntare dell’alba. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.8735 | 36.5555 | 650.09% |
| **BERTscore** | 0.6787 | 0.9376 | 38.15% |
| **MeteorScore** | 0.0505 | 0.6918 | 1269.90% |

___



| **N. 16** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וְכָל הַנֶּאֱכָלִים לְיוֹם אֶחָד –</p> |
| **Target** | e tutti i sacrifici che si mangiano in un solo giorno |
| **LLM** | e tutti gli alimenti che si consumano in un solo giorno |
| **LLM+TM** | e tutto ciò che può essere consumato soltanto nello stesso giorno |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 31.7023 | 4.9324 | -84.44% |
| **BERTscore** | 0.9123 | 0.7851 | -13.94% |
| **MeteorScore** | 0.7081 | 0.1364 | -80.74% |

___



| **N. 17** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מִצְוָתָן עַד שֶׁיַּעֲלֶה עַמּוּד הַשַּׁחַר,</p> |
| **Target** | possono essere consumati fino allo spuntare dell’alba. |
| **LLM** | fino a quando non sorga la colonna del mattino |
| **LLM+TM** | può essere compiuta fino allo spuntare dell’alba, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.8735 | 36.5555 | 650.09% |
| **BERTscore** | 0.6692 | 0.8773 | 31.10% |
| **MeteorScore** | 0.0505 | 0.6918 | 1269.90% |

___



| **N. 18** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>כְּדֵי לְהַרְחִיק אָדָם מִן הָעֲבֵירָה.</p> |
| **Target** | Al fine di allontanare l’uomo dalla trasgressione. |
| **LLM** | Per allontanare l'uomo dal peccato. |
| **LLM+TM** | è per allontanare l’uomo dal peccato |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 6.5673 | 11.0448 | 68.18% |
| **BERTscore** | 0.8688 | 0.8308 | -4.37% |
| **MeteorScore** | 0.1042 | 0.405 | 288.68% |

___



| **N. 19** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>יְצִיאוֹת הַשַּׁבָּת שְׁתַּיִם שֶׁהֵן אַרְבַּע בִּפְנִים</p> |
| **Target** | Le possibilità di trasferire oggetti di Shabbàt vietate dalla Torà, nel caso in cui la persona che sta dentro (in dominio privato) abbia steso la mano fuori, sono due, che diventano quattro, aggiungendo due divieti di origine rabbinica; |
| **LLM** | Le uscite del sabato sono due che sono quattro all'interno. |
| **LLM+TM** | Le uscite di Shabbat sono due che diventano quattro, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 2.0447 | 6.5043 | 218.11% |
| **BERTscore** | 0.6709 | 0.746 | 11.19% |
| **MeteorScore** | 0.0601 | 0.1692 | 181.53% |

___



| **N. 20** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וּשְׁתַּיִם שֶׁהֵן אַרְבַּע בַּחוּץ,</p> |
| **Target** | e anche nel caso in cui la persona che sta fuori (in dominio pubblico) abbia steso la mano dentro sono due, che diventano quattro, aggiungendo due divieti di origine rabbinica. |
| **LLM** | E due che sono quattro fuori, |
| **LLM+TM** | e due che diventano quattro fuori |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 1.7176 | 4.6745 | 172.15% |
| **BERTscore** | 0.6565 | 0.6976 | 6.26% |
| **MeteorScore** | 0.1087 | 0.1592 | 46.46% |

___



| **N. 21** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>פָּשַׁט הֶעָנִי אֶת יָדוֹ לִפְנִים וְנָתַן לְתוֹךְ יָדוֹ שֶׁל בַּעַל הַבַּיִת,</p> |
| **Target** | se il povero ha steso la sua mano dentro e ha messo nella mano del padrone di casa un recipiente affinché ci mettesse dentro un dono, |
| **LLM** | Il povero stende la mano in avanti e il padrone di casa gli mette qualcosa nella mano. |
| **LLM+TM** | Se il povero ha steso la sua mano dentro e ha messo nella mano del padrone di casa, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 8.3011 | 65.4985 | 689.03% |
| **BERTscore** | 0.7862 | 0.9007 | 14.56% |
| **MeteorScore** | 0.3174 | 0.7218 | 127.41% |

___



| **N. 22** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>פָּשַׁט בַּעַל הַבַּיִת אֶת יָדוֹ לַחוּץ וְנָתַן לְתוֹךְ יָדוֹ שֶׁל עָנִי,</p> |
| **Target** | Se il padrone di casa ha steso la sua mano fuori e ha messo nella mano del povero il dono, |
| **LLM** | Il padrone di casa stese la mano fuori e mise dentro la mano del povero. |
| **LLM+TM** | quando il padrone di casa ha steso la sua mano fuori e ha messo il dono nella cesta che era nella mano del povero, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 21.5188 | 62.0983 | 188.58% |
| **BERTscore** | 0.8489 | 0.9294 | 9.48% |
| **MeteorScore** | 0.5114 | 0.9308 | 82.01% |

___



| **N. 23** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אוֹ שֶׁנָּטַל מִתּוֹכָהּ וְהִכְנִיס</p> |
| **Target** | oppure il padrone di casa ha preso un recipiente (per metterci il dono) da essa (dalla mano del povero) e l’ha portato dentro, |
| **LLM** | O che ha preso da essa e vi ha introdotto |
| **LLM+TM** | oppure il povero ha preso il dono da essa e l’ha portato dentro |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 3.9936 | 13.8726 | 247.37% |
| **BERTscore** | 0.7043 | 0.8667 | 23.06% |
| **MeteorScore** | 0.1825 | 0.5095 | 179.18% |

___



| **N. 24** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אוֹ שֶׁנָּתַן לְתוֹכָהּ וְהוֹצִיא</p> |
| **Target** | oppure (il padrone di casa) ha messo il dono in essa (nella mano del povero) e (il povero) ha tirato fuori dalla casa la sua mano (che tiene il dono), |
| **LLM** | O che ha messo dentro di essa e ha fatto uscire |
| **LLM+TM** | oppure il povero ha messo in essa il recipiente e il padrone di casa lo ha portato fuori, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 2.5803 | 9.9309 | 284.87% |
| **BERTscore** | 0.7004 | 0.8284 | 18.28% |
| **MeteorScore** | 0.1325 | 0.3165 | 138.87% |

___



| **N. 25** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שְׁנֵיהֶם פְּטוּרִין.</p> |
| **Target** | sono ambedue esenti. |
| **LLM** | Entrambi sono esenti. |
| **LLM+TM** | Sono ambedue esenti. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 35.3553 | 100.0 | 182.84% |
| **BERTscore** | 0.8632 | 0.9386 | 8.73% |
| **MeteorScore** | 0.6389 | 0.9922 | 55.30% |

___



| **N. 26** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>פָּשַׁט בַּעַל הַבַּיִת אֶת יָדוֹ לַחוּץ וְנָטַל הֶעָנִי מִתּוֹכָהּ,</p> |
| **Target** | Se il padrone di casa ha steso la sua mano (che tiene il dono) fuori e il povero ha preso da essa il dono, |
| **LLM** | Il padrone di casa stese la mano verso l'esterno e il povero prese da essa. |
| **LLM+TM** | Il padrone di casa ha steso la sua mano fuori e il povero ha preso da essa il dono |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 14.7246 | 62.1852 | 322.32% |
| **BERTscore** | 0.7977 | 0.9136 | 14.53% |
| **MeteorScore** | 0.343 | 0.7238 | 111.02% |

___



| **N. 27** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אוֹ שֶׁנָּתַן לְתוֹכָהּ וְהִכְנִיס</p> |
| **Target** | oppure il povero ha messo in essa (nella mano del padrone di casa) il recipiente (affinché ci mettesse dentro il dono), e il padrone di casa ha riportato dentro la mano (con il recipiente), |
| **LLM** | O che ha messo dentro di essa e l'ha introdotta |
| **LLM+TM** | oppure il povero ha messo in essa il recipiente affinché il padrone di casa ci mettesse dentro il dono e quest’ultimo ha riportato dentro la mano con il recipiente, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 2.2987 | 40.6125 | 1666.76% |
| **BERTscore** | 0.664 | 0.8915 | 34.26% |
| **MeteorScore** | 0.0773 | 0.6823 | 782.66% |

___



| **N. 28** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שְׁנֵיהֶם פְּטוּרִין.</p> |
| **Target** | sono ambedue esenti. |
| **LLM** | Entrambi sono esenti. |
| **LLM+TM** | Sono ambedue esenti. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 35.3553 | 100.0 | 182.84% |
| **BERTscore** | 0.8632 | 0.9386 | 8.73% |
| **MeteorScore** | 0.6389 | 0.9922 | 55.30% |

___



| **N. 29** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מָבוֹי שֶׁהוּא גָּבוֹהַּ לְמַעְלָה מֵעֶשְׂרִים אַמָּה – יְמַעֵט,</p> |
| **Target** | La trave di un vicolo che è posizionata più in alto di venti braccia va abbassata. |
| **LLM** | Un ingresso che è alto più di venti cubiti, si riduce. |
| **LLM+TM** | La trave di un vicolo che è posizionata più in alto di venti braccia va abbassata, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 7.6924 | 93.5133 | 1115.66% |
| **BERTscore** | 0.7623 | 0.9629 | 26.32% |
| **MeteorScore** | 0.3803 | 0.9411 | 147.46% |

___



| **N. 30** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>רַבִּי יְהוּדָה אוֹמֵר: אֵינוֹ צָרִיךְ.</p> |
| **Target** | Rabbì Yehudà invece dice che non vi è bisogno di abbassarla. |
| **LLM** | Rabbi Yehudah dice: non è necessario. |
| **LLM+TM** | Rabbì Yehudà dice: Non vi è bisogno. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.7892 | 27.092 | 465.69% |
| **BERTscore** | 0.7908 | 0.886 | 12.04% |
| **MeteorScore** | 0.1724 | 0.641 | 271.81% |

___



| **N. 31** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וְהָרָחָב מֵעֶשֶׂר אַמּוֹת – יְמַעֵט.</p> |
| **Target** | Se la soglia del vicolo è più larga di dieci braccia va ristretta. |
| **LLM** | E il largo di dieci cubiti sarà diminuito. |
| **LLM+TM** | Se l’entrata del vicolo è più larga di dieci braccia va ristretta, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 6.2856 | 69.3098 | 1002.68% |
| **BERTscore** | 0.7383 | 0.8904 | 20.60% |
| **MeteorScore** | 0.1893 | 0.7778 | 310.88% |

___



| **N. 32** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>כָּל מָקוֹם שֶׁאֵין מַכְנִיסִין בּוֹ חָמֵץ –</p> |
| **Target** | Ogni posto in cui non si è soliti introdurre chamètz |
| **LLM** | Ogni luogo in cui non si introduce lievito |
| **LLM+TM** | Ogni posto dove non si è soliti introdurre chamètz |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 27.7762 | 58.1431 | 109.33% |
| **BERTscore** | 0.8109 | 0.9761 | 20.37% |
| **MeteorScore** | 0.4939 | 0.8018 | 62.34% |

___



| **N. 33** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אֵין צָרִיךְ בְּדִיקָה.</p> |
| **Target** | non è necessario controllarlo. |
| **LLM** | Non è necessario un esame. |
| **LLM+TM** | non è necessario controllarlo. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 34.9833 | 100.0 | 185.85% |
| **BERTscore** | 0.8423 | 1.0 | 18.72% |
| **MeteorScore** | 0.7353 | 0.996 | 35.45% |

___



| **N. 34** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>מָקוֹם שֶׁמַּכְנִיסִין בּוֹ חָמֵץ,</p> |
| **Target** | La regola vale soltanto in un posto in cui si è soliti introdurre chamètz. |
| **LLM** | Luogo in cui si introduce il lievito |
| **LLM+TM** | Posto in cui si è soliti introdurre chamètz |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 9.7824 | 47.5873 | 386.46% |
| **BERTscore** | 0.7315 | 0.8705 | 19.00% |
| **MeteorScore** | 0.2074 | 0.5589 | 169.48% |

___



| **N. 35** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בֵּית שַׁמַּאי אוֹמְרִים:</p> |
| **Target** | La Scuola di Shammài dice: |
| **LLM** | La scuola di Shammai dice: |
| **LLM+TM** | La Scuola di Shammài dice: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 37.9918 | 100.0 | 163.21% |
| **BERTscore** | 0.9386 | 1.0 | 6.54% |
| **MeteorScore** | 0.8067 | 0.9977 | 23.68% |

___



| **N. 36** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וּבֵית הִלֵּל אוֹמְרִים:</p> |
| **Target** | E la Scuola di Hillèl dice: |
| **LLM** | E la scuola di Hillel dice: |
| **LLM+TM** | La Scuola di Hillèl dice invece: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 48.8923 | 64.3459 | 31.61% |
| **BERTscore** | 0.9447 | 0.9397 | -0.53% |
| **MeteorScore** | 0.8413 | 0.8413 | 0.00% |

___



| **N. 37** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שְׁתֵּי שׁוּרוֹת הַחִיצוֹנוֹת,</p> |
| **Target** | Basta controllare soltanto le due file più esterne, |
| **LLM** | Le due file esterne |
| **LLM+TM** | le due file più esterne |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 19.0708 | 44.6324 | 134.04% |
| **BERTscore** | 0.801 | 0.8583 | 7.15% |
| **MeteorScore** | 0.4412 | 0.5791 | 31.26% |

___



| **N. 38** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שֶׁהֵן הָעֶלְיוֹנוֹת.</p> |
| **Target** | che sono quelle superiori. |
| **LLM** | Poiché essi sono i più alti. |
| **LLM+TM** | che sono le superiori |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 8.5153 | 23.6435 | 177.66% |
| **BERTscore** | 0.7211 | 0.8893 | 23.33% |
| **MeteorScore** | 0.1923 | 0.5215 | 171.19% |

___



| **N. 39** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בְּאֶחָד בְּנִיסָן — רֹאשׁ הַשָּׁנָה לַמְּלָכִים וְלָרְגָלִים.</p> |
| **Target** | Il primo di nisàn è il capodanno per i re e per le feste di pellegrinaggio. |
| **LLM** | Il primo di Nisan — è l'inizio dell'anno per i re e per le feste. |
| **LLM+TM** | Il primo di nisàn è il capodanno per i re e per le feste di pellegrinaggio. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 44.815 | 100.0 | 123.14% |
| **BERTscore** | 0.8464 | 1.0 | 18.15% |
| **MeteorScore** | 0.6657 | 0.9999 | 50.20% |

___



| **N. 40** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בְּאֶחָד בֶּאֱלוּל רֹאשׁ הַשָּׁנָה לְמַעְשַׂר בְּהֵמָה</p> |
| **Target** | Il primo di elùl è il capodanno per la decima del bestiame. |
| **LLM** | Nel primo giorno del mese di Elul è il capodanno per la decima parte del bestiame. |
| **LLM+TM** | Il primo di elùl è il capodanno per la decima del bestiame. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 37.4444 | 100.0 | 167.06% |
| **BERTscore** | 0.8726 | 1.0 | 14.60% |
| **MeteorScore** | 0.8012 | 0.9998 | 24.79% |

___



| **N. 41** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>רַבִּי אֶלְעָזָר וְרַבִּי שִׁמְעוֹן אוֹמְרִים: בְּאֶחָד בְּתִשְׁרֵי.</p> |
| **Target** | Rabbì Elazàre rabbì Shimòn dicono che il capodanno per la decima del bestiame è il primo di tishrì. |
| **LLM** | Rabbi El'azar e Rabbi Shimon dicono: il primo di Tishrei. |
| **LLM+TM** | Rabbì Elazàr e rabbì Shimòn dicono che il capodanno per la decima del bestiame è il primo di tishrì. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 8.5624 | 85.1916 | 894.95% |
| **BERTscore** | 0.7485 | 0.9702 | 29.62% |
| **MeteorScore** | 0.2437 | 0.9942 | 307.96% |

___



| **N. 42** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בֵּית הִלֵּל אוֹמְרִים: בַּחֲמִשָּׁה עָשָׂר בּוֹ</p> |
| **Target** | mentre la Scuola di Hillèl dice che il capodanno degli alberi è il 15 di shevàt. |
| **LLM** | Casa di Hillel dice: nel quindicesimo di esso |
| **LLM+TM** | La Scuola di Hillèl dice: nel quindici di esso |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 3.0098 | 22.4075 | 644.48% |
| **BERTscore** | 0.7309 | 0.7747 | 5.99% |
| **MeteorScore** | 0.0926 | 0.3613 | 290.17% |

___



| **N. 43** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שִׁבְעַת יָמִים קוֹדֶם יוֹם הַכִּפּוּרִים</p> |
| **Target** | Sette giorni prima di Yom Kippùr |
| **LLM** | Sette giorni prima del Giorno dell'Espiazione |
| **LLM+TM** | Sette giorni prima di Yom Kippùr |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 30.2138 | 100.0 | 230.97% |
| **BERTscore** | 0.7887 | 1.0 | 26.79% |
| **MeteorScore** | 0.4907 | 0.9977 | 103.32% |

___



| **N. 44** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וּמַתְקִינִין לוֹ כֹּהֵן אַחֵר תַּחְתָּיו,</p> |
| **Target** | e gli si prepara un altro sacerdote affinché possa prendere il suo posto |
| **LLM** | E gli stabiliscono un altro sacerdote al suo posto. |
| **LLM+TM** | E gli si prepara un altro sacerdote al suo posto. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 16.9006 | 52.0551 | 208.01% |
| **BERTscore** | 0.8066 | 0.8703 | 7.90% |
| **MeteorScore** | 0.5295 | 0.6993 | 32.07% |

___



| **N. 45** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שֶׁמָּא יֶאֱרַע בּוֹ פְּסוּל.</p> |
| **Target** | qualora gli capitasse (al primo) di trovarsi in una condizione invalidante causata ad esempio da una impurità. |
| **LLM** | Affinché non gli capiti nulla di male. |
| **LLM+TM** | poiché potrebbe capitargli un difetto invalidante |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 2.5198 | 1.9146 | -24.02% |
| **BERTscore** | 0.6997 | 0.758 | 8.33% |
| **MeteorScore** | 0.0798 | 0.0269 | -66.29% |

___



| **N. 46** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>רַבִּי יְהוּדָה אוֹמֵר:</p> |
| **Target** | Rabbì Yehudà dice: |
| **LLM** | Rabbi Yehudah dice: |
| **LLM+TM** | Rabbì Yehudà dice: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 31.9472 | 100.0 | 213.02% |
| **BERTscore** | 0.8483 | 1.0 | 17.88% |
| **MeteorScore** | 0.4688 | 0.9922 | 111.65% |

___



| **N. 47** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שֶׁנֶּאֱמַר</p> |
| **Target** | poiché è scritto: |
| **LLM** | che è stato detto |
| **LLM+TM** | come è detto: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 15.9736 | 18.9959 | 18.92% |
| **BERTscore** | 0.8256 | 0.8735 | 5.80% |
| **MeteorScore** | 0.125 | 0.25 | 100.00% |

___



| **N. 48** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>״וְכִפֶּר בַּעֲדוֹ וּבְעַד בֵּיתוֹ״</p> |
| **Target** | Ed espierà per se stesso e per la sua casa (Lev. 16:6): |
| **LLM** | E farà l'espiazione per sé e per la sua casa. |
| **LLM+TM** | Ed espierà per se stesso e per la sua casa |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 21.8698 | 51.1829 | 134.03% |
| **BERTscore** | 0.7751 | 0.8491 | 9.55% |
| **MeteorScore** | 0.4338 | 0.649 | 49.61% |

___



| **N. 49** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בֵּיתוֹ זוֹ אִשְׁתּוֹ.</p> |
| **Target** | con “la sua casa” s’intende sua moglie, e quindi è necessario che sia sposato. |
| **LLM** | Sua moglie è in casa. |
| **LLM+TM** | la sua casa è sua moglie |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 5.8166 | 5.8166 | 0.00% |
| **BERTscore** | 0.7088 | 0.7536 | 6.32% |
| **MeteorScore** | 0.2 | 0.3024 | 51.20% |

___



| **N. 50** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אָמְרוּ לוֹ:</p> |
| **Target** | Gli dissero: |
| **LLM** | Gli dissero: |
| **LLM+TM** | Gli dissero: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 100.0 | 100.0 | 0.00% |
| **BERTscore** | 1.0 | 1.0 | 0.00% |
| **MeteorScore** | 0.9815 | 0.9815 | 0.00% |

___



| **N. 51** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>אִם כֵּן אֵין לַדָּבָר סוֹף.</p> |
| **Target** | Se è così, la cosa non ha fine, perché allora dovrebbero preparargli una terza moglie se anche la seconda morisse. |
| **LLM** | Se così, allora la questione non ha fine. |
| **LLM+TM** | Se così fosse, la cosa non avrebbe fine. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 8.9276 | 12.2591 | 37.32% |
| **BERTscore** | 0.788 | 0.8021 | 1.79% |
| **MeteorScore** | 0.3172 | 0.2452 | -22.70% |

___



| **N. 52** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>סוּכָּה שֶׁהִיא גְּבוֹהָה לְמַעְלָה מֵעֶשְׂרִים אַמָּה – פְּסוּלָה,</p> |
| **Target** | Una sukkà (capanna) il cui sekhàkh (tetto) sia posizionato a un’altezza superiore alle venti ammòt (cubiti) non è valida; |
| **LLM** | Una succa che è alta più di venti cubiti è invalida. |
| **LLM+TM** | Una sukkà che abbia un’altezza maggiore di venti cubiti non è valida, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 2.0429 | 7.6047 | 272.25% |
| **BERTscore** | 0.6949 | 0.7627 | 9.76% |
| **MeteorScore** | 0.0758 | 0.3511 | 363.19% |

___



| **N. 53** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וְרַבִּי יְהוּדָה מַכְשִׁיר.</p> |
| **Target** | rabbì Yehudà invece la ritiene valida. |
| **LLM** | E Rabbi Yehudah macchia. |
| **LLM+TM** | mentre rabbì Yehudà la considera valida, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 6.5673 | 15.6197 | 137.84% |
| **BERTscore** | 0.701 | 0.8736 | 24.62% |
| **MeteorScore** | 0.0735 | 0.4509 | 513.47% |

___



| **N. 54** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בֵּיצָה <span class=“filtered“><span class=“filtered“>שֶׁנּוֹלְדָה</span></span> בְּיוֹם טוֹב,</p> |
| **Target** | Riguardo a un uovo che è stato deposto in un giorno di festa (Yom Tov), |
| **LLM** | un uovo nato in giorno di festa |
| **LLM+TM** | un uovo che è stato deposto in un giorno di festa |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 10.5215 | 57.3057 | 444.65% |
| **BERTscore** | 0.7868 | 0.8627 | 9.65% |
| **MeteorScore** | 0.3024 | 0.6356 | 110.19% |

___



| **N. 55** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>בֵּית שַׁמַּאי אוֹמְרִים:</p> |
| **Target** | la Scuola di Shammài dice: |
| **LLM** | La scuola di Shammai dice: |
| **LLM+TM** | La Scuola di Shammài dice: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 37.9918 | 100.0 | 163.21% |
| **BERTscore** | 0.9311 | 0.988 | 6.11% |
| **MeteorScore** | 0.8067 | 0.9977 | 23.68% |

___



| **N. 56** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>תֵּאָכֵל,</p> |
| **Target** | È permesso mangiarlo. |
| **LLM** | sarà mangiato |
| **LLM+TM** | che l’uovo potrà essere mangiato |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 0.0 | 0.0 | 0.00% |
| **BERTscore** | 0.7099 | 0.6792 | -4.32% |
| **MeteorScore** | 0.0 | 0.0 | 0.00% |

___



| **N. 57** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וּבֵית הִלֵּל אוֹמְרִים:</p> |
| **Target** | La Scuola di Hillèl dice invece: |
| **LLM** | E la scuola di Hillel dice: |
| **LLM+TM** | La Scuola di Hillèl dice invece: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 27.7762 | 100.0 | 260.02% |
| **BERTscore** | 0.8984 | 1.0 | 11.31% |
| **MeteorScore** | 0.6371 | 0.9985 | 56.73% |

___



| **N. 58** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>לֹא תֵּאָכֵל.</p> |
| **Target** | È proibito mangiarlo quello stesso giorno. |
| **LLM** | Non sarà mangiato. |
| **LLM+TM** | non potrà essere mangiato neanche nel giorno successivo, a causa della “regola di Rabbà”. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 6.5673 | 2.1591 | -67.12% |
| **BERTscore** | 0.7382 | 0.7317 | -0.88% |
| **MeteorScore** | 0.0746 | 0.1235 | 65.55% |

___



| **N. 59** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שְׂאוֹר בְּכַזַּיִת,</p> |
| **Target** | Il lievito (seòr) è proibito dalla Torà nella festa di Pèsach soltanto a partire dal volume di un’oliva, |
| **LLM** | Lievemente come l'olio d'oliva |
| **LLM+TM** | Il lievito è proibito a partire dal volume di un’oliva |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 0.0 | 27.6536 | inf% |
| **BERTscore** | 0.6813 | 0.8556 | 25.58% |
| **MeteorScore** | 0.0 | 0.5437 | inf% |

___



| **N. 60** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וְחָמֵץ בְּכַכּוֹתֶבֶת,</p> |
| **Target** | mentre un alimento lievitato (chamètz) è proibito dalla Torà soltanto a partire dal volume di un dattero. |
| **LLM** | e l'aceto nella scrittura |
| **LLM+TM** | e che un alimento lievitato è proibito a partire dal volume di un dattero, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 0.0 | 38.6396 | inf% |
| **BERTscore** | 0.654 | 0.8546 | 30.67% |
| **MeteorScore** | 0.0 | 0.6106 | inf% |

___



| **N. 61** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>וּבֵית הִלֵּל אוֹמְרִים:</p> |
| **Target** | La Scuola di Hillèl dice invece: |
| **LLM** | E la scuola di Hillel dice: |
| **LLM+TM** | La Scuola di Hillèl dice invece: |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 27.7762 | 100.0 | 260.02% |
| **BERTscore** | 0.8984 | 1.0 | 11.31% |
| **MeteorScore** | 0.6371 | 0.9985 | 56.73% |

___



| **N. 62** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>זֶה וָזֶה בְּכַזַּיִת.</p> |
| **Target** | Entrambi sono proibiti a partire dal volume di un’oliva. |
| **LLM** | Questo e quello nell'olio d'oliva. |
| **LLM+TM** | In questo caso e in quel caso, un kazàyit. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.1961 | 3.7968 | -9.52% |
| **BERTscore** | 0.7245 | 0.6671 | -7.92% |
| **MeteorScore** | 0.0439 | 0.084 | 91.34% |

___



| **N. 63** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>הַשּׁוֹחֵט חַיָּה וָעוֹף בְּיוֹם טוֹב,</p> |
| **Target** | Riguardo a colui che macella un animale selvatico o un volatile in un giorno di festa, |
| **LLM** | Colui che uccide un animale o un uccello nel giorno di festa. |
| **LLM+TM** | Colui che macella un animale selvatico o un volatile in un giorno di festa |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 14.088 | 80.5312 | 471.63% |
| **BERTscore** | 0.8345 | 0.921 | 10.37% |
| **MeteorScore** | 0.4618 | 0.8382 | 81.51% |

___



| **N. 64** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>לֹא יִשְׁחוֹט אֶלָּא אִם כֵּן הָיָה לוֹ עָפָר מוּכָן מִבְּעוֹד יוֹם.</p> |
| **Target** | Non potrà macellare se non nel caso in cui abbia già del terriccio pronto dalla vigilia della festa (lett. “da quando era ancora giorno”). |
| **LLM** | Non si macellerà se non se ha avuto polvere preparata fin dal giorno prima. |
| **LLM+TM** | Non potrà macellare se non nel caso in cui abbia già del terriccio pronto dalla vigilia della festa. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 3.176 | 63.0224 | 1884.33% |
| **BERTscore** | 0.74 | 0.9323 | 25.99% |
| **MeteorScore** | 0.0877 | 0.6571 | 649.26% |

___



| **N. 65** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שֶׁיַּחְפּוֹר בְּדֶקֶר וִיכַסֶּה,</p> |
| **Target** | scavi con una zappa e ricopra il sangue, |
| **LLM** | Che scavi nella polvere e lo copra. |
| **LLM+TM** | scavi con la zappa e ricopra il sangue, |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 5.6698 | 66.0633 | 1065.18% |
| **BERTscore** | 0.7587 | 0.9781 | 28.92% |
| **MeteorScore** | 0.1124 | 0.8819 | 684.61% |

___



| **N. 66** | Content | 
| --- | --- |
| **Source** | <p style='direction:rtl; text-align: right'>שֶׁאֵפֶר כִּירָה מוּכָן הוּא.</p> |
| **Target** | infatti la cenere della stufa è riservata a un uso consentito nel giorno di festa e quindi è permesso utilizzarla. |
| **LLM** | Poiché la cenere è pronta come un focolare. |
| **LLM+TM** | Infatti la cenere della stufa è riservata a un uso consentito nel giorno di festa e quindi è permesso utilizzarla. |

                  
|| LLM | LLM+TM | Delta |
| ------------- | ------------- | ------------- | ------------- |
| **SacreBLEU** | 4.5672 | 100.0 | 2089.53% |
| **BERTscore** | 0.7344 | 0.9927 | 35.17% |
| **MeteorScore** | 0.1879 | 0.9999 | 432.14% |

___

