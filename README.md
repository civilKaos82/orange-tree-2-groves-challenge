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


### Release 0: Apples and Apple Trees
We have an `OrangeTree` class with a public interface:  methods like `#age`, `#mature?`, `#dead?`, etc.  We are going to create an `AppleTree` class that copies this exact interface.  In other words, the messages that we send to an orange tree will be the same that we send to an apple tree.  

However, while orange trees and apples trees will have the same behaviors, they will have different life cycles.  They'll produce fruit at different ages, grow at different rates, die at different ages, etc.  The particulars for each tree type can be found in Table 1.

Start by writing tests for the `AppleTree` class.  Use the tests for the orange tree as a pattern, modifying them for the particulars of an apple tree.  Then, implement the class itself.  Don't forget to create an `Apple` class as well; we wouldn't want an apple tree that produces oranges.



### Release 1: From Specific Types to a General Type
We have now modeled two specific types of fruit tree.  Our orange and apple trees behave very similarly.  Based on the similarities in behavior among the two types of tree, we can create a more generalize case: a fruit tree.  

We can create a `FruitTree` class with generalized behaviors.  Our `OrangeTree` and `AppleTree` classes can inherit behaviors from this general class and implement their own specifics.  For example, both orange trees and apple trees have a height.  With each passing season, the trees grow by some amount until they reach a maximum height.  This is the general behavior that can be represented in a general fruit tree model.  That general behavior would be inherited by each of the specific types of fruit tree with each specific type defining by how much it grows each year and its own maximum height.


```ruby
class FruitTree
  # define the class
end

class OrangeTree < FruitTree
  # define the class
end

class AppleTree < FruitTree
  # define the class
end
```
*Figure 1*. Defining `OrangeTree` and `AppleTree` classes which inherit from a `FruitTree` superclass or parent class. 


Define a `FruitTree` class and modify the `OrangeTree` and `AppleTree` classes to inherit from it (see Figure 1).  Incrementally move the shared behaviors from the specific trees to the general tree.  Do the same for our fruit classes.

As we do so, our tests should continue to pass—we might need to make small updates to our tests if we change our method names, but we shouldn't need to change the logic of our tests. That's the beauty of tests, they're a safety net when we engage in large refactors like this one. If our tests continue to pass, we know we're in good shape. If not, we get to catch our mistakes early.


### Release 2: The `PearTree` and `Pear` Classes

Now that you have `FruitTree` and `Fruit` classes, create a `PearTree` class that yields `Pears`, just like `OrangeTree` and `AppleTree`.

Yup, you'll want to write tests for that too. It's going to be feel like you're copying and pasting with minor edits. Don't worry about it. Our RSpec-fu will improve over time.

### Release 3: Create a `TreeGrove` Class

Let's plant some trees!  Create a `TreeGrove` class that works as follows.

1. You can initialize a `TreeGrove` with an `Array` of any kind of `FruitTree`, of any age.
2. There is a `TreeGrove#age!` method will will age each tree in the grove one year by calling `age!` on each `FruitTree`.
3. There is a `TreeGrove#trees` method which returns all trees
4. There is a `TreeGrove#mature_trees` method which returns all trees that can currently bear fruit
5. There is a `TreeGrove#dead_trees` method which returns all dead trees

Write tests for `TreeGrove` to assert that it's working as your expect.


[orange tree challenge]: ../../../orange-tree-1-just-oranges-challenge
[rubylearning.com inheritance]: http://rubylearning.com/satishtalim/ruby_inheritance.html
