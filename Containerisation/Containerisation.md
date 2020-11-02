@Leg-en

Docker
======

Containerisation
----------------

-   Software verpackt in standardisierte Einheiten für Entwicklung,
    Einsatz und Verteilung
    -   Eine solche Einheit ist ein Container
-   Ein Container ist eine Softwareeinheit, in das der gesamte Code und
    alle Abhängigkeiten gepackt werden
-   Software läuft so schnell und zuverlässig auch auf anderen Computer
    Systemen
-   Mehrere Container können auf einer Maschine laufen und teilen sich
    den gleichen OS kernel
    -   Jeder Container läuft trotzdem isoliert und unabhängig von den
        anderen
-   Container sind in der Regel wenige Megabyte groß
    -   Benötigen damit deutlich weniger Speicher als Virtual Machines
    -   Es gibt auch deutlich größere, einige R Container sind oft 1
        Gigabyte oder größer
-   Führende Containerisation Software: Docker

Quelle:  
[What is a
Container?](https://www.docker.com/resources/what-container)  
[How Docker Helps Development Teams](https://www.docker.com/use-cases)

Docker Alternativen
-------------------

-   rkt von CoreOS
    -   Rocket Ausgesprochen
    -   Stärkster Docker Konkurrent
    -   Vorstellung im Jahre 2014, Veröffentlicht 2016
    -   Entwickelt, weil die Ziele des Unternehmens andere sind als von
        Docker
    -   Punktet mit Sicherheitsfeatures
-   LXC
    -   Set aus Tools, Templates, Bibliotheken und Language Bindings
    -   Ermöglicht zugriff auf die Native Container Funktionalität des
        Linuxkernels
-   LXD
    -   Nachfolger von LXC
    -   Kann docker auch Ergänzen
-   Linux VServer, runC und viele andere

Quelle:  
[Alternativen zu Docker: Container-Plattform im
Überblick](https://www.ionos.de/digitalguide/server/knowhow/docker-alternativen-im-ueberblick/)
[App-Container: 5 professionelle Docker-Alternativen im
Überblick](https://t3n.de/news/docker-alternativen-container-783741/)

Docker — Meta Info
------------------

### Docker Geschichte

-   2013 ist Docker gestartet als Open Source Docker Engine
-   Es verbesserte bereits existierende Konzepte von Containern in der
    Linux welt
    -   Primitives bekannt als cgroups und namespaces
-   Durch den Erfolg folgte eine Partnerschaft mit Microsoft
    -   Docker verfügbar für Windows Server bzw., Docker Windows
-   2015 Spendete Docker die Container Spezifikation an die OCI, um
    einen standardisiertes Wachstum des Container Ökosystems zu
    ermöglichen
    -   OCI - Open Container Initiative
-   2017 Spendete Docker das Container Project an die CNCF
    -   CNCF - Cloud Native Computing Foundation

Quelle:  
[What is a
Container?](https://www.docker.com/resources/what-container)  
[How Docker Helps Development Teams](https://www.docker.com/use-cases)

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
    -   “It works on my machine!” — Unabhängigkeit von der Entwicklungs-
        / Laufzeitsumgebung
    -   Schnelles aufsetzen von Entwicklungsumgebungen für neue
        Entwickler
    -   Geeignet für Microservice Architektur
    -   Legacy Apps mit Docker
    -   ML
-   Sharing von Containern über Dockerhub

Quelle:  
[What is a
Container?](https://www.docker.com/resources/what-container)  
[How Docker Helps Development Teams](https://www.docker.com/use-cases)

### Docker Container Images & Container

-   Ein Docker Container Image ist eine kleine, alleinstehende und
    ausführbare Datei, welche alles beinhaltet, was sie braucht: Code,
    Laufzeitumgebung, System Tools, System Bibliotheken und
    Einstellungen
-   Ein Docker Container Image wird zur Laufzeit zu einem Docker
    Container
-   Container, die auf der Docker Engine laufen, sind:
    -   Standardisiert - Bilden den de facto Industrie standard
    -   “Lightweight” - sehr klein und effizient. Anwendungen benötigen
        kein eigenes Os und sparen daher Server und Lizenz Kosten
    -   Sicher - Docker Container sind voneinander strikt isoliert

Quelle:  
[What is a
Container?](https://www.docker.com/resources/what-container)  
[How Docker Helps Development Teams](https://www.docker.com/use-cases)

### Dockerhub

-   Docker Hub ist eine Plattform zum Teilen von Container Images
-   Betrieben von Docker
-   Docker Images stehen mit allen Dependencies direkt zum Download zur
    Verfügung
    -   Downloaden & Starten
-   Rechte Management — Freigeben für alle oder nur für das eigene Team
-   Automatisierte Erstellung von Container Images (Webhooks)
    -   Z. B. mit Github, bei jedem neuen Commit wird ein neues Docker
        Image online generiert

Quelle:  
[Docker Hub](https://hub.docker.com/)

Docker — Umsetzung
------------------

### Containerisation mit Docker

-   Voraussetzungen
    -   Docker Desktop installiert & konfiguriert
    -   Projekt zur Containerisation
-   Dockerfile erstellen
-   Docker Build
-   Docker Run

### Dockerfile

-   Enthält Anweisungen für den Container
-   Aufbau:

<!-- -->

    # Comment
    INSTRUCTION arguments

-   Nicht Case Sensitive jedoch ist die Konvention, dass die Aufgabe
    groß ist und das Argument klein
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

Quelle: [Get Started](https://docs.docker.com/get-started/part2/)

### Beispiel Dockerfile Erklärung

    FROM node:current-slim

Bezieht das offizielle Node Image als Ausgangs Image .

    WORKDIR /usr/src/app

Setzt das Arbeitsverzeichnis. Alle folgenden Aktivitäten gehen hiervon
aus.

    COPY package.json .

Kopiert die Package JSON (Enthält auflistung aller Node Modules).

    COPY package.json .

Führt npm install aus. Installiert entsprechend den Server.

    EXPOSE 8080

Expose weist Docker daraufhin, dass der Server auf dem Port 8080
reagiert. Entsprechend wird der Port freigegeben.

    CMD [ "npm", "start" ]

Führt Start Argumente aus.

    COPY . .

Kopiert das restliche Projekt.

Quelle:  
[Dockerfile
reference](https://docs.docker.com/engine/reference/builder/)

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
-   Zusätzliche Argumente möglich
    -   empfehlenswert:

<!-- -->

     -t NAME

-   Gibt dem Image einen Namen/Tag

-   Beispiele:

<!-- -->

    docker build .

Gebaut mit lokalem Dockerfile über PATH

     docker build https://github.com/Leg-en/Geosoft_Project

Gebaut mit Github Repository über URL

Quelle:  
[docker
build](https://docs.docker.com/engine/reference/commandline/build/)

### Docker Run

-   Format:

<!-- -->

     docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]

-   Es wird ein Image benötigt, um daraus ein Container zu erstellen
-   Der Optionsoperator ermöglicht es die Default werte des Entwicklers
    zu überschreiben
    -   Ebenso Default Docker Variablen können so überschrieben werden
    -   Wichtige Parameter:
        -   -a spezifiziert woran Docker das Container bindet
            -   STDIN, STDOUT und/oder STDERR
            -   Default sind STDIN und STDERR
        -   -d für Detached, lässt den Container im Hintergrund laufen
        -   -p für Port spezifiziert einen Port für den Container
        -   -i, lässt den Standard Input (STDIN) geöffnet, auch wenn der
            Prozess detached ist
        -   -t Legt eine pseudo TTY an.
            -   tty ist genutzt, um den Standardoutput eines Terminals
                zu überprüfen. -t erstellt entsprechend einen pseudo
                Standard Output
-   Für interaktive Prozesse (Im Terminal zum Beispiel) müssen - i und
    -t (auch -it möglich) zusammen genutzt werden
-   Alternativ: Über Docker Desktop Starten

Beispiel Mit Tags:

     docker run -a stdin -a stdout -i -t IMAGE

Quelle:  
[Docker run reference](https://docs.docker.com/engine/reference/run/)

### Docker rm

-   Format:

<!-- -->

     docker rm [OPTIONS] CONTAINER [CONTAINER...]

-   Entfernt einen oder mehrere Container
-   Alle gestoppten Container Löschen:

<!-- -->

     docker rm $(docker ps -a -q)

Quelle:  
[docker rm](https://docs.docker.com/engine/reference/commandline/rm/)

### Docker prune

-   Format:

<!-- -->

     docker system prune [OPTIONS]

-   Entfernt alle ungenutzten Container & Images

Quelle:  
[docker system
prune](https://docs.docker.com/engine/reference/commandline/system_prune/)

Docker Compose
--------------

-   Ist ein Tool um Anwendungen die aus mehreren Docker Containern
    bestehen zu Verwenden.
    -   Beispiel: Eigenes Projekt auf Node Basis mit einer Zusaätzlichen
        MongoDB. Node und MongoDB sind jeweil in eigenen Containern
        laufen aber mit docker compose zusammen
-   Vordefinierung der gesamt anwendung in der Docker-compose.yml
-   Starten der anwendung mit

<!-- -->

     docker-compose up [options] [--scale SERVICE=NUM...] [SERVICE...]

-   Genaueres Folgt in @Svub1 Vortag

[Overview of Docker Compose](https://docs.docker.com/compose/)

Binder
======

Mybinder
--------

-   Binder Project ist eine offene Community, welche es möglich macht,
    teilbare, interaktive und reproduzierbare Umgebungen zu erschaffen
-   Ein Binder (oder Binder Ready Repository) ist ein Code Repository,
    welches:
    -   Code oder Inhalte die ausgeführt werden sollen (z. B. Jupyter
        Notebook, R Scripte)
    -   Konfigurationsdateien für die Umgebung
        -   Binder benötigt diese, um den Code auszuführen
        -   Werden im Root Verzeichnis oder im Binder/ Verzeichnis
            platziert
-   BinderHUB ist eine Web Applikation welche solche Umgebungen
    erschafft
    -   Dafür nutzt es repo2docker um für jedes Repository ein eigenen
        Container zu erstellen und JupyterHub für die Interaktivität
-   Mybinder:
    <a href="https://mybinder.org/" class="uri">https://mybinder.org/</a>

Quelle:  
[binder](https://jupyter.org/binder)  
[Get started with
Binder](https://mybinder.readthedocs.io/en/latest/introduction.html)

repo2docker
-----------

-   repo2docker ist ein Tool, welches code repositories in Docker Images
    umwandelt
    -   repo2docker stellt direkt eine Zugriffsmöglichkeit via Jupyter
        zu Verfügung
        -   Es wird ein Link mit einem Token in der Befehlszeile zu
            Verfügung gestellt, womit der Zugriff ermöglicht wird
        -   Im Hintergrund läuft das Docker Image in einem Container
        -   Direkter Zugriff auf Dateien möglich
            -   Ebenso das ausführen von Code (Segmenten) in Jupyter
                Notebooks
-   Es definiert die “Reproducible Execution Environment Specification”
    (REES) welche genutzt wird um Regeln für die Konvertierung zu docker
    images definieren
    -   REES soll die Automatisierung von computergestützten Umgebungen
        erleichtern
    -   Soll ebenso von Menschen lesbar und umsetzbar sein
-   Frei downloadbar und anwendbar

Quelle:  
[The Reproducible Execution Environment
Specification](https://repo2docker.readthedocs.io/en/latest/specification.html)

Kubernetes
==========

-   Erfunden von Google und als 2014 Open Source zur Verfügung gestellt
-   Ist eine portable, erweiterbare Open-Source-Plattform zur Verwaltung
    von containerisierten Arbeitslasten und Services
-   Nutzen von Kubernetes
    -   Containerplattform
    -   Microservices-Plattform
    -   portable Cloud-Plattform
-   Ist eine containerzentrierte Managementum
    -   koordiniert Computer-, Netzwerk und Speicherinfrastruktur

Quelle:  
[Was ist
Kubernetes?](https://kubernetes.io/de/docs/concepts/overview/what-is-kubernetes/)
