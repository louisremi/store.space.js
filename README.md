store.space.js
==============

a [store.js](https://github.com/marcuswestin/store.js) plugin bringing namespaces to localStorage, in half a kB.

Why do I need it?
------------------------

For the same reasons that you shouldn't pollute the global scope with global Javascript variables,
you should pay attention to localStorage pollution.  
Yes, you could put all of your data in an object and use a single item to store it in it's JSON form.
But if you do so, updating your object will soon become a complicated and ressource expensive task:

1. the item has to be retrieved from the localStorage
2. then parsed from a JSON string to an object
3. a property of the object can be updated
4. the object is turned back to a string
5. the item is stored to the localStorage

Here is what hapens with a namespaced store:

1. the object is turned to a string
2. the item is stored to the localStorage

It is however more expensive to:

- store an item with a new key for the first time
- remove an item from localStorage

Both operations require to write to a specific item that acts as an index for all items of the namespace.

Usage
-----

	// create a namespaced store or reuse an existing one
	myStore = store.space('my');
	
	// use the namespaced store just like a normal store
	myStore.set('key', 'value');
	myStore.set('key');

You can create/update items sharing the same key in different namespaces and `clear()` a namespace without loosing other items.

	store1 = store.space('_1_');
	store2 = store.space('_2_');
	
	store1.set('key', 'value1');
	store2.set('key', 'value2');
	
	store1.get('key') === 'value1';
	
	store1.clear();
	store2.get('key') === 'value2';