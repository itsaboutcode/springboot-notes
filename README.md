# SpringBoot

## Application Architecture

![Untitled Diagram](https://user-images.githubusercontent.com/204423/194636202-29c31fc6-2899-44b9-8407-93c94ab52329.jpg)

## [Spring MVC](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc)

![SpringResponseBodyAnnotation](https://user-images.githubusercontent.com/204423/194721555-60729dee-0e51-426e-8e91-ad42fb78843f.jpg)

### `@Controller` Annotation

- In Spring MVC, any class which has the annotation `@Controller` can handle HTTP requests.

```
import org.springframework.stereotype.Controller;

@Controller
public class Employee {
}
```

### @RequestBody Annotation

- `@RequestBody` annotation maps the `HttpRequest body` to a transfer or domain object, enabling automatic `deserialization` of the inbound `HttpRequest body` onto a Java object.
- Spring automatically deserializes the JSON into a Java type, assuming an appropriate one is specified.

```
@RequestMapping(method = RequestMethod.POST)
@ResponseBody
public HttpStatus something(@RequestBody MyModel myModel) 
{
    return HttpStatus.OK;
}
```

### @RequestBody – Map Version

```
@RestController
public class HelloController {

  @RequestMapping(path = "/v2/login", method = RequestMethod.POST)
  public boolean validateLoginMapVersion(@RequestBody Map<String, String> login) {

      if (login == null) return false;
      String username = login.get("username");
      String password = login.get("password");

      // simple check
      if ("mkyong".equalsIgnoreCase(username) && "123456".equals(password)) {
          return true;
      } else {
          return false;
      }
  }

}
```

The `@RequestBody` annotation comes with the `required` attribute that defaults to `true`.  Above all, this enforces that a request always contains body content. If not so, an exception is thrown. You can switch this to `false` if you prefer null to be passed when the body content is null.

```
@PostMapping("users")
@ResponseStatus(HttpStatus.CREATED)
public User registerUserCredential(@RequestBody User user, required=”false”)
```

### `@ResponseBody` annotation.

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


2 **`@RequestMapping` with Method:** We can use it with method to provide the URI pattern for which handler method will be used.

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

4 - **`@RequestMapping` with HTTP Method:** Sometimes we want to perform different operations based on the HTTP method used, even though request URI remains same. If you don't specify the method, method is `GET`

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

7 - **`@RequestMapping` default method:** If value is empty for a method, it works as default method for the controller class. 

```
@RequestMapping()
@ResponseBody
public String defaultMethod(){
	return "default method";
}
```

8 - **`@RequestMapping` fallback method:** We can create a fallback method for the controller class to make sure we are catching all the client requests even though there are no matching handler methods. It is useful in sending custom 404 response pages to users when there are no handler methods for the request.

```
@RequestMapping("*")
@ResponseBody
public String fallbackMethod(){
	return "fallback method";
}
```

### @PathVariable Annotation

`@RequestMapping` with `@PathVariable` annotation can be used to handle dynamic URIs where one or more of the URI value works as a parameter.



```
@RequestMapping(value="/method7/{id}")
@ResponseBody
public String method7(@PathVariable("id") int id){
	return "method7 with id="+id;
}
	
@RequestMapping(value="/method8/{id:[\\d]+}/{name}")
@ResponseBody
public String method8(@PathVariable("id") long id, @PathVariable("name") String name){
	return "method8 with id= "+id+" and name="+name;
}
```

### @RequestParam Annotation

`@RequestMapping` with `@RequestParam` for URL parameters in the request URL, mostly in `GET` requests.

```
@RequestMapping(value="/method9")
@ResponseBody
public String method9(@RequestParam("id") int id){
	return "method9 with id= "+id;
}
```

For this method to work, the parameter name should be "id" and it should be of type int. If param name and variable name are the same, you can use could remove the "id" in `@RequestParam.`

```
@RequestMapping(value="/method9")
@ResponseBody
public String method9(@RequestParam int id){
	return "method9 with id= "+id;
}
```

### @GetMapping, @PostMapping, @PutMapping, @DeleteMapping and @PatchMapping.

These mappings works exactly the same way as `@RequestMapping` except you don't have to specify the method as it's clear from the annoation name.


### @ResponseStatus Annotation

### @Value Annotation

- Spring `@Value` annotation is used to **assign default values to variables and method arguments.** We can **read spring environment variable**s as well as **system variables** using @Value annotation. Spring `@Value` annotation also supports **SpEL.**

### Spring @Value - Default Value

- We can assign default value to a class property using `@Value` annotation.

```
@Value("Default DBConfiguration")
private String defaultName;
```

### ResponseEntity class

- `ResponseEntity` represents the whole HTTP response: **status code, headers, and body**. As a result, we can use it to fully configure the HTTP response.

```
@GetMapping("/hello")
ResponseEntity<String> hello() {
    return new ResponseEntity<>("Hello World!", HttpStatus.OK);
}

// Different Status
@GetMapping("/age")
ResponseEntity<String> age(
  @RequestParam("yearOfBirth") int yearOfBirth) {
 
    if (isInFuture(yearOfBirth)) {
        return new ResponseEntity<>(
          "Year of birth cannot be in the future", 
          HttpStatus.BAD_REQUEST);
    }

    return new ResponseEntity<>(
      "Your age is " + calculateAge(yearOfBirth), 
      HttpStatus.OK);
}

// Header Example
@GetMapping("/customHeader")
ResponseEntity<String> customHeader() {
    HttpHeaders headers = new HttpHeaders();
    headers.add("Custom-Header", "foo");
        
    return new ResponseEntity<>(
      "Custom header set", headers, HttpStatus.OK);
}
```

- `ResponseEntity` provides two nested builder interfaces: **HeadersBuilder** and its subinterface, **BodyBuilder**. 

```
@GetMapping("/hello")
ResponseEntity<String> hello() {
    return ResponseEntity.ok("Hello World!");
}

@GetMapping("/age")
ResponseEntity<String> age(@RequestParam("yearOfBirth") int yearOfBirth) {
    if (isInFuture(yearOfBirth)) {
        return ResponseEntity.badRequest()
            .body("Year of birth cannot be in the future");
    }

    return ResponseEntity.status(HttpStatus.OK)
        .body("Your age is " + calculateAge(yearOfBirth));
}


@GetMapping("/customHeader")
ResponseEntity<String> customHeader() {
    return ResponseEntity.ok()
        .header("Custom-Header", "foo")
        .body("Custom header set");
}
```



# Reference

- https://spring.io/projects/spring-boot
- https://start.spring.io/
- https://projectlombok.org/
- https://www.tutorialspoint.com/spring_boot/index.htm
- https://www.tutorialspoint.com/jackson/jackson_overview.htm
- https://howtodoinjava.com/series/spring-boot-tutorial/
