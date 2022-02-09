# XML

1. Prolog: don't have a closing tag, so it isn't a part of XML doc
   
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   ```

2. Must have a **Closing Tag**

3. Tags are **Case Sensitive**

4. Must be properly **Nested**
   
   ```xml
   <b><i>abc</b></i>    <!--wrong: it is HTML-->
   <b><i>abc</i></b>    <!--true-->
   ```

5. Attribute values must always be **Quoted**
   
   ```xml
   <note date="12/11/2222">
   </note>
   ```

6. Replace special characters with **Entity reference**
   
   `&lt;` is `<` is less than
   
   `&gt;` is `>` is greater than
   
   `&amp;` is `&` is ampersand
   
   `&apos;` is `'` is apostrophe
   
   `&quot;` is `"` is quotation mark

7. Comments: `<!-- comment -->`

8. Don't truncate multiple white-spaces: `Hello    world`

9. XML Element: contain text, attribute, others element
   
   ```xml
   <bookstore>
     <book category="children">
       <title>Harry Potter</title>
       <author>J K. Rowling</author>
       <year>2005</year>
       <price>29.99</price>
     </book>
   </bookstore>
   ```
   
   - Text content: <title>, <author>, ... because contain text
   
   - Element content: <book>, ... because contain element
     
     ```xml
     <element></element>    <!--empty element-->
     <element/>             <!--self-closing element-->
     ```
     
     Rules for element names: 
     
     - Case-sensitive
     
     - Must start a letter or underscore, **except** xml, Xml, XML
     
     - Can contain letter, digit, hyphen `-`, underscore
     
     - Not contain spaces
     
     - Short and simple <bool_title> not <the_book_title>
     
     - Avoid `-`, `.`, `:`
     
     - Naming style: lower, upper, underscore, pascal, camel

10. XML Attribute: be quoted, single `'` or double quotes `"`
    
    - Using **Entity character** replace special character
    
    - Attribute and Element
      
      ```xml
      <note date="2018-01-10">
        <to>A</to>
        <from>B</from>
      </note>
      ```
      
      The sample
      
      ```xml
      <note>
        <date>2018-01-10</date>
        <to>Anna</to>
        <from>Smith</from>
      </note>
      ```
      
      The sample: => so good 
      
      ```xml
      <note>
        <date>
          <year>2008</year>
          <month>01</month>
          <day>10</day>
        </date>
        <to>Tove</to>
        <from>Jani</from>
      </note>
      ```
    
    - Using ID attribute for element
      
      ```xml
      <note id="501">
      ```

11. XML namespace
    
    - Solving conflict name by prefix, ex `<table>` in HTML and XML
    
    - Namespace for prefix must be **defined** by an **xmlns** attribute
    
    - Syntax: `xmlns:prefix="URI"`
      
      ```xml
      <h:table xmlns:h="http://...">
          <h:tr>
          </h:tr>
      </h:table>
      ```
      
      Namespaces can also be declared in the XML root element
      
      ```xml
      <root xmlns:h="http://www.w3.org/TR/html4/">
      
      <h:table>
        <h:tr>
          <h:td>Apples</h:td>
          <h:td>Bananas</h:td>
        </h:tr>
      </h:table>
      
      </root>
      ```
    
    - Default namespace
      
      > xmlns="namespaceURI"

12. XSLT
    
    - XSLT is a language that can be used to transform XML documents into other formats
      
      ```xml
      <xsl:stylesheet version="1.0" 
      xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
      
      <xsl:template match="/">
      ```

13. XMLHttpRequest
    
    ```javascript
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
           // Typical action to be performed when the document is ready:
           document.getElementById("demo").innerHTML = xhttp.responseText;
        }
    };
    xhttp.open("GET", "filename", true);
    xhttp.send();
    ```

