# XML Course-Catalog XSLT Exercises

## Q1

Return a list of department titles. 

Your solution should fill in the following stylesheet: 

```
    <?xml version="1.0" encoding="ISO-8859-1"?>
    <xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:template match=...>
            ... template body ...
        </xsl:template>
        ... more templates as needed ...
    </xsl:stylesheet>
```

Note: You do not need to use "doc(..)" in your solution. It will be executed on courses.xml. 

**Answer**

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="Department">
       <Title><xsl:value-of select="Title" /></Title>
    </xsl:template>
</xsl:stylesheet>
```

## Q2

Return a list of department elements with no attributes and two subelements each: the department title and the entire Chair subelement structure. 

Your solution should fill in the following stylesheet: 

```
    <?xml version="1.0" encoding="ISO-8859-1"?>
    <xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:template match=...>
            ... template body ...
        </xsl:template>
        ... more templates as needed ...
    </xsl:stylesheet>
```

Note: You do not need to use "doc(..)" in your solution. It will be executed on courses.xml. 

**Answer**

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="Department">
    <Department>   
      <Title><xsl:value-of select="Title" /></Title>
      <xsl:copy-of select="Chair" />
    </Department>
  </xsl:template>
</xsl:stylesheet>
```
