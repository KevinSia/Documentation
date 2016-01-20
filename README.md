#Ruby & Rails Coding Style Documentation

  
```
loop.do{puts"hello,world!"}
#Example of bad code style!
```
#Ruby
##Syntaxes

+ 2 spaces indentation with soft tabs
```ruby
if something
..do something
end
```

+ One expression per line
```ruby 
def some_method
  # Do something.
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
  + Around braces `{}`
  ```ruby
  { provider: facebook }
  ```
+ No spaces 
  + around `[]` and `()`
  ```ruby
  object.(parameter1, parameter2, parameter3)
  [1, 2, 3].size
  ```
  + after `!` 
  ```ruby
  !something
  ```
  + range literals
  ```ruby
  1..5
  ```
+ `case-when` & `if-else`
  + case and when syntax same indentation
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
  + assigning with `if-else` (putting in on next line makes it efficient to read)
  ```ruby
  result =
    #condition same line with syntax
    if condition1   
      do something12
    else 
      do another thing
    end
  ```
+ Keep to 80 chars per line (tweak subline to show limit line)
+ Long string concatenation
```ruby
str = 'We wish you a merry christmas, ' +
      'we wish you a merry christmas, ' +
      'we wish you a merry christmas, ' +
      'and a happy new year!'
```
+ method chaining (by Law of Demeter, nope)
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
1000000000 # What value is this?
1_000_000_000 # A billion
````
+ avoid trailing whitespaces (sneaky)(sublime plugin?)
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
+ Ternary operator > `if/then/else/end`
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
+ Avoid `!!` 
```ruby
x = 'text'
if !!x
  do_something
end

# instead do as below
x = 'text

unless x.nil?
  # many codes here
end  
```
+ Use modifier `if` or `unless` for one expression body
```ruby
do_something if condition
do_something unless condition
```

+ Try single-line control flow (`||` and `&&`)
```ruby
document.saved? || document.save!

some_condition && do_something
```

+ No parentheses in `if` condition unless involves assignment 
```ruby
if condition
  do something
end

if ( v = array.grep(Integer) )
  do something
end
```
+ Use `&&` and `||` instead of `and` and `or`
+ Use `loop` instead of while/until for infinite loop
```ruby
loop do
  do something
end
```
+ Use the proc invocation shorthand when the invoked method is the only operation of a block. 
```ruby
# bad
names.map { |name| name.upcase }

# good
names.map(&:upcase)
```
+ Avoid `self` when not required (except when self write accessor)
```ruby
def ready?
  if last_reviewed_at > last_updated_at
    worker.update(content, options)
    self.status = :in_progress
  end
  status == :verified
end
```
+ Avoid nested methods. 
```ruby
# Good but no bar redefinition on every foo call.
def bar(y)
  # Body omitted
end

def foo(x)
  bar(x)
end

# This is also good.
def foo(x)
  bar = ->(y) { ... }
  bar.call(x)
end
```
+ Prefix with _ for unused block parameters and local variables
```ruby
result = hash.map { |_k, v| v + 1 }

def something(x)
  _unused_var, used_var = something_else(x)
  # ...
end
```
+ Use guard clause if possible (bails out of function asap)
```ruby
def compute_thing(thing)
  return unless thing[:foo]
  update_with_bar(thing[:foo])
  return re_compute(thing) unless thing[:foo][:bar]
  partial_compute(thing)
end
```
+ `next` in loops vs `if-else`
```ruby
[1,2,3,4].each do |item|
  next unless item.even?
  puts item
end
```
## The art of naming in ruby / rails
+ use snake_case for 
  + symbols, methods, and variables
  ```ruby
  :symbol_one
  
  def method_two
  end
  ```
  + file and directory names
  ```ruby
  hello_world.rb
  orange_tree/orange_tree.rb
  ```
+ use CamelCase for class and module names
```ruby
class NextAcademy
end

module SpecOps
end
```
+ use SCREAMING_SNAKE_CASE for constants
```ruby
MY_AGE = 18
```
+ end method names with ? if it returns a boolean
```ruby
def old?
  MY_AGE > 18
end
```
+ end method names with ! if it has a safe version of it
```ruby
def update! # Dangerous method.
end

