# Authorization Quiz

## Q1 

The following SQL statement over tables R(a,b), S(b,c), and T(a,c) requires certain privileges to execute:

```
   UPDATE R
   SET a = 10
   WHERE b IN (SELECT c FROM S)
   AND NOT EXISTS (SELECT a FROM T WHERE T.a = R.a)
```

Which of the following privileges is not useful for execution of this SQL statement?

- **SELECT ON S(b)**
- UPDATE ON R(a)
- SELECT ON R
- SELECT ON T(a)

## Q2 

Consider a set of users A, B, C, D, E. Suppose user A creates a table T and thus is the owner of T. Now suppose the following set of statements is executed in order:

```
  1. User A: grant update on T to B,C with grant option
  2. User B: grant update on T to D with grant option
  3. User C: grant update on T to D with grant option
  4. User D: grant update on T to E
  5. User A: revoke update on T from C cascade
```

After execution of statement 5, which of the following is true?

- D and E do not have privilege UPDATE ON T, but B does
- B no longer has privilege UPDATE ON T
- **D has privilege UPDATE ON T**
- D no longer has privilege UPDATE ON T

## Q3 

The following SQL statement over tables R(c,d), S(f,g), and T(a,b) requires certain privileges to execute:

```
   UPDATE T
   SET a=1, b=2
   WHERE a <= ALL (SELECT d FROM R)
   OR EXISTS (SELECT f FROM S WHERE f > T.a)
```

Which of the following privileges is not useful for execution of this SQL statement?

- UPDATE ON T(b)
- **INSERT ON T(b)**
- SELECT ON R
- SELECT ON T(a)

## Q4

Consider a set of users U, V, W, X, and Y. Suppose user U creates a table T and thus is the owner of T. Now suppose the following set of statements is executed in order:

```
  1. User U: grant select on T to V,W with grant option
  2. User V: grant select on T to W
  3. User W: grant select on T to X,Y
  4. User U: grant select on T to Y
  5. User U: revoke select on T from V restrict
  6. User U: revoke select on T from W cascade
```

Which of the following statements is true?

- **W has privilege SELECT ON T after statement 5**
- W does not have privilege SELECT ON T after statement 5
- X does not have SELECT ON T privilege after statement 5
- V has privilege SELECT ON T after statement 5