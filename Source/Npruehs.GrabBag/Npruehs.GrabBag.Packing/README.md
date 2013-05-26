2D Packing
==========

TODO: Describe packing problems in general.

* _item_
* _strip_
* _solution_
* _levels_
* _solution quality_


In this implementation, items that have to be packed are represented by
rectangles. While the initial position of these rectangles doesn't 
matter for the packing algorithms, their size does.

```csharp
List<PackingItem> items = new List<PackingItem>();

items.Add(new PackingItem(0, 0.3f, 0.5f));
items.Add(new PackingItem(1, 0.5f, 0.4f));
items.Add(new PackingItem(2, 0.4f, 0.8f));
```

Given a stip width, each algorithm is able to find a solution for an
arbitrary list of items. Some of the algorithms, such as the Epstein/van Stee,
rotate items in order to approximate a better solution.

```csharp
FirstFitDecreasingHeight ffdh = new FirstFitDecreasingHeight();
float stripWidth = 1.0f;

ffdh.FindSolution(stripWidth, items);
```

The solution, in other words the positions of all packed items, can be
accessed by enumerating the algorithm instance.

```csharp
foreach (PackingItem item in ffdh)
{
    if (item.Rectangle.X + item.Rectangle.Width > stripWidth)
    {
        Assert.Fail("Item {0} exceeds strip width {1}.", item, stripWidth);
    }
}
```

The algorithms in this library belong to the class of level-oriented
packing algorithms. After having found a solution, you may enumerate the
solution levels as well, accessing their items and y-position.