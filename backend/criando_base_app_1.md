node -> executar scripts em js fora do browser
npm -> gerenciador de pacotes (instalar bibliotecas de terceiros no projeto)
yarn -> mais veloz que o npm e traz features a mais

choco install => cinst
PowerShell tem os comandos parecidos com os do Unix já configurados

arrow function -> função escrita de forma reduzida
req -> requisição que o usuário estiver enviando para a aplicação
res -> serve para devolver uma resposta para essa requisição

se passarmos essa função arrow fazia ela ficará executando um looping infinito, para devolver algo para o cliente(navegador) é preciso dar um return

Nessa primeira aula faremos o desenvolvimento da api rest(serviço que vai disponibilizar dados pro nosso frontend)

Json => estrutura de dados -> envia e recebe dados que ambos os lados(back e front) conseguem interpretar

express- microframework(conjunto de ferramentas prontas) que nos ajuda a definir rotas, entre outras coisas.

Métodos utilizados pela API Rest
GET => buscar informação do backend
POST => criar nova informação no backend
PUT => editar algumas informações (não conseguiremos acessar atraves do navegador, uma vez que por padrao o navegador não suporta executar dois métodos em conjunto, nesse caso seria o get e post, por isso usaremos outra ferramenta para acessar
métodos que utilizam outros métodos => Insomnia.rest
DELETE

server.js
{

> > const app = express(); //função

> > app.get("/", (req, res) => {
> > return res.json({ message: "Hello World" });
> > }); //rota para execução do código

> > app.listen(3333); //localhost:3333
> > }

Ex.: app.get("/users", (req, res) => {
return res.json({ idade: req.query.idade }); //usar o software insomnia, add em querys name:idade value:20

req.query => serve para acessar query params => utilizado com filtros
req.params => acessar routes params => utilizados para editar e deletar
{query params = mais utilizados para filtrar (dados que ficarão expostos na nossa url)}

Ex.:
{

> > app.put("/users/:id", (req, res) => {
> > return res.json({ id: req.params.id });
> > });

}

Add na própria url do Insomnia: http://localhost:3333/users/1

corpo da requisição (usado para criar ou editar)

req.body => serve para acessarmos o corpo da requisição

Ex.:
{

> > app.post("/users", (req, res) => {
> > return res.json(req.body);
> > });
> > }
> > Configuramos uma requisição POST no Insomnia, criamos um JSON na aba Body

Por padrão o express não interpreta Json's, então precisamos dizer para ele, dizemos através dessa linha de código

> > app.use(express.json());

Iremos separar as rotas num arquivo chamado "routes.js"
./ significa que é na mesma pasta

->O banco de dados que utilizaremos será o MongoDB porque ele é bem performático e trará velocidade para o nosso desenvolvimento
->Hospedagem de banco de dados gratuitos até 500GB
=>MondoDB Atlas
Criaremos um servidor que poderá ter vários bancos para várias aplicações diferentes.

Add uma dependecia no projeto 'mongoose'- biblioteca que facilitará o nosso trabalho com o mongodb

Utilizaremos MVC, no momento só model e controller
controller = regra de negócio (deverá ser extraida para design pattern) - recebe requisição, trata e devolve uma resposta
model = schema

Dentro dos Controllers temos os seguintes métodos: index(estamos criando um método que está criando uma listagem de sessões), show(listar uma unica), store, (criar uma unica) update, destroy

Spots (insomnia)
-> O formato JSON não suporta o envio de imagens para o backend
Utilizaremos o formato "Multipart Form" quando tivermos um upload dentro do requerimento
O express nao entende o multipart form, para isso utilizaremos a lib multer

uploads.js
Como o windows intepreta não interpreta a barra normal /, e sim, \, vamos utilizar o path.resolve e separar cada parte do caminho; Passar a variável global \_\_dirname como parâmetro, que informa o diretório atual.

Lembrando que tech é um array com várias Strings, é preciso separá-lo, para isso usamos o split, após percorremos esse array com map e para cada string realizaremos o tech.trim, que tirará os espaços antes e depois de uma string
techs: techs.split(',').map(tech => tech.trim())

=> Programa utilizado para fazer os protótipos (Sketch)

BookingController.js

> > module.exports = {
> > async store(req, res) {
> > const { user_id } = req.headers;
> > const { spot_id } = req.params;
> > const { date } = req.body;

> > const booking = await Booking.create({
> > user: user_id,
> > spot: spot_id,
> > date
> > });

Desse jeito ele retornará os números, e se quisessemos que ele retornasse os dados?
Basta adicionar essa linha de código, logo abaixo dessas ai, isso porque o mongo nos ajuda.

> > await booking.populate('spot').populate('user').execPopulate();

aprendemos relacionamento, bd, metodos http, json, upload de imagens.

add a depencencia cors, controlar os acessos ao backend
