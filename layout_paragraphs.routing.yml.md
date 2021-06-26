* The permission machine name is `administer nodes` not `administer content`. However,
* I believe that the permission on many of these routes should either:
  * use a new permission,
  * not use a permission and rely on field access,
  * or use a permission from paragraphs.permissions.yml such as `administer paragraphs settings`
    or `edit behavior plugin settings`.
* `layout_paragraphs.builder.choose_component`
  * Related to the above:
    * I set up a Layout Paragraphs field on the out-of-the-box Article content type
    * I created a user with the OOTB "Authenticated" role.
    * I added the `create article content` permission to the `authenticated` user role.
    * I logged in as the newly created user.
    * I visited `/node/add/article`
    * I was unable to add paragraphs content.
      * The network inspection tab revealed that the AJAX request was receiving a `403` response.
      * I believe this is because I did not add the `administer content` permission to the `authenticated` user role.
  * Nit: I would prefer a query string over URL path parts since this is kinda like passing parameters to a function.
    Path parts are good for when the response is really a conceptually distinct resource like `/node/{node}`.
* `layout_paragraphs.builder.*`
  * All of these use the `administer content` permission.
  * I think I would refactor the URLs to: `/node/{node}/edit/layout_paragraphs/{field_name}/{layout_operation}?parent_type={param}&parent={param}&region={param}`
    * This would allow the controller to rely on field access to protect itself.
    * Note: another route for `/node/add/layout_paragraphs/{field_name}/{layout_operation}` would be required, but it
      could reuse the same controller.
  * Alternatively, (and I'm not even sure if it *is* actually different), I would make a route for the modeal
