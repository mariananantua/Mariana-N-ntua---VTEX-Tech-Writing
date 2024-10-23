# How to invoice an order and send its tracking number

Invoicing an order is the last step of the [order flow](https://help.vtex.com/en/tutorial/fluxo-e-status-de-pedidos--tutorials_196) and it means that the order was successfully completed. After shipping the order, you can add its tracking number by updating the order's partial invoice. 

You can find more information on the sections below.

## Invoice an order
Adding the invoice to the order changes its status to `invoiced`. After that, you cannot change the order status.

Before making this request, make sure you have the necessary [permissions](https://developers.vtex.com/docs/api-reference/orders-api#post-/api/oms/pvt/orders/-orderId-/invoice).

You can send the invoice:

* Through [VTEX Admin](https://help.vtex.com/en/tutorial/how-to-manually-invoice-an-order--7p1h852V5t54KyscpgxE2v).
* Through API.


To invoice an order through API:


1. Send a POST request to the following endpoint:
```
https://{accountName}.{environment}.com.br/api/oms/pvt/orders/{orderId}/invoice
```

2.  Include the required parameters for this request:

* `type`: the type of invoice. You can use one of the following values:
	* Output:	for a selling invoice.
	* Input: for a return invoice. 
* `issuanceDate`: the date the order was invoiced in the VTEX platform.
* `invoiceNumber`: the unique code that identifies the invoice.
* `invoiceValue`: the total amount in cents.
* `items`: an array containing the SKUs invoiced.
	* `id`: ID of the SKU invoiced.
	* `price`: prince of the SKU in cents.
	* `quantity`: the amount of the SKU in inventory.

> You can access the [full list of the parameters](https://developers.vtex.com/docs/api-reference/orders-api#post-/api/oms/pvt/orders/-orderId-/invoice) for this request.

Here's an example using Python:

```python
import http.client

conn = http.client.HTTPSConnection("apiexamples.vtexcommercestable.com.br")

payload = "{\"type\":\"Output\",\"issuanceDate\":\"2024-01-31T18:25:43-05:00\",\"invoiceNumber\":\"DFG-v7731485plzv-01\",\"invoiceValue\":\"2499\",\"invoiceKey\":\"CFe35201100063960001504590006629690333214542150\",\"invoiceUrl\":\"https://luxstore.com/invoices/24382.pdf\",\"embeddedInvoice\":\"<NFe>\\r\\n<infNFe Id=\\\"NFe34687999999090910270550010000000015180000000000\\\" versao=\\\"1.10\\\">\\r\\n<ide>\\r\\n<cUF>37</cUF>\\r\\n<cNF>000005177</cNF>\\r\\n<natOp>Venda a vista</natOp>\\r\\n<indPag>0</indPag>\\r\\n<mod>55</mod>\\r\\n<serie>1</serie>\\r\\n<nNF>1</nNF>\\r\\n<dEmi>2018-07-06</dEmi>\\r\\n<dSaiEnt>2018-07-06</dSaiEnt>\\r\\n<tpNF>0</tpNF>\\r\\n<cMunFG>79950308</cMunFG>\\r\\n<tpImp>1</tpImp>\\r\\n<tpEmis>1</tpEmis>\\r\\n<cDV>3</cDV>\\r\\n<tpAmb>2</tpAmb>\\r\\n<finNFe>1</finNFe>\\r\\n<procEmi>0</procEmi>\\r\\n<verProc>NF-eletronica.com</verProc>\\r\\n</ide>\\r\\n<emit>\\r\\n<CNPJ>99999090998760</CNPJ>\\r\\n<xNome>NF-e Associacao NF-e</xNome>\\r\\n<xFant>NF-e</xFant>\\r\\n<enderEmit>\\r\\n<xLgr>Rua Central</xLgr>\\r\\n<nro>100</nro>\\r\\n<xCpl>Fundos</xCpl>\\r\\n<xBairro>Distrito Industrial</xBairro>\\r\\n<cMun>0000000</cMun>\\r\\n<xMun>Município</xMun>\\r\\n<UF>SP</UF>\\r\\n<CEP>0000000</CEP>\\r\\n<cPais>1058</cPais>\\r\\n<xPais>Brasil</xPais>\\r\\n<fone>1733021717</fone>\\r\\n</enderEmit>\\r\\n<IE>123456789012</IE>\\r\\n</emit>\\r\\n<dest>\\r\\n<CNPJ>00000000000000</CNPJ>\\r\\n<xNome>DISTRIBUIDORA DE AGUAS MINERAIS</xNome>\\r\\n<enderDest>\\r\\n<xLgr>AV DAS FONTES</xLgr>\\r\\n<nro>1777</nro>\\r\\n<xCpl>1001 ANDAR</xCpl>\\r\\n<xBairro>PARQUE</xBairro>\\r\\n<cMun>0000000</cMun>\\r\\n<xMun>Sao Paulo</xMun>\\r\\n<UF>SP</UF>\\r\\n<CEP>00000000</CEP>\\r\\n<cPais>1058</cPais>\\r\\n<xPais>BRASIL</xPais>\\r\\n<fone>3900000000</fone>\\r\\n</enderDest>\\r\\n<IE> </IE>\\r\\n</dest>\\r\\n<retirada>\\r\\n<CNPJ>000000000004</CNPJ>\\r\\n<xLgr>AV PAULISTA</xLgr>\\r\\n<nro>12345</nro>\\r\\n<xCpl>TERREO</xCpl>\\r\\n<xBairro>CERQUEIRA CESAR</xBairro>\\r\\n<cMun>0000000</cMun>\\r\\n<xMun>SAO PAULO</xMun>\\r\\n<UF>SP</UF>\\r\\n</retirada>\\r\\n<entrega>\\r\\n<CNPJ>00000000299000194</CNPJ>\\r\\n<xLgr>AV FARIA LIMA</xLgr>\\r\\n<nro>154400</nro>\\r\\n<xCpl>156 ANDAR</xCpl>\\r\\n<xBairro>PINHEIROS</xBairro>\\r\\n<cMun>0000308</cMun>\\r\\n<xMun>SAO PAULO</xMun>\\r\\n<UF>SP</UF>\\r\\n</entrega>\\r\\n<det nItem=\\\"1\\\">\\r\\n<prod>\\r\\n<cProd>00001</cProd>\\r\\n<cEAN/>\\r\\n<xProd>Agua Mineral</xProd>\\r\\n<CFOP>5101</CFOP>\\r\\n<uCom>dz</uCom>\\r\\n<qCom>1000000.0000</qCom>\\r\\n<vUnCom>1</vUnCom>\\r\\n<vProd>10000000.00</vProd>\\r\\n<cEANTrib/>\\r\\n<uTrib>und</uTrib>\\r\\n<qTrib>12000000.0000</qTrib>\\r\\n<vUnTrib>1</vUnTrib>\\r\\n</prod>\\r\\n<imposto>\\r\\n<ICMS>\\r\\n<ICMS00>\\r\\n<orig>0</orig>\\r\\n<CST>00</CST>\\r\\n<modBC>0</modBC>\\r\\n<vBC>10000000.00</vBC>\\r\\n<pICMS>18.00</pICMS>\\r\\n<vICMS>1800000.00</vICMS>\\r\\n</ICMS00>\\r\\n</ICMS>\\r\\n<PIS>\\r\\n<PISAliq>\\r\\n<CST>01</CST>\\r\\n<vBC>10000000.00</vBC>\\r\\n<pPIS>0.65</pPIS>\\r\\n<vPIS>65000</vPIS>\\r\\n</PISAliq>\\r\\n</PIS>\\r\\n<COFINS>\\r\\n<COFINSAliq>\\r\\n<CST>01</CST>\\r\\n<vBC>10000000.00</vBC>\\r\\n<pCOFINS>2.00</pCOFINS>\\r\\n<vCOFINS>200000.00</vCOFINS>\\r\\n</COFINSAliq>\\r\\n</COFINS>\\r\\n</imposto>\\r\\n</det>\\r\\n<det nItem=\\\"2\\\">\\r\\n<prod>\\r\\n<cProd>00002</cProd>\\r\\n<cEAN/>\\r\\n<xProd>Agua Mineral</xProd>\\r\\n<CFOP>5101</CFOP>\\r\\n<uCom>pack</uCom>\\r\\n<qCom>5000000.0000</qCom>\\r\\n<vUnCom>2</vUnCom>\\r\\n<vProd>10000000.00</vProd>\\r\\n<cEANTrib/>\\r\\n<uTrib>und</uTrib>\\r\\n<qTrib>3000000.0000</qTrib>\\r\\n<vUnTrib>0.3333</vUnTrib>\\r\\n</prod>\\r\\n<imposto>\\r\\n<ICMS>\\r\\n<ICMS00>\\r\\n<orig>0</orig>\\r\\n<CST>00</CST>\\r\\n<modBC>0</modBC>\\r\\n<vBC>10000000.00</vBC>\\r\\n<pICMS>18.00</pICMS>\\r\\n<vICMS>1800000.00</vICMS>\\r\\n</ICMS00>\\r\\n</ICMS>\\r\\n<PIS>\\r\\n<PISAliq>\\r\\n<CST>01</CST>\\r\\n<vBC>10000000.00</vBC>\\r\\n<pPIS>0.65</pPIS>\\r\\n<vPIS>65000</vPIS>\\r\\n</PISAliq>\\r\\n</PIS>\\r\\n<COFINS>\\r\\n<COFINSAliq>\\r\\n<CST>01</CST>\\r\\n<vBC>10000000.00</vBC>\\r\\n<pCOFINS>2.00</pCOFINS>\\r\\n<vCOFINS>200000.00</vCOFINS>\\r\\n</COFINSAliq>\\r\\n</COFINS>\\r\\n</imposto>\\r\\n</det>\\r\\n<total>\\r\\n<ICMSTot>\\r\\n<vBC>20000000.00</vBC>\\r\\n<vICMS>18.00</vICMS>\\r\\n<vBCST>0</vBCST>\\r\\n<vST>0</vST>\\r\\n<vProd>20000000.00</vProd>\\r\\n<vFrete>0</vFrete>\\r\\n<vSeg>0</vSeg>\\r\\n<vDesc>0</vDesc>\\r\\n<vII>0</vII>\\r\\n<vIPI>0</vIPI>\\r\\n<vPIS>130000.00</vPIS>\\r\\n<vCOFINS>400000.00</vCOFINS>\\r\\n<vOutro>0</vOutro>\\r\\n<vNF>20000000.00</vNF>\\r\\n</ICMSTot>\\r\\n</total>\\r\\n<transp>\\r\\n<modFrete>0</modFrete>\\r\\n<transporta>\\r\\n<CNPJ>00000000000000</CNPJ>\\r\\n<xNome>Distribuidora de Bebidas Fazenda de SP Ltda.</xNome>\\r\\n<IE>00000000999119</IE>\\r\\n<xEnder>Rua Central 100 - Fundos - Distrito Industrial</xEnder>\\r\\n<xMun>SAO PAULO</xMun>\\r\\n<UF>SP</UF>\\r\\n</transporta>\\r\\n<veicTransp>\\r\\n<placa>BXI1717</placa>\\r\\n<UF>SP</UF>\\r\\n<RNTC>123456789</RNTC>\\r\\n</veicTransp>\\r\\n<reboque>\\r\\n<placa>UUU0000</placa>\\r\\n<UF>SP</UF>\\r\\n<RNTC>123456789</RNTC>\\r\\n</reboque>\\r\\n<vol>\\r\\n<qVol>10000</qVol>\\r\\n<esp>CAIXA</esp>\\r\\n<marca>LINDOYA</marca>\\r\\n<nVol>500</nVol>\\r\\n<pesoL>1000000000.000</pesoL>\\r\\n<pesoB>1200000000.000</pesoB>\\r\\n<lacres>\\r\\n<nLacre>XYZ10231486</nLacre>\\r\\n</lacres>\\r\\n</vol>\\r\\n</transp>\\r\\n<infAdic>\\r\\n<infAdFisco>Nota Fiscal de exemplo NF-eletronica.com</infAdFisco>\\r\\n</infAdic>\\r\\n</infNFe>\\r\\n<Signature>\\r\\n<SignedInfo>\\r\\n<CanonicalizationMethod Algorithm=\\\"http://www.w3.org/TR/2001/REC-xml-c14n-0321120010315\\\"/>\\r\\n<SignatureMethod Algorithm=\\\"http://www.w3.org/2000/09/xmldsig#rsa-sha1\\\"/>\\r\\n<Reference URI=\\\"#NFe3508059999977777777705500100000000000000000\\\">\\r\\n<Transforms>\\r\\n<Transform Algorithm=\\\"http://www.w3.org/2000/09/xmldsig#enveloped-signature\\\"/>\\r\\n<Transform Algorithm=\\\"http://www.w3.org/TR/2001/REC-xml-c14n-66666615\\\"/>\\r\\n</Transforms>\\r\\n<DigestMethod Algorithm=\\\"http://www.w3.org/2000/09/xmldsig#sha1\\\"/>\\r\\n<DigestValue>xFzhgdgnhjSD1e9uqe04lnoHT4ZzLSY=</DigestValue>\\r\\n</Reference>\\r\\n</SignedInfo>\\r\\n<SignatureValue>\\r\\nIz5Z3PLQbzZt9jnBtr6xsmHZMOu/3plXG9xxfFjRCQYGnD1rjlhzBGrqt026Ca2VHHM/bHNepi6FuFkAi595GScKVuHREUotzifE2OIjgavvTOrMwbXG7+0LYgkwPFiPCao2S33UpZe7MneaxcmKQGKQZw1fP8fsWmaQ4cczZT8=\\r\\n</SignatureValue>\\r\\n<KeyInfo>\\r\\n<X509Data>\\r\\n<X509Certificate>\\r\\nMIIEuzCCA6OgAwIBAgIDMTMxMA0GasfFSDAGQUAMIGSMQswCQYDVQQGEwJCUjELMAkGA1UECBMCUlMxFTATBgNVBAcTDFBvcnRvIEFsZWdyZTEdMBsGA1UEChMUVGVzdGUgUHJvamV0byBORmUgUlMxHTAbBgNVBAsTFFRlc3RlIFByb2pldG8gTkZlIFJTMSEwHwYDVQQDExhORmUgLSBBQyBJbnRlcm1lZGlhcmlhIDEwHhcNMDgwNDI4MDkwMTAyWhcNMDkwNDMwMjM1OTU5WjCBnjELMAkGA1UECBMCUlMxHTAfvw4567DRhg76FByb2pldG8gTkZlIFJTMR0wGwYDVQQKExRUZXN0ZSBQcm9qZXRvIE5GZSBSUzEVMBMGA1UEBxMMUE9SVE8gQUxFR1JFMQswCQYDVQQGEwJCUjEtMCsGA1UEAxMkTkZlIC0gQXNzb2NpYWNhbyBORi1lOjk5OTk5MDkwOTEwMjcwMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDDh6RRv0bj4RYX+tDQrZRb5opa77LBVVs+6LphIfSF3TSWPfnKh0+xLlBFdmnB5YGgbbW9Uon6pZQTfaC8jZhRhI5eFRRofY/Ugoeo0NGt6PcIQNZQd6lLQ/ASd1qWwjqJoEa7udriKjy3h351Mf1bng1VxS1urqC3Dn39ZWIEwQIDAQABo4IBjjCCAYowIgYDVR0jAQEABBgwFoAUPT5TqhNWAm+ZpcVsvB7malDBjEQwDwYDVR0TAQH/BAUwAwEBADAPBgNVHQ8BAf8EBQMDAOAAMAwGA1UdIAEBAAQCMAAwgbwGA1UdEQEBAASBsTCBrqA4BgVgTAEDBKAvBC0wNzA4MTk1MTE1MTk0NTMxMDg3MDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDCgHQYFYEwBAwKgFAQSRmVybmFuZG8gQ2FudG8gQWx0oBkGBWBMAQMDoBAEDjk5OTk5MDkwOTEwMjcwoBcGBWBMAQMHoA4EDDAwMDAwMDAwMDAwMIEfZmVybmFuZG8tYWx0QHByb2NlcmdzLnJzLmdvdi5icjAgBgNVHSUBAf8EFjAUBggrBgEFBQcDAgYIKwYBBQUHAwQwUwYDVR0fAQEABEkwRzBFoEOgQYY/aHR0cDovL25mZWNlcnRpZmljYWRvLnNlZmF6LnJzLmdvdi5ici9MQ1IvQUNJbnRlcm1lZGlhcmlhMzguY3JsMA0GCSqGSIb3DQEBBQUAA4IBAQCNPpaZ3Byu3/70nObXE8NiM53j1ddIFXsb+v2ghCVd4ffExv3hYc+/a3lfgV8H/WfQsdSCTzS2cHrd4Aasr/eXfclVDmf2hcWz+R7iysOHuT6B6r+DvV3JcMdJJCDdynR5REa+zViMnVZo1G3KuceQ7/y5X3WFNVq4kwHvonJ9oExsWyw8rTwUK5bsjz0A2yEwXkmkJIngnF41sP31+9jCImiqkXcmsesFhxzX7iurAQAQCZOm7iwMWxQKcAjXCZrgSZWRQy6mU224sX3HTArHahmLJ9Iw+WYAua5qBJsiN6PC7v5tfhdsgGD46DHMnOecxvkkPolDUyBa7d7xwgm\\r\\n</X509Certificate>\\r\\n</X509Data>\\r\\n</KeyInfo>\\r\\n</Signature>\\r\\n</NFe>\",\"courier\":\"carrierOne\",\"trackingNumber\":\"87658\",\"trackingUrl\":\"https://www.tracking.com/url\",\"dispatchedDate\":\"2019-02-08T13:16:13.4617653+00:00\",\"items\":[{\"id\":\"123\",\"price\":2499,\"description\":\"335\",\"quantity\":2}]}"

headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
    'X-VTEX-API-AppKey': "",
    'X-VTEX-API-AppToken': ""
    }

conn.request("post", "/api/oms/pvt/orders//invoice", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

3. The server will send a response with the following parameters:

* `date`: the date and time of the notification.
* `orderId`: the identification of the order.
* `receipt`: the protocol code (generated by the update) that identifies the receipt. 

> **Note**
> 
> Every time this endpoint is called with the same `invoiceNumber`, a new `receipt` code is generated, overriding the previous one. 

Here's an example of a successful response:

```json
{
  "date": "2024-02-07T15:22:56.7612218-02:00",
  "orderId": "123543123",
  "receipt": "38e0e47da2934847b489216d208cfd91"
}
```



## Send an order's tracking number

After shipping the order, you can update the [Partial invoice](https://help.vtex.com/en/tracks/pedidos--2xkTisx4SXOWXQel8Jg8sa/q9GPspTb9cHlMeAZfdEUe) with the order's tracking number.

To add a tracking number to the order:

1. Send a PATCH request to the following endpoint:
```
https://{accountName}.{environment}.com.br/api/oms/pvt/orders/{orderId}/invoice/{invoiceNumber}
```
2. In the request body, include the necessary parameters:

* `trackingNumber`: the code that identifies the order tracking.
* `trackingUrl`: the package tracking URL.
* `dispatchedDate`: the date the package was dispatched.
* `courier`: the name of the carrier delivering the order.

See below an example using Python:

```python
import http.client

conn = http.client.HTTPSConnection("apiexamples.vtexcommercestable.com.br")

payload = "{\"trackingNumber\":\"87658\",\"trackingUrl\":\"https://www.tracking.com/url\",\"courier\":\"carrierOne\",\"dispatchedDate\":\"2022-02-08T13:16:13.4617653+00:00\"}"

headers = {
    'Accept': "application/json",
    'Content-Type': "application/json",
    'X-VTEX-API-AppKey': "",
    'X-VTEX-API-AppToken': ""
    }

conn.request("patch", "/api/oms/pvt/orders//invoice/", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

3. The server will send a response with the following parameters:

* `date`.
* `orderId`.
* `receipt`. 

Here's an example of a successful response:

```json
{
  "date": "2019-02-08T13:16:13.4617653+00:00",
  "orderId": "00-v5195004lux-01",
  "receipt": "527b1ae251264ef1b7a9b597cd8f16b9"
}
```


After sending this request, you can use the [Update order tracking status](https://developers.vtex.com/docs/api-reference/orders-api#put-/api/oms/pvt/orders/-orderId-/invoice/-invoiceNumber-/tracking) API request to add tracking events to the order.