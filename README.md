# Cheatsheet

A documentation of useful tricks, formulas, and other helpers for efficiency, consistency and out-right speed.

---

## Concatenation
```
$foo: 'condensed';

.bar {
	$font: 'barlow-' + $foo; // 'barlow-condensed'
}
```
## Mixins
```
@mixin foo( $bar, $baz: false ) {
  color: $bar;
  @if baz {
    border-width: $baz;
  }
}

.qux {
  @include foo( #1e90ff, 2px );
}
```

#### Variable Arguments
```
// @see https://github.com/saucyrooster/cheatsheet#variable-arguments
@mixin bar( $baz... ) {
  box-shadow: $baz
}

.qux {
  $baz: 0 0 2px #333, 0 0 4px #666, 0 0 8px #999;
  @include bar( $baz );
}
```

## Control Directives

if, if else, else

**for loop**

```
// @see https://github.com/saucyrooster/cheatsheet#control-directives
$foo: bar;

.qux {
  @if $foo == bar {
     color: #000;
  } @else if $foo == baz {
    color: #fff;
   } @else {
     color: #999;
   }
}

.qux {
	color: if($foo == bar, #000, #999); // if([condition], [if true], [else])
}
```

or here's a doozy…

```
$foo: "foo";
$bar: "bar";
$qux: "qux";

@if ($foo == "foo" and not ($bar == "bar")) or ($qux == "qux") {
  // first condition is false, second condition is true
}
```
[]: # (This is a comment)
[]: # "And this is a comment"
[]: # 'Also this is a comment'
[//]: # (Yet another comment)
[comment]: # (Still another comment)
## Stagger loop
```
// @see https://github.com/saucyrooster/cheatsheet#stagger-loop
$n: 5; // $n = intiger - Sets the number of loops to complete

@for $x from 2 through $n {
	&:nth-child( #{ $x } ) {
		animation-delay: $x * 100ms; // $x = intiger - prints the loop count
	}
}
```

## Stagger loop - reverse
```
// @see https://github.com/saucyrooster/cheatsheet#stagger-loop---reverse
@for $x from 1 through ( $n - 1 ) {
	&:nth-child( #{ $x } ) {
		animation-delay: ( $n - $x ) * 120ms;
	}
}
```

Notice two things. First, we're beginning the loop from the second element whether its from the start or finish. In the reverse version we still count one less than `$n` but we want to start from the end, `$n - 1`, in our case, '4' then run the loop in reverse `( $n - $x )`. Beginning at the second element improves the experience in our animations. Finally, don't forget to use interpolation to append the loop count to the class.
