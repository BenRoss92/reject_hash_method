# `.reject`

## What is `.reject?`

* Part of the **Hash Class**
* Returns a copy of original hash
* Inside copy, deletes **every** key-value pair when block passed in equals **true**

## Selecting items by keys:

##### Example:

```
hash = {'Bank'=>1,'Aldgate'=>2,'Hammersmith'=>3,'Morden'=>2 }
hash.reject { |k| k == 'Morden' } # => {"Bank"=>1, "Aldgate"=>2, "Hammersmith"=>3}
hash = {'Bank'=>1,'Aldgate'=>2,'Hammersmith'=>3,'Morden'=>2 }
```
* Creates a copy of original `hash`
* Original `hash` kept the same

#### How can we utilise this new hash?

1. Can assign new hash to a variable, e.g. `new_hash`:

##### Example:

```
new_hash = hash.reject { |k| k == 'Morden' } # => {"Bank"=>1, "Aldgate"=>2, "Hammersmith"=>3}
```

2. Use `.reject!` to alter original, e.g.:

##### Example:

```
hash = {'Bank'=>1,'Aldgate'=>2,'Hammersmith'=>3,'Morden'=>2 }
hash.reject! { |k| k == 'Morden' }
hash # => {"Bank"=>1, "Aldgate"=>2, "Hammersmith"=>3}
```

* Original `hash` has now been altered - **be careful as deletions will be permanent!**
* _Tip: If no changes are made to hash, returns_ `nil`
  * `.delete_if` **won't** return `nil` if no changes are made

### Selecting items by values:

* Must specify 2 arguments inside pipes (i.e. `|key, value|`)
  * If only specifies value argument - e.g. `{ |v| v == 3 }`, will look for key value instead.

##### Example:

```
hash = {'Bank'=>1,'Aldgate'=>2,'Hammersmith'=>3,'Morden'=>2 }
new_hash = hash.reject { |k,v| v == 1 } # => {"Aldgate"=>2, "Hammersmith"=>3, "Morden"=>2}
```

* `'Bank'` and `1` key-pair are deleted from hash
* Other comparison operators can be used inside the block, e.g. `>=` and `!=`

## What about common keys/values?

* `.reject` removes **any** common key-pairs (not just 1)

##### Example:

```
hash = {'Bank'=>1,'Aldgate'=>2,'Hammersmith'=>3,'Morden'=>2 }
```

2 is a common value in our hash - both the `Bank` and `Morden`
keys have them, so they will be deleted:

```
new_hash = hash.reject { |k,v| v == 2 } # => {"Bank"=>1, "Hammersmith"=>3}
```

* Removes any key-value pairs with values equalling 2

## Some 'good-to-knows':

* Similar to `.delete_if`, but nicer :D (can't delete things by accident!)
  * `.delete_if` does **not** make a copy
* If block is not provided, returns an Enumerator - can then use Enumerator
methods on hash
  * Allows you to then chain Enumerators together - e.g.
`hash.map.with_index...`
* `.delete` will remove specified key from hash and return deleted value,
**not** the altered hash

## Donts:

* Putting values on their own in the block has no effect:

```
new_hash = hash.reject { |v| v == 2 } # => {'Bank'=>1,'Aldgate'=>2,'Hammersmith'=>3,'Morden'=>2 }
# returns same original hash
```

## Other Examples:

* Could find and delete all instances of a certain class:

```
hash = {(Object.new)=>:symbol,'string'=>7}
new_hash = hash.reject { |k,v| k.class == Object }
new_hash # => {"string"=>7}
```
