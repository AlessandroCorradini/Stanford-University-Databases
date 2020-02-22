# Relational Algebra Exercises


In this assignment you are to write relational algebra queries over a small database, executed using our RA Workbench. Behind the scenes, the RA workbench translates relational algebra expressions into SQL queries over the database stored in SQLite. Since relational algebra symbols aren't readily available on most keyboards, RA uses a special syntax described in our RA Relational Algebra Syntax guide.

We've created a small sample database to use for this assignment. It contains four relations:

    Person(name, age, gender)       // name is a key
    Frequents(name, pizzeria)       // [name,pizzeria] is a key
    Eats(name, pizza)               // [name,pizza] is a key
    Serves(pizzeria, pizza, price)  // [pizzeria,pizza] is a key

View the database. (You can also download the schema and data.)

Instructions: You are to write relational algebra expressions over the pizza database. We strongly suggest that you work the queries out on paper first, using conventional relational algebra symbols. When you click "Check Answer" our back-end runs your query against the sample database. It displays the result and compares your answer against the correct one. When you're satisfied with your solution for a given problem, click the "Submit" button to check your answer.

Please Note: You are to translate the English into an expression that computes the desired result over all possible databases. All we actually check is that your query gets the right answer on the small sample database. Thus, even if your solution is marked as correct, it is possible that your query does not correctly reflect the problem at hand. (For example, if we ask for a complex condition that requires accessing all of the tables, but over our small data set in the end the condition is satisfied only by Amy, then the query "\project_{name} (\select_{name='Amy'} Person)" will be marked correct even though it doesn't reflect the actual question.) Circumventing the system in this fashion will get you a high score on the exercises, but it won't help you learn relational algebra. On the other hand, an incorrect attempt at a general solution is unlikely to produce the right answer, so you shouldn't be led astray by our checking system.


## Q1 

Find all pizzas eaten by at least one female over the age of 20.

```
\project_{pizza} (
  (
    (\project_{name} \select_{gender='female'} Person)
      \intersect
    (\project_{name} \select_{age>20} Person)
  \join Eats)
)
```

## Q2

Find the names of all females who eat at least one pizza served by Straw Hat. (Note: The pizza need not be eaten at Straw Hat.)

```
\project_{name} (
  \select_{gender='female' AND pizzeria='Straw Hat'} (
    Person \join Eats \join Serves
  )
);
```

## Q3

Find all pizzerias that serve at least one pizza for less than $10 that either Amy or Fay (or both) eat.

```
\project_{pizzeria} (
    \select_{price<10} Serves
    \join
    \select_{name='Amy' OR name='Fay'} Eats
);
```

## Q4 

Find all pizzerias that serve at least one pizza for less than $10 that both Amy and Fay eat.

```
\project_{pizzeria} (
    \select_{price<10} Serves
    \join
    (
        (\project_{pizza} \select_{name='Amy'} Eats)
        \intersect  
        (\project_{pizza} \select_{name='Fay'} Eats)
    )
);
```

## Q5 

Find the names of all people who eat at least one pizza served by Dominos but who do not frequent Dominos.

```
\project_{name} (
  Eats
  \join
  \project_{pizza} \select_{pizzeria='Dominos'} Serves
)
\diff (\project_{name} \select_{pizzeria='Dominos'} Frequents)
```

## Q6 

Find all pizzas that are eaten only by people younger than 24, or that cost less than $10 everywhere they're served.

```
\project_{pizza} Eats \diff (\project_{pizza}
(\select_{age>=24} Person \join Eats)
\intersect
\project_{pizza} (\select_{price>=10} Serves))
```

## Q7 

Find the age of the oldest person (or people) who eat mushroom pizza.

```
\rename_{age2}(\project_{age}(\project_{name}(\select_{pizza = 'mushroom'}Eats) \join Person))
\diff
\project_{age2}(
\rename_{age2}(\project_{age}(\project_{name}(\select_{pizza = 'mushroom'}Eats) \join Person)) 
\join_{age2<age1} 
\rename_{age1}(\project_{age}(\project_{name}(\select_{pizza = 'mushroom'}Eats) \join Person))
)
```

## Q8 

Find all pizzerias that serve only pizzas eaten by people over 30.

```
\project_{pizzeria} (Serves \join Person)
\diff
\project_{pizzeria} (
  (Serves \join Person)
  \join
  (
    (\project_{pizza} Serves)
    \diff
    (\project_{pizza}((\select_{age>'30'} Person)
      \join Eats)
    )
  )  
)
```

## Q9

Find all pizzerias that serve every pizza eaten by people over 30.

```
\project_{pizzeria}(Serves)
\diff
\project_{pizzeria}(
    (\project_{pizzeria}(Serves)
    \cross
    \project_{pizza}(\project_{name}(\select_{age>30}(Person))\join Eats))
    \diff
    \project_{pizzeria,pizza}(Serves)
)
```