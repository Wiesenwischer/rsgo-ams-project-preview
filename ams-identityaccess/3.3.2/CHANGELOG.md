# Changelog – ams.identityaccess

Alle nennenswerten Änderungen an diesem Produkt werden hier dokumentiert.
Das Format orientiert sich an [Keep a Changelog](https://keepachangelog.com/de/1.1.0/),
die Versionierung folgt [Semantic Versioning](https://semver.org/lang/de/).

ams.identityaccess ist der eigenständig ausgelieferte Identity Provider für die
ams-Produkte (IdentityServer, AdminPortal, ClientHub, EmailSender).

## [3.3.2] – 2026-07-17

### Behoben
- **Der Sitzungsdauer-Fix greift jetzt auch beim normalen Login.** Die in 3.3.1
  eingeführte `refresh_expires_in`-Ausgabe war daran gebunden, dass `offline_access`
  in den angefragten Scopes auftaucht. IdentityServer4 stellt dieses Scope dort aber
  nicht bereit, sodass der **Authorization-Code-Login** den Hinweis nie erhielt und
  die BFF-Sitzung weiterhin nach ~1 Stunde ablief. `refresh_expires_in` wird jetzt für
  den **Authorization-Code-** und den **Refresh-Token-Grant** ausgegeben, abgesichert
  über die Client-Einstellung `AllowOfflineAccess`.
  **Wirkung:** Angemeldete Nutzer bleiben so lange eingeloggt, wie ihr Refresh Token
  gültig ist (Tage statt ~1 Stunde) — auch über den regulären Anmeldeweg.

## [3.3.1] – 2026-07-16

### Behoben
- **Die BFF-Sitzung überlebt jetzt die Lebensdauer des Zugriffstokens.** IdentityServer4
  meldet — anders als Keycloak — die Refresh-Token-Lebensdauer nicht im Token-Response.
  Die Web-BFF nutzt diesen Wert, um die TTL ihres serverseitigen Token-Vaults zu
  dimensionieren; ohne ihn fiel die TTL auf die kurze Access-Token-Lebensdauer zurück,
  sodass die Sitzung ~1 Stunde nach dem Login endete, obwohl das Refresh Token noch
  tagelang gültig war. Ein neuer `ICustomTokenRequestValidator` ergänzt ein
  Keycloak-kompatibles `refresh_expires_in` (aus der konfigurierten
  Refresh-Token-Lebensdauer des Clients), sobald ein Refresh Token ausgestellt wird.
  Token-Exchange-Responses bleiben unverändert.

## [3.3.0] – 2026-07-02

### Geändert
- **IdentityAccess läuft jetzt standardmäßig „self-contained" in einer einzigen
  Datenbank.** Die separate NServiceBus-Transport-Datenbank ist **optional** geworden.
  Neue Variable **`DB_TRANSPORT_NAME` (optional)**:
  - **leer lassen** → IdentityAccess nutzt seine Persistenz-Datenbank (`DB_NAME`) auch
    für Queues und Subscriptions (empfohlen für den eigenständigen Betrieb);
  - **gesetzt** → nur die gemeinsame Tabelle `dbo.SubscriptionRouting` liegt im
    Transport-Katalog — für kontextübergreifendes Pub/Sub (z. B. gemeinsam mit dem
    ams.project-Stack).
- **Einheitliche Subscription-Routing-Platzierung.** Migrator und Laufzeit adressieren
  `dbo.SubscriptionRouting` identisch; die Tabelle wird **idempotent** im richtigen
  Katalog angelegt — von IdentityAccess oder dem Platform-Stack, je nachdem, was zuerst
  läuft. Keine verwaisten Duplikat-Tabellen mehr.
- **`SERVICE_BUS_CATALOG` entfällt.** Der Subscription-Katalog wird jetzt aus
  `DB_TRANSPORT_NAME` abgeleitet (eine einzige Quelle der Wahrheit).

### Behoben
- **Kontextübergreifendes Pub/Sub im rc-Kanal repariert.** Die Host-Dienste lasen den
  Katalog aus `SERVICE_BUS_CATALOG`, der rc-Deploy lieferte aber `DB_TRANSPORT_NAME` —
  dadurch war der Katalog zur Laufzeit leer und `SubscriptionRouting` fiel je Dienst auf
  die eigene Datenbank zurück, was Pub/Sub still brach.
- **Fehlende Berechtigung ergänzt:** Der Laufzeit-Benutzer erhält jetzt zuverlässig
  `dbo.error` auf der Persistenz-Datenbank (zuvor eine latente Lücke).
- Entfernte tote/duplizierte Transport-Queue-Tabellen sowie die verwaiste Standard-Tabelle
  `IdentityAccess.SubscriptionRouting`.

### Hinweis für Betreiber
- Bestehende eigenständige Deployments bleiben unverändert (self-contained). Wer bisher
  `SERVICE_BUS_CATALOG` gesetzt hatte, stellt auf `DB_TRANSPORT_NAME` um.

## [3.2.0] – 2026-05-11

- Basisversion des als eigenständiges RSGO-Produkt ausgelieferten IdentityAccess
  (IdentityServer, AdminPortal, ClientHub, EmailSender). Frühere Historie ist in
  diesem Changelog nicht erfasst.
