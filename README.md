# eslint-prittier-typescript
![Adicionando o projeto ao repositório do GitHub](https://res.cloudinary.com/practicaldev/image/fetch/s--QHbKowFk--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ph911resnofxjl5ynsln.jpg)

## Adicionando/Clonando um repositório

Sempre que vou iniciar um projeto, gosto de começar criando já meu repositório, e depois clonando o projeto.
O primeiro passo é acessar o GitHub, acessar sua conta e adicionar um novo repositório.
Agora vamos adicionar esse repositório localmente:
~~~
git clone https://github.com/USER_NAME/REPO_NAME.git
~~~

Agora devemos conectar nosso repositório local ao remoto, para isso utilizamos o seguinte comando:
~~~
git remote add origin git@github.com:USER_NAME/REPO_NAME.git
~~~
Em seguida criamos nossa branch principal:
~~~
git branch -M main
~~~
desde outubro de 2020 o GitHub passou a utilizar main ao invés de master, veja aqui

E por fim subimos para o repositório remoto nosso projeto recém-criado:
~~~
git push -u origin main
~~~
Projeto adicionado ao GitHub, quando finalizar o projeto é usar os comenados!
~~~
git status 
git add . 
git commit -a -m atualizado
~~~


![Criando o projeto React](https://res.cloudinary.com/practicaldev/image/fetch/s--ORt9s9Rx--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/72tgzouj3mzox2mrrc0f.png)

## Criando o projeto React 

Depois dessa configuração, vamos criando nosso projeto React, nesse exemplo vou usar o Create-React-App:
~~~
npx create-react-app my-app --template typescript
~~~

>é indicado utilizar npx pois garante que estaremos utilizando a ultima versão do create-react-app.
>my-app é o nome do projeto e pode ser substituído por qualquer coisa desde que possua apenas letras minúsculas.

Finalizada a instalação podemos acessar a pasta do projeto, eu gosto de criar logo a basta:
~~~
cd my-app
npm start
~~~
Projeto criado, hora de começarmos a configurá-lo para uso!


![Configurando o ESLint](https://res.cloudinary.com/practicaldev/image/fetch/s--pKSFygHT--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i49va9ntnx02ynrkbpue.jpeg)

## Configurando o ESLint

Essa costuma ser a parte que eu me perco quando configuro novos projetos, mas novamente, se seguirmos a documentação de cada uma das bibliotecas não tem erro!

Começando pelo ESLint, devemos utilizar o seguinte comando:
~~~
yarn add eslint -D
~~~
> usamos -D para adicionar o ESLint como dependência de desenvolvimento já que quando nosso código for para produção ele não servirá de nada

E em seguida já inicializamos ele com:
~~~
npx eslint --init
~~~
> esse passo costuma mudar um pouco de acordo com as atualizações que saem para o ESLint, não se desespere se tiver alguma configuração que não mencionei aqui, em caso de dúvidas só pesquisar no Google e entender melhor o que está sendo solicitado!

Agora começamos a configurar o ESLint, a primeira pergunta é referente a como iremos utilizar o ESLint em nosso sistema
~~~
? How would you like to use ESLint? ... 
  To check syntax only // apenas para checagem de sintaxe
  To check syntax and find problems // para checagem de sintaxe e encontrar problemas
> To check syntax, find problems, and enforce code style // para checagem de sintaxe, encontrar problemas e reforçar estilo de escrita
~~~
aqui eu aconselho a selecionar a ultima opção (navegue com as setas e confirme com o enter!) mas fica ao seu critério

Depois devemos escolher qual tipo de módulos nosso projeto usa, nesse caso como estamos lidando com React é a primeira opção mesmo:
~~~
? What type of modules does your project use? ... 
> JavaScript modules (import/export)
  CommonJS (require/exports)
  None of these
~~~
No próximo passo selecionamos qual framework estamos utilizando, novamente será a primeira opção:
~~~
? Which framework does your project use? ...       
> React
  Vue.js
  None of these
~~~
A próxima pergunta é sobre o TypeScript, como estamos configurando o projeto com ele é só selecionar Yes:
~~~
? Does your project use TypeScript? » No / Yes
~~~
No próximo passo devemos selecionar onde nosso código irá rodar, no caso do React será sempre no navegador, então é só dar enter e seguir pro próximo passo:
~~~
? Where does your code run? ...  (Press <space> to select, <a> to toggle all, <i> to invert selection)
√ Browser
  Node
~~~
Agora somos solicitados a escolher um estilo a ser utilizado no projeto, devemos escolher entre um existente, criar um estilo ou utilizar um próprio, eu sempre escolho utilizar um existente e opto por utilizar o do AirBNB:
~~~
? How would you like to define a style for your project? ... 
> Use a popular style guide
  Answer questions about your style
  Inspect your JavaScript file(s)
~~~
E por fim escolhemos o formato do nosso arquivo de configuração, novamente uma escolha pessoal, mas eu sempre opto pelo JSON pela facilidade do auto-complete do VSCode:
~~~
? What format do you want your config file to be in? ... 
  JavaScript
  YAML
> JSON
~~~
Encerradas as configurações o **ESLint** vai perguntar se você deseja instalar as dependências utilizando o **npm**, como nosso projeto está utilizando o **yarn** aqui você tem duas opções:

* selecionar **Yes**, apagar o arquivo package.lock.json gerado após a instalação e rodar yarn para instalar as dependências no arquivo yarn.lock

* selecionar **No**, copiar a lista de dependências descrita e instalar as mesmas utilizando o yarn add ... (não esquecer de adicionar o -D caso opte por essa opção)

Agora temos nosso arquivo  .eslintrc criado e podemos começar a editar ele, mas antes só mais um passo.

Vamos instalar a biblioteca eslint-import-resolver-typescript que permite importar arquivos .ts/.tsx e algumas outras funcionalidades dentro do nosso projeto, novamente seguindo a [documentação] é só usar o comando:
~~~
yarn add -D eslint-plugin-import @typescript-eslint/parser eslint-import-resolver-typescript
~~~
> nesse comando ele tenta instalar duas bibliotecas que já estão instaladas, mas não tem problema

E em seguida devemos atualizar nosso arquivo .eslintrc, é só adicionar uma configuração à chave rules e uma à chave settings (caso não exista é só criar abaixo da última chave):
~~~
...
"rules": {
  ...
  "import/no-unresolved": "error"
},
"settings": {
  "import/resolver": {
    "typescript": {}
  }
}
...
~~~
ESLint configurado, vamos para o ultimo passo.

![Configurando o Prettier](https://res.cloudinary.com/practicaldev/image/fetch/s--TELSordu--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v1wh98ygdvjw582agh7x.png)

## Configurando o Prettier
Aqui iremos instalar duas dependências para configurar o Prettier junto do ESLint, a primeira desabilita as regras conflitantes entre o Prettier e o ESLint e a segunda transforma o Prettier e suas configurações em regras do ESLint, assim conseguimos integrar os dois, vamos lá:
~~~
yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
~~~ 
Agora iremos atualizar nosso arquivo .eslintrc novamente, basta adicionar uma linha à nossa chave extends e uma à nossa chave plugins:
~~~
"extends": [
  "plugin:react/recommended",
  "airbnb",
  "plugin:@typescript-eslint/recommended",
  "plugin:prettier/recommended"
],
"plugins": [
  "react", 
  "react-hooks", 
  "@typescript-eslint", 
  "prettier"
]
~~~
Caso você queira ainda pode adicionar um arquivo .prettierrc para modificar suas configurações do prettier

