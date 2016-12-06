## Chapter II Persistence

    Persistence is achieved by copying the affected nodes of a data structure
    and making all changes in the copy rather that in the original.
    Because nodes are never modified directly, all nodes that are unaffected by an
    update can be shared between the old and new versions of the data structure without
    worrying that a change in one version will inadvertently be visible to the other,
    
    
### Lists

    In functional setting we cannot destructively modify the last cell of the first
    in this way.Instead we copy the cell and modify the tail pointer of the last cell
    We continue in this fashion until we have copied the entire list
    
    fun xs++ys=if isEmpty xs then ys else cons(head xs,tail xs++ ys)
    
    
    -> [0|x]-> [1|x] - > [2|x]  ==xs
    
    -> [3|x]->[7|x] ==  ys
    
    xs ++ ys
    
    ->[0|x] -> [1|x] -> [2|x] ---> [3|x]->[7|x]
    
`
    fun update([],i,y)
    = (update x::xs,0,y)=y::xs
    | (update x:xs,i,y)=x::update(xs,i-1,y) 
`
 
    Here we do not copy the entire argument list. Rather we copy only the node to be modified
    (node i) and all those nodes that contain direct or indirect pointer to a node i.
    In other words, to modifya single node, we copy all the nodes on the path from the root
    to the node in question.
    All nodes that are not on this path are shared between the original version and the updated
    version.
