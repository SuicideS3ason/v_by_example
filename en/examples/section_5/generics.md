# Generics

The concept of generics makes it possible to create more abstract code.
One could define a [`struct`](../struct/struct.md), [`function`](../functions/functions.md) or [`method`](../methods/methods.md) with a generic type parameter `T` and the specification of that type will be deffered when declaring or instantiating the implementation.
This is an example taken from the official V documentation (it will be explained after):

```v
struct Repo<T> {
    db DB
}

// new_repo<T>() creates a new Repo for type T
fn new_repo<T>(db DB) Repo<T> {
    return Repo<T>{ db: db }
}

// find_by_id(id int) finds a Repo given its ID and returns it.
// Since the return type is Option error could be returned, too.
fn (r Repo<T>) find_by_id(id int) ?T {
    table_name := T.name
    return r.db.query_one<T>('select * from ${table_name} where id = ?', id)
}

```
