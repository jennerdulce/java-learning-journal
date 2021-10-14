# title

- Automatic login helper method
- HTTPServelet method

```java
    @Autowired
    private HttpServletRequest request;

   @PostMapping("/signup")
    public RedirectView createUser(String username, String password, String nickname){
        SomeUser newUser = new SomeUser();
        newUser.setUsername(username);
        newUser.setNickname(nickname);
        String hashedPassword = passwordEncoder.encode(password);
        newUser.setPassword(hashedPassword);
        userRepository.save(newUser);
        authWithHttpServlet(username, password);
        return new RedirectView("/");
    }

    public void authWithHttpServlet (String username, String password){
        try{
            request.login(username, password);
        } catch (ServletException se){
            // print out stack trace
            se.printStackTrace();
        }
    }
```

- AuthenticationManager method

## Replacing whitelabel error pages

- `server.error.whitelabel.enables=false` in application.properties
- Create new error page
- 'error.html' black magic will find it and display it

```java
    public String testPage(Principal p, Model m){
        throw new RuntimeException("TESTING THIS IS THE NEW PASSED ERROR");
    }

<span th:if="${exception}" th:text="${message}"></span>
```

- Reusable templates
- Create Fragements
- html file

```java
<h3 th:if="${username}" th:text="'Current User: ' + ${username}"></h3>
<!--Reference fragment from another html page-->
<nav th:Fragment="dino-header"></nav>
```

- import into where you want in other html doc

```java
<!--    th:insert goes into the tag-->
    <div th:insert="/fragments/navheader :: h3"></div>
    <div th:replace="/fragments/navheader :: dino-header"></div>
```



- How to handle duplicate accounts
- Error handling
- Flash Attributes
- retrieve short lifecycle attribute
- Persists through redirects; use instead of model.setAttribute

```java
  @PostMapping("/signup")
    public RedirectView createUser(RedirectAttributes ra, String username, String firstName, String lastName,  String bio, String password){
        ApplicationUser existingUser = applicationUserRepository.findByUsername(username);
        // Handles duplicate accounts
        if(existingUser != null){
            ra.addFlashAttribute("errorMessage", "That username is already taken please choose another name..");
            return new RedirectView("/signup");
        }
        String hashedPassword = passwordEncoder.encode(password);
        ApplicationUser newUser = new ApplicationUser(username, firstName, lastName, bio, hashedPassword);
        applicationUserRepository.save(newUser);
        authWithHttpServlet(username, password);
        return new RedirectView("/");
    }
```

- `RedirectAttributes ra`
- `ra.addFlashAttribute("varName", "String")`
- Can be pulled imported to the document exactly the same as the model. ${}
