{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "toc_visible": true,
      "authorship_tag": "ABX9TyMvyXl8HDrOM7/Y7803BuLG",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/dxspimentel/PUC/blob/main/README.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "# **PUC_MVP_Aprender_Conectado**"
      ],
      "metadata": {
        "id": "cOHLiI3Oouf6"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "##Um pouco sobre o tema"
      ],
      "metadata": {
        "id": "JAOWTfdkrHMv"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "O projeto \"**Aprender Conectado**\" é uma iniciativa do governo federal brasileiro que visa levar internet de alta velocidade para escolas públicas de educação básica, com o objetivo de transformar o processo de aprendizagem e ampliar o acesso ao conhecimento para alunos e professores. O projeto faz parte da Estratégia Nacional de Escolas Conectadas (ENEC) e é financiado com recursos do leilão do 5G.\n",
        "\n",
        "Este projeto é monitorado pela Entidade Administradora da Conectividade de Escolas (EACE), responsável pela implementação do mesmo, em parceria com o MEC, Ministério das Comunicações e Anatel, e supervisionado pelo Grupo de Acompanhamento do Custeio a Projetos de Conectividade de Escolas (GAPE), formado por 5 grandes empresas de Telecom do Brasil."
      ],
      "metadata": {
        "id": "YuvSlCFgpJG6"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Qual a proposta do MVP?"
      ],
      "metadata": {
        "id": "JO2Z71c6rNJf"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Neste trabalho, será desenvolvida uma solução que facilite a identificação de quais escolas foram de fato entregues, sem pendências, dentro do universo de escolas com obras já contratadas.\n"
      ],
      "metadata": {
        "id": "fK_wFPpNpCx9"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Cada escola tem a sua particularidade, com isso trabalha com escopo específico. O escopo de cada projeto é dividido em 3 tipos de obras:<br>\n",
        "1) Rede Interna<br>\n",
        "2) Rede Externa<br>\n",
        "3) Gerador Solar\n",
        "\n",
        "A questão é analisar se as etapas previstas em cada escola foram concluídas e com isso classificar como Conectada."
      ],
      "metadata": {
        "id": "8cjOgLHduhJP"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Porque?"
      ],
      "metadata": {
        "id": "yB-YD54WtADE"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "A quantidade de escolas contempladas é bastante expressiva (já passa de 15 mil escolas e com previsão de mais contratação) e atualmente o acompanhamento de evolução das obras é bastante manual, apensar de contar com a ferramenta (Aniel - nosso sistema de workflow)."
      ],
      "metadata": {
        "id": "Y_UcmAPCtChO"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Como?"
      ],
      "metadata": {
        "id": "zJpVxgrSs3c6"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Serão utilizadas 2 bases para montar o nosso Dataset:\n",
        "- **Base de Projetos**: listando as atividades já realizadas em campo, com seus devidos status e agrupamentos por tipo de obra. É uma base exportada do Aniel.\n",
        "- **Base de Escopo**: Listagem das escolas contempladas até a fase atual do projeto, com os respectivos escopos (Rede Interna, Rede Externa e Gerador Solar)."
      ],
      "metadata": {
        "id": "1XHcXxd2s6E8"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "A **Base de Projetos** está verticalizada, ou seja, os status das etapas estão empilhados. Já a **Base de Escopo** já está bem definida, trazendo os escopos em 3 colunas distintas, para cada projeto, além da informação se a escola já está conectada (Sim/Não)."
      ],
      "metadata": {
        "id": "QpupLmuxvq6Q"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Para cruzar as bases, será necessário fazer uma análise exploratória em ambas, para enteder o conteúdo de cada uma e aplicar os tratamentos corretos, antes de realizar o cruzamento entre elas e comparar escopo com execução."
      ],
      "metadata": {
        "id": "pXxG3r2Ov3GW"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "###Linguagem / Repositório / Links"
      ],
      "metadata": {
        "id": "JyQ1IhAqwWe5"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Para rodar este projeto, é necessário ter o Python 3.1+ instalado, juntamente com as seguintes bibliotecas:\n",
        "- pandas\n",
        "- matplotlib\n",
        "- seaborn\n",
        "- sklearn (esta apenas na etapa de Machine Learning)"
      ],
      "metadata": {
        "id": "xs4JXdahw2vZ"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "As bases estão disponíveis no Github.<br>\n",
        "- https://github.com/dxspimentel/PUC\n",
        "\n",
        "URLs importadas<br>\n",
        "- github_projetos<br>\n",
        "'https://raw.githubusercontent.com/dxspimentel/PUC/main/PUC_Db_01_Base_Projetos.csv'\n",
        "- github_escopo<br>\n",
        "'https://raw.githubusercontent.com/dxspimentel/PUC/main/PUC_Db_02_Base_Escopo.csv'"
      ],
      "metadata": {
        "id": "sggIlIhux5JB"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "### Classificação"
      ],
      "metadata": {
        "id": "TIJGyzsV2ubi"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "O alvo do trabalho é classificar a Escola como conectada ou não. Para isso a lógica utilizada será, por exemplo:\n",
        "\n",
        "- Escola: 567235\n",
        "- Escopo: RE + RI + GS (os 3 serviços possíveis)\n",
        "\n",
        "Cruzaremos as bases, utilizando a coluna **PROJETO** como chave, para saber se a escola 567235 tem os 3 serviços concluídos (**STATUS_RDO** = '*Aprovado Sala Técnica*'). Se sim, a escola será classificada como conectada '*Sim*', caso contrário, conectada '*Não*'.  "
      ],
      "metadata": {
        "id": "EYexk16z3qO_"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Característas dos DataFrames"
      ],
      "metadata": {
        "id": "PQGXX2vD6GPC"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Tratamentos aplicados"
      ],
      "metadata": {
        "id": "lXAMbP3X6LUH"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "## Conclusão"
      ],
      "metadata": {
        "id": "WuubIcE76T-n"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Para esta etapa do trabalho, consegui identificar em ambos DataFrames as necessidades de tratamentos/limpeza e respectivas soluções. Em seguida o cruzamento das tabelas foi bem sucedido, e a visualização dos dados satisfatória, demostrando que o Dataset final está pronto para ser utilizado em Machine Learning."
      ],
      "metadata": {
        "id": "kHs3hAea7nPB"
      }
    }
  ]
}