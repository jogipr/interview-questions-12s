1. Different ways of creating an Object
      <details>
      <summary>Object literal syntax</summary>

      ```
       const person = {
        firstName:"Prashant",
        lastName:"Jogi"  
      }; 

      In this case person object __proto__ property points to Object.prototype
      ```
      </details>
      
      <details>
      <summary>Using Object.create method</summary>

      ```
       const person = Object.create({}); 
       const person = Object.create(null); 
       const emp={
        name:"Prashant"
       }       
       const person = Object.create(emp);

      In this case person object __proto__ property points to Object.prototype
      ```
      </details>
      
      <details>
      <summary>Using Constructor function</summary>

      ```
      //Constructor function declaration
       function Employee() {
          this.name = 'Prashant';
          this.dept = 'general';
          this.getDepartment=function (){
            return this.dept;
          }
        // this does not Add function to object,
        // As it is not tied to any property and it will treated like nested function  
          function getDepartment2(){
            return this.dept + 2
          }
      }
      // We are assigning function to prototype and function will be accessible to all object instances.
      Employee.prototype.getName=function(){
          return this.name;
      }

    //Object initialisation  using constructor function 
    let emp =new Employee()
      In this case emp object __proto__ property points to Employee.prototype
      ```
      </details>
2.Inheritance using es5

  <details>
      <summary>Using constructor function</summary>
      ```
      //base object
        function Employee() {
          this.name = 'Prashant';
          this.dept = 'general';
          this.getDepartment=function (){
            return this.dept;
         }
       }
      Employee.prototype.getName=function(){
        return this.name;
      }
  
    //derived object  
    function Manager() {
      Employee.call(this);
      this.reports = [];
    }
    Manager.prototype = Object.create(Employee.prototype);
    Manager.prototype.constructor = Manager;

    //Object Creation
    let mng2= new Manager();
      
  ```
   </details>
  
3. Inheritance using es6
