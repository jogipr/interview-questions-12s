1. Coercion during addition ,substraction ,multipication etc

  a) To String Coercion 
  When a string is added with the number or non-string value using the plus(+) operator then the output of the expression is always a string.
  
    
    
      10 + '10'     //'1010'
      
      '10' + 10     //'1010'
      
      true + '10'   //'true10'
      
      undefined + '10'  // 'undefined10'
      
      null + '10'   // 'null10'
      
      NaN + ""  // 'NaN'
      Any type + string // 'typestring'
      
    
      
   b) To Number Coercion:
      The mathematical operations like Subtraction(-), Multiplication(*), Division(/), and Modulus(%) performed with the string then the output of the expression is          converted into a number implicitly.
      
   
       10  + 10     // 20
       
       true + 10    // 11
       
       undefined + 10  // NAN
      
       null + 10   // 10
       
       12 * '2'   //24
       
       true + null //  1
       
       true + undefined // NAN
       
       Any type + NaN   // NaN
       
       Any type + undefined // NaN
      
    
2. Coercion during equality and indentity equality operator.

[Follow this link for more details](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/)


