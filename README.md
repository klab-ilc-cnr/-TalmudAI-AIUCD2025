# TalmudAI-AIUCD2025

# Introduction
This page presents the interactions conducted with the LLM llama-3.1-8b, both in direct interactions and within the context of its use in the extended RAG architecture that was tested. The prompts and the answers are provided in Italian, as the experiment involved natural language querying of the Italian translation of the Babylonian Talmud.
# Querying the LLMs Directly
## The prompt
    Che differenze ci sono tra Shetuqìm e Asufìm? E a uno Shetuqì o un Asufì con chi era permesso sposarsi?
## The Answer from Llama
Mi dispiace, ma non riesco a fornire informazioni su "shetuqìm" e "asufìm". È possibile che si tratti di termini utilizzati in contesti culturali o linguistici specifici che non sono noti a me. Se hai altre domande o se c\'è qualcos\'altro con cui posso aiutarti, sarò felice di provare ad aiutarti.
# Querying the Extended RAG System
## The Query
Che differenze ci sono tra Shetuqìm e Asufìm? E a uno Shetuqì o un Asufì con chi era permesso sposarsi?
## The Prompt
    Sei un esperto di Talmud babilonese al quale viene posta una DOMANDA. 
    Per rispondere utilizza esclusivamente CONTESTO e GLOSSARI forniti, ma non inventare. 
    Dopo la risposta stampa l'elenco dei contesti forniti nel formato (pagina, contenuto) dove la pagina è presa dai metadati e il contenuto dal page_content.
    Successivamente stampa l'elenco dei glossari forniti nel formato (pagina, contenuto) dove la pagina è presa dai metadati e il contenuto dal page_content.
            
    DOMANDA: {quest}
    CONTESTO: {context}
    GLOSSARI: {glossaries}
    Risposta:
## The Answer from RAG Using Llama Without Glossaries
Gli shetuqìm sono coloro che conoscono l'identità della madre ma non quella del padre, mentre gli asufìm sono i trovatelli che non conoscono né l'identità del padre né quella della madre.

Secondo il contesto fornito, uno shetuqì (un uomo che conosce l'identità della madre ma non quella del padre) non dovrebbe essere permesso di sposare la figlia di una shetuqìt (una donna che conosce l'identità del padre ma non quella della madre), per evitare che si sposi con sua sorella da parte di padre.

Inoltre, il contesto suggerisce che anche uno shetuqì non dovrebbe essere permesso di sposare una shetuqìt, al fine di evitare che si sposi con sua sorella da parte di padre.

Ecco l'elenco dei contesti forniti:

1. (pagina 69a, contenuto: "Questi sono gli shetuqìm: chi conosce l’identità di sua madre, ma non conosce l’identità di suo padre.")
2. (pagina 73a, contenuto: "Almeno non dovrebbero permettere a uno shetuqì di sposare la figlia di una shetuqìt, per evitare che si sposi con sua sorella da parte di padre!")
3. (pagina 73a, contenuto: "Se è così, di conseguenza, non dovrebbero permettere neanche a uno shetuqì di sposare una shetuqìt, affinché non si sposi con sua sorella da parte di padre.")
4. (pagina 73a, contenuto: "Cosa potresti dire invece per squalificare il figlio? Forse potresti dire che è lei a essere andata da uno di loro a coabitare.")
## The Answer from RAG Using Llama with Glossaries
Sembra che tu stia cercando di comprendere le differenze tra shetuqìm e asufìm, due tipi di persone con identità incerta.

Secondo il contesto fornito, gli shetuqìm sono coloro che conoscono l'identità della madre ma non quella del padre. Gli asufìm, invece, sono bambini trovati per strada e non si conoscono né i genitori.

Inoltre, il glossario fornisce ulteriori informazioni su questi due tipi di persone:

*   Shetuqì: "Lett. “azzittito”, “messo a tacere”. È uno dei dieci tipi di lignaggio: si tratta di una persona di identità incerta, di cui si conosce la madre ma non il padre."
*   Asufì: "Pl. asufìm. È un bambino trovato per strada del quale non si conoscono i genitori."

In base a questi contesti e glossari, possiamo dire che gli shetuqìm sono persone che hanno una madre conosciuta ma non un padre, mentre gli asufìm sono bambini trovati per strada senza alcuna informazione sui loro genitori.

Quanto ai matrimoni, il contesto fornisce alcune informazioni interessanti:

*   Non dovrebbero permettere a uno shetuqì di sposare la figlia di una shetuqìt, per evitare che si sposi con sua sorella da parte di padre!
*   Non dovrebbero permettere neanche a uno shetuqì di sposare una shetuqìt, affinché non si sposi con sua sorella da parte di padre.

In sintesi, gli shetuqìm sono persone che hanno una madre conosciuta ma non un padre, mentre gli asufìm sono bambini trovati per strada senza alcuna informazione sui loro genitori. I matrimoni tra questi due tipi di persone sono soggetti a limitazioni e restrizioni.

**Contesti forniti:**

1.  (69a) "Questi sono gli shetuqìm: chi conosce l’identità di sua madre, ma non conosce l’identità di suo padre. E questi sono gli asufìm (trovatelli): chi è stato preso dalla strada e non conosce l’identità né di suo padre né di sua madre. Abbà Shaùl chiamava gli shetuqìm: beduqìm."
2.  (73a) "Almeno non dovrebbero permettere a uno shetuqì di sposare la figlia di una shetuqìt, per evitare che si sposi con sua sorella da parte di padre!"
3.  (73a) "Se è così, di conseguenza, non dovrebbero permettere neanche a uno shetuqì di sposare una shetuqìt, affinché non si sposi con sua sorella da parte di padre."
4.  (73a) "Cosa potresti dire invece per squalificare il figlio? Forse potresti dire che è lei a essere andata da uno di loro a coabitare. Questo significa che il padre era fisso a casa sua quando hanno generato il bambino, e la regola afferma che qualsiasi cosa fissa che non si separa, è considerata come se fosse al cinquanta percento (kol qavùa‘ kemechetzà ‘al mechetzà damè)."

**Glossari forniti:**

1.  Nome: Shetuqì
    Descrizione: Lett. “azzittito”, “messo a tacere”. È uno dei dieci tipi di lignaggio: si tratta di una persona di identità incerta, di cui si conosce la madre ma non il padre.
2.  Nome: Asufì
    Descrizione: Pl. asufìm. È un bambino trovato per strada del quale non si conoscono i genitori.
3.  Nome: Natìn-netinà
    Descrizione: I netinìm sono discendenti dei Ghiv‘onìm (Gabaoniti). Dal racconto di Gios. 9 i Ghiv‘onìm erano una popolazione indigena di Canaan aggregatasi al popolo ebraico con un sotterfugio. Giosuè si impegnò con un patto a non espellerli, ma assegnò loro lavori umili (Gios. 9:27). In TB, Yevamòt 78b è riportato che il re David emise un decreto perché rimanessero una classe separata proibendo loro di sposarsi con ebrei.