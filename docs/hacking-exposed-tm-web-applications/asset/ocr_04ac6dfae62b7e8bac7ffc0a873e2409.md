# 248 Hacking Exposed Web Applications

```
<?xml version="1.0"?>
<definitions name="StockTrader">
targetNamespace="http://stocktrader.edu/stockquote.wsdl"
  xmlns:ns="http://stocktrader.edu/stockquote.wsdl"
  xmlns:xsd="http://stocktrader.edu/stockquote.xsd"
  xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
  xmlns="http://schemas.xmlsoap.org/wsdl/"

  <types>
    <schema targetNamespace="http://stocktrader.edu/stockquote.xsd"
    xmlns="http://www.w3.org/2000/XMLSchema">
      <element name="GetQuote">
        <complexType>
          <all>
            <element name="tickersSymbol" type="string"/>
          </all>
        </complexType>
      </element>
      <element name="Price">
        <complexType>
          <all>
            <element name="price" type="float"/>
          </all>
        </complexType>
      </element>
    </schema>
  </types>

<message name="GetQuoteInput">
  <part name="body" element="xsd:QuoteRequest"/>
</message>

<message name="GetQuoteOutput">
  <part name="body" element="xsd:StockPrice"/>
</message>

<portType name="StockPortType">
  <operation name="GetQuote">
    <input message="tns:GetQuoteInput" />
    <output message="tns:GetQuoteOutput" />
  </operation>
</portType>
```