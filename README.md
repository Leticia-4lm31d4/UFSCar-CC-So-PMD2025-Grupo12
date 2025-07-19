<hr>

Projeto de Disciplina – **Relações de plantas e animais para cultivo eficiente**

<hr>

Universidade Federal de São Carlos

Curso: Bacharelado em Ciência da Computação de Sorocaba

Disciplina: Processamento Massivo de Dados

Professora: Profa. Dra. Sahudy Montenegro González
<hr>

Grupo 12

**Integrantes**

- Felipe Ottoni Pereira - RA:
- Letícia Almeida Paulino de Alencar Ferreira - RA: 800480

<hr>

**Resumo:**

>de 3 a 4 linhas explicando o que o projeto faz

<hr>

**1. DESCRIÇÃO DO TEMA** 

O plantio companheiro é uma prática agrícola baseada na combinação de diferentes espécies vegetais em um mesmo espaço, visando benefícios mútuos. Essa técnica contribui para a sustentabilidade da produção, pois reduz o uso de insumos químicos, melhora a saúde do solo e promove o controle natural de pragas. As interações entre as plantas podem ser benéficas, quando uma espécie auxilia no desenvolvimento da outra, seja repelindo pragas, atraindo polinizadores ou melhorando a disponibilidade de nutrientes, ou antagônicas, quando uma prejudica o desenvolvimento da outra, seja por competição por recursos, alelopatia ou atração de pragas indesejadas.

Além das relações diretas entre plantas, outros elementos entram nesse ecossistema agrícola, como insetos benéficos, que polinizam ou predam pragas, pragas específicas, que podem ser repelidas ou atraídas pelas plantas, nutrientes do solo, cuja disponibilidade pode ser alterada por algumas espécies, como as leguminosas, que fixam nitrogênio. Nesse sentido, entender essas relações pode fornecer insights úteis para práticas agrícolas mais produtivas, resilientes e sustentáveis, promovendo um manejo mais inteligente do solo e das espécies cultivadas. Dado que essas relações formam uma rede complexa de interações biológicas, o uso de tecnologias de dados é interessante para mapear, analisar e extrair conhecimento desse sistema.

**2. OBJETIVO** 

O principal objetivo deste projeto é desenvolver um sistema de apoio à decisão para o setor agrícola com duas frentes complementares para gerar um cultivo eficiente:

1. **Frente de Análise de Mercado:** Realizar análises de produção agrícola por região, com base em dados históricos de culturas. Essa frente busca fornecer suporte à decisão quanto à escolha de culturas mais promissoras para investimento e onde plantar elas, com base em métricas como crescimento, demanda e produtividade.

2. **Frente Ecológica:** Modelar e analisar as relações ecológicas entre plantas, considerando aspectos como:
- Cultivos companheiros e antagônicos;
- Interações com pragas, insetos e outros animais;
- Papel de plantas no fornecimento de nutrientes, como fixação de nitrogênio e retenção de umidade no solo.

Essa frente visa auxiliar agricultores e pesquisadores no planejamento de cultivos consorciados, promovendo práticas sustentáveis, aumento da produtividade e proteção ambiental. <br>
Portanto em resumo o objetivo é gerar insights para um cultivo eficiente, eficiente de um ponto de vista de quais culturas investir, quais culturas estão em alta e com demanda no mercado agrícola e posteriormente eficiência de um ponto de vista de como otimizar a produção das culturas definidas pelos insights passados, por meio das práticas de plantio companheiro e rotação de cultura.

Já os objetivos técnicos são:
- Representar e analisar redes ecológicas complexas utilizando bancos de dados orientados a grafos (Neo4j);
- Integrar as tecnologias de dados Neo4j, MongoDB e Apache Spark;
- Demonstrar a viabilidade técnica dessa arquitetura híbrida, explorando o melhor de cada tecnologia no contexto da agricultura de precisão e sustentável.

**3. FONTE DE DADOS**<br><br>
>Atualizar aqui falando mais sobre os datasets <br>
Nossas fontes de dados, que encontramos até o momento, são tabelas [2] e artigos científicos sobre agroecologia, websites especializados em plantio consorciado [3] e [4] e datasets complementares sobre pragas e insetos benéficos, que ajudam a mapear quais espécies são repelidas ou atraídas. <br><br>
>
**3.1 Datasets usados para a frente ecológica de plantio companheiro (Neo4j):** <br> <br>
- companion_plant_wikipedia___after_prepro-1: 
<br> Essa é a principal tabela usada para o povoamento no neo4j,as outras tabelas servem como auxiliares para incrementar essa tabela ou auxiliar na limpeza e tratamento dela.
  - *Common name*: campo com o nome usual da planta (planta podendo representar uma espécie de planta, um gênero de planta ou uma categoria de planta).
  - *Type*: campo que representa uma categoria na qual a planta está incluída.
  - *Scientific name*: campo com o nome científico da planta.
  - *Helps*: campo com uma lista das plantas que a planta representada em *"Common name"* ajuda.
  - *Helped by*: campo com as plantas que são ajudadas pela planta representada em *"Common name"*.
  - *Attracts*: Campo com uma lista dos animais que são atraídos pela planta.
  - *-Repels/distracts*: Campo com uma lista dos animais que são repelidos pela planta.
  - *Avoid*: campo com todas as plantas que atrapalham a planta representada em *"Common name"*.
  - *Comments*: campo com uma descrição sobre detalhes e características da planta e de suas relações com outras plantas
