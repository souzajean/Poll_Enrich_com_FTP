# Poll_Enrich_com_FTP
SAP BTP CPI - Poll Enrich com FTP


![Capa](imagens/capa-linkedin.png)

Neste artigo é demonstrado como implementar o padrão de integração Content Enricher utilizando o componente Poll Enrich no SAP Integration Suite (Cloud Integration).

O cenário recebe uma requisição HTTP contendo uma lista de fornecedores em formato XML. 

Durante o processamento do iFlow, o componente Poll Enrich consulta um servidor FTP externo para recuperar informações adicionais dos fornecedores, como CNPJ, categoria e dados bancários.

Após a recuperação dos dados no FTP, o algoritmo de agregação REPLACE é utilizado para substituir o payload original pelo conteúdo enriquecido. 

O resultado final é então gravado novamente em um servidor FTP como arquivo de saída.

Esse cenário demonstra uma arquitetura comum de integração onde dados são enriquecidos a partir de uma fonte externa durante o fluxo de processamento.



📊 Exemplo Prático do Fluxo

### Criando nosso Iflow
![Fluxo](imagens/Screenshot_1.png)
```
PollEnrichwithFTP
```

### Criando o Integration Flow
![Fluxo](imagens/Screenshot_2.png)
```
PollEnrich_FTP_SupplierData_Integration
```


### Criar nosso Manage Security
![Fluxo](imagens/Screenshot_3.png)


### Criando nossas credenciais  para o FTP
![Fluxo](imagens/Screenshot_4.png)


### Adicionando o User para as credenciais do FTP
![Fluxo](imagens/Screenshot_5.png)
```
FTP_USER
```


### Adicionando um novo Sender
![Fluxo](imagens/Screenshot_6.png)


### Renomeando nosso Sender
![Fluxo](imagens/Screenshot_7.png)
```
FTP
```

### Sender vamos conectar no Start
![Fluxo](imagens/Screenshot_8.png)


### Adicionando o endereço do nosso Endpoint
![Fluxo](imagens/Screenshot_9.png)
```
Address: /pollenrich/ftp
```


### Selecionar o External Call
![Fluxo](imagens/Screenshot_10.png)


### Adicionando o Poll Enrich
![Fluxo](imagens/Screenshot_11.png)


### Vamos conectar o Sender no Poll Enrich
![Fluxo](imagens/Screenshot_12.png)


### Selecionar o FTP
![Fluxo](imagens/Screenshot_13.png)


### Adicionando as configurações do FTP no Source
![Fluxo](imagens/Screenshot_14.png)


### Adicionando as configurações do FTP no Processing
![Fluxo](imagens/Screenshot_15.png)


### Conectar o End no Receiver
Aqui vamos salvar o conteudo dentro do FTP.
![Fluxo](imagens/Screenshot_16.png)


### Selecionar nosso adapter do FTP
![Fluxo](imagens/Screenshot_17.png)


### Adicionando as configurações do FTP no Target
Aqui vamos definir o nome do nosso arquivo 
```
output.xml
```

![Fluxo](imagens/Screenshot_18.png)



### Adicionando as configurações do FTP no Processing
![Fluxo](imagens/Screenshot_19.png)


### Configuração no WINSCP para p FTP
![Fluxo](imagens/Screenshot_20.png)



### XML Original
```
<?xml version="1.0" encoding="UTF-8"?>
<SupplierDetails>
    
    <Supplier>
        <SupplierID>SUP-1001</SupplierID>
        <CNPJ>99.999.999/0001-99</CNPJ>
        <Category>Materiais de Escritório</Category>
        <PaymentTerms>30</PaymentTerms>
        <Bank>
            <BankName>Banco do Brasil</BankName>
            <Agency>1234</Agency>
            <Account>98765-0</Account>
        </Bank>
    </Supplier>

    <Supplier>
        <SupplierID>SUP-1002</SupplierID>
        <CNPJ>11.222.333/0001-44</CNPJ>
        <Category>Distribuidor</Category>
        <PaymentTerms>45</PaymentTerms>
        <Bank>
            <BankName>Itaú</BankName>
            <Agency>5678</Agency>
            <Account>12345-9</Account>
        </Bank>
    </Supplier>

</SupplierDetails>
```

![Fluxo](imagens/Screenshot_21.png)


### Configurando o Postman
![Fluxo](imagens/Screenshot_22.png)


### No FTP arquivo output.xml
![Fluxo](imagens/Screenshot_23.png)
```
<?xml version="1.0" encoding="UTF-8"?>
<SupplierDetails>
    
    <Supplier>
        <SupplierID>SUP-1001</SupplierID>
        <CNPJ>99.999.999/0001-99</CNPJ>
        <Category>Materiais de Escritório</Category>
        <PaymentTerms>30</PaymentTerms>
        <Bank>
            <BankName>Banco do Brasil</BankName>
            <Agency>1234</Agency>
            <Account>98765-0</Account>
        </Bank>
    </Supplier>

    <Supplier>
        <SupplierID>SUP-1002</SupplierID>
        <CNPJ>11.222.333/0001-44</CNPJ>
        <Category>Distribuidor</Category>
        <PaymentTerms>45</PaymentTerms>
        <Bank>
            <BankName>Itaú</BankName>
            <Agency>5678</Agency>
            <Account>12345-9</Account>
        </Bank>
    </Supplier>

</SupplierDetails>
```


### Selecionando o PokemonAPI.xsd
![Fluxo](imagens/Screenshot_24.png)





## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow – PollEnrich_FTP_](https://github.com/souzajean/Poll_Enrich_com_FTP/raw/main/Package/PollEnrich_FTP_SupplierData_Integration.zip)




> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

