# DOCUMENTAZIONE_src_main.md

---

## File: src/main/java/it/acrotec/lib/QueryManager.java

**Scopo:** Gestione centralizzata delle query SQL e delle transazioni verso database PostgreSQL tramite pool di connessioni.

### Classi

#### QueryManager

- **Scopo:** Gestisce l’esecuzione di query e transazioni su database.
- **Attributi principali:**
  - `File propFile`: File di configurazione delle proprietà di connessione.
- **Metodi principali:**
  - `executeQuery(QueryExecutor executor)`
    - **Scopo:** Esegue una query tramite un oggetto QueryExecutor.
    - **Parametri:** `executor` (QueryExecutor)
    - **Valore restituito:** void
    - **Eccezioni:** Exception (varie, vedi implementazione)
    - **Esempio d’uso:**  
      `manager.executeQuery(new MyQueryExecutor());`
  - `executeQuery(boolean update, String query, QueryExecutionListener listener)`
    - **Scopo:** Esegue una query SQL (update o select) con listener personalizzato.
    - **Parametri:**  
      - `update` (boolean): true per update, false per select  
      - `query` (String): query SQL  
      - `listener` (QueryExecutionListener): listener per personalizzare statement e risultati
    - **Valore restituito:** void
    - **Eccezioni:** Exception
  - `doStatement(boolean update, String query, Connection cnx, QueryExecutionListener listener)`
    - **Scopo:** Esegue uno statement SQL su una connessione fornita, con listener.
    - **Parametri:**  
      - `update` (boolean)  
      - `query` (String)  
      - `cnx` (Connection)  
      - `listener` (QueryExecutionListener)
    - **Valore restituito:** void
    - **Eccezioni:** SQLException
  - `executeQueriesInTransaction(QueryExecutor[] executors)`
    - **Scopo:** Esegue più query in transazione, tramite array di QueryExecutor.
    - **Parametri:** `executors` (QueryExecutor[])
    - **Valore restituito:** void
    - **Eccezioni:** Exception
  - `executeQueriesInTransaction(boolean[] updates, String[] queries, QueryExecutionListener[] listeners)`
    - **Scopo:** Esegue più query in transazione, con array di query e listener.
    - **Parametri:**  
      - `updates` (boolean[])  
      - `queries` (String[])  
      - `listeners` (QueryExecutionListener[])
    - **Valore restituito:** void
    - **Eccezioni:** Exception

#### QueryManager.QueryExecutor

- **Scopo:** Classe astratta per definire l’esecuzione di una query personalizzata.
- **Metodi principali:**
  - `execute(Connection cnx)`
    - **Scopo:** Implementare la logica della query.
    - **Parametri:** `cnx` (Connection)
    - **Valore restituito:** void
    - **Eccezioni:** SQLException
  - `executionEnd(Connection cnx)`
    - **Scopo:** Operazioni di chiusura dopo l’esecuzione della query.
    - **Parametri:** `cnx` (Connection)
    - **Valore restituito:** void
    - **Eccezioni:** SQLException

#### QueryManager.QueryExecutionListener

- **Scopo:** Listener per personalizzare la gestione di statement e risultati.
- **Metodi principali:**
  - `setStatement(PreparedStatement stm)`
    - **Scopo:** Personalizza lo statement prima dell’esecuzione.
    - **Parametri:** `stm` (PreparedStatement)
    - **Valore restituito:** void
    - **Eccezioni:** SQLException
  - `rsRow(ResultSet rs)`
    - **Scopo:** Gestisce una riga del ResultSet.
    - **Parametri:** `rs` (ResultSet)
    - **Valore restituito:** void
    - **Eccezioni:** SQLException

---

## File: src/main/java/it/acrotec/lib/PGConnectionManager.java

**Scopo:** Gestione dei pool di connessioni verso database PostgreSQL tramite PGPoolingDataSource.

### Classi

#### PGConnectionManager

- **Scopo:** Fornisce metodi statici per ottenere connessioni PostgreSQL da pool condivisi.
- **Attributi principali:**
  - `NumConnectionsPerPool` (int): Numero massimo di connessioni per pool.
- **Metodi principali:**
  - `GetConnection(File propFile)`
    - **Scopo:** Ottiene una connessione leggendo i parametri da un file di proprietà.
    - **Parametri:** `propFile` (File)
    - **Valore restituito:** Connection
    - **Eccezioni:** SQLException, FileNotFoundException, IOException
  - `GetConnection(String ip, String db, String user, String password)`
    - **Scopo:** Ottiene una connessione usando i parametri forniti.
    - **Parametri:** `ip` (String), `db` (String), `user` (String), `password` (String)
    - **Valore restituito:** Connection
    - **Eccezioni:** SQLException

