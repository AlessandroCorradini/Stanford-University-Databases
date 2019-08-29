# XML World-Countries XPath and XQuery Exercises

## Q1 

Return the area of Mongolia. 

Note: Your solution will need to reference doc("countries.xml")to access the data. 

Reminder: To return the value of an attribute attr, you must use data(@attr), although just @attr may be used in comparisons. You will need to remember this for some later questions as well. 

**Answer**

```
doc("countries.xml")//country[@name = "Mongolia"]/data(@area)
```

## Q2

Return the names of all cities that have the same name as the country in which they are located. 

**Answer**

```
for $b in doc("countries.xml")//country
for $c in $b/city
where $c/name = $b/@name
return $c/name
```

## Q3 

Return the average population of Russian-speaking countries. 

**Answer**

```
avg(doc("countries.xml")//country[language="Russian"]/data(@population))
```

## Q4 

Return the names of all countries that have at least three cities with population greater than 3 million. 

Note: Your solution will need to reference doc("countries.xml") to access the data. 

**Answer**

```
doc("countries.xml")//country[count(city[population>3000000])>=3]/data(@name)
```

## Q5 

Create a list of French-speaking and German-speaking countries. The result should take the form:

```
<result>
  <French>
    <country>country-name</country>
    <country>country-name</country>
    ...
  </French>
  <German>
    <country>country-name</country>
    <country>country-name</country>
    ...
  </German>
</result>
```

**Answer**

```
<result>
  <French>
    {for $b in doc("countries.xml")//country
    where $b/language="French"
    return <country>{ $b/data(@name) }</country> }
  </French>
  <German>
    {for $b in doc("countries.xml")//country
    where $b/language="German"
    return <country>{ $b/data(@name) }</country> }
  </German>
</result>
```

## Q6 

Return the countries with the highest and lowest population densities. Note that because the "/" operator has its own meaning in XPath and XQuery, the division operator is infix "div". To compute population density use "(@population div @area)". You can assume density values are unique. The result should take the form:

```
<result>
  <highest density="value">country-name</highest>
  <lowest density="value">country-name</lowest>
</result> 
```

**Answer**

```
<result>
  <highest density="{max(doc("countries.xml")//country/(@population div @area))}">
    { for $b in doc("countries.xml")//country
      where data($b/(@population div @area)) = max(doc("countries.xml")//country/(@population div @area))
      return data($b/@name)
    }
  </highest>
  <lowest density="{min(doc("countries.xml")//country/(@population div @area))}">
      { for $b in doc("countries.xml")//country
        where data($b/(@population div @area)) = min(doc("countries.xml")//country/(@population div @area))
        return data($b/@name)
      }
  </lowest>
</result>
```