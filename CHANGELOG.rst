Change Log
==========

All notable changes to this project will be documented in this file.
This project adheres to `Semantic Versioning`_ starting with version 0.11.0.

..
    You should **NOT** be adding new change log entries to this file, this
    file is managed by ``towncrier``.
    You **may** edit previous change logs to fix problems like typo corrections or such.
    You can find more information on how to add a new change log entry at
    https://github.com/RasaHQ/rasa-sdk/tree/master/changelog/ .

.. towncrier release notes start

[1.9.0] - 2020-03-24
^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- `#110 <https://github.com/rasahq/rasa/issues/110>`_: Exit program (``python -m rasa_sdk --actions actions`` or
  ``rasa run actions --actions actions``) if a requested module under the
  ``--actions`` command-line option cannot be found.


[1.8.1] - 2020-03-09
^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- `#153 <https://github.com/rasahq/rasa/issues/153>`_: Make it possible to use the ``requests`` library inside the default Rasa SDK container.


[1.8.0] - 2020-02-26
^^^^^^^^^^^^^^^^^^^^

Improvements
------------
- `#130 <https://github.com/rasahq/rasa/issues/130>`_: Copied over instance methods ``last_executed_action_has()``, ``get_last_event_for()`` and
    ``applied_events`` from the Rasa ``DialogueStateTracker`` class to the SDK ``Tracker`` class.
- `#145 <https://github.com/rasahq/rasa/issues/145>`_: Add ``poetry`` for dependency management and reduce the size of Docker image.

Miscellaneous internal changes
------------------------------
- #148, #149


[1.7.0] - 2020-01-29
^^^^^^^^^^^^^^^^^^^^

Improvements
------------
- ``ReminderScheduled`` and ``ReminderCancelled`` now take ``intent`` and ``entities``
  as options, instead of ``action``. This is because starting with Rasa 1.7 reminders
  trigger intents (with entities) instead of actions.
- The following ``FormAction`` methods are now ``async`` by default: ``validate_slots``,
  ``validate``, ``submit`` and ``run``. User-defined classes inheriting from
  ``FormAction`` should be adapted to use ``async`` for these methods. Existing
  synchronous implementations will continue to work as normal, but this behaviour will
  be deprecated in the future.
- The following ``ActionQueryKnowledgeBase`` methods are now ``async``:
  ``utter_objects`` and ``run``.
- The following ``KnowledgeBase`` methods are now ``async``:
  ``get_attributes_of_object``, ``get_key_attribute_of_object``,
  ``get_representation_function_of_object``, ``get_objects`` and ``get_object``. Same
  warning for ``FormAction`` applies here - user-defined classes should be updated to
  use ``async``, but will continue to work for the moment.
- The following ``InMemoryKnowledgeBase`` methods are now ``async``:
  ``get_attributes_of_object``, ``get_objects`` and ``get_object``.

[1.6.1] - 2020-01-07
^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- Pinned ``sanic~=19.9.0`` to fix breaking changes introduced in sanic 19.9.12.


[1.6.0] - 2019-12-18
^^^^^^^^^^^^^^^^^^^^

Features
--------
- Added ``SessionStarted`` event for compatibility with conversation sessions in Rasa
  1.6.0.


[1.5.2] - 2019-12-11
^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- Pinned ``multidict`` dependency to 4.6.1 to prevent sanic from breaking,
  see https://github.com/huge-success/sanic/issues/1729

[1.5.1] - 2019-11-27
^^^^^^^^^^^^^^^^^^^^

Features
--------
- Added ``LOG_LEVEL_LIBRARIES`` environment variable to set log level of libraries, such as ``sanic``

Improvements
------------
- ``DeprecationWarning``s are now ``FutureWarning``s, as they should be seen
  by end users
- ``text`` is now the first positional argument in ``utter_message`` instead of
  ``image``

Bugfixes
--------
- The deprecated ``utter_elements`` now correctly uses ``utter_message``

[1.5.0] - 2019-11-22
^^^^^^^^^^^^^^^^^^^^

Features
--------
- Add support for multiple sanic workers (configurable with the
  ``ACTION_SERVER_SANIC_WORKERS`` environment variable).
- Add support for async ``run`` methods in the ``Action`` class.
- Return status code ``404`` in case requested action was not found.
- Return status code ``400`` in case an empty request body was sent to the ``/webhook``
  endpoint.

Improvements
------------
- Replace ``flask`` server framework with ``sanic``.
- Replace ``flask_cors`` with ``sanic-cors``.
- ``CollectingDispatcher.utter_message`` can now do anything that other dispatcher
  methods can do.
- The ``CollectingDispatcher`` methods ``utter_custom_message``, ``utter_elements``,
  ``utter_button_message``, ``utter_attachment``, ``utter_button_template``,
  ``utter_template``, ``utter_custom_json`` and ``utter_image_url`` were deprecated in
  favor of ``utter_message``.
- Updated format strings to f-strings where appropriate.

Deprecations and Removals
-------------------------
- Remove ``requests`` dependency
- Remove ``gevent`` dependency

[1.4.0] - 2019-10-19
^^^^^^^^^^^^^^^^^^^^

Features
--------
- Added Python 3.7 support.

