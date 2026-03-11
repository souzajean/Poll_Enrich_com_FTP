# Poll_Enrich_com_FTP
SAP BTP CPI - Poll Enrich com FTP


Neste artigo é demonstrado como implementar o padrão de integração Content Enricher utilizando o componente Poll Enrich no SAP Integration Suite (Cloud Integration).

O cenário recebe uma requisição HTTP contendo uma lista de fornecedores em formato XML. 

Durante o processamento do iFlow, o componente Poll Enrich consulta um servidor FTP externo para recuperar informações adicionais dos fornecedores, como CNPJ, categoria e dados bancários.

Após a recuperação dos dados no FTP, o algoritmo de agregação REPLACE é utilizado para substituir o payload original pelo conteúdo enriquecido. 

O resultado final é então gravado novamente em um servidor FTP como arquivo de saída.

Esse cenário demonstra uma arquitetura comum de integração onde dados são enriquecidos a partir de uma fonte externa durante o fluxo de processamento.



