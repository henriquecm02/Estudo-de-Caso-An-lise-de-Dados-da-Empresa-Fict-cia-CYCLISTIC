# ANÁLISE DE DADOS DA CYCLISTIC

## Henrique Couto Machado
**Data:** 25/03/2024

## Índice
- Introdução
- Metodologia
- Análise de Dados
- Visualizações de Dados
- Conclusões e Recomendações
- Apêndice
- Referências

## Introdução
Este relatório visa documentar e apresentar os resultados do processo de análise de dados para o estudo de caso da Cyclistic, uma empresa fictícia de compartilhamento de bicicletas. O objetivo é compreender as diferenças no uso das bicicletas entre membros anuais e ciclistas casuais e desenvolver estratégias de marketing para aumentar o número de membros anuais.

## Metodologia
Toda a análise realizada neste estudo de caso seguiu a metodologia padrão para análise de dados, passando pelas 5 etapas conhecidas: Perguntar, Processar, Analisar, Compartilhar e Agir. Segue a descrição do que foi realizado em cada etapa.

#### Perguntar
Problema Identificado: Como os membros anuais e os ciclistas casuais usam as bicicletas da Cyclistic de maneira diferente?
Objetivo: Utilizar insights de dados para orientar decisões de marketing e aumentar a conversão de ciclistas casuais em membros anuais.

#### Preparar
Fontes de Dados: Dados históricos de trajetos da Cyclistic dos últimos 12 meses.
Organização dos Dados: Dados armazenados em arquivos CSV mensais.
Credibilidade dos Dados: Dados considerados confiáveis, sem viés aparente, e licenciados para uso.

#### Processar
Ferramentas Utilizadas: RStudio para processamento e análise de dados.
Limpeza de Dados: Remoção de campos irrelevantes, padronização de nomes de colunas e formatos de data/hora.
Documentação: Processo de limpeza e manipulação de dados documentado para revisão e compartilhamento.

#### Analisar
Análise Descritiva: Realizada para entender padrões de uso, como duração média das viagens e preferências de dia da semana.
Descobertas: Identificação de tendências de uso distintas entre membros e ciclistas casuais.

#### Compartilhar
Visualizações de Dados: Gráficos e tabelas criados para ilustrar as descobertas de maneira clara e acessível.
Narrativa de Dados: História contada pelos dados focada nas diferenças de comportamento entre os grupos de usuários.

#### Agir
Definição das 3 recomendações para equipe de Marketing baseadas na análise dos dados.

## Análise de Dados
A análise foi realizada tendo como norte: a busca pela resposta, através da análise de dados, da pergunta feita pela equipe de Marketing, que foi a seguinte:
"Como os membros anuais e os ciclistas casuais usam as bicicletas da Cyclistic de forma diferente?"
A partir deste ponto de partida, foram realizadas etapas de definição da análise através de perguntas bem direcionadas que levaram as etapas posteriores de manipulações de dados, extrações de informações complementares através de cálculos matemáticos, visando ter uma análise completa.

## Visualizações de Dados

![image](https://github.com/henriquecm02/Estudo-de-Caso-An-lise-de-Dados-da-Empresa-Fict-cia-CYCLISTIC/assets/139300033/85c7977d-cda8-424d-a24c-b3cb960c1ef0)

## Conclusões e Recomendações
Ao longo deste estudo de caso, exploramos extensivamente os padrões de comportamento dos usuários da Cyclistic, uma empresa fictícia de compartilhamento de bicicletas. Nossa análise revelou diferenças significativas entre os hábitos de ciclistas casuais e membros anuais, particularmente em relação aos horários de viagem, frequência de uso e duração das viagens. As visualizações de dados forneceram insights claros que destacaram a tendência dos membros anuais de utilizar o serviço para deslocamentos regulares, enquanto os ciclistas casuais mostraram preferência por viagens esporádicas e de lazer.

As recomendações propostas são estratégias direcionadas que a Cyclistic pode implementar para incentivar a conversão de ciclistas casuais em membros anuais. Estas incluem a introdução de planos de associação flexíveis, campanhas de marketing personalizadas e promoções sazonais baseadas em análises de dados detalhadas.

Este relatório não apenas fornece uma base sólida para decisões estratégicas de marketing, mas também serve como um exemplo do poder da análise de dados na compreensão do comportamento do consumidor e na otimização de serviços. A capacidade de extrair e interpretar dados complexos será uma ferramenta inestimável em minha futura carreira como analista de dados, e as habilidades desenvolvidas neste projeto serão aplicadas em desafios analíticos subsequentes.


## Apêndice
Código em R, utilizado no Rstudio.

```r
# Análise Completa do Ano da Divvy
# Este script é baseado no estudo de caso da Divvy "Sophisticated, Clear, and Polished': Divvy and Data Visualization" escrito por Kevin Hartman.

# Carregar os pacotes necessários
library(tidyverse) # Ajuda na manipulação de dados
library(lubridate) # Ajuda na manipulação de atributos de data
library(ggplot2) # Ajuda na visualização de dados

# Definir o diretório de trabalho
setwd("/caminho/para/seus/dados")

# Passo 1: Coletar Dados
# Carregar os conjuntos de dados da Divvy
Q2_2019 <- read_csv("Divvy_Trips_2019_Q2.csv")
Q3_2019 <- read_csv("Divvy_Trips_2019_Q3.csv")
Q4_2019 <- read_csv("Divvy_Trips_2019_Q4.csv")
Q1_2020 <- read_csv("Divvy_Trips_2020_Q1.csv")

# Passo 2: Manipular Dados e Combinar em um Único Arquivo
# Renomear colunas para padronizar com q1_2020
Q4_2019 <- rename(q4_2019,
Ride_id = trip_id, Rideable_type = bikeid, Started at = start time, Ended at = end time, Start station_name = from_station_name, Start station_id = from_station_id, End station name = to_station_name, End station_id = to_station_id, Member casual = usertype)

Q3_2019 <- rename(q3_2019,
Ride_id = trip_id, Rideable_type = bikeid, Started at = start time, Ended at = end_time, Start station_name = from_station_name, Start station_id = from_station_id, End station name = to_station_name, End station_id = to_station_id, Member casual = usertype)

Q2_2019 <- rename(q2_2019,
Ride_id = '01 - Rental Details Rental ID', Rideable_type = '01 - Rental Details Bike ID', Started at = '01 - Rental Details Local Start Time', Ended at = '01 - Rental Details Local End Time', Start station name = '03 - Rental Start Station Name', Start station id = '03 - Rental Start Station ID', End station name = '02 - Rental End Station Name', End station id = '02 - Rental End Station ID', Member casual = 'User Type')

# Converter ride_id e rideable_type para character para que possam ser empilhados
Q4_2019 <- mutate(Q4_2019, ride_id = as.character(ride_id), 
rideable_type = as.character(rideable_type))
Q3_2019 <- mutate(Q3_2019, ride_id = as.character(ride_id), 
rideable_type = as.character(rideable_type))
Q2_2019 <- mutate(Q2_2019, ride_id = as.character(ride_id), 
rideable_type = as.character(rideable_type))
Q1_2020 <- mutate(Q1_2020, ride_id = as.character(ride_id), 
rideable_type = as.character(rideable_type))

# Empilhar os data frames individuais em um grande data frame
All_trips <- bind_rows(Q2_2019, Q3_2019, Q4_2019, Q1_2020)

# Passo 3: Limpar e Adicionar Dados para Preparar para Análise
# Remover campos lat, long, birthyear e gender, pois esses dados foram removidos a partir de 2020
All_trips <- All_trips %>% select(-c(start_lat, start_lng, end_lat, end_lng, birthyear, gender, 
`01 – Rental Details Duration In Seconds Uncapped`, 
`05 – Member Details Member Birthday Year`, 
`Member Gender`, `tripduration`))

# Adicionar colunas que listam a data, mês, dia e ano de cada passeio
All_trips$date <- as.Date(All_trips$started_at) # O formato padrão é aaaa-mm-dd
All_trips$month <- format(as.Date(All_trips$date), "%m")
All_trips$day <- format(as.Date(All_trips$date), "%d")
All_trips$year <- format(as.Date(All_trips$date), "%Y")
All_trips$day_of_week <- format(as.Date(All_trips$date), "%A")

# Adicionar um cálculo de "ride_length" (duração do passeio) a All_trips (em segundos)
All_trips$ride_length <- difftime(All_trips$ended_at, All_trips$started_at, units = "secs")

# Converter "ride_length" de Factor para numeric para que possamos executar cálculos nos dados
All_trips$ride_length <- as.numeric(as.character(All_trips$ride_length))

# Remover dados "ruins"
# O dataframe inclui algumas entradas quando as bicicletas foram retiradas dos docks e verificadas por qualidade pela Divvy ou ride_length foi negativo
All_trips_v2 <- All_trips[!(All_trips$start_station_name == "HQ QR" | All_trips$ride_length < 0),]

# Passo 4: Realizar Análise Descritiva
# Análise descritiva sobre a duração das viagens
mean(All_trips_v2$ride_length) # média simples (duração total da viagem / viagens)
median(All_trips_v2$ride_length) # número do meio na matriz ascendente de durações de viagens
max(All_trips_v2$ride_length) # viagem mais longa
min(All_trips_v2$ride_length) # viagem mais curta

# Passo 5: Exportar Arquivo Resumo para Análise Adicional
write.csv(All_trips_v2, file = 'caminho/para/salvar/all_trips_summary.csv')
```

## Referências

- Coursera. (2024). *Projeto Final: Conclua um Estudo de Caso*. Disponível em: https://coursera.org/learn/projeto-final-conclua-um-estudo-de-caso. Acesso em: 23/03/2024.
- Microsoft. (2024). *Microsoft Copilot* [Software]. Disponível em: site oficial da Microsoft.

