
# Monitoramento de Custos no Azure Data Factory

Este repositório apresenta um passo a passo detalhado para criar um sistema de monitoramento de custos no Azure Data Factory (ADF), utilizando recursos nativos do Azure, integração com Log Analytics e visualização em Power BI. O objetivo é permitir o acompanhamento proativo dos custos dos pipelines, facilitando a otimização e o controle financeiro do ambiente de dados.

## Visão Geral

Este projeto demonstra como monitorar custos de pipelines no Azure Data Factory, integrando logs, consultas e dashboards para análise e otimização financeira.

## Pré-requisitos
- Conta ativa no [Azure](https://portal.azure.com/)
- Permissão para criar e editar recursos no Azure Data Factory
- Permissão para acessar o Azure Cost Management + Billing
- Permissão para criar recursos no Azure Storage e Log Analytics
- [Azure Data Factory](https://learn.microsoft.com/pt-br/azure/data-factory/introduction) provisionado

## Passo a Passo

### 1. Configuração Inicial no Azure
1. Acesse o [Portal do Azure](https://portal.azure.com/).
2. Navegue até o recurso do Azure Data Factory.
3. No menu lateral, clique em **Monitoramento** e depois em **Configurar Monitoramento de Custo**.
4. Siga as instruções para habilitar o monitoramento e definir alertas de custo.

### 2. Habilitando Logs e Integração com Log Analytics
1. No Data Factory, acesse a seção **Diagnóstico e logs**.
2. Crie um grupo de Log Analytics ou selecione um existente.
3. Habilite a exportação de logs de execução de pipeline e atividades.

### 3. Criando Pipelines para Coleta de Dados
1. No ambiente de desenvolvimento do Data Factory, crie uma pipeline chamada `MonitoramentoCustosADF`.
2. Adicione atividades que executem pipelines reais e gerem logs.
3. Configure triggers para execução automática (diária, semanal, etc).


### 4. Consultando Custos com Kusto Query Language (KQL)
No Log Analytics, utilize consultas KQL para analisar os custos dos pipelines. Exemplo de consulta:

```kusto
ADFActivityRun
| where ActivityType == "Copy"
| summarize TotalCost = sum(ActivityRunCost) by PipelineName, bin(TimeGenerated, 1h)
```

### 5. Visualizando Dados no Power BI
1. No Power BI Desktop, conecte-se ao Log Analytics.
2. Importe os dados das consultas KQL.
3. Crie dashboards interativos para monitoramento dos custos.
