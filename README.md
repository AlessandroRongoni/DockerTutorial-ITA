# DockerTutorial-ITA
# 🐳 Guida Completa: Come Usare Docker

![Docker Banner](doker_banner.png)

Questa guida ti accompagnerà passo dopo passo nell'utilizzo di Docker, dalla sua installazione alla creazione di immagini, container e molto altro.

---

## 📚 Indice

1. [Cos'è Docker?](#cos-e-docker)
2. [Prerequisiti](#prerequisiti)
3. [🔧 Installazione di Docker](#installazione-di-docker)
4. [📜 Comandi Base di Docker](#comandi-base-di-docker)
5. [🛠️ Creazione di un'immagine Docker](#creazione-di-unimmagine-docker)
6. [📦 Gestione dei Container](#gestione-dei-container)
7. [📋 Docker Compose](#docker-compose)
8. [🌐 Esempio Completo: Applicazione Web](#esempio-completo-applicazione-web)
9. [🔗 Risorse Utili](#risorse-utili)

---

## 🐋 Cos'è Docker?

Docker è una piattaforma che consente di creare, distribuire e gestire applicazioni in container. I container sono ambienti isolati che includono tutto ciò che un'applicazione necessita per funzionare, indipendentemente dal sistema operativo sottostante.

---

## ⚙️ Prerequisiti

Prima di iniziare, assicurati di avere:

- Un sistema operativo compatibile (Linux, Windows o macOS).
- Accesso amministrativo al tuo computer.
- Una conoscenza base della riga di comando.

---

## 🔧 Installazione di Docker

### Su Windows e macOS
1. Scarica Docker Desktop dal [sito ufficiale](https://www.docker.com/products/docker-desktop/).
2. Esegui il file di installazione e segui le istruzioni.
3. Una volta installato, avvia Docker Desktop e assicurati che sia in esecuzione.

### Su Linux
1. Aggiorna i pacchetti:
   ```bash
   sudo apt update
   sudo apt upgrade
   ```
2. Installa i pacchetti necessari:
   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```
3. Aggiungi il repository Docker:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
4. Installa Docker:
   ```bash
   sudo apt update
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```
5. Verifica l'installazione:
   ```bash
   docker --version
   ```

---

## 📜 Comandi Base di Docker

### Verifica che Docker funzioni correttamente:
```bash
docker run hello-world
```

### Lista dei container in esecuzione:
```bash
docker ps
```

### Lista di tutti i container (anche fermati):
```bash
docker ps -a
```

### Lista delle immagini disponibili:
```bash
docker images
```

### Avvio di un container:
```bash
docker run -d -p 8080:80 nome_immagine
```

### Stop di un container:
```bash
docker stop ID_container
```

### Rimozione di un container:
```bash
docker rm ID_container
```

### Rimozione di un'immagine:
```bash
docker rmi nome_immagine
```

---

## 🛠️ Creazione di un'immagine Docker

1. Crea un file chiamato `Dockerfile` nella directory del tuo progetto.
2. Esempio di un semplice `Dockerfile` per un'app Node.js:
   ```dockerfile
   # Usa un'immagine base
   FROM node:14

   # Imposta la directory di lavoro
   WORKDIR /app

   # Copia i file necessari
   COPY package.json .
   RUN npm install
   COPY . .

   # Espone la porta
   EXPOSE 3000

   # Comando per avviare l'app
   CMD ["npm", "start"]
   ```
3. Costruisci l'immagine:
   ```bash
   docker build -t nome_immagine .
   ```
4. Esegui l'immagine:
   ```bash
   docker run -p 3000:3000 nome_immagine
   ```

---

## 📦 Gestione dei Container

- **Avvia un container fermo:**
  ```bash
  docker start ID_container
  ```

- **Visualizza i log di un container:**
  ```bash
  docker logs ID_container
  ```

- **Accedi al terminale di un container in esecuzione:**
  ```bash
  docker exec -it ID_container bash
  ```

---

## 📋 Docker Compose

Docker Compose consente di definire e gestire applicazioni multi-container utilizzando un file YAML.

### Installazione
Se Docker Compose non è già installato:
```bash
sudo apt install docker-compose
```

### Esempio di `docker-compose.yml`
Un'applicazione web con Node.js e un database MySQL:
```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    depends_on:
      - db
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: mydb
```

### Comandi Compose
- Avvia i servizi:
  ```bash
  docker-compose up
  ```
- Stoppa i servizi:
  ```bash
  docker-compose down
  ```

---

## 🌐 Esempio Completo: Applicazione Web

Creiamo un'applicazione Node.js con Docker Compose.

1. **Struttura del progetto:**
   ```
   my-app/
   |-- Dockerfile
   |-- docker-compose.yml
   |-- package.json
   |-- index.js
   ```
2. **File `index.js`:**
   ```javascript
   const express = require('express');
   const app = express();

   app.get('/', (req, res) => {
     res.send('Ciao da Docker!');
   });

   app.listen(3000, () => {
     console.log('Server in esecuzione su http://localhost:3000');
   });
   ```
3. **Comandi per eseguire:**
   ```bash
   docker-compose up
   ```
4. Apri il browser su `http://localhost:3000`.

---

## 🔗 Risorse Utili

- [Documentazione ufficiale di Docker](https://docs.docker.com/)
- [Tutorial su Docker Compose](https://docs.docker.com/compose/)
- [Docker Hub](https://hub.docker.com/)