def update  # Safe method.
end
```
#`# Comments & Comment Annotations`
+ Write comments in English!
+ Keep comments up-to-date
+ Use annotation keywords while describing problem to indicate problem type
  + Example:
  ```ruby
  def bar
    # FIXME: This has crashed occasionally since v3.2.1. It may
    #   be related to the BarBazUtil upgrade.
    baz(:quux)
  en
  ```
  + Use `TODO` to note missing features or functionality that should be added at a later date
  + Use `FIXME` to note broken code that needs to be fixed. 
  + Use `OPTIMIZE` to note slow or inefficient code that may cause performance problems. 
  + Use `HACK` to note code smells where questionable coding practices were used and should be refactored away. 
  + Use `REVIEW` to note anything that should be looked at to confirm it is working as intended. 
  + Create own annotation keywords here?
  ```ruby
  # REVIEW: Are we sure this is how the client 
  #   does X currently? 
  ```
  + For multiple line annotations, use 1+2 (or 3) indentation for subsequent lines (1 after `#`, 2 for general indent)
## Classes and modules

+ indent `public`, `private` and `protected` as much as method definition
```ruby
class MyClass
  def method_one
    # ...
  end
  
  def method_two
    # ...
  end
  # one line space before keyword
  private
  # one line space after keyword
  def user_params
    # ...
  end
end
```
+ Class methods 
```ruby
class MyClass
  # method 1 
  def self.method_one
   # ...
  end
  
  # method 2 ( for multiple class methods )
  class << self
    def method_two
      # ...
    end
    
    def method_three
      # ...
    end
  end
end
```
## Collections
+ Defining empty array / hashes
```ruby
# Instead of doing this
arr = Array.new
hash = Hash.new

# Do this
arr = []
hash = {}
```

+ Array literals
  + For words
  ```ruby
  arr = %w(foo bar baz)
  ```
  + For symbols
  ```ruby
  arr = %i(boo far faz)
  ```

+ Hash literals
```ruby
# No more hash rockets!
hash = { one: 1, two: 2, three: 3 }

# Unless there exist multiple type of keys
hash = { :one => 1 , 'two' => 2 }
```
+ Hash methods 
```ruby
# No more has_key and has_value method
hash.key?(:key)
hash.value?(value)

# Use each_key and each_value instead of key.each or value.each
hash.each_key {|k| puts k}
```
+ If value existence is important , use `fetch` instead
```ruby
heroes = { batman: 'Bruce Wayne', superman: 'Clark Kent' }
heroes[:batman] # => 'Bruce Wayne'
heroes[:suparman] # => nil (might not want this to happen)

heroes.fetch(:suparman) # raises an exception instead
```
+ Retrieving several values from hash
```ruby
# Instead of
username = data[:username]
email = data[:email]

# You can do this
username, email = data.values_at(:username, :email)
```
+ When providing an accessor for a collection, provide an alternate form to save users from checking for nil before accessing an element in the collection. 
```ruby
# bad
def awesome_things
  @awesome_things
end

# good
def awesome_things(index = nil)
  if index && @awesome_things
    @awesome_things[index]
  else
    @awesome_things
  end
end
```
## String
+ String interpolation over String concatenation
```ruby
# In this case the padding inside braces is not needed
email_with_name = "#{user.name} #{user.email}
```
+ Adopt consistent string literal style : `'string'` or `"string"`
+ Avoid `String#+` , use `String#<<` instead
```ruby
names = ''

name_list.each { |n| name << #{n} }
```
+ Avoid `gsub` if possible (use gsub for regex)
```ruby
'abcde'.tr('bda', '123') # => '31c2e'
'foo-bar-baz'.tr('-','_') # => 'foo_bar_baz'
```
## RegEx
+ Use x modifier for complex regexps. This makes them more readable and you can add some useful comments. Just be careful as spaces are ignored. 
```ruby
regexp = /
  start         # some text
  \s            # white space char
  (group)       # first group
  (?:alt1|alt2) # some alternation
  end
/x
```
+ Test with rubular if regex is necessary
  
  
  
  
  
  
  
  
  #References
  1. https://github.com/bbatsov/ruby-style-guide#no-dsl-decorating
  2. 
