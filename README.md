# Poll_Enrich_com_FTP
# :rocket: SAP BTP CPI - Poll Enrich com FTP




Neste artigo é demonstrado como implementar o padrão de integração Content Enricher utilizando o componente Poll Enrich no SAP Integration Suite (Cloud Integration).

O cenário recebe uma requisição HTTP contendo uma lista de fornecedores em formato XML. 

Durante o processamento do iFlow, o componente Poll Enrich consulta um servidor FTP externo para recuperar informações adicionais dos fornecedores, como CNPJ, categoria e dados bancários.

Após a recuperação dos dados no FTP, o algoritmo de agregação REPLACE é utilizado para substituir o payload original pelo conteúdo enriquecido. 

O resultado final é então gravado novamente em um servidor FTP como arquivo de saída.

Esse cenário demonstra uma arquitetura comum de integração onde dados são enriquecidos a partir de uma fonte externa durante o fluxo de processamento.

![Capa](imagens/capa-linkedin.png)

<br><br>

📊 Exemplo Prático do Fluxo

<br>

### Criando nosso Iflow
![Fluxo](imagens/Screenshot_1.png)

```
PollEnrichwithFTP
```

<br>

### Criando o Integration Flow
![Fluxo](imagens/Screenshot_2.png)
```
PollEnrich_FTP_SupplierData_Integration
```

<br>

### Criar nosso Manage Security
![Fluxo](imagens/Screenshot_3.png)

<br>

### Criando nossas credenciais  para o FTP
![Fluxo](imagens/Screenshot_4.png)

<br>

### Adicionando o User para as credenciais do FTP
![Fluxo](imagens/Screenshot_5.png)
```
FTP_USER
```

<br>

### Adicionando um novo Sender
![Fluxo](imagens/Screenshot_6.png)

<br>

### Renomeando nosso Sender
![Fluxo](imagens/Screenshot_7.png)
```
FTP
```
<br>

### Sender vamos conectar no Start
![Fluxo](imagens/Screenshot_8.png)

<br>

### Adicionando o endereço do nosso Endpoint
![Fluxo](imagens/Screenshot_9.png)
```
Address: /pollenrich/ftp
```

<br>

### Selecionar o External Call
![Fluxo](imagens/Screenshot_10.png)

<br>

### Adicionando o Poll Enrich
![Fluxo](imagens/Screenshot_11.png)

<br>

### Vamos conectar o Sender no Poll Enrich
![Fluxo](imagens/Screenshot_12.png)

<br>

### Selecionar o FTP
![Fluxo](imagens/Screenshot_13.png)

<br>

### Adicionando as configurações do FTP no Source
![Fluxo](imagens/Screenshot_14.png)

<br>

### Adicionando as configurações do FTP no Processing
![Fluxo](imagens/Screenshot_15.png)

<br>

### Conectar o End no Receiver
Aqui vamos salvar o conteudo dentro do FTP.
![Fluxo](imagens/Screenshot_16.png)

<br>

### Selecionar nosso adapter do FTP
![Fluxo](imagens/Screenshot_17.png)

<br>

### Adicionando as configurações do FTP no Target
Aqui vamos definir o nome do nosso arquivo 
```
output.xml
```

![Fluxo](imagens/Screenshot_18.png)


<br>

### Adicionando as configurações do FTP no Processing
![Fluxo](imagens/Screenshot_19.png)


<br>

### Configuração no WINSCP para p FTP
![Fluxo](imagens/Screenshot_20.png)


<br>

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

<br>

### Configurando o Postman
![Fluxo](imagens/Screenshot_22.png)

<br>

### No FTP arquivo output.xml
![Fluxo](imagens/Screenshot_23.png)
```

<br>

### Abrindo o arquivo Output.xml
![Fluxo](imagens/Screenshot_24.png)

<br>

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






<br><br>

## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow – PollEnrich_FTP_](https://github.com/souzajean/Poll_Enrich_com_FTP/raw/main/Package/PollEnrich_FTP_SupplierData_Integration.zip)




> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

