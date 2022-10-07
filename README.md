# SpringBoot

## Application Architecture


## Spring MVC

- In Spring MVC, any class which has the annotation `@Controller` can handle HTTP requests.

```
import org.springframework.stereotype.Controller;

@Controller
public class Employee {
}
```

- You map methods inside your controller to URI using `RequestMapping` annotation and also put `@ResponseBody` annotation.


```
@Controller
public class Employee {

    @RequestMapping(value = "/employee", method = RequestMethod.GET)
    @ResponseBody
    public String hello() {
        return "Hello World!!";
    }
}
```





# Reference

- https://spring.io/projects/spring-boot
- https://start.spring.io/
- https://www.tutorialspoint.com/spring_boot/index.htm
- https://www.tutorialspoint.com/jackson/jackson_overview.htm
