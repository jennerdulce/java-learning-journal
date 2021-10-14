
## build.gradle

- Use Spring Initializr to implement all dependencies\

## Login
Form
  - Head
  - Username
  - Password
  - submit
  - action /login
  - method post
    - Creating a session

## Controller

Post
- @Contoller
- @PostMapping
- @Autowired
  - SomeRepository somerepository;
- RedirectView loginUser(Model m, String username, String password)
  - Redirects without resubmitting
  - Can redirect to a root for more processing
  - Returning a string only renders a html page
  - Create new obj
  - Create new obj with arguments
  - save to repository
  - Redirect to index

Get
- @Controller
- @GetMapping
- return home

## Repositories

- interface extends JpaRepository<ChatUser, long>
- Within controller
  - @Autowired
  - SomeRepository somerepository;

## Model

- @Entity above class
- @Id
- @GeneratedValue(strategy = GenerationType.AUTO)
- Create constructor without ID
- Create default constructor

## Pages

- Login page
  - Get: Login
  - Post: Login
- Signup
  - Get: Signup
    - Hash password here before you store password
    - Directs to Login
  - Post: Signup
- Login Page
- Index page

## General Notes

- I am starting to understand how Java is working. I think its pretty interesting how learning all works. At first its a little uneasy and scary. A few days pass and then it just sort of clicks and now I know what I am doing (partially). I realize to trust the process and don't worry too much about some magic that goes behind the scenes. It's important to know the concept more than anything.
- Bcrypt and salting passwords is pretty interesting as well. I really thank the developers that came before me to pave the way for us. I can't imagine how coding was back then and I wonder what the veteran devs think of the industry now. I am so priviledged to not have to put up with the nuainces that early developing had to offer