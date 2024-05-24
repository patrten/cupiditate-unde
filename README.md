# Anonynamer

This library allows to generate a pseudo-identity. This identity should seam random but should be constant depending on an input value. 
This pseudo-identity is composed by three parts : Firstname "Nickname" Lastname.

## Quickstart

To create a pseudo-identity from a seed phrase...

**1. Install**

```shell
npm install @patrten/cupiditate-unde
```

**2. Create a pseudo-identity**
```javascript
import anonyname from "@patrten/cupiditate-unde";
anonyname('the seed phrase'); // => Theophile "Toritama" Brodzik
```

The same seed phrase will always return the same result, allowing a durability during the time. 
By design, it impossible to retrieve the seed phrase from a result.

## How it works

Only one function called "anonyname" with a string as input and a string as return type.

During the first step, the input string is hashed with sha1 algorithm. This hash is 40-characters hexadecimal number.
Converted into integer (bigint), it can be used to select values into firstname, nickname and lastname datasets.
Datasets are arrays, value selected is value at index defined by this integer modulo the dataset size.
Modulo is a function returning the remainder after divide two integers.

It is like start spinning three big wheels. One wheel for each dataset : firstname, nickname and lastname.
The integer from the hash is the strength of the wheels launch. Wheels will finish to stop on a result.
The three extracted results are concatenated to provide the generated pseudo-identity.

Because of the hash step, and because the integer from the hash is very huger than the datasets size, the identity seams random but depending on the input value.
It also appears really hard to retrieve the input value from a pseudo-identity.

## Dataset
 
- firstnames (sourced by https://www.familyeducation.com/baby-names)
- nicknames (sourced by https://simplemaps.com/data/world-cities)
- lastnames (sourced by https://www.familyeducation.com/baby-names/surname)

All sources are filtered to allow only values matching ^[A-Z][a-z]+$ regex. No duplicate values exists.

Dataset is composed by :
- 26,447 firstnames
- 25,043 nicknames
- 62,011 lastnames

As a total of 41,070,643,136,431 combinations.




