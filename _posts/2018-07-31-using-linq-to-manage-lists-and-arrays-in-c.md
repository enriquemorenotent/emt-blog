---
layout: post
title: 'Using LINQ to manage Lists and Arrays in C#'
---
All developers need to loop through arrays or lists sooner or later, to perform operations on its items. For instance, let us say that we want to loop through an array of \*enemies\* to check in any of them are alive.

```c#
Enemy[] enemies = GetEnemies();
bool anyEnemyAlive = false;
foreach (Enemy enemy in enemies) {
    if (enemy.alive) {
    anyEnemyAlive = true;
    break;
    }
}
if (anyEnemyAlive) { /* Do something */ }
```

We all have been there, and we often use `for` loops or `foreach`. I recently discovered there is a simpler way to do this in C#, using LINQ.

```c#
using System.Linq;
Enemy\[] enemies = GetEnemies();
if (enemies.Any(enemy => enemy.alive)) { /\* Do something \*/ }
```

Feels much more idiomatic, and definitely easier to read and write. **But** this approach should be use with care, since it can have unexpected performance hits or garbage allocations. It would be best used for methods that just need to run once, like constructors and such, probably.

Feel free to comment on this technique and share your thoughts.

Credit: [ADAMGRYU](https://twitter.com/adamgryu/status/664116395823747073)
