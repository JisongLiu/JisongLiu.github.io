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
    -  How to get a Slide: ``` x := make([]float64, 5) ```
    -  
  
