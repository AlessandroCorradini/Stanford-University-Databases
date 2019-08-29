# XML World-Countries XSLT Exercises

## Q1 

Return all countries with population between 9 and 10 million. Retain the structure of country elements from the original data. 

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

Note: You do not need to use "doc(..)" in your solution. It will be executed on countries.xml. 

**Answer**

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="country[@population &gt; 9000000][@population &lt; 10000000]">
    <xsl:copy-of select="." />
  </xsl:template>
  <xsl:template match="text()" />
</xsl:stylesheet>
```

## Q2

Create a table using HTML constructs that lists all countries that have more than 3 languages. Each row should contain the country name in bold, population, area, and number of languages. Sort the rows in descending order of number of languages. No header is needed for the table, but use ```<table border="1">``` to make it format nicely, should you choose to check your result in a browser. (Hint: You may find the data-type and order attributes of ```<xsl:sort>``` to be useful.) 

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

Reminder: To return the value of an attribute attr, you must use data(@attr), although just @attr may be used in comparisons. You will need to remember this for the next question as well. 
Note: You do not need to use "doc(..)" in your solution. It will be executed on countries.xml. 

**Answer**

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="countries">
    <html>
      <table border="1">
        <xsl:for-each select="country[count(language) &gt; 3]">
          <xsl:sort select="count(language)" order="descending" />
          <tr>
            <td><b><xsl:value-of select="@name" /></b></td>
            <td><xsl:value-of select="@population" /></td>
            <td><xsl:value-of select="@area" /></td>
            <td><xsl:value-of select="count(language)" /></td>
          </tr>
        </xsl:for-each>
      </table>
```

## Q3 

Create an alternate version of the countries database: for each country, include its name and population as sublements, and the number of languages and number of cities as attributes (called "languages" and "cities" respectively). 

```
Your solution should fill in the following stylesheet: 
    <?xml version="1.0" encoding="ISO-8859-1"?>
    <xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
        <xsl:template match=...>
            ... template body ...
        </xsl:template>
        ... more templates as needed ...
    </xsl:stylesheet>
```

Note: You do not need to use "doc(..)" in your solution. It will be executed on countries.xml. 

**Answer**

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:template match="countries">
    <countries>
      <xsl:for-each select="country">
        <country languages="{ count(language) }" cities="{ count(city) }">
          <name><xsl:value-of select="@name" /></name>
          <population><xsl:value-of select="@population" /></population>
        </country>
      </xsl:for-each>      
    </countries>
  </xsl:template>
</xsl:stylesheet>
```
