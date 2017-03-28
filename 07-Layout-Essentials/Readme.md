# Layout Essentials

### Objectives

- UIStackView
- UIScrollView
- UITableView
- UICollectionView


## UIStackView
Layout mechanism similar to CSS Flexbox
Better than Auto Layout for dynamic layouts

Position of views in UIStackView is determined by:
- axis: horizontal | vertical
- distribution: fill | even spacing |
- alignment: center | top | bottom | leading | trailing
- spacing: 10

Instead of using constraints, stack different
UIStackViews to build layout:

**Benefits**

- Layout is re-calculated when views are
hidden or added
- Try to build interface with UIStackView, add
explicit constraints only when necessary


## UIScrollView

Allows to display content that is larger than screen size User can scroll,
zoom, etc to view the entire content

UITableView and UICollectionView use UIScrollView internally

## UITableView

Use for list content, where amount of elements could be arbitrary large.
Ideal for uniform content.


## UICollectionView

Similar to UITableView but provides flexible, non-linear layout

- Provides default flow layout

- Allows to implement custom layouts

- Layout encapsulates logic for sizing and animating the cells


## Discussion

1. When should we use UITableView? UICollectionView or UIScrollView?


# Next - [Persistence](../07-Persistence/persistence.md)