# Ruby Arrays - Iterating

## Objectives

Students will learn about the array `.each` method as well as other iterators that can be used on an array.

## SWBATS

+ ARRAYS - use `.each` for iteration
+ ARRAYS - use `.each` to perform common array operations:
  - create a new array by modifying elements from the previous
  - filter an array by applying a conditional to its elements
  - reduce an array by summing all of its elements

## Improving the Access by Index Method

In the previous lesson, we used a counter to access each element of an array by index:

```ruby
idx = 0
while idx < arr.length
  puts "This is the element at index: #{idx}: #{arr[idx]}"
  idx += 1
end
```

What we are doing above, (iterating over every element, one after the other), is such a common operation that most modern languages have incorporated a built in way of doing just that! Ruby arrays provide us with the `.each` method which allows us to run some code for every element _and_ it abstracts the unnecessary repetitive use of an index counter to the background. The real advantage here is that we can express ourselves quicker while writing less 'boilerplate' code.

## `array.each`

As an example, let's imagine we are the lead programmer in charge of adding features to the Amazon 'cart'. One of the variables we have access to is an array of prices that gets `.push(new_item_price)` performed on it whenever a user selects a new item. Our array could look like the following:

```Ruby
cart_item_prices = [12.43, 19.99, 3.49, 75.00]
```

As the lead programmers of this 'cart' feature, our Amazon customer experience contact has come to us and said: "We want to make sure users can click a button which displays all of the prices, in order, of the items they have in their cart".

Naturally, we reply: "No problem, here is how I would do it, using the power of `arr.each`...":

**NOTE:** some new syntax that students likely haven't seen yet is in the next code block. Make sure to express "some of this may not click immediately -- that's expected! Let's take our time and go through line by line unpacking what's new here. You will see that it is nothing we haven't done before."

```ruby
count = 1

cart_item_prices.each do |price|
  puts "Item #{count}: #{price}"
  count += 1 # even though we are using this count, its only so we can format a nice print out (i.e. 'Item 1'. Try removing it from the loop and showing that it still runs fine. We don't want students confusing it with the access by index method.)
end
# > Item 1: 12.43
# > Item 2: 19.99
# > Item 3: 3.49
# > Item 4: 75.0

# identical code using the index method:
#
# index = 0
# while index < cart_item_prices
#   puts "Item #{index + 1}: #{cart_item_prices[index]}"
#   index += 1
# end
```

**NOTE**: could also introduce `.each_with_index`, but we are trying to keep this focused and stick with building on the `.each` method for the time being.

Alright, you should see something new above: a `do`, followed by some new variable wrapped in `|` pipes `|`. As the block runs, that variable represents the value of the _current element of iteration_.

That variable's name could be whatever we want. We name it when we create the `.each` block. In this example, we chose the name `price` because, each time our looping code block runs, it will represent _a single price_.

**MINI LAB ON `.each` - log out all the items**

Now that we have the powerful `.each` method under our belts, let's jump right into doing more advanced operations with our array!

## Altering all values

Our Amazon contact has reached out again and, now that they are no longer selling items exclusively in Delaware, made it clear they need to apply a sales tax to every item. They have requested the following: "Instead of just the base price of the item, we want a new array of the prices with tax included."

Confidently, we begin to ideate a solution...:

```Ruby
tax_included = []

cart_item_prices.each do |price|
  price_with_tax = price * 0.17
  tax_included << price_with_tax
end
# => [12.43, 19.99, 3.49, 75.0]
```

**QUERY/PROGRAM TOGETHER:** Alright, our contact was so impressed with our work, they asked if we could do one more thing. They want to have an array created with all of the modified price + tax values in it. How could we do this?

## Filtering an array

Another common task we find ourselves performing on arrays is filtering, that is, going through an array and collecting only those values that meet a certain criteria. To stick with our cart example, let's imagine our contact wants us to display only the 'big ticket' prices:

"Alright, the team loves your work. Next, we need some way to display only items that are over $15 dollars. We are running an exclusive offer where all items under $15 are free!"

Just as you are about to explain why this is a potentially catastrophic business decision, you become engrossed in creating a solution...:

```ruby
big_ticket_prices = []

cart_item_prices.each do |price|
  if price >= 15
    big_ticket_prices << price
  end
end

big_ticket_prices
# => [19.99, 75.0]
```

At this point, your programming solutions to the Amazon team have been so timely, so concise, that they request your services one last time for the most important deliverable yet:

## Reducing an array to a single value

The team expresses that their users are having trouble mentally calculating the sum of their individual item prices. This makes sense: our users are provided with a print out of prices, after which they would be forced to perform good ol' arithmetic to add them up.

"The marketing team has determined users care about seeing a 'total value' when checking out, and we are looking to provide just that. Do you have a code solution?"

```ruby
total = 0

cart_item_prices.each do |price|
  total += price
end

total
# => 110.91
```
