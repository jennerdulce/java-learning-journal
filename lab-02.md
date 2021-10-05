# Arrays, for loops, testing

## Today I learned how to create a libaray

- By doing gradle init we are able to create a Java library

## Testing

- Testing was fairly simple although these are very basic tests. 
- I was getting errors from my tests, I believe it is because I need to create a BeforeEach statement of some sort to reset my `Library systemUnderTest = new Library()` before each test.

## Array of Arrays

- were kind of annoying, but I think I understand them. 
- Kind of curious of how to have an array of ArrayLists
- Would it be something like int[]ArrayList<Integer> ? Need to know what I can and cannot do.

## Something that was extra annoying was declaring variables.

- Apparently you cannot declare an array and overwrite it at a later time within a function.

`int[] lowestArr;` 
- I set this at the beginning of my method and tried to assign it within a for loop and 
it was saying "It may not have been declared yet" or something like that.. 
- What fixed it was actually setting the array variable to a bs array something like 
`in[] lowestArr = new int[5]` now that the array had been created, 
I can actually overwrite the variable with a different array

```java
public static String averageArray(int[][] arr){
        double lowestAvg = Double.POSITIVE_INFINITY;
        int[] lowestArr = new int[5];
        for(int i = 0; i < arr.length; i++){
            int[] currentArr = arr[i];
            int sum = calculateAverage(currentArr);
            if(sum < lowestAvg){
                lowestArr = arr[i];
                lowestAvg = sum;
            }
        }
        return Arrays.toString(lowestArr);
    }
 ```
