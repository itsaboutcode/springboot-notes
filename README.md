# SpringBoot

## Application Architecture

![Untitled Diagram](https://user-images.githubusercontent.com/204423/194636202-29c31fc6-2899-44b9-8407-93c94ab52329.jpg)

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
