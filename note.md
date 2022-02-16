# Italian Note version:

Gli script sono nati principalmente per i seguenti motivi:

- ero stufo di utilizzare app o sito ufficiale perchè pieni di traccianti, social, ecc.. che ledono la privacy del consumatore, e che coattamente  ti obbligano ad accettare, un qualcosa che reputo inverosimile, visto che il servizio pubblico di informazione rai è finanziato  dal  canone.

- il podcast non utilizza il formato aperto rss xml per la sua fruizione libera, ma un formato proprietario, l'app! costringendoti ad utilizzarla per forza per compatibilità tecnica.

- sito e app fanno un uso pesante di javascript e chissà cos'altro..  sprecano le risorse del pc-telefono inutilmente, questo comporta che spesso il browser o l'app si blocchi. Nei mie sistemi di mia proprieta (pc- telefono) ho il diritto di decidere in che modo un sito remoto  (in questo caso il sito rai) possa eseguire codice sulla mia macchina. 
I controlli del player web non funzionano su tutti i sistemi.... potrei continuare all'infinito..

- troppa publicità, visto che è un servizio pubblico  finanziato dal canone tv. Mi obbligano ad iscrivermi a facebook, per fruire dei contenuti...

- dover "acquistare" pc gaming o un telefono "gaming "per poter ascolatare un podcast è stupido... da indiscrezioni di amici pare che l'hardware citato potrebbe essere insufficente a fruire dei servizi rai!

