# Cheatsheet

A documentation of useful tricks, formulas, and other helpers for efficiency, consistency and out-right speed.

---

## Loops

### Stagger loop
**$n:** = intiger; Set the count of loops you want to complete

**$x:** = intiger; prints the loop count

```
$n: 5;

@for $x from 2 through $n {
	&:nth-child( #{ $x } ) {
		animation-delay: $x * 100ms;

		@content
	}
}
```

### Stagger loop - reverse

```
@for $x from 1 through ( $n - 1 ) {
	&:nth-child( #{ $x } ) {
		animation-delay: ( $n - $x ) * 120ms;
	}
}
```

Notice two things. First, we're beginning the loop from the second element whether its from the start or finish. In the reverse version we still count one less than `$n` but we want to start from the end, `$n - 1`, in our case, '4' then run the loop in reverse `( $n - $x )`. Beginning at the second element improves the experience in our animations. Finally, don't forget to use interpolation to append the loop count to the class.
