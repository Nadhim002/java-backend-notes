### @SprintBootApplication in composed of the Following annotations

@ComponentScan - Enables component scan of current packages and all sub packages recursively

To tell sprint search components in other packages we can add 

```Java
@SpringBootApplication(scanBasePackages = {"com.mycompany.myapp", "com.external.library"})
public class SpringcoreApplication {
}
```

@EnableAutoConfiguration - Enable sprint boot auto configuration support

@Configuration - Able to register extra bean with @Bean or import other config classes

<!-- ************************************************************** -->

### Constructor injection 

- It is the default choice for required dependencies.
- The field can be final, which makes the object immutable.


### Setter injection

- It is for optional or changeable dependencies. If the bean has a sensible default and the setter only overrides it, the setter fits. 
- It can break circular dependencies, b
- Its drawbacks are that the field can't be final, and the object can sit half-initialized if the setter is never called.ecause the object can be created first and wired afterward. Constructor injection fails on a cycle.


### Field Injection

- Harder to unit test
- No need for constructer or setters

```Java
@Autowired
private Coach coach ;
```

### Qualifiers , Autowired


Use qualifier when you want use particular bean instead of primary one 

```Java
@Autowired
void setCoach(@Qualifier("footBallCoach") Coach coach){
    myCoach = coach ;
}
```

Use @Primary to have defualt bean when mutiple bean implements the same interface

```Java
@Component
@Primary
public class CricketCoach implements Coach{
    @Override
    public String getDailyWorkout(){
        return "Enjoy the Day Dumb!!!!!" ;
    }
}
```

Lazy Initialisation 

Set this in properties file when want lazy initialisation for all the beans in our project 

```Javascript
spring.main.lazy-initialisation=true
```

Use @Lazy when we want create bean only when needed
```Java
@Lazy
@Component
public class LazyComponent implements Component{
 ...
}
```

Pros 

- Maybe less startup time if u have larger number of components
- Only create as needed

Cons 

- May not discover conig issue upfront
- Need to make sure we have memory for all components