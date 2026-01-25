<!-- title: HMTL markup for navigation -->
There's been a lot of griping today about the use of an unordered list for a navigation menu (from @calevans among others). Although it is a generally accepted practice with the argument that a navigation menu is an unordered list of links, it's not too difficult to find an alternative that is just as efficient is it? What's the most basic code we could use as an alternative?

In html5 you could use the following: -

```html
<nav>
<a title="First link additional text" href="#">Link 1</a>
<a title="Second link additional text" href="#">Link 2</a>
<a title="Third link additional text" href="#">Link 3</a>
</nav>
```

with css to sort out positioning and look.

For some specific layouts you may want to specify a `:first-child` pseudo class or a `class="last"` on a link. 

For HTML4 strict just substitute a `<div class="menu">` for `<nav>`.

So, not as complicated as I once thought!
