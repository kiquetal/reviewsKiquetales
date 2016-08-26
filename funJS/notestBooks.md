# Chapter I

    OO makes code understandable by encapsulating moving parts.
    FP makes code understandable by minimizing moving parts.

## Concepts 

* Declarative programming
* Pure functions
* Referential transparency
* Inmutability.
    
    
*Declarative programming*

    It's a paradigm that express a set of operations without revealing how they're
    implemented or how data flows through them.
    Imperative programming treats a computer program as merely a sequence of top-to-bottom
    statements that changes the state of the system in order to compute a result.
    


*Pure functions*

    It depends only on the input provided and not on any hidden or external state
    that may change during its evaluation or between calls.
    
    It doesn't inflict changes beyond their scopes, such as modifiying a global object or a 
    parameter passed by reference.
    
    
*Referential transparency*

    Is a more formal way of defining a pure function. If a function consistently yields the same
    result on the same input, it's said to be referentially transparent.
    
*Inmutability*

    The object never changes when it's assigned.

## Chapter II

    The state of a program can be defined as a snapshot of the data stored in all of its objects at 
    any moment in the future
    
    Lenses also known as functional interfaces, are functional programming's solution to accesing and 
    immutably manipulating attributes of stateful data types.

### Examples Lens

    var person=new Person('Alonso','Church','4434343');
    var lastnamelens=R.lenseProp('lastname');
    
    R.view(lastnameLens,person);
    
    var new Person=R.set(lastnameLens,'Mourning',person);
    
    newPerson.lastname;
    person.lastname;
    
      
### CopyOnWrite Strategy

    Utilizing the "copy on write strategy".
    Preserving the original instance.
    

### Call vs Apply

    Call vs Apply
    Call accepts an argument list, and apply accepts array.
    
    
