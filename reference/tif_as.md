# Coerce Between tif Object Specifications

These functions convert between the various valid formats for corpus and
tokens objects. By using these in other packages, maintainers need to
only handle whichever specific format they would like to work with, but
gain the freedom to output (or convert into) the one most suited to
their package's paradigm.

## Usage

``` r
tif_as_corpus_character(corpus)

# Default S3 method
tif_as_corpus_character(corpus)

# S3 method for class 'character'
tif_as_corpus_character(corpus)

# S3 method for class 'data.frame'
tif_as_corpus_character(corpus)

tif_as_corpus_df(corpus)

# Default S3 method
tif_as_corpus_df(corpus)

# S3 method for class 'character'
tif_as_corpus_df(corpus)

# S3 method for class 'data.frame'
tif_as_corpus_df(corpus)

tif_as_tokens_df(tokens)

# Default S3 method
tif_as_tokens_df(tokens)

# S3 method for class 'list'
tif_as_tokens_df(tokens)

# S3 method for class 'data.frame'
tif_as_tokens_df(tokens)

tif_as_tokens_list(tokens)

# Default S3 method
tif_as_tokens_list(tokens)

# S3 method for class 'list'
tif_as_tokens_list(tokens)

# S3 method for class 'data.frame'
tif_as_tokens_list(tokens)
```

## Arguments

- corpus:

  valid tif corpus object to coerce

- tokens:

  valid tif tokens object to coerce

## Details

No explicit checking is done on the input; the output is guaranteed to
be valid only if the input is a valid format. In fact, we make an effort
to not modify an object that appears to be in the required format
already due to R's copy on modify semantics.

## Examples

``` r
# coerce corpus object
corpus <- c("Aujourd'hui, maman est morte.",
            "It was a pleasure to burn.",
            "All this happened, more or less.")
names(corpus) <- c("Camus", "Bradbury", "Vonnegut")

new <- tif_as_corpus_df(corpus)
new
#>     doc_id                             text
#> 1    Camus    Aujourd'hui, maman est morte.
#> 2 Bradbury       It was a pleasure to burn.
#> 3 Vonnegut All this happened, more or less.
tif_as_corpus_character(new)
#>                              Camus                           Bradbury 
#>    "Aujourd'hui, maman est morte."       "It was a pleasure to burn." 
#>                           Vonnegut 
#> "All this happened, more or less." 

# coerce tokens object
tokens <- list(doc1 = c("aujourd'hui", "maman", "est", "morte"),
               doc2 = c("it", "was", "a", "pleasure", "to", "burn"),
               doc3 = c("all", "this", "happened", "more", "or", "less"))

new <- tif_as_tokens_df(tokens)
new
#>    doc_id       token
#> 1    doc1 aujourd'hui
#> 2    doc1       maman
#> 3    doc1         est
#> 4    doc1       morte
#> 5    doc2          it
#> 6    doc2         was
#> 7    doc2           a
#> 8    doc2    pleasure
#> 9    doc2          to
#> 10   doc2        burn
#> 11   doc3         all
#> 12   doc3        this
#> 13   doc3    happened
#> 14   doc3        more
#> 15   doc3          or
#> 16   doc3        less
tif_as_tokens_list(new)
#> $doc1
#> [1] "aujourd'hui" "maman"       "est"         "morte"      
#> 
#> $doc2
#> [1] "it"       "was"      "a"        "pleasure" "to"       "burn"    
#> 
#> $doc3
#> [1] "all"      "this"     "happened" "more"     "or"       "less"    
#> 
```
