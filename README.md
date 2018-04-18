# Resposive-CSS-from-scratch
This is about how to use CSS Grid to create a super cool image grid which varies the amount of columns with the width of the screen.
This means we don't have to clutter up the HTML with ugly class names (i.e. co-sm-4, col-md-8) or create media queries for every single screen size.
Here's how the initial grid looks like

HTML
```
<div class="container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```
And the CSS
```
.container{
    display:grid;
    grid-template-columns:100px 100px 100px;
    grid-template-rows:50px 50px;
}
```
## Basic responsiveness with the fraction unit
CSS brings with it a whole new value called a fraction unit. The fraction unit is written like ```fr```, and it allows you to split the container into as many fractions as you want.

Let's look an example.
```
.container{
    display:grid;
    grid-template-columns:1fr 1fr 1fr;
    grid-template-rows:50px 50px;
}
```
What happens hereis that the grid splits the entire width into three fractions and each of the columns take up one unit each.If we change the ```grid-template-columns```value to ```1fr 2fr 1fr```, the second column will now be twice as wide as the two other columns. The total width is now four fraction units, and the second one takes up two of them, while other take up one each.

## Advanced responsiveness
However,the example above doesn't give us the resposiveness we want,as this grid will always be three columns wide. We want our grid to vary the amount of columns with the width of the container.
### repeat()
we'll  go with ```repeat()``` function.This is a more powerful way of specifing you columns and rows.
```
.container{
    display:grid;
    grid-template-columns:repeat(3,100px);
    grid-template-rows:repeat(2,50px);
}
```
In other words ```repeat(3,100px)``` is identical to ```100px 100px 100px```.
first parameter specifies how many columns you want,an the second specifies their width.
### auto-fit
Let's skip having a fixed amount of columns, and rather replace 3 with ```auto-fit```.
```
.container{
    display:grid;
    grid-gap:5px;
    grid-template-columns:repeat(auto-fit,100px);
    grid-template-rows:repeat(2,50px);
}
```
The grid now varies the amount of columns with the width of the container.
*It simply tries to fit as many 100px wide columns into the container as possible.*
### minmax()
However,if we hard code all columns to be exactly 100px, we'll never get the flexibility we want,as they'll rarely add up to the full width.The final ingredient we need in order to fix this called ```minmax()```.we'll simply replace 100px with ```minmax(100px,1fr)```.Here's the final CSS.
```
.container{
    display:grid;
    grid-gap:5px;
    ** grid-template-columns:repeat(auto-fit,minmax(100px,1fr)); **
    grid-template-rows:repeat(2,100px);
}
```
*Notice that all the responsiveness happens in a single line of CSS.*
And as you can see that works perfectly.The ```minmax()```function defines a size range greater than or equal to **min** and less than or equal to max.
