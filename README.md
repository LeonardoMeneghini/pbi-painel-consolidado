# pbi-painel-consolidado <br>

Relatório de Atividades dos Processos SEI - Análise Consolidada <br>

**1. Diagrama dos objetos envolvidos nesse painel** <br>
     
   [![Descrição](Relacionamentos Dados Consolidados 2.jpg)](https://github.com/LeonardoMeneghini/pbi-painel-consolidado/blob/main/Relacionamentos%20Dados%20Consolidados%202.jpg) <br>

**2. DAX para contar a ocorrência de um atributo ou operações relacionados com aquele atributo (Ex: "Concluído")** <br>
   
   Operações de Conclusão_COUNTROWS = <br>
COUNTROWS ( <br>
    FILTER ( <br>
        'fonte-de-dados', <br>
        'fonte-de-dados'[Coluna do Atributo] = "Atributo que será contabilizado" <br>
    ) <br>
) <br>
**3. DAX para contar a ocorrência de processos com esse atributo (Ex: "Concluído")**
   
Processos Concluídos_DISTINCTCOUNT = 
CALCULATE (
    DISTINCTCOUNT ( 'fonte-de-dados'[Coluna do número do Processo] ),
    'fontes (2)'[Coluna do Atributo] = "Concluído"
)

Comentário 1: a coluna "número do Processo" deve ser um atributo de identidade como uma chave PK.
Comentário 2: geralmente o valor de Operações > Processos que sofreram a operação.

**4. DAX para calcular a média (Ex: Média mensal dos processos que sofreram a operação identificada na coluna "Atributo")**
   
Concluídos_MEDIA = 
AVERAGEX (
    VALUES ( Calendario_2025[Mes] ),
    CALCULATE (
        [Processos Concluídos_DISTINCTCOUNT],
        Calendario_2025[Ano] = 2025
    )
)
