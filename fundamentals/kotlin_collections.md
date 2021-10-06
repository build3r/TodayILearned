Kotlin

## Collections:

### List:

Initialize:

```kotlin
val list = mutableListOf(1,2,3)
```

Access:

```
list.forEach {
	element -> println(element)
}
```



### Set:

Collection of unique elements

Initialize:

```kotlin
val mSet = mutableSetOf(1,2,3)
mSet.add(4) //returns true
mSet.add(1) //returns false
```

Access:

```kotlin
 mSet.forEach {
       e -> println(e)
   }
```



### Map:

Key value pair

Initialize:

```kotlin
val mMap = mutableMapOf(1 to "x", 2 to "y", 3 to "z") //to is easy way to map element
mMap.containsKey(1) //true
mMap.getValue(2) // y
val mapWithDefault = mL.withDefault { key -> key+"x" }
val value4 = mapWithDefault.getValue(5)  //return 5x
```

Access:

```kotlin
mMap.forEach {
  k,v -> println(k,v)
}
```



### Filter:

Filter a list based on predicate

Initialize:

```kotlin
val mL = mutableListOf(1,2,3)
```

Usage:

```kotlin
mL.filter{x -> x<3 } //1,2
```



### Map:

Transform a list

Initialise:

```kotlin
val mL = mutableListOf(1,2,3)
```

Usage:

```kotlin
mL.map { x -> x*2} //2,4,6

```



### Any, All, none:

Any: check if any element matches predicate

All: Check if all element match predicate

None: no elements match predicate



### Find, FindLast

Find: returns the first element which matches predicate

FindLast: returns the last



### Count:

Counts the elements which match the predicate.

### associateBy, groupBy:

Create a map indexed by the specified key 

```kotlin
data class Person(val name: String, val city: String, val phone: String) // 1

val people = listOf(                                                     // 2
    Person("John", "Boston", "+1-888-123456"),
    Person("Sarah", "Munich", "+49-777-789123"),
    Person("Svyatoslav", "Saint-Petersburg", "+7-999-456789"),
    Person("Vasilisa", "Saint-Petersburg", "+7-999-123456"))

val phoneBook = people.associateBy { it.phone }                          // map with phone as key and person object as value
val cityBook = people.associateBy(Person::phone, Person::city)           // phone is key and city is value
val peopleCities = people.groupBy(Person::city, Person::name)  //key: city, value = list of names
```



### Partition:

Splits the list based on predicate

Returns a tuple

```kotlin
val numbers = listOf(1, -2, 3, -4, 5, -6)                // 1

val evenOdd = numbers.partition { it % 2 == 0 }           // Pair of lists
println(evenOdd)
val (positives, negatives) = numbers.partition { it > 0 } // destructured
```



### FlatMap:

transforms each element of a collection into an iterable object and  builds a single list of the transformation results. The transformation  is user-defined. 

### Sorted:

Sort list based on predicate

```kotlin
val shuffled = listOf(5, 4, 2, 1, 3, -10)                   // 1
val natural = shuffled.sorted()                             // 2
val inverted = shuffled.sortedBy { -it }                    // 3
val descending = shuffled.sortedDescending()                // 4
val descendingBy = shuffled.sortedByDescending { abs(it)  } // 5
```



### Zip

Merges two collection into a pair of elements, size = length of shortest collections

```kotlin
val A = listOf("a", "b", "c")                  // 1
val B = listOf(1, 2, 3, 4)                     // 1

val resultPairs = A zip B                      //A to B: [(a, 1), (b, 2), (c, 3)]
val resultReduce = A.zip(B) { a, b -> "$a$b" } //$A$B: [a1, b2, c3]


```



### getOrElse:

Get value or return the default specified.


Source:  
[Kotlin Playground](https://play.kotlinlang.org/byExample/05_Collections/)  
[Youtube Series](https://www.youtube.com/playlist?list=PLMZ2RODGNLRKIDSJlSVygPsi5bru4jk4g)