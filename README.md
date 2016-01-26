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
## Comments & Comment Annotations`
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
# Rails

## Configuration
+ Keep initialization file in seperate file and name it with gem's name 
  + Example: `clearance.rb` , `carrierwave.rb` 
+ Keep configuration that's applicable to all environments in the config/application.rb file. 
## Routes
+ Use `member`/`collection` routes to add action into RESTful resource
```ruby
# recognizes photos/:id/preview
# and creates path & url
resources :photos do
  get 'preview' on: :member
end

# recognizes photos/search
# and creates path & url
resources :photos do
  get 'search' on: :collection
end
```
+ Multiple `member` / `collection` routes
```ruby
resources :listings do
  member do
    get 'reservations'
    get 'photos'
  end
end
```
+ Use nested routes to describe relationship between models
```ruby
# posts has_many comments and comments belongs_to post
resources :posts do
  resources :comments
end
```
+ Resources should never be nested more than 1 level deep
  + Use shallow: true if must to avoid long path_name and urls
  ```ruby
  resources :posts, shallow: true do
    resources :comments do
      resources :versions
    end
  end
  ```
# Controller
+ Keep the controller skinny
  + Controller should only be used to
    + Retrieve data
    + Redirect/rendering
    + Authentication/authorization and session/cookie handling
  + No business logic should present in controller
+ Share not more than two instance variables between controller and view
+ Use `render plain` to render text
```ruby
render plain: 'Rails'
```
# Models
+ Feel free to introduce non ActiveRecord classes to make Model 'skinny'
```ruby
# non ActiveRecord class
~/app/model/rating.rb
class Rating
  def self.from_cost(cost)
    if cost <= 2
      new("A")
    elsif cost <= 4
      new("B")
    elsif cost <= 8
      new("C")
    elsif cost <= 16
      new("D")
    else
      new("F")
    end
  end
end

~/app/model/movie.rb
class Movie < ActiveRecord::Base
  # some codes
  
  def rating
    @rating ||= Rating.from_cost(cost)
  end
end
```
+ Time.zone.today instead of Date.today

----------

## R-Spec coding styles
+ No empty lines below `describe`, `context`, or `feature`
```ruby
describe 'foo' do
  context 'bar' do
    it `baz` do
      # test something
    end
  end
end
```
+ Leave empty lines below `let`, `before/after`, or `subject`
```ruby
subject{ FactoryGirl.create(:something) }
let(:user){ FactoryGirl.create(:user) }

describe 'qux' do
  # code something
end
```
+ Use `let`/`subject`/`it` blocks whenever possible to DRY up your code
```ruby
Bad example:

describe 'Card' do
  describe '#new' do
    describe 'Two of hearts' do
      it 'has a value of 2' do
        card = Card.new("2H")
        card.value.should equal(2)
      end
    end
    
    describe 'King of clubs' do
      it 'has a value of 13' do
        card = Card.new("KC")
        card.value.should equal(13)
      end
    end

    describe 'Bad value' do
      it 'should raise StandardError' do
        expect { card = Card.new("ZZ") }.to raise_error(StandardError)
      end
    end
  end
end

Good example:

# used *subject* for initialization
describe 'Card' do
  subject do
    Card.new(card_type)
  end
  
  describe '#value' do
    context 'Two of hearts' do
      let(:card_type) {"2H"}      # more readable
      its(:value) { should == 2 } 
    end
    
    context 'king of clubs' do
      let(:card_type) {"KC"}
      its(:value) { should == 13 }
    end
    
    #no changes below
    context 'bad value' do
      it 'should raise StandardError' do
        expect { card = Card.new("ZZ") }.to raise_error(StandardError)
      end
    end
  end
end
```
+ `describe` use `.` when referring to class method and `#` for instance method
```ruby
describe '.authenticate' do
end

describe '#admin' do
end
```
+ Group `let`/`subject` blocks but seperate them from `before`/`after` blocks
```ruby
describe Thing do
  subject { FactoryGirl.create(:some_article) }
  let(:user) { FactoryGirl.create(:user) }

  before do
    # ...
  end

  after do
    # ...
  end
end
```
+
  
  
  
  
  #References
  1. [Ruby Coding Styles](https://github.com/bbatsov/ruby-style-guide#no-dsl-decorating)
  2. [Rails Coding Styles](https://github.com/bbatsov/rails-style-guide/blob/master/README.md)
  3. [Mistakes A Rails Programmer Makes](http://www.toptal.com/ruby-on-rails/top-10-mistakes-that-rails-programmers-make)
  4. [R-spec Style Guide](https://github.com/reachlocal/rspec-style-guide)
  5. [Better Specs](http://betterspecs.org/)
  6. 

