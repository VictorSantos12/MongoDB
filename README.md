<img src="https://user-images.githubusercontent.com/61476935/137227890-529b5933-d40c-4eee-b819-e5e69c3abeb9.png">

<br>
<img src="https://img.shields.io/static/v1?label=MongoDb&message=DataBase&color=green&style=for-the-badge&logo=MongoDB"/>


O [MongoDB](https://www.mongodb.com/pt-br/what-is-mongodb) é um banco de dados orientado a documentos, NoSQL, desenvolvido e mantido pela MongoDB Inc que oferece a possibilidade de deployment local e cloud-hosted em diferentes versões, que podem ou não ser gratuitas.

Sendo bastante popular por ser uma alternativa as opções mais consolidadas de bancos de dados, especialmente os da Oracle, como SQL e MySQL. O Mongo oferece uma estrutura de armazenamento diferente de seus concorrentes, já que faz uso do JavaScript Object Notation, popular formato de intercâmbio de dados, mais conhecido como Json. Esse formato permite manter armazenado um mapa das informações chamado de documento, o que torna o processo de comunicação e tratamento dos dados mais simplificado.

A estrutura do Json consiste em um objeto compost de chaves, também chamados de campos, e valores. O valor de um campo pode conter um outro documento Json, um array, que pode conter uma série de outros documentos, ou mesmo outros arrays:

<img src="https://user-images.githubusercontent.com/61476935/137230375-5c5714f7-66d4-4ef5-b317-3b052e3440e3.png"/>

As vantagens de usar documentos são:

- Documentos (objetos) são correspondentes a tipos nativos de várias linguagens de programação.
- Documentos e matrizes incorporados reduzem a necessidade de junções caras.
- O esquema dinâmico suporta polimorfismo fluente.

O valor de um campo pode ser de qualquer tipo suportado pelo BSON data types. Por exemplo, o documento a seguir contém valores de diversos tipos:

    var mydoc = {
       _id: ObjectId("5099803df3f4948bd2f98391"),
       name: { first: "Alan", last: "Turing" },
       birth: new Date('Jun 23, 1912'),
       death: new Date('Jun 07, 1954'),
       contribs: [ "Turing machine", "Turing test", "Turingery" ],
       views : NumberLong(1250000)
    }

O exemplo acima conta com os seguintes tipos em suas respectivas chaves:

- _id contém um [ObjectId](https://docs.mongodb.com/manual/reference/bson-types/#std-label-objectid).
- name contém um documento incorporado que contém os campos primeiro e último.
- birth e death contêm valores do tipo Date.
- views contém um tipo <i>NumberLong</i>.


<h1>Collection</h1>


As collections para o MongoDB são como as tabelas para bancos de dados relacionais. Os documentos em que as informações são registradas são, por sua vez, armazenados em collections:

<img src="https://user-images.githubusercontent.com/61476935/137231179-29d86114-b76b-40c9-903f-5a0a3ab20918.png"/>

Caso uma collection não exista, o MongoDB irá criá-la caso um registro seja feito:

    db.myNewCollection2.insertOne( { x: 1 } )
    db.myNewCollection3.createIndex( { y: 1 } )

Ambas as operações <i>insertOne()</i> e <i>createIndex()</i> criam suas respectivas collections caso as mesmas já não existam. E para isso, o MongoDB possui alguns parâmetros de nomenclatura:


<h2>Restrições de Nomenclatura de Bancos de Dados</h2>


Para evitar possíveis conflitos, o MongoDB mantém padrões que tornam a criação de diferentes bancos de dados não conflitantes. Exemplo:

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


<h1>Instalação</h1>


O MongoDB está disponível em duas edições: Community e Enterprise, sendo mais recomendado fazer o download de uma versão community, já que a mesma é gratuita. O link a seguir disponibiliza diferentes versões para diferentes sistemas operacionais e suas restrições: [Installation](https://docs.mongodb.com/manual/installation/).

Em seguida, para que seja possível utilizar a Shell interface do MongoDB, faça o download da ferramenta <i>mongosh</i>, disponível no link a seguir: [mongosh](https://docs.mongodb.com/mongodb-shell/install/).

Após ambos os downloads, acesse o terminal e faça o run do seguinte comando:

    mongosh

E como resultado temos acesso a interface de linha de comando do mongosh, que conta com alguns detelhes sobre as instalações, contendo as versões instaladas e o Log ID do mongosh:

    Current Mongosh Log ID: 61678f008200fe466d146371
    Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000
    Using MongoDB:          5.0.3
    Using Mongosh:          1.1.0
    
    For mongosh info see: https://docs.mongodb.com/mongodb-shell/
    
    
    To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
    You can opt-out by running the disableTelemetry() command.
    
    ------
       The server generated these startup warnings when booting:
       2021-10-13T22:55:30.057-03:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
    ------
    
    test>

Além disso, quando acessamos a interface do mongosh, inicialmente já temos uma base de test criada por default. Para ver as informações que essa contém, use o comando a seguir:

    show dbs

Por padrão, temos os seguintes resultados a consulta:

admin     41 kB
config  61.4 kB
local     41 kB


<h2>Criando Um Banco de Dados</h2>



