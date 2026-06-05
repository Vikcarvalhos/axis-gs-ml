# Axis + Copernicus Sentinel-2

Projeto da Global Solution da disciplina de IA e Machine Learning com dados de temática espacial.

## Sobre o projeto

O Axis é uma aplicação pensada para gerar grafos causais de consequências a partir de uma pergunta norteadora. O usuário informa um evento inicial e o sistema expande possíveis impactos em múltiplos níveis.

Exemplo conceitual:

> A taxa de natalidade do Japão sobe 4x.

A partir dessa pergunta, o Axis poderia gerar um grafo com consequências sociais, econômicas, logísticas, ambientais e estruturais.

Neste trabalho, conectamos essa ideia ao contexto espacial usando dados Copernicus/Sentinel-2. A proposta é transformar uma imagem de observação da Terra em uma camada de apoio para grafos de consequências em cenários de grandes eventos, como impacto de asteroide, tempestade solar, crise climática ou falha de infraestrutura espacial.

## Pergunta investigada

Usando apenas bandas espectrais Sentinel-2, é possível segmentar automaticamente a superfície observada e gerar um índice operacional interpretável para apoiar os grafos causais do Axis?

## Dataset

Foi utilizado um produto Copernicus/Sentinel-2 Level-2A da região da Nova Zelândia:

```text
S2C_MSIL2A_20260527T222541_N0512_R029_T59GML_20260528T031956.SAFE
```

O notebook espera que essa pasta `.SAFE` esteja na raiz do projeto.

Estrutura esperada:

```text
GS - Machine Learning/
├─ axis_copernicus_sentinel2_estudo.ipynb
├─ Relatorio_Axis_Copernicus_Sentinel2.pdf
├─ axis_copernicus_outputs/
└─ S2C_MSIL2A_20260527T222541_N0512_R029_T59GML_20260528T031956.SAFE/
```

## Arquivos principais

```text
axis_copernicus_sentinel2_estudo.ipynb
```

Notebook principal com código, gráficos, métricas e interpretação.

```text
Relatorio_Axis_Copernicus_Sentinel2.pdf
```

PDF explicativo da entrega.

```text
axis_copernicus_outputs/
```

Pasta com figuras, CSVs de métricas, perfis dos clusters e mapas reduzidos.

```text
S2C_MSIL2A_20260527T222541_N0512_R029_T59GML_20260528T031956.SAFE/
```

Produto Sentinel-2 usado como base de dados.

## Dependências

Instale as bibliotecas abaixo antes de executar o notebook:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn pillow rasterio nbformat nbclient
```

Dependências usadas:

| Biblioteca | Uso |
|---|---|
| `numpy` | manipulação numérica dos arrays das imagens |
| `pandas` | tabelas, métricas e exportação de CSVs |
| `matplotlib` | geração dos gráficos e mapas |
| `seaborn` | visualizações estatísticas |
| `scikit-learn` | K-Means, PCA, Random Forest e métricas |
| `pillow` | leitura dos arquivos `.jp2` do Sentinel-2 |
| `rasterio` | leitura de metadados geoespaciais, CRS, resolução e bounds |
| `nbformat` | suporte à leitura do notebook |
| `nbclient` | suporte à execução do notebook |

## Como executar o notebook

1. Clone ou baixe este repositório.

2. Confirme que a pasta `.SAFE` está na raiz do projeto:

```text
S2C_MSIL2A_20260527T222541_N0512_R029_T59GML_20260528T031956.SAFE/
```

3. Instale as dependências:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn pillow rasterio nbformat nbclient
```

4. Abra o notebook:

```text
axis_copernicus_sentinel2_estudo.ipynb
```

5. Execute as células em ordem.

Ao final, o notebook gera/atualiza a pasta:

```text
axis_copernicus_outputs/
```

Essa pasta contém:

- figuras usadas no relatório;
- métricas do K-Means;
- perfis dos clusters;
- importância das variáveis;
- mapas reduzidos em `.npz`.

## Metodologia resumida

1. Leitura das bandas Sentinel-2.
2. Redimensionamento para uma grade comum de 900 x 900 pixels.
3. Cálculo dos índices espectrais `NDVI`, `NDWI`, `NDBI` e `NBR`.
4. Conversão dos pixels válidos em dataset tabular.
5. Padronização das variáveis com `StandardScaler`.
6. Segmentação não supervisionada com K-Means.
7. Seleção de `k` usando Silhouette e Davies-Bouldin.
8. Comparação fraca com a camada `SCL`.
9. Uso de Random Forest como modelo auxiliar interpretável.
10. Criação do Índice Axis de risco operacional pós-evento.

## Principais resultados

- Produto: Sentinel-2 Level-2A.
- Data de aquisição: `2026-05-27T22:25:41.024Z`.
- Cobertura de nuvens: aproximadamente `19,58%`.
- Pixels válidos na grade reduzida: `386.931`.
- Melhor número de clusters: `k = 6`.
- Silhouette do melhor modelo: `0,3489`.
- Davies-Bouldin do melhor modelo: `0,9650`.
- Acurácia do Random Forest auxiliar: `0,9902`.

## Equipe

| Nome | RM |
|---|---:|
| Diana Letícia de Souza Inocencio | RM553562 |
| João Viktor Carvalho de Souza | RM552613 |
| Victor Augusto Pereira dos Santos | RM553518 |
