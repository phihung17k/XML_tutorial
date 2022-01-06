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

13. 

14. 





 