Deprecations and Removals
-------------------------
- Removed Python 2.7 support.
- Removed Python 3.5 support.


[1.3.3] - 2019-09-28
^^^^^^^^^^^^^^^^^^^^

Features
--------
- SSL support, certificates can be passed with --ssl-certificate and --ssl-keyfile


[1.3.2] - 2019-09-06
^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- fixed TypeError on ``request_next_slot`` method of ``FormAction`` class

[1.3.1] - 2019-09-05
^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- undid Removed unused ``tracker`` argument from ``utter_template`` and ``utter_button_template``
  methods as it resulted in compatibility issues

[1.3.0] - 2019-09-05
^^^^^^^^^^^^^^^^^^^^

Compatibility release for Rasa 1.3.0.

Features
--------
- add ``InMemoryKnowledgeBase`` implementation as a default ``KnowledgeBase``
- add ``ActionQueryKnowledgeBase`` as a default action to interact with a knowledge base

Improvements
------------
- Removed unused ``tracker`` argument from ``utter_template`` and ``utter_button_template``
  methods

[1.2.0] - 2019-08-13
^^^^^^^^^^^^^^^^^^^^

Compatibility release for Rasa 1.2.0. There have not been any
additional changes.

[1.1.1] - 2019-07-25
^^^^^^^^^^^^^^^^^^^^

Features
--------
- ``dispatcher.utter_image_url()`` to dispatch images from custom actions

Bugfixes
--------
- correct slots print in debug mode before submitting a form

[1.1.0] - 2019-06-13
^^^^^^^^^^^^^^^^^^^^

Compatibility release for Rasa 1.1.0. There have not been any
additional changes.

[1.0.0] - 2019-05-21
^^^^^^^^^^^^^^^^^^^^

Features
--------
- validate events returned from action - checks for sanity
- endpoint to retrieve all registered actions at ``/actions``

Improvements
------------
- package renamed from ``rasa_core_sdk`` to ``rasa_sdk`` - please make sure to
  update your imports accordingly

[0.14.0] - 2019-04-26
^^^^^^^^^^^^^^^^^^^^^

Compatibility release for Rasa Core 0.14.0. There have not been any
additional changes when compared to ``0.13.1``.

[0.13.1] - 2019-04-16
^^^^^^^^^^^^^^^^^^^^^

Features
--------
- add formatter 'black'
- Slots filled before the start of a form are now validated upon form start
- In debug mode, the values of required slots for a form are now printed
  before submitting

Improvements
------------
- validate_{} functions for slots now return dictionaries of form {slot: value}
  instead of value

Bugfixes
--------
- Slots extracted from entities in user input upon calling form activation are
  now correctly validated

[0.13.0] - 2019-03-26
^^^^^^^^^^^^^^^^^^^^^

Features
--------
- Abstract Actions can now be subclassed
- add warning in case of mismatched version of rasa_core and rasa_core_sdk
- ``FormAction.from_trigger_intent`` allows slot extraction from message
  triggering the FormAction
- ``Tracker.active_form`` now includes ``trigger_message`` attribute to allow
  access to message triggering the form

[0.12.2] - 2019-02-17
^^^^^^^^^^^^^^^^^^^^^

Features
--------
- add optional `validate_{slot}` methods to `FormAction`
- forms can now be deactivated during the validation function by returning
  `self.deactivate()`
- Function to get latest input channel from the tracker with
  ``tracker.get_latest_input_channel()``

Improvements
------------
- ``self._deactivate()`` method from the ``FormAction`` class has been
  renamed to ``self.deactivate()``
- changed endpoint function so that it is now accessible with Python as well

[0.12.1] - 2018-11-11
^^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- doc formatting preventing successful rasa core travis build

[0.12.0] - 2018-11-11
^^^^^^^^^^^^^^^^^^^^^

Features
--------
- added Dockerfile for rasa_core_sdk
- add ``active_form`` and ``latest_action_name`` properties to ``Tracker``
- add ``FormAction.slot_mapping()`` method to specify the mapping between
  user input and requested slot in the form
- add helper methods ``FormAction.from_entity(...)``,
  ``FormAction.from_intent(...)`` and ``FormAction.from_text(...)``
- add ``FormAction.validate(...)`` method to validate user input
- add warning in case of mismatched version of rasa_core and rasa_core_sdk

Improvements
------------

- ``FormAction`` class was completely refactored
- ``required_fields()`` is changed to ``required_slots(tracker)``
- moved ``FormAction.get_other_slots(...)`` functionality to
  ``FormAction.extract_other_slots(...)``
- moved ``FormAction.get_requested_slot(...)`` functionality to
  ``FormAction.extract_requested_slot(...)``
- logic of requesting next slot can be customized in
  ``FormAction.request_next_slot(...)`` method

Deprecations and Removals
-------------------------

- ``FormField`` class and its subclasses

Bugfixes
--------

[0.11.5] - 2018-09-24
^^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- current state call in tracker

[0.11.4] - 2018-09-17
^^^^^^^^^^^^^^^^^^^^^

Bugfixes
--------
- wrong event name for the ``AgentUttered`` event - due to the wrong name,
  rasa core would deserialise the wrong event.


.. _`master`: https://github.com/RasaHQ/rasa_core/

.. _`Semantic Versioning`: http://semver.org/