- utilizzando un raspberry pi, cron, gli script citati e [syncthing](https://syncthing.net/) (o un altro programma di sincronizzazione concorrente, cloud e non) sincronizzo i podcast scaricati in automatico in tutti i miei dispositivi, risparmiando banda dati mobile quando sono fuori casa perchè l'audio è compresso. Posso ascoltare i podcast con un telefono vecchio di un decennio fa!

- Il poscast così come è codificato spreca troppa banda dati mobile in caso di fruizione da mobile.

- il podcast fruito tramite server raspberry pi, script e synctyng permette un risparmio di banda dati mobile di 5, 6 volte.


## alcune informazioni tecniche:

### note valide fino alla V:1.0 dello script, valide fino ad settembre 2021

i podcast  del gr 1,2,3 sono  mp3 stereo con campionamento a 48KhZ e bitrate a 256KBps (alta qualità, file grandi) mediamente per il gr1 dai 20 minuti in su, siamo intorno ai 45 MB o superiore come peso per singolo file...

 Ricodificandoli in opus ho file che pesano 12MB circa, qualità audio invariata, su rete mobile quando li sincronizzo, risparmio 4 volte la banda dati che normalmente dovrei usare, e non è poco.

Per chi volesse nello script è possibile codificare in aac  basta commentare o deccommentare le ultime righe del codice.

Si può disabilitare del tutto la codifica commentando con # le righe da 70 a 72

Negli script del GRR regionale il bit rate in mp3 varia da 96 a 128 kbps quindi i file sono relativamente piccoli e negli script per ora, non è prevista la ricodifica in opus o aac dei file.


### note tecniche valide dalla V2.0 dello script, da Dicembre 2021


I podcast principali gr1,2,3 sono ora dei file mp3 stereo con campionamentoa 48KHz e bitrate 320Kbps (in qualche caso sporadico sono a 256Kbps) quindi i file del podcast sono ancora più grandi basti pensare che 10 minuti di podcast sono circa 25MB, l'edizione da circa 22 minuti del gr1 della mattina adesso pesa circa 50-55MB a puntata. Alcune volte tocca anche la soglia dei 60MB.. potete ben capire su connessione mobile quanta banda dati fa sprecare.. Manco fosse un podcast per veri audiofili, per avere tutta questa qualità.

Ovviamete lo script (di defoult v1.0 e v2.0) ricodifica in opus, audio stereo a circa 64kbps vbr mode (bitrate medio di circa 72kbps) con file di circa 10-13 MB.

Per chi volesse, adesso  che, il bit-rate sorgente non manca, potrebbe impostare gli script con delle codifiche ancora più incisive per ridurre ancora di più il peso dei file senza rinunciare la qualità audio. Una tecnica semplice è quella di rinunciare all' audio stereofonico per avere delle codifiche ancore più spinte (bitrate più contenuti) ove l'algoritmo di compressione lo supporti. Per questo motivo ho inserito nello script in maniera commentata (#) i comandi ffmpeg per fare ciò, basta attivare quello desiderato, e commentare quello di default.
Li trovate nelle ultime righe dello script se presenti.

## Tipi di codifica opzionali:

Come accennato prima è possibile utilizzare dei formati di codifica opzionali rispetto a quello di default, vediamoli nel dettaglio:

NB: negli esempi **grX** può essere (gr1,gr2,gr_ecc)

### opus 
per chi volesse risparmiare ancora più banda di sincronizzazione e avere file ancora più piccoli può usare opus in mono canale con bitrate compresi tra 32-56 Kbps, un buon compromesso tra qualità e dimensione è tra 40-48 Kbps quest'ultima configurazione sarà attivata di defoult negli script che presentano una nomeclatura >= V2.1.1

```

ffmpeg -n -i grX_"$Data"_"$Ora".mp3 -vn -acodec libopus -ab 48k -ac 1 grX_"$Data"_"$Ora".opus

```

### ogg (Vorbis)

per sistemi che non supportano la codifica opus nativa, (tipo melafonino) o vecchi sistemi, vecchi player audio (in vecchi telefoni.. ecc) è possibile qualora supportino il Vorbis (tutti sistemi android) codificare in questo formato. Per mantenere un buon rapporto tra qualità audio e dimensione file ho scelto dopo vari test questa condizione di codifica che reputo ottimale,  il file così codificato è in mono, con un bitrate medio di circa 60kbps.

```
ffmpeg -n -i grX_"$Data"_"$Ora".mp3 -vn -acodec libvorbis -aq 0 -ac 1 grX_"$Data"_"$Ora".ogg

```
per utilizzarlo decommentare il codice sopra citato nello script e commentare la codifica di default.

### aac (advance audio codec)

codifica mono canale con bitrate fisso a 64kbps, Utilizando il codificatore aac fatto in casa da ffmpeg vers 3 o superiore (supporta solo lo standard AAC LC (Low Complexity)) questo perchè non sempre il codificatore fdk è presente nel sistema. Questo formato è supportato dai device super costosi con il logo di un frutto. E' supportato in tutti i device android.

```
ffmpeg -n -i grX_"$Data"_"$Ora".mp3 -vn -acodec aac -ab 64k -ac 1 grX_"$Data"_"$Ora".m4a
```

per utilizzarlo decommentare il codice sopra citato nello script e commentare la codifica di default.

### mp3

Per chi non volesse abbandonare il collaudato ma meno performate mp3, il quale funziona persino nei tostapane smart, o nei frullatori, può ricodificare in mp3 con audio mono ad un bitrate più basso (96 kbps mono) rispetto a quello proposto rai. Ance se produrà dei file leggermente più alti rispetto ai codec smart. Questo escamotage permette una qualità audio mono paragonabile a una fruizione stereo di 192kbps in mp3 (visto che l'ultimo qui citato, lo stereo a 192kbps utilizza 96kbps per codificare ogni traccia stereo).. Lo reputo un buon compromesso.

Nota bene : il alcuni player del coso morsicato è presente un bug il quale non supporta il formato mono nell'mp3, non rompete è usate acc.

```
ffmpeg -n -i grX_"$Data"_"$Ora".mp3 -vn -acodec libmp3lame -ab 96k -ac 1 grX_"$Data"_"$Ora".mp3
```
per utilizzarlo decommentare il codice sopra citato nello script e commentare la codifica di default.


## licenze sui formati e codificatori

per questione etica io propongo di utilizzare formati aperti e privi di royality come o**gg(vorbis) o opus**.

Vi ricordo che i brevetti sull'**mp3** sono scaduti nel 2017 (quindi un altra alternativa etica)

**aac** è coperto da svariati brevetti; i  produttori di chip, di software, di dispositivi, i consumatori finali ecc.. pagano royality direttamente o indirettamente al consorzio che ne detiene i diritti.

 Dal punto di vista etico possibilmente sarebbe da evitare per promuovere servizi liberi, ma visto che direttamente o indirettamente io fruiture finale di un dispositivo, insieme al dispositivo stesso al momento dell'acquisto ho pagato anche le royality di licenza duso per tali formati, quindi:  **lo usi**. 
 
Perche tra televisore, decoder, telefono, tostapane, frullatore smart, frigo domotico, citofono con internet delle cose.. ecc..  sti signori hanno fatto di fatto, tanti soldini, anche dai miei soldini visto tutto il materiale tecnologico presente in casa che usa tale tecnologia,  e quindi...

***permettetemi di usarlo e di codificare in santa pace!***

---

## Cambio api e app: rainews24, raiplay sound

### Dicembre 2021

l'api è cambiata del tutto, siamo passati da raiplay a raiplaysound, o sistemato momentaneamente gli script con la v2 beta.

### 12 gennaio 2022

l'api legacy di rainews 24 (dove si reperiscono i grr regionali) del sito e dell' app è stata deprecata, da browser non è più possibile avere accesso diretto  alla nuova api per mancanza dei permessi, (se teoricamente è fattibile, in pratica è una rogna assurda per le complessità dell'ingegneria inversa da fare su app o sito e sullo script) adesso i dati json dell'api e dei relinker sono integrati nell'html della pagina, volutamente è stato fatto in modo tale, che anche se si estrapolano con un phaser json, il jason non è conforme e non può essere elaborato, infatti buona parte del nuovo javascript dellla pagina e del player multimediale ora hanno delle lunghe funzioni  per la rielaborazione dei dati json malformattati apposta,  per riformattarli in maniera corretta prima di essere passati al player. Un altro dei tentativi di mamma rai di offuscare i sorgenti del podcast.

Costruire un phaser in bash per recuperare il jason dall'html e riformattarlo non è fattibile per le mie attuali conoscenze, anche perchè le modifiche di mamma rai ultimamente sono all'ordine del giorno, e starci sopra 24 ore al giorno,  non è fattibile. In oltre tra regione e regione ci sono chiamate api diverse, come se non bastasse.

NB: alcune funzioni dell' api legacy continuano a funzionare.. (fino a quando?) la parte essenziale dei relinker da errore 404. 

Quindi  gli script regionali sono momentaneamente in sospeso di manutenzione, finchè non trovo qualcosa di fattibile.

### 12 Febbraio 2022

fix sperimentale errore 404 dell' api legacy, in fase di test nello script grr sardegna, in caso di stabilità, esporto a tempo debito ad altre grr regionali

### Note sulla versione: V2.1 alpha

in questa versione è stato aggiunto lo script **raipodcast-dl** che è uno script generico che serve a scaricare il singolo episodio di un podcast dandoli in pasto (input) il link della pagina html del singolo episodio, funziona bene con gli audio-book di "ad alta voce" sia con le normali puntate di tutti gli altri podcast, utilizza l' api level 2, in caso di bisogno tenta di utilizzare in automatico l'api legacy, per i vecchi podcast, è ancora in fase alpha, quindi non è esente da bug o possibili malfunzionamenti.

```
use: raipodcast-dl [link episode]
```

per fare un esempio pratico del suo uso uso ipotizziamo che voglia scaricare la "rassegna stampa del 16 febbraio 2022", mi reco con il browser allindirizzo: https://www.raiplaysound.it/programmi/radio3mondo e cerco il link di quel episodio, che nel mio caso è
https://www.raiplaysound.it/audio/2022/02/Radio3-Mondo-del-16022022-3347dde9-bba2-403a-9a90-eb6a2b2ffe99.html

per usare lo script do un:

```

raipodcast-dl "https://www.raiplaysound.it/audio/2022/02/Radio3-Mondo-del-16022022-3347dde9-bba2-403a-9a90-eb6a2b2ffe99.html"


```

