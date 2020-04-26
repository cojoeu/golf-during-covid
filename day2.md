# Challenge 2 (11/04/2020)

Given a list of elements, a surpasser of an element 
is an element on its right hand side that is larger
than it. The surpasser count of an element is the
number of its surpassers. Return the maximum surpasser
count of a list.

## Premises

* List of elements may occupy max memory size;
* The set of elements are any a poset (orderable);
  
## Examples

```
msc of G,E,N,E,R,A,T,I,N,G is 6
msc of 10,3,4,5,2 is 2
```

## Solutions

### (18) APL by Hugo
```apl
msc←{⌈/+/¨⍵<⊖,\⊖⍵}
```

### (42) APL by Hugo
```apl
msc←{1>⍴⍵:0⋄H←(1↑⍵)⋄(+/{H<⍵}¨(1↓⍵))⌈∇(1↓⍵)}
```

### (42) Haskell by Restivo

```haskell
msc[]=0;msc(h:t)=sum[1|y<-t,y>h]`max`msc t
```

### (43) Haskell by André Silva

```haskell
msc[]=0;msc(h:t)=max(sum[1|x<-t,h<x])$msc t
```

### (43) Haskell by Hugo
```haskell
msc l=maximum[sum[1|x<-t,x>h]|h:t<-tails l]
```

### (50) Haskell by Hugo

```haskell
msc=maximum.ap(zipWith((length.).filter.(<)))tails
```

### (57) Julia by Ferrolho

```julia
msc(x)=maximum(count(>(x[i]),x[i:end]) for i=1:length(x))
```

### (73) Python by António

```python
msc=lambda l: max([sorted(l[i:])[::-1].index(e) for i,e in enumerate(l)])
```

### (76) Python by Mafalda

```python
msc=lambda l:max([len([x for x in l[e:] if x>l[e]]) for e in range(len(l))])
```

### (79) Haskell by Mafalda

```haskell
msc l=maximum(map length(groupBy(==)[x|x<-[0..length l-1],y<-drop x l,y>l!!x]))
```

### (100 😢) Swift by Tiago

```swift
func msc<T:Comparable>(_ l:[T]){l.enumerated().map{i,e in l.dropFirst(i).filter{e<$0}.count}.max()!}
```

Either by ignorance or by Swift type system, in order to work with Array of Arrays we need to teach Swift how we want to compare those arrays. 

```swift
extension Array: Comparable where Element: Comparable {
    public static func < (lhs: [Element], rhs: [Element]) -> Bool {
        return lhs.count < rhs.count
    }
}
```
