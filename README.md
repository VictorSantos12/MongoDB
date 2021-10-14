<img src="https://user-images.githubusercontent.com/61476935/137227890-529b5933-d40c-4eee-b819-e5e69c3abeb9.png">

<br>
<img src="https://img.shields.io/static/v1?label=MongoDb&message=DataBase&color=green&style=for-the-badge&logo=MongoDB"/>


O MongoDB é um banco de dados orientado a documentos, NoSQL, desenvolvido e mantido pela MongoDB Inc. Sendo bastante popular por ser uma alternativa as opções mais consolidadas de bancos de dados, especificamente os da Oracle, como SQL e MySQL. O Mongo oferece uma estrutura de armazenamento diferente de seus concorrentes, já que faz uso do popular formato de intercâmbio de dados, o JavaScript Object Notation, popularmente conhecido como Json. Esse formato permite manter armazenado um mapa das informações, chamado de documento, o que torna o processo de comunicação e tratamento dos dados mais simplificado.

Além disso, o Mongo oferece a possibilidade de deployment local e cloud-hosted, permitindo ter acesso a esses recursos em diferentes versões, que podem ou não ser gratuitas. 

Como já foi dito, os registros no MongoDB seguem o padrão de estrutura do Json, que consiste em um objeto compost de chaves, também chamados de campos, e valores. O valor de um campo pode conter um outro documento Json, um array, que pode conter uma série de outros documentos, ou mesmo outros arrays:

<img src="https://user-images.githubusercontent.com/61476935/137230375-5c5714f7-66d4-4ef5-b317-3b052e3440e3.png"/>

As vantagens de usar documentos são:

- Documentos (objetos) são correspondentes a tipos nativos de várias linguagens de programação.
- Documentos e matrizes incorporados reduzem a necessidade de junções caras.
- O esquema dinâmico suporta polimorfismo fluente.

<h1>Collection</h1>

As collections para o MongoDB são como as tabelas para bancos de dados relacionais. Os documentos em que as informaçõe são registradas são, por sua vez, armanenados em collections:

<img src="https://user-images.githubusercontent.com/61476935/137231179-29d86114-b76b-40c9-903f-5a0a3ab20918.png"/>

Caso uma collection não exista, o MongoDB irá criá-la caso um registro seja feito.

    db.myNewCollection2.insertOne( { x: 1 } )
    db.myNewCollection3.createIndex( { y: 1 } )

Ambas as operações <i>insertOne()</i> e <i>createIndex()</i> criam suas respectivas collections caso as mesmas já não existam. E para isso, o MongoDB possui alguns parâmetros para que seja possível nomear uma conllection:


<h2>Restrições de Nomenclatura de Bancos de Dados</h2>


Para evitar possíveis conflitos, o MongoDB mantém padrões que tornam a criação de diferentes bancos de dados ou collections não conflitantes. Exemplo:

    mixedCase = db.getSiblingDB('salesDB')
    lowerCase = db.getSiblingDB('salesdb')
    
    mixedCase.retail.insertOne({ "widgets": 1, "price": 50 })

A operação <i>insertOne()</i> seria bem sucedida, e criaria implicitamente o banco de dados SalesDB. Caso a operação a seguir fosse utilizada, o resultado seria diferente:

    lowerCase.retail.insertOne({ "widgets": 1, "price": 50 })

A operação <i>insertOne()</i> tentaria criar a base de dados <i>saledb</i> e seria bloqueada pela restrição de nomenclatura, já que é preciso diferenciar mais que apenas o case quando nomeamos algo no MongoDB. Outras restrições são:

- Para deployments do MongoDB rodando no Windows, nenhuma base de dados pode ser nomeada utilizando os caracteres /\. "$*<>:|? ou ser null.

- Para deployments do MongoDB rodando no Unix ou Linux, nenhuma base de dados pode ser nomeada utilizando os caracteres  /\. "$ ou ser null.

- Os nomes dos bancos de dados não podem estar vazios e devem ter menos de 64 caracteres.


<h2>Restrições de Nomenclatura de Collections</h2>


Os nomes das collections devem começar com um sublinhado ou uma letra e não podem:

- Conter $.
- Ser um string vazio ("").
- Conter o identifcador null.
- Iniciar o prefixo system.

