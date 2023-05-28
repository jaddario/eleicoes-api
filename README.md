# Case Eleições Presidenciais de 2014

Projeto de estudo criado com a intenção de praticar assuntos relacionados à criação de API's, bem como uso de frameworks
como Redis, Testcontainers e Feign.

## Cenário

Estamos no dia 5 de outubro de 2014, dia de votação do primeiro turno das eleições para presidente e o TSE
acaba de liberar um arquivo num formato compacto com os resultados do primeiro turno e votação de todos os
candidatos em todos os municípios do Brasil. Um partido político encomenda a criação de um site de
exploração dos votos em todos os níveis de unidades político administrativas do Brasil para entender como foi
a distribuição dos seus votos entre regiões, estados, mesorregiões, microrregiões e municípios e te dá uma
semana para implementar a solução.

## Desafio

Implementar uma API que retorne o número de votos de todos os candidatos/partidos por unidades político
administrativa junto com informações geográficas com as fronteiras das unidades em formato GeoJson.
O retorno da API em si é livre para sua decisão porém a estrutura de URLs não. Ela deve seguir exatamente o
seguinte padrão:

**Retornar informações dos votos nas regiões:**
```http
GET /api/eleicao/2014/presidente/primeiro-turno/
```
**Retornar informações dos votos nos estados das regiões {Regiões}:**
```http
GET /api/eleicao/2014/presidente/primeiro-turno/{Regiões}
```
**Retornar informações dos votos nas mesorregiões das regiões {Regiões} e estados {UFs}:**
```http
GET /api/eleicao/2014/presidente/primeiro-turno/{Regiões}/{UFs}
```
**Retornar informações dos votos nas microrregiões das regiões {Regiões}, estados {UFs} e mesorregiões
{Mesorregiões}:**
```http
GET /api/eleicao/2014/presidente/primeiro-turno/{Regiões}/{UFs}/{Mesorregiões}
```
**Retornar informações dos votos nos municípios das regiões {Regiões}, estados {UFs}, mesorregiões
{Mesorregiões} e microrregiões {Microrregiões}:**
```http
GET /api/eleicao/2014/presidente/primeiro-turno/{Regiões}/{UFs}/{Mesorregiões}/{Microrregiões}
```

Cada uma das URLs precisa retornar o número total de votos de todos os candidatos agregados no próximo
nível de unidade político administrativa começando pelas regiões até municípios. As variáveis nas URLs podem
ser o código, sigla ou nome da unidade
Exemplos de chamadas possíveis:

```http
GET /api/eleicao/2014/presidente/primeiro-turno/SE
GET /api/eleicao/2014/presidente/primeiro-turno/SE/RJ
GET /api/eleicao/2014/presidente/primeiro-turno/SE/RJ/Metropolitana do Rio de Janeiro
GET /api/eleicao/2014/presidente/primeiro-turno/SE/RJ/Metropolitana do Rio de Janeiro/Rio de Janeiro
```

Deve ser possível também selecionar mais de uma unidade em qualquer nível. As unidades devem ser
separadas por pipe ‘|’, exemplos:

```http
GET /api/eleicao/2014/presidente/primeiro-turno/SE|S
GET /api/eleicao/2014/presidente/primeiro-turno/SE|S/RJ|SP|SC
```

Para atender as necessidades do frontend você está livre para criar qualquer outro endpoint adicional.