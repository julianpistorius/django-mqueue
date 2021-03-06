Registered models
=================

.. highlight:: python

Models can be registered. They will be automatically monitored.

Autoregister a model
^^^^^^^^^^^^^^^^^^^^

In ``settings.py``:

::

   MQUEUE_AUTOREGISTER = (
   	#('app.module.model', registration level: 1=create+delete, 2=1+save),
   	('django.contrib.auth.models.User', 1),
   	('pages.models.Page', 2),
   	('contact.models.Message', 1),
   	)

The registered models will be monitored according to the chosen monitoring level.

Manualy register a model
^^^^^^^^^^^^^^^^^^^^^^^^

In any installed app ``apps.py`` :

::

   from django.apps import AppConfig
   
   class MyappConfig(AppConfig):
       name = "myapp"
       verbose_name = "My app"
       
       def ready(self):
           from mqueue.tracking import mqueue_tracker
           from myapp.models import TheModel
    
           mqueue_tracker.register(TheModel)


By default this will set the model to monitoring level 1 (records create
and delete). Set it to 2 if you want to record also every save on the
model:

::

   mqueue_tracker.register(TheModel, 2)



