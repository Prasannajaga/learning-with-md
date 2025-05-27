# All the Ways to Use `stream().collect()` in Java

When you use `stream().collect()`, you're transforming a stream into a collection, a value, or a custom structure.

---

# 🔥 Common Ways to Use `collect()`

## 1. Collect into a `List`
```java
List<String> names = people.stream()
                           .map(Person::getName)
                           .collect(Collectors.toList());
```

## 2. Collect into a `Set`
```java
Set<String> uniqueNames = people.stream()
                                .map(Person::getName)
                                .collect(Collectors.toSet());
```

## 3. Collect into a `Map`
```java
Map<Integer, String> idToName = people.stream()
    .collect(Collectors.toMap(
        Person::getId,
        Person::getName
    ));
```
If keys might duplicate:
```java
.collect(Collectors.toMap(
    Person::getId,
    Person::getName,
    (name1, name2) -> name1 + ", " + name2
));
```

## 4. Collect into a `String` (Joining)
```java
String allNames = people.stream()
                        .map(Person::getName)
                        .collect(Collectors.joining(", "));
```
Joining with prefix/suffix:
```java
.collect(Collectors.joining(", ", "[", "]"))
```
Gives output like: `[John, Jane, Jack]`

## 5. Grouping (groupingBy)
```java
Map<String, List<Person>> peopleByCity = people.stream()
    .collect(Collectors.groupingBy(Person::getCity));
```
Advanced grouping:
```java
Map<String, Long> peopleCountByCity = people.stream()
    .collect(Collectors.groupingBy(
        Person::getCity,
        Collectors.counting()
    ));
```

## 6. Partitioning (partitioningBy)
```java
Map<Boolean, List<Person>> partitioned = people.stream()
    .collect(Collectors.partitioningBy(person -> person.getAge() > 18));
```

## 7. Summarizing
```java
IntSummaryStatistics stats = people.stream()
    .collect(Collectors.summarizingInt(Person::getAge));

System.out.println(stats.getAverage());
System.out.println(stats.getMax());
System.out.println(stats.getMin());
```

## 8. Counting
```java
long count = people.stream()
                   .collect(Collectors.counting());
```

## 9. Reducing
```java
Optional<String> combinedNames = people.stream()
    .map(Person::getName)
    .collect(Collectors.reducing((name1, name2) -> name1 + " & " + name2));
```

---

# 🛡️ Bonus: Custom Collector
```java
Collector<String, ?, TreeSet<String>> toTreeSet() {
    return Collector.of(TreeSet::new, TreeSet::add, (left, right) -> { left.addAll(right); return left; });
}
```
Usage:
```java
TreeSet<String> names = people.stream()
                              .map(Person::getName)
                              .collect(toTreeSet());
```

---

# 💪 TL;DR Summary
| Use Case | Method |
|:---------|:-------|
| List | `toList()` |
| Set | `toSet()` |
| Map | `toMap()` |
| String | `joining()` |
| Group by property | `groupingBy()` |
| Split into two groups | `partitioningBy()` |
| Stats (min, max, avg, etc.) | `summarizingInt()` |
| Count elements | `counting()` |
| Combine manually | `reducing()` |

---

# ⚡ Real-World Tip
If you are collecting and transforming heavily, sometimes it's better to use `map()` + `collect()` carefully or explore third-party libraries like Vavr or Apache Commons for more clean utilities.

---

**Want a real-world project example using ALL of these?** Let me know 🚀

