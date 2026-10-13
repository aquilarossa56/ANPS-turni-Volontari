# ANPS Milano · Turni volontari

App web (PWA-ready, mobile first) per il calendario dei turni dei volontari A.N.P.S. Milano.
Sito statico (GitHub Pages) + database e login con [Supabase](https://supabase.com) (piano gratuito).

## Funzioni
- Login con **email + password** decise dall'amministratore
- Calendario mensile; i volontari vedono solo i turni **futuri** (giorno, nomi, ore); il **responsabile** (primo nome) è evidenziato
- Amministratore: nuovo turno (1–50 volontari, tipo di servizio), elenco volontari, logo, rimborso a servizio, riepilogo annuale (1 gen–31 dic), classifiche servizi/ore, export CSV
- I turni passati non sono cancellati: restano nelle statistiche

## Installazione
1. **Supabase**: crea un progetto → *SQL Editor* → incolla ed esegui `supabase/schema.sql`.
2. *Authentication → Users → Add user*: crea il tuo utente e uno per ogni volontario (email + password scelta da te).
3. Rendi te stesso amministratore (SQL Editor):
   `update public.profiles set role = 'admin' where email = 'tua-email@esempio.it';`
4. Copia *Project URL* e *anon key* (*Project Settings → API*) in `config.js`.
5. **GitHub**: carica questi file in un repository → *Settings → Pages → Deploy from branch → main / (root)*.
6. Apri l'indirizzo `https://<utente>.github.io/<repo>/` e accedi. Su cellulare: "Aggiungi a schermata Home".

## Note di sicurezza
- La `anon key` è pubblica per progetto: i dati sono protetti dalle regole RLS in `schema.sql`. Non inserire mai la `service_role key`.
- Tipo di servizio, note, rimborsi, elenco volontari sono leggibili solo dall'amministratore (lato database, non solo a schermo).
- Nell'elenco volontari inserisci la stessa email usata per l'accesso, così ognuno ritrova i propri turni.
- Dati personali: valuta l'informativa privacy (GDPR) per i volontari.
