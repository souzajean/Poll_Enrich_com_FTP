# Poll_Enrich_com_FTP
SAP BTP CPI - Poll Enrich com FTP


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


### Adicionando o External Call
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



### Adicionando o Mapping
![Fluxo](imagens/Screenshot_21.png)


### Adicionando o Source Mapping
![Fluxo](imagens/Screenshot_22.png)


### Selecionando o Message
![Fluxo](imagens/Screenshot_23.png)
```
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="ResultsPokemon">
    <xs:complexType>
      <xs:sequence>
        <xs:element type="xs:string" name="form_name"/>
        <xs:element type="xs:string" name="form_names"/>
        <xs:element type="xs:byte" name="form_order"/>
        <xs:element type="xs:byte" name="id"/>
        <xs:element type="xs:string" name="is_battle_only"/>
        <xs:element type="xs:string" name="is_default"/>
        <xs:element type="xs:string" name="is_mega"/>
        <xs:element type="xs:string" name="name"/>
        <xs:element type="xs:string" name="names"/>
        <xs:element type="xs:byte" name="order"/>
        <xs:element name="pokemon">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:string" name="name"/>
              <xs:element type="xs:string" name="url"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="sprites">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:string" name="back_default"/>
              <xs:element type="xs:string" name="back_female"/>
              <xs:element type="xs:string" name="back_shiny"/>
              <xs:element type="xs:string" name="back_shiny_female"/>
              <xs:element type="xs:string" name="front_default"/>
              <xs:element type="xs:string" name="front_female"/>
              <xs:element type="xs:string" name="front_shiny"/>
              <xs:element type="xs:string" name="front_shiny_female"/>
              <xs:element name="versions">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element name="generation-ix">
                      <xs:complexType>
                        <xs:sequence>
                          <xs:element name="scarlet-violet">
                            <xs:complexType>
                              <xs:sequence>
                                <xs:element type="xs:string" name="front_default"/>
                                <xs:element type="xs:string" name="front_female"/>
                              </xs:sequence>
                            </xs:complexType>
                          </xs:element>
                        </xs:sequence>
                      </xs:complexType>
                    </xs:element>
                    <xs:element name="generation-viii">
                      <xs:complexType>
                        <xs:sequence>
                          <xs:element name="brilliant-diamond-shining-pearl">
                            <xs:complexType>
                              <xs:sequence>
                                <xs:element type="xs:string" name="front_default"/>
                                <xs:element type="xs:string" name="front_female"/>
                              </xs:sequence>
                            </xs:complexType>
                          </xs:element>
                        </xs:sequence>
                      </xs:complexType>
                    </xs:element>
                  </xs:sequence>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="types" maxOccurs="unbounded" minOccurs="0">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:byte" name="slot"/>
              <xs:element name="type">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element type="xs:string" name="name"/>
                    <xs:element type="xs:string" name="url"/>
                  </xs:sequence>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="version_group">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:string" name="name"/>
              <xs:element type="xs:string" name="url"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```


### Selecionando o PokemonAPI.xsd
![Fluxo](imagens/Screenshot_24.png)
```
PokemonAPI.xsd
```
📦 [Download do PokemonAPI.xsd – Integração com API Pokémon](https://github.com/souzajean/PokemonAPIMapping/blob/main/ArquivosXSD/PokemonAPI.xsd)










## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow – Integração com API PokemonAPIMapping](https://github.com/souzajean/PokemonAPIMapping/raw/main/Package/Integracao_com_API_Pokemon_Mapping.zip)

> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

