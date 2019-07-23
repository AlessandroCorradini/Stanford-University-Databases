# UML to Relations

## Q1

Suppose we had 0..2 on the right-hand side, so students can apply to up to 2 colleges? Is there still a way to "fold in" the association relation in this case, or must we have a separate Applied relation?

- **Yes there is a way**
- No, if it's not 0..1 or 1..1 then Applied is required

## Q2

Consider a superclass S with some number of subclasses. Suppose the subclassing relationship is incomplete (partial) and overlapping. Let size1, size2, and size3 denote the total number of tuples using translation schemes 1, 2, and 3. How are these three values guaranteed to be related for any data?

- size1 < size2 < size3
- size1 <= size2 <= size3
- size3 < size2 < size1
- **size3 <= size2 <= size1** 