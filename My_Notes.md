# My Notes

## Ruby
- Array methods in ruby
```ruby
  arr = ['a', 'b', 'c', 'd', 'e', 'f']
  arr.fetch(100)        #=> raise Exception
  arr.fetch(100,"oops") #=> "oops"
  
  arr.take(3)   #=> ['a', 'b', 'c']
  arr.drop(3)   #=> ['d', 'e', 'f']
  
  arr << 'g'             #=> ['a', 'b', 'c', 'd', 'e', 'f', 'g']
  arr.unshift('z')       #=> ['z', 'a', 'b', 'c', 'd', 'e', 'f', 'g']
  arr.insert(3, 'apple') #=> ['z', 'a', 'b', 'apple, 'c', 'd', 'e', 'f', 'g']
  arr.shift              #=> ['a', 'b', 'apple, 'c', 'd', 'e', 'f', 'g']
  arr.pop                #=> ['a', 'b', 'apple, 'c', 'd', 'e', 'f']
  arr.delete('apple')    #=> ['a', 'b', 'c', 'd', 'e', 'f']
  arr.unshift(nil).insert(3,nil).push(nil) #=> [nil ,'a', 'b', nil, 'c', 'd', 'e', 'f', nil]
  arr.compact            #=> ['a', 'b', 'c', 'd', 'e', 'f']
  arr                    #=> [nil ,'a', 'b', nil, 'c', 'd', 'e', 'f', nil]
  arr.compact!           # arr => ['a', 'b', 'c', 'd', 'e', 'f']
  arr.shift('a')         #=> ['a', 'a', 'b', 'c', 'd', 'e', 'f']
  arr.uniq               #=> ['a', 'b', 'c', 'd', 'e', 'f']
  
```

## R-Spec
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
  
  # top most group wins (even there are two classes)
  
  class ArrayWithOneElement < Array
    def initialize(*)
      super
      unshift "first element"
    end
  end

  describe Array do
    describe ArrayWithOneElement do
      context "referenced as subject" do
        it "should be empty (because it is the Array declared at the top)" do
          subject.should be_empty
        end
      end
  
      context "created in the example" do
        it "should not be empty" do
          ArrayWithOneElement.new.should_not be_empty
        end
      end
    end
  end
  
```

-




