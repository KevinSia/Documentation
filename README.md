#Ruby & Rails Coding Style Documentation

1. [Ruby](#ruby)
2. [Rails](#rails)

  
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
+ Keep to 80 chars per line (tweak sublime to show limit line)
+ Long string concatenation
```ruby
str = 'We wish you a merry christmas, ' +
      'we wish you a merry christmas, ' +
      'we wish you a merry christmas, ' +
      'and a happy new year!'
```
+ method chaining (Law of Demeter*)
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
## Comments & Comment Annotations
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
hash.each_key { |k| puts k }
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

name_list.each { |n| name << "#{n}" }
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
--------------------------------------------------------------------------------------------------
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

## Controller
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
## Models
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
+ Model sequence
```ruby
  class User < ActiveRecord::Base
  # keep the default scope first (if any)
  default_scope { where(active: true) }

  # constants come up next
  COLORS = %w(red green blue)

  # afterwards we put attr related macros
  attr_accessor :formatted_date_of_birth

  attr_accessible :login, :first_name, :last_name, :email, :password

  # followed by association macros
  belongs_to :country

  has_many :authentications, dependent: :destroy

  # and validation macros
  validates :email, presence: true
  validates :username, presence: true
  validates :username, uniqueness: { case_sensitive: false }
  validates :username, format: { with: /\A[A-Za-z][A-Za-z0-9._-]{2,19}\z/ }
  validates :password, format: { with: /\A\S{8,128}\z/, allow_nil: true }

  # next we have callbacks
  before_save :cook
  before_save :update_username_lower

  # other macros (like devise's) should be placed after the callbacks

  ...
end
```
+ Use `self` instead of `read_attribute` or `write_attribute`
```ruby
def convert_amount
  self[:amount] * 100
end

def set_amount
  self[:amount] = 100
end
```
+ Avoid old validation style
```ruby
class User < ActiveRecord::Base
  # old style
  validates_presence_of :email
  validates_presence_of :name
  validates_length of :name, maximum: 30
  
  # new style
  validates :name, presence: true, length: { maximum: 100 }
  validates :email, presence: true
end
```
+ Custom validation
  + Create when validation is used more than once / RegEx
  ```ruby
  class EmailformatValidator < ActiveRecord::EachValidator
    def validate_each(record, attribute, &valueO)
      record.errors[:attribute] << (options(message) || "is not a valid email" unless value =~               /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\z/i
    end
  end
  
  class User
  validates :email, emailformat: true
  ```
  + Keep these classes under directory app/validators
+ Use scopes freely
```ruby
  class User < ActiveRecord::base
    scope(:active), -> { where(active: true) }
    scope(:status), -> status { where(status: status) }
  end
```
+ Unless scopes get very complicated with lambda (readability), use class method instead
```ruby
  class User < ActiveRecord::base
    def self.with_orders
    joins(:orders).select('distinct(users.id)')
  end
```
+ Use `find_each` over `all` or `each` for iterating over ActiveRecord objects
```ruby
User.find_each do |user|
  user.party
end

User.where('age > 21').find_each do |user|
  user.drink
end
```
+ Rails creates callback for dependant associations and is executed before `before_destory` callback. To override this, use `prepend: true`
```ruby
class Classroom < ActiveRecord::Base
  has_many :student, dependent: destroy

  before_destroy :grade_fail, prepend: true

  private
    def grade_fail
      student.pass_test?
    end
end
```
## ActiveRecord queries
+ Avoid string interpolation in queries (prone to SQL injections). 
```ruby
Admin.where('permission = ?',params[:permission])
```
+ Use `find` over `where`
```ruby
User.find(id)
```
+ Use `find_by` for multiple attributes
```ruby
User.find_by(first_name: hello, last_name: kitty)
```
+ Use `find_each` to iterate through datas
```ruby
User.find_each do |user|
  'Hi #{user.name}!'
end
```
+ Use `where.not` over `!=`
```ruby
User.where.not(id: id)
```
## Migrations
+ Use `change` method instead of `up` and `down` when writing constructive migrations.
```ruby
class AddInterestToUser < ActiveRecord::Migration
  def change
    add_column :users, :height, :string
  end
end
```
+ Avoid using model classes in migrations as the model changes often.
+ 
## Views
+ DRY up your code by using layouts and partials.
+ Never make complex formatting in the views, export the formatting to a method in the view helper or the model.
+ Never call model layer directly from view.

## Assets
+ Reserve app/assets for custom stylesheets, javascripts, or images.
+ Use lib/assets for your own libraries that don’t really fit into the scope of the application. 
+ Third party code such as jQuery or bootstrap should be placed in vendor/assets. 
+ When possible, use gemified versions of assets (e.g. jquery-rails, jquery-ui-rails, bootstrap-sass, zurb-foundation). 



--------------------------------------------------------------------------------------------------
# R-Spec 
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
+ Leave one line around `it` blocks
```ruby
describe '#pay_debt do
  it 'returns money' do
  end
  
  it 'goes away' do
  end
  
  it 'disappear' do
  end
end
```
+ Avoid using `before(:each)` if possible, use `before` instead
```ruby
describe '#this' do
  before { # do something }
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
+ General rule of thumb - Use one expectation/assertion in one `it` block
```ruby
describe UsersController do
  describe 'GET new' do
    it 'assigns a new user' do
      get :new
      expect(assign[:user]).to be_a(Article)
    end
    
    it 'render new template' do
      get :new
      expect(response).to render_template :new
    end
  end
end
```
+ `context` should contain both positive & negative(complementary) cases/states
```ruby
describe '#edit' do
  context 'when user keys in valid input' do
  end
  
  context 'when user keys in invalid input' do
  end
end
```
## Test Description
+ `context` description should always starts with 'when' and in proper grammar
```ruby
context 'when email is not present' do
# do something
end
```
+ (subjective practice) Avoid writing *should* in the beginning of `it` description. It represents actual funtionality (It will happen!)
+ Conditional statements should not appear in `it`, wrap it in `context` instead
```ruby
Bad example:
it `returns 0 if its an even number' do
end

Better example:
context 'when the number is even' do
  it `returns 0` do
    # do something
  end
end

context 'when the number is odd' do
  it 'returns 1' do
    # do something
  end
end
```
+ In `describe` description, use `.` when referring to class method and `#` for instance method
```ruby
describe '.authenticate' do
  # test something
end

describe '#admin' do
  # test something
end
```
+ Avoid incidental state.
```ruby
  # Bad example
  it 'cures a new patient' do
    patient.cure
    expect(Patient.count).to eq(5) 
  end
  
  # Good example
  it 'cures a new patient' do
    expect{ patient.cure }.to change(Patient, :count).by(1)
  end
```
+ Use Rspec magical matcher.
```ruby
  # say you have a method called published?
  it 'is published' do
    expect(article).to be_published
  end
```
+ Use `let` over `before`/`before(:each)` as `let` is lazily evaluated.
```ruby
# use this:
let(:article) { FactoryGirl.create(:article) }

# ... instead of this:
before { @article = FactoryGirl.create(:article) }
```
## Views

+ The directory structure of the view specs spec/views matches the one in app/views. 
  + For example the specs for the views in app/views/users are placed in spec/views/users.
+ The naming convention for the view specs is adding `_spec.rb` to the view name, for example the view `_form.html.erb` has a corresponding spec `_form.html.erb_spec.rb`.
+ spec_helper.rb needs to be required in each view spec file.

+ The outer describe block uses the path to the view without the app/views part. This is used by the render method when it is called without arguments.
```ruby
      # spec/views/articles/new.html.erb_spec.rb
      require 'spec_helper'

      describe 'articles/new.html.erb' do
        # ...
      end
```
+ Always mock the models in the view specs. The purpose of the view is only to display information.

+ The method assign supplies the instance variables which the view uses and are supplied by the controller.
```ruby
# spec/views/articles/edit.html.erb_spec.rb
  describe 'articles/edit.html.erb' do
    it 'renders the form for a new article creation' do
      assign(:article, double(Article).as_null_object)
      render
      expect(rendered).to have_selector('form',
        method: 'post',
        action: articles_path
      ) do |form|
          expect(form).to have_selector('input', type: 'submit')
        end
    end
  end
```
+ Prefer the capybara negative selectors over to_not with the positive.
```ruby
    # bad
    expect(page).to_not have_selector('input', type: 'submit')
    expect(page).to_not have_xpath('tr')

    # good
    expect(page).to have_no_selector('input', type: 'submit')
    expect(page).to have_no_xpath('tr')
```
+ When a view uses helper methods, these methods need to be stubbed. Stubbing the helper methods is done on the template object:
```ruby
  # app/helpers/articles_helper.rb
  class ArticlesHelper
    def formatted_date(date)
      # ...
    end
  end

  # app/views/articles/show.html.erb
  <%= 'Published at: #{formatted_date(@article.published_at)}' %>

  # spec/views/articles/show.html.erb_spec.rb
  describe 'articles/show.html.erb' do
    it 'displays the formatted date of article publishing' do
      article = double(Article, published_at: Date.new(2012, 01, 01))
      assign(:article, article)

      allow(template).to_receive(:formatted_date).with(article.published_at).and_return('01.01.2012')

      render
      expect(rendered).to have_content('Published at: 01.01.2012')
    end
  end
```
+ The helpers specs are separated from the view specs in the spec/helpers directory.

## Controllers

+ Mock the models and stub their methods. Testing the controller should not depend on the model creation.
+ Test only the behaviour the controller should be responsible about:
  + Execution of particular methods
  + Data returned from the action - assigns, etc.

  + Result from the action - template render, redirect, etc.
  ```ruby
          # Example of a commonly used controller spec
          # spec/controllers/articles_controller_spec.rb
          # We are interested only in the actions the controller should perform
          # So we are mocking the model creation and stubbing its methods
          # And we concentrate only on the things the controller should do

          describe ArticlesController do
            # The model will be used in the specs for all methods of the controller
            let(:article) { double(Article) }

            describe 'POST create' do
              before { allow(Article).to receive(:new).and_return(article) }

              it 'creates a new article with the given attributes' do
                expect(Article).to receive(:new).with(title: 'The New Article Title').and_return(article)
                post :create, message: { title: 'The New Article Title' }
              end

              it 'saves the article' do
                expect(article).to receive(:save)
                post :create
              end

              it 'redirects to the Articles index' do
                allow(article).to receive(:save)
                post :create
                expect(response).to redirect_to(action: 'index')
              end
            end
          end
    ```
+ Use context when the controller action has different behaviour depending on the received params.
```ruby
      # A classic example for use of contexts in a controller spec is creation or update when the object saves successfully or not.

      describe ArticlesController do
        let(:article) { double(Article) }

        describe 'POST create' do
          before { allow(Article).to receive(:new).and_return(article) }

          it 'creates a new article with the given attributes' do
            expect(Article).to receive(:new).with(title: 'The New Article Title').and_return(article)
            post :create, article: { title: 'The New Article Title' }
          end

          it 'saves the article' do
            expect(article).to receive(:save)
            post :create
          end

          context 'when the article saves successfully' do
            before do
              allow(article).to receive(:save).and_return(true)
            end

            it 'sets a flash[:notice] message' do
              post :create
              expect(flash[:notice]).to eq('The article was saved successfully.')
            end

            it 'redirects to the Articles index' do
              post :create
              expect(response).to redirect_to(action: 'index')
            end
          end

          context 'when the article fails to save' do
            before do
              allow(article).to receive(:save).and_return(false)
            end

            it 'assigns @article' do
              post :create
              expect(assigns[:article]).to eq(article)
            end

            it 're-renders the 'new' template' do
              post :create
              expect(response).to render_template('new')
            end
          end
        end
      end
```
## Models

+ Do not mock the models in their own specs.

+ Use FactoryGirl.create to make real objects, or just use a new (unsaved) instance with subject.
```ruby
  describe Article do
    let(:article) { FactoryGirl.create(:article) }

    # Currently, 'subject' is the same as 'Article.new'
    it 'is an instance of Article' do
      expect(subject).to be_an Article
    end

    it 'is not persisted' do
      expect(subject).to_not be_persisted
    end
  end
```
+ It is acceptable to mock other models or child objects.

+ Create the model for all examples in the spec to avoid duplication.
```ruby
  describe Article do
    let(:article) { FactoryGirl.create(:article) }
  end
```
+ Add an example ensuring that the FactoryGirl.created model is valid.
```ruby
  describe Article do
    it 'is valid with valid attributes' do
      expect(article).to be_valid
    end
  end
```
+ When testing validations, use have(x).errors_on to specify the attribute which should be validated. Using be_valid does not guarantee that the problem is in the intended attribute.
```ruby
# bad
describe '#title' do
  it 'is required' do
    article.title = nil
    expect(article).to_not be_valid
  end
end

# preferred
describe '#title' do
  it 'is required' do
    article.title = nil
    expect(article).to have(1).error_on(:title)
  end
end
```
+ Add a separate describe for each attribute which has validations.
```ruby
  describe Article do
    describe '#title' do
      it 'is required' do
        article.title = nil
        expect(article).to have(1).error_on(:title)
      end
    end
  end
```
+ When testing uniqueness of a model attribute, name the other object another_object.
```ruby
  describe Article do
    describe '#title' do
      it 'is unique' do
        another_article = FactoryGirl.create(:article, title: article.title)
        expect(article).to have(1).error_on(:title)
      end
    end
  end
```
# Mailers
+ The model in the mailer spec should be mocked. The mailer should not depend on the model creation.
+ The mailer spec should verify that:
  + the subject is correct
  + the receiver e-mail is correct
  + the e-mail is sent to the right e-mail address
  + the e-mail contains the required information
  ```ruby
  describe SubscriberMailer do
    let(:subscriber) { double(Subscription, email: 'johndoe@test.com', name: 'John Doe') }

    describe 'successful registration email' do
      subject { SubscriptionMailer.successful_registration_email(subscriber) }

      its(:subject) { should == 'Successful Registration!' }
      its(:from) { should == ['info@your_site.com'] }
      its(:to) { should == [subscriber.email] }

      it 'contains the subscriber name' do
        expect(subject.body.encoded).to match(subscriber.name)
      end
    end
  end
  ```

  
  
  
  # References
  1. [Ruby Coding Styles](https://github.com/bbatsov/ruby-style-guide#no-dsl-decorating)
  2. [Rails Coding Styles](https://github.com/bbatsov/rails-style-guide/blob/master/README.md)
  3. [Mistakes A Rails Programmer Makes](http://www.toptal.com/ruby-on-rails/top-10-mistakes-that-rails-programmers-make)
  4. [R-spec Style Guide](https://github.com/reachlocal/rspec-style-guide)
  5. [Better Specs](http://betterspecs.org/)
  

