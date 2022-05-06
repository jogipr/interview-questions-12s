1. Write the function to get nth prime number ?
  
   <details>
    <summary>Solution</summary>

    ```

        const isPrimeNumber = (num) => {
        let isPrime = true
        if (num >= 2) {
            for (let i = 2; i < num; i++) {
                if (num % i == 0) {
                    isPrime = false;
                    break;
                }
            }
        }
        return isPrime;
    }

    function nthPrimeNumber(pos) {

        let num = 2;
        let cnt = 1;
        while (cnt <= pos) {
            if (!isPrimeNumber(num)) {
                num++;
            } else {
                cnt++;
                num++;
            }

        }
        return num - 1;
    }

        console.log(nthPrimeNumber(3))
        // 2 3 5 7 11 => 5
            
    ```
    </details>

2. Write a function to flaten the array 

    <details>
    <summary>Solution</summary>

    ```
    let arr = [1, [2, [3, [4]]], 5, [6]]
    //output -> [1, 2, 3, 4, 5, 6]


    function getFlatArray(arr) {
        let output=[]
        arr.forEach(item=>{
        
            if(Array.isArray(item)){
            output= output.concat(getFlatArray(item))
            }else{
                output.push(item)
            }

        })
        return output;
    }

    getFlatArray(arr)
    
    ```
    </details>

3. Write a function to get count of all the letter in the given string

    <details>
    <summary>Solution</summary>

        ```
            
            function getUnique(input) {
            let output={}
            for (let index = 0; index < input.length; index++) {
                    if(output[input[index]]){
                        output[input[index]]=++output[input[index]]
                    }else{
                        output[input[index]]=1;
                    }
                }   
                console.log(output)
            }

            var str = 'aaecca';
            getUnique(str
            
        ```
    </details>
  
 
