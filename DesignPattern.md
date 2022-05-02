1. Singleton Pattern implementation.
    <details>
    <summary>Using class based approach</summary>
    
    ```
        class Singleton {
            constructor(){
                if(Singleton._instance){
                    return Singleton._instance;
                }

                Singleton._instance = this;
            }

            static instance() {
                if(!Singleton._instance){
                    return new Singleton();
                }
                return Singleton._instance;
            }
        }

        Singleton._instance = null;
        
    ```
    </details>

    <details>
    <summary>Using IIFE based approach</summary>
    
    ```
        let _SingleTon =(function () {
        let instance;
        return{
            getInstance:function () {
                    if(!instance){
                        instance= {};  // we can separate function for creating instance
                        return instance;
                    }
                return instance
            }
        }
        
    })();

    console.log(_SingleTon.getInstance()===_SingleTon.getInstance())
    ```
    </details>
