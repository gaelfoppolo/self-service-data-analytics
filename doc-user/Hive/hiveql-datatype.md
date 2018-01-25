## Hive Data type

The Hive data type can be classified in 4 types.

### Column type

Column types are used as column data types of Hive.

#### Integral types:

| Type     | Example |
| :------- | :------ |
| TINYINT  | 10Y     |
| SMALLINT | 10S     |
| INT      | 10      |
| BIGINT   | 10L     |

#### String type:

String type data types can be specified using single quotes (' ') or double quotes (" "). It contains two data types: VARCHAR and CHAR. Hive follows C-types escape characters.

| Type    | Length     |
| ------- | ---------- |
| VARCHAR | 1 to 65355 |
| CHAR    | 255        |

#### Timestamp:

It supports traditional UNIX timestamp with optional nanosecond precision.

#### Dates :

DATE values are described in year/month/day ( YYYY-MM-DD).,

#### Decimal :

The DECIMAL type in Hive is as same as Big Decimal format of Java. The syntax is as :

**DECIMAL(*precision, scale*)**

*Example:*  decimal(10,0)

#### Union types :

Union is a collection of heterogeneous data types. You can create an instance using **create union**. More information are available in hive documentation (link at the end).

### Literals

The following literals are used in Hive :

- Floating point types (DOUBLE )
- decimal types (Higher than DOUBLE)

### Null values

Missing values are represented by the special value NULL

### Complex types

The complex types are essentially Object from Java such as ARRAY , MAP.