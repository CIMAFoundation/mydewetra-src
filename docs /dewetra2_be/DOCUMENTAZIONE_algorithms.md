# DOCUMENTAZIONE ALGORITHMS

Questa documentazione descrive i file, le classi, le funzioni e i metodi presenti nella cartella `algorithms`. Ogni elemento include una descrizione, i parametri, i valori restituiti, le eccezioni sollevate e un esempio d'uso, se pertinente.

---

## File: `resources.py`

**Scopo:** Gestisce le risorse per l'esecuzione di algoritmi definiti dinamicamente.

### Classe: `AlgorithResource`

**Descrizione:** Fornisce un'interfaccia per eseguire algoritmi tramite richieste HTTP.

#### Metodo: `getMyUrl()`
- **Descrizione:** Restituisce una lista di URL supportati per l'interazione con le risorse.
- **Parametri:** Nessuno.
- **Restituisce:** Lista di oggetti `URLHelper` che rappresentano gli endpoint supportati.
- **Eccezioni:** Nessuna.
- **Esempio d'uso:**
  ```python
  resource = AlgorithResource()
  urls = resource.getMyUrl()
  ```

#### Metodo: `run(request, **kwargs)`
- **Descrizione:** Esegue un algoritmo specificato tramite una richiesta HTTP POST.
- **Parametri:**
  | Nome    | Tipo   | Descrizione                                      |
  |---------|--------|--------------------------------------------------|
  | `request` | `HttpRequest` | La richiesta HTTP contenente i dati dell'algoritmo. |
  | `kwargs`  | `dict` | Argomenti aggiuntivi opzionali.                |
- **Restituisce:** Risultato dell'esecuzione dell'algoritmo.
- **Eccezioni:** 
  - `HttpApplicationError` se i dati della richiesta sono invalidi.
- **Esempio d’uso:**
  ```python
  # Esempio di richiesta HTTP POST
  data = {
      "alg": "modulo.algoritmo",
      "input": {"param1": "valore1"}
  }
  response = AlgorithResource().run(request_with_data(data))
  ```

---

## File: `__init__.py`

**Scopo:** File di inizializzazione per il modulo `algorithms`.

**Contenuto:** Nessuna classe o funzione definita.

---

## File: `.gitignore`

**Scopo:** Specifica i file e le directory da ignorare nel controllo di versione.

**Contenuto:**  
- `/laminazione/`: Ignora la directory `laminazione`.

```markdown
# Contenuto del file:
# /laminazione/
```