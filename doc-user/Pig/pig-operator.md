## Pig Latin Built-in operators

### Arithmetic operators

| Operator                                 | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| +                                        | **Addition** − Adds values on either side of the operator |
| −                                        | **Subtraction** − Subtracts right hand operand from left hand operand |
| *                                        | **Multiplication** − Multiplies values on either side of the operator |
| /                                        | **Division** − Divides left hand operand by right hand operand |
| %                                        | **Modulus** − Divides left hand operand by right hand operand and returns remainder |
| ? :                                      | **Bincond** − Evaluates the Boolean operators. It has three operands: variable **x** = (expression) ? **value1** *if true* : **value2** *if false*. () |
| CASE <br />WHEN<br /> THEN <br />ELSE <br />END | **Case** − The case operator is equivalent to nested bincond operator |

### Comparison Operators

| Operator | Description                              |
| -------- | ---------------------------------------- |
| ==       | **Equal** − Checks if the values of two operands are equal or not; if yes, then the condition becomes true |
| !=       | **Not Equal** − Checks if the values of two operands are equal or not. If the values are not equal, then condition becomes true |
| >        | **Greater than** − Checks if the value of the left operand is greater than the value of the right operand. If yes, then the condition becomes true |
| <        | **Less than** − Checks if the value of the left operand is less than the value of the right operand. If yes, then the condition becomes true |
| >=       | **Greater than or equal to** − Checks if the value of the left operand is greater than or equal to the value of the right operand. If yes, then the condition becomes true |
| <=       | **Less than or equal to** − Checks if the value of the left operand is less than or equal to the value of the right operand. If yes, then the condition becomes true |
| matches  | **Pattern matching** − Checks whether the string in the left-hand side matches with the constant in the right-hand side |

### Type construction Operators

| Operator | Description                              |
| -------- | ---------------------------------------- |
| ()       | **Tuple constructor operator** − This operator is used to construct a tuple |
| {}       | **Bag constructor operator** − This operator is used to construct a bag |
| []       | **Map constructor operator** − This operator is used to construct a tuple |

