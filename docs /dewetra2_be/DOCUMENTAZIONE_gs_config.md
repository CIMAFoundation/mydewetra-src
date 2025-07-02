# Documentazione della cartella `gs_config`

Questa documentazione descrive i file e il codice contenuto nella cartella `gs_config`, inclusi i file Python e le loro funzioni, classi e metodi.

---

## File: `gs_manager.py`

**Scopo:** Gestisce la pubblicazione di dati e stili su GeoServer.

### Classe: `GsManager`
#### Metodo: `__init__(self, gsUrl, gsUser, gsPsw)`
- **Descrizione:** Inizializza il gestore GeoServer con URL, utente e password.
- **Parametri:**
  - `gsUrl`: URL del GeoServer.
  - `gsUser`: Nome utente per l'autenticazione.
  - `gsPsw`: Password per l'autenticazione.
- **Restituisce:** Nessuno.
- **Eccezioni:** Solleva un'eccezione se l'autenticazione non è valida.

#### Metodo: `publish_data(self, uFile)`
- **Descrizione:** Pubblica un file (shapefile o GeoTIFF) su GeoServer.
- **Parametri:**
  - `uFile`: File caricato dall'utente.
- **Restituisce:** Dizionario con l'URL del GeoServer e l'ID del layer pubblicato.
- **Eccezioni:** Solleva un'eccezione se il file non è valido o non può essere pubblicato.

#### Metodo: `publish_shapefile(self, shapefilePath)`
- **Descrizione:** Pubblica uno shapefile su GeoServer.
- **Parametri:**
  - `shapefilePath`: Percorso dello shapefile.
- **Restituisce:** ID del layer pubblicato.
- **Eccezioni:** Solleva un'eccezione se la pubblicazione fallisce.

#### Metodo: `publish_geotiff(self, geoTiffPath)`
- **Descrizione:** Pubblica un file GeoTIFF su GeoServer.
- **Parametri:**
  - `geoTiffPath`: Percorso del file GeoTIFF.
- **Restituisce:** ID del layer pubblicato.
- **Eccezioni:** Solleva un'eccezione se la pubblicazione fallisce.

#### Metodo: `get_styles(self)`
- **Descrizione:** Recupera la lista degli stili disponibili su GeoServer.
- **Parametri:** Nessuno.
- **Restituisce:** Lista di stili.
- **Eccezioni:** Solleva un'eccezione se non è possibile recuperare gli stili.

#### Metodo: `publish_style(self, styleFile)`
- **Descrizione:** Pubblica uno stile su GeoServer.
- **Parametri:**
  - `styleFile`: File dello stile da pubblicare.
- **Restituisce:** Nome dello stile pubblicato.
- **Eccezioni:** Solleva un'eccezione se la pubblicazione fallisce.

#### Metodo: `set_layer_style(self, idLayer, idStyle)`
- **Descrizione:** Imposta uno stile per un layer specifico su GeoServer.
- **Parametri:**
  - `idLayer`: ID del layer.
  - `idStyle`: ID dello stile.
- **Restituisce:** Messaggio di conferma.
- **Eccezioni:** Solleva un'eccezione se il layer o lo stile non esistono o se l'operazione fallisce.

---

## File: `resources.py`

**Scopo:** Fornisce risorse per interagire con GeoServer tramite API REST.

### Classe: `GsManagerResource`
#### Metodo: `getMyUrl(self)`
- **Descrizione:** Restituisce gli URL gestiti dalla risorsa GeoServer.
- **Parametri:** Nessuno.
- **Restituisce:** Lista di oggetti `URLHelper` con gli endpoint disponibili.
- **Eccezioni:** Nessuno.

#### Metodo: `gssettings(self, request, **kwargs)`
- **Descrizione:** Recupera le impostazioni di GeoServer per l'utente autenticato.
- **Parametri:**
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Restituisce:** Dizionario con le impostazioni di GeoServer.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato.

#### Metodo: `publishdatas(self, request, **kwargs)`
- **Descrizione:** Pubblica dati (shapefile o GeoTIFF) su GeoServer.
- **Parametri:**
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Restituisce:** Dizionario con l'URL del GeoServer e l'ID del layer pubblicato.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato o `HttpApplicationError` in caso di errore.

#### Metodo: `publishstyle(self, request, **kwargs)`
- **Descrizione:** Pubblica uno stile su GeoServer.
- **Parametri:**
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Restituisce:** Nome dello stile pubblicato.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato o `HttpApplicationError` in caso di errore.

#### Metodo: `styles(self, request, **kwargs)`
- **Descrizione:** Recupera la lista degli stili disponibili su GeoServer.
- **Parametri:**
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Restituisce:** Lista di stili.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato o `HttpApplicationError` in caso di errore.

#### Metodo: `setlayerstyle(self, request, **kwargs)`
- **Descrizione:** Imposta uno stile per un layer specifico su GeoServer.
- **Parametri:**
  - `request`: Oggetto della richiesta HTTP.
  - `**kwargs`: Parametri aggiuntivi.
- **Restituisce:** Messaggio di conferma.
- **Eccezioni:** Restituisce `HttpUnauthorized` se l'utente non è autenticato o `HttpApplicationError` in caso di errore.

---

## File: `__init__.py`

**Scopo:** Indica che la cartella `gs_config` è un modulo Python.

---

Fine documentazione.
