## Italian Note version:

Gli script sono nati principalmente per i seguenti motivi:

- ero stufo di utilizzare app o sito ufficiale perchè pieni di traccianti

- il podcast non utilizza il formato rss xml per la sua fruizione ma un formato proprietario, l'app!

- sito e app fanno un uso pesante di javascript e chissà cos'altro..  sprecano le risorse del pc inutilmente, questo comporta che spesso il browser o l'app si blocchi. I controlli del player web non funzionano su tutti i sistemi.... potrei continuare all'infinito..

- troppa publicità, visto che è un servizio pubblico  finanziato dal canone tv. Mi obbligano ad iscrivermi a facebook, per fruire dei contenuti...

- dover "acquistare" pc gaming o un telefono "gaming "per poter ascolatare un podcast è stupido... da indiscrezioni di amici pare che l'hardware citato potrebbe essere insufficente a fruire dei servizi rai!

- utilizzando un raspberry pi, cron, gli script citati e [syncthing](https://syncthing.net/) sincronizzo i podcast scaricati in automatico in tutti i miei dispositivi, risparmiando banda dati mobile quando sono fuori casa perchè l'audio è compresso. Posso ascoltare i podcast con un telefono vecchio di un decennio fa!


### alcune info tecniche

i podcast sono  mp3 stereo con campionamento a 48KhZ e bitrate a 256KBps (alta qualità, file grandi) mediamente per il gr1 dai 20 minuti in su, siamo intorno ai 45 MB o superiore come peso per singolo file...

 Ricodificandoli in opus ho file che pesano 12MB circa, qualità audio invariata, su rete mobile quando li sincronizo, risparmio 4 volte la banda dati che normalmente dovrei usare, e non è poco.

Per chi volesse nello script è possibile codificare in aac  basta commentare o deccommentare le ultime righe del codice.

Si può disabilitare del tutto la codifica commentando con # le righe da 70 a 72