<br>
<p align="center">
<img width="1314" height="412" alt="image" src="https://github.com/user-attachments/assets/915edf90-7d02-49e9-b5ee-500640d26c13" /> 
</p>
<br> <br>

- tabela_extra_plantas_companheiras___Mecanismos: 
<br> tabela feita analisando a descrição da coluna *"Comments"* da tabela principal para extrair os tipos de mecanismos de cada planta e adicionar a coluna *Mecanism* na tabela principal
  - *Plants*: nome usual das plantas.
  - *Mecansim*: lista de mecanismos que essa planta oferece.
<br>
<p align="center">
<img width="713" height="193" alt="image" src="https://github.com/user-attachments/assets/cc45b029-8ff6-4172-b8f4-14cb43f3a251" />
</p>
<br> <br>

- tabela_extra_plantas_companheiras___taxonomia: 
<br> tabela que contém relações de plantas que estão dentro de determinado grupo, serve como uma tabela extra para incrementar as relações de plantas que estão dentro de determinada categoria, indo além da relação definida pela coluna Type na tabela principal
  - *from*: contém o nome da categoria.
  - *to*: contém o nome da planta dentro da categoria.
<br>
<p align="center">
<img width="282" height="185" alt="image" src="https://github.com/user-attachments/assets/b9d44755-c6b7-415e-b3ce-f3a7ca61f673" /> 
</p>  
<br> <br>

- tabela_extra_plantas_companheiras___caracteristicas_relacoes: 
<br> tabela extra construída a partir de detalhes da coluna Comments na tabela principal. A tabela estabelece relações expecíficas extras com alguns motivos do porquê algumas plantas ajudam outras.
  - *Plant 1*: contém a planta que ajuda
  - *Plant 2*: contém a planta que é ajudada
  - Caracteristica/beneficio: contém o motivo ou benefício trazido
<br>
<p align="center">
<img width="604" height="216" alt="image" src="https://github.com/user-attachments/assets/8edd0594-dc0c-4d9f-aa61-3cbc2e98589c" /> 
</p>
<br> <br>

- synonym: tabela para substituir palavras por sinônimos para que seja possível fazer a junção de tabelas.
  - *name*: nome a ser substituido
  - *synonym*: sinônimo
<br> <br>
<p align="center">
<img width="250" height="337" alt="image" src="https://github.com/user-attachments/assets/d48d5c6d-a99a-48ee-bcf8-d426efed6810" /> 
</p>  
<br><br>

**4. TECNOLOGIAS E COMO FORAM IMPLEMENTADAS**

> Fazer uma mini intro da seção aqui

<br>**Apache Spark**<br><br>
O Apache Spark será utilizado, por meio do *Databricks Notebook*, como ferramenta de ETL para extrair dados de múltiplas fontes, transformá-los (limpeza, padronização, enriquecimento) e carregá-los no MongoDB e no Neo4j. Isso porque de acordo com as documentações no Mongo e Neo, existem conectores nativos para eles com o Spark. Além do ETL, o Spark também pensamos em utilizar para análises em larga escala, como agregações complexas e estatísticas relacionadas às relações entre plantas e pragas. 

<hr>

**Neo4j**<br><br>
O armazenamento em Neo4j atuará na frente que visa explorar as relações entre as plantas para utilizar práticas como plantas companheiras e rotação de cultura para otimizar a produção de alguma planta, assim, com ele o usuario pode ter a informação sobre como plantar a cultura que desejar.

Escolhemos utilizar o Neo4j para armazenar e analisar dados sobre relações entre plantas, como no plantio companheiro e na rotação de culturas, pois permite modelar entidades (plantas, pragas, nutrientes) como nós e suas interações como arestas (ex: "atrai", "repele"). Sua abordagem orientada a grafos é ideal para navegar e consultar redes complexas, especialmente com a linguagem Cypher, permitindo uma visualização mais clara. <br>
As relações ficam como o foco, sendo propriedades navegáveis diretamente, permitindo consultas baseadas em caminhos e uma capacidade de compreender não apenas os dados, mas também as relações entre eles. Além disso, lida melhor com dados semi-estruturados e flexíveis, comuns nesse contexto, enquanto bancos relacionais exigiriam muitas tabelas e perderiam eficiência e flexibilidade.