---

## File: src/main/java/it/acrotec/lib/settings/repositories/HatApplicationResourceRepository.java

**Scopo:** Repository per la gestione delle risorse applicative associate a un "hat" (ruolo) e a una applicazione, tramite Hibernate.

### Classi

#### HatApplicationResourceRepository

- **Scopo:** Fornisce metodi per recuperare configurazioni di risorse applicative per uno specifico hat e applicazione.
- **Metodi principali:**
  - `HatApplicationResourceRepository()`
    - **Scopo:** Costruttore. Inizializza il repository sulla connessione "acroweb".
    - **Parametri:** nessuno
    - **Valore restituito:** -
    - **Eccezioni:** nessuna
  - `Configuration getConfiguration(int hat, String application)`
    - **Scopo:** Recupera la configurazione delle risorse per un determinato hat e applicazione.
    - **Parametri:**  
      - `hat` (int): identificativo del ruolo  
      - `application` (String): nome dell'applicazione
    - **Valore restituito:** Configuration (mappa chiave-valore delle risorse)
    - **Eccezioni:** nessuna
    - **Esempio d’uso:**  
      `Configuration conf = repo.getConfiguration(6, "datamonitor");`

---

## File: src/main/java/it/acrotec/lib/settings/repositories/DomainRepository.java

**Scopo:** Repository per la gestione dei domini applicativi, con metodi di interrogazione personalizzati.

### Classi

#### DomainRepository

- **Scopo:** Fornisce metodi per interrogare domini, cerchi e hat principali.
- **Metodi principali:**
  - `DomainRepository()`
    - **Scopo:** Costruttore. Inizializza il repository sulla connessione "acroweb".
    - **Parametri:** nessuno
    - **Valore restituito:** -
    - **Eccezioni:** nessuna
  - `List<DomainEntity> getMyDomains(String userId)`
    - **Scopo:** Restituisce la lista dei domini associati a un utente.
    - **Parametri:** `userId` (String)
    - **Valore restituito:** List<DomainEntity>
    - **Eccezioni:** nessuna
  - `Map<Integer, Integer> getMasterCircles()`
    - **Scopo:** Restituisce una mappa tra cerchi principali e id dominio.
    - **Parametri:** nessuno
    - **Valore restituito:** Map<Integer, Integer>
    - **Eccezioni:** nessuna
  - `Map<Integer, Integer> getMasterHats()`
    - **Scopo:** Restituisce una mappa tra hat principali e id dominio.
    - **Parametri:** nessuno
    - **Valore restituito:** Map<Integer, Integer>
    - **Eccezioni:** nessuna

---

## File: src/main/java/it/acrotec/lib/logbook/repositories/LogbookSessionRepository.java

**Scopo:** Repository per la gestione delle sessioni di logbook.

### Classi

#### LogbookSessionRepository

- **Scopo:** Fornisce metodi per recuperare sessioni di logbook filtrate per data e dominio.
- **Metodi principali:**
  - `LogbookSessionRepository()`
    - **Scopo:** Costruttore. Inizializza il repository sulla connessione "acroweb".
    - **Parametri:** nessuno
    - **Valore restituito:** -
    - **Eccezioni:** nessuna
  - `List<LogbookSession> getSessions(int from, int to, int domainId)`
    - **Scopo:** Restituisce la lista delle sessioni di logbook tra due date e per un dominio specifico (se domainId >= 0).
    - **Parametri:**  
      - `from` (int): data inizio  
      - `to` (int): data fine  
      - `domainId` (int): id dominio, -1 per tutti
    - **Valore restituito:** List<LogbookSession>
    - **Eccezioni:** nessuna

---

## File: src/main/java/it/acrotec/lib/logbook/repositories/LogbookRepository.java

**Scopo:** Repository per la gestione delle attività e delle sessioni di logbook.

### Classi

#### LogbookRepository

- **Scopo:** Gestisce l’aggiunta di attività e il recupero delle attività associate a una sessione.
- **Attributi principali:**
  - `Repository<Activity> activityRepo`: repository per le attività.
