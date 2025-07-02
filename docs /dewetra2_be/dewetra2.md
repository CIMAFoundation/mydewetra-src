# DOCUMENTAZIONE DEWETRA2

Questa documentazione descrive i file, le classi, le funzioni e i metodi presenti nella cartella `dewetra2`. Ogni elemento include una descrizione, i parametri, i valori restituiti, le eccezioni sollevate e un esempio d'uso, se pertinente.

---

## File: `wsgi.py`

**Scopo:** Configura l'applicazione WSGI per il progetto Django.

### Funzione: `application`
- **Descrizione:** Punto di ingresso WSGI per il progetto Django.
- **Parametri:** Nessuno.
- **Restituisce:** Oggetto WSGI callable.
- **Eccezioni:** Nessuna.
- **Esempio d'uso:**
  ```python
  from wsgi import application
  ```

---

## File: `urls.py`

**Scopo:** Configura le URL del progetto Django.

### Variabile: `urlpatterns`
- **Descrizione:** Elenco delle URL configurate per il progetto.
- **Parametri:** Nessuno.
- **Restituisce:** Nessuno.
- **Eccezioni:** Nessuna.
- **Esempio d'uso:**
  ```python
  from urls import urlpatterns
  ```

---

## File: `settings.py`

**Scopo:** Contiene le impostazioni principali del progetto Django.

### Variabile: `DATABASES`
- **Descrizione:** Configurazione del database per il progetto.
- **Parametri:** Nessuno.
- **Restituisce:** Nessuno.
- **Eccezioni:** Nessuna.
- **Esempio d'uso:**
  ```python
  from settings import DATABASES
  ```

---

## File: `models.py`

**Scopo:** Definisce i modelli del database per il progetto.

### Classe: `Server`
- **Descrizione:** Rappresenta un server DDS.
- **Attributi:**
  | Nome       | Tipo       | Descrizione                          |
  |------------|------------|--------------------------------------|
  | `name`     | `CharField`| Nome del server.                    |
  | `descr`    | `TextField`| Descrizione del server.             |
  | `url`      | `CharField`| URL del server.                     |
  | `user`     | `CharField`| Nome utente per l'autenticazione.   |
  | `password` | `CharField`| Password per l'autenticazione.      |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del server.
    - **Restituisce:** Stringa con la descrizione del server.

### Classe: `LayerType`
- **Descrizione:** Rappresenta il tipo di layer.
- **Attributi:**
  | Nome   | Tipo       | Descrizione              |
  |--------|------------|--------------------------|
  | `name` | `CharField`| Nome del tipo di layer.  |
  | `code` | `CharField`| Codice del tipo di layer.|
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del tipo di layer.
    - **Restituisce:** Stringa con il nome del tipo di layer.

### Classe: `Tag`
- **Descrizione:** Rappresenta un tag associato ai layer.
- **Attributi:**
  | Nome   | Tipo       | Descrizione              |
  |--------|------------|--------------------------|
  | `name` | `CharField`| Nome del tag.            |
  | `descr`| `TextField`| Descrizione del tag.     |
  | `icon` | `CharField`| Icona associata al tag.  |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del tag.
    - **Restituisce:** Stringa con la descrizione del tag.

### Classe: `Group`
- **Descrizione:** Rappresenta un gruppo di layer.
- **Attributi:**
  | Nome       | Tipo       | Descrizione              |
  |------------|------------|--------------------------|
  | `hierarchy`| `CharField`| Gerarchia del gruppo.    |
  | `name`     | `CharField`| Nome del gruppo.         |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del gruppo.
    - **Restituisce:** Stringa con il nome e la gerarchia del gruppo.

### Classe: `Path`
- **Descrizione:** Rappresenta un percorso gerarchico.
- **Attributi:**
  | Nome       | Tipo       | Descrizione              |
  |------------|------------|--------------------------|
  | `hierarchy`| `CharField`| Gerarchia del percorso.  |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del percorso.
    - **Restituisce:** Stringa con la gerarchia del percorso.

### Classe: `LayerCategory`
- **Descrizione:** Rappresenta una categoria di layer.
- **Attributi:**
  | Nome   | Tipo       | Descrizione              |
  |--------|------------|--------------------------|
  | `name` | `CharField`| Nome della categoria.    |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale della categoria.
    - **Restituisce:** Stringa con il nome della categoria.

