
# CRUD Operations:
CRUD operations are fundamental in software development and database management, serving as a foundation for various applications and systems involving data manipulation. CRUD is an acronym that stands for Create, Read, Update, and Delete.

## Create (C):
This operation involves the creation of new data records or objects in a database. It typically involves inserting new data into a database table or adding new resources in an application.

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```
### Read (R)

The "Read" operation is about retrieving and reading data from a database or resource. It allows you to access and view existing data without modifying it. In database terms, this is often done through queries, and in software applications, it's akin to reading information from a file or an API.
Example (SQL):
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
### Update (U)

This operation is used to modify or update existing data. You can use it to change the attributes or properties of an object or to update records in a database table. It is typically used to keep data up to date.
 Example (SQL):
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
### Delete (D)

The "Delete" operation involves removing data or objects from a database or application. It's used when you want to eliminate unnecessary or outdated information.
Example (SQL):
```sql
DELETE FROM table_name
WHERE condition;
```

*Requirements*:

Maven 3.0+, IDE (Eclipse or IntelliJ), JDK 1.8+, database (MySql database), Postman for testing.
Dependencies: Add “Spring Web,” “Spring Data JPA,” and “H2” (in-memory database for this example)


### Step 1:

In the project, go to application.yml file or application.properties configure database settings.

```
spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=mydb
spring.datasource.username=user
spring.datasource.password=123456
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
<!-- spring.jpa.database-platform=org.hibernate.dialect.SQLServer2012Dialect -->
```
### Step 2: Define the Model
Create model classes to represent essential entities like User and Account.

``` java
// User

@Entity
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Table(name="USER_DETAILS")
public class User {
@Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    @NotBlank
    private String username;
    @NotBlank
    private String password;
    private String email;
    private String name;
}

// Account

@Entity
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Table(name="ACCOUNT")
public class Account {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private BigInteger id;
    @NotNull
    private Long userId;
    private double balance;
}
```

### Step 3: Create Repositories

Create JPA repositories for the User and Account entities. Spring Data JPA will provide default CRUD methods for these repositories:

``` java
// User Repository
import org.springframework.data.jpa.repository.JpaRepository;
public interface UserRepository extends JpaRepository<User, Long> {
    User findByUsername(String username);
}

// Account Repository
import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;
public interface AccountRepository extends JpaRepository<Account, Long> {
    List<Account> findByUserId(Long userId);
}
```

### Step 4: Create Controllers

Implement controllers for user creation, account creation, and other CRUD operations.

``` java 
// Controller To Perform CRUD Operations Related To User
@RestController
@RequestMapping("/api/users")
@RequiredArgsConstructor
public class UserController {

    private final UserService userService;

    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }


    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }


    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User updatedUser) {
        return userService.updateUserDetails(id, updatedUser);
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
    }
}
```
In the above UserController, we will perform the following CRUD operations:

The `getAllUsers`: method uses a GET request to retrieve a list of all users.

The `getUserById` method retrieves a user by their unique id.

The `createUser` method uses a POST request to create a new user.

The `updateUser` method uses a PUT request to update an existing user's details.

The `deleteUser` method uses a DELETE request to delete a user by their id.

``` java
// Controller To Perform CRUD Operations Related To Account Of An User

@RestController
@RequestMapping("/api/accounts")
public class AccountController {

    private final AccountService accountService;

    @Autowired
    public AccountController(AccountService accountService) {
        this.accountService = accountService;
    }

    @GetMapping("/{userId}")
    public List<Account> getUserAccounts(@PathVariable Long userId) {
        return accountService.getUserAccounts(userId);
    }

    @PostMapping
    public Account createAccount(@RequestBody Account account) {
        return accountService.createAccount(account);
    }

    @GetMapping("/{accountId}")
    public Account getAccountById(@PathVariable Long accountId) {
        return accountService.getAccountById(accountId);
    }

    @PutMapping("/{accountId}")
    public Account updateAccount(@PathVariable Long accountId, @RequestBody Account updatedAccount) {
        return accountService.updateAccountDetails(accountId, updatedAccount);
    }

    @DeleteMapping("/{accountId}")
    public void deleteAccount(@PathVariable Long accountId) {
        accountService.deleteAccount(accountId);
    }
}
```
In this AccountController, we will perform the following CRUD operations:

The `getUserAccounts` method retrieves a list of accounts associated with a user, given the userId.

The `createAccount` method allows creating a new account for an user.

The `getAccountById` method retrieves an account by its unique accountId.

The `updateAccount` method is used to update account details.

The `deleteAccount` method allows deleting an account by its unique accountId.

### Step 5: Run And Test Spring Boot CRUD API

- mvn spring-boot:run -->  to run the program i.e start the application

We can use tools like Postman or cURL to test the application. Ensure you have proper authentication and authorization mechanisms in place to protect sensitive data.
**1.Create User:**
Create a user with the below request:
``` json
{
    "username": "reetesh",
    "password": "password123",
    "email": "reet.test@test.com",
    "name": "Spring Boot Crud Demo"
}
```



## CURL :
CLient URL Request Library.
it allows to Sends data over URLs using terminal.

So in hacking, its very useful i.e you can transefer anyfiles.

**cURL (Client for URLs):**

cURL is a command-line tool and library for transferring data with URLs. It supports a wide range of protocols, including HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, LDAPS, and more. cURL is widely used in scripting and programming to make HTTP requests and interact with various APIs.

**Key Features:**

1. **URL Formatting:** cURL allows users to specify URLs to fetch and can handle different protocols.

2. **HTTP Methods:** It supports various HTTP methods like GET, POST, PUT, DELETE, etc., enabling users to perform different actions on web resources.

3. **Data Transfer:** cURL can be used to upload or download data to or from a server. It supports various data transfer methods.

4. **Authentication:** Supports user authentication through various methods, including basic, digest, and OAuth.

5. **Headers:** Users can customize HTTP headers for requests, allowing for more control over the request and response.

6. **Cookies:** cURL can handle cookies, making it useful for sessions and maintaining state during multiple requests.

7. **Proxy Support:** It supports making requests through proxies, allowing for additional privacy and security.

**Common Use Cases:**

1. **API Requests:** cURL is widely used to make HTTP requests to APIs, retrieve data, and interact with web services.

2. **Testing Web Services:** Developers use cURL to test and debug web services and APIs from the command line.

3. **Downloading Files:** It's often used for downloading files from the internet directly to the local machine.

4. **Automation:** cURL is frequently incorporated into scripts and automation workflows to perform tasks like data extraction or periodic data retrieval.

**Examples:**

- **Simple GET Request:**
  ```bash
  curl https://example.com
  ```

- **POST Request with Data:**
  ```bash
  curl -X POST -d "param1=value1&param2=value2" https://api.example.com/resource
  ```

- **Download File:**
  ```bash
  curl -O https://example.com/file.zip
  ```

