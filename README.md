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
    
    | Expression   | Description                                          |
    | ------------ | ---------------------------------------------------- |
    | node_name    | select all node with the name is "*node_name*"       |
    | /            | select from root                                     |
    | //           | select nodes in current context in depth to top down |
    | .            | select current node                                  |
    | ..           | selects the parent of the current node               |
    | @            | select attributes                                    |
    | book[1]      | select the first book, in depth to top down          |
    | book[last()] | select the last book, in depth to top down           |
    |              |                                                      |
    |              |                                                      |
    |              |                                                      |
    |              |                                                      |
    
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
            </section>
        </div> 
        <div id="b">
            <div id="b1"></div>
            <div id="b2"></div>
        </div>
    </body>
    </html>               
    ```
    
    | Expression    | Description                                                                                                                                                             |
    | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | div           | everything include element, attribute, atomic value with name is "*div*"                                                                                                |
    | /html         | select from /html                                                                                                                                                       |
    | //div         | select all <div> with order id=`a` ->`a1`->`a2`->`b`->`b1`->`b2`                                                                                                        |
    | //div/a       | select all <a> with parent <div>                                                                                                                                        |
    | //div//a      | select all <a> with ascentors <div>                                                                                                                                     |
    | //a/@tabindex | select all <a> with attribute `tabindex`                                                                                                                                |
    | /.            | = /html doc                                                                                                                                                             |
    | //div[1]      | the first <div> in any element, id="a" -> "a1" -> "b1"                                                                                                                  |
    | //div[2]      | - check <div> ancestor that contain the number of children <div> tags >= 2<br/>- select the 2nd children <div> tag in that <div> tag<br/>- Ex: <div> id=`a2`->`b`->`b2` |
    |               |                                                                                                                                                                         |
    |               |                                                                                                                                                                         |

17. XML DTD
    
    - ```xml
      <!DOCTYPE dtd_name[
        <!ELEMENT element-name (element-content type)>  
      ]>
      ```
    
    - 

18. 
