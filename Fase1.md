# INFORME TÈCNIC: AVALUACIÓ I SELECCIÓ D'UN GESTOR DE CONTRASENYES CORPORATIU

---

## 1. Introducció i Justificació Tècnica

### 1.1. Riscos de les contrasenyes febles o reutilitzades
En l'entorn corporatiu actual, la gestió deficient de l'autenticació i la debilitat de les credencials continuen sent un dels principals vectors d'atac utilitzats pels ciberdelinqüents. La utilització de contrasenyes febles, perdedores de complexitat o la seva reutilització entre múltiples serveis exposa l'organització a riscos crítics de seguretat:

* **Atacs de Diccionari i Força Bruta:** Els atacants utilitzen eines automatitzades capaces de provar milions de combinacions de caràcters o paraules contingudes en diccionaris en qüestió de segons. Les contrasenyes curtes o basades en termes comuns són desxifrades de manera immediata.
* **Credential Stuffing:** Quan un servei extern o plataforma de tercers pateix una fuita de dades (*data breach*), les llistes de credencials filtrades (parelles de correu electrònic i contrasenya) són provades automàticament en altres serveis corporatius. Si un empleat reutilitza la mateixa clau per al correu d'empresa i per a un servei extern compromès, l'accés a la xarxa corporativa queda directament exposat.
* **Risc de Compromís d'Accés Privilegiat:** En el cas de l'equip tècnic, l'ús de credencials febles pot derivar en el compromís de comptes d'administrador, servidors crítics, bases de dades i panells de gestió d'infraestructura.

### 1.2. Funció del gestor de contrasenyes
Un gestor de contrasenyes corporatiu actua com un repositori centralitzat i xifrat d'alta seguretat que permet mitigar aquests riscos mitjançant:
* **Generació de contrasenyes d'alta entropia:** Permet crear i emmagatzemar claus úniques, aleatòries i complexes (més de 16-20 caràcters) per a cada servei sense necessitat que l'usuari les hagi de recordar.
* **Ús d'una sola Contrasenya Mestra (*Master Password*):** Redueix la càrrega cognitiva de l'empleat a una sola clau mestra robusta.
* **Protecció contra el *Phishing*:** Els gestors de contrasenyes integrats al navegador validen el domini web actual abans d'oferir l'emplenament automàtic, evitant la introducció involuntària de credencials en llocs web fraudulents.

---

## 2. Comparativa Tècnica: Bitwarden vs. KeePassXC

A continuació, es presenta una anàlisi comparativa entre una solució basada en el núvol (**Bitwarden**) i una solució d'escriptori local (**KeePassXC**):

| Criteri | Bitwarden (Online / Núvol) | KeePassXC (Offline / Escriptori) |
| :--- | :--- | :--- |
| **Arquitectura d'Emmagatzematge** | Base de dades centralitzada al núvol (SaaS o servidor *Self-Hosted*). | Fitxer local xifrat (`.kdbx`) emmagatzemat en disc o unitat de xarxa. |
| **Model de Seguretat** | Xifratge *End-to-End* (AES-256 / PBKDF2 o Argon2). Les dades es xifren i desxifren localment abans de la sincronització. | Xifratge local complet (AES-256, ChaCha20, Argon2). Sense exposició directa a la xarxa. |
| **Sincronització** | Automàtica i en temps real entre dispositius i plataformes. | Manual o mitjançant eines de sincronització de tercers (Nextcloud, Syncthing, SMB). |
| **Accés Multidispositiu** | Molt alt: Aplicació d'escriptori, extensió de navegador, app mòbil i accés Web Vault. | Mitjà/Baix: Aplicació d'escriptori nativa; requereix eines de tercers compatibles en mòbils. |
| **Model de Llicència i Cost** | Codi obert (*Open Source*). Model Freemium amb plans corporatius d'alt valor afegit. | 100% Codi obert i gratuït (GPLv3). Sense cap cost directament associat ni subscripcions. |
| **Portabilitat i Independència** | Dependent de la connectivitat a internet o servidor intern (tot i tenir memòria cau local). | Alta portabilitat del fitxer de base de dades `.kdbx` (executable des d'unitats USB o entorns *Air-Gapped*). |

---

## 3. Avantatges i Inconvenients (Model Online vs. Offline)

### 3.1. Model Online (Bitwarden)
* **Avantatges (Pros):**
  * **Usabilitat i productivitat:** Sincronització immediata entre ordinadors de treball, entorns virtuals i dispositius mòbils.
  * **Treball en equip:** Gestió de la Vault corporativa amb carpetes compartides, grups d'usuaris i control d'accés basat en rols (RBAC).
  * **Control i Auditoria:** Permet l'establiment de polítiques de seguretat obligatòries, registres d'accés i integració amb sistemes 2FA o Single Sign-On (SSO).
* **Inconvenients (Contres):**
  * Dependència de la connectivitat de xarxa per a la sincronització d'elements nous o canvis.
  * Major superfície d'atac teòrica en estar la infraestructura de sincronització exposada a la xarxa (mitigada pel xifratge de coneixement zero).

### 3.2. Model Offline (KeePassXC)
* **Avantatges (Pros):**
  * **Aïllament total (*Air-Gapped*):** Gran nivell de privadesa; la base de dades no toca mai servidors externs.
  * **Sense costos recurrents:** Llicència completament lliure sense límit de funcions ni usuaris.
  * **Control total del fitxer:** Ideal per a equips o servidors aïllats sense connexió a internet.
* **Inconvenients (Contres):**
  * **Risc de conflictes de versió:** Si diversos tècnics modifiquen el fitxer `.kdbx` simultàniament en una unitat de xarxa, es poden generar sobreescriptures de dades.
  * **Col·laboració complexa:** Dificultat per compartir credencials de manera àgil i auditada entre els membres de l'equip.
  * **Gestió de backup manual:** La responsabilitat de realitzar còpies de seguretat periòdiques recau exclusivament en l'usuari o l'administrador local.

---

## 4. Recomanació i Justificació

> **Decisió Recomanada:** Es proposa la selecció de **Bitwarden** com a gestor de contrasenyes corporatiu principal per al personal tècnic de l'organització.

### Justificació Tècnica
1. **Equilibri entre Seguretat i Operativa:** L'arquitectura de xifratge d'extrem a extrem (*zero-knowledge architecture*) garanteix que les credencials es desxifren únicament en la memòria local del dispositiu de l'usuari.
2. **Eficiència per a l'Equip Tècnic:** L'equip d'IT requereix accedir de forma ràpida i constant a múltiples entorns (infraestructura en el núvol, servidors locals, panells de gestió). La sincronització automàtica i la integració amb navegadors redueixen el temps de resposta i eviten pràctiques insegures (com l'ús de fulls de càlcul o fitxers de text).
3. **Escalabilitat Corporativa:** Permet la gestió centralitzada de permisos, facilitant l'alta i baixa d'empleats i la revocació d'accessos a credencials compartides de manera immediata.