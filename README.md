# reactive-jdbc-adapter

Simple reactive adapter for CrudRepository

Decorates CurdRepository methods to make them return reactive types. 

Methods processing delegates to dedicated Scheduler, which prevents reactive flow from blocking operations.

### How to use adapter

1. Declare your CrudRepository:
```java
@Repository
public interface BookRepository extends CurdRepository<Book, String> {
}
```

2. Implement adapter with
```java
@Service
public class ReactiveBookRepository extends ReactiveRepositoryAdapter<Book, String> {

    @Autowired
    public ReactiveBookRepository(Scheduler scheduler, BookRepository crudRepository) {
        super(scheduler, crudRepository);
    }
}
```

### Warning:
Do not use Transactions and Lazy initialization, because it may cause unexpected behavior.

### How to add dependency (example with Gradle):
```
repositories {
    maven {
        url = uri("https://raw.githubusercontent.com/PanyukovNN/reactive-jdbc-adapter/master/maven-repo")
    }
}

dependencies {
    implementation "org.panyukovnn:reactive-jdbc-adapter:1.0.0"
}
```