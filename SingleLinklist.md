1.SinglyLinklist and its few operations

```
function Node(data){
     this.data=data;
    this.next=null;
}


class SinglyLinkList{
    
    constructor(){
       this.head =null;
    }


    printAllNodes(){
        let node=this.head
        while(node.next){
            console.log(node.data);
            node=node.next;
        }
    }

    addNodLast(data){
        if(!this.head){
            this.head= new Node(data);
        }else{
            let node;
            node =this.head
            while(node.next){
                node = node.next;
            }
            node.next= new Node(data);
        }
        
    }
}


list=new SinglyLinkList();
list.addNodLast(10);
list.addNodLast(20);
list.addNodLast(30);


list.printAllNodes();
```
