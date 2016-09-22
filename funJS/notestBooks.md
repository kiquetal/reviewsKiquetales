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
    
### Big problem with global scope

    Any objects and variables declared in the outermost level of a script (not contained in any function) are
    part of the *global* scope and accesible from all Javascript code.
    
## Chapter III

*Computaional processes are abstract beings that inhabit computers.
 As the evolve, processes manipulate other abstract things called data.*
 
 
### Method chaining

OOP pattern that allows multiple methods to be called in a single statement.

### Function chaining

*Java,for instance has an explosion of concrete List classes for each need*

    Functional programming takes a different approach. Instead of creating new data structure
    classes to meet specific needs, it uses common ones like arrays and applies a number
    of coarse-grained, high-order operations that are agnostic to the underlying representation
    of the data. These operations are designated to do the follogin:
    
    ..- Accept function arguments in order to inject specialized behavior that solves your
    particular task
    
    ..- Replace the traditional, manual looping mechanism that contain mutation of temporary 
    variables and side effects, thereby creating less code to maintain and fewer places where 
    error can occur.
    
    Lambda expressions uphold the functional definition of a function because they encourage
    you to always return a value. In fact, for one-line expressions, the return value results from 
    the value of the function body.
    
##### Reduce
 
    Is a high order function that compresses an array of elements down to a single value.The
    value is computed from the accumulated result of invoking a function with an accumulator
    value against each element.
    
 
 
## Chapter IV

*A complex system that works is invaribly found to have evolved from a system that worked.*

### Requirements for compatible functions

    OO programmers use pipelines sporadically, in specific scenarios, on the other hand, functional
    programming relies on pipelines as the sole method of building programs. Depending on the task
    at hand, there's usually quite a gap between a problem definition and a proposed stages are
    represented by functions that execute with the condition that their inputs and outputs be 
    compatible in two ways:
    
  * Type
        The type returned by one function must match the argument type of a receiving function.
        
  * Arity
        A receiving function must declare at least one parameter in order to handle the value
        returned from a preceding function call.
        
#### Definitions
  
    Formally speaking, two functions f and g are type-compatible if the output of *f* has a
    type equivalent to the set of inputs of g.
    Arity can be defined as the number of arguments a function accepts, it's also referred to as the
    function's length.
     
    Tuple finite, orderd list of elements, usually grouping two or three values at a time, and
    written(a,b,c)
    
    Currying is a technique that converts a multivariable function into a stepwise sequence
    of unary functions by suspending or 'procrastinating' its execution until all arguments
    have been provided, which could happen later.
     
   It's useful when
   * Emulating function interfacces.
   
   * Implementing reusable, modular functions templates.
   
#### Differences between Partials and currying

     Currying generates nested unary functions at each partial invocation. Internally, the final
     result is generated from the step-wise composition of these unary functions. Also, variations
     of curry allow you to partially evaluate a number of arguments;therefore, it gives you
     complete control over when and how evalution take place.
     
     Partial application binds a function's arguments to predefined values and generates a new
     function of fewer arguments. The resulting function contains the fixed parameters in its 
     closure and is completely evaluated on the subsequent call.
     
    
    function filter(arr, predicate)
{

    let idx=-1,
    len=arr.length;
     result=[];
     while(++idx<len)
     {
         let value=arr[idx];
         if(predicate(value,idx,this)){
         result.push(value);
         }
     
     }
    return result;

}

    Tuples offer more advantages:
        
        Inmutable
        Once created you can't change a tuple's internal contents.
        Avoid creating ad hoc types.
        Tuples can relatae values that may have no relationship at all
        to each other. So defining and instantiating new types solely
        for grouping data together makes your model unnecesarily convoluted.
        Avoid creating heterogenous arrays
        Working with arrays contining different types of elements is hard
        because it leads to writting code filled with lots of defensive type checks
        Traditionally, arrays are meant to store objects of the same type.
        
        
    So unlike currying, calling consoleLog with just one argument won't return a new function
    and will instead evaluate with the last one set to undefined.But you can continue 
    applying partial arguments to consoleLog by using _partial again.
     
    Example partial
    
    String.prototype.first=_.partial(String.prototype.substring,0,_);
    'Functional Programming'.first(3);
    
    const Scheduler=(function(){
        const delayedFn=_.bind(setTiemout,undefined,_,_)
        
        return{
        delay5:_.partial(delayedFn,_,5000),
        delay10:_.partial(dellayedFn,_,10000)
        }
    
    })();
    
    Scheduler.delay5(function(){
      console.log('Executing After 5 seconds');
    });
    

    Functional composition: separating description from evaluation.
    
    Functional composition is a process used to group together complex behavior that has been
    broken into simpler tasks. I defined it briefly in chapter I, and now I'll explain it in detail.
    Let's go over a quick example that uses Rambda's R.compose to combine two pure functions:
    
    const str='We can only see a short distance ahead but we can see plenty there
    that needs to be done';
    cons explode=(str)=>str.split(/\s+/);
    const count=(arr)=>arr.length;
    
    const countWords=R.compose(count,explode);
    
    countWords(str);
    
    The result of composition is another function that waits to be called
    with its respective argument: the argument to countWords.
    Separating a function's description from its evaluation.
    
    Using compose
    
    const trim = (str) => str.replace(/^\s*|\s*$/g,'')
    const normalize=(str)=>str.replace(/\-/g,'');
    const validateLength=(param,str)=>str.length==param;
    const checkLengthSsn=_.partial(validLenght,9);
    
    const cleanInput=R.compose(normalize,trim);
    const isValidSSn=R.compose(checkLengthSsn,cleanInput);
    
    `Entire program can be built from the combination of other side effect-free, pure program or modules`
    
    
    
     
