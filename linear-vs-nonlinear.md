# Linear vs Non-Linear History

Linear history example:

```
* c6121fd (HEAD -> master, topic/feature) fixes issue with feature
* fcbba2d adds blah to feature
* 2e09b2a adds feature foo
* 2985b6b blah blah
* ebe0262 blah
* 03f4f8d previous commit
* 62a0ee9 ...
```

Non-linear history example:

```
*   f17ba26 (HEAD -> master) Merge branch 'topic/feature'
|\
| * cba1d40 (topic/feature) fixes issue with feature
| * 8b29f74 adds blah to feature
| * 7f295dd adds feature foo
* | 2985b6b blah blah
* | ebe0262 blah
|/
* 03f4f8d previous commit
* 62a0ee9 ...
```

In general, it is recommended to **strive for a linear history**, because it is easier to figure out what happened than with a non-linear history. Non-linear history becomes exceedingly unreadable when a lot of branches forked off and merged across a longer commit range.

---

[back to index](index.html)
