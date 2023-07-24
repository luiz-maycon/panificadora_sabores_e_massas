# Panificadora Sabores & Massas

## 1.0 Contexto do Negócio
Há, no interior do Rio Grande do Norte, uma pequena padaria chamada Sabores & Massas com mais de dez anos de idade e que possuia praticamente todos os seus dados anotados em cadernos. Conforme a empresa crescia, foi se tornando cada vez mais difícil manter todos esses dados organizados. Em algum momento, o antigo gerente introduziu um sistema de gerenciamento para auxiliar nas questões burocráticas com a Receita Federal.

Os novos gastos gerados (tanto em tempo como recursos) de fato resolveram tais questões, mas não trouxeram outros benefícios para a empresa , de modo que ela continuava com a maior parte dos seus dados anotados em papeis e, consequentemente, sem conhecê-los com afinco, sem conseguir explorá-los.

O sistema escolhido, assim como os outros consultados na região, foca em auxiliar as empresas na parte burocrática, sendo muito padronizado e pouco eficiente em questões mais específicas, principalmente para empresas não habituadas ao uso de tecnologia. Além disso, a Sabores & Massas não possuia orçamento e conhecimento suficiente para contratar uma empresa para que construisse o seu próprio software - e a questão da falta de conhecimento também impacta na busca por softwares já desenvolvidos para padarias pelo fato de não haver suporte na região.

Foi conhecendo esses problemas que um analista de dados, que já convivia diariamente dentro da empresa, decidiu agir buscando uma solução. Ele concluiu que uma boa solução seria adaptar, inicialmente, a tecnologia ao formato de trabalho da empresa (e não o contrário, como fazia o sistema adotado), fazendo uma engenharia de dados, criando um ambiente tecnológico que facilitasse o dia a dia da empresa e a habituasse, aos poucos, ao uso de tecnologia e à coleta de dados visualizando, para o longo prazo, a tornar data driven (com decisões orientadas a dados). 

## 2.0 Premissas
**2.1** Esse projeto foi desenvolvido com três principais objetivos: I) incentivar uma pequena empresa a adotar tecnologia na sua rotina de trabalho; II) ajudar tal empresa, através do uso de dados, a se conhecer melhor; e III) ajudar o desenvolvedor do projeto a estudar sobre como implementar a cultura de tomada de decisão orientada a dados em micro e pequenas empresas.

**2.2** As propostas de solução aqui apresentadas poderão não serem as melhores dentre as várias opções, pois, além do citado no ponto 2.1, deve-se considerar que o foco está na agilidade para por as soluções em prática e na praticidade de uso, dado que os consumidores das soluções (a empresa) não estão acostumados a tais tecnologias.

**2.3** Assim sendo, baseado no que foi dito nos pontos anteriores, após se sentir confortável, a empresa pode usar o presente projeto para auxiliar na escolha de um sistema de gerenciamento mais robusto que se encaixe nos seus padrões ou até (aconselhado pelo desenvolvedor) auxiliar na criação de um software próprio oferecido por empresas que têm esse foco na automação de pequenos negócios.

**2.4** Esse projeto não é uma versão final. As soluções aqui propostas estão sendo colocadas em prática e avaliadas para que sejam feitas modificações conforme mais atualizações sejam desenvolvidas e as já desenvolvidas sejam revisadas. Dessa forma, esse projeto continuará sendo atualizado conforme mais resultados sejam alcançados.

**2.5** Por questões privacidade, os dados que aparecem nas imagens utilizadas no projeto foram devidamente alterados, de modo que não representam os reais valores.

## 3.0 Planejamento da Solução
**3.1 Produto Final**
O resultado a ser entregue pelo analista para uso da empresa é, até o momento - lembrando da quarta premissa: I) uma ferramenta que possa coletar e armazenar os dados de três setores nomeados como “Faturamento & Despesas”, “Delivery” e “Produção”; e II) um dashboard para cada setor.

**3.2 Processo**
Sendo que, o que fosse produzido, seria imediatamente colocado em prática e avaliado, o processo de construção foi dividido em ciclos onde a execução de um depende dos resultados de seu anterior, isso inclui uma revisão (e tentativa de melhora) em tudo o que já foi feito para, em seguida, introduzir uma nova funcionalidade. A seguir, estão todos os ciclos planejados até o momento:
- “Ciclo 01: coletar os dados de Faturamento & Despesas e Delivery”, o que inclui criar duas planilhas com suas interfaces e bases de dados.
- “Ciclo 02: criar os dashboards de Faturamento & Despesas e Delivery”, sendo necessário esperar alguns dias para que uma boa base de dados seja coletada e, assim, possam ser gerados dashboards com gráficos já planejados, mas que serão limitados pela qualidade e quantidade dos dados que estarão disponíveis.
- “Ciclo 03: coletar os dados e criar o dashboard de Produção”. Conforme os dois primeiros ciclos sejam bem-sucedidos, a estrutura será replicada para abranger outros setores importantes. Nesse caso, se trata do controle da produção.
- “Ciclo 04: Migrar as bases de dados do Sheets para um banco de dados”. Aqui (e no ciclo seguinte) o objetivo se torna ganhar eficiência e segurança, iniciando pelo armazenamento, na adoção de banco de dados.
- “Ciclo 05: Migrar as interfaces do Sheets para uma interface própria”. Segue o caminho do ciclo anterior, melhorando imensamente o processo da coleta dos dados e a experiência do usuário.

