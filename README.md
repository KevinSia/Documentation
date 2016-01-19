#Ruby-Coding-Style-Documentation
  
```ruby
loop.do{puts"hello,world!"}
#Example of bad code style!
```

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
  def some_method(arg1 = :default, arg2 = :default2); end
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
  object.(parameter1, parameter2, parameter3)
  [1, 2, 3].size
  ```
  + after ! 
  ```ruby
  !something
  ```
  + range literals
  ```ruby
  1..5
  ```
+ case-when & if-else  
  + case and when syntax same line
  ```ruby
  case
  when statement1
    puts 'foo'
  when statement2
    puts 'bar'
  else
    puts 'baz'
  end
  ```
  + assigning with if-else (putting in on next line -> efficient)
  ```ruby
  result =
    #condition same line with syntax
    if condition1   
      do something
    else 
      do another thing
    end
  ```
+ Keep to 80 chars per line
+ Long string concatenation
```ruby
str = 'We wish you a merry christmas, ' +
      'we wish you a merry christmas, ' +
      'we wish you a merry christmas, ' +
      'and a happy new year!'
```
+ method chaining
```ruby
one.two.three
  .four
```
+ long parameters
```ruby
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text
  )
end
```
+ align array literals
```ruby
menu_item = 
  ['vegetables', 'meat', 'seafood', 'toufu', 'abc', 'def',
   'ghi', 'jkl' ,'mno', 'pqr']
```
+ big numbers
```ruby 
1_000_000
````
+ trailing whitespaces (sneaky)
```ruby
Hello world!        
```
+ Multiple assignments
```ruby
a = 'foo'
b = 'bar'
c = 'baz'
d = 'qux'
```
+ Ternary operator > if/then/else/end
```ruby
result = condition ? short_expression : short_expression2
```
+ But not the case for nested conditions
```ruby
if condition1
  nested_condition ? nested1 : nested2
else
  something_else
end
```
+ avoid !! 
```ruby
x = 'text'
if !!x
  do_something
end

# instead do as below
x = 'text

unless x.nil?
  do_something
end
```

+






