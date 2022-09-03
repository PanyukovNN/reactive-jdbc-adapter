# reactive-jdbc-adapter

Simple reactive adapter for CrudRepository

### How to use adapter

1. Declare CrudRepository:
```java
@Repository
public interface BookRepository extends CurdRepository<Book, String> {
}
```

2. 
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
Do not use Transactions and Lazy initialization, because it may cause unexpected behavior of your program.

### How to add dependency (example with Gradle):
```
repositories {
    maven {
        url = uri("https://raw.githubusercontent.com/PanyukovNN/reactive-jdbc-adapter/master/mvn-artifact/repository")
    }
}

dependencies {
    implementation "org.panyukovnn:reactive-jdbc-adapter:1.0.0"
}
```