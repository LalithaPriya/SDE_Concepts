
Primitive types:

- String: "hey" or 'hey'
- Number: 2 or 2.4
- BigInt: used to store number which are above limit of Number datatype
    typeof 234567890123456789012345678901234567890n // Returns bigint
- Boolean : true or false
- Undefined: declared but not assigned
        var x = undefined // can aslo assign
- Null
- Symbol:used to store anonymous or unique value

--> Primitive data types can store only a single value. To store multiple and complex values, non-primitive data types are used.

Non primitive types:

- object

--> Variable initialization are not hoisted, only variable declarations are hoisted
i.e x = 20;
console.log(x); //20
var x;

To avoid hoisting, can run in strict mode by using "use strict" on top of code
i.e 
"use strict";
x = 20;
console.log(x); //error
var x;




