.. _addressBooks_api:

============
addressBooks
============

The address books API, also including the :doc:`contacts` and :doc:`mailingLists` namespaces, first appeared in Thunderbird 64.

The `Address Books`__ sample extension uses this API.

__ https://github.com/thundernest/sample-extensions/tree/master/addressBooks

.. role:: permission

.. rst-class:: api-main-section

Permissions
===========

.. api-member::
   :name: :permission:`addressBooks`

   Read and modify your address books and contacts

.. rst-class:: api-permission-info

.. note::

   The permission :permission:`addressBooks` is required to use ``addressBooks``.

.. rst-class:: api-main-section

Functions
=========

.. _addressBooks.openUI:

openUI()
--------

.. api-section-annotation-hack:: 

Opens the address book user interface.

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.closeUI:

closeUI()
---------

.. api-section-annotation-hack:: 

Closes the address book user interface.

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.list:

list([complete])
----------------

.. api-section-annotation-hack:: 

Gets a list of the user's address books, optionally including all contacts and mailing lists.

.. api-header::
   :label: Changes in Thunderbird 85

   
   .. api-member::
      :name: Read-only address books are now returned as well as read-write books.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: [``complete``]
      :type: (boolean)
      
      If set to true, results will include contacts and mailing lists for each address book.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: array of :ref:`addressBooks.AddressBookNode`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.get:

get(id, [complete])
-------------------

.. api-section-annotation-hack:: 

Gets a single address book, optionally including all contacts and mailing lists.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   
   
   .. api-member::
      :name: [``complete``]
      :type: (boolean)
      
      If set to true, results will include contacts and mailing lists for this address book.
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: :ref:`addressBooks.AddressBookNode`
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.create:

create(properties)
------------------

.. api-section-annotation-hack:: 

Creates a new, empty address book.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``properties``
      :type: (object)
      
      .. api-member::
         :name: ``name``
         :type: (string)
      
   

.. api-header::
   :label: Return type (`Promise`_)

   
   .. api-member::
      :type: string
      
      The id of the new address book.
   
   
   .. _Promise: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.update:

update(id, properties)
----------------------

.. api-section-annotation-hack:: 

Renames an address book.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   
   
   .. api-member::
      :name: ``properties``
      :type: (object)
      
      .. api-member::
         :name: ``name``
         :type: (string)
      
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.delete:

delete(id)
----------

.. api-section-annotation-hack:: 

Removes an address book, and all associated contacts and mailing lists.

.. api-header::
   :label: Parameters

   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. rst-class:: api-main-section

Events
======

.. _addressBooks.onCreated:

onCreated
---------

.. api-section-annotation-hack:: 

Fired when an address book is created.

.. api-header::
   :label: Parameters for onCreated.addListener(listener)

   
   .. api-member::
      :name: ``listener(node)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``node``
      :type: (:ref:`addressBooks.AddressBookNode`)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.onUpdated:

onUpdated
---------

.. api-section-annotation-hack:: 

Fired when an address book is renamed.

.. api-header::
   :label: Parameters for onUpdated.addListener(listener)

   
   .. api-member::
      :name: ``listener(node)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``node``
      :type: (:ref:`addressBooks.AddressBookNode`)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. _addressBooks.onDeleted:

onDeleted
---------

.. api-section-annotation-hack:: 

Fired when an addressBook is deleted.

.. api-header::
   :label: Parameters for onDeleted.addListener(listener)

   
   .. api-member::
      :name: ``listener(id)``
      
      A function that will be called when this event occurs.
   

.. api-header::
   :label: Parameters passed to the listener function

   
   .. api-member::
      :name: ``id``
      :type: (string)
   

.. api-header::
   :label: Required permissions

   - :permission:`addressBooks`

.. rst-class:: api-main-section

Types
=====

.. _addressBooks.AddressBookNode:

AddressBookNode
---------------

.. api-section-annotation-hack:: 

A node representing an address book.

.. api-header::
   :label: object

   
   .. api-member::
      :name: ``id``
      :type: (string)
      
      The unique identifier for the node. IDs are unique within the current profile, and they remain valid even after the program is restarted.
   
   
   .. api-member::
      :name: ``name``
      :type: (string)
   
   
   .. api-member::
      :name: ``type``
      :type: (:ref:`addressBooks.NodeType`)
      
      Always set to ``addressBook``.
   
   
   .. api-member::
      :name: [``contacts``]
      :type: (array of :ref:`contacts.ContactNode`)
      
      A list of contacts held by this node's address book or mailing list.
   
   
   .. api-member::
      :name: [``mailingLists``]
      :type: (array of :ref:`mailingLists.MailingListNode`)
      
      A list of mailingLists in this node's address book.
   
   
   .. api-member::
      :name: [``parentId``]
      :type: (string)
      
      The ``id`` of the parent object.
   
   
   .. api-member::
      :name: [``readOnly``]
      :type: (boolean)
      
      Indicates if the object is read-only.
   
   
   .. api-member::
      :name: [``remote``]
      :type: (boolean)
      :annotation: -- [Added in TB 91]
      
      Indicates if the address book is accessed via remote look-up.
   

.. _addressBooks.NodeType:

NodeType
--------

.. api-section-annotation-hack:: 

Indicates the type of a Node, which can be one of ``addressBook``, ``contact``, or ``mailingList``.

.. api-header::
   :label: `string`

   
   .. container:: api-member-node
   
      .. container:: api-member-description-only
         
         Supported values:
         
         .. api-member::
            :name: ``addressBook``
         
         .. api-member::
            :name: ``contact``
         
         .. api-member::
            :name: ``mailingList``
   
