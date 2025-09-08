📖 Coding Style – TestSuite CoDeSys
1. Struttura del progetto
	• Application → contiene la logica e i test.
	• Utility → funzioni comuni (UT_Assert..., UT_LogResult, ecc.).
	• Test FB → FB_Test_<NomeFunzione> per ogni funzione da validare.
	• Program Runner → PRG_TestRunner, unico punto di ingresso che richiama tutti i test.


2. Naming convention
	• Funzioni/FB di test: UT_<Azione>_<Tipo>
		○ UT_AssertEqual_REAL, UT_AssertEqual_INT, UT_LogResult.
	• FB di test specifici: FB_Test_<NomeFunzione>
		○ FB_Test_ClampF, FB_Test_Deadband.
	• Program runner: sempre PRG_TestRunner.
	• Variabili globali del framework: prefisso UT_
		○ UT_Failures, UT_Log, UT_LogIndex.
	• Variabili input POU: iniziale maiuscola (Actual, Expected, Label).
	• Variabili interne POU: iniziale minuscola (ok, msg, count).
	• Nomi descrittivi, niente sigle inutili: meglio ValvePosition che vp.


3. Stile del codice
	• Indentazione: 4 spazi.
	• IF/ELSE/END_IF sempre allineati.
	• Commenti: brevi, in italiano o inglese, ma solo dove serve (non ripetere il codice).
		○ ✅ // verifica che il valore resti entro i limiti
		○ ❌ // esegue IF
	• Un POU = una responsabilità (no “god functions”).


4. Assert e logging
	• Tutti i test devono usare funzioni UT_Assert... → niente confronti hardcoded nel codice di test.
	• Ogni assert:
		○ verifica la condizione,
		○ genera un messaggio standard (“OK” o “FAIL: expected…, got…”),
		○ aggiorna automaticamente i contatori/log con UT_LogResult.
	• Il FB di test non fa concat manuali: scrive solo righe di assert.


5. Organizzazione dei test
	• Ogni FB_Test_* deve avere un flag Done per eseguire i test una volta sola.
	• Risultati disponibili in:
		○ UT_Failures (contatore globale),
		○ UT_Log[0..UT_LogIndex-1] (array di messaggi).
	• Il PRG_TestRunner richiama tutti i FB_Test_* registrati.


6. Commit e repository
	• Export Application in PLCopenXML → è la fonte di verità su Git.
	• Mai committare file binari .project, .compiled-library, ecc.
	• Ogni commit deve contenere:
		○ Modifica funzionale chiara (es. “aggiunto UT_AssertEqual_INT”).
		○ Test aggiornati se cambi logica.


7. Filosofia
	• Leggibilità prima dell’ottimizzazione.
	• Consistenza > originalità: meglio tutti i nomi nello stesso stile che 10 stili diversi.
	• Piccoli passi: aggiungi test e moduli uno alla volta, con commit frequenti.