### Classe: `GeoScale`
- **Descrizione:** Rappresenta una scala geografica.
- **Attributi:**
  | Nome   | Tipo       | Descrizione              |
  |--------|------------|--------------------------|
  | `name` | `CharField`| Nome della scala.        |
  | `descr`| `TextField`| Descrizione della scala. |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale della scala.
    - **Restituisce:** Stringa con la descrizione della scala.

### Classe: `Layer`
- **Descrizione:** Rappresenta un layer geografico.
- **Attributi:**  
  (Elenco parziale per brevità)
  | Nome       | Tipo           | Descrizione                                      |
  |------------|----------------|--------------------------------------------------|
  | `dataid`   | `CharField`    | Identificativo del layer.                        |
  | `name`     | `CharField`    | Nome del layer.                                  |
  | `descr`    | `TextField`    | Descrizione del layer.                           |
  | `lonw`     | `FloatField`   | Longitudine ovest del bounding box.              |
  | `lone`     | `FloatField`   | Longitudine est del bounding box.                |
  | `lats`     | `FloatField`   | Latitudine sud del bounding box.                 |
  | `latn`     | `FloatField`   | Latitudine nord del bounding box.                |
  | `type`     | `ForeignKey`   | Tipo del layer (relazione con `LayerType`).      |
  | `server`   | `ForeignKey`   | Server associato al layer (relazione con `Server`).|
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del layer.
    - **Restituisce:** Stringa con il nome, l'identificativo, il tipo e la categoria del layer.

### Classe: `LayerGroupPermission`
- **Descrizione:** Gestisce i permessi per i gruppi di layer.
- **Attributi:**
  | Nome   | Tipo           | Descrizione                          |
  |--------|----------------|--------------------------------------|
  | `user` | `ForeignKey`   | Utente associato al permesso.        |
  | `groups`| `ManyToManyField`| Gruppi associati al permesso.     |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale del permesso.
    - **Restituisce:** Stringa con l'utente associato.

### Classe: `UserSettings`
- **Descrizione:** Gestisce le impostazioni utente.
- **Attributi:**
  | Nome          | Tipo       | Descrizione                          |
  |---------------|------------|--------------------------------------|
  | `user`        | `ForeignKey`| Utente associato alle impostazioni. |
  | `stationgroup`| `CharField`| Gruppo di stazioni associato.        |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale delle impostazioni.
    - **Restituisce:** Stringa con l'utente e il gruppo di stazioni.

### Classe: `TagStatistics`
- **Descrizione:** Raccoglie statistiche sui tag.
- **Attributi:**
  | Nome   | Tipo       | Descrizione                          |
  |--------|------------|--------------------------------------|
  | `acuid`| `CharField`| Identificativo univoco dell'utente.  |
  | `tag`  | `ForeignKey`| Tag associato alle statistiche.    |
  | `count`| `BigIntegerField`| Conteggio delle occorrenze.   |

### Classe: `Tool`
- **Descrizione:** Rappresenta uno strumento associato ai dati.
- **Attributi:**
  | Nome     | Tipo           | Descrizione                          |
  |----------|----------------|--------------------------------------|
  | `dataid` | `CharField`    | Identificativo dello strumento.      |
  | `name`   | `CharField`    | Nome dello strumento.                |
  | `descr`  | `TextField`    | Descrizione dello strumento.         |
  | `config` | `TextField`    | Configurazione dello strumento.      |
  | `manager`| `CharField`    | Manager responsabile dello strumento.|
  | `users`  | `ManyToManyField`| Utenti associati allo strumento.   |
- **Metodi:**
  - `__unicode__()`: Restituisce una rappresentazione testuale dello strumento.
    - **Restituisce:** Stringa con l'identificativo, il nome e la descrizione dello strumento.
---

## File: `admin.py`

**Scopo:** Configura l'interfaccia di amministrazione di Django.

### Classe: `Dewetra2LayerAdmin`
- **Descrizione:** Configura l'amministrazione per il modello `Layer`.
- **Metodi:**
  - Nessuno specifico.

---

## File: `manage.py`

**Scopo:** Script di gestione per il progetto Django.

### Funzione: `main`
- **Descrizione:** Punto di ingresso per i comandi di gestione di Django.
- **Parametri:** Nessuno.
- **Restituisce:** Nessuno.
- **Eccezioni:** Nessuna.
- **Esempio d'uso:**