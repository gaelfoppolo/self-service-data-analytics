## Hive Built-in operator

### Predicate operators :

| Operator                | Types               | Description                              |
| ----------------------- | ------------------- | ---------------------------------------- |
| A = B                   | All primitive types | TRUE if expression A is equal to expression B otherwise FALSE |
| A <=> B                 | All primitive types | Returns same result with EQUAL(=) operator for non-null operands, but returns TRUE if both are NULL, FALSE if one of them is NULL (as of version 0.9.0) |
| A == B                  | None!               | Fails because of invalid syntax. SQL uses =, not == |
| A <> B                  | All primitive types | NULL if A or B is NULL, TRUE if expression A is NOT equal to expression B otherwise FALSE |
| A != B                  | All primitive types | a synonym for the <> operator            |
| A < B                   | All primitive types | NULL if A or B is NULL, TRUE if expression A is less than expression B otherwise FALSE |
| A <= B                  | All primitive types | NULL if A or B is NULL, TRUE if expression A is less than or equal to expression B otherwise FALSE |
| A > B                   | All primitive types | NULL if A or B is NULL, TRUE if expression A is greater than expression B otherwise FALSE |
| A >= B                  | All primitive types | NULL if A or B is NULL, TRUE if expression A is greater than or equal to expression B otherwise FALSE |
| A [NOT] BETWEEN B AND C | All primitive types | NULL if A, B or C is NULL, TRUE if A is greater than or equal to B AND A less than or equal to C otherwise FALSE. This can be inverted by using the NOT keyword. (as of version 0.9.0) |
| A IS NULL               | all types           | TRUE if expression A evaluates to NULL otherwise FALSE |
| A IS NOT NULL           | All types           | FALSE if expression A evaluates to NULL otherwise TRUE |
| A [NOT] LIKE B          | strings             | NULL if A or B is NULL, TRUE if string A matches the SQL simple regular expression B, otherwise FALSE. The comparison is made character by character. The _ character in B matches any character in A (similar to . in POSIX regular expressions) while the % character in B matches an arbitrary number of characters in A (similar to .* in POSIX regular expressions) e.g. 'foobar' like 'foo' evaluates to FALSE where as 'foobar' like 'foo_ _ _' evaluates to TRUE and so does 'foobar' like 'foo%' |
| A [NOT] RLIKE B         | strings             | NULL if A or B is NULL, TRUE if any (possibly empty) substring of A matches the Java regular expression B, otherwise FALSE. E.g. 'foobar' RLIKE 'foo' evaluates to FALSE whereas 'foobar' RLIKE '^f.*r$' evaluates to TRUE. |
| A REGEXP B              | strings             | Same as RLIKE                            |

### Arithmetic Operators :

| Operator | Types   | Description                              |
| -------- | ------- | ---------------------------------------- |
| A + B    | Numbers | Gives the result of adding A and B. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. e.g. since every integer is a float, therefore float is a containing type of integer so the + operator on a float and an int will result in a float. |
| A - B    | Numbers | Gives the result of subtracting B from A. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. |
| A * B    | Numbers | Gives the result of multiplying A and B. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. Note that if the multiplication causing overflow, you will have to cast one of the operators to a type higher in the type hierarchy. |
| A / B    | Numbers | Gives the result of dividing B from A. The result is a double type. |
| A % B    | Numbers | Gives the reminder resulting from dividing A by B. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. |
| A & B    | Numbers | Gives the result of bitwise AND of A and B. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. |
| A \| B   | Numbers | Gives the result of bitwise OR of A and B. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. |
| A ^ B    | Numbers | Gives the result of bitwise XOR of A and B. The type of the result is the same as the common parent(in the type hierarchy) of the types of the operands. |
| ~A       | Numbers | Gives the result of bitwise NOT of A. The type of the result is the same as the type of A. |

### Logical Operators :

| Operator                   | Types   | Description                              |
| -------------------------- | ------- | ---------------------------------------- |
| A AND B                    | boolean | TRUE if both A and B are TRUE, otherwise FALSE. NULL if A or B is NULL |
| A && B                     | boolean | Same as A AND B                          |
| A OR B                     | boolean | TRUE if either A or B or both are TRUE; FALSE OR NULL is NULL; otherwise FALSE |
| A \|\| B                   | boolean | Same as A OR B                           |
| NOT A                      | boolean | TRUE if A is FALSE or NULL if A is NULL. Otherwise FALSE. |
| ! A                        | boolean | Same as NOT A                            |
| A IN (val1, val2, ...)     | boolean | TRUE if A is equal to any of the values  |
| A NOT IN (val1, val2, ...) | boolean | TRUE if A is not equal to any of the values |

#### Operators for complex types :

| Operator | Types                         | Description                              |
| -------- | ----------------------------- | ---------------------------------------- |
| A[n]     | A is an Array and n is an int | Returns the nth element in the array A. The first element has index 0 e.g. if A is an array comprising of ['foo', 'bar'] then A[0] returns 'foo' and A[1] returns 'bar' |
| M[key]   | M is a Mapand key has type K  | Returns the value corresponding to the key in the map e.g. if M is a map comprising of {'f' -> 'foo', 'b' -> 'bar', 'all' -> 'foobar'} then M['all'] returns 'foobar' |
| S.x      | S is a struct                 | Returns the x field of S. e.g for struct foobar {int foo, int bar} foobar.foo returns the integer stored in the foo field of the struct. |