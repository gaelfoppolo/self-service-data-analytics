## Hive built-in functions

### Mathematical Functions :

| Return Type | Name(Signature)                          | Description                              |
| ----------- | ---------------------------------------- | ---------------------------------------- |
| double      | round(double a)                          | Returns the rounded BIGINT value of the double |
| double      | round(double a, int d)                   | Returns the double rounded to d decimal places |
| bigint      | floor(double a)                          | Returns the maximum BIGINT value that is equal or less than the double |
| bigint      | ceil(double a), ceiling(double a)        | Returns the minimum BIGINT value that is equal or greater than the double |
| double      | rand(), rand(int seed)                   | Returns a random number (that changes from row to row) that is distributed uniformly from 0 to 1. Specifying the seed will make sure the generated random number sequence is deterministic. |
| double      | exp(double a)                            | Returns ea where e is the base of the natural logarithm |
| double      | ln(double a)                             | Returns the natural logarithm of the argument |
| double      | log10(double a)                          | Returns the base-10 logarithm of the argument |
| double      | log2(double a)                           | Returns the base-2 logarithm of the argument |
| double      | log(double base, double a)               | Return the base "base" logarithm of the argument |
| double      | pow(double a, double p), power(double a, double p) | Return ap                                |
| double      | sqrt(double a)                           | Returns the square root of a             |
| string      | bin(bigint a)                            | Returns the number in binary format (see <http://dev.mysql.com/doc/refman/5.0/en/string-functions.html#function_bin>) |
| string      | hex(bigint a) hex(string a)              | If the argument is an int, hex returns the number as a string in hex format. Otherwise if the number is a string, it converts each character into its hex representation and returns the resulting string. (see <http://dev.mysql.com/doc/refman/5.0/en/string-functions.html#function_hex>) |
| string      | unhex(string a)                          | Inverse of hex. Interprets each pair of characters as a hexadecimal number and converts to the character represented by the number. |
| string      | conv(bigint num, int from_base, int to_base), conv(STRING num, int from_base, int to_base) | Converts a number from a given base to another (see <http://dev.mysql.com/doc/refman/5.0/en/mathematical-functions.html#function_conv>) |
| double      | abs(double a)                            | Returns the absolute value               |
| int double  | pmod(int a, int b) pmod(double a, double b) | Returns the positive value of a mod b    |
| double      | sin(double a)                            | Returns the sine of a (a is in radians)  |
| double      | asin(double a)                           | Returns the arc sin of x if -1<=a<=1 or null otherwise |
| double      | cos(double a)                            | Returns the cosine of a (a is in radians) |
| double      | acos(double a)                           | Returns the arc cosine of x if -1<=a<=1 or null otherwise |
| double      | tan(double a)                            | Returns the tangent of a (a is in radians) |
| double      | atan(double a)                           | Returns the arctangent of a              |
| double      | degrees(double a)                        | Converts value of a from radians to degrees |
| double      | radians(double a)                        | Converts value of a from degrees to radians |
| int double  | positive(int a), positive(double a)      | Returns a                                |
| int double  | negative(int a), negative(double a)      | Returns -a                               |
| float       | sign(double a)                           | Returns the sign of a as '1.0' or '-1.0' |
| double      | e()                                      | Returns the value of e                   |
| double      | pi()                                     | Returns the value of pi                  |

### Collection Functions :

| Return Type | Name(Signature)                 | Description                              |
| ----------- | ------------------------------- | ---------------------------------------- |
| int         | size(Map<K.V>)                  | Returns the number of elements in the map type |
| int         | size(Array<T>)                  | Returns the number of elements in the array type |
| array<K>    | map_keys(Map<K.V>)              | Returns an unordered array containing the keys of the input map |
| array<V>    | map_values(Map<K.V>)            | Returns an unordered array containing the values of the input map |
| boolean     | array_contains(Array<T>, value) | Returns TRUE if the array contains value |
| array<t>    | sort_array(Array<T>)            | Sorts the input array in ascending order according to the natural ordering of the array elements and returns it |

### Types Conversions Functions :

| Return Type                   | Name(Signature)        | Description                              |
| ----------------------------- | ---------------------- | ---------------------------------------- |
| binary                        | binary(string\|binary) | Casts the parameter into a binary        |
| Expected "=" to follow "type" | cast(expr as <type>)   | Converts the results of the expression expr to <type> e.g. cast('1' as BIGINT) will convert the string '1' to it integral representation. A null is returned if the conversion does not succeed |

### Date Functions :

| Return Type | Name(Signature)                          | Description                              |
| ----------- | ---------------------------------------- | ---------------------------------------- |
| string      | from_unixtime(bigint unixtime[, string format]) | Converts the number of seconds from unix epoch (1970-01-01 00:00:00 UTC) to a string representing the timestamp of that moment in the current system time zone in the format of "1970-01-01 00:00:00" |
| bigint      | unix_timestamp()                         | Gets current time stamp using the default time zone. |
| bigint      | unix_timestamp(string date)              | Converts time string in format `yyyy-MM-dd HH:mm:ss` to Unix time stamp, return 0 if fail: unix_timestamp('2009-03-20 11:30:01') = 1237573801 |
| bigint      | unix_timestamp(string date, string pattern) | Convert time string with given pattern (see [here](http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html)) to Unix time stamp, return 0 if fail: unix_timestamp('2009-03-20', 'yyyy-MM-dd') = 1237532400 |
| string      | to_date(string timestamp)                | Returns the date part of a timestamp string: to_date("1970-01-01 00:00:00") = "1970-01-01" |
| int         | year(string date)                        | Returns the year part of a date or a timestamp string: year("1970-01-01 00:00:00") = 1970, year("1970-01-01") = 1970 |
| int         | month(string date)                       | Returns the month part of a date or a timestamp string: month("1970-11-01 00:00:00") = 11, month("1970-11-01") = 11 |
| int         | day(string date) dayofmonth(date)        | Return the day part of a date or a timestamp string: day("1970-11-01 00:00:00") = 1, day("1970-11-01") = 1 |
| int         | hour(string date)                        | Returns the hour of the timestamp: hour('2009-07-30 12:58:59') = 12, hour('12:58:59') = 12 |
| int         | minute(string date)                      | Returns the minute of the timestamp      |
| int         | second(string date)                      | Returns the second of the timestamp      |
| int         | weekofyear(string date)                  | Return the week number of a timestamp string: weekofyear("1970-11-01 00:00:00") = 44, weekofyear("1970-11-01") = 44 |
| int         | datediff(string enddate, string startdate) | Return the number of days from startdate to enddate: datediff('2009-03-01', '2009-02-27') = 2 |
| string      | date_add(string startdate, int days)     | Add a number of days to startdate: date_add('2008-12-31', 1) = '2009-01-01' |
| string      | date_sub(string startdate, int days)     | Subtract a number of days to startdate: date_sub('2008-12-31', 1) = '2008-12-30' |
| timestamp   | from_utc_timestamp(timestamp, string timezone) | Assumes given timestamp ist UTC and converts to given timezone |
| timestamp   | to_utc_timestamp(timestamp, string timezone) | Assumes given timestamp is in given timezone and converts to UTC |

### Conditional Functions :

| Return Type | Name(Signature)                          | Description                              |
| ----------- | ---------------------------------------- | ---------------------------------------- |
| T           | if(boolean testCondition, T valueTrue, T valueFalseOrNull) | Return valueTrue when testCondition is true, returns valueFalseOrNull otherwise |
| T           | COALESCE(T v1, T v2, ...)                | Return the first v that is not NULL, or NULL if all v's are NULL |
| T           | CASE a WHEN b THEN c [WHEN d THEN e]* [ELSE f] END | When a = b, returns c; when a = d, return e; else return f |
| T           | CASE WHEN a THEN b [WHEN c THEN d]* [ELSE e] END | When a = true, returns b; when c = true, return d; else return e |

### String Functions :

| Return Type                  | Name(Signature)                          | Description                              |
| ---------------------------- | ---------------------------------------- | :--------------------------------------- |
| int                          | ascii(string str)                        | Returns the numeric value of the first character of str |
| string                       | concat(string\|binary A, string\|binary B...) | Returns the string or bytes resulting from concatenating the strings or bytes passed in as parameters in order. e.g. concat('foo', 'bar') results in 'foobar'. Note that this function can take any number of input strings. |
| array<struct<string,double>> | context_ngrams(array<array<string>>, array<string>, int K, int pf) | Returns the top-k contextual N-grams from a set of tokenized sentences, given a string of "context". See [StatisticsAndDataMining](https://cwiki.apache.org/confluence/display/Hive/StatisticsAndDataMining) for more information. |
| string                       | concat_ws(string SEP, string A, string B...) | Like concat() above, but with custom separator SEP. |
| string                       | concat_ws(string SEP, array<string>)     | Like concat_ws() above, but taking an array of strings. |
| int                          | find_in_set(string str, string strList)  | Returns the first occurance of str in strList where strList is a comma-delimited string. Returns null if either argument is null. Returns 0 if the first argument contains any commas. e.g. find_in_set('ab', 'abc,b,ab,c,def') returns 3 |
| string                       | format_number(number x, int d)           | Formats the number X to a format like '#,###,###.##', rounded to D decimal places, and returns the result as a string. If D is 0, the result has no decimal point or fractional part. |
| string                       | get_json_object(string json_string, string path) | Extract json object from a json string based on json path specified, and return json string of the extracted json object. It will return null if the input json string is invalid. The json path can only have the characters [0-9a-z_], i.e., no upper-case or special characters. Also, the keys *cannot start with numbers.* This is due to restrictions on Hive column names. |
| boolean                      | in_file(string str, string filename)     | Returns true if the string str appears as an entire line in filename. |
| int                          | instr(string str, string substr)         | Returns the position of the first occurence of substr in str |
| int                          | length(string A)                         | Returns the length of the string         |
| int                          | locate(string substr, string str[, int pos]) | Returns the position of the first occurrence of substr in str after position pos |
| string                       | lower(string A) lcase(string A)          | Returns the string resulting from converting all characters of B to lower case e.g. lower('fOoBaR') results in 'foobar' |
| string                       | lpad(string str, int len, string pad)    | Returns str, left-padded with pad to a length of len |
| string                       | ltrim(string A)                          | Returns the string resulting from trimming spaces from the beginning(left hand side) of A e.g. ltrim(' foobar ') results in 'foobar ' |
| array<struct<string,double>> | ngrams(array<array<string>>, int N, int K, int pf) | Returns the top-k N-grams from a set of tokenized sentences, such as those returned by the sentences() UDAF. See [StatisticsAndDataMining](https://cwiki.apache.org/confluence/display/Hive/StatisticsAndDataMining) for more information. |
| string                       | parse_url(string urlString, string partToExtract [, string keyToExtract]) | Returns the specified part from the URL. Valid values for partToExtract include HOST, PATH, QUERY, REF, PROTOCOL, AUTHORITY, FILE, and USERINFO. e.g. parse_url('http://facebook.com/path1/p.php?k1=v1&k2=v2#Ref1', 'HOST') returns 'facebook.com'. Also a value of a particular key in QUERY can be extracted by providing the key as the third argument, e.g. parse_url('http://facebook.com/path1/p.php?k1=v1&k2=v2#Ref1', 'QUERY', 'k1') returns 'v1'. |
| string                       | printf(String format, Obj... args)       | Returns the input formatted according do printf-style format strings |
| string                       | regexp_extract(string subject, string pattern, int index) | Returns the string extracted using the pattern. e.g. regexp_extract('foothebar', 'foo(.*?)(bar)', 2) returns 'bar.' Note that some care is necessary in using predefined character classes: using '\s' as the second argument will match the letter s; ' s' is necessary to match whitespace, etc. The 'index' parameter is the Java regex Matcher group() method index. See docs/api/java/util/regex/Matcher.html for more information on the 'index' or Java regex group() method. |
| string                       | regexp_replace(string INITIAL_STRING, string PATTERN, string REPLACEMENT) | Returns the string resulting from replacing all substrings in INITIAL_STRING that match the java regular expression syntax defined in PATTERN with instances of REPLACEMENT, e.g. regexp_replace("foobar", "oo\|ar", "") returns 'fb.' Note that some care is necessary in using predefined character classes: using '\s' as the second argument will match the letter s; ' s' is necessary to match whitespace, etc. |
| string                       | repeat(string str, int n)                | Repeat str n times                       |
| string                       | reverse(string A)                        | Returns the reversed string              |
| string                       | rpad(string str, int len, string pad)    | Returns str, right-padded with pad to a length of len |
| string                       | rtrim(string A)                          | Returns the string resulting from trimming spaces from the end(right hand side) of A e.g. rtrim(' foobar ') results in ' foobar' |
| array<array<string>>         | sentences(string str, string lang, string locale) | Tokenizes a string of natural language text into words and sentences, where each sentence is broken at the appropriate sentence boundary and returned as an array of words. The 'lang' and 'locale' are optional arguments. e.g. sentences('Hello there! How are you?') returns ( ("Hello", "there"), ("How", "are", "you") ) |
| string                       | space(int n)                             | Return a string of n spaces              |
| array                        | split(string str, string pat)            | Split str around pat (pat is a regular expression) |
| map<string,string>           | str_to_map(text[, delimiter1, delimiter2]) | Splits text into key-value pairs using two delimiters. Delimiter1 separates text into K-V pairs, and Delimiter2 splits each K-V pair. Default delimiters are ',' for delimiter1 and '=' for delimiter2. |
| string                       | substr(string\|binary A, int start) substring(string\|binary A, int start) | Returns the substring or slice of the byte array of A starting from start position till the end of string A e.g. substr('foobar', 4) results in 'bar' (see <http://dev.mysql.com/doc/refman/5.0/en/string-functions.html#function_substr>) |
| string                       | substr(string\|binary A, int start, int len) substring(string\|binary A, int start, int len) | Returns the substring or slice of the byte array of A starting from start position with length len e.g. substr('foobar', 4, 1) results in 'b' (see <http://dev.mysql.com/doc/refman/5.0/en/string-functions.html#function_substr>) |
| string                       | translate(string input, string from, string to) | Translates the input string by replacing the characters present in the `from` string with the corresponding characters in the `to` string. This is similar to the `translate` function in [PostgreSQL](http://www.postgresql.org/docs/9.1/interactive/functions-string.html). If any of the parameters to this UDF are NULL, the result is NULL as well |
| string                       | trim(string A)                           | Returns the string resulting from trimming spaces from both ends of A e.g. trim(' foobar ') results in 'foobar' |
| string                       | upper(string A) ucase(string A)          | Returns the string resulting from converting all characters of A to upper case e.g. upper('fOoBaR') results in 'FOOBAR' |

### Miscellaneous Functions :

| Return Type | Name(Signature)   | Description                           |
| ----------- | ----------------- | ------------------------------------- |
| int         | hash(a1[, a2...]) | Returns a hash value of the arguments |

## 