É importante ressaltar que novos ciclos podem ser acrescentados durante o processo. Abaixo está uma figura que representa o estado atual do planejamento:

<p align="center">
  <img src="/img/excalidraw/ciclos_de_construcao.png">
</p>

<p align="center">
  Figura 01: Ciclos de Construção do Projeto.
</p>

**3.3 Ferramentas**
- Google Sheets
- Google Apps Script
- Google Looker Studio

## 4.0 Construção
**4.1 Ciclo 1: Coletar os dados de Faturamento e Despesas e Delivery**
Esta etapa, o pontapé inicial do projeto, surgiu pelo fato da liderança da empresa fazer suas anotações diárias de faturamento e despesas em cadernos. A ideia foi, então, fazer com que fosse utilizada uma planilha para fazer tais anotações de forma mais rápida, fazendo também com que os dados ficassem melhor armazenados em comparação aos cadernos, além de possibilitar futuras análises descritivas para que o empreendedor pudesse compreender melhor o que estava acontecendo em sua empresa. A seguir estão imagens de como está atualmente a planilha “Faturamento & Despesas”:

<p align="center">
  <img src="/img/telas/fatudesp01.png">
</p>

<p align="center">
  Figura 02: tela MENU da planilha Faturamento & Despesas. Apresenta duas tabelas a serem preenchidas. Na primeira o usuário preenche o faturamento do dia separado pelo tipo (dinheiro, cartão e pix) - a data e o valor total já vêm automaticamente. A segunda tabela apresenta uma lista suspensa para o usuário escolher a despesa e, ao lado, colocar o valor (o total vem automaticamente). Além disso, a planilha possui os botões HISTÓRICO que foi criado com um macro que direciona o usuário para uma página que será explicada a seguir e FECHAR DIA que executa a função no script* que salva os dados na base de dados.
</p>

<p align="center">
  <img src="/img/telas/fatudesp02.png">
</p>

<p align="center">
  Figura 03: página HISTORICO da planilha Faturamento & Despesas. Nela é possível consultar os dados de qualquer data desejada pelo usuário através de funções query. Além disso, possui o botão MENU, que utiliza uma macro para retornar para a paǵina principal.
</p>

<p align="center">
  <img src="/img/telas/fatudesp03.png">
  <img src="/img/telas/fatudesp04.png">
</p>

<p align="center">
  Figuras 04 e 05: páginas DB_FATURAMENTO e DB_DESPESAS da planilha Faturamento & Despesas. Essas são as duas bases de dados onde os dados coletados são armazenados.
</p>

<p align="center">
  <img src="/img/telas/fatudesp05.png">
</p>

<p align="center">
  Figura 06: página LISTA_DESPESAS da planilha Faturamento & Despesas. Essa é a lista de despesas que gera a lista suspensa conforme vista na figura 02.
</p>

Já se tratando da planilha “Delivery”, essa surgiu de forma bem mais simplificada com o intuito de consolidar as entregas feitas através de dois aplicativos de delivery e pelo Whatsapp. Com o melhor desenvolvimento da Faturamento & Despesas, veio a ideia de adaptar também para essa planilha. Dessa forma, ela foi construída seguindo os mesmos princípios citados anteriormente e conforme as imagens abaixo:

<p align="center">
  <img src="/img/telas/delivery01.png">
</p>

<p align="center">
  Figura 07: página MENU da planilha Delivery. Possui uma tabela com uma coluna para os valores de cada venda, uma coluna com uma lista suspensa trazendo os valores para cada entrega e uma coluna com outra lista suspensa com os tipos de pagamento. Há outra pequena tabela preenchida automaticamente que traz algumas informações gerais e dois botões: FECHAR DIA, que armazena os dados na base de dados através de um script, e IMPRIMIR, que, através de dois scripts, gera um arquivo pdf e o imprime.
</p>

<p align="center">
  <img src="/img/telas/delivery02.png">
</p>

<p align="center">
  Figura 08: página IMPRIMIR da planilha Delivery. Consolida as principais informações das entregas feitas no dia e utiliza dois scripts para gerar um arquivo pdf e o imprimir.
</p>

<p align="center">
  <img src="/img/telas/delivery03.png">
</p>

<p align="center">
  Figura 09: página DB_DELIVRY da planilha Delivery. É a base de dados onde os dados coletados são armazenados.
</p>

###### *Todos os scripts citados podem ser conferidos na pasta “scripts” em formato txt.
