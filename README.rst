Django appsettings
==================

finally, a unified system for pluggable apps to have configurable settings.
the django-appsettings app provides a clean api for keeping track of settings,
and, most importantly, having settings that are configurable for a user that
does not have write access to your server :) appsettings also provides an
interface (similar to the admin interface for models) for editing these
settings.

Todo
----

- unittests
- the web interface; hopefully with customizeable templates

Usage
=====

So you want to use this in your app? Well, just create a settings.py for your
app (which will be autodiscovered by _appsettings_) and register your
settings. Example::

    import appsettings
    from appsettings import values
    register = appsettings.register('mymodule')

    # settings are organized into groups.
    # this will define settings
    # mymodule.story.greeting, 
    # mymodule.story.pigs,
    # etc.
    @register
    class Story:
        # int, string, and float types are auto-discovered.
        greeting = "hello"
        pigs = 3
        wolves = 1
        # or you can specify the type
        houses = valuse.IntValue(3, doc = "number of houses in which to hide")
        myhouse = values.ChoiceValue(['straw','sticks','bricks'], 'straw')

using the settings in the rest of your app couldn't be easier::

    from appsettings import settings.mymodule as settings

    def run_away():
        return "%s pigs are running into a house made of %s"
                        %(settings.story.pigs, settings.story.myhouse)

more thorough documentation (hopefully sphinx-pretty API docs) to come shortly.