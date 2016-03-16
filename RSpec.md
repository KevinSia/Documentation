# My Notes
- Array methods in ruby
```ruby
  arr = ['a', 'b', 'c', 'd', 'e', 'f']
  arr.fetch(100)        #=> raise Exception
  arr.fetch(100,"oops") #=> "oops"
  
  arr.take(3)   #=> ['a', 'b', 'c']
  arr.drop(3)   #=> ['d', 'e', 'f']
  
  arr << 'g'        #=> ['a', 'b', 'c', 'd', 'e', 'f', 'g']
  arr.unshift('z')  #=> ['z', 'a', 'b', 'c', 'd', 'e', 'f', 'g']
  
```
- if Argument of most outer example is a Class, an instance of that Class can be exposed to the inner examples with `.subject`
```ruby
  # under top level group
  describe Array do
    it "should be empty when first created" do
      subject.should be_empty  # similiar to array.should be_empty
    end
  end
  
  # under nested group
  describe Array do
    describe "when first created" do
      it "should be empty" do
        subject.should be_empty
      end
    end
  end
```