**Esquema no Neo4j**

<div style="text-align: center;">
  <img alt="image Neo4j" src="./img/esquemaNeo4j.png" />
</div>

<br>

**Implementação**



<hr>

**MongoDB**<br><br>
O armazenamento no MongoDB atuará na frente que tem como objetivo indicar ao usuário onde e o que plantar, com informações sobre culturas plantadas em determinadas regiões e períodos. Escolhemos essa tecnologia por sua flexibilidade em lidar com dados heterogêneos e esquemas dinâmicos, o que é ideal para representar a produção agrícola em diferentes países, culturas e anos. Cada documento pode conter métricas variadas de produção, mesmo com campos ausentes ou inconsistentes. Isso facilita a análise de mercado e produção por região, permitindo consultas agregadas e comparações sem a complexidade de joins típicos em bancos relacionais. Além disso, o modelo pode evoluir com o tempo, incluindo novas variáveis conforme necessário, o que favorece análises históricas e comparativas.

**Esquema no MongoDB**

```javascript
_id: "38"
continente: "africa" pais: "cabo verde"
ano: 1982
▾ culturas: Array (36)
  ▾ 0: Object
    nome: "oilcrops"
    producao_(tonnes): 10082 area_colhida_(ha): 3124
    rendimento_(hg/ha): 32273
  ▾ 1: Object
    nome: "onions, dry" producao_(tonnes) : 300
    area_colhida_(ha): 20
    rendimento_(hg/ha): 150000
```

**Implementação**



<hr>

<br>**5. FLUXOGRAMA DO SISTEMA**<br>

>Explicar o fluxograma

<img width="1222" height="546" alt="image" src="https://github.com/user-attachments/assets/8b4bf77f-b3ea-44a7-9b1a-8a7084a3d644" />

<br>**6. CONSULTAS E RESULTADOS**<br>

**MongoDB**

Definições importantes:
1. Rendimento: o quanto foi produzido de um produto, por unidade de área colhida. 
2. Produção: quantidade total colhida de um produto.
3. Área colhida: extensão de terra de onde a produção foi efetivamente colhida. Área plantada != Área colhida

```shell
db.producao_agricula_final.countDocuments()
> 12390
```

- Quais culturas tiveram pouco (rendimento menor que 10.000 hg/ha) rendimento na Austrália nos últimos 3 anos?

```shell
db.producao_agricola_final.aggregate([
  { $match: { pais: "australia", ano: { $gte: 2016 } } },
  { $unwind: "$culturas" },
  { $match: { "culturas.rendimento_(hg/ha)": { $lt: 10000 } } },
  {
    $project: {
      ano: 1,
      cultura: "$culturas.nome",
      rendimento: "$culturas.rendimento_(hg/ha)"
    }
  }
])
  
> {
    _id: '17179870612',
    ano: 2016,
    cultura: 'safflower seed',
    rendimento: 5928
  }
  {
    _id: '17179870612',
    ano: 2016,
    cultura: 'canary seed',
    rendimento: 6793
  }
```
  
- Listar o top 5 culturas com maior produção (toneladas) na Europa (últimos 5 anos)

```shell
db.producao_agricola_final.aggregate([
  { $match: { continente: "europa", ano: { $gte: 2015, $lte: 2019 } } },
  { $unwind: "$culturas" },
  { $match: { "culturas.producao_(tonnes)": { $ne: null } } },
  {
    $project: {
      cultura: "$culturas.nome",
      producao: "$culturas.producao_(tonnes)",
      pais: 1,
      ano: 1
    }
  },
  { $sort: { producao: -1 } },
  { $limit: 5 }
])

>{
  _id: '42949674287',
  pais: 'russian federation',
  ano: 2017,
  cultura: 'cereals, total',
  producao: 131289930
}
{
  _id: '51539608850',
  pais: 'russian federation',
  ano: 2019,
  cultura: 'cereals, total',
  producao: 117868242
}
{
  _id: '25769805096',
  pais: 'russian federation',
  ano: 2016,
  cultura: 'cereals, total',
  producao: 117751078
}
```
  
- Qual a cultura com maior quantidade de área colhida (hectare)? Onde foi colhida? (últimos 10 anos)