14. XML Parser 
    
    - Parse String to XML
    
    ```html
    <html>
        <body>
            <p id="demo"></p>
    
            <script>
            var parser, xmlDoc;
            var text = "<bookstore><book>" +
                        "<title>Everyday Italian</title>" +
                        "<author>Giada De Laurentiis</author>" +
                        "<year>2005</year>" +
                        "</book></bookstore>";
                parser = new DOMParser();
                xmlDoc = parser.parseFromString(text,"text/xml");
    
                document.getElementById("demo").innerHTML =
                xmlDoc.getElementsByTagName("year")[0]
                      .childNodes[0]
                      .nodeValue;
            </script>
        </body>
    </html>
    ```
    
    - Parse XML to String: request file [cd_catalog.xml](https://www.w3schools.com/xml/cd_catalog.xml)
    
    ```js
    var xmlDoc = xmlhttp.responseXML;
    var txt = "";
    var x = xmlDoc.getElementsByTagName("ARTIST");
    for (i = 0; i < x.length; i++) {
        txt += x[i].childNodes[0].nodeValue + "<br>";
    }
    document.getElementById("demo").innerHTML = txt;
    ```

15. XML DOM ([Document Object Model](https://www.w3schools.com/xml/dom_intro.asp))

16. XPath
    
    - There are 7 kinds of node: element, attribute, text, namespace, processing-instruction, comment, and document nodes
      
      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <bookstore>
        <book>
          <title lang="en">Harry Potter</title>
          <author>J K. Rowling</author>
          <year>2005</year>
          <price>29.99</price>
        </book>
      </bookstore>
      ```
      
      - `<bookstore>` : root element node
      
      - `<year>2005</year>` : element node
      
      - `lang="en"` : attribute node
    
    - Atomic values: are nodes with no children or parent
      
      > J K. Rowling
      > 
      > "en"
    
    - Items: are atomic values or nodes
    
    - Relationship of nodes: 
      
      - Parent: each element and attribute has one parent
        
        - `book` is parent of `title`, `author`
        
        - `title` is parent of `lang`
      
      - Children: element may have zero, one or more children
        
        - `title`, `author` are children of `book`
      
      - Siblings: the same parent
        
        - `title` and `author` is siblings
      
      - Ancestors: parent, parent's parent, etc
        
        - `bookstore`, `book` are ancestors of `title` 
      
      - Descendants: children, children's children, etc
        
        - `book`, `title` are descendants of `bookstore`
    
    . Syntax:
    
    | Expression                 | Description                                                                      |
    | -------------------------- | -------------------------------------------------------------------------------- |
    | node_name                  | select all node with the name is "*node_name*"                                   |
    | /                          | select from root                                                                 |
    | //                         | select nodes in current context in depth to top down                             |
    | .                          | select current node                                                              |
    | ..                         | selects the parent of the current node                                           |
    | @                          | select attributes                                                                |
    | book[1]                    | select the first book, in depth to top down                                      |
    | book[last()]               | select the last book, in depth to top down                                       |
    | book[position()<3]         | select the 1st and 2nd book                                                      |
    | title[@lang]               | select all title that have `lang` attribute                                      |
    | title[@lang='en']          | select all title that have `lang="en"` attribute                                 |
    | book[price>35.00]          | select all book that price > 35.00                                               |
    | *                          | match any element node                                                           |
    | @*                         | match any attribute node                                                         |
    | node()                     | match any node                                                                   |
    | //book/title\|//book/price | selects all the title AND price elements of all book elements                    |
    | //title \| //price         | Selects all the title AND price elements in the document                         |
    | //book/title \| //price    | Selects all the <title> of the <book> AND all the price elements in the document |
    
      Example:
    
    ```html
    <html>
    <head>
        <meta charset="utf-8">
    </head>
    
    <body lang="en-us" dir="ltr">
        <div id="a">
            <a class="abc1" tabindex="-1">Skip to main content</a>
            <div hidden="" id="a1">
                <a class="abc2"></a>
                <a class="abc3"></a>
            </div>
            <div id="a2"></div>
            <section id="sec1">
                <a class="abc3"></a>
                <div id="secdiv1"></div>
                <div id="secdiv2"></div>
            </section>
        </div> 
        <div id="b">
            <div id="b1"></div>
            <div id="b2"></div>
        </div>
    </body>
    </html>               
    ```
    
    | Expression          | Description                                                                                                                                                                      |
    | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | div                 | everything include element, attribute, atomic value with name is "*div*"                                                                                                         |
    | /html               | select from /html                                                                                                                                                                |
    | //div               | select all <div> with order id=`a` ->`a1`->`a2`->...->`b1`->`b2`                                                                                                                 |
    | //div/a             | select all <a> with parent <div>                                                                                                                                                 |
    | //div//a            | select all <a> with ascentors <div>                                                                                                                                              |
    | //a/@tabindex       | select all element from <a> in depth with attribute `tabindex`                                                                                                                   |
    | /.                  | = /html doc                                                                                                                                                                      |
    | //div[1]            | the first <div> in any element, id=`a` -> `a1` -> "b1"                                                                                                                           |
    | //div[2]            | - check any elements that contain the number of children <div> tags >= 2<br/>- select the 2nd children <div> tag in that <div> tag<br/>- Ex: <div> id=`a2`->`secdiv2`->`b`->`b2` |
    | //div[position()<2] | - select the 1st <div> tag<br/>- The same //div[1]                                                                                                                               |
    | //a[@tabindex]      | select all <a> with attribute `tabindex`                                                                                                                                         |
    | /*                  | = /html                                                                                                                                                                          |
    | //*                 | select all element                                                                                                                                                               |
    | //a[@*]             | select all <a> which have at least 1 attribute                                                                                                                                   |

17. XML DTD
    
    **Internal DTD**:
    
    - ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <!DOCTYPE dtd_name[
          <!ELEMENT element-name (content_model type)>
          <!ALLLIST element-name attr-name attr-type constraint>
          <!ENTITY entity-name "entity-value">
      ]>
      ```
    
    **External DTD**:
    
    - Reference in file xml:
      
      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <!DOCTYPE root_name SYSTEM "file/uri">
      
      <!--Example-->
      <!DOCTYPE bookstore SYSTEM "book.dtd">
      ```
      
      - root_name: the name of root element in xml file
      
      - SYSTEM: indicate the DTD file is private
      
      - file/uri: location of file dtd
    
    - In file dtd:
      
      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <!ELEMENT element-name (content_model type)>
      <!ATTLIST element-name attr-name attr-type default-value>
      <!ENTITY entity-name "entity-value">
      ```
    
    - Declare element:
      
      ```xml
      <!ELEMENT element-name [content_model]>
      <!ELEMENT element-name (element-child-1, element-child-2, ...)>
      <!--nested/mixed element-->
      <!ELEMENT element-name (#PCDATA | element-child-1 | ...)*>
      ```
      
      - content_model: 
        
        - `(#PCDATA)`: content of element contains characters, string
        
        - `EMPTY`:  empty tag
        
        - `ANY`: content of element contains characters or element-child 
      
      - element-child: append characters
        
        - `?`:  appear 0 or 1 time
        
        - `+`: appear at least 1 time
        
        - `*`: appear at least 0 time 
        
        - nothing: default appear 1
        
        - element-child-1, element-child-2: order of appearance 1, 2
        
        - element-child-1 | element-child-2:  appear child-1 or child-2
        
        - `()`: group
        
        - `(#PCDATA | child-1 | child-2 | ...)*`: mixed content
      
      ```xml
      <!--Example-->
      <!ELEMENT book (name+, price*)>
      <!ELEMENT name (#PCDATA)>
      <!ELEMENT price (#PCDATA)>
      <!--specially mix content-->
      <!ELEMENT book (#PCDATA | name)*>
      <!--result-->
      <book>this is mixed content
          <name>ABC</name>
      <book>
      ```
    
    - Define attribute:
      
      ```xml
      <!ATTLIST element-name attr-name attr-type constraint>
      <!ATTLIST element-name attr-name-1 attr-type-1 contraint-1
                             attr-name-2 attr-type-2 contraint-2>
      ```
      
      - attr-type:
        
        | attribute-type   | description                                                     |
        | ---------------- | --------------------------------------------------------------- |
        | CDATA            | character                                                       |
        | NMTOKEN          | value is valid like a element tag, may start with a **digit**   |
        | NMTOKENS         | a set of one or more NMTOKEN, separated by **white-space**      |
        | ID               | unique id                                                       |
        | IDREF            | reference other id                                              |
        | IDREFS           | a set of one or more IDREF, separated by **white-space**        |
        | ENTITY           | the name of entity                                              |
        | ENTITIES         | a set of one or more ENTITIE, separated by **white-space**      |
        | NOTATION         | reference to a file, a directory or a path, MIME or binary type |
        | (eval\|eval\|..) | enumeration                                                     |
      
      - constraint: 
        
        | constraint     | description                                |
        | -------------- | ------------------------------------------ |
        | #REQUIRED      | require attribute, may empty               |
        | #IMPLIED       | can appear or not                          |
        | #FIXED “value” | must assign = "value"                      |
        | "value"        | default "value" if attribute cannot appear |
      
      ```xml
      <!--Example-->
      <!ELEMENT person EMPTY>
      <!ATTLIST person name CDATA #REQUIRED>
      <!ATTLIST person gender (M|F) "M"
                       age NMTOKEN #IMPLIED> 
      ```
    
    - Define entity:
      
      All entity must be defined before using
      
      - Only use in DTD file to declare: **parameter entity**
      
      - Reference to XML: **general entity**
      
      Divided 5 type:
      
      | Type                               | Description                                                                                                                                                                                                                                                                                                                                                                |
      | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
      | Internal Parsed General Entity     | declare in XML or DTD file, to reference value to XML<br/>Syntax: `<!ENTITY entity_name "value">`<br/>in XML: `&entity_name;`                                                                                                                                                                                                                                              |
      | External Parsed General Entities   | read from other DTD<br/>Syntax: `<!ENTITY entity_name SYSTEM\|PUBLIC "uri">`<br/>in XML: `&entity_name;`                                                                                                                                                                                                                                                                   |
      | External Unparsed General Entities | reference MIME or binary data type<br/>Syntax: `<!ENTITY entity_name SYSTEM\|PUBLIC "uri" NDATA reference_name>`                                                                                                                                                                                                                                                           |
      | Internal Parsed Parameter Entities | - declare a **string**<br/>- use for **attribute type or content model**<br/>- reuse in DTD file<br/>Syntax: `<!Entity % entity_name "value">`<br/>in DTD: `%entity_name;`<br/>for attribute: <br/><!Entity % entity_name "<br/>          attr_name_1 attr_type constraint <br/>          attr_name_2 attr_type constraint"<br/>><br/>`<!ATTLIST attr_name %entity_name;>` |
      | External Parsed Parameter Entities | reference from other DTD<br/>Syntax: `<!Entity % entity_name SYSTEM\|PUBLIC "uri">`<br/>in DTD: `%entity_name;`                                                                                                                                                                                                                                                            |
      
      Example:
      
      ```xml
      <!ENTITY abc "abc">
      <book id="&abc;">
      ```
      
      <!ENTITY % common_attr 
          'id     ID     #REQUIRED
          account CDATA  #IMPLIED'
      >
      
      <!ATTLIST item %common_attr;>

```xml
  <!ENTITY % old SYSTEM "combine.dtd">
  %old;
  ```
```

18. XML Schema
    
    XML Schema Language is XML Schema Definition (XSD)
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                targetNamespace="http://xml.netbeans.org/schema/mail"
                xmlns="http://xml.netbeans.org/schema/mail"
                elementFormDefault="qualified">
        <xsd:element/>
    </xsd:schema>
    ```
    
    - `<[prefix]:schema xmlns:[prefix]=(http://www.w3.org/2001/XMLSchema)">`: element  root `schema` for XML Schema
    
    - Elements and data type are validated at [(http://www.w3.org/2001/XMLSchema)](http://www.w3.org/2001/XMLSchema)
    
    - All element and data type must start with `[prefix]` in `xmlns:[prefix]` (xsd)
    
    - `targetNamespace="uri"`: define uri namespace for reusing in other doc. It is similar defining package in class in java. **[Optional]**
    
    - ``xmlns="uri"`: default namespace. **[Optional]**
    
    - `elementFormDefault="qualified"`: apply XML, must define **prefix** before element tag. Example `<xsd:book name="abc"/>`
    
    In XML file:
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <mail xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="http://xml.netbeans.org/schema/mail"
        xsi:schemaLocation="http://xml.netbeans.org/schema/mail mail.xsd">
        <to>abc</to>
    </mail>
    
    <!--Example: other-->
    <mail xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:noNamespaceSchemaLocation="mail.xsd">
    </mail>
    ```
    
    - `xsi:schemaLocation="namespace_uri instance"`: define namespace of the validated schema, specified instance. Here is **mail.xsd**. Include name of namespace and location of schema file (mail.xsd)
    
    ###### Declare in Schema:
    
    - Element: 
      
      ```xml
      <xs:element name="element_name"
                  type="data_type"
                  minOccurs="minimum_appear"
                  maxOccurs="maximum_appear"
                  default|fixed="value">
      </xs:element>
      ```
      
      - | minOccurs   | maxOccurs   | number of times element can occur |
        | ----------- | ----------- | --------------------------------- |
        | 0           | 1           | 0 or 1                            |
        | 3           | 3           | 3                                 |
        | 0           | unbounded   | 0 -> infinity                     |
        | 1           | unbounded   | 1 -> infinity                     |
        | n           | unbounded   | at least n times                  |
        | > maxOccurs | ...         | Error                             |
        | ...         | < minOccurs | Error                             |
      
      [![image alt text](http://img.tobebetter.info/khanhkt/XML/XML_Schema_files/image003.jpg)]
      
      Declare element by ways:
      
      - **Simple type**: only contains text, no attribute
        
        - User-Derived: avaiable in schema
          
          - atomic: int, long, double, ...
          
          - non-atomic: contains more 1 value such as Array, Collection
        
        - Build-in:
          
          - Primitive: basic data type: int, long, float, double, ...
          
          - Derived: extension or restriction from primitive
      
      - **Complex type**: 
        
        - Empty: **no body**, may be have **attribute**
        
        - Simple Content: **body** is text, **type** is extension or restriction from the avaiable data type
        
        - Complex Content: **body** can be text, element, ... and contains **attribute**
      
      Detail of Type:
      
      - Simple Type:
        
        ```xml
        <xsd:element name="element_name" type="data_type"/>
        <xsd:element ref="reference_element_name"/>
        
        <xsd:element name="element_name" 
                     type="data_type" 
                     default|fixed="value"/>
        <!--nillable: allow value null or not-->
        <xsd:element name="element_name" 
                     type="data_type" 
                     nillable="true|false"/>
        ```

19. 

20. 

21. 
