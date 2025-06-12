* Beschreibe den Zweck der zwei Stages (Builder und Runner) in deinem multi-stage Dockerfile für die React App und warum dieser Ansatz für CI/CD vorteilhaft ist

A: - Builder baut die Anwendung, indem alle notwendigen Abhängigkeiten installiert und der Code kompiliert wird, sodass die fertigen statischen Dateien entstehen.
   - Runner ist eine Umgebung, der nur die gebauten Dateien übernimmt und bereitstellt.

Dieser Ansatz ist für CI/CD besonders vorteilhaft, weil er kleine, effiziente und sichere Images erzeugt, die nur das Nötigste enthalten. So werden Build- und Laufzeitumgebung sauber getrennt, was den Prozess schneller, stabiler und leichter wartbar macht.
   

* Wie hast du deine Docker Hub Zugangsdaten sicher in deiner CI-Plattform gespeichert? Warum ist das sicherer, als sie direkt in der 
Pipeline-Konfigurationsdatei im Git-Repository zu hinterlegen?

A: Ich habe in den Repository-Einstellungen meiner CI-Plattform zwei Secrets angelegt – eines für meinen Docker Hub Benutzernamen und eines für mein Access Token. Diese werden in der Pipeline verwendet, ohne dass sie im Code sichtbar sind. Das ist sicherer, weil die Zugangsdaten nicht im Repository gespeichert sind und so nicht versehentlich veröffentlicht werden können.

* Beschreibe die Abfolge der vier Hauptschritte, die deine erweiterte CI-Pipeline nun ausführt (Code holen, Image bauen, Login, Image pushen) und was jeder Schritt bewirkt. 

A: Zuerst wird der Code aus dem Repository geladen, damit die Pipeline mit dem aktuellen Stand arbeitet. Danach wird das Docker-Image aus dem React-Projekt gebaut. Anschließend loggt sich die Pipeline mit den gespeicherten Secrets bei Docker Hub ein. Zum Schluss wird das gebaute Image in das Docker Hub Repository hochgeladen, damit es von dort aus genutzt oder weiterverteilt werden kann.

* Welche Informationen hast du als Image-Tag verwendet, um das gebaute Docker Image eindeutig zu identifizieren? Warum ist ein eindeutiges Tag wichtig (besonders im Hinblick auf spätere Deployments)?

A: Ich habe als Image-Tag latest verwendet. So lässt sich jedes Image eindeutig zuordnen. Das ist wichtig, um bei Deployments genau nachvollziehen zu können, welche Version gerade verwendet wird – und bei Bedarf gezielt eine bestimmte Version ausrollen oder zurückrollen zu können.

* Stell dir vor, deine Pipeline würde fehlschlagen, weil das Docker Image nicht gepusht werden konnte. Welche Schritte würdest du zur Fehlersuche unternehmen? (Denke an Logs und Überprüfung von Secrets).

A: Ich würde zuerst die Logs in der CI-Pipeline ansehen, um die genaue Fehlermeldung zu finden. Dann würde ich prüfen, ob die Docker-Login-Daten als Secrets richtig gespeichert und in der Pipeline verwendet werden. Außerdem sicherstellen, dass das Access Token noch gültig ist und die nötigen Rechte zum Pushen hat.