Input field types
=================

There are four values for the ``type`` keyword which have an input field:

1. ``string`` - For text, email, date, file, and other inputs.
2. ``number`` - For number input (including floats).
3. ``integer`` - For integer only number input.
4. ``boolean`` - For ``True`` - ``False`` inputs (checkbox by default).

We've excluded ``array`` and ``object`` types as they can't have input fields.


.. _inputs for string type:

Inputs for ``string`` type
--------------------------

The input fields for ``string`` values can be customized using the ``format``
and ``widget`` keywords.

Possible values for ``format`` keyword are:

============ ===========
Format       Description
============ ===========
``color``    A colour input
``date``     A date input
``email``    An email input
``password`` A password input
``range``    A range input
``time``     A time input
``data-url`` A file input. See :ref:`File inputs` for details.
``file-url`` A file input. See :ref:`File inputs` for details.
============ ===========

Possible values for ``widget`` keyword are:

============ ===========
Widget       Description
============ ===========
``textarea`` A textarea input
============ ===========


Examples:

.. code-block:: python

    # 1. Text input (default)
    {
        'type': 'string'
    }

    
    # 2. Date input
    {
        'type': 'string',
        'format': 'date'
    }


    # 3. Email input
    {
        'type': 'string',
        'format': 'email'
    }

    # 4. Textarea input
    {
        'type': 'string',
        'widget': 'textarea'
    }

    # ...

File inputs
~~~~~~~~~~~

There are two ``format`` values for file uploads: 

1. ``data-url`` - for embedding base64 encoded data in the JSON object.
2. ``file-url`` - for keeping only the link to the file in JSON object.

Read :doc:`Uploading files <upload>` document for a full guide on uploading files.

.. note::
    
    Do not use ``file`` format for file inputs. This won't work as you may expect.


Inputs for ``number`` and ``integer`` types
-------------------------------------------

The ``number`` and ``integer`` types get an HTML ``number`` input field.

They are not customizable.


Inputs for ``boolean`` type
---------------------------

The ``boolean`` type gets an HTML ``checkbox`` input. Currently, it can't be 
customized to another input type.

However, you can use :doc:`choices <choices>` to display a ``radio`` or ``select``
input with *Yes/No* options to choose from.


Default values
--------------

.. versionadded:: 2.6.0

You can specify default initial values for inputs using the ``default`` keyword:

.. code-block:: python

    # 1. String input
    {
        'type': 'string',
        'default': 'Hello world'
    }

    # 2. Boolean
    {
        'type': 'boolean',
        'default': True
    }

    # 3. Default choice
    {
        'type': 'string',
        'choices': ['Eggs', 'Juice', 'Milk'],
        'default': 'Milk'
    }

    # 4. Default array items
    {
        'type': 'array',
        'items': {
            'type': 'string',
            'default': 'Hello world' # default value for every new array item
        }
    }


Readonly inputs
---------------

.. versionadded:: 2.6.0

You can make inputs uneditable using a ``readonly`` (alias ``readOnly``) keyword:

.. code-block:: python

    # 1. String inputs
    {
        'type': 'string',
        'readonly': True
    }

    # 2. Array items
    {
        'type': 'array',
        'items': {
            'type': 'string',
            'readonly': True # all items will be readonly
        }
    }