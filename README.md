[notebook_lucas_revisado.ipynb](https://github.com/user-attachments/files/30882542/notebook_lucas_revisado.ipynb)
# python-basics-sprint-2
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Revisão de código\n",
    "\n",
    "Olá! Meu nome é Alan e estou feliz em revisar seu projeto hoje!\n",
    "\n",
    "Quando eu identificar um erro pela primeira vez, apenas o apontarei. A ideia é que você tente identificá-lo e corrigi-lo por conta própria. Ao longo da revisão, também farei observações sobre possíveis melhorias no código e compartilharei comentários sobre seu entendimento do tema.\n",
    "\n",
    "Caso encontre dificuldades para resolver algum ponto, na próxima iteração fornecerei dicas mais específicas e exemplos práticos para ajudá-lo. Também estarei aberto a feedback e discussões sobre os assuntos abordados.\n",
    "\n",
    "Você poderá encontrar meus comentários em caixas verdes, amarelas ou vermelhas, como estas:\n",
    "\n",
    "<div class=\"alert alert-block alert-success\"><b>Comentário: </b> <a class=\"tocSkip\"></a>Sucesso. Tudo está correto.</div>\n",
    "\n",
    "<div class=\"alert alert-block alert-warning\"><b>Comentário: </b> <a class=\"tocSkip\"></a>Observações. Algumas recomendações.</div>\n",
    "\n",
    "<div class=\"alert alert-block alert-danger\"><b>Comentário: </b> <a class=\"tocSkip\"></a>O bloco requer algumas correções. O trabalho não pode ser aceito com os comentários vermelhos.</div>\n",
    "\n",
    "Você pode me responder usando isto:\n",
    "\n",
    "<div class=\"alert alert-block alert-info\"><b>Resposta do aluno    </b><a class=\"tocSkip\"></a></div>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-success\"><b>Comentário geral do revisor: </b> <a class=\"tocSkip\"></a>Olá, Lucas! Muito bom trabalho — todas as etapas do pré-processamento (cabeçalhos, valores ausentes, duplicados explícitos e implícitos) estão corretas, a função <code>number_tracks()</code> está bem implementada, e as respostas escritas ao longo do notebook (visão geral dos dados, conclusões de pré-processamento, conclusão da hipótese) são detalhadas e bem fundamentadas, indo além do que era pedido. Os números obtidos (Springfield com 42.741 reproduções vs. Shelbyville com 18.512, por exemplo) conferem com os valores esperados para este dataset, então a integridade dos dados foi preservada em todas as etapas.<br><br>Não há pontos vermelhos. Encontrei apenas duas observações amarelas, veja abaixo.</div>"
   ]
  },
  {
   "cell_type": "raw",
   "metadata": {
    "id": "E0vqbgi9ay0H"
   },
   "source": [
    "# Se liga na música"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-warning\"><b>Comentário do revisor: </b> <a class=\"tocSkip\"></a>Esta célula (e a célula de conclusões do pré-processamento, mais adiante) está com o tipo <b>Raw</b> (texto puro), não Markdown. Isso significa que o <code>#</code> aqui não vai ser renderizado como título, e mais adiante a formatação (cabeçalhos, marcadores) das suas conclusões de pré-processamento também não vai aparecer formatada — tudo será exibido como texto simples. Mude o tipo dessas células para Markdown (no Jupyter, selecione a célula e pressione <code>M</code>).</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "fhq_eyov_Zcs"
   },
   "source": [
    "# Conteúdo <a id='back'></a>\n",
    "\n",
    "* [Introdução](#intro)\n",
    "* [Etapa 1. Visão geral dos dados](#data_review)\n",
    "    * [Conclusões](#data_review_conclusions)\n",
    "* [Etapa 2. Pré-processamento de dados](#data_preprocessing)\n",
    "    * [2.1 Estilo do cabeçalho](#header_style)\n",
    "    * [2.2 Valores ausentes](#missing_values)\n",
    "    * [2.3 Duplicados](#duplicates)\n",
    "    * [2.4 Conclusões](#data_preprocessing_conclusions)\n",
    "* [Etapa 3. Teste da hipótese](#hypothesis)\n",
    "    * [3.1 Hipótese 1: atividade dos usuários nas duas cidades](#activity)\n",
    "* [Conclusões](#end)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "VUC88oWjTJw2"
   },
   "source": [
    "## Introdução <a id='intro'></a>\n",
    "O trabalho de um analista é analisar dados para obter percepções valiosas dos dados e tomar decisões fundamentadas neles. Esse processo consiste em várias etapas, como visão geral dos dados, pré-processamento dos dados e testes de hipóteses.\n",
    "\n",
    "Sempre que fazemos uma pesquisa, precisamos formular uma hipótese que depois poderemos testar. Às vezes nós aceitamos essas hipóteses; outras vezes, nós as rejeitamos. Para fazer as escolhas certas, um negócio deve ser capaz de entender se está fazendo as suposições certas ou não.\n",
    "\n",
    "Neste projeto, você vai comparar as preferências musicais dos habitantes de Springfild e Shelbyville. Você vai estudar os dados de um serviço de streaming de música online para testar a hipótese apresentada abaixo e comparar o comportamento dos usuários dessas duas cidades.\n",
    "\n",
    "### Objetivo:\n",
    "Teste a hipótese:\n",
    "1. A atividade dos usuários é diferente dependendo do dia da semana e da cidade.\n",
    "\n",
    "\n",
    "### Etapas\n",
    "Os dados sobre o comportamento do usuário são armazenados no arquivo `/datasets/music_project_en.csv`. Não há informações sobre a qualidade dos dados, então será necessário examiná-los antes de testar a hipótese.\n",
    "\n",
    "Primeiro, você avaliará a qualidade dos dados e verá se seus problemas são significativos. Depois, durante o pré-processamento dos dados, você tentará tratar dos problemas mais críticos.\n",
    "\n",
    "O seu projeto consistirá em três etapas:\n",
    " 1. Visão geral dos dados\n",
    " 2. Pré-processamento de dados\n",
    " 3. Teste da hipótese\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "hDt6pg-Rw-1U"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Ml1hmfXC_Zcs"
   },
   "source": [
    "## Etapa 1. Visão geral dos dados <a id='data_review'></a>\n",
    "\n",
    "Abra os dados e examine-os."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "57eAOGIz_Zcs"
   },
   "source": [
    "Você precisará da `pandas`, então, importe-a."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "id": "AXN7PHPN_Zcs"
   },
   "outputs": [],
   "source": [
    " # importando pandas\n",
    "import pandas"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-warning\"><b>Comentário do revisor: </b> <a class=\"tocSkip\"></a>Funciona perfeitamente, mas é mais comum importar como <code>import pandas as pd</code> e depois usar <code>pd.read_csv(...)</code> em vez de <code>pandas.read_csv(...)</code> — é só uma convenção, mas torna o código mais compacto e é o padrão que você vai ver na maioria dos materiais e códigos de terceiros.</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "SG23P8tt_Zcs"
   },
   "source": [
    "Leia o arquivo `music_project_en.csv` da pasta `/datasets/` e salve-o na variável `df`:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "id": "fFVu7vqh_Zct"
   },
   "outputs": [],
   "source": [
    "# lendo o arquivo e armazenando em df\n",
    "df = pandas.read_csv('/datasets/music_project_en.csv')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "rDoOMd3uTqnZ"
   },
   "source": [
    "Imprima as primeiras 10 linhas da tabela:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "id": "oWTVX3gW_Zct",
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "     userID                        Track            artist   genre  \\\n",
      "0  FFB692EC            Kamigata To Boots  The Mass Missile    rock   \n",
      "1  55204538  Delayed Because of Accident  Andreas Rönnberg    rock   \n",
      "2    20EC38            Funiculì funiculà       Mario Lanza     pop   \n",
      "3  A3DD03C9        Dragons in the Sunset        Fire + Ice    folk   \n",
      "4  E2DC1FAE                  Soul People        Space Echo   dance   \n",
      "5  842029A1                       Chains          Obladaet  rusrap   \n",
      "6  4CB90AA5                         True      Roman Messer   dance   \n",
      "7  F03E1C1F             Feeling This Way   Polina Griffith   dance   \n",
      "8  8FA1D3BE                     L’estate       Julia Dalia  ruspop   \n",
      "9  E772D5C0                    Pessimist               NaN   dance   \n",
      "\n",
      "        City        time        Day  \n",
      "0  Shelbyville  20:28:33  Wednesday  \n",
      "1  Springfield  14:07:09     Friday  \n",
      "2  Shelbyville  20:58:07  Wednesday  \n",
      "3  Shelbyville  08:37:09     Monday  \n",
      "4  Springfield  08:34:34     Monday  \n",
      "5  Shelbyville  13:09:41     Friday  \n",
      "6  Springfield  13:00:07  Wednesday  \n",
      "7  Springfield  20:47:49  Wednesday  \n",
      "8  Springfield  09:17:40     Friday  \n",
      "9  Shelbyville  21:20:49  Wednesday  \n"
     ]
    }
   ],
   "source": [
    "# obtenha as 10 primeiras 10 linhas da tabela df\n",
    "print(df.head(10))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "id": "DSf2kIb-_Zct"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 65079 entries, 0 to 65078\n",
      "Data columns (total 7 columns):\n",
      " #   Column    Non-Null Count  Dtype \n",
      "---  ------    --------------  ----- \n",
      " 0     userID  65079 non-null  object\n",
      " 1   Track     63736 non-null  object\n",
      " 2   artist    57512 non-null  object\n",
      " 3   genre     63881 non-null  object\n",
      " 4     City    65079 non-null  object\n",
      " 5   time      65079 non-null  object\n",
      " 6   Day       65079 non-null  object\n",
      "dtypes: object(7)\n",
      "memory usage: 3.5+ MB\n"
     ]
    }
   ],
   "source": [
    "# obtendo informações gerais sobre os nossos dados\n",
    "df.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "EO73Kwic_Zct"
   },
   "source": [
    "Obtenha informações gerais sobre a tabela usando um comando. Você conhece o método para exibir informações gerais que precisamos obter."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "TaQ2Iwbr_Zct"
   },
   "source": [
    "Aqui estão as nossas observações sobre a tabela. Ela contém sete colunas. Elas armazenam o mesmo tipo de dado: `object`.\n",
    "\n",
    "De acordo com a documentação:\n",
    "- `' userID'` — identificação do usuário\n",
    "- `'Track'` — título da música\n",
    "- `'artist'` — nome do artista\n",
    "- `'genre'` — gênero da música\n",
    "- `'City'` — cidade do usuário\n",
    "- `'time'` — o tempo exato que a música foi reproduzida\n",
    "- `'Day'` — dia da semana\n",
    "\n",
    "Podemos ver três problemas de estilo nos cabeçalhos da tabela:\n",
    "1. Alguns cabeçalhos são escritos em letras maiúsculas, outros estão em minúsculas.\n",
    "2. Alguns cabeçalhos contêm espaços.\n",
    "3. A coluna userID usa camelCase, onde a primeira letra é minúscula e a segunda palavra começa com maiúscula. Isto é um problema, já que em boas práticas de programação, especialmente um Python, recomenda-se usar snake_case. Se estivesse escrito da forma correta seria user_id, como foram escritas as demais colunas.\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "MCB6-dXG_Zct"
   },
   "source": [
    "### Escreva suas observações. Aqui estão algumas perguntas que podem ajudar: <a id='data_review_conclusions'></a>\n",
    "\n",
    "1. Que tipo de dados temos nas linhas? E como podemos entender as colunas?  Estrutura de Dados:\n",
    "\n",
    "•Unidade de Observação (Linhas): Cada linha representa um evento de streaming musical:\n",
    " Registro individual de reprodução de faixa por usuário, capturado em tempo real pelo sistema;\n",
    "\n",
    "•Variáveis/Atributos (Colunas): O dataset contém 7 variáveis categóricas e temporais que descrevem as dimensões do comportamento de consumo musical:\n",
    "\n",
    "user_id: Identificador único do usuário (variável categórica);  \n",
    "\n",
    "track: Nome da faixa musical (variável categórica);  \n",
    "\n",
    "artist: Nome do artista/banda (variável categórica);  \n",
    "\n",
    "genre: Classificação do gênero musical (variável categórica);  \n",
    "\n",
    "city: Localização geográfica do usuário (variável categórica);  \n",
    "\n",
    "time: Timestamp da reprodução (variável temporal);  \n",
    "\n",
    "day: Dia da semana da reprodução (variável categórica ordinal);\n",
    " \n",
    "`2.   Esses dados são suficientes para responder à nossa hipótese ou precisamos de mais dados?`\n",
    "\n",
    "Sim, os dados disponíveis são suficientes para responder à hipótese proposta. Aqui está uma análise mais detalhada:  \n",
    "\n",
    "•Todas as demais colunas: Representam eventos de streaming únicos para contagem;  \n",
    "\n",
    "•Day: Possibilita análise por dia da semana (segunda, quarta, sexta);  \n",
    "\n",
    "•City: Permite comparar Springfield vs Shelbyville;  \n",
    "\n",
    "Metodologia de Análise Viável:\n",
    "A atividade musical será medida através da contagem de streams por cidade e por dia. A metodologia focará na variação relativa, analisando se o padrão de atividade ao longo da semana é diferente entre Springfield e Shelbyville.  \n",
    "\n",
    "Limitações Identificadas:\n",
    "•Ausência de dados demográficos: Não temos informações sobre idade, gênero ou perfil socioeconômico dos usuários;  \n",
    "\n",
    "•Período temporal limitado: Não sabemos se os dados representam uma semana típica ou período específico;  \n",
    "\n",
    "•Contexto sazonal: Falta informação sobre época do ano que pode influenciar padrões de consumo;  \n",
    "\n",
    "Dados Adicionais que Enriqueceriam a Análise:  \n",
    "\n",
    "•Duração das sessões de escuta;  \n",
    "\n",
    "•Horário de pico de atividade por cidade;  \n",
    "\n",
    "•Dados de múltiplas semanas para identificar padrões consistentes;\n",
    "\n",
    "`3.   Você notou algum problema nos dados, como valores ausentes, duplicados ou tipos de dados errados`\n",
    "\n",
    "\n",
    "Após examinar o dataset, identifiquei alguns problemas de qualidade dos dados que precisam ser tratados antes da análise, caso contrário podem impactar a confiabilidade da mesma, se não forem corrigidos adequadamente:  \n",
    "\n",
    "•Valores ausentes em algumas colunas: Presença de valores NaN (ausentes) que podem distorcer estatísticas;  \n",
    "\n",
    "Ex.: coluna artist (linha 9).  \n",
    "\n",
    "•Problemas de formatação nos cabeçalhos: Mistura de maiúsculas/ minúsculas, espaços desnecessários e uso de camelCase, que dificultam manipulação de dados;  \n",
    "\n",
    "Ex.: ' userID' (com espaço no início), 'userID' deveria ser 'user_id' (snake_case).  \n",
    "\n",
    "•Duplicados nos dados: Possíveis linhas completamente idênticas no dataset que precisam ser verificadas, que podem inflar contagens e distorcem resultados;  \n",
    "\n",
    "Ex.: Para confirmar, será necessário executar df.duplicated().sum()  \n",
    "\n",
    "Dentre esses problemas específicos, do ponto de vista de análise de dados, os valores duplicados representam o maior risco para a validade da análise. Se temos a mesma linha repetida, isso inflaria artificialmente o número de streams de uma cidade, o que pode levar a conclusões errôneas sobre diferenças de atividade entre Springfield e Shelbyville. Portanto, a remoção de duplicados será priorizada antes de prosseguir com a análise comparativa.\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-success\">\n",
    "<b>Comentário: </b> <a class=\"tocSkip\"></a>\n",
    "\n",
    "Você importou corretamente a biblioteca pandas, carregou os dados utilizando read_csv() e utilizou métodos como `head()`, `info()` e `columns` para explorar a estrutura do DataFrame. Além disso, identificou características importantes dos dados antes de iniciar o processo de limpeza.\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "3eL__vcwViOi"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "SjYF6Ub9_Zct"
   },
   "source": [
    "## Etapa 2. Pré-processamento de dados <a id='data_preprocessing'></a>\n",
    "\n",
    "O objetivo aqui é preparar os dados para a análise.\n",
    "O primeiro passo é resolver todos os problemas com o cabeçalho. E então podemos passar para os valores ausentes e duplicados. Vamos começar.\n",
    "\n",
    "Corrija a formatação nos cabeçalhos da tabela.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "dIaKXr29_Zct"
   },
   "source": [
    "### Estilo do cabeçalho <a id='header_style'></a>\n",
    "Imprima os cabeçalhos da tabela (os nomes das colunas):"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "id": "oKOTdF_Q_Zct"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Index(['  userID', 'Track', 'artist', 'genre', '  City  ', 'time', 'Day'], dtype='object')\n"
     ]
    }
   ],
   "source": [
    "# imprima os nomes das colunas\n",
    "print(df.columns)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "zj5534cv_Zct"
   },
   "source": [
    "Mude os cabeçalhos da tabela conforme as boas práticas de estilo:\n",
    "* Todos os caracteres precisam estar com letras minúsculas\n",
    "* Exclua espaços\n",
    "* Se o nome tiver várias palavras, use snake_case"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Xu0zkfe5zNJe"
   },
   "source": [
    "Anteriormente, você aprendeu sobre uma maneira automatizada de renomear colunas. Vamos usá-la agora. Use o ciclo for para percorrer os nomes das colunas e transformar todos os caracteres em letras minúsculas. Após fazer isso, imprima os cabeçalhos da tabela novamente:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "id": "6I_RwwMhzM4e"
   },
   "outputs": [],
   "source": [
    "# Percorrendo os cabeçalhos e convertendo tudo em minúsculos\n",
    "new_columns = []\n",
    "for column in df.columns:\n",
    "    new_columns.append(column.lower())\n",
    "df.columns = new_columns"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "pweIRxjSzPYW"
   },
   "source": [
    "Agora, usando a mesma abordagem, exclua os espaços no início e no final de cada nome de coluna e imprima os nomes das colunas novamente:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "id": "vVQXbFyJzSYl"
   },
   "outputs": [],
   "source": [
    "# Percorrendo os cabeçalhos e removendo os espaços\n",
    "new_columns = []\n",
    "for column in df.columns:\n",
    "    new_columns.append(column.strip())\n",
    "df.columns = new_columns"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "yCb8MW1JzURd"
   },
   "source": [
    "Precisamos aplicar a regra de sublinhado no lugar de espaço à coluna `userid`. Deveria ser `user_id`. Renomeie essa coluna e imprima os nomes de todas as colunas quando terminar."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "id": "ISlFqs5y_Zct"
   },
   "outputs": [],
   "source": [
    "# Renomeando a coluna \"userid\"\n",
    "df.rename(columns={'userid': 'user_id'}, inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "1dqbh00J_Zct"
   },
   "source": [
    "Verifique o resultado. Imprima os cabeçalhos novamente:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "id": "d4NOAmTW_Zct"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Index(['user_id', 'track', 'artist', 'genre', 'city', 'time', 'day'], dtype='object')\n"
     ]
    }
   ],
   "source": [
    "# verificando o resultado: a lista de cabeçalhos\n",
    "print(df.columns)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "xYJk6ksJVpOl"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "5ISfbcfY_Zct"
   },
   "source": [
    "### Valores Ausentes <a id='missing_values'></a>\n",
    " Primeiro, encontre a quantidade de valores ausentes na tabela. Você precisa usar dois métodos em sequência para obter o número de valores ausentes."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "id": "RskX29qr_Zct"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "user_id       0\n",
       "track      1343\n",
       "artist     7567\n",
       "genre      1198\n",
       "city          0\n",
       "time          0\n",
       "day           0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# calculando o número de valores ausentes\n",
    "df.isna().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "qubhgnlO_Zct"
   },
   "source": [
    "Nem todos os valores ausentes afetam a pesquisa. Por exemplo, os valores ausentes em `track` e `artist` não são críticos. Você pode simplesmente substituí-los por valores padrão, como a string `'unknown'`.\n",
    "\n",
    "Mas valores ausentes em `'genre'` podem afetar a comparação de preferências musicais de Springfield e Shelbyville. Na vida real, seria útil descobrir as razões pelas quais os dados estão ausentes e tentar corrigi-los. Mas nós não temos essa possibilidade neste projeto. Então, você terá que:\n",
    "* Preencha esses valores ausentes com um valor padrão\n",
    "* Avalie em que medida os valores ausentes podem afetar sua análise"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "fSv2laPA_Zct"
   },
   "source": [
    "Substitua os valores ausentes nas colunas `'track'`, `'artist'` e `'genre'` pela string `'unknown'`. Como mostramos nas lições anteriores, a melhor maneira de fazer isso é criar uma lista para armazenar os nomes das colunas nas quais precisamos fazer a substituição. Em seguida, use essa lista e percorra as colunas nas quais a substituição seja necessária e faça a substituição."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "id": "KplB5qWs_Zct"
   },
   "outputs": [],
   "source": [
    "# percorrendo os cabeçalhos e substituindo valores ausentes por 'unknowncolumns\n",
    "columns_to_fill = ['track','artist','genre']\n",
    "for column in columns_to_fill:\n",
    "    df[column]= df[column].fillna('unknown')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Ilsm-MZo_Zct"
   },
   "source": [
    "Agora verifique o resultado para ter certeza de que o conjunto de dados não contenha valores ausentes após a substituição. Para fazer isso, conte os valores ausentes novamente."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "id": "Tq4nYRX4_Zct"
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "user_id    0\n",
      "track      0\n",
      "artist     0\n",
      "genre      0\n",
      "city       0\n",
      "time       0\n",
      "day        0\n",
      "dtype: int64\n"
     ]
    }
   ],
   "source": [
    "# contando os valores ausentes\n",
    "print(df.isna().sum())"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "74ZIBmq9VrsK"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "BWKRtBJ3_Zct"
   },
   "source": [
    "### Duplicados <a id='duplicates'></a>\n",
    "Encontre o número de duplicados explícitos na tabela. Lembre-se de que você precisa aplicar dois métodos em sequência para obter o número de duplicados explícitos."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "id": "36eES_S0_Zct"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "3826"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# contando duplicados explícitos\n",
    "df.duplicated().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Ot25h6XR_Zct"
   },
   "source": [
    "Agora descarte todos os duplicados. Para fazer isso, chame o método que faz exatamente isso."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "id": "exFHq6tt_Zct"
   },
   "outputs": [],
   "source": [
    "# removendo duplicados explícitos\n",
    "df.drop_duplicates(inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Im2YwBEG_Zct"
   },
   "source": [
    "Agora vamos verificar se descartamos todos os duplicados. Conte duplicados explícitos mais uma vez para ter certeza de que você removeu todos eles:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "id": "-8PuNWQ0_Zct"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# verificando duplicados novamente\n",
    "df.duplicated().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "QlFBsxAr_Zct"
   },
   "source": [
    "Agora queremos nos livrar dos duplicados implícitos na coluna `genre`. Por exemplo, o nome de um gênero pode ser escrito de maneiras diferentes. Alguns erros afetarão também o resultado."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "eSjWwsOh_Zct"
   },
   "source": [
    "Para fazer isso, vamos começar imprimindo uma lista de nomes de gênero únicos, ordenados em ordem alfabética: Para fazer isso:\n",
    "* Extraia a coluna `genre` do DataFrame\n",
    "* Chame o método que retornará todos os valores únicos na coluna extraída\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "id": "JIUcqzZN_Zct"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array(['rock', 'pop', 'folk', 'dance', 'rusrap', 'ruspop', 'world',\n",
       "       'electronic', 'unknown', 'alternative', 'children', 'rnb', 'hip',\n",
       "       'jazz', 'postrock', 'latin', 'classical', 'metal', 'reggae',\n",
       "       'triphop', 'blues', 'instrumental', 'rusrock', 'dnb', 'türk',\n",
       "       'post', 'country', 'psychedelic', 'conjazz', 'indie',\n",
       "       'posthardcore', 'local', 'avantgarde', 'punk', 'videogame',\n",
       "       'techno', 'house', 'christmas', 'melodic', 'caucasian',\n",
       "       'reggaeton', 'soundtrack', 'singer', 'ska', 'salsa', 'ambient',\n",
       "       'film', 'western', 'rap', 'beats', \"hard'n'heavy\", 'progmetal',\n",
       "       'minimal', 'tropical', 'contemporary', 'new', 'soul', 'holiday',\n",
       "       'german', 'jpop', 'spiritual', 'urban', 'gospel', 'nujazz',\n",
       "       'folkmetal', 'trance', 'miscellaneous', 'anime', 'hardcore',\n",
       "       'progressive', 'korean', 'numetal', 'vocal', 'estrada', 'tango',\n",
       "       'loungeelectronic', 'classicmetal', 'dubstep', 'club', 'deep',\n",
       "       'southern', 'black', 'folkrock', 'fitness', 'french', 'disco',\n",
       "       'religious', 'hiphop', 'drum', 'extrememetal', 'türkçe',\n",
       "       'experimental', 'easy', 'metalcore', 'modern', 'argentinetango',\n",
       "       'old', 'swing', 'breaks', 'eurofolk', 'stonerrock', 'industrial',\n",
       "       'funk', 'middle', 'variété', 'other', 'adult', 'christian',\n",
       "       'thrash', 'gothic', 'international', 'muslim', 'relax', 'schlager',\n",
       "       'caribbean', 'nu', 'breakbeat', 'comedy', 'chill', 'newage',\n",
       "       'specialty', 'uzbek', 'k-pop', 'balkan', 'chinese', 'meditative',\n",
       "       'dub', 'power', 'death', 'grime', 'arabesk', 'romance', 'flamenco',\n",
       "       'leftfield', 'european', 'tech', 'newwave', 'dancehall', 'mpb',\n",
       "       'piano', 'top', 'bigroom', 'opera', 'celtic', 'tradjazz',\n",
       "       'acoustic', 'epicmetal', 'hip-hop', 'historisch', 'downbeat',\n",
       "       'downtempo', 'africa', 'audiobook', 'jewish', 'sängerportrait',\n",
       "       'deutschrock', 'eastern', 'action', 'future', 'electropop',\n",
       "       'folklore', 'bollywood', 'marschmusik', 'rnr', 'karaoke', 'indian',\n",
       "       'rancheras', 'afrikaans', 'rhythm', 'sound', 'deutschspr', 'trip',\n",
       "       'lovers', 'choral', 'dancepop', 'retro', 'smooth', 'mexican',\n",
       "       'brazilian', 'ïîï', 'mood', 'surf', 'gangsta', 'inspirational',\n",
       "       'idm', 'ethnic', 'bluegrass', 'broadway', 'animated', 'americana',\n",
       "       'karadeniz', 'rockabilly', 'colombian', 'self', 'hop', 'sertanejo',\n",
       "       'japanese', 'canzone', 'lounge', 'sport', 'ragga', 'traditional',\n",
       "       'gitarre', 'frankreich', 'emo', 'laiko', 'cantopop', 'glitch',\n",
       "       'documentary', 'oceania', 'popeurodance', 'dark', 'vi', 'grunge',\n",
       "       'hardstyle', 'samba', 'garage', 'art', 'folktronica', 'entehno',\n",
       "       'mediterranean', 'chamber', 'cuban', 'taraftar', 'gypsy',\n",
       "       'hardtechno', 'shoegazing', 'bossa', 'latino', 'worldbeat',\n",
       "       'malaysian', 'baile', 'ghazal', 'arabic', 'popelectronic', 'acid',\n",
       "       'kayokyoku', 'neoklassik', 'tribal', 'tanzorchester', 'native',\n",
       "       'independent', 'cantautori', 'handsup', 'punjabi', 'synthpop',\n",
       "       'rave', 'französisch', 'quebecois', 'speech', 'soulful', 'jam',\n",
       "       'ram', 'horror', 'orchestral', 'neue', 'roots', 'slow', 'jungle',\n",
       "       'indipop', 'axé', 'fado', 'showtunes', 'arena', 'irish',\n",
       "       'mandopop', 'forró', 'dirty', 'regional'], dtype=object)"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# visualizando nomes de gêneros únicos\n",
    "df['genre'].unique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "qej-Qmuo_Zct"
   },
   "source": [
    "Olhe a lista e encontre duplicados implícitos do gênero `hiphop`. Esses podem ser nomes escritos incorretamente, ou nomes alternativos para o mesmo gênero.\n",
    "\n",
    "Você verá os seguintes duplicados implícitos:\n",
    "* `hip`\n",
    "* `hop`\n",
    "* `hip-hop`\n",
    "\n",
    "Para se livrar deles, crie uma função `replace_wrong_genres()` com dois parâmetros:\n",
    "* `wrong_genres=` — essa é uma lista que contém todos os valores que você precisa substituir\n",
    "* `correct_genre=` — essa é uma string que você vai usar para a substituição\n",
    "\n",
    "Como resultado, a função deve corrigir os nomes na coluna `'genre'` da tabela `df`, isto é, substituindo cada valor da lista `wrong_genres` por valores de `correct_genre`.\n",
    "\n",
    "Dentro do corpo da função, use um ciclo `'for'` para percorrer a lista de gêneros errados, extrair a coluna `'genre'` e aplicar o método `replace` para fazer as correções."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "id": "ErNDkmns_Zct"
   },
   "outputs": [],
   "source": [
    "# função para substituir duplicados implícitos\n",
    "def replace_wrong_genres(wrong_genres, correct_genre):\n",
    "    for genre in wrong_genres:\n",
    "        df['genre'] = df['genre'].replace(genre, correct_genre)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "aDoBJxbA_Zct"
   },
   "source": [
    "Agora, chame a função `replace_wrong_genres()` e passe argumentos apropriados para que ela limpe duplicados implícitos (`hip`, `hop` e `hip-hop`) substituindo-os por `hiphop`:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "id": "YN5i2hpmSo09"
   },
   "outputs": [],
   "source": [
    "# removendo duplicados implícitos\n",
    "replace_wrong_genres(['hip','hop','hip-hop'] , 'hiphop')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "zQKF16_RG15m"
   },
   "source": [
    "Certifique-se que os nomes duplicados foram removidos. Imprima a lista de valores únicos da coluna `'genre'` mais uma vez:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {
    "id": "wvixALnFG15m"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array(['rock', 'pop', 'folk', 'dance', 'rusrap', 'ruspop', 'world',\n",
       "       'electronic', 'unknown', 'alternative', 'children', 'rnb',\n",
       "       'hiphop', 'jazz', 'postrock', 'latin', 'classical', 'metal',\n",
       "       'reggae', 'triphop', 'blues', 'instrumental', 'rusrock', 'dnb',\n",
       "       'türk', 'post', 'country', 'psychedelic', 'conjazz', 'indie',\n",
       "       'posthardcore', 'local', 'avantgarde', 'punk', 'videogame',\n",
       "       'techno', 'house', 'christmas', 'melodic', 'caucasian',\n",
       "       'reggaeton', 'soundtrack', 'singer', 'ska', 'salsa', 'ambient',\n",
       "       'film', 'western', 'rap', 'beats', \"hard'n'heavy\", 'progmetal',\n",
       "       'minimal', 'tropical', 'contemporary', 'new', 'soul', 'holiday',\n",
       "       'german', 'jpop', 'spiritual', 'urban', 'gospel', 'nujazz',\n",
       "       'folkmetal', 'trance', 'miscellaneous', 'anime', 'hardcore',\n",
       "       'progressive', 'korean', 'numetal', 'vocal', 'estrada', 'tango',\n",
       "       'loungeelectronic', 'classicmetal', 'dubstep', 'club', 'deep',\n",
       "       'southern', 'black', 'folkrock', 'fitness', 'french', 'disco',\n",
       "       'religious', 'drum', 'extrememetal', 'türkçe', 'experimental',\n",
       "       'easy', 'metalcore', 'modern', 'argentinetango', 'old', 'swing',\n",
       "       'breaks', 'eurofolk', 'stonerrock', 'industrial', 'funk', 'middle',\n",
       "       'variété', 'other', 'adult', 'christian', 'thrash', 'gothic',\n",
       "       'international', 'muslim', 'relax', 'schlager', 'caribbean', 'nu',\n",
       "       'breakbeat', 'comedy', 'chill', 'newage', 'specialty', 'uzbek',\n",
       "       'k-pop', 'balkan', 'chinese', 'meditative', 'dub', 'power',\n",
       "       'death', 'grime', 'arabesk', 'romance', 'flamenco', 'leftfield',\n",
       "       'european', 'tech', 'newwave', 'dancehall', 'mpb', 'piano', 'top',\n",
       "       'bigroom', 'opera', 'celtic', 'tradjazz', 'acoustic', 'epicmetal',\n",
       "       'historisch', 'downbeat', 'downtempo', 'africa', 'audiobook',\n",
       "       'jewish', 'sängerportrait', 'deutschrock', 'eastern', 'action',\n",
       "       'future', 'electropop', 'folklore', 'bollywood', 'marschmusik',\n",
       "       'rnr', 'karaoke', 'indian', 'rancheras', 'afrikaans', 'rhythm',\n",
       "       'sound', 'deutschspr', 'trip', 'lovers', 'choral', 'dancepop',\n",
       "       'retro', 'smooth', 'mexican', 'brazilian', 'ïîï', 'mood', 'surf',\n",
       "       'gangsta', 'inspirational', 'idm', 'ethnic', 'bluegrass',\n",
       "       'broadway', 'animated', 'americana', 'karadeniz', 'rockabilly',\n",
       "       'colombian', 'self', 'sertanejo', 'japanese', 'canzone', 'lounge',\n",
       "       'sport', 'ragga', 'traditional', 'gitarre', 'frankreich', 'emo',\n",
       "       'laiko', 'cantopop', 'glitch', 'documentary', 'oceania',\n",
       "       'popeurodance', 'dark', 'vi', 'grunge', 'hardstyle', 'samba',\n",
       "       'garage', 'art', 'folktronica', 'entehno', 'mediterranean',\n",
       "       'chamber', 'cuban', 'taraftar', 'gypsy', 'hardtechno',\n",
       "       'shoegazing', 'bossa', 'latino', 'worldbeat', 'malaysian', 'baile',\n",
       "       'ghazal', 'arabic', 'popelectronic', 'acid', 'kayokyoku',\n",
       "       'neoklassik', 'tribal', 'tanzorchester', 'native', 'independent',\n",
       "       'cantautori', 'handsup', 'punjabi', 'synthpop', 'rave',\n",
       "       'französisch', 'quebecois', 'speech', 'soulful', 'jam', 'ram',\n",
       "       'horror', 'orchestral', 'neue', 'roots', 'slow', 'jungle',\n",
       "       'indipop', 'axé', 'fado', 'showtunes', 'arena', 'irish',\n",
       "       'mandopop', 'forró', 'dirty', 'regional'], dtype=object)"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# verificando valores duplicados\n",
    "df['genre'].unique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "ALgNbvF3VtPA"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "raw",
   "metadata": {
    "id": "jz6a9-7HQUDd"
   },
   "source": [
    "\n",
    "### Suas observações <a id='data_preprocessing_conclusions'></a>\n",
    "\n",
    "\n",
    "•Problemas de formatação em 4 dos 7 cabeçalhos: Mistura de maiúsculas/minúsculas, espaços desnecessários e uso de camelCase, que dificultam a manipulação de dados; \n",
    "\n",
    "Ex.: ' userID' (espaço no início e camelCase) deveria ser 'user_id' (snake_case).\n",
    "\n",
    "•Foram identificadas 3.826 linhas duplicadas em um total de 65.079 registros (5,87%), e após a limpeza das mesmas restaram 61.253 linhas, utilizando o método .duplicated().sum() para verificação de quantas duplicatas existem, .drop_duplicates(inplace=True) para remoção das mesmas  e .duplicated().sum() para verificação final. A não remoção dos mesmo causa inflação de contagens e distorção de resultados.\n",
    "\n",
    "•Foram identificados 10.108 valores ausentes nas colunas track, artist, genre, deste total, 1.198 apenas na coluna genre. A coluna genre merece atenção especial pois é a coluna que permite comparar as preferências musicais entre Springfield e Shelbyville. Ao invés de remover as linhas com os mesmos, substitui por 'unknown' utilizando o método .fillna(), pois a remoção dessas linhas eliminaria informações ainda válidas para análise, como cidade e gênero musical.\n",
    "\n",
    "•Foram identificados gêneros duplicados implícitos, que seriam hip, hop e hip-hop. Dentro do corpo da função, foi utilizado o ciclo 'for' para percorrer a lista de gêneros errados, extrair a coluna 'genre' que seria nossa coluna de interesse e assim aplicar o método .replace() para fazer as correções, e o método .unique() para verificação de que não teríamos mais gêneros duplicados implícitos.\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-warning\"><b>Comentário do revisor: </b> <a class=\"tocSkip\"></a>Mesmo problema indicado no início do notebook: esta célula também está com o tipo Raw em vez de Markdown, então toda essa conclusão bem escrita não vai aparecer formatada (títulos, marcadores) na versão final. Mude o tipo da célula para Markdown.</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-success\"><b>Comentário do revisor: </b> <a class=\"tocSkip\"></a>\n",
    "Excelente trabalho!\n",
    "\n",
    "Você realizou corretamente as principais tarefas de limpeza dos dados:\n",
    "- Padronizou os nomes das colunas.\n",
    "- Removeu espaços e ajustou a nomenclatura para o padrão esperado.\n",
    "- Identificou e tratou valores ausentes.\n",
    "- Removeu duplicados explícitos.\n",
    "- Criou uma função para corrigir duplicados implícitos nos gêneros musicais.\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "eK1es74rVujj"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "WttZHXH0SqKk"
   },
   "source": [
    "## Etapa 3. Teste da hipótese <a id='hypothesis'></a>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Im936VVi_Zcu"
   },
   "source": [
    "### Hipótese: comparação do comportamento dos usuários nas duas cidades <a id='activity'></a>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "nwt_MuaL_Zcu"
   },
   "source": [
    "A hipótese afirma que existem diferenças no consumo de música pelos usuários em Springfield e em Shelbyville. Para testar a hipótese, use os dados dos três dias da semana: segunda-feira (Monday), quarta-feira (Wednesday) e sexta-feira (Friday).\n",
    "\n",
    "* Agrupe os usuários por cidade.\n",
    "* Compare o número de músicas tocadas por cada grupo na segunda, quarta e sexta.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "8Dw_YMmT_Zcu"
   },
   "source": [
    "Execute cada cálculo separadamente.\n",
    "\n",
    "O primeiro passo é avaliar a atividade dos usuários em cada cidade. Não se esqueça das etapas \"divisão-aplicação-combinação\" sobre as quais falamos anteriormente na lição. Agora seu objetivo é agrupar os dados por cidade, aplicar o método de contagem apropriado durante a etapa de aplicação e então encontrar o número de músicas tocadas por cada grupo, especificando a coluna para a qual você quer obter a contagem.\n",
    "\n",
    "Veja um exemplo de como o resultado final deve ser:\n",
    "`df.groupby(by='....')['column'].method()` Execute cada cálculo separadamente.\n",
    "\n",
    "Para avaliar a atividade dos usuários em cada cidade, agrupe os dados por cidade e encontre o número de músicas reproduzidas em cada grupo.\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "id": "0_Qs96oh_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "city\n",
       "Shelbyville    18512\n",
       "Springfield    42741\n",
       "Name: track, dtype: int64"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Contando as músicas tocadas em cada cidade\n",
    "df.groupby(by='city')['track'].count()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "t_Qx-3NewAnK"
   },
   "source": [
    "O resultado mostra que Springfield tem 42.741 músicas tocadas e Shelbyville tem 18.512 "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "dzli3w8o_Zcu"
   },
   "source": [
    "Agora vamos agrupar os dados por dia da semana e encontrar a quantidade de músicas tocadas na segunda, quarta e sexta-feira. Use a mesma abordagem que antes, mas agora precisamos agrupar os dados de uma forma diferente.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "id": "uZMKjiJz_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "day\n",
       "Friday       21840\n",
       "Monday       21354\n",
       "Wednesday    18059\n",
       "Name: track, dtype: int64"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Calculando as músicas escutadas em cada um desses três dias\n",
    "df.groupby(by='day')['track'].count()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "cC2tNrlL_Zcu"
   },
   "source": [
    "O resultado mostra que os dias da semana que as músicas são mais reproduzidas em ordem crescente é respectivamente Wednesday com 18059, Monday com 21354 e Friday com 21840. Friday sendo o dia com mais reproduções enquanto Wednesday é o dia com menos. Isso pode indicar que os usuários tendem a ouvir mais músicas no final de semana."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "POzs8bGa_Zcu"
   },
   "source": [
    "Você acabou de aprender como contar entradas agrupando-as por cidade ou por dia. E agora você precisa escrever uma função que possa contar entradas simultaneamente com base em ambos os critérios.\n",
    "\n",
    "Crie a função `number_tracks()` para calcular o número de músicas tocadas em um determinado dia **e** em uma determinada cidade. A função deve aceitar dois parâmetros:\n",
    "\n",
    "- `day`: um dia da semana pelo qual precisamos filtrar os dados. Por exemplo, `'Monday'`.\n",
    "- `city`: uma cidade pela qual precisamos filtrar os dados. Por exemplo, `'Springfield'`.\n",
    "\n",
    "Dentro da função, você vai aplicar uma filtragem consecutiva com indexação lógica.\n",
    "\n",
    "Primeiro, filtre os dados por dia e então filtre a tabela resultante por cidade.\n",
    "\n",
    "Depois de filtrar os dados usando os dois critérios, conte o número de valores na coluna 'user_id' da tabela resultante. O resultado da contagem representará o número de entradas que você quer encontrar. Armazene o resultado em uma nova variável e imprima-o."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "id": "Nz3GdQB1_Zcu"
   },
   "outputs": [],
   "source": [
    "# Declare a função number_tracks() com dois parâmetros: day= e city=.\n",
    "def number_tracks(day, city):\n",
    "    # Armazene as linhas do DataFrame em que o valor na coluna 'day' é igual ao parâmetro day=\n",
    "    track_filtered = df[df['day'] == day]\n",
    "    # Filtre as linhas em que o valor na coluna 'city' é igual ao parâmetro city=\n",
    "    track_filtered = track_filtered[track_filtered['city'] == city]\n",
    "    # Extraia a coluna 'user_id' da tabela filtrada e aplique o método count()\n",
    "    result = track_filtered['user_id'].count()\n",
    "    # Retorne o número dos valores da coluna 'user_id'\n",
    "    return result"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "ytf7xFrFJQ2r"
   },
   "source": [
    "Chame a função `number_tracks()` seis vezes, mudando os valores dos parâmetros, para que você possa recuperar os dados de ambas as cidades para cada um dos três dias."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {
    "id": "rJcRATNQ_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "15740"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# a quantidade de músicas tocadas em Springfield na segunda-feira\n",
    "number_tracks('Monday','Springfield')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "id": "hq_ncZ5T_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "5614"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# a quantidade de músicas tocadas em Shelbyville na segunda-feira\n",
    "number_tracks('Monday','Shelbyville')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {
    "id": "_NTy2VPU_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "11056"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# a quantidade de músicas tocadas em Springfield na quarta-feira\n",
    "number_tracks('Wednesday','Springfield')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {
    "id": "j2y3TAwo_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "7003"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# a quantidade de músicas tocadas em Shelbyville na quarta-feira\n",
    "number_tracks('Wednesday','Shelbyville')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {
    "id": "vYDw5u_K_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "15945"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# a quantidade de músicas tocadas em Springfield na sexta-feira\n",
    "number_tracks('Friday','Springfield')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {
    "id": "8_yzFtW3_Zcu"
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "5895"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# a quantidade de músicas tocadas em Shelbyville na sexta-feira\n",
    "number_tracks('Friday','Shelbyville')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "-EgPIHYu_Zcu"
   },
   "source": [
    "**Conclusões**\n",
    "\n",
    "`Comente sobre se a terceira hipótese está correta ou deve ser rejeitada. Explique seu raciocínio.`\n",
    "\n",
    "Hipótese pode sim ser aceita, já que através dos dados podemos constatar que os padrões dos ouvintes nas duas cidades são completamente diferentes. Em Springfield foram registradas altas atividades na segunda feira (15740) e sexta feira (15945), com queda significativa na quarta feira (11056). Já em Shelbyville foi registrado um pico de atividade na quarta feira (7003), resultando segunda feira (5614) e sexta feira (5895) com uma menor atividade."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "p7nFQajCVw5B"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "ykKQ0N65_Zcv"
   },
   "source": [
    "# Conclusões <a id='end'></a>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "tjUwbHb3_Zcv"
   },
   "source": [
    "`Resuma suas conclusões sobre a hipótese aqui`\n",
    "\n",
    "1. Visão geral dos dados: \n",
    " Nessa primeira observação do dataset, foi possivel observar as 10 primeiras linhas das respectivas 7 colunas de dados sobre identificação do usuário, título da música, nome do artista,\n",
    "gênero da música, cidade do usuário, o tempo exato que a música foi reproduzida e dia da semana, através do método .head(). Também utilizei o método .info() para obter informações gerais o que já possibilitou identificar problemas de formatação nos cabeçalhos.\n",
    "\n",
    "2. Pré-processamento:\n",
    " Cada fase do pré-processamento foi mostrando, na ordem a seguir, problemas que afetariam a análise da pesquisa sendo eles:\n",
    "•Problemas de formatação em 4 dos 7 cabeçalhos: Mistura de maiúsculas/minúsculas, espaços desnecessários e uso de camelCase, que dificultam a manipulação de dados; \n",
    "\n",
    "Ex.: ' userID' (espaço no início e camelCase) deveria ser 'user_id' (snake_case).\n",
    " \n",
    "•Foram identificados 10.108 valores ausentes nas colunas track, artist, genre, deste total, 1.198 apenas na coluna genre. A coluna genre merece atenção especial pois é a coluna que permite comparar as preferências musicais entre Springfield e Shelbyville. Ao invés de remover as linhas com os mesmos, substitui por 'unknown' utilizando o método .fillna(), pois a remoção dessas linhas eliminaria informações ainda válidas para análise, como cidade e gênero musical.\n",
    "\n",
    "•Foram identificadas 3.826 linhas duplicadas em um total de 65.079 registros (5,87%), e após a limpeza das mesmas restaram 61.253 linhas, utilizando o método .duplicated().sum() para verificação de quantas duplicatas existem, .drop_duplicates(inplace=True) para remoção das mesmas  e .duplicated().sum() para verificação final. A não remoção dos mesmo causa inflação de contagens e distorção de resultados.\n",
    "\n",
    "•Foram identificados gêneros duplicados implícitos, que seriam hip, hop e hip-hop. Dentro do corpo da função, foi utilizado o ciclo 'for' para percorrer a lista de gêneros errados, extrair a coluna 'genre' que seria nossa coluna de interesse e assim aplicar o método .replace() para fazer as correções, e o método .unique() para verificação de que não teríamos mais gêneros duplicados implícitos.\n",
    "\n",
    "\n",
    "3. Teste da hipótese\n",
    " O objetivo da hipótese testada é que a atividade dos usuários é diferente dependendo do dia da semana e da cidade. A mesma pode ser comprovada com os dados analisados que mostram padrões totalmente diferentes entre ambas as cidades. Em Springfield foram registradas altas atividades na segunda feira (15740) e sexta feira (15945), com queda significativa na quarta feira (11056). Já em Shelbyville foi registrado um pico de atividade na quarta feira (7003), resultando segunda feira (5614) e sexta feira (5895) com uma menor atividade.\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-block alert-success\">\n",
    "<b>Comentário: </b> <a class=\"tocSkip\"></a>\n",
    "\n",
    "Você utilizou corretamente `groupby()` para analisar as reproduções por cidade e por dia da semana. Além disso, implementou a função `number_tracks()` corretamente, realizando os filtros necessários e retornando o resultado esperado.\n",
    "\n",
    "Também foi positivo ver que você executou as chamadas da função para diferentes combinações de cidade e dia, validando o comportamento da solução. Além disso, suas observações são pertinentes e batem com o código que foi executado no notebook. \n",
    "\n",
    "Como sugestão, recomendo que explore mais a formatação do markdown para que seus textos sejam exibidos de forma mais elegante\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "azLHu64yOIp7"
   },
   "source": [
    "### Importante\n",
    "Em projetos de pesquisas reais, o teste estatístico de hipóteses é mais preciso e quantitativo. Observe também que conclusões sobre uma cidade inteira nem sempre podem ser tiradas a partir de dados de apenas uma fonte.\n",
    "\n",
    "Você aprenderá mais sobre testes de hipóteses no sprint sobre a análise estatística de dados."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "id": "Ju4AHDSgV1FE"
   },
   "source": [
    "[Voltar ao Índice](#back)"
   ]
  }
 ],
 "metadata": {
  "colab": {
   "collapsed_sections": [
    "E0vqbgi9ay0H",
    "VUC88oWjTJw2"
   ],
   "provenance": []
  },
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.23"
  },
  "toc": {
   "base_numbering": 1,
   "nav_menu": {},
   "number_sections": true,
   "sideBar": true,
   "skip_h1_title": true,
   "title_cell": "Table of Contents",
   "title_sidebar": "Contents",
   "toc_cell": false,
   "toc_position": {},
   "toc_section_display": true,
   "toc_window_display": false
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
