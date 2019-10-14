#Filter Duplicate Posts in the Loop


###Loop no.1

```
<?php
$do_not_duplicate = array(); // set befor loop variable as array

// 1. Loop
query_posts('ca=1,2,3&showposts=5');
while ( have_posts() ) : the_post();
    $do_not_duplicate[] = $post->ID; // remember ID's in loop
    // display post ...
    the_title();
endwhile;
?>
```

###Loop no.2

```
<?php
// 2. Loop
query_posts( 'cat=4,5,6&showposts=15' );
while (have_posts()) : the_post();
    if ( !in_array( $post->ID, $do_not_duplicate ) ) { // check IDs         
// display posts ...
        the_title();
    }
endwhile;
?>
```

###Loop no.3

```
<?php
// another loop without duplicates
query_posts( array(
    'cat' => 456,
    'post__not_in' => $do_not_duplicate
    )
);
while ( have_posts() ) : the_post();
    // display posts...
        the_title();
endwhile;
?>
```