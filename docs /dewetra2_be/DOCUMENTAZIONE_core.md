# Documentazione della cartella `core`

Questa documentazione descrive i file e il codice contenuto nella cartella `core`, inclusi i file Python e le loro funzioni, classi e metodi.

---

## File: `util_resources.py`

**Scopo:** Fornisce risorse utili come il download di report e il proxying di richieste.

### Classe: `UtilRes`
#### Metodo: `downloadAutporReport(self, request, **kwargs)`
- **Descrizione:** Permette il download di un file specifico dal server.
- **Parametri:**
  | Nome       | Tipo   | Descrizione                     |
  |------------|--------|---------------------------------|
  | `request`  | HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs` | dict   | Parametri aggiuntivi.           |
- **Restituisce:** Risposta HTTP con il file scaricato.
- **Eccezioni:** Solleva `HttpApplicationError` se il file non esiste o non è accessibile.

#### Metodo: `proxy(self, request, **kwargs)`
- **Descrizione:** Gestisce richieste proxy per inoltrare dati a un URL specificato.
- **Parametri:**
  | Nome       | Tipo   | Descrizione                     |
  |------------|--------|---------------------------------|
  | `request`  | HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs` | dict   | Parametri aggiuntivi.           |
- **Restituisce:** Risposta HTTP con i dati ricevuti dal server remoto.
- **Eccezioni:** Restituisce `HttpApplicationError` in caso di errore durante la richiesta proxy.

---

## File: `tools_resources.py`

**Scopo:** Gestisce strumenti e scenari, inclusi caricamenti di shapefile e conversioni.

### Classe: `ToolsResource`
#### Metodo: `getToolById(self, request, **kwargs)`
- **Descrizione:** Recupera uno strumento specifico tramite il suo ID.
- **Parametri:**
  | Nome       | Tipo   | Descrizione                     |
  |------------|--------|---------------------------------|
  | `request`  | HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs` | dict   | Parametri aggiuntivi.           |
- **Restituisce:** Dati dello strumento richiesto.
- **Eccezioni:** Solleva `HttpApplicationError` in caso di errore.

#### Metodo: `saveTool(self, request, **kwargs)`
- **Descrizione:** Salva o aggiorna uno strumento.
- **Parametri:**
  | Nome       | Tipo   | Descrizione                     |
  |------------|--------|---------------------------------|
  | `request`  | HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs` | dict   | Parametri aggiuntivi.           |
- **Restituisce:** Messaggio di conferma.
- **Eccezioni:** Solleva `HttpApplicationError` in caso di errore.

---

## File: `permissions.py`

**Scopo:** Definisce classi per la gestione delle autorizzazioni.

### Classe: `DewetraBaseAuthorization`
- **Descrizione:** Classe base per le autorizzazioni.
- **Metodi:** Implementa metodi per negare tutte le operazioni CRUD.

### Classe: `DewetraLayerAuthorization`
#### Metodo: `_getFilteredLayersByUser(self, object_list, bundle)`
- **Descrizione:** Filtra i layer accessibili all'utente corrente.
- **Parametri:**
  | Nome         | Tipo   | Descrizione                     |
  |--------------|--------|---------------------------------|
  | `object_list`| QuerySet | Lista di oggetti da filtrare. |
  | `bundle`     | dict   | Bundle della richiesta.         |
- **Restituisce:** Lista filtrata di layer.
- **Eccezioni:** Nessuna.

---

## File: `exceptions.py`

**Scopo:** Definisce eccezioni personalizzate.

### Classe: `DewetraError`
- **Descrizione:** Eccezione generica per errori in Dewetra.

---

## File: `report_resources.py`

**Scopo:** Gestisce risorse relative ai report.

### Classe: `ReportUtilRes`
#### Metodo: `getForecastDatasAvailability(self, request, **kwargs)`
- **Descrizione:** Recupera la disponibilità di dati di previsione per un intervallo di tempo specificato.
- **Parametri:**
  | Nome       | Tipo   | Descrizione                     |
  |------------|--------|---------------------------------|
  | `request`  | HTTP   | Oggetto della richiesta HTTP.   |
  | `**kwargs` | dict   | Parametri aggiuntivi.           |
- **Restituisce:** Lista di dati di previsione disponibili.
- **Eccezioni:** Restituisce `HttpApplicationError` in caso di errore durante la ricerca dei dati.

---

Fine aggiornamento.
