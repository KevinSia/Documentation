# My RSpec Notes

- if Argument of most outer example is a Class, an instance of that Class can be exposed to the inner examples with `.subject`
```ruby
  describe Array do
    it "should be empty when first created" do
      subject.should be_empty  # similiar to array.should be_empty
    end
  end
```

