# Praxisbeispiel IT-SEC 2026
## Schritt 1: Aufklärung
Wie gewohnt, *wollen* wir herausfinden, ob und was sich auf unserem Ziel so befindet.  
Die IP-Adresse des Systems ist:  
$$127.0.0.1$$

<details>
  <summary>Hinweis</summary>
Versuche, (z.B. mit nmap) herauszufinden, welche Services oder Ports auf dem System offen sind. 
</details>

<details>
  <summary>Lösungsansatz</summary>

```bash
nmap -sV <ip>
nmap -sV -p 1024 65535 <ip>
```
</details>

## Schritt 2: Vorbereitung
Die Schwachstelle ist leider nicht am Service erkennbar.  
Möglicherweise war der Benutzer zu faul, den Standardport zu ändern?  

<details>
  <summary>Hinweis 2a</summary>

In Metasploit kann man gezielt nach Standardports von Exploits suchen.
```bash
msfconsole> search port:_____
```
</details>

<details>
  <summary>Hinweis 2b</summary>
die Schwachstellen gehören gewissermaßen zusammen, im Fokus steht aber ein **sandbox escape**.
</details>

<details>
  <summary>Hinweis 2c</summary>
Für eine Liste verfügbarer Payloads:

```bash
msfconsole> show payloads
```
verschiedene funktionieren, ich würde *meterpreter/reverse_shell* empfehlen wegen der Zusatzfunktionen.

</details>

## Schritt 3: Angriff!
Jetzt, wo das Ziel erkannt ist, können wir sie ausnutzen.
<details>
  <summary>Hinweis 2c</summary>
Für eine Liste verfügbarer Payloads:

```bash
msfconsole> show payloads
```
verschiedene funktionieren, ich würde *meterpreter/reverse_shell* empfehlen wegen der Zusatzfunktionen.

</details>

## 4. Schaden verursachen
Falls wir es in das System geschafft haben, könnten wir jetzt *poc*-artig Dateien ablegen.  

Wir könnten aber auch schauen, ob sich bestimmte Progamme auf dem System befinden, die unter fahrlässiger Handhabung zum Verhängnis werden können.
Gängige Passwortmanager bieten eine Druckfunktion.
Dafür erzeugen manche Programme eine HTML-Datei, die **nicht automatisch gelöscht** wird.

Suche nach Programmen, die du kennst.
Häufig werden solche Dateien standardmäßig im Dokumentenverzeichnis abgelegt,
falls der Nutzer kein anderes Verzeichnis angibt.

<details>
  <summary>Hinweis 4a</summary>
Bei Keepass gibt es diese Funktion, die DB beim exportieren als *HTML* oder *CSV* abzulegen.

```bash
meterpreter> search

```
<details>
  <summary>Suchhilfe</summary>
Bei Keepass gibt es diese Funktion, die DB beim exportieren als *HTML* oder *CSV* abzulegen.

```bash
meterpreter> search -f *keepass*/*.html -r
```
- -r Rekursiv (alle Verzeichnisse)
- -f Datei mit Namensmuster (inkl. Pfad)
</details>
</details>


