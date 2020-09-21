# Windows installation with Docker

### the command: `$ npm run dev --noDocker` doesn't work on windows.

### [Install Docker Desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)

#### After installation run the commands:

```
$ npm install -g @greenpress/cli
$ greenpress create my-app
$ cd my-app
```

- Go to `compose` folder and change the name of the `.env.example` file to `.env`

- Run:

```
$ npm run dev:docker
```

  <p>
  If you get the error : `Cannot start service greenpress: Ports are not available...`
  go to `docker-compose.local.yml` and comment line 17 or 18 depending on which is the non available Port.<br>
  Run agin `npm run dev:docker`
  </P>

- run:

```
docker ps
```

- Copy the id of the container : `compose_greenpress`

- run:

```
  docker exec {id} npm run populate-db

```

- Now greenpress should be running on your localhost 3000 port

Go to `localhost:3000/gp-admin`
and sign in with:

- username: `test@test.com`
- password: `admin`
