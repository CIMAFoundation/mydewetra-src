# Documentazione della cartella `dds`

Questa documentazione descrive i file e il codice contenuto nella cartella `dds`, inclusi i file Python e le loro funzioni, classi e metodi.

---

## File: `dds_client.py`

### Descrizione
Questo file contiene le classi `DDSClient`, `DDSMapClient` e `DDSSerieClient`, che forniscono metodi per interagire con i servizi DDS.

### Classe: `DDSClient`
#### Metodo: `__init__(self, url, user, password)`
- **Scopo**: Inizializza il client DDS con URL, utente e password.
- **Parametri**:
  - `url`: URL del servizio DDS.
  - `user`: Nome utente per l'autenticazione.
  - `password`: Password per l'autenticazione.
- **Return**: Nessuno.

#### Metodo: `get(self, method, paramData=None)`
- **Scopo**: Esegue una richiesta GET al servizio DDS.
- **Parametri**:
  - `method`: Metodo da chiamare sul servizio DDS.
  - `paramData`: Parametri opzionali per la richiesta.
- **Return**: Risultato della richiesta in formato JSON.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `post(self, method, data)`
- **Scopo**: Esegue una richiesta POST al servizio DDS.
- **Parametri**:
  - `method`: Metodo da chiamare sul servizio DDS.
  - `data`: Dati da inviare nella richiesta.
- **Return**: Risultato della richiesta in formato JSON.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `getAsText(self, method, paramData=None)`
- **Scopo**: Esegue una richiesta GET al servizio DDS e restituisce il risultato come testo.
- **Parametri**:
  - `method`: Metodo da chiamare sul servizio DDS.
  - `paramData`: Parametri opzionali per la richiesta.
- **Return**: Risultato della richiesta in formato testo.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `getAsItIs(self, method, paramData=None)`
- **Scopo**: Esegue una richiesta GET al servizio DDS e restituisce il risultato senza modifiche.
- **Parametri**:
  - `method`: Metodo da chiamare sul servizio DDS.
  - `paramData`: Parametri opzionali per la richiesta.
- **Return**: Risultato della richiesta senza modifiche.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `postAsText(self, method, data)`
- **Scopo**: Esegue una richiesta POST al servizio DDS e restituisce il risultato come testo.
- **Parametri**:
  - `method`: Metodo da chiamare sul servizio DDS.
  - `data`: Dati da inviare nella richiesta.
- **Return**: Risultato della richiesta in formato testo.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

### Classe: `DDSMapClient`
#### Metodo: `supported(self)`
- **Scopo**: Recupera i tipi di dati supportati dal servizio DDS.
- **Parametri**: Nessuno.
- **Return**: Lista di tipi di dati supportati.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `properties(self, dataId)`
- **Scopo**: Recupera le proprietà di un layer DDS.
- **Parametri**:
  - `dataId`: ID del layer.
- **Return**: Proprietà del layer in formato JSON.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

---

## File: `dds_client2.py`

### Descrizione
Questo file contiene la classe `DDSMapClient2`, che estende le funzionalità del client DDS per mappe.

### Classe: `DDSMapClient2`
#### Metodo: `availability(self, props, t1, t2)`
- **Scopo**: Recupera la disponibilità di dati per un intervallo di tempo specifico.
- **Parametri**:
  - `props`: Proprietà del layer.
  - `t1`: Timestamp di inizio.
  - `t2`: Timestamp di fine.
- **Return**: Lista di dati disponibili.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `punctualSerie(self, props, t1, t2, lon, lat)`
- **Scopo**: Recupera una serie temporale puntuale per una posizione specifica.
- **Parametri**:
  - `props`: Proprietà del layer.
  - `t1`: Timestamp di inizio.
  - `t2`: Timestamp di fine.
  - `lon`: Longitudine della posizione.
  - `lat`: Latitudine della posizione.
- **Return**: Serie temporale puntuale.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `restore(self, props, days)`
- **Scopo**: Ripristina i dati di un layer DDS per un intervallo di giorni specificato.
- **Parametri**:
  - `props`: Proprietà del layer.
  - `days`: Numero di giorni da ripristinare.
- **Return**: Risultato del ripristino in formato JSON.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

#### Metodo: `getLayerBBox(self, layerId)`
- **Scopo**: Recupera il bounding box di un layer DDS.
- **Parametri**:
  - `layerId`: ID del layer.
- **Return**: Bounding box del layer in formato JSON.
- **Eccezioni**: Solleva `DDSError` in caso di errore.

---

## File: `resources.py`

### Descrizione
Questo file definisce le risorse DDS per l'interazione con i servizi DDS tramite API REST.

### Classe: `DDSMapResource`
#### Metodo: `supported(self, request, **kwargs)`
- **Scopo**: Recupera i tipi di dati supportati dal servizio DDS.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Lista di tipi di dati supportati.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `availability(self, request, **kwargs)`
- **Scopo**: Recupera la disponibilità di dati per un intervallo di tempo specifico.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Lista di dati disponibili.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `punctualserie(self, request, **kwargs)`
- **Scopo**: Recupera una serie temporale puntuale per una posizione specifica tramite API REST.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Serie temporale puntuale in formato JSON.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `publish(self, request, **kwargs)`
- **Scopo**: Pubblica un nuovo layer DDS tramite API REST.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Dettagli del layer pubblicato.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `permanent(self, request, **kwargs)`
- **Scopo**: Rende permanente un layer DDS tramite API REST.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Risultato dell'operazione.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `layerstyle(self, request, **kwargs)`
- **Scopo**: Recupera lo stile di un layer DDS.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Stile del layer in formato JSON.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `layerbbox(self, request, **kwargs)`
- **Scopo**: Recupera il bounding box di un layer DDS.
- **Parametri**:
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Return**: Bounding box del layer in formato JSON.
- **Eccezioni**: Restituisce `HttpUnauthorized` se l'utente non è autenticato.

---

## File: `__init__.py`

### Descrizione
File vuoto per indicare che la cartella è un modulo Python.

---

Fine documentazione.
