# SpringBoot

## Application Architecture

![Untitled Diagram](https://user-images.githubusercontent.com/204423/194636202-29c31fc6-2899-44b9-8407-93c94ab52329.jpg)

## Spring MVC

![SpringResponseBodyAnnotation](https://user-images.githubusercontent.com/204423/194721555-60729dee-0e51-426e-8e91-ad42fb78843f.jpg)

### `@Controller` Annotation

- In Spring MVC, any class which has the annotation `@Controller` can handle HTTP requests.

```
import org.springframework.stereotype.Controller;

@Controller
public class Employee {
}
```


### `@ResponseBody` annotation.

- You map methods inside your controller to URI using `RequestMapping` annotation and also put `@ResponseBody` annotation.
- The `@ResponseBody` annotation tells a controller that the object returned is automatically serialized into JSON and passed back into the HttpResponse object.


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

### `@RestController` annotation

- `@RestController` annotation combination of the `@Controller` and `@ResponseBody` annotation. 

```
@RestController
public class Employee {

    @RequestMapping(value = "/employee", method = RequestMethod.GET)
    public String hello() {
        return "Hello World!!";
    }
}
```

### @RequestMapping Annotation

1 - **`@RequestMapping` with Class:** We can use it with class definition to create the base URI.

```
@Controller
@RequestMapping("/home")
public class HomeController {

}
```

- Now `/home` is the URI for which this controller will be used.


2 = **`@RequestMapping` with Method:** We can use it with method to provide the URI pattern for which handler method will be used.

```
@RequestMapping(value="/method0")
@ResponseBody
public String method0(){
	return "method0";
}
```

3 - **`@RequestMapping` with Multiple URI:** We can use a single method for handling multiple URIs.

```
@RequestMapping(value={"/method1","/method1/second"})
@ResponseBody
public String method1(){
	return "method1";
}
```

4 - **`@RequestMapping` with HTTP Method:** Sometimes we want to perform different operations based on the HTTP method used, even though request URI remains same.

```
@RequestMapping(value="/method2", method=RequestMethod.POST)
@ResponseBody
public String method2(){
	return "method2";
}
	
@RequestMapping(value="/method3", method={RequestMethod.POST,RequestMethod.GET})
@ResponseBody
public String method3(){
	return "method3";
}
```

5 - **`@RequestMapping` with Headers:** We can specify the headers that should be present to invoke the handler method.

```
@RequestMapping(value="/method4", headers="name=pankaj")
@ResponseBody
public String method4(){
	return "method4";
}
	
@RequestMapping(value="/method5", headers={"name=pankaj", "id=1"})
@ResponseBody
public String method5(){
	return "method5";
}
```

6 - **`@RequestMapping` with Produces and Consumes:** We can use header `Content-Type` and `Accept` to find out request contents and what is the mime message it wants in response. For clarity, `@RequestMapping` provides `produces and consumes` variables where we can specify the `request content-type` for which method will be invoked and the `response content type`. 

```
@RequestMapping(value="/method6", produces={"application/json","application/xml"}, consumes="text/html")
@ResponseBody
public String method6(){
	return "method6";
}
```

# Reference

- https://spring.io/projects/spring-boot
- https://start.spring.io/
- https://www.tutorialspoint.com/spring_boot/index.htm
- https://www.tutorialspoint.com/jackson/jackson_overview.htm