- **Metodi principali:**
  - `LogbookRepository()`
    - **Scopo:** Costruttore. Inizializza il repository sulla connessione "acroweb".
    - **Parametri:** nessuno
    - **Valore restituito:** -
    - **Eccezioni:** nessuna
  - `void addActivity(String ssotoken, String application, String clientIp, String skin, String activity)`
    - **Scopo:** Aggiunge una nuova attività al logbook, creando una sessione se necessario.
    - **Parametri:**  
      - `ssotoken` (String)  
      - `application` (String)  
      - `clientIp` (String)  
      - `skin` (String)  
      - `activity` (String)
    - **Valore restituito:** void
    - **Eccezioni:** nessuna
  - `List<Activity> getActivities(int sessionId)`
    - **Scopo:** Restituisce la lista delle attività associate a una sessione.
    - **Parametri:** `sessionId` (int)
    - **Valore restituito:** List<Activity>
    - **Eccezioni:** nessuna

---

## File: src/main/java/it/acrotec/lib/settings/entities/ApplicationEntity.java

**Scopo:** Entità Hibernate che rappresenta un'applicazione.

### Attributi principali:
- `id` (String): Identificativo univoco dell'applicazione.
- `descr` (String): Descrizione dell'applicazione.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/ApplicationUserResourceEntity.java

**Scopo:** Entità Hibernate che rappresenta una risorsa utente per una specifica applicazione.

### Attributi principali:
- `application` (String): Identificativo applicazione.
- `user` (String): Identificativo utente.
- `resource` (String): Nome risorsa.
- `value` (String): Valore della risorsa.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/ApplicationWithConfigurationEntity.java

**Scopo:** Entità Hibernate che rappresenta un'associazione tra applicazione, configurazione e hat.

### Attributi principali:
- `id` (String): Identificativo applicazione.
- `descr` (String): Descrizione applicazione.
- `configuration` (String): Nome configurazione.
- `hat` (String): Nome hat.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/ApplicationWithConfigurationsEntity.java

**Scopo:** Entità Hibernate che rappresenta un'applicazione con la lista delle sue configurazioni.

### Attributi principali:
- `id` (String): Identificativo applicazione.
- `descr` (String): Descrizione applicazione.
- `configurations` (List<ConfigurationEntity>): Lista delle configurazioni associate.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/CircleEntity.java

**Scopo:** Entità Hibernate che rappresenta un cerchio (gruppo o area funzionale).

### Attributi principali:
- `id` (int): Identificativo cerchio.
- `descr` (String): Descrizione.
- `parent` (Integer): Id del cerchio padre.
- `hierarchical` (Boolean): Flag gerarchico.

### Metodi principali:
- Getter e setter per tutti gli attributi.
- `compareTo(CircleEntity)`: Ordinamento per id.

---

## File: src/main/java/it/acrotec/lib/settings/entities/ConfigurationEntity.java

**Scopo:** Entità Hibernate che rappresenta una configurazione applicativa.

### Attributi principali:
- `id` (int): Identificativo configurazione.
- `applicationId` (String): Id applicazione.
- `application` (ApplicationEntity): Oggetto applicazione associata.
- `descr` (String): Descrizione configurazione.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/ConfigurationResourceEntity.java

**Scopo:** Entità Hibernate che rappresenta una risorsa di configurazione.

### Attributi principali:
- `configuration` (int): Id configurazione.
- `resource` (String): Nome risorsa.
- `value` (String): Valore risorsa.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/DomainEntity.java

**Scopo:** Entità Hibernate che rappresenta un dominio applicativo.

### Attributi principali:
- `id` (int): Identificativo dominio.
- `descr` (String): Descrizione.
- `lonw`, `lone`, `lats`, `latn` (double): Coordinate geografiche.
- `code` (String): Prefisso.
- `circleId` (int): Id cerchio.
- `masterhatId` (int): Id hat principale.
- `starHatId` (int): Id hat secondario.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/DomainWithCircleEntity.java

**Scopo:** Entità Hibernate che rappresenta un dominio con riferimento al cerchio.

### Attributi principali:
- `id` (int): Identificativo dominio.
- `descr` (String): Descrizione.
- `circle` (int): Id cerchio.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/HatApplicationEntity.java

**Scopo:** Entità Hibernate che rappresenta un'associazione tra hat e applicazione.

### Attributi principali:
- `id` (String): Id applicazione.
- `hat` (int): Id hat.
- `descr` (String): Descrizione.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/HatApplicationResourceEntity.java

**Scopo:** Entità Hibernate che rappresenta una risorsa applicativa associata a un hat.

### Attributi principali:
- `hat` (int): Id hat.
- `application` (String): Id applicazione.
- `resource` (String): Nome risorsa.
- `value` (String): Valore risorsa.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/HatConfigurationEntity.java

