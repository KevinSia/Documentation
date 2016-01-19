#Ruby-Coding-Style-Documentation

#Hello!

```ruby
hello
```

+ 2 spaces indentation with soft tabs
```ruby
if something
..do something
end
```

+ One expression per line
```ruby 
def some_method
  #do something
end
```
+ Except empty body method
```ruby
def some_method; end
```
+ Spaces
  + Between operators
  ```ruby
  1 + 1 or foo == bar
  ```
  + After commas, colons, and semicolons 
  ```ruby
  [1, 2, 3]
  foo: bar
  ```
  + Around braces
  ```ruby
  { provider: facebook }
  ```
+ No spaces 
  + around [] and ()
  ```ruby
  object.(parameter)
  [1, 2, 3].size
  ```
  + after ! 
  ```ruby
  !something
  ```
  



