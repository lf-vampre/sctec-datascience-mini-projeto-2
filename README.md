![Logos](./images/logos.png)

<br>
<br>

## 💻 Curso Datascience - Visualização de Dados e Business Intelligence. 

Mini Projeto Avaliativo - Módulo 2 - Semana 7

Aluno: Luiz Felipe F V Vieira

<br>
<br>

## 🔍 ETL / AED / BI: "Dashboard Analítico de Compras Públicas em Saúde (BPS - 2020 a 2026)" 
Utilizando o banco de dados público do Ministério da Saúde que reúne informações de compras públicas e privadas de medicamentos e dispositivos médicos.
(https://dadosabertos.saude.gov.br/dataset/bps)

<br>

---

### 🎯 Propósito

> O desafio consiste em desenvolver um dashboard analítico para acompanhar as compras de medicamentos e dispositivos médicos registradas no Banco de Preços em Saúde (BPS) entre os anos de 2020 e 2026. O **objetivo** é praticar o pipeline de dados completo desde a aquisição dos dados até a disposição em um dashboard de BI. 

> Para tal proposta os dados foram baixados do site do Ministério da Saúde em arquivos distintos de cada ano (2020 a 2026), preparados e concatenados em um único conjunto de dados histórico e realizadas as etapas de ETL, AED e visualização no Google Data Studio (antigo Looker). 

<br>

---

### 📦 Entregáveis

> O Projeto deverá ser entregue com os seguintes resultados:

<br>

1. - [ ] Uma base consolidada com os arquivos do BPS referentes aos anos de 2020 a 2026

2. - [ ] Um dashboard desenvolvido preferencialmente no Data Studio - Looker Studio.

3. - [ ] Um arquivo `README.md` com a documentação do projeto.

4. - [ ] Um vídeo de apresentação com duração máxima de 5 minutos.

5. - [ ] A publicação do projeto completo no GitHub (Versionamento com branch e commit).

6. - [ ] Arquivo `.ipynb` em Python (Jupyter Notebook) estruturado com as transformações e análises.

<br>

---

### ⚙️ Requisitos Funcionais (RF)

> O projeto deverá contemplar os seguintes sprints / etapas:

<br>

- [ ] RF01: Sprint 1: Entendimento do problema e dos dados

- [ ] RF02: Sprint 2: Preparação e concatenação das bases

- [ ] RF03: Sprint 3: Definição das métricas e dos KPIs

- [ ] RF04: Sprint 4: Construção do dashboard

- [ ] RF05: Sprint 5: Análise dos resultados

- [ ] RF06: Sprint 6: Organização e publicação


<br>

---

## 1. Objetivo do projeto

> Construir um pipeline de dados completo (ETL, Análise Exploratória e Modelagem em Arquitetura Medalhão) e um dashboard analítico interativo para monitorar, analisar e dar transparência às compras públicas de medicamentos e dispositivos médicos registradas no Banco de Preços em Saúde (BPS) entre 2020 e 2026.

<br>

O projeto visa transformar os dados brutos do BPS em uma solução de Business Intelligence baseada em KPIs, gráficos e filtros interativos para responder às seguintes questões de negócio:

* **Evolução Temporal:** Acompanhamento dos valores totais registrados ao longo dos anos.
* **Distribuição Geográfica e Institucional:** Identificação dos estados, municípios e órgãos com maior volume financeiro.
* **Curva de Produtos:** Mapeamento dos medicamentos e dispositivos médicos mais adquiridos.
* **Mercado fornecedor:** Análise de participação de fornecedores e fabricantes nas aquisições.
* **Variação de Preços:** Monitoramento de preços unitários entre produtos, instituições, regiões e períodos.
* **Modalidades de Compra:** Avaliação dos formatos de aquisição mais utilizados.
* **Oportunidades de Investigação:** Identificação de discrepâncias relevantes de preços para auditoria e gestão.

*Nota de contexto:* A identificação de variações de preços busca apontar oportunidades de investigação e não comprova, isoladamente, sobrepreço ou irregularidade. As divergências podem decorrer de fatores como especificações do fabricante, unidade de fornecimento, volume loteado, logística regional e momento da negociação.

<br>

---

## 2. Contextualização do problema

> A dispersão e o volume dos dados brutos de compras públicas de saúde dificultam o acompanhamento dos gastos, a comparação de preços praticados e a identificação de assimetrias de mercado entre diferentes entes federativos e períodos.

<br>

A gestão de suprimentos na saúde pública envolve expressivo volume financeiro e pulverização de fornecedores, exigindo mecanismos eficientes de controle e transparência. Os principais desafios enfrentados incluem:

* **Assimetria de Informação e Discrepância de Preços:** Diferentes órgãos públicos frequentemente adquirem os mesmos insumos por valores unitários significativamente distintos, sem visibilidade imediata das médias de mercado.
* **Volume e Fragmentação dos Dados:** A separação dos registros em bases anuais extensas impede uma análise histórica contínua e integrada sem o devido tratamento de dados.
* **Complexidade na Comparabilidade:** Variações nas descrições de produtos, unidades de fornecimento e modalidades de compra dificultam a tomada de decisão rápida durante os processos licitatórios.
* **Necessidade de Inteligência Fiscal e Operacional:** A ausência de painéis consolidados restringe a capacidade dos gestores e órgãos de controle em identificar gargalos e negociar melhores condições de aquisição.

Este projeto aborda a necessidade de consolidar um volume expressivo de dados históricos para transformar registros esparsos em inteligência operacional e fiscal.

<br>

---

## 3. Fonte dos dados

> Dados públicos de aquisições de medicamentos e dispositivos médicos obtidos a partir do Portal Brasileiro de Dados Abertos do Ministério da Saúde, cobrindo o período de 2020 a 2026. 

<br>

Os dados utilizados neste projeto têm como origem o **Banco de Preços em Saúde (BPS)**, mantido pelo Ministério da Saúde para registrar e dar transparência às compras públicas do setor:

* **Origem:** Ministério da Saúde — Banco de Preços em Saúde (BPS)
* **Endereço eletrônico:** https://dadosabertos.saude.gov.br/dataset/bps
* **Período Coberto:** 2020 a 2026 (7 arquivos anuais).
* **Formato Original:** Arquivos em formato `.csv`.
* **Armazenamento Inicial:** Diretório local `dados/bronze/` mantendo as estruturas originais (*raw data*).

Após auditoria estrutural na primeira fase do ETL, foi confirmada a consistência de 25 colunas idênticas em toda série histórica, totalizando 342.716 registros brutos.

<br>

---

## 4. Procedimentos utilizados para baixar e concatenar as bases anuais

> Download dos 7 arquivos em formato `.csv` (2020 a 2026), após submetidos a uma auditoria estrutural e preparados para consolidaçõa em um único arquivo.

<br>

* **Obtenção e Armazenamento:** Os conjuntos de dados públicos foram baixados do Portal Brasileiro de Dados Abertos do Ministério da Saúde e salvos na camada Bronze (dados/bronze/) preservando o formato original (raw data).

* **Extração:** Utilizou-se um dicionário de dados em Python via pandas para estruturar a leitura iterativa dos 7 arquivos anuais.

* **Auditoria de Integridade:** Realizou-se a validação comparativa de colunas, confirmando a consistência de 25 campos idênticos em toda a série histórica, totalizando 342.716 registros brutos prontos para a unificação.

<br>

---

## 5. Tratamentos e transformações realizados nos dados

> 

<br>



<br>

---

## 6. Descrição das principais colunas utilizadas

> 

<br>



<br>

---

## 7. Definição dos KPIs e das métricas

> 

<br>



<br>

---

## 8. Link ou imagens do dashboard

> 

<br>



<br>

---

## 9. Principais análises e descobertas

> 

<br>



<br>

---

## 10. Recomendações baseadas nos dados

> 

<br>



<br>

---

## 11. Limitações identificadas na base ou na análise

> 

<br>



<br>

---

## 12. Instruções para reprodução do projeto

> Guia passo a passo para configurar o ambiente de desenvolvimento, estruturar os diretórios e executar o pipeline de dados a partir dos arquivos brutos.

<br>

1. **Pré-requisitos:**
   * _Python:_ Versão 3.12.3 ou superior instalado.
   * _Ambiente virtual .venv:_ Criação do ambinte virtual e instalação das dependências.

<br>

2. **Clone o repositório e acesse a pasta:**

```bash
git clone https://github.com/lf-vampre/sctec-datascience-mini-projeto-2
cd sctec-datascience-mini-projeto-2
```

<br>

3. **Crie e ative o ambiente virtual (venv):**

```bash
python3 -m venv .venv # ou então: python -m venv .venv
```

* Ativação (Linux/WSL/MacOS):

```bash
source .venv/bin/activate
```

* Ativação (Windows - PowerShell):

```bash
.\.venv\Scripts\Activate.ps1
```

<br>

4. **Instale as dependências:**

```bash
pip install -r requirements.txt
```

<br>

5. **Execução do Pipeline:**

* Abra o arquivo `projeto_bps.ipynb` no vscode ou alguma IDE que reconheça `.ipynb`, selecione o kernel do python do ambiente .venv e rode todas as células ou uma a uma para acompanhar o pipeline de dados.

<br>

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python (Pandas), SQL
* **Base de Dados:** csv
* **Ambiente:** VS Code / WSL / venv
* **Orquestração:** Lógica celular em Jupyter Notebook
* **Ferramenta de BI:** Google Data Studio


<br>

---

## 📜 Histórico de Commits (git log --oneline)

<br>



<br>