Schema guide
============

django-jsonform currently implements a custom JSON Schema spec written specifically
for Django.

You should also read the standard spec at
`https://json-schema.org <https://json-schema.org/learn/getting-started-step-by-step>`_.

At present, certain features from the standard spec are not supported by
django-jsonform. However, we've also implemented a few extra features which are
not in the standard spec.

For some complex schema examples, see :doc:`Examples page <examples>`.


Types
-----

Currently, only these six types are supported:

.. contents::
    :depth: 1
    :local:
    :backlinks: none


``array`` (alias ``list``)
~~~~~~~~~~~~~~~~~~~~~~~~~~

A JSON array (similar to Python list).

Keywords:

- ``items`` (**required**) - Specifies the type of items allowed in the list.
- ``minItems`` (alias ``min_items``) - Limit the minimum number of items in a list.
- ``maxItems`` (alias ``max_items``) - Limit the maximum number of items in a list.
- ``title`` - Specify a title for the list.

This example shows a schema of a list containing string items:

.. code-block:: python

    # Schema
    {
        'type': 'list', # or 'array'
        'items': {
            'type': 'string'
        },
        'min_items': 1,
        'max_items': 5
    }


    # Output data
    ['one', 'two', 'three', ...]


``object`` (alias ``dict``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

A JSON object (similar to Python dict).

Keywords:

- ``properties`` (alias ``keys``; **required**) - Specifies the keys (or fields)
  in a dict/object.
- ``additionalProperties`` - Allow users to add extra keys not delclared in the
  schema.
- ``title`` - Specify a title for the dict.

This example shows a schema of a basic dict:

.. code-block:: python

    # Schema
    {
        'type': 'dict': # or 'object'
        'keys': { # or 'properties'
            'name': {
                'type': 'string'
            },
            'email': {
                'type': 'string'
            },
            'age': {
                'type': 'number',
                'title': 'Age in years'
            }
        }
    }


    # Output data
    {
        'name': 'John Doe',
        'email': 'john@example.com',
        'age': 99
    }


Additional keys
^^^^^^^^^^^^^^^

By default, an object's data can only contain keys declared in the schema.
But you can allow users to add extra keys using the ``additionalProperties``
key:

.. code-block:: python

    # Schema
    {
        'type': 'dict': # or 'object'
        'keys': { # or 'properties'
            'name': {
                'type': 'string'
            },
        },
        'additionalProperties': True
    }


    # Output data
    {
        'name': 'John Doe', # declared in the schema
        'gender': 'Male', # added by the user
    }

The keys added by the user will only be of ``string`` type.


``string``
~~~~~~~~~~

A string.

This can't be at the top level of the schema. If you only want to save
a string, you should use Django's ``CharField``.

Keywords:

- ``title`` - Specify the label for the input field.
- ``choices`` - Specify choices for the field. A ``select`` input will be rendered.
  See the :doc:`document on Choices <guide/choices>` for details.
- ``format`` - Use this to specify the input field type. See :ref:`inputs for string type`
  for more.
- ``widget`` - Use this to specify the input field type. Only use this with ``choices``
  keyword. For other cases, prefer the ``format`` keyword.


``number``
~~~~~~~~~~

A number (including floats).

This can't be at the top level of the schema. If you only want to save a number,
you should use Django's ``FloatField``.

Keywords:

- ``title`` - Specify the label for the input field.
- ``choices`` - Specify choices for the field. A ``select`` input will be rendered.
  See the :doc:`document on Choices <guide/choices>` for details.

It gets a ``number`` HTML input by default. It can't be overriden.


``integer``
~~~~~~~~~~~

An integer.

This can't be at the top level of the schema. If you only want to save an integer,
you should use Django's ``IntegerField``.

Keywords:

- ``title`` - Specify the label for the input field.
- ``choices`` - Specify choices for the field. A ``select`` input will be rendered.
  See the :doc:`document on Choices <guide/choices>` for details.

It gets a ``number`` HTML input by default. It can't be overriden.


``boolean``
~~~~~~~~~~~

A boolean.

This can't be at the top level of the schema. If you only want to save an boolean,
you should use Django's ``BooleanField``.

Keywords:

- ``title`` - Specify the label for the input field.

It gets a ``checkbox`` HTML input by default. It can't be overriden.


Unsupported features
--------------------

Recursion and validation are the two major features which are not supported at
present.
