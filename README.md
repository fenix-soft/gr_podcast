# gr_podcast

## Italian: Read Me version

**gr_podcast** è una raccolta di script bash che consente all'utente, di recuperare in maniera agevole, gli ultimi episodi inseriti del podcast del radio giornale rai  '**gr**' .. e  all'occorenza una volta scaricati, ricodificarli in formato **opus** o "**aac**" (audio codec) per risparmiare spazio di archiviazione, vedi [note.md](note.md) 




La raccolta prevede al momento, gli script per il:  **gr1**, **gr2**, **gr3**,  del giornale radio nazionale

La raccolta attualmente prevede, gli scripr del *grr regionale*: **Lazio**, **Lombardia**


## dipendenze:

curl

[jq](https://stedolan.github.io/jq/)

cat

wget

ffmpeg  (usato per la codifica opus o aac)

### uso:
impostare i permessi di esecuzione per ogni script (chmod +x "nome_script”), **aprire un terminale nella cartella di lavoro degli script** e avviare quello che vi interessa

### esempio:
scaricare  l'ultimo podcast del gr1, esegui 

    ./gr1 

se vuoi invece integrare lo script nel sistema, per poterlo lanciare in qualisiasi posizione il terminale si trovi,  modifica il tuo file **.bashrc** e aggiungi un percorso per lo script  directory personalizzato.

#### esempio modifica integrazione di file .bashrc

    export PATH = $ PATH: "path  directory script"

ora bash dovrebbe vedere lo script. In alcuni casi potrebbe essere necesssario riavviare la sessione.. o il sistema..

per eseguirlo dare per esempio

    gr1
    
buon ascolto!

---

## English: Read Me version

**gr_podcast** is a collection of bash scripts that allows the user to easily retrieve the latest episodes included in the podcast of the radio newspaper rai '**gr**' .. and if necessary, once downloaded, recode them in **opus** or "**aac**" format (audio codec) to save storage space, see [note.md](note.md) 

The collection currently includes scripts for: gr1, gr2, gr3

### dependency script:

curl

[jq](https://stedolan.github.io/jq/)

cat

wget

ffmpeg (used for opus or aac encoding)

### use:

set the execution permissions for each script (chmod + x "script_name"), open a terminal in the script workbook and start the one you need

example:

download the latest gr1 podcast, run

    ./gr1
    
if you want to integrate the script into the system instead, to be able to run it wherever the terminal is, edit your .bashrc file and add a path to the custom script directory.

### example change integration of .bashrc file

    export PATH = $ PATH: "path directory script"

bash should now see the script. In some cases it may be necessary to restart the session .. or the system ..

to execute it give for example

    gr1
    
good listening!