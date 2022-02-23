1.  The organizational structure of a company is provided as a tree. The tree is structured as an object keyed by employee name. The value for a given key is a list of names of people who report to that employee. The list of reports may be empty.

// Example input:
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

// Solution :
function printSuborg2(leader) {  
 let reportees = tree[leader];  
 if(reportees.length===0){  
 return leader;
}  
 reportees.forEach( rep =>{
output.push(printSuborg2( rep))
})
return leader;
}
// run function
printSuborg('Jane Mayer');
