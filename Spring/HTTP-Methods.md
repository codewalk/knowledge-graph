### Key Attributes of HTTP Methods: GET, PUT, POST, and DELETE

The Hypertext Transfer Protocol (HTTP) is a fundamental protocol used for communication on the World Wide Web. It defines a set of request methods to indicate the desired action to be performed on a resource. Here are the key attributes of the commonly used HTTP methods: GET, PUT, POST, and DELETE.

#### **1. GET Method:**

- **Purpose:** The GET method requests data from a specified resource.
  
- **Idempotent:** Yes. Repeating the same GET request multiple times produces the same result. It does not have any side effects.

- **Data in Request:** Typically, no request body. Parameters are included in the URL.

- **Safe:** Yes. It should not change the state of the server.

- **Example:**
  ```http
  GET /api/users?id=123
  ```

#### **2. PUT Method:**

- **Purpose:** The PUT method updates a resource or creates a new resource if it does not exist at the specified URL.

- **Idempotent:** Yes. Repeating the same PUT request multiple times has the same effect.

- **Data in Request:** The request typically includes the full representation of the resource.

- **Safe:** No. It modifies the state of the server.

- **Example:**
  ```http
  PUT /api/users/123
  Content-Type: application/json

  {
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
  ```

#### **3. POST Method:**

- **Purpose:** The POST method is used to submit data to be processed to a specified resource.

- **Idempotent:** No. Repeating the same POST request may have different effects each time.

- **Data in Request:** The request typically includes data to be processed.

- **Safe:** No. It may modify the state of the server.

- **Example:**
  ```http
  POST /api/users
  Content-Type: application/json

  {
    "name": "Jane Doe",
    "email": "jane.doe@example.com"
  }
  ```

#### **4. DELETE Method:**

- **Purpose:** The DELETE method requests the removal of a resource at a specified URL.

- **Idempotent:** Yes. Repeating the same DELETE request multiple times has the same effect.

- **Data in Request:** Typically, no request body. The resource to be deleted is identified in the URL.

- **Safe:** No. It modifies the state of the server.

- **Example:**
  ```http
  DELETE /api/users/123
  ```

### Differences:

- **State Modification:**
  - **GET:** Does not modify the state of the server.
  - **PUT:** Modifies or creates a resource.
  - **POST:** Submits data for processing.
  - **DELETE:** Removes a resource.

- **Idempotence:**
  - **GET:** Idempotent.
  - **PUT:** Idempotent.
  - **POST:** Not idempotent.
  - **DELETE:** Idempotent.

- **Data Handling:**
  - **GET:** Parameters in the URL. No request body.
  - **PUT:** Includes the full representation of the resource in the request body.
  - **POST:** Includes data to be processed in the request body.
  - **DELETE:** Typically no request body.

- **Safety:**
  - **GET:** Safe.
  - **PUT:** Not safe.
  - **POST:** Not safe.
  - **DELETE:** Not safe.

Understanding these attributes helps in selecting the appropriate HTTP method based on the desired action and the characteristics of the operation.
