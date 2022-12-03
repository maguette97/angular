# Hello

Ce projet a été généré avec [Angular CLI] version 12.2.18.

## Development server

Exécutez `ng serve` pour un serveur de développement. Accédez à `http://localhost:4200/`. L'application se rechargera automatiquement si vous modifiez l'un des fichiers source.

## Code scaffolding

Exécutez `ng generate component nom-composant` pour générer un nouveau composant. Vous pouvez également utiliser `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Exécutez `ng build` pour compiler le projet. Les artefacts de construction seront stockés dans le répertoire `dist/`.


## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

## Création du fichier dockerfile
FROM node:14.17.3 as builder : je donne la version du nodejs
WORKDIR /usr/src/app
COPY package.json package-lock.json ./ : je copie les fichiers de configuration
RUN npm install
COPY . .
RUN npm run build --prod

FROM nginx:1.17 : je précise la version du nginx
COPY --from=builder ${WORK_DIR}/dist/hello /usr/share/nginx/html : builder l'application vers mon serveur nginx sur docker

J'ouvre le terminal et j'exécute la commande : 
docker build . -t sidjz/hello
