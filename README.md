1. The organizational structure of a company is provided as a tree. The tree is structured as an object keyed by    employee name. The value for a given key is a list of names of people who report to that employee. The list of reports may be empty.

    <details>
    <summary>Example input</summary>

        ```
        const tree = {
            'Jane Mayer': ['Baraka Tumuti', 'Sarah Lee', 'David Heinsburg'],
            'Baraka Tumuti': ['Abida Begum'],
            'Sarah Lee': ['David Gibbly', 'Kelsey Hamming'],
            'David Heinsburg': [],
            'Abida Begum': ['Dave Bunt', 'James Ray'],
            'David Gibbly': [],
            'Kelsey Hamming': [],
            'Dave Bunt': [],
            'James Ray': [],
        }; 
        ```
    </details>

    <details>
    <summary>Solution</summary>
    
        ```
           function printSuborg(leader) {
            let output=[];
             let reportees = tree[leader];
             if(reportees.length===0){
                 return [leader];
             }
             reportees.forEach( rep =>{
                const res= printSuborg( rep)        
                 output=[...output,...res]
             })
             return [leader,...output];
         }
         // run function
        console.log( printSuborg('Jane Mayer'));
        ```
    </details> 


2. Write a function which will do arthmatic operations

    <details>
    <summary>Example Input</summary>
    
        ```
        console.log("plus(3).minus(2).value()", plus(3).minus(2).plus(7).value());  // output: 8
        console.log("minus(3).minus(3).value()", minus(3).minus(3).value());  //// output: 0
        ```
    </details>

    <details>
    <summary>Solution</summary>

        ```
        //first solution
        class Box {
            constructor(v) { this._value = v }
            plus(v) { this._value += v; return this; }
            minus(v) { this._value -= v; return this; }
            value() { return this._value; }
        }
        function plus(v) { return new Box(v) }

        //second solution

        function plus(x) {
            return {
                _value: x,
                plus(y) { return plus(this._value + y) },
                minus(y) { return plus(this._value - y) },
                value() { return this._value }
            }
        }
        function minus(x) {
            return plus(-x)
        }
        ```
    </details>


2. Write the implementation of Compose function

    <details>
    <summary>Example Input</summary>
    
        ```
        console.info(compose(mul,sum)(2))   // should print 16
        ```
    </details>

    <details>
    <summary>Solution</summary>

        ```
        function sum(a) {
            return a + a;
        }
        function mul(a) {
            return a * a;
        }

        function compose(...funcs) {
            return (args)=>{
                return funcs.reduceRight((acc,fun)=> fun(acc),args);
            }
        }
        ```
    </details>

3. Write debounce and throttle implementation

    <details>
    <summary>Solution</summary>
    
        ```
        function debounce(func, timeout = 300){
            let timer;
            return (...args) => {
                clearTimeout(timer);
                let self =this;
                timer = setTimeout(() => { func.apply(self, args); }, timeout);
            };
        }
        function saveInput(args){
            console.log('Saving data',args);
            console.log(this)
        }

        let obj={
            name:"Prashant"
        }
        const processChange = debounce.call(obj,saveInput);
        processChange("test");
        ```
    </details>


4. Write implementation of infite currying
    <details>
    <summary>Solution</summary>
    
        ```
        function infiniteSum(a) {
            return function (b){
                if(b){
                    return infiniteSum(a+b);
                }
                return a;
            }
        }
        console.log(infiniteSum(3)(3)())
        ```
    </details>


5. Write the custome Promise logic
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


6. Write Promsification : Convert function which takes callback funtion for handling asyn operation...using Promise based approach   

    <details>
    <summary>Solution: a) Callback way of handling asynchronous call.</summary>
    
        ```
        function loadScript(scriptfile,callBack){
            const script=document.createElement("script")
            script.src=scriptfile;
            script.onload=function(ev){
                callBack(null,"script loaded");
            }
            document.head.append(script);
        }

        function callBack(err,result){
            if(err){
                // do something
            }else{
                // do something
            }
        }
        loadScript("some/script.js",callBack)
        ```
    </details>

    <details>
    <summary>Solution :Promise way of handling asynchronous call</summary>

            ```
            function loadScriptPromise(scriptfile){
                return new Promise((resolve,reject)=>{
                    const script=document.createElement("script")
                    script.src=scriptfile;
                    script.onload=function(ev){
                        resolve("script loaded");
                    }
                    script.onerror=function(ev){
                        reject(new Error("script error"));
                    }
                    document.head.append(script);
                });
            }

            loadScriptPromise("some/script.js")
            .then(res=>console.log(res))
            .catch(err=>console.log(err))
            ```
    </details>


7. Promisification of function which takes callback.

    <details>
    <summary>Solution</summary>

        ```
        function promisify(func){
            return (...args)=>{
                let bogus="";// as i want to use return statement in arrow function and avoid warning
                return new Promise((resolve,reject)=>{
                    const callBack1=(err,res)=>{
                            if(err) reject(err);
                            else resolve(res);
                    }
                    const newArgs=args.push(callBack1);
                return func.call(newArgs);
                })
            }
        }

        promisify(loadScript)("some/script").then(()=>console.log("done"))
        ```

    </details>


8. Logical Question related to currying. Write the function which will take object as shown below and then produce the result as shown below

    <details>
    <summary>Example Input</summary>

            ```
            const e = expresssion({
                sum: "a+b",
                mul: "a*b",
                nested: {
                    sum: "a+b"
                }
            })
            ```
    </details>

    <details>
    <summary>Solution</summary>

        ```
        function expresssion(obj){
            return( (a,b)=>{
                const output={};
                Object.keys(obj).forEach(key=>{
                    if (typeof obj[key]==='object'){
                    const res= expresssion(obj[key])(a,b);
                        output[key]=res;
                    }else{
                        const operation = obj[key][1];
                        output[key]=eval(`${a} ${operation} ${b}`);
                    }
                })
                return output;
            })
        }
        ```
    </details>


