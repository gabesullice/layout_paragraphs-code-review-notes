* `::build()`
  * Consider using `FALSE` or `NULL` instead of empty strings for argument defaults. Or
  * Use `empty()` for the conditions.
  * `$build['controls']['#edit_url']`
    * This is a great use of [Hypermedia as the Engine of Application State](https://en.wikipedia.org/wiki/HATEOAS)!!
  * `$build['controls']['#dialog_options']`
    * Is `Drupal.settings` infeasible because of AJAX?
  * `return $component_menu;`
    * This might need a `#cache` on it. Technically it doesn't because the route defines `_admin_route: TRUE`
      (but I'm not sure that it should).
      * Could use `max-age=0` to disable caching.
