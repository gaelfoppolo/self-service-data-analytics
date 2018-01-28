## Pig Latin Built-in Functions

### Evaluation Functions

| Function name                            | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [AVG(expression)](https://pig.apache.org/docs/r0.9.1/func.html#avg) | To compute the average of the numerical values within a bag |
| [BagToString(vals:bag [, delimiter:chararray])](http://pig.apache.org/docs/r0.17.0/func.html#bagtostring) | Concatenate the elements of a Bag into a chararray string, placing an optional delimiter between each value |
| [BagToTuple(expression)](http://pig.apache.org/docs/r0.17.0/func.html#bagtotuple) | Un-nests the elements of a bag into a tuple |
| [Bloom(String hashType, String mode, String vectorSize, String nbHash)](http://pig.apache.org/docs/r0.17.0/func.html#bloom) | Bloom filters are a common way to select a limited set of records before moving data for a join or other heavy weight operation |
| [CONCAT(expression, expression, [...expression])](https://pig.apache.org/docs/r0.9.1/func.html#concat) | To concatenate two or more expressions of same type |
| [COUNT(expression)](https://pig.apache.org/docs/r0.9.1/func.html#count) | To get the number of elements in a bag, while counting the number of tuples in a bag |
| [COUNT_STAR(expression)](https://pig.apache.org/docs/r0.9.1/func.html#count-star) | It is similar to the **COUNT()** function. It is used to get the number of elements in a bag |
| [DIFF(expression, expression)](https://pig.apache.org/docs/r0.9.1/func.html#diff) | To compare two bags (fields) in a tuple  |
| [IsEmpty(expression)](https://pig.apache.org/docs/r0.9.1/func.html#isempty) | To check if a bag or map is empty        |
| [MAX(expression)](https://pig.apache.org/docs/r0.9.1/func.html#max) | To calculate the highest value for a column (numeric values or chararrays) in a single-column bag |
| [MIN(expression)](https://pig.apache.org/docs/r0.9.1/func.html#min) | To get the minimum (lowest) value (numeric or chararray) for a certain column in a single-column bag |
| [PluckTuple(expression1,expression3)](http://pig.apache.org/docs/r0.17.0/func.html#plucktuple) | Allows the user to specify a string prefix, and then filter for the columns in a relation that begin with that prefix or match that regex pattern. Optionally, include flag 'false' to filter for columns that do not match that prefix or match that regex pattern |
| [SIZE(expression)](https://pig.apache.org/docs/r0.9.1/func.html#size) | To compute the number of elements based on any Pig data type |
| [SUBSTRACT(expression, expression)](http://pig.apache.org/docs/r0.17.0/func.html#subtract) | To subtract two bags. It takes two bags as inputs and returns a bag which contains the tuples of the first bag that are not in the second bag |
| [SUM(expression)](https://pig.apache.org/docs/r0.9.1/func.html#sum) | To get the total of the numeric values of a column in a single-column bag |
| [IN(expression)](http://pig.apache.org/docs/r0.17.0/func.html#in) | IN operator allows you to easily test if an expression matches any value in a list of values. It is used to reduce the need for multiple OR conditions |
| [TOKENIZE(expression [, 'field_delimiter'])](https://pig.apache.org/docs/r0.9.1/func.html#tokenize) | To split a string (which contains a group of words) in a single tuple and return a bag which contains the output of the split operation |

### Load & Store Functions :

| Function name                            | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [Handling Compression](https://pig.apache.org/docs/r0.9.1/func.html#handling-compression) | In Pig Latin, we can load and store compressed data |
| [BinStorage()](https://pig.apache.org/docs/r0.9.1/func.html#binstorage) | To load and store data into Pig using machine readable format |
| [JsonLoader(['schema']) , JsonStorage()](http://pig.apache.org/docs/r0.17.0/func.html#jsonloadstore) | Load or store JSON data                  |
| [PigDump()](https://pig.apache.org/docs/r0.9.1/func.html#pigdump) | PigDump stores data as tuples in human-readable UTF-8 format |
| [PigStorage([field_delimiter] , ['options'])](https://pig.apache.org/docs/r0.9.1/func.html#pigstorage) | To load and store structured files       |
| [TextLoader()](https://pig.apache.org/docs/r0.9.1/func.html#textloader) | To load unstructured data into Pig       |
| [HBaseStorage('columns', ['options'])](http://pig.apache.org/docs/r0.17.0/func.html#HBaseStorage) | Loads and stores data from an HBase table |
| [AvroStorage(['schema\|record name'], ['options'])](http://pig.apache.org/docs/r0.17.0/func.html#AvroStorage) | Loads and stores data from Avro files    |
| [TrevniStorage(['schema\|record name'], ['options'])](http://pig.apache.org/docs/r0.17.0/func.html#TrevniStorage) | Loads and stores data from Trevni files  |
| [AccumuloStorage (['columns'[, 'options'] ])](http://pig.apache.org/docs/r0.17.0/func.html#AccumuloStorage) | Loads or stores data from an Accumulo table. The first element in a Tuple is equivalent to the "row" from the Accumulo Key, while the columns in that row are can be grouped in various static or wildcarded ways. Basic wildcarding functionality exists to group various columns families/qualifiers into a Map for LOADs, or serialize a Map into some group of column families or qualifiers on STOREs |
| [OrcStorage(['options'])](http://pig.apache.org/docs/r0.17.0/func.html#OrcStorage) | Loads from or stores data to Orc file    |

### Bag & Tuple Functions

| Function name                            | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [TOBAG(expression [, expression ...])](https://pig.apache.org/docs/r0.9.1/func.html#tobag) | To convert two or more expressions into a bag |
| [TOP(topN,column,relation)](https://pig.apache.org/docs/r0.9.1/func.html#topx) | To get the top **N** tuples of a relation |
| [TOTUPLE(expression [, expression ...])](https://pig.apache.org/docs/r0.9.1/func.html#totuple) | To convert one or more expressions into a tuple |
| [TOMAP(key-expression, value-expression [, key-expression, value-expression ...])](http://pig.apache.org/docs/r0.17.0/func.html#tomap) | Converts key/value expression pairs into a map |

### Math Functions

| Function name                            | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [ABS(expression)](http://pig.apache.org/docs/r0.17.0/func.html#abs) | Returns the absolute value of an expression |
| [ACOS(expression)](http://pig.apache.org/docs/r0.17.0/func.html#acos) | Returns the arc cosine of an expression  |
| [ASIN()](http://pig.apache.org/docs/r0.17.0/func.html#asin) | Returns the arc sine of an expression    |
| [ATAN(expression)](http://pig.apache.org/docs/r0.17.0/func.html#atan) | Returns the arc tangent of an expression |
| [CBRT(expression)](http://pig.apache.org/docs/r0.17.0/func.html#cbrt) | Returns the cube root of an expression   |
| [CEIL(expression)](http://pig.apache.org/docs/r0.17.0/func.html#ceil) | Returns the value of an expression rounded up to the nearest integer |
| [COS(expression)](http://pig.apache.org/docs/r0.17.0/func.html#cos) | Returns the trigonometric cosine of an expression |
| [COSH(expression)](http://pig.apache.org/docs/r0.17.0/func.html#cosh) | Returns the hyperbolic cosine of an expression |
| [EXP(expression)](http://pig.apache.org/docs/r0.17.0/func.html#exp) | Returns Euler's number e raised to the power of x |
| [FLOOR(expression)](http://pig.apache.org/docs/r0.17.0/func.html#floor) | Returns the value of an expression rounded down to the nearest integer |
| [LOG(expression)](http://pig.apache.org/docs/r0.17.0/func.html#log) | Returns the natural logarithm (base e) of an expression |
| [LOG10(expression)](http://pig.apache.org/docs/r0.17.0/func.html#log10) | Returns the base 10 logarithm of an expression |
| [RANDOM(expression)](http://pig.apache.org/docs/r0.17.0/func.html#random) | Returns a pseudo random number           |
| [ROUND(expression)](http://pig.apache.org/docs/r0.17.0/func.html#round) | Returns the value of an expression rounded to an integer |
| [ROUND_TO(expression)](http://pig.apache.org/docs/r0.17.0/func.html#round_to) | Returns the value of an expression rounded to a fixed number of decimal digits |
| [SIN(expression)](http://pig.apache.org/docs/r0.17.0/func.html#sin) | Returns the sine of an expression        |
| [SINH(expression)](http://pig.apache.org/docs/r0.17.0/func.html#sinh) | Returns the hyperbolic sine of an expression |
| [SQRT(expression)](http://pig.apache.org/docs/r0.17.0/func.html#sqrt) | Returns the positive square root of an expression |
| [TAN(expression)](http://pig.apache.org/docs/r0.17.0/func.html#tan) | Returns the trigonometric tangent of an angle |
| [TANH(expression)](http://pig.apache.org/docs/r0.17.0/func.html#tanh) | Returns the hyperbolic tangent of an expression |

### String Functions

| Function name                            | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [ENDSWITH(string, testAgainst)](http://pig.apache.org/docs/r0.17.0/func.html#endswith) | Tests inputs to determine if the first argument ends with the string in the second |
| [EqualsIgnoreCase(string1, string2)](http://pig.apache.org/docs/r0.17.0/func.html#equalsignorecase) | Compares two Strings ignoring case considerations |
| [INDEXOF(string, 'character', startIndex)](http://pig.apache.org/docs/r0.17.0/func.html#indexof) | Returns the index of the first occurrence of a character in a string, searching forward from a start index |
| [LAST_INDEX_OF(string, 'character')](http://pig.apache.org/docs/r0.17.0/func.html#last-index-of) | Returns the index of the last occurrence of a character in a string, searching backward from the end of the string |
| [LCFIRST(expression)](http://pig.apache.org/docs/r0.17.0/func.html#lcfirst) | Converts the first character in a string to lower case |
| [LOWER(expression)](http://pig.apache.org/docs/r0.17.0/func.html#lower) | Converts all characters in a string to lower case |
| [LTRIM(expression)](http://pig.apache.org/docs/r0.17.0/func.html#ltrim) | Returns a copy of a string with only leading white space removed |
| [REGEX_EXTRACT(string, regex, index)](http://pig.apache.org/docs/r0.17.0/func.html#regex-extract) | Performs regular expression matching and extracts the matched group defined by an index parameter |
| [REGEX_EXTRACT_ALL(string, regex)](http://pig.apache.org/docs/r0.17.0/func.html#regex-extract-all) | Performs regular expression matching and extracts all matched groups |
| [REGEX_SEARCH((string, 'regExp')](http://pig.apache.org/docs/r0.17.0/func.html#regex-search) | Performs regular expression matching and searches all matched characters in a string |
| [REPLACE(string, 'regExp', 'newChar')](http://pig.apache.org/docs/r0.17.0/func.html#replace) | Replaces existing characters in a string with new characters |
| [RTRIM(expression)](http://pig.apache.org/docs/r0.17.0/func.html#rtrim) | Returns a copy of a string with only trailing white space removed |
| [SPRINTF(format, [...vals])](http://pig.apache.org/docs/r0.17.0/func.html#sprintf) | Formats a set of values according to a printf-style template, using the native Java Formatter library |
| [STARTSWITH(string, testAgainst)](http://pig.apache.org/docs/r0.17.0/func.html#startswith) | Tests inputs to determine if the first argument starts with the string in the second |
| [STRSPLIT(string, regex, limit)](http://pig.apache.org/docs/r0.17.0/func.html#strsplit) | Splits a string around matches of a given regular expression |
| [STRSPLITTOBAG(string, regex, limit)](http://pig.apache.org/docs/r0.17.0/func.html#strsplittobag) | Splits a string around matches of a given regular expression and returns a databag |
| [SUBSTRING(string, startIndex, stopIndex)](http://pig.apache.org/docs/r0.17.0/func.html#substring) | Returns a substring from a given string  |
| [TRIM(expression)](http://pig.apache.org/docs/r0.17.0/func.html#trim) | Returns a copy of a string with leading and trailing white space removed |
| [UCFIRST(expression)](http://pig.apache.org/docs/r0.17.0/func.html#ucfirst) | Returns a string with the first character converted to upper case |
| [UPPER(expression)](http://pig.apache.org/docs/r0.17.0/func.html#upper) | Returns a string converted to upper case |
| [UniqueID](http://pig.apache.org/docs/r0.17.0/func.html#uniqueid) | Returns a unique id string for each record in the alias |

### DateTime Functions

| Function name                            | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [AddDuration(datetime, duration)](http://pig.apache.org/docs/r0.17.0/func.html#add-duration) | Returns the result of a DateTime object plus a Duration object |
| [CurrentTime()](http://pig.apache.org/docs/r0.17.0/func.html#current-time) | Returns the DateTime object of the current time |
| [DaysBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#days-between) | Returns the number of days between two DateTime objects |
| [GetDay(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-day) | Returns the day of a month from a DateTime object |
| [GetHour(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-hour) | Returns the hour of a day from a DateTime object |
| [GetMilliSecond(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-milli-second) | Returns the millisecond of a second from a DateTime object |
| [GetMinute(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-minute) | Returns the minute of a hour from a DateTime object |
| [GetMonth(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-month) | Returns the month of a year from a DateTime object |
| [GetSecond(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-second) | Returns the second of a minute from a DateTime object |
| [GetWeek(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-week) | Returns the week of a week year from a DateTime object |
| [GetWeekYear(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-week-year) | Returns the week year from a DateTime object |
| [GetYear(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#get-year) | Returns the year from a DateTime object  |
| [HoursBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#hours-between) | Returns the number of hours between two DateTime objects |
| [MilliSecondsBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#milli-seconds-between) | Returns the number of milliseconds between two DateTime objects |
| [MinutesBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#minutes-between) | Returns the number of minutes between two DateTime objects |
| [MonthsBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#months-between) | Returns the number of months between two DateTime objects |
| [SecondsBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#seconds-between) | Returns the number of seconds between two DateTime objects |
| [SubtractDuration(datetime, duration)](http://pig.apache.org/docs/r0.17.0/func.html#subtract-duration) | Returns the result of a DateTime object minus a Duration object |
| [ToDate(userstring, format, timezone)](http://pig.apache.org/docs/r0.17.0/func.html#to-date) | Returns a DateTime object according to parameters |
| [ToMilliSeconds(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#to-milli-seconds) | Returns the number of milliseconds elapsed since January 1, 1970, 00:00:00.000 GMT for a DateTime object |
| [ToString(datetime [, format string])](http://pig.apache.org/docs/r0.17.0/func.html#to-string) | ToString converts the DateTime object to the ISO or the customized string |
| [ToUnixTime(datetime)](http://pig.apache.org/docs/r0.17.0/func.html#to-unix-time) | Returns the Unix Time as long for a DateTime object. UnixTime is the number of seconds elapsed since January 1, 1970, 00:00:00.000 GMT |
| [WeeksBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#weeks-between) | Returns the number of weeks between two DateTime objects |
| [YearsBetween(datetime1, datetime2)](http://pig.apache.org/docs/r0.17.0/func.html#years-between) | Returns the number of years between two DateTime objects |

