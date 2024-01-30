### Versioning in Spring REST

Versioning in Spring REST allows you to manage different versions of your RESTful APIs. There are several approaches to achieve versioning, and one commonly used method is through URI and Request Headers. Let's explore both approaches.

#### **1. URI Versioning:**

In URI versioning, the version information is included in the URI path.

##### **Example:**

Suppose you have a resource representing users, and you want to introduce a new version of your API. You might have the following URIs:

- **Version 1:**
  ```http
  /api/v1/users
  ```

- **Version 2:**
  ```http
  /api/v2/users
  ```

##### **Implementation:**

In Spring, you can achieve URI versioning using `@RequestMapping` or `@GetMapping` annotations.

```java
@RestController
@RequestMapping("/api/v1/users")
public class UserControllerV1 {
    // Controller logic for version 1
}
```

```java
@RestController
@RequestMapping("/api/v2/users")
public class UserControllerV2 {
    // Controller logic for version 2
}
```

#### **2. Request Headers Versioning:**

In request headers versioning, the version information is passed in the headers of the HTTP request.

##### **Example:**

- **Version 1:**
  ```http
  GET /api/users
  Host: example.com
  Accept: application/vnd.company.v1+json
  ```

- **Version 2:**
  ```http
  GET /api/users
  Host: example.com
  Accept: application/vnd.company.v2+json
  ```

##### **Implementation:**

In Spring, you can use the `produces` attribute of `@RequestMapping` or `@GetMapping` to specify the media type.

```java
@RestController
@RequestMapping(value = "/api/users", produces = "application/vnd.company.v1+json")
public class UserControllerV1 {
    // Controller logic for version 1
}
```

```java
@RestController
@RequestMapping(value = "/api/users", produces = "application/vnd.company.v2+json")
public class UserControllerV2 {
    // Controller logic for version 2
}
```

#### **3. Other Approaches:**

- **Request Parameter Versioning:** Include version information as a request parameter.
- **Media Type Versioning:** Use different media types for different versions.

##### **Example (Request Parameter Versioning):**

```http
GET /api/users?version=1
```

##### **Implementation:**

```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    @GetMapping(params = "version=1")
    public ResponseEntity<String> getUserV1() {
        // Logic for version 1
    }

    @GetMapping(params = "version=2")
    public ResponseEntity<String> getUserV2() {
        // Logic for version 2
    }
}
```

Choose the versioning strategy that aligns with your application's requirements and constraints. Each approach has its advantages and considerations, so make sure to evaluate them based on your project needs.
