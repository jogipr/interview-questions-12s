1. Write your own implementation for JSON.stringyfy .
   Input to function

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
 }]
};
```

Implementation

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

2. Write the polyfill for filter method of Array
   //Solution

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

3. Write Polyfill for flat method of an Array

Solution :
Implementation using normal function

```
const input =[ "one", "two",["three","four",["five","six"]]];

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

//Implementation Polyfill function

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
