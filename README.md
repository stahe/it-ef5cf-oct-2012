# Migrazione da NHibernate a Entity Framework 5 (ottobre 2012)

Questo documento illustra un'**architettura applicativa ASP.NET flessibile e scalabile**
e mostra come sostituire l'ORM **NHibernate** con **Entity Framework 5**
senza modificare il livello applicativo.

🌐 Il sito web associato è accessibile all'indirizzo: https://stahe.github.io/it-ef5cf-oct-2012/

---

## Contesto

**Entity Framework** è un ORM (Object Relational Mapper) originariamente creato da Microsoft
e reso open source nel luglio 2012.

In un corso su ASP.NET, questo documento si basa su un'architettura a livelli
che consente di aggiornare le tecnologie (ORM, DBMS) senza influire sull'applicazione.

---

## Architettura generale

Il diagramma sottostante mostra le architetture utilizzate nell'applicazione:

![Architettura ASP.NET con NHibernate e Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D200000183315F4E40.png)

![Architettura ASP.NET con Entity Framework 5 e Spring.NET](https://stahe.github.io/ef5cf-oct-2012/images/10000000000007D7000001825B1CF7DD.png)

### Descrizione dei livelli

- **Applicazione ASP.NET**  
  Livello di presentazione e logica di business.

- **DAO (Data Access Objects)**  
  Interfaccia di accesso ai dati utilizzata dall'applicazione.

- **ORM (NHibernate / Entity Framework)**  
  Responsabile della generazione di SQL e della comunicazione con ADO.NET.

- **ADO.NET**  
  Connettore al DBMS.

- **DBMS**  
  Sistema di gestione del database.

- **Spring.NET**  
  Garantisce l'integrazione dei livelli e l'iniezione delle dipendenze.

---

## Perché utilizzare un ORM?

Collegare il livello DAO direttamente ad ADO.NET rende l'applicazione dipendente dal DBMS:

- differenze nei tipi di dati;
- SQL proprietario;
- librerie specifiche del DBMS.

Con un ORM, cambiare il DBMS equivale essenzialmente a **modificare la configurazione**
dell'ORM. Il livello DAO rimane invariato.

---

## Ruolo di Spring.NET

Spring.NET consente:

- all'applicazione ASP.NET di ottenere un riferimento al livello DAO;
- la creazione di questo livello da un file di configurazione;
- la sostituzione di un'implementazione DAO con un'altra **senza modificare il codice**,
  a condizione che l'interfaccia rimanga la stessa.

---

## Scopo del presente documento

Dimostrare nella pratica che l'architettura:

- è **resiliente ai cambiamenti nel DBMS**;
- è **resiliente ai cambiamenti nell'ORM**;
- consente **la sostituzione di NHibernate con Entity Framework 5**
  senza modificare il livello dell'applicazione ASP.NET.

---

## Approccio seguito

La migrazione viene effettuata in diverse fasi:

1. Esplorazione di **Entity Framework 5** con diversi DBMS;
2. Creazione di un nuovo livello di accesso ai dati (**DAO2**);
3. Collegamento dell'applicazione ASP.NET esistente a questo nuovo livello DAO.

---

## Destinatari
- Sviluppatori ASP.NET
- Studenti e docenti di architettura del software
- Chiunque sia interessato alle architetture disaccoppiate e scalabili
---
## Licenza e utilizzo
Documento didattico destinato all'insegnamento e alla dimostrazione
di architetture applicative scalabili.
