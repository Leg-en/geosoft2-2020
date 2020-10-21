@Leg-en

Docker
======

Containerisation
----------------

-   Software verpackt in standardisierte Einheiten für Entwicklung,
    Einsatz und Verteilung
    -   Eine solche einheit ist ein Container
-   Ein Container ist eine Softwareeinheit in das der gesamte Code und
    alle Abhängigkeiten gepackt werden
-   Software läuft so schnell und zuverlässig auch auf anderen Computer
    Systemen
-   Mehrere Container können auf einer Maschine laufen und teilen sich
    den gleichen OS kernel
    -   Jeder Container läuft trotzdem Isoliert und unabhängig von den
        anderen
-   Container sind in der Regel wenige Megabyte groß
    -   Benötigen damit deutlich weniger Speicher als Virtual Machines
-   Führende Containerisation Software: Docker

Docker — Meta Info
------------------

### Docker Geschichte

-   2013 ist Docker Gestartet als Open Source Docker Engine
-   Es verbesserte bereits Existierende Konzepte von Containern in der
    Linux welt
    -   Primitives bekannt als cgroups und namespaces
-   Durch den Erfolg, folgte eine Partnerschaft mit Microsoft
    -   Docker Verfügbar Windows Server bzw, Docker Windows
-   2015 Spendete Docker die Container Spezifikation an die OCI um einen
    Standardisiertes wachstum des Container Ökosystems zu ermöglichen
    -   OCI - Open Container Initiative
-   2017 Spendete Docker das Containerd Project an die CNCF
    -   CNCF - Cloud Native Computing Foundation

### Docker

-   Docker ist eine Containerisation Software
-   Basic Funktionalität ist Kostenlos
    -   Pro Abos jedoch auch möglich
-   Desktop Software: Docker Desktop
    -   Desktop Anwendung für die schnelle Containerisation von
        Anwendungen
    -   Überprüft Code auf Schwachstellen
    -   Direkte Verbindung zu Azure möglich (Beta)
    -   Verfügbar für MacOS und Windows
-   Erlaubt verbesserte Entwicklung
    -   “It works on my machine!” — Unabhängigkeit von der Entwickungs /
        Laufzeitsumgebung
    -   Schnelles aufsetzen von Entwicklungsumgebungen für neue
        Entwickler
    -   Geeignet für Microservice Architektur
    -   Legacy Apps mit Docker
    -   ML
-   Sharing von Containern über Dockerhub

### Docker Container Images & Container

-   Ein Docker Container Image ist eine kleine, alleinstehende und
    ausführbare datei, welche alles beinhaltet was sie braucht: Code,
    Laufzeitumgebung, System Tools, System Bibliotheken und
    Einstellungen
-   Ein Docker Container Image wird zur laufzeit zu einem Docker
    Container
-   Container die auf der Docker Engine Laufen sind:
    -   Standardisiert - Bilden de Facto, den Industrie standard
    -   “Lightweight” - Sehr Klein und Effizient. Anwendungen benötigen
        kein eigenes Os und sparen daher Server und Lizenz Kosten
    -   Sicher - Docker Container sind voneinander strikt Isoliert

### Dockerhub

-   Docker Hub ist eine Plattform zum Teilen von Container Images
-   Betrieben von Docker
-   Docker Images stehen mit allen Dependencies direkt zum Download zur
    Verfügung
    -   Downloaden & Starten
-   Rechte Management — Freigeben für alle oder nur für das eigene Team
-   Automatisierte Erstellung von Container Images (Webhooks)
    -   Z.b. mit Github, bei jedem neuen Commit wird ein neues Docker
        Image Online generiert

Docker — Umsetzung
------------------

### Containerisation mit Docker

-   Voraussetzungen
    -   Docker Desktop Installiert & Konfiguriert
    -   Projekt zur Containerisation
-   Dockerfile erstellen
-   Docker Build
-   Docker Run

### Dockerfile

-   Enthält anweisungen für den Container
-   Aufbau:

<!-- -->

    # Comment
    INSTRUCTION arguments

-   Nicht Case Sensitive, jedoch ist die Konvention das die Aufgabe groß
    ist und das Argument klein
-   Kommentare mit \#
-   Abfolge von Schritten

### Beispiel Dockerfile

    # Use the official image as a parent image.
    FROM node:current-slim
    # Set the working directory.
    WORKDIR /usr/src/app
    # Copy the file from your host to your current location.
    COPY package.json .
    # Run the command inside your image filesystem.
    RUN npm install
    # Add metadata to the image to describe which port the container is listening on at runtime.
    EXPOSE 8080
    # Run the specified command within the container.
    CMD [ "npm", "start" ]
    # Copy the rest of your app's source code from your host to your image filesystem.
    COPY . .

Quelle:
<a href="https://docs.docker.com/get-started/part2/" class="uri">https://docs.docker.com/get-started/part2/</a>

### Beispiel Dockerfile Erklärung

    FROM node:current-slim

Bezieht das Offizielle Node Image als Ausgangs Image

    WORKDIR /usr/src/app

Setzt das Arbeitsverzeichnis, Alle folgenden Aktivitäten gehen hiervon
aus

    COPY package.json .

Kopiert die Package JSON (Enthält auflistung aller Node Modules)

    COPY package.json .

Führt npm install aus. Installiert Entsprechend den Server

    EXPOSE 8080

Expose weist docker daraufhin, dass der Server auf dem Port 8080
reagiert. Entsprechend wird der Port freigegeben

    CMD [ "npm", "start" ]

Führt Start argumente aus.

    COPY . .

Kopiert das restliche Projekt

### Docker Build

-   Format:

<!-- -->

    docker build [OPTIONS] PATH | URL | -

-   Baut Docker Images von einem Dockerfile und dem “Kontext”
    -   Der Kontext ist gesetzt im PATH oder URL
-   Die URL verweist entweder auf:
    -   Git Repositories
    -   pre-packaged Tarball Contexts
    -   Text Files
-   Zusätzliche Argumente Möglich
    -   Empfehlenswert:

<!-- -->

     -t NAME

-   Gibt dem Image einen Namen/Tag

-   Beispiele:

<!-- -->

    docker build .

Gebaut mit lokalem Dockerfile über PATH

     docker build https://github.com/Leg-en/Geosoft_Project

Gebaut mit Github Repository über URL

### Docker Run

-   Format:

<!-- -->

     docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]

-   Es wird ein Image benötigt um daraus ein Container zu erstellen
-   Der Options Operator ermöglicht es die Default werte des Entwicklers
    zu Überschreiben
    -   Ebenso Default Docker Variablen können so Überschrieben werden
    -   Wichtige Parameter:
        -   -d für Detached, Lässt den Container im Hintergrund laufen
        -   -p für Port, Spezifiziert einen Port für den Container
-   Alternativ: Über Docker Desktop Starten

### Docker rm

-   Format:

<!-- -->

     docker rm [OPTIONS] CONTAINER [CONTAINER...]

-   Entfernt einen oder mehrere container
-   Alle gestoppten Container Löschen:

<!-- -->

     docker rm $(docker ps -a -q)

### Docker rm

-   Format:

<!-- -->

     docker system prune [OPTIONS]

-   Entfernt alle ungenutzten Container & Images

Binder
======

-   Binder Project ist eine offene Comunity, welche es möglich macht,
    teilbare, interaktive und reproduzierbare umgebungen zu erschaffen
-   Ein Binder (oder Binder Ready Repository) ist ein Code Repository
    welches:
    -   Code oder Inhalte die Ausgeführt werden sollen (z.b. Jupyter
        Notebook, R Scripte)
    -   Konfigurationsdateien für die Umgebung
        -   Binder benötigt diese um den code auszuführen
        -   Werden im Root verzeichnis oder im binder/ verzeichnis
            Platziert
-   BinderHUB ist eine Web Applikation welche solche umgebungen
    erschafft
    -   Dafür Nutzt es repo2docker um für jedes Repository ein eigenen
        Container zu erstellen und JupyterHub für die Interaktivität
-   Mybinder:
    <a href="https://mybinder.org/" class="uri">https://mybinder.org/</a>

repo2docker
-----------

-   repo2docker ist ein tool, welches code repositories in Docker Images
    umwandelt
-   Es definiert die “Reproducible Execution Environment Specification”
    (REES) welche genutzt wird um regeln für die Konvertierung zu docker
    images definieren
    -   REES soll die Automatisierung von Computergestützten umgebungen
        erleichtern
    -   Soll ebenso von Menschen Lesbar und umsetzbar sein
-   Frei downloadbar und anwendbar

Quellen:
========

-   <a href="https://www.docker.com/resources/what-container" class="uri">https://www.docker.com/resources/what-container</a>
-   <a href="https://www.docker.com/use-cases" class="uri">https://www.docker.com/use-cases</a>
-   <a href="https://romannurik.github.io/SlidesCodeHighlighter/" class="uri">https://romannurik.github.io/SlidesCodeHighlighter/</a>
-   <a href="https://docs.docker.com/engine/reference/builder/" class="uri">https://docs.docker.com/engine/reference/builder/</a>
-   <a href="https://docs.docker.com/engine/reference/commandline/build/" class="uri">https://docs.docker.com/engine/reference/commandline/build/</a>
-   <a href="https://docs.docker.com/engine/reference/run/" class="uri">https://docs.docker.com/engine/reference/run/</a>
-   <a href="https://docs.docker.com/engine/reference/commandline/rm/" class="uri">https://docs.docker.com/engine/reference/commandline/rm/</a>
-   <a href="https://mybinder.readthedocs.io/en/latest/introduction.html" class="uri">https://mybinder.readthedocs.io/en/latest/introduction.html</a>
-   <a href="https://jupyter.org/binder" class="uri">https://jupyter.org/binder</a>
-   <a href="https://repo2docker.readthedocs.io/en/latest/specification.html" class="uri">https://repo2docker.readthedocs.io/en/latest/specification.html</a>