```shell
db.producao_agricola_final.aggregate([
  { $match: { ano: { $gte: 2009, $lte: 2019 } } },
  { $unwind: "$culturas" },
  { $match: { "culturas.area_colhida_(ha)": { $ne: null } } },
  {
    $project: {
      cultura: "$culturas.nome",
      area: "$culturas.area_colhida_(ha)",
      pais: 1,
      continente: 1,
      ano: 1
    }
  },
  { $sort: { area: -1 } },
  { $limit: 1 }
])

> {
  _id: '779',
  continente: 'asia',
  pais: 'china, mainland',
  ano: 2015,
  cultura: 'cereals, total',
  area: 103281871
}
```

- Qual cultura teve uma grande produção no Brasil em 2018?

```shell
db.producao_agricola_final.aggregate([
  { $match: { pais: "brazil", ano: 2018 } },
  { $unwind: "$culturas" },
  { $match: {"culturas.producao_(tonnes)": { $ne: null } } },
  {
    $project: {
      cultura: "$culturas.nome",
      producao: "$culturas.producao_(tonnes)"
    }
  },
  { $sort: { producao: -1 } },
  { $limit: 1 }
])

> {
  _id: '34359738851',
  cultura: 'sugar cane',
  producao: 747060316
}
```

<br>

**Neo4j**
- Das plantas que repelem lesmas quais outras plantas atrapalham e oferecem risco para o seu cultivo?
```shell
MATCH (p2:plant) -[r:`repels/distracts`]-> (a:animal)
WHERE a.name = 'slugs'
OPTIONAL MATCH (p2) -[h:avoid]-> (p1)
RETURN p1, p2, r, a, h
```
  
- Qual o menor caminho para gerar uma disposição física benéfica entre duas plantas específicas? (o que plantar ao lado do que)
```shell
MATCH p = shortestPath((p1:plant {name: "pumpkin"}) -[:helps*1..5]-> (p2:plant {name: "strawberry"}))
WHERE ALL(node IN nodes(p) WHERE node:plant)
```
  
- Quais são as plantas que ajudam a batata por meio da fixação de nitrogênio?
```shell
MATCH (p1:plant) -[o:offers]-> (m:mecanism {name: 'nitrogen fixation'})
MATCH(p1)-[h:helps]->(p2 {name: "potato"})
RETURN p1, p2, h
```
  
- Quais são as plantas que mais ajudam plantas que são ervas?
```shell
MATCH (p1:plant) -[:helps]-> (p2:plant)
MATCH (p2) <-[:contains]- (c:category {name: 'herb'})
RETURN p1.name AS plant, count(p1) AS help_count
ORDER BY help_count DESC
LIMIT 5
```

<hr>

**6. CONCLUSÕES**



**7. DIFICULDADES**



**8. FONTES**

1. Companion Planting | Portland Nursery. Disponível em: <https://www.portlandnursery.com/veggies/companion-planting>.
2. Rotação de culturas: objetivos, vantagens e desvantagens. Disponível em: <https://brasilescola.uol.com.br/geografia/rotacao-culturas.htm>.
3. WIKIPEDIA CONTRIBUTORS. List of companion plants.  <‌https://en.wikipedia.org/wiki/List_of_companion_plants#>
4. HTTPS://WWW.FACEBOOK.COM/MARTHASTEWART. Companion Planting Is the Key to a Thriving Vegetable Garden—Here’s How to Pair Varieties to Deter Pests and Attract Pollinators. Disponível em: <https://www.marthastewart.com/8379510/companion-planting-guide>.
5. 14 Vegetables You Should Never Plant Together. Disponível em: <https://www.marthastewart.com/vegetables-to-never-plant-together-8425391>.
6. GOVERNMENT, N. T. Companion planting. Disponível em: <https://nt.gov.au/environment/home-gardens/companion-planting>.
7. MOMENI, M. Crop Production. Disponível em: <https://www.kaggle.com/datasets/imtkaggleteam/crop-production>. Acesso em: 18 jun. 2025.
8. HUANG, S. Maintain a Companion Plant Knowledge Graph in Google Sheets and Neo4j | Towards Data Science. Disponível em: <https://towardsdatascience.com/maintain-a-companion-plant-knowledge-graph-in-google-sheets-and-neo4j-4142c0a5065b/>. Acesso em: 18 jun. 2025.
9. COMPANION_PLANT_WIKIPEDIA. companion_plant_wikipedia. Disponível em: <https://docs.google.com/spreadsheets/d/1U4K93EeOU6V4SZ9AgI3wOeV4kgdW9TmKSY_pIypDA-A/edit#gid=0>. Acesso em: 18 jun. 2025.
10. PATEL, Y. Vegetables Cultivation Data Exclusive. Disponível em: <https://www.kaggle.com/datasets/ysthehurricane/vegetables-cultivation-data-exclusive?select=vegetablecropNPK.csv>. Acesso em: 18 jun. 2025.

---

Sorocaba, 2025
