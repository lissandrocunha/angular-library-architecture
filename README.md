# angular-library-architecture

### criar o projeto

Criar o projeto sem criar a aplicação, e sem os arquivos de teste
`ng new angular-library-architecture --create-application=false --skipTests=true --prefix app-libraries`

### criar uma biblioteca dentro do projeto

Cria-se a biblioteca dentro da pasta do projeto criado:
`ng g library app-lib --skip-install --prefix app-lib`
`ng g library app-lib-core --skip-install --prefix app-lib-core`

### configurar

remover o conteúdo da pasta lib dentro a biblioteca criada
`cd app-lib`
`cd app-lib-core`

corrigir as informações dos "paths" no arquivo tsconfig.json

> "paths": {
> "@app/app-lib/_": [
> "projects/app-lib/app-lib/_",
> "projects/app-lib"
> ],
> "@app/app-lib": [
>
> > "dist/app-lib/app-lib/_",
> > "dist/app-lib"
> > ],
> > "@app/app-lib-core/*": [
> > "projects/app-lib-core/app-lib-core/*",
> > "projects/app-lib-core"
> > ],
> > "@app/app-lib-core": [
> > "dist/app-lib-core/app-lib-core/_",
> > "dist/app-lib-core"
> > ]
> > },

### criando uma feature para uma biblioteca

adicionar os pacotes dos esquemas do ng-samurai
`npm i -D ng-samurai`

criando a feature a
`cd app-lib`
`ng g ng-samurai:generate-subentry src/lib/feature-a --gm false --gc false`

criando um service no feature a
`ng g s .\src\lib\feature-a\a`

criando a feature b
`ng g ng-samurai:generate-subentry src/lib/feature-b --gm false --gc false`

criando um service no feature b
`ng g s .\src\lib\feature-b\b`

criando a feature c
`ng g ng-samurai:generate-subentry src/lib/feature-b --gm false --gc false`

criando um service no feature c
`ng g s .\src\lib\feature-c\c`

### compilar a biblioteca

se houver apenas uma biblioteca basta executar o comando
`ng build`

caso contrário será necessário informar o nome da biblioteca que se deseja compilar
`ng build app-lib-core`

ou alterar o arquivo 'angular.json' adicionando as bibliotecas que se deseja compilar com o comando 'ng build'

> "scripts": {
> "ng": "ng",
> "start": "ng serve",
> "build": "ng build app-lib && ng build app-lib-core",
> "build-all-prod": "ng build app-lib --prod && ng build app-lib-core --prod ",
> "watch": "ng build --watch --configuration development",
> "test": "ng test"
> },

### References

https://tomastrajan.medium.com/the-best-way-to-architect-your-angular-libraries-87959301d3d3
