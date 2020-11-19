[Back to index](./index.md)

## Convert integer to string

Converts an integer number to its string representation

``` C
void tostring(char str[], long int num)
{
  long int i, rem, len = 0, n;
  n = num;
  while (n != 0)
  {
    len++;
    n /= 10;
  }
  for (i = 0; i < len; i++)
  {
    rem = num % 10;
    num = num / 10;
    str[len - (i + 1)] = rem + '0';
  }
  str[len] = '\0';
}
```

``` C
void tostring(char [], long int);
```

Usage:

``` C
char text[20];
int i = 12345;

tostring(text, i);
```