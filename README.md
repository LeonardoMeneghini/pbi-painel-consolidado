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
**3. DAX para contar a ocorrência de processos com esse atributo (Ex: "Concluído")** <br>
   
Processos Concluídos_DISTINCTCOUNT = <br>
CALCULATE ( <br>
    DISTINCTCOUNT ( 'fonte-de-dados'[Coluna do número do Processo] ),<br>
    'fontes (2)'[Coluna do Atributo] = "Concluído" <br>
) <br>

_Comentário 1: a coluna "número do Processo" deve ser um atributo de identidade como uma chave PK._ <br>
_Comentário 2: geralmente o valor de Operações > Processos que sofreram a operação._ <br>

**4. DAX para calcular a média (Ex: Média mensal dos processos que sofreram a operação identificada na coluna "Atributo")** <br>
   
Concluídos_MEDIA = <br>
AVERAGEX ( <br>
    VALUES ( Calendario_2025[Mes] ),<br>
    CALCULATE (<br>
        [Processos Concluídos_DISTINCTCOUNT],<br>
        Calendario_2025[Ano] = 2025 <br>
    )
)