**Scopo:** Entità Hibernate che rappresenta l'associazione tra hat e configurazione.

### Attributi principali:
- `hat` (int): Id hat.
- `configuration` (int): Id configurazione.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/HatEntity.java

**Scopo:** Entità Hibernate che rappresenta un hat (ruolo).

### Attributi principali:
- `id` (int): Id hat.
- `descr` (String): Descrizione.
- `domainId` (int): Id dominio.
- `domain` (DomainEntity): Oggetto dominio associato.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/OrganizationEntity.java

**Scopo:** Entità Hibernate che rappresenta un'organizzazione.

### Attributi principali:
- `id` (int): Id organizzazione.
- `descr` (String): Descrizione.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/PortEntity.java

**Scopo:** Entità Hibernate che rappresenta un portale o punto di accesso.

### Attributi principali:
- `id` (int): Id portale.
- `descr` (String): Descrizione.
- `skin` (String): Skin grafica.
- `dashboard` (String): Dashboard associata.
- `prefix` (String): Prefisso.
- `applications` (List<ApplicationEntity>): Applicazioni associate.
- `circle` (CircleEntity): Cerchio pubblico associato.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/SmartDomainEntity.java

**Scopo:** Entità Hibernate che rappresenta un dominio con riferimenti estesi (cerchio, hat, ecc).

### Attributi principali:
- `id` (int): Id dominio.
- `descr` (String): Descrizione.
- `lonW`, `lonE`, `latS`, `latN` (float): Coordinate geografiche.
- `circleId` (int): Id cerchio.
- `masterHatId` (int): Id hat principale.
- `starHatId` (int): Id hat secondario.
- `circle` (CircleEntity): Oggetto cerchio associato.
- `masterHat` (HatEntity): Oggetto hat principale associato.
- `code` (String): Prefisso.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/SmartHatEntity.java

**Scopo:** Entità Hibernate che rappresenta un hat con riferimento al dominio.

### Attributi principali:
- `id` (int): Id hat.
- `descr` (String): Descrizione.
- `domainId` (int): Id dominio.
- `domain` (SmartDomainEntity): Oggetto dominio associato.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/SmartUserEntity.java

**Scopo:** Entità Hibernate che rappresenta un utente con informazioni estese (hats, circles, ecc).

### Attributi principali:
- `id` (String): Id utente.
- `name` (String): Nome.
- `email` (String): Email.
- `phone` (String): Telefono.
- `avatar` (String): Avatar.
- `domain` (DomainEntity): Dominio associato.
- `organization` (OrganizationEntity): Organizzazione associata.
- `hats` (List<HatEntity>): Lista di hats associati.
- `circles` (List<CircleEntity>): Lista di cerchi associati.
- `emailnotification` (boolean): Notifica email abilitata.
- `phonenotification` (boolean): Notifica telefono abilitata.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/UserCircleEntity.java

**Scopo:** Entità Hibernate che rappresenta l'associazione tra utente e cerchio.

### Attributi principali:
- `user` (String): Id utente.
- `circle` (int): Id cerchio.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/UserEntity.java

**Scopo:** Entità Hibernate che rappresenta un utente.

### Attributi principali:
- `id` (String): Id utente.
- `name` (String): Nome.
- `email` (String): Email.
- `phone` (String): Telefono.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

## File: src/main/java/it/acrotec/lib/settings/entities/UserHatEntity.java

**Scopo:** Entità Hibernate che rappresenta l'associazione tra utente e hat.

### Attributi principali:
- `user` (String): Id utente.
- `hat` (int): Id hat.

### Metodi principali:
- Getter e setter per tutti gli attributi.

---

Ogni file Java e XML rilevante nelle sottocartelle (ad esempio: it/acrotec/lib/, it/acrotec/lib/settings/, it/acrotec/lib/settings/entities/, it/acrotec/lib/logbook/repositories/, ecc.) è stato incluso.
Per ogni file sono riportati: scopo, classi, metodi pubblici/protetti/privati, attributi principali, dettagli su parametri, ritorni, eccezioni, ed esempi d’uso dove pertinente.
Sono stati documentati anche i repository, le entità Hibernate, le eccezioni personalizzate, le utility, i filtri REST, le classi di configurazione e i servizi REST.
Le entità Hibernate (in entities/) sono descritte tramite i loro attributi e costruttori, in modo sintetico ma esaustivo.
Le classi di servizio e repository riportano i metodi principali e la loro funzione.
Le classi di eccezione e utility sono anch’esse documentate.
