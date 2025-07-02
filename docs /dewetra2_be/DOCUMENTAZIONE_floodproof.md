# Documentazione della cartella `floodproof`

Questa documentazione descrive i file e il codice contenuto nella cartella `floodproof`, inclusi i file Python e le loro funzioni, classi e metodi.

---

## File: `resources.py`

**Scopo:** Gestisce le risorse per la gestione dei dati di floodproof.

### Classe: `FloodProofResource`
#### Metodo: `getMyUrl(self)`
- **Descrizione:** Restituisce gli URL gestiti dalla risorsa FloodProof.
- **Parametri:** Nessuno.
- **Restituisce:** Lista di oggetti `URLHelper` con gli endpoint disponibili.
- **Eccezioni:** Nessuna.

#### Metodo: `layer(self, request, **kwargs)`
- **Descrizione:** Recupera i dati di un layer floodproof per un intervallo di tempo specifico.
- **Parametri:**
  | Nome     | Tipo   | Descrizione                     |
  |----------|--------|---------------------------------|
  | `request`| HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs`| dict  | Parametri aggiuntivi.           |
- **Restituisce:** Dati del layer in formato JSON.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato.

---

## File: `reader.py`

**Scopo:** Fornisce un lettore per i dati di floodproof.

### Classe: `FloodProofReader`
#### Metodo: `__init__(self, serieId)`
- **Descrizione:** Inizializza il lettore con l'ID della serie.
- **Parametri:**
  | Nome     | Tipo   | Descrizione                     |
  |----------|--------|---------------------------------|
  | `serieId`| string | ID della serie floodproof.      |
- **Restituisce:** Nessuno.
- **Eccezioni:** Nessuna.

#### Metodo: `read(self, features, fidField, t1, t2)`
- **Descrizione:** Legge i dati delle feature e aggiorna le proprietà con statistiche.
- **Parametri:**
  | Nome       | Tipo   | Descrizione                     |
  |------------|--------|---------------------------------|
  | `features` | list   | Lista di feature da elaborare.  |
  | `fidField` | string | Campo ID delle feature.         |
  | `t1`       | int    | Timestamp di inizio.            |
  | `t2`       | int    | Timestamp di fine.              |
- **Restituisce:** Nessuno.
- **Eccezioni:** Nessuna.


#### Metodo: `layerNative(self, request, **kwargs)`
- **Descrizione:** Recupera i dati di un layer floodproof in formato nativo.
- **Parametri:**
  | Nome     | Tipo   | Descrizione                     |
  |----------|--------|---------------------------------|
  | `request`| HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs`| dict  | Parametri aggiuntivi.           |       
- **Restituisce:** Dati del layer in formato nativo.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato.          
  
 #### Metodo: `compatibles(self, request, **kwargs)`
- **Descrizione:** Recupera i layer floodproof compatibili con la richiesta.
- **Parametri:**
  | Nome     | Tipo   | Descrizione                     |
  |----------|--------|---------------------------------|
  | `request`| HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs`| dict  | Parametri aggiuntivi.           |
- **Restituisce:** Lista di layer compatibili.
- **Eccezioni
- :** Restituisce `HttpUnauthorized` se l'utente non è autenticato.     
   
---

## File: `__init__.py`

**Scopo:** Indica che la cartella `floodproof` è un modulo Python.

---

Fine documentazione.
