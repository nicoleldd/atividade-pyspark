# Exercícios PySpark — NYC Taxi Trip Data

Análise exploratória de ~4,1 milhões de corridas de táxi em Nova York usando **PySpark**, cobrindo leitura de dados em larga escala, seleção, filtros, agregações, joins e conceitos de execução distribuída (transformações vs. ações, lazy evaluation, shuffle).

## Conteúdo

O notebook [`exercicios_pyspark.ipynb`](./exercicios_pyspark.ipynb) resolve 10 questões:

1. Schema inferido, amostra e contagem total de linhas
2. Seleção de colunas específicas
3. Filtro combinado (distância + número de passageiros)
4. *Dissertativa:* `inferSchema` vs. `StructType`/`StructField`
5. Agregação de receita por forma de pagamento (`groupBy` + `agg`)
6. Tarifa e distância média por hora do dia
7. *Dissertativa:* transformações vs. ações e lazy evaluation
8. Percentual de gorjeta por corrida
9. Join com tabela de referência de zonas (bairros de origem)
10. *Dissertativa:* custo de `count()` vs. `groupBy()` e o conceito de shuffle

## Dataset

 Disponibilizado em: [huggingface.co/datasets/alexvaroz/nyc_tripdata_2024_sample_4M](https://huggingface.co/datasets/alexvaroz/nyc_tripdata_2024_sample_4M)

O próprio notebook baixa os arquivos automaticamente (`!wget`) na célula de preparação do ambiente (não é necessário baixar nada manualmente.)

## Principais achados

- O dataset tem **4.118.743 corridas**.
- **Cartão de crédito** (`payment_type=1`) responde por ~79% da receita total.
- **Manhattan** concentra ~88% das corridas de origem.
- Operações de agregação (`groupBy`) levaram ~4x mais tempo que um `count()` simples, devido ao *shuffle* necessário para reunir registros pela mesma chave.
