# Model a Grove of Different Trees

## Summary
In [another challenge][orange tree challenge] we modeled an orange tree for our client, Fran the Farmer.  We were able to model for her the production of an orange tree over the course of its lifetime.  She was satisfied enough with our work that she's engaging us on another project.  Her orange farm is considering the acquisition of a neighboring tree grove, a grove that includes varieties of trees beyond orange trees.

We're going to build a simple model of a tree grove.  We'll begin with our  orange tree and use it as a pattern for modeling an apple tree.  Once we have the two tree classes and the corresponding fruit classes, we'll take time to refactor our code.  Once our code is refactored, we'll add an additional tree type:  pear trees.  Finally, we'll model the tree grove.


### Inheritance
When we later refactor our code, we'll use *inheritance* to eliminate the repetition that exists in what will then be our `OrangeTree` and `AppleTree` classes.  We'll create a general `FruitTree` class, from which we can create more specific classes of trees:  orange, apple, and later pear.  Our generic fruit tree model will provide the basic behaviors of our trees: they grow, they mature, they die, etc.  The orange, apple, and pear trees will share the same basic behaviors, but each will differ in its implementation: one tree produces oranges, another apples; one tree dies at age 100, another at 45; and so on.  See Table 1.

For more information on inheritance in Ruby, see this [description from learningruby.com][rubylearning.com inheritance].

|                    | orange trees | apple trees | pear trees |
| ------------------ | -----------: | ----------: | ---------: |
| maximum height     | 30           | 26          | 20         |
| growth rate        | 2.5          | 2           | 2.5        |
| annual fruit yield | 100 - 300    | 400 - 600   | 175 - 225  |
| age of maturity    | 6            | 5           | 5          |
| age of death       | 100          | 45          | 40         |
| type of fruit      | oranges      | apples      | pears      |

*Table 1*.  Data for orange trees and apple trees.



## Releases
### Pre-release:  Copy the Orange Tree Model
Before we begin, copy the code from the orange tree challenge.  Bring over both the code for the orange tree and the orange fruit.  Bring the tests, too, and make sure that they are passing.


###Release 0 : The `AppleTree` and `Apple` Classes

Let's start by defining `AppleTree` and `Apple` classes.  They should behave the same as `OrangeTree`, although have a different life cycle.

That is, they should support all the same methods, but the particularities might differ: apples have a smaller diameter but apple trees bear fruit sooner and bear more fruit when they do.

Creating the `Apple` and `AppleTree` class at this stage shouldn't involve much more than copying your `Orange` and `OrangeTree` classes and changing a few variables or constants.  If it's more complicated than that ask for help!

You'll need to add tests for `AppleTree` and `Apple`. Those tests are going to look a whole lot like `OrangeTree` and `Orange`. Don't worry if your specs aren't DRY for now.

###Release 1 : The `FruitTree` and `Fruit` Classes

You now have two kinds of trees which each bear their own fruits.  They have tons of code in common.  One way to deal with this repetition is to **abstract out** the common parts into a parent class.  We'll call that parent class `FruitTree`, so your `OrangeTree` class should now look like:

```ruby
class OrangeTree < FruitTree
  # code goes here
end
```

Think carefully about the parameters that make an orange tree different from an apple tree.  They might include parameters like

1. How much the tree grows each year
2. How old the tree must be before it stops growing
3. How old the tree must be before it bares fruit
4. How much fruit the tree yields each year
5. Maybe most importantly, what *kind* of fruit it bares

There could be others, but this gives you an idea of some of the "parameters" that differentiate one fruit tree's behavior from another.

Most importantly, your tests should still run. You might need to make small fixes if you change your method names on your classes, but you shouldn't need to change the logic of your tests. That's the beauty of tests, they're a safety net when we engage in large refactors like this one. If they continue to go green, you know you're in good shape. If not, you get to catch your mistakes early.

#### The `PearTree` and `Pear` Classes

Now that you have `FruitTree` and `Fruit` classes, create a `PearTree` class that yields `Pears`, just like `OrangeTree` and `AppleTree`.

Yup, you'll want to write tests for that too. It's going to be feel like you're copying and pasting with minor edits. Don't worry about it. Our RSpec-fu will improve over time.

###Release 2 : Create a `TreeGrove` Class

Let's plant some trees!  Create a `TreeGrove` class that works as follows.

1. You can initialize a `TreeGrove` with an `Array` of any kind of `FruitTree`, of any age.
2. There is a `TreeGrove#age!` method will will age each tree in the grove one year by calling `age!` on each `FruitTree`.
3. There is a `TreeGrove#trees` method which returns all trees
4. There is a `TreeGrove#mature_trees` method which returns all trees that can currently bear fruit
5. There is a `TreeGrove#dead_trees` method which returns all dead trees

Write tests for `TreeGrove` to assert that it's working as your expect.


[orange tree challenge]: ../../../orange-tree-1-just-oranges-challenge
[rubylearning.com inheritance]: http://rubylearning.com/satishtalim/ruby_inheritance.html
