**UNIVERSIDADE FEDERAL DE SÃO CARLOS - *CAMPUS* SOROCABA** <br>
**CIÊNCIA DA COMPUTAÇÃO** <br>
**PROCESSAMENTO MASSIVO DE DADOS** <br>
PROFª. DRª. SAHUDY MONTENEGRO GONZÁLEZ
---
<img width="1012" height="568" alt="image" src="https://github.com/user-attachments/assets/740786cc-70e1-4869-9dcb-525cd1d4ead0" />
---

**PROJETO PRÁTICO** 

Grupo 12<br>
Relações de plantas e animais para cultivo eficiente <br>

**INTEGRANTES**

- Felipe Ottoni Pereira
- Letícia Almeida Paulino de Alencar Ferreira

### **1. DESCRIÇÃO DO TEMA** 

O plantio companheiro é uma prática agrícola baseada na combinação de diferentes espécies vegetais em um mesmo espaço, visando benefícios mútuos. Essa técnica contribui para a sustentabilidade da produção, pois reduz o uso de insumos químicos, melhora a saúde do solo e promove o controle natural de pragas. As interações entre as plantas podem ser benéficas, quando uma espécie auxilia no desenvolvimento da outra, seja repelindo pragas, atraindo polinizadores ou melhorando a disponibilidade de nutrientes, ou antagônicas, quando uma prejudica o desenvolvimento da outra, seja por competição por recursos, alelopatia ou atração de pragas indesejadas.

Além das relações diretas entre plantas, outros elementos entram nesse ecossistema agrícola, como insetos benéficos, que polinizam ou predam pragas, pragas específicas, que podem ser repelidas ou atraídas pelas plantas, nutrientes do solo, cuja disponibilidade pode ser alterada por algumas espécies, como as leguminosas, que fixam nitrogênio. Nesse sentido, entender essas relações pode fornecer insights úteis para práticas agrícolas mais produtivas, resilientes e sustentáveis, promovendo um manejo mais inteligente do solo e das espécies cultivadas. Dado que essas relações formam uma rede complexa de interações biológicas, o uso de tecnologias de dados é interessante para mapear, analisar e extrair conhecimento desse sistema.

### **2. OBJETIVO** 

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

### **3. TECNOLOGIAS**

**Neo4j**<br>
O armazenamento em Neo4j atuará na frente que visa explorar as relações entre as plantas para utilizar práticas como plantas companheiras e rotação de cultura para otimizar a produção de alguma planta, assim, com ele o usuario pode ter a informação sobre como plantar a cultura que desejar.

Escolhemos utilizar o Neo4j para armazenar e analisar dados sobre relações entre plantas, como no plantio companheiro e na rotação de culturas, pois permite modelar entidades (plantas, pragas, nutrientes) como nós e suas interações como arestas (ex: "atrai", "repele"). Sua abordagem orientada a grafos é ideal para navegar e consultar redes complexas, especialmente com a linguagem Cypher. Além disso, lida melhor com dados semi-estruturados e flexíveis, comuns nesse contexto, enquanto bancos relacionais exigiriam muitas tabelas e perderiam eficiência e flexibilidade.

**Esquema no Neo4j**

<div style="text-align: center;">
  <img width="853" height="557" alt="image" src="https://github.com/user-attachments/assets/54076d99-4186-42d3-8afb-c851f46306cd" />
</div>

<br>**MongoDB**<br>
O armazenamento no MongoDB atuará na frente que tem como objetivo indicar ao usuário onde e o que plantar, com informações sobre culturas plantadas em determinadas regiões e períodos. Escolhemos essa tecnologia por sua flexibilidade em lidar com dados heterogêneos e esquemas dinâmicos, o que é ideal para representar a produção agrícola em diferentes países, culturas e anos. Cada documento pode conter métricas variadas de produção, mesmo com campos ausentes ou inconsistentes. Isso facilita a análise de mercado e produção por região, permitindo consultas agregadas e comparações sem a complexidade de joins típicos em bancos relacionais. Além disso, o modelo pode evoluir com o tempo, incluindo novas variáveis conforme necessário, o que favorece análises históricas e comparativas.

**Esquema no MongoDB**

<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/ac6abf6c-85f0-4d3b-a318-1b7971aacdcd" alt="Imagem MongoDB" style="width: 30%;">
</div>

<br>**Apache Spark**<br>
O Apache Spark será utilizado, por meio do *Databricks Notebook*, como ferramenta de ETL para extrair dados de múltiplas fontes, transformá-los (limpeza, padronização, enriquecimento) e carregá-los no MongoDB e no Neo4j. Isso porque de acordo com as documentações no Mongo e Neo, existem conectores nativos para eles com o Spark. Além do ETL, o Spark também pensamos em utilizar para análises em larga escala, como agregações complexas e estatísticas relacionadas às relações entre plantas e pragas. 

**Fontes de Dados**<br>
Nossas fontes de dados, que encontramos até o momento, são tabelas [2] e artigos científicos sobre agroecologia, websites especializados em plantio consorciado [3] e [4] e datasets complementares sobre pragas e insetos benéficos, que ajudam a mapear quais espécies são repelidas ou atraídas.

### **4. FLUXOGRAMA**

<img width="1222" height="546" alt="image" src="https://github.com/user-attachments/assets/8b4bf77f-b3ea-44a7-9b1a-8a7084a3d644" />


### **5. Consultas**

MongoDB
- Qual a produção total de soja no Brasil do ano de 2010 até 2019?
- Qual a produção média da cultura de arroz no Japão, nos ultimos 5 anos?
- Quais culturas tiveram pouco rendimento na australia nos ultimos 3 anos?
- Listar o top 5 culturas com maior rendimento na europa
- Qual a cultura com maior quantidade de área colhida e onde foi colhida?
- Qual a média de area colhida de cacau na asia?
  

Neo4j
- Quais plantas ajudam outras plantas que repelem a praga X?
- Quais plantas da mesma categoria se atrapalham?
- Quais as plantas que mais ajudam as plantas da categoria Y? (ranking: top 3)
- Quais os gêneros de planta que oferecem maior variedade de mecanismos (analisar relação de mecanismo com gênero e com planta daquele gênero)
- Para cada planta, liste quantas ou quais plantas ela pode alcançar ajudar com até 2 saltos
- Qual o menor caminho entre a planta A e a planta B, usando relação AJUDA entre plantas (determinar a ordem em que elas devem estar dispostas umas com as outras)
- Plantas que oferecendo o mecanismo P ajudam outras plantas? (Pode identificar tanto plantas companheiras quanto rotação de 
cultura)

### **6. FONTES**

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
