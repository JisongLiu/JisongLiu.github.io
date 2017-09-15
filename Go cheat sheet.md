### Basic type and variable

- Integer, String, boolean
- Assign:  x1 := x2
- Declare: ```var (x1, x2, x3) or var x1 String = "Hello World"  // the String is not necessary since the compile can
infer the type of variable directly```


### Structure control

- Switch: 
``` 
switch i {
case 0: fmt.Println("Zero")
case 1: fmt.Println("One")
case 2: fmt.Println("Two")
case 3: fmt.Println("Three")
case 4: fmt.Println("Four")
case 5: fmt.Println("Five")
default: fmt.Println("Unknown Number")
} 
```

- if else

```
if i % 2 == 0 {
  // even
} else {
  // odd
}
```

- for loop

```
for i <= 10 {
    fmt.Println(i)
    i = i + 1
  }
  ```
  
  ```
for i := 0; i < len(x); i++ {
  total += x[i]
}
  ```
  
  ```
for i, value := range x {
  total += value
}
  ```
  
  ### Integrated data structure
  
  - Array
  ```
  x := [5]float64{
  98,
  93,
  77,
  82,
  83,
}
  ```

  ```
    var x [5]int
  ```
  
  - Slice (a flexible array)
    -  How to get a Slide: ``` x := make([]float64, 5) ``` or ``` arr := [5]float64{1,2,3,4,5} x := arr[0:5] ```
    -  Slide operations: 
      - append: ```  slice1 := []int{1,2,3} slice2 := append(slice1, 4, 5) // 4 and 5 will be added after 3 ```
      - copy: ```  slice1 := []int{1,2,3} slice2 := make([]int, 2) copy(slice2, slice1) // the contents in slice2 will be copied to slice1 ```
      
   - Map
   ```
   x := make(map[string]int) // string is key, int is value
   
   ```
  
