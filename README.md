## Windows‑Hinweis: %HOME% setzen

Damit Emacs unter Windows den SSH‑Konfigurationsordner findet (`%USERPROFILE%\.ssh`),
muss die Umgebungsvariable `%HOME%` explizit gesetzt werden:

Das passiert mit
Erweiterte Systemeinstellungen ->
Umgebungsvariablen ->
Systemvariablen ->
HOME → %USERPROFILE%

## TRAMP-Methode `/sshtt:` – OpenSSH unter Windows mit erzwungener TTY

Windows-OpenSSH verhält sich in TRAMP-Sitzungen anders als unter Linux. 
Insbesondere wird keine TTY zugewiesen, was zu Problemen mit Shell-Initialisierung, 
PATH-Verhalten und Remote-Kommandos führen kann.

Die Methode `/sshtt:` erzwingt mit `-tt` eine echte TTY und verhält sich damit 
identisch zu Linux-SSH.

### Emacs-Konfiguration

```elisp
(add-to-list 'tramp-methods
               '("sshtt"
                 (tramp-login-program "ssh")
                 (tramp-login-args (("-tt") ("%h")))
                 (tramp-remote-shell "/bin/bash")
                 (tramp-remote-shell-args ("-c"))
                 (tramp-default-port 22)))
