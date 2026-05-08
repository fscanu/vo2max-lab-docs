---
layout: page
title: Privacy Policy (Italiano)
permalink: /privacy-policy-it/
---

**App:** VO2max Lab (`com.fescacomit.vo2maxlab`)
**Sviluppatore:** FESCACOM IT (Federico Scanu)
**Contatto:** [scanufe@fescacomit.com](mailto:scanufe@fescacomit.com)
**Ultimo aggiornamento:** 08/05/2026
**Data di efficacia:** 08/05/2026

# Informativa sulla Privacy

> Versione italiana. La versione di riferimento legale e' quella inglese, disponibile su [/privacy-policy/](../privacy-policy/). In caso di discrepanze prevale il testo inglese.

## In breve

VO2max Lab e' un'app Android local-first. Non gestiamo alcun server. Non raccogliamo, non trasmettiamo, non condividiamo, non vendiamo i tuoi dati personali. Tutto quello che registri (frequenza cardiaca, tracce GPS, velocita' del tapis roulant, storico degli allenamenti, dati del profilo) resta sul tuo dispositivo. L'unico traffico di rete generato dall'app sono le richieste a OpenFreeMap per scaricare le tile della mappa che vedi durante gli allenamenti outdoor. Disinstallando l'app cancelli ogni dato che ti riguarda, perche' non ne abbiamo mai conservato uno.

Se leggi una sola sezione, leggi questa.

---

## 1. Chi siamo

VO2max Lab e' pubblicata da **FESCACOM IT**, ditta individuale di Federico Scanu (Italia). Non c'e' un team, non c'e' una capogruppo, non c'e' un editore terzo. Domande, reclami, richieste in materia di dati: **scanufe@fescacomit.com**.

Il nome del pacchetto sul Google Play Store e' `com.fescacomit.vo2maxlab`. Se vedi un'altra app che si dichiara VO2max Lab con un nome di pacchetto diverso, non e' nostra.

---

## 2. Ambito dell'informativa

La presente informativa si applica:

- All'app Android **VO2max Lab** distribuita tramite Google Play e tramite eventuali canali APK diretti che controlliamo;
- Al sito statico GitHub Pages all'indirizzo `https://fscanu.github.io/vo2max-lab/` che ospita questa informativa.

**Non** copre:

- Altre app che usi insieme a VO2max Lab (Health Connect, l'app del produttore del tuo tapis roulant Bluetooth, app di mappe);
- Servizi a cui rimandiamo con link (la pagina del repository GitHub, le impostazioni di sistema del tuo dispositivo, la pagina Google Play).

Per il trattamento dei dati su tali servizi consulta le rispettive informative.

---

## 3. Dati trattati

VO2max Lab tratta le seguenti categorie di dati **esclusivamente sul tuo dispositivo**.

### 3.1 Dati di profilo

Inserisci peso, altezza, eta', sesso biologico, frequenza cardiaca a riposo (opzionale), frequenza cardiaca massima (opzionale), nome del profilo. L'app supporta piu' profili sullo stesso dispositivo per famiglie o coach.

- **Memorizzazione:** database Room locale (SQLite) nello storage privato dell'app. Le altre app non possono leggerlo senza root.
- **Uso:** stima del V̇O2max (formula di Cooper, stimatore non-exercise Aspenes 2011), calcolo della frequenza cardiaca massima (Tanaka), confronti per fasce d'eta'.
- **Trasmissione fuori dal dispositivo:** nessuna.
- **Conservazione:** finche' non elimini il profilo dall'app o disinstalli l'app.

### 3.2 Frequenza cardiaca

I campioni di frequenza cardiaca provengono da Health Connect (permesso `android.permission.health.READ_HEART_RATE`) oppure, su Android 13 e precedenti, dalla deprecata API Body Sensors (`android.permission.BODY_SENSORS`) quando nessuna sorgente Health Connect e' disponibile.

- **Memorizzazione:** database Room locale, associata a ciascun allenamento Cooper o 4x4 completato.
- **Uso:** visualizzazione FC in tempo reale durante l'allenamento, calcolo media e picco nel riepilogo, analisi delle zone di allenamento.
- **Trasmissione fuori dal dispositivo:** nessuna.
- **Health Connect:** leggiamo soltanto la frequenza cardiaca. Health Connect resta la fonte autoritativa e puoi revocare il nostro accesso in qualsiasi momento dalle impostazioni di Health Connect.

### 3.3 Letture V̇O2max (lettura e scrittura)

Dichiariamo due permessi Health Connect per il V̇O2max: `READ_VO2_MAX` per mostrare i risultati storici e `WRITE_VO2_MAX` per riscrivere il risultato di ciascun test Cooper o 4x4 in Health Connect, **sul tuo dispositivo**, in modo che altre app per la salute che usi possano vederlo.

- **Memorizzazione:** Health Connect (gestita dall'app Health Connect di Google, in locale) e database Room nostro per il riepilogo dell'allenamento.
- **Trasmissione fuori dal dispositivo:** nessuna. Health Connect e' una piattaforma di scambio dati on-device; i dati non lasciano il telefono salvo che **tu** autorizzi un'app terza dentro Health Connect a sincronizzarli.

### 3.4 Sessioni di esercizio e distanza (lettura Health Connect)

I permessi `READ_EXERCISE` e `READ_DISTANCE` consentono all'app di mostrare allenamenti esterni (per esempio una corsa outdoor registrata da un'altra app fitness) quando scegli di associarli a un ricalcolo dell'eta' di fitness. Non scriviamo mai sessioni di esercizio.

- **Uso:** sola lettura nello schermo dello storico.
- **Trasmissione fuori dal dispositivo:** nessuna.

### 3.5 Posizione GPS

Il GPS viene usato **solo** durante due attivita' specifiche:

- **Test di Cooper, modalita' outdoor** (`Fase D WS4`): il FusedLocationProvider campiona la posizione ogni ~3 secondi per 12 minuti per calcolare la distanza percorsa.
- **Test 4x4 norvegese, modalita' outdoor** (`Fase H WS-H3`): lo stesso provider campiona durante i quattro intervalli ad alta intensita' e i tre recuperi attivi (~43 minuti totali).

Permessi coinvolti: `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION`, `FOREGROUND_SERVICE`, `FOREGROUND_SERVICE_LOCATION`.

- **Accesso in background:** **nessuno.** Il campionamento si interrompe quando l'allenamento termina, premi Stop o il foreground service viene chiuso.
- **Geofencing o riconoscimento attivita':** **nessuno.**
- **Memorizzazione:** il percorso e' salvato come elenco di punti `(latitudine, longitudine, accuratezza)` con timestamp nel database Room locale, allegato al singolo allenamento.
- **Trasmissione fuori dal dispositivo:** nessuna. Non eseguiamo reverse-geocoding, non interroghiamo POI, non comunichiamo a nessun server dove ti trovi.
- **Tile della mappa:** il rendering del percorso richiede di scaricare le tile da OpenFreeMap (vedi sezione 4). L'URL della tile contiene le coordinate della tile, non le tue coordinate GPS esatte, ma rivela comunque alla CDN di OpenFreeMap l'area approssimativa che stai consultando.

### 3.6 Bluetooth (tapis roulant BT FTMS)

Permessi `BLUETOOTH_SCAN` (con flag `neverForLocation`), `BLUETOOTH_CONNECT` e, su Android 11 e precedenti, i legacy `BLUETOOTH` e `BLUETOOTH_ADMIN`.

- **Uso:** scoprire e connettersi a un tapis roulant compatibile Fitness Machine Service (FTMS, service UUID standard `0x1826`). Durante l'allenamento leggiamo la distanza totale e la velocita' istantanea riportate dal tapis e, soltanto per il test 4x4 (`Fase M WS-M1`), inviamo comandi di scrittura della velocita' target affinche' il tapis si regoli automaticamente fra intervalli e recuperi.
- **Memorizzazione:** il log di velocita' del tapis e' salvato in locale in Room come parte del record di allenamento. **Non** salviamo, non logghiamo e non trasmettiamo l'indirizzo MAC o l'identificativo del dispositivo fuori dal telefono.
- **Trasmissione fuori dal dispositivo:** nessuna.
- **Flag `neverForLocation`:** dichiarato affinche' Android non deduca la posizione dagli scan BLE. Non usiamo davvero il BLE per la localizzazione.

### 3.7 Notifiche del foreground service

Il permesso `POST_NOTIFICATIONS` e' richiesto da Android 13 (API 33) in poi per mostrare la notifica persistente che mantiene attivo il foreground service del timer di allenamento mentre lo schermo e' spento.

- **Uso:** mostrare il countdown dell'allenamento perche' il sistema operativo non termini il servizio a meta' test.
- **Dati personali nelle notifiche:** soltanto tipo di allenamento e tempo residuo.

### 3.8 Vibrazione

Il permesso `VIBRATE` fornisce feedback aptico ai cambi di fase (inizio intervallo, inizio recupero, fine test). Nessuna implicazione sui dati.

### 3.9 Stato della rete

Il permesso `ACCESS_NETWORK_STATE` viene letto dalla libreria di rendering MapLibre per rilevare il passaggio Wi-Fi vs dati mobili e regolare il caching delle tile. Non trasmette nulla.

---

## 4. Traffico di rete generato dall'app

VO2max Lab effettua richieste HTTPS in uscita **solo** verso:

- **`tiles.openfreemap.org`**: tile vettoriali e descrittore di stile (`style.json`) usati dalla MapLibre map view durante Cooper outdoor e 4x4 outdoor. Le richieste partono solo quando la mappa e' a schermo durante un allenamento tracciato.

E' l'intera lista. Non c'e' alcun endpoint di analytics, alcun endpoint di crash reporting, alcun endpoint pubblicitario, alcun endpoint di remote configuration, alcun endpoint di autenticazione.

OpenFreeMap e' gestita da un soggetto terzo. Le informazioni che riceve in una richiesta tile sono: il tuo indirizzo IP, le coordinate della tile (z, x, y) e lo User-Agent. Non controlliamo OpenFreeMap. La loro privacy policy e' documentata su [`https://openfreemap.org`](https://openfreemap.org).

Se non usi mai la mappa outdoor (cioe' esegui Cooper o 4x4 solo in modalita' indoor o con tapis roulant), l'app effettua **zero** richieste di rete dopo l'installazione.

---

## 5. Servizi terzi

**Non** integriamo:

- Google Analytics, Firebase Analytics o altri SDK di analytics;
- Firebase Crashlytics, Sentry, Bugsnag o altri SDK di crash reporting;
- AdMob o altri network pubblicitari;
- Facebook SDK, TikTok SDK o altri SDK di social platform;
- Servizi di push notification (FCM, OneSignal);
- Servizi di A/B testing o remote configuration;
- Provider di Single Sign-On o di identita'.

Gli unici SDK terzi presenti nell'app sono librerie che operano interamente sul dispositivo (Room, Hilt, MapLibre, Nordic BLE, Health Connect Jetpack, Google Play Services Location). Tra queste, solo Google Play Services Location e MapLibre hanno capacita' di rete e le configuriamo come descritto sopra (location: locale; MapLibre: solo tile OpenFreeMap).

---

## 6. Riepilogo permessi

Ogni permesso dichiarato nel manifest Android, in linguaggio chiaro:

| Permesso | Perche' lo chiediamo | Opzionale? |
|---|---|---|
| `health.READ_HEART_RATE` | Leggere la FC durante l'allenamento | Si' (concesso via Health Connect) |
| `health.READ_VO2_MAX` | Mostrare il V̇O2max storico da Health Connect | Si' |
| `health.WRITE_VO2_MAX` | Salvare il risultato Cooper / 4x4 in Health Connect, sul dispositivo | Si' |
| `health.READ_EXERCISE` | Mostrare allenamenti esterni nello storico | Si' |
| `health.READ_DISTANCE` | Mostrare i record di distanza esterni nello storico | Si' |
| `BODY_SENSORS` | Lettura FC di fallback su Android 13 e precedenti | Si' |
| `ACCESS_FINE_LOCATION` | Distanza GPS durante Cooper outdoor / 4x4 outdoor | Si' (solo se usi outdoor) |
| `ACCESS_COARSE_LOCATION` | Fallback GPS coarse durante outdoor | Si' |
| `BLUETOOTH_SCAN` (`neverForLocation`) | Scoprire tapis roulant FTMS | Si' (solo per modalita' tapis) |
| `BLUETOOTH_CONNECT` | Connessione al tapis FTMS | Si' |
| `BLUETOOTH` / `BLUETOOTH_ADMIN` (`maxSdkVersion=30`) | Idem su Android 11 e precedenti | Si' |
| `INTERNET` | Scaricare tile OpenFreeMap quando la mappa outdoor e' a schermo | Si' (no mappa = no traffico) |
| `ACCESS_NETWORK_STATE` | Comportamento cache tile MapLibre | Si' |
| `FOREGROUND_SERVICE`, `FOREGROUND_SERVICE_HEALTH`, `FOREGROUND_SERVICE_LOCATION`, `FOREGROUND_SERVICE_CONNECTED_DEVICE` | Mantenere vivo il timer mentre lo schermo e' spento | No (requisito Android) |
| `POST_NOTIFICATIONS` | Mostrare la notifica del foreground service (Android 13+) | Si' (concessione di sistema) |
| `VIBRATE` | Feedback aptico ai cambi di fase | No (concesso all'install, nessuna implicazione dati) |

Puoi revocare ogni permesso runtime in qualsiasi momento da Impostazioni Android, App, VO2max Lab, Permessi oppure, per Health Connect, dall'app Health Connect. La funzionalita' corrispondente degrada in modo controllato (per esempio, revocando il GPS si disabilita la modalita' outdoor ma l'app continua a funzionare).

---

## 7. Privacy dei minori

VO2max Lab **non e' rivolta ai minori di 13 anni**. Non raccogliamo consapevolmente dati da minori di 13 anni perche' non raccogliamo dati da nessuno, ma i contenuti dell'app (test cardiovascolari di fitness, V̇O2max stimato, zone di allenamento) sono pensati per adulti che si allenano sotto la propria responsabilita'. Se hai meno di 13 anni, chiedi a un genitore o tutore prima di usare l'app e consulta un medico prima di qualsiasi test a sforzo massimale.

---

## 8. Conservazione e cancellazione dei dati

Poiche' tutti i dati sono locali:

- **Cancellazione singola:** elimina un allenamento dalla schermata storico nell'app.
- **Cancellazione per profilo:** elimina un profilo dalla schermata profili; cancella in cascata i suoi allenamenti.
- **Disinstallazione completa:** disinstalla l'app da Impostazioni Android, App, VO2max Lab, Disinstalla. Cosi' azzeri il database Room e tutte le preferenze DataStore.
- **Dati in Health Connect:** quanto eventualmente scritto in Health Connect (letture V̇O2max) resta in Health Connect dopo la disinstallazione, perche' Health Connect e' un'app separata. Gestiscili dall'app Health Connect.

Non abbiamo server, ne' backup, ne' log, ne' ticket di supporto contenenti i tuoi dati. Non c'e' nulla a cui inoltrare una richiesta di cancellazione.

---

## 9. I tuoi diritti (GDPR e Codice Privacy)

Anche se non trattiamo dati personali su nessun server, conservi i diritti garantiti dal Regolamento UE 2016/679 (GDPR) e dal Codice in materia di protezione dei dati personali (D.Lgs. 196/2003 e successive modifiche):

- **Diritto di accesso:** esercitabile tramite lo storico in-app e le funzioni di esportazione (pianificate per una versione futura; nel frattempo, contattaci).
- **Diritto di rettifica:** modifica il profilo nell'app.
- **Diritto alla cancellazione:** elimina il profilo o disinstalla l'app.
- **Diritto alla portabilita':** funzione di export pianificata; nel frattempo, scrivici via email.
- **Diritto di opposizione e limitazione:** non c'e' alcun trattamento off-device a cui opporsi; il trattamento on-device e' interamente sotto il tuo controllo.
- **Diritto di reclamo:** al Garante per la protezione dei dati personali (`https://www.garanteprivacy.it`) o all'autorita' di protezione dati competente.

Per esercitare uno di questi diritti scrivi a **scanufe@fescacomit.com**. Rispondiamo entro 30 giorni come previsto dall'articolo 12 GDPR.

---

## 10. Sicurezza

I dati risiedono nello storage privato dell'app sul tuo telefono, isolato da Android dalle altre app. Ci appoggiamo alla cifratura full-disk del dispositivo (default da Android 10) per la protezione at-rest. Non implementiamo un passcode in-app o un blocco biometrico; se condividi il dispositivo, valuta le funzioni di blocco per app del launcher o l'App Lock di Android 14+.

Se scopri un problema di sicurezza che riguarda l'app, scrivi a **scanufe@fescacomit.com** con `[security]` nell'oggetto. Puntiamo a una prima risposta entro 5 giorni lavorativi.

---

## 11. Modifiche alla presente informativa

Aggiorniamo questa Privacy Policy quando l'app introduce una funzionalita' che cambia in modo sostanziale il trattamento dei dati (per esempio, una sincronizzazione cloud opt-in che oggi non esiste). Quando lo facciamo:

- La data `Ultimo aggiornamento` in alto cambia.
- Per modifiche non banali mostriamo un avviso in-app al primo lancio successivo e chiediamo di prenderne atto prima di proseguire.
- Le versioni precedenti restano disponibili nello storico commit del repository GitHub all'indirizzo `https://github.com/fscanu/vo2max-lab`.

Se una modifica futura peggiorasse la tua privacy rispetto alla versione che hai accettato in origine, richiederemo un consenso esplicito.

---

## 12. Disclaimer (medico)

VO2max Lab e' uno strumento di autovalutazione del fitness. Non e' un dispositivo medico e non diagnostica, non cura, non previene alcuna patologia. I test a sforzo massimale come Cooper e il 4x4 norvegese comportano rischi cardiovascolari; consulta un medico prima di eseguirli, soprattutto se hai piu' di 35 anni, sei sedentario o hai una patologia cardiaca, polmonare o metabolica nota.

Questo disclaimer non incide sui tuoi diritti previsti dalla presente informativa; e' incluso per completezza.

---

## 13. Contatti

**Email:** [scanufe@fescacomit.com](mailto:scanufe@fescacomit.com)
**Indirizzo postale:** disponibile su richiesta.

Per richieste relative alla privacy, includi `[privacy]` nell'oggetto cosi' la indirizziamo correttamente.
