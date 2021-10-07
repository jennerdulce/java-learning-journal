# Something

## mockMVC

```java
@Aytowired
MockMvc mockMvc;

public void Test_salmon_cookie_app(){
  mockMvc.perform(get("/"))
    .andDo(print()) // shows output for debugging
    .andExpect(content())
}

```

- Perform action "get"
- We check to see if "get" does what we thought it was supposed to do
- Expect