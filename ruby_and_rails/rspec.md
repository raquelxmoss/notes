## Subject

### Implicitly defined subject

In the example below, subject will be an instance of `Cat`

```ruby
RSpec.describe Cat do
  it "meows" do
    expect(subject.meow).to be_true
  end
end
```

### Explicitly defined subject

Use this to pre-populate what would otherwise be an implicitly defined subject

```ruby
subject { Cat.new(name: "Meiko", meow: false) }

it "is named Meiko" do
  expect(subject.name).to eq("Meiko")
end
```

Subject is memoized _within_ an example, but not _across_ examples.

You can name a subject

```ruby
subject(:named_cat) { Cat.new(name: "Starbuck") }

it "is named Starbuck" do
  expect(named_cat.name).to eq("Starbuck")
  expect(subject.name).to eq("Starbuck")
end
```

### One Liner Syntax

```ruby
RSpec.describe Array do
  describe "initializing an array" do
    it "is empty" do
      expect(subject).to be_empty
    end
    # OR
    it { is_expected.to be_empty }
  end
end
```

