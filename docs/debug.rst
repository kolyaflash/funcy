Debugging
=========

.. function:: tap(value)

    Prints value and then returns it. Useful to tap into some functional pipeline for debugging::

        fields = (f for f in fields_for(category) if section in tap(tap(f).sections))
        # ... do something with fields


.. decorator:: log_calls(print_func, errors=True)
               print_calls

    Will log or print all function calls, including arguments, results and raised exceptions. Can be used as decorator or tapped into call expression::

        sorted_fields = sorted(fields, key=print_calls(lambda f: f.order))

    If ``errors`` is set to ``False`` then exceptions are not logged. This could be used to separate channels for normal and error logging::

        @log_calls(log.info, errors=False)
        @log_errors(log.exception)
        def some_suspicious_function(...):
            # ...

    :func:`print_calls` always prints everything.


.. decorator:: log_errors(print_func)
               print_errors

    Will log or print all function errors providing function arguments causing them.

    Can be combined with :func:`silent` or :func:`ignore` to trace occasionally misbehaving function::

        @silent
        @log_errors(logging.warning)
        def guess_user_id(username):
            initial = first_guess(username)
            # ...


.. decorator:: log_durations(print_func)
               print_durations

    Will time each function call and log or print its duration.
