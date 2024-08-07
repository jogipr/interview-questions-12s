1. Write your own implementation for JSON.stringyfy.

    <details>
    <summary>Example Input</summary>

        ```
        const input = {
        'name': 'Prashant',
        'address' : {
            'city': 'pune',
            'state': 'MH'
        },
        'company': [{
            'name': 'xyz',
            'phone':  {
            'home': 'test1',
            'work': 'test2'
            }
        }]};
        
        ```
    </details>

    <details>
    <summary>Solution</summary>

    ```
    function stringifyObj(input) {
    let output="";
        if(Array.isArray(input)){
            output="[";
            Object.keys(input).forEach(key=>{
                if(typeof input[key]==='object'){
                    output += `'${stringifyObj(input[key])}'`
                    output += "],"
                }
                else{
                    output += `'${key}': '${input[key]}'`;
                    output += ","
                }
            })
        }else{
            output="{";
            Object.keys(input).forEach(key=>{
                if(typeof input[key]==='object'){
                    output += `'${key}': '${stringifyObj(input[key])}'`
                    output += "},"
                }
                else{
                    output += `'${key}': '${input[key]}'`;
                    output += ","
                }
            })
        }
    return output;
    }
    ```
    </details>

2. Write the polyfill for filter method of Array.

    <details>
    <summary>Example Input</summary>

        ```
        var logicAlbums = [
        {
            name: 'Bobby Tarantino',
            rating: 5,
        },
        { name: 'The Incredible True Story', rating: 4.5 },
        {
            name: 'Supermarket',
            rating: 4.9,
        },
        { name: 'Under Pressure', rating: 5 },
        ]
        ```
    </details>

    <details>
    <summary>Solution</summary>

        ```
        Array.prototype.filterAlbums = function(callback) {
        arr = []
        for (var i = 0; i < this.length; i++) {
            if (callback(this[i])) {
            arr.push(this[i])
            }
        }
        return arr
        }
        const newAlbums=logicAlbums.filterAlbums(function(album) {
        return album.rating > 4.9 // providing the context here
        })

        console.log(newAlbums)
        ```
    </details>

3. Write Polyfill for flat method of an Array

    <details>
    <summary>Example Input</summary>

        ```
        const input =[ "one", "two",["three","four",["five","six"]]];
        ```
    </details>

    <details>
    <summary>Solution</summary>

        ```
        let output=[];
        function getFlat(input){
            input.forEach(arr=>{
                if(!Array.isArray(arr)){
                    output.push(arr);
                }else{
                    getFlat(arr)
                }
            })
        }

        getFlat(input);
        console.log(output);

        // Implementation Polyfill function

        Array.prototype.myFlat=function(){
            let output=[];
            this.forEach(ar=>{
                if(!Array.isArray(ar)){
                    output.push(ar);
                }else{
                output= output.concat(ar.myFlat() )
                }
            })
            return output;
        }

        console.log(input.myFlat())
        ```
    </details>

4. Write the custome Promise logic
    <details>
    <summary>Solution</summary>
    
        ```
        Solution:
        function CustomePromise(executorFunc) {

            let resolution="pending";
            let successCb=[];
            let failureCb=[];

            function resolve(params) {
                const [successfunc] = successCb;
                successfunc(params);
            }

            function reject(params) {
                const [failureFunc] = failureCb;
                failureFunc(params);
            }

            setTimeout(()=>{
                executorFunc(resolve,reject);
            },1000);

            return{
                status:resolution,
                then:function (successfunc,failureFunc) {
                    if(this.status=='pending'){
                        successCb.push(successfunc);
                        failureCb.push(failureFunc);
                    }else{
                        successCb("successCb");
                    }
                }
            }
        }


        const ourPromise = new CustomePromise((resolve,reject)=>{
            resolve("i am done");
        })

        console.log(ourPromise)
        ourPromise.then((value)=> console.log(value));
        ```
    </details>

5. Write the Polyfill for call ,apply and bind
    <details>
    <summary>Solution</summary>
        
        ```
        const greet =function (){
                console.log(`hello ${this.name}`)
            }

        const person ={
            name:"John"
        }
        
        Function.prototype.myCall=function (context,...params) {
          
            if(typeof this!='function'){
                return new Error("error");
            }
            context.fn=this;
            context.fn(params)
        }
        console.log(greet.myCall(person))
        
        Function.prototype.myBind=function (context) {
           
            if(typeof this!='function'){
                return new Error("error");
            }
            context.fn=this;
            return function (params) {
                return context.fn(params)
            }
        }
        
        const boundedGreet=greet.myBind(person)
        console.log(boundedGreet())
        ```
    </details>
