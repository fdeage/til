# SASS: mixins vs placeholders


## Mixins

`.scss` file:  

```
@mixin button($text, $background) {
  background: $background;		//variable
  border-radius: 10px;
  color: $text;				   //variable
  padding: 0 15px;
  text-decoration: none;
  text-transform: uppercase;
}

.active-button {
  @include button($green-mid, $green-light);
}

.inactive-button {
  @include button($grey-light, $green-dark);
}
```

After compilation:  

```
.active-button {
  border-radius: 10px;
  background: #637a3d;
  color: #c0d0aa
  padding: 0 15px;
  text-decoration: none;
  text-transform: uppercase;
}

.inactive-button {
  border-radius: 10px;
  background: #3f5526;
  color: #f9f9f9;
  padding: 0 15px;
  text-decoration: none;
  text-transform: uppercase;
}
```

-> useless repetitions in the compiled code.


## Placeholders

`.scss` file:  

```
%hide {
  height: 0;
  margin: 0;
  overflow: hidden;
  padding: 0;
}

.site-title {
  @extend %hide;
}

.skip-link {
  @extend %hide;
}
```

After compilation:  

```
.site-title,
.skip-link {
  height: 0;
  margin: 0;
  overflow: hidden;
  padding: 0;
}
```
