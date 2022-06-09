uthash.h - A hash table for C structure
============================================

Overview
-----------

Any C structure can be stored in a hash table using uthash. Just add a `UT_hash_handle` to the structure and choose one or more fields in your structure to act as the key. Then use these macros to store, retrieve or delete items from the hash table.

- If key is integer, using `HASH_ADD_INT`
- If key is string， using `HASH_ADD_STR`
- If key is pointer , using `HASH_ADD_PTR`
- If key is another type, we can use `HASH_ADD`. (The macros above are all implemeted by `HASH_ADD`.)

Steps before using uthash
-----------------------------

Step 1. Include header
+++++++++++++++++++++++

.. code-block:: c

    #include "uthash.h"

Step 2. Define a structure with a pair of key-value 
++++++++++++++++++++++++++++++++++++++++++++++++++++

Note that the structure must have one `UT_hash_handle` member.

.. code-block:: c

    struct my_struct {
        int id;            /* we'll use this field as the key */
        char name[10];     /* value */
        UT_hash_handle hh; /* makes this structure hashable */
    };

Step 3. Define a pointer to a hash table. And it points to the NULL.
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: c
    
    struct myhash *users  = NULL;


Examples of using uthash
----------------------------

Here are the exmpales to show how to use uthash.

Example 1. Adding an item to a hash.
+++++++++++++++++++++++++++++++++++++

.. code-block:: c

    struct my_struct *users = NULL;

    void add_user(struct my_struct *s) {
        HASH_ADD_INT( users, id, s );
    }

Example 2. Looking up an item in a hash.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: c

    struct my_struct *find_user(int user_id) {
        struct my_struct *s;

        HASH_FIND_INT( users, &user_id, s );
        return s;
    }


Example 3. Deleting an item from a hash.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: c

    void delete_user(struct my_struct *user) {
        HASH_DEL( users, user );
    }

Example 4. Counting the items
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: c

    int count_user(struct my_struct *user){
        HASH_COUNT( users );
    }

Example 5. Sorting the hash table
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: c

    int name_sort(struct my_struct *a, struct my_struct *b)
    {
        return strcmp(a->name,b->name);
    }

    int id_sort(struct my_struct *a, struct my_struct *b)
    {
        return (a->id - b->id);
    }

    void sort_by_name(struct my_struct *head)
    {
        HASH_SORT(*head, name_sort);
    }

    void sort_by_id(struct my_struct *head)
    {
        HASH_SORT(*head, id_sort);
    }

Example 6. Traverse the hash table
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: c

    void print_user_iterator(struct my_struct head)
    {
        struct my_struct *s, *tmp;

        HASH_ITER(hh, head, s, tmp)
        {
            printf("user id %d: name %s\n", s->id, s->name);
            /* ... it is safe to delete and free s here */
        }
    }

Reference
-----------

- https://troydhanson.github.io/uthash/
- https://www.796t.com/content/1588597565.html