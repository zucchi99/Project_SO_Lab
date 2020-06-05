# Project_SO_Lab
Nim Game: laboratory project for Operating System Project
Consegna
Il progetto qui assegnato consiste nel redigere un programma in linguaggio C
che operi nel modo descritto nella prossima sezione.
• Il progetto, facoltativo, svolto eventualmente in coppia o al massimo in
gruppi da tre persone, è da consegnare entro dieci giorni dalla data dell’appello di esame di Laboratorio di Sistemi Operativi al quale lo studente
si vuole presentare, all’indirizzo email nicola.gigante@uniud.it.
• Al progetto, se consegnato in tempo e di valutazione sufficiente, viene
assegnato un punteggio tra 1 e 5.
• Il punteggio viene aggiunto al voto del compito scritto di Laboratorio di
Sistemi Operativi, che avrà un massimo di 26 punti.
• Il progetto è dunque facoltativo, ma necessario per ottenere, nel corso di
Laboratorio, un voto maggiore di 26.
1
Testo del Progetto
Il progetto consiste nell’implementazione di una versione client/server del gioco
chiamato Nim1
. Il gioco, che si svolge tra due giocatori, prevede due pile di
pedine di lunghezza arbitraria. A turno ogni giocatore sceglie una delle due pile
e un numero arbitrario di pedine da rimuovere dalla pila scelta. Alla fine, vince
il giocatore che si trova a rimuovere l’ultima pedina.
Il progetto sarà diviso in un programma nimserver che si occupa di gestire
la partita, e un programma nimclient che fornisce l’interfaccia di gioco:
• nimserver resta in ascolto di connessioni da parte dei client su un socket
locale di dominio UNIX.
• Ogni singolo giocatore si collega al server utilizzando nimclient.
• Alla connessione del primo client, nimserver aspetta che se ne connetta
un secondo. Dopodiché, fa cominciare la partita gestendo la connessione
con i due client su un thread separato, tornando nel thread principale ad
aspettare altre connessioni per, eventualmente, gestire altre partite.
• All’inizio della partita, nimserver sceglie casualmente2
il numero di pedine presenti nelle due pile, e comunica i due valori ai due client, assieme
all’informazione di quale dei due giocatori deve muovere per primo (scelto
in modo arbitrario, ad es. il primo ad essersi connesso).
• Ad ogni turno, il server chiede di muovere al client a cui spetta il turno,
informandolo sul conteggio attuale di pedine rimaste nelle due pile.
• Quando la mossa di uno dei due giocatori fa terminare le pedine in entrambe le pile, il server informa entrambi i client del fatto che la partita è terminata, informando di chi ha vinto. I client riportano questa informazione
all’utente.
Entrambi i programmi devono essere il più robusti possibile: eventuali errori
di comunicazione (ad esempio se al server non si collega il client giusto) non
devono risultare in crash del programma o in comportamenti bizzarri. Bensì,
nimserver deve gentilmente chiudere la comunicazione con un client che comunichi in modo non valido, continuando a gestire correttamente eventuali altre
partite in corso. In ogni caso, se un client si disconnette per questo motivo
o di sua spontanea volontà, il server non deve subire interruzioni e il client
dell’avversario deve accorgersi della chiusura della partita informando l’utente
dell’accaduto. Non deve essere possibile per un client assicurarsi la vittoria in
modo fraudolento